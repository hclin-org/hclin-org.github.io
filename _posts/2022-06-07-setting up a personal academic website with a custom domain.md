---
layout: post
title: Setting up a personal academic website with a custom domain
description: "My experience with GitHub Pages, Jekyll, and custom domain configuration"
---

I have longed for a personal academic website to share my CV and research interests. However, I did not know what to do with this idea because it looked challenging to balance cost and performance. On the one hand, as a PhD student, I hesitated to subscribe to hosting services, which is typically $5 to $10 per month, on top of $10 to $20 for a custom domain. On the other hand, I do not feel confident in managing the technical parts of self-hosting, particularly keeping my website from security vulnerabilities. This summer, I came across the idea of combining GitHub Pages, the free web hosting, with Jekyll, the static site generators. I decided to give it a try as it incurs minimal monetary and time costs and delivers great performance. Also, it allows for custom domains. I based my experiment on the manual by [Jordi Pont-Tuset](https://jponttuset.cat/building-an-academic-website/). To configure my personal domain, I referred to the instructions of [GitHub Docs](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site) and [Google Domains](https://domains.google.com). Below, I will share some of the glitches I encountered and how I solved them, and I hope these may be helpful for you with troubleshooting when building a Jekyll website on GitHub Pages.

## Don't panic if the newly forked site is not working: it takes *commit*
As Jordi suggested, I forked his website on GitHub, so I had the repository (Jekyll) needed to make my own website. However, the forked website did not work on my GitHub pages. I learned that any change, e.g., adding a space or a line in README.md, can "commit" the changes and render the website. After I made a random change to the README.md, my forked website started to run!

## Adding a custom domain does take multiple steps
I wanted to use my domain name linking to my website hosted on GitHub Pages. First, I went to my Jekyll repository on GitHub and clicked **setting**. On the left panel, there was **Pages** in the category **Code and automation**. Click it, type your domain in the **Custom Domain**, and save the settings. GitHub suggested I make relevant changes in my domain registrar.
<br />
![setting_domain_01](/images/setting_domain_01.png)
<br />
As I registered my domain name at Google Domains, I needed to configure the domain records there. If you use Google Domains, the following steps might be helpful. To begin with, I went to the landing page of Google Domains and clicked **manage** to the right of my domain name.
<br />
![setting_domain_02](/images/setting_domain_02.png)
<br />
Later, I clicked **DNS** on the left panel and, subsequently, **Manage custom records** on the right panel.
<br />
![setting_domain_03](/images/setting_domain_03.png)
<br />
As I wanted to use apex domain and a www subdomain to reach my website, i.e., people could find my website at both *hclin.org* and *www.hclin.org*, I must add A and CNAME records to my DNS configuration. I also added the AAAA entry for IPv6 compatibility. The purpose of the entries is to make my domain linked to the GitHub servers that house my website.

For the apex domain, the host name was blank, and the type was *A*. I did not change the default TTL. In the data column, I entered the four IPs in respective entries:
- 185.199.108.153
- 185.199.109.153
- 185.199.110.153
- 185.199.111.153

For the www subdomain, I entered *www* in the host name, and the type was *CNAME*. I did not change the default TTL, either. In the data column, I entered *yourgithubid.github.io*.

I also created another entry for IPv6 compatibility. This was similar to the previous type A setting. However, the type should be *AAAA*, instead. The data entries were the four IPv6 addresses: 
- 2606:50c0:8000::153
- 2606:50c0:8001::153
- 2606:50c0:8002::153
- 2606:50c0:8003::153
<br />
![setting_domain_04](/images/setting_domain_04.png)
<br />
After saving these settings in Google Domains, I returned to the GitHub settings, and the custom domain worked. I also [verified my domain](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/verifying-your-custom-domain-for-github-pages) and [enforce HTTPS](https://docs.github.com/en/pages/getting-started-with-github-pages/securing-your-github-pages-site-with-https) to enhance security.