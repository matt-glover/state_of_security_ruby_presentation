gradient: diagonal #5555dd #acacff
footer:
subfooter:
title: The State of Security in Ruby
author: Matt Glover

The State of Security in Ruby
=============================

What Will Be Covered
====================
TODO: Convert this into a proper TOC
TODO: Make sections into a one-liner or two followed by detail slides

Security in Ruby
================
Over the past (6-12?) months we have seen a variety of security issues reported against Ruby the language, major gems like Rails, and supporting infrastructure like rubygems.org.

Ruby Examples
=============
DoS attack? (Ruby 1.9.2 -> 1.9.3)

Rails Examples
==============
YAML parsing

Rubygems Website Example
========================
Gem Signing

CVEs in Other Gems
==================
Provide a list of CVEs and a time frame.

Security Vulnerability Impacts
==============================
Personal Rails Example (Scumbag Rails logo)
Tight Coupling (Plethora of stuff pulled in via Rails including ORM, mailer, web request stack)
Github Email Example

Why are we seeing this?
=======================
 - Popularity of Ruby
 - Popularity of major libraries like Rails
 - Increases/improvements in the software security research community
 - Things long known to be broken or questionable finally coming to relevance

Where are we at now?
 - A lot of low hanging fruit left?

How Does Ruby Stack Up?
=======================
Ruby v. Java
Ruby v. Other OSS (Apache, postgres, etc.)
Ruby v. Closed software

What Can You Do?
================

Accepting Reality
=================
Security breaches are inevitable (add exact Mandia quote)

Compare to the idea of bug-free code.

    :software_security == :software_quality

(Strictly speaking it is probably `:software_security >= :software_quality`)

Easy! Just Write Good Code!
===========================
<img src="images/good_code.png" style="display: block;margin-left: auto;margin-right: auto;width: 30%;" title="XKCD: How to write good code" alt="XKCD: How to write good code" />

Calibrating Risk
================
<img src="images/the_general_problem.png" style="display: block;margin-left: auto;margin-right: auto;height: 45%;" title="XKCD: Over-engineering - The general problem" alt="XKCD: Over-engineering The general problem" />

### <center>VS.</center>

<img src="images/goto.png" style="display: block;margin-left: auto;margin-right: auto;height: 45%;width: 75%" title="XKCD: Under-engineering - GOTO" alt="XKCD: Under-engineering - GOTO" />

Risk Management
===============
Detection, Defense, and Mitigation
Scaling security: Give examples of personal blog versus twitter. Personal blog versus small site that handles financials or health records versus amazon

Defense in Depth
================
<img src="images/7proxies.png" style="display: block;margin-left: auto;margin-right: auto;width: 70%;" title="Good luck I'm behind 7 proxies" alt="Good luck I'm behind 7 proxies" />

Detection - Internal
====================
Detecting a compromise:
 - Logging/auditing
 - Monitoring and notifications
 - External reporters of compromise

Detecting vulnerabilities:
 - Smart Testing (including fuzzing)
   - Testing for security
 - Third parties?

Detection - External
====================
 - 3rd party code (gems)
 - Tracking 3rd party libs (infrastructure postgres, apache, etc.)
 - Problems with your hosting provider (Linode compromise)

Defense
=======
Tools:
 - brakeman
 - metrics
 - esapi
Practices:
 - Helpful Practices (OWASP): Inline several of these
Callback to Flip:
 - Roll your own code
   - Possible security trade-off here.
   - Know your likely attack cases.

Mitigation
==========
Recovery Strategy (backups, logging/auditing/scanning)
 - Ancillary benefits

- Helpful Practices (OWASP)

What We Can Do
==============
Community efforts that can help.
 - Open communication
 - Careful communication of issues you discover
Go back to rubygems-trust example.

Credits
=======
XKCD, Rails, etc.

Any Questions?
==============
Email:
GPG Key:

CCs license
