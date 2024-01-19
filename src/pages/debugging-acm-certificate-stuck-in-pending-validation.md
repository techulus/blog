---
template: post
title: "Debugging ACM certificate stuck in 'Pending validation'"
date_published: 1666654043000
# cover: /cover/acm.jpeg
---

>***TL;DR*** *My domain had a CNAME record pointing to Vercel, which had a CAA recording that prevented AWS from issuing certificates. The fix was to replace the* ***CNAME*** *record with an* ***A*** *record.*

![Debugging ACM certificate stuck in Pending validation](/images/acm/domains.png)

I had an interesting encounter with **AWS Certificate Manager** (ACM) recently. There was this certificate issued by ACM which had been working and renewing fine for several years now, but all of a sudden it couldn't renew. I got the validation emails and I had successfully validated the renewal for both domains, but for some reason, the certificate just wouldn't renew, it was simply stuck with this error "**The status of this certificate renewal request is "Pending validation". Further action is needed to validate and approve the certificate renewal**".

At first, I thought it might be some weird delay with ACM validation and ignored it (the error was not useful), but then I got my final warning regarding renewal, I was about to lose the certificate, uh oh!

![Debugging ACM certificate stuck in Pending validation](/images/acm/thisisfine.png)

I spend some time trying to debug, there were several other reports of the same issue in AWS forums and the solution suggested by most folks was adding a DNS CAA entry. It made sense and so I added a CAA entry to the root domain and decided to wait. Sadly that didn't fix the issue.

> DNS Certification Authority Authorization (CAA) is an Internet security policy mechanism that allows domain name holders to indicate to certificate authorities whether they are authorized to issue digital certificates for a particular domain name.

I gave up and reach out to AWS support, they explained the situation. The problem was with CAA, but my fix was incorrect. Even though I had added CAA certificate for `techulus.in`, there was another subdomain in the middle that was causing the problem. The certificate I request was for `*.capture.techulus.in`, and `capture.techulus.in` had a CNAME record pointing to Vercel, which had its own CAA records and whenever we use a CNAME record, the CAA checked follows that domain (in my case [cname.vercel-dns.com](https://support.console.aws.amazon.com/support/cname.vercel-dns.com?ref=techulus.xyz)) instead of techulus.in. :faceplam:

So we've identified the problem, and all we need is a fix. Obviously, we cannot change CAA records for [cname.vercel-dns.com](https://support.console.aws.amazon.com/support/cname.vercel-dns.com?ref=techulus.xyz) (duh) and I don't want to move away from Vercel. So I write to Vercel describing the problem, and they come back with a simple solution. Instead of using a CNAME record, just point my domain to Vercel using an A record and everything will be solved.

For future reference, identifying the problem is pretty easy, just use `dig`.

> dig is a network administration command-line tool for querying the Domain Name System

```bash
dig CAA capture.techulus.in +short cname.vercel-dns.com. 0 issue "letsencrypt.org" 0 issue "globalsign.com"
```

While using CNAME record, we can clearly see that there is a CAA record (from Vercel) and it doesn't have amazon.com, hence ACM cannot issue a certificate.

After changing the CNAME record to A record;

```bash
dig CAA capture.techulus.in +short
```

There is no CAA record, so it checks the parent domain.

```bash
dig CAA techulus.in +short 0 issue "amazon.com" 0 issue "globalsign.com" 0 issue "letsencrypt.org"
```

We've amazon.com, yay :)
