gradient: diagonal #5555dd #acacff
footer:
subfooter:
title: The State of Security in Ruby
author: Matt Glover

<% content_for :css do %>
.step { visibility: hidden; }
<% end %>

The State of Security in Ruby
=============================

<% left do %>
  <img src="images/broken_lock.png" title="Broken lock" alt="Broken lock" style="display: block;margin-left: auto;margin-right: auto;width: 70%;" />
<% end %>

<% right do %>
  <img src="images/ruby_logo.png" title="Ruby logo" alt="Ruby logo" style="display: block;margin-left: auto;margin-right: auto;width: 50%;" />
<% end %>

Who Does This Guy Think He Is!?
===============================
He Is:

* Matt Glover
* Software engineer at [Mandiant](http://www.mandiant.com/)
* Interested in software security and secure coding concepts

He Is **NOT**:

* A security expert
* More qualified to speak about security than anyone else in the room
    * Even though he works at a security-focused company
    * He just has to worry about security a little more often

He Also Is:

* Looking to hire:
    * Test automation engineers and QA
    * Developers with a strong background in Ruby and/or JavaScript
    * Strong UI developers (HTML/CSS)

What Will Be Covered
====================

1. Recent Security Issues in the Ruby Ecosystem

2. Is Ruby Security A Mess?

3. What Can Be Done? - Practices, Tools, and Tips

Security Issues in Ruby
=======================
A rocky 12 months on the security front (primarily since the start of 2013)

* [55 CVEs mentioning Ruby](https://web.nvd.nist.gov/view/vuln/search-results?adv_search=true&cves=on&cve_id=&query=Ruby&cwe_id=&pub_date_start_month=4&pub_date_start_year=2012&pub_date_end_month=-1&pub_date_end_year=-1&mod_date_start_month=-1&mod_date_start_year=-1&mod_date_end_month=-1&mod_date_end_year=-1&cvss_sev_base=&cvss_av=&cvss_ac=&cvss_au=&cvss_c=&cvss_i=&cvss_a=):
    * MRI, JRuby, Rubinius, etc.
    * Rails, Devise, JSON, etc.
    * Various other gems large and small
* Rubygems compromise in January

Ruby Example
============
[Hash-flooding DoS vulnerability for ruby 1.9](http://www.ruby-lang.org/en/news/2012/11/09/ruby19-hashdos-cve-2012-5371/).

TL;DR - Replaces hashing algorithm to avoid predictable collisions leading to worst-case insert times.

<img src="images/ruby_logo.png" title="Ruby logo" alt="Ruby logo" style="display: block;margin-left: auto;margin-right: auto;width: 15%;" />


Rails Example
=============
[3.2.11 Abitrary Code Execution via XML](http://weblog.rubyonrails.org/2013/1/8/Rails-3-2-11-3-1-10-3-0-19-and-2-3-15-have-been-released/)

TL;DR - Entity types, like YAML, were parsed in XML parameter hash construction. Now vulnerable types are not allowed.

Rubygems Website Example
========================
[Rubygems compromise in January](http://blog.rubygems.org/2013/01/31/data-verification.html)

TL;DR - Executed `Yaml.load` on gem metadata enabling code execution. Now whitelists classes demarshalled from gems.

CVEs in Other Gems
==================
A *non*-exhaustive list of other Ruby gem CVEs over the past year:

* [rack-cache (CVE-2012-2671)](https://web.nvd.nist.gov/view/vuln/detail?vulnId=CVE-2012-2671)
* [mail (CVE-2012-2140)](https://web.nvd.nist.gov/view/vuln/detail?vulnId=CVE-2012-2140)
* [authlogic (CVE-2012-6497)](https://web.nvd.nist.gov/view/vuln/detail?vulnId=CVE-2012-6497)
* [json (CVE-2013-0269)](https://web.nvd.nist.gov/view/vuln/detail?vulnId=CVE-2013-0269)
* [curl (CVE-2013-2617)](https://web.nvd.nist.gov/view/vuln/detail?vulnId=CVE-2013-2617)
* [nori (CVE-2013-0285)](https://web.nvd.nist.gov/view/vuln/detail?vulnId=CVE-2013-0285)
* [crack (CVE-2013-1800)](https://web.nvd.nist.gov/view/vuln/detail?vulnId=CVE-2013-1800)
* [httparty (CVE-2013-1801)](https://web.nvd.nist.gov/view/vuln/detail?vulnId=CVE-2013-1801)
* [extlib (CVE-2013-1802)](https://web.nvd.nist.gov/view/vuln/detail?vulnId=CVE-2013-1802)
* [multi_xml (CVE-2013-0175)](https://web.nvd.nist.gov/view/vuln/detail?vulnId=CVE-2013-0175)
* [devise (CVE-2013-0233)](https://web.nvd.nist.gov/view/vuln/detail?vulnId=CVE-2013-0233)
* [md2pdf (CVE-2013-1948)](https://web.nvd.nist.gov/view/vuln/detail?vulnId=CVE-2013-1948)

Security Vulnerability Impacts
==============================
Upgrading Rails:

<% step do %><img src="images/x.png" alt="x" /> [3.2.8 => 3.2.9]: Backwards incompatible changes. Wait for the revert.<% end%>

<% step do %><img src="images/x.png" alt="x" /> [3.2.8 => 3.2.10]: Still waiting on the 3.2.9 reverts and easy to patch.<% end %>

<% step do %><img src="images/x.png" alt="x" /> [3.2.8 => 3.2.11]: Still waiting on the 3.2.9 reverts and easy to patch.<% end %>

<% step do %><img src="images/x.png" alt="x" /> [3.2.8 => 3.2.12]: Okay this is getting out of hand. Are the reverts even coming?<% end %>

<% step do %><img src="images/checkmark.png" alt="check" /> [3.2.8 => 3.2.13]: Reverts! More incompatible changes!? Work around issues?<% end %>

Why Rails Patches Are Painful
================================

Tight coupling between multiple components makes patching difficult.

Rails includes an ORM, a mailer, a full web request stack, parameter handlers, etc.

Github's recent email problem demonstrated these pains

[Rails has improved their patch policy](http://weblog.rubyonrails.org/2013/2/24/maintenance-policy-for-ruby-on-rails/)

Why are we seeing this?
=======================
<% step do %>* Popularity of Ruby<% end %>
<% step do %>* Popularity of major libraries like Rails<% end %>
<% step do %>* Increases/improvements in the software security research community<% end %>
<% step do %>* Things long known to be broken or questionable finally coming to relevance<% end %>

<% step do %>
Where are we at now?

* A lot of low hanging fruit left?
<% end %>

How Does Ruby Stack Up?
=======================
Ruby v. Java - Java is a mature enterprise-grade solution! That **MUST** be more secure!!!
<% step do %>
<img src="images/x.png" alt="x" /> [US government advises computer users to disable Java software](https://www.us-cert.gov/ncas/alerts/TA13-010A)

<img src="images/x.png" alt="x" /> [Oracle’s Java SE Critical Patch Update for April 2013](http://www.oracle.com/technetwork/topics/security/javacpuapr2013-1928497.html) contains 19 CVEs with CVSS base score of 10 (the highest you can go)
<% end %>

<% step do %>
---
Ruby v. Other OSS (Apache, Postgres, etc.)
<% end %>
<% step do %>
* [Apache had 70+ CVEs over the past year](https://web.nvd.nist.gov/view/vuln/search-results?adv_search=true&cves=on&cve_id=&query=Apache&cwe_id=&pub_date_start_month=4&pub_date_start_year=2012&pub_date_end_month=-1&pub_date_end_year=-1&mod_date_start_month=-1&mod_date_start_year=-1&mod_date_end_month=-1&mod_date_end_year=-1&cvss_sev_base=&cvss_av=&cvss_ac=&cvss_au=&cvss_c=&cvss_i=&cvss_a=)
* [Postgres recently issued a major security patch](http://www.postgresql.org/about/news/1397/)
<% end %>

What Is The Lesson Here?
========================
<% left do %>
  <% step do %>* Ruby has terrible security!<% end %>
<% end %>
<% right do %>
  <% step do %><img src="images/x.png" alt="x" /><% end %>
<% end %>
<% left do %>
  <% step do %>* Everything has terrible security!!<% end %>
<% end %>
<% right do %>
  <% step do %><img src="images/x.png" alt="x" /><% end %>
<% end %>
<% left do %>
  <% step do %>* Security is hard!!!<% end %>
<% end %>
<% right do %>
  <% step do %><img src="images/x.png" alt="x" /><% end %>
<% end %>
<% left do %>
  <% step do %>* Writing software is hard.<% end %>
<% end %>
<% right do %>
  <% step do %><img src="images/checkmark.png" alt="check" /><% end %>
<% end %>

Accepting Reality
=================

---
---*Security Breaches Are Inevitable*---
  
<% step do %>
Disagree? Consider the following:

> "Software bugs are inevitable."
<% end %>
<% step do %>
In my view:

    :software_security == :software_quality

*Arguably software security includes non-software elements that fall outside software quality*
<% end %>

<% step do %>
So how do we deal with this reality?
<% end %>

Easy! Just Write Good Code!
===========================
<img src="images/good_code.png" style="display: block;margin-left: auto;margin-right: auto;width: 30%;" title="XKCD: How to write good code" alt="XKCD: How to write good code" />

Calibrating Risk
================
<img src="images/the_general_problem.png" style="display: block;margin-left: auto;margin-right: auto;width: 55%;" title="XKCD: Over-engineering - The general problem" alt="XKCD: Over-engineering The general problem" />

### <center>VS.</center>

<img src="images/goto.png" style="display: block;margin-left: auto;margin-right: auto;width: 75%;" title="XKCD: Under-engineering - GOTO" alt="XKCD: Under-engineering - GOTO" />

Risk Management
===============
Scale your security.
<% step do %>
* Compare a personal blog to Twitter
<% end %>
<% step do %>
* Compare a personal blog to a small site handling financial data
<% end %>
<% step do %>
* Compare a small financial site to a global financial organization
<% end %>

Defense in Depth
================
<img src="images/7proxies.png" style="display: block;margin-left: auto;margin-right: auto;width: 70%;" title="Good luck I'm behind 7 proxies" alt="Good luck I'm behind 7 proxies" />

Detection - Internal Issues
===========================
<% left do %>
Detecting a compromise:

* Logging/auditing
* Monitoring and notifications
* Make it easy to report vulnerabilities and compromises securely
<% end %>
<% right do %>
Detecting vulnerabilities:

* Smart testing
    * Writing tests for security (edge cases, authorization checks, etc.)
    * Utilize security-focused testing tools like SAST and DAST
* Hiring third parties
<% end %>

Detection - External Issues
===========================

Areas to Consider:

* 3rd party code (gems)
* Tracking 3rd party libs (infrastructure postgres, apache, etc.)
* Problems with your hosting provider (Linode compromise)

<% step do %>
Some Tracking Mechanisms:

* Find a place that announces security issues and follow it
* If that fails find a place that announces releases in general and follow it
    * RSS/Atom feeds
    * Mailing lists
* Follow established members of the tech community (blogs, Twitter, etc.)
* Track CVEs from NIST
<% end %>

Defense
=======
<% left do %>
Practices:

* [OWASP Top 10 Security Risks](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project)
* [Read the OWASP Development Guide](https://owasp.org/index.php/Category:OWASP_Guide_Project)
* Security controls as design elements and requirements
* Ask security questions during code reviews
* Integrate security cases into your test suite
* Consider rolling your own code in place of third party libraries
    * [*I'm with you Flip!*](http://www.meetup.com/dcruby/events/68564112/)
    * Possible security trade-off here
    * Know your likely attack cases
* Controls on third party libraries
<% end %>
<% right do %>
<img src="images/clippy_secure.jpg" style="display: block;margin-left: auto;margin-right: auto;" title="It looks like you're trying to secure your software" alt="It looks like you're trying to secure your software" />
<% end %>

Defense - Continued
===================
Concepts:

* (C)onfidentiality
* (I)ntegrity
* (A)vailability

Tools:

* [brakeman](http://brakemanscanner.org/) is a SAST for Rails
* Code quality suites, like [metric_fu](https://github.com/metricfu/metric_fu), call out weak spots in your code
* [OWASP ESAPI gem](http://thesp0nge.github.io/owasp-esapi-ruby/) brings a FOSS web application security control library to Ruby
* One of many dynamic application security tools
    * [OWASP ZAP](https://www.owasp.org/index.php/OWASP_Zed_Attack_Proxy_Project)
    * [OWASP WebScarab](https://owasp.org/index.php/Category:OWASP_WebScarab_Project)
    * [Burp Suite](https://en.wikipedia.org/wiki/Burp_suite) - Costs $$$
* Intentionally cause failures in a cloud setting with [Chaos Monkey by Netflix](https://github.com/Netflix/SimianArmy)


Mitigation
==========
To reiterate: *Security breaches are inevitable*

<% step do %>
Treat a security response like a disaster recovery response:

* Keep backups
    * **Test your restore process**
* Encrypt sensitive data
    * SHA-2 hashing of passwords (or bcrypt, scrypt, et. al. if you prefer)
    * `OpenSSL.fips_mode = true` for Federal clients!
* Load balancing
* Ship audits/logs to another machine
    * Logs tell you who, what, when, where, and how
* Notify appropriate stakeholders
    * Sometimes compromise of data carries an obligation to notify
<% end %>

<% step do %>
Ancillary benefits:

* During a breach don't panic. You have a plan!
* Multi-purpose: Downed servers, corrupted data stores, etc.
<% end %>

What We Can Do
==============
Community efforts that can help:

* Open communication
* Thoughtful disclosure of issues you discover
* Make step-wise progress
    * rubygems-trust attempted a large scale solution to gem signing

Credits
=======

Most images under a Creative Commons license.

* Comics - [xkcd.com](https://xkcd.com/)
* Broken Lock - [Iron Bishop via wikimedia commons](https://commons.wikimedia.org/wiki/File:Image-Wikimania--5_agosto--Broken_lock.png)
* Ruby Logo - [Yukihiro Matsumoto via wikimedia commons](https://commons.wikimedia.org/wiki/File:Ruby_logo.png)
* Red X - [Yerson_O via wikimedia commons](https://commons.wikimedia.org/wiki/File%3AX.png)
* Green Checkmark - Public domain! Woo!!!

Any Questions?
==============

---

Email: [Matt Glover <matt.glover@mandiant.com>](mailto:matt.glover@mandiant.com)

GPG Key: [2048R/54C013B4](http://pgp.mit.edu:11371/pks/lookup?op=vindex&search=0x093E4CC354C013B4)

Presentation: [https://github.com/matt-glover/state_of_security_ruby_presentation](https://github.com/matt-glover/state_of_security_ruby_presentation)

---

<div style="text-align: center;vertical-align: middle;">
<a rel="license" href="http://creativecommons.org/licenses/by/3.0/deed.en_US"><img alt="Creative Commons License" style="border-width:0" src="http://i.creativecommons.org/l/by/3.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">The State of Security in Ruby</span> by <span xmlns:cc="http://creativecommons.org/ns#" property="cc:attributionName">Matt Glover</span> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by/3.0/deed.en_US">Creative Commons Attribution 3.0 Unported License</a>.
</div>
