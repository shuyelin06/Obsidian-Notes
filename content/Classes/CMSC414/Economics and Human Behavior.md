---
title: Economics and Human Behavior
tags:
- cmsc414
---

We end with a discussion of economics and human behavior, both of which are also important in computer security, yet often are less considered.

# Economic Incentives
## Why is Security so Bad?
In security, money is the underlying driver for both attack and defense.
- What data is for sale?
- By whom is the data from?
- How is the data obtained?
- Who is buying software?

Understanding these economic incentives can help us find places in the system that are most vulnerable for preventing attacks.

At the bottom line, everything comes down to **externalities**. Everyone says they want security, but no one wants to actually pay extra for security. 
- Security costs money to develop and maintain
- Security provides minimal benefit to the companies themselves
- Neglecting security costs nothing.

Furthermore, because we only notice security when it fails, many companies aren't penalized for poor security, and as such aren't incentivized to keep things secure.

Actual security requires either **customer demand** creating an incentive, or **regulation** forcing the security. Unfortunately, in the current climate we have neither of these.

## Zero-Days
For a vulnerability, a typical timeline is as follows:
1. The vulnerability is introduced
2. An exploit using this vulnerability is released
3. The vulnerability is discovered by vendor
4. Vulnerability is disclosed publicly
5. AV Signatures released
6. Patch released
7. Patch deployment completed

Between (2) and (4) is what's known as the **zero-day attack period**, as during this period, the vulnerability has an exploit that is not publicly known. 

Without the public knowing about the exploit, it can be particularly powerful and has a lot of value. Thus, buying and selling zero-days is a very big business, as they can be treated as a commodity!

**Exploit brokers** are people who drive this business, by matching buyers and sellers for a commission. The bigger the target (customer base), the more the zero-days sell for.
> Payments often will continue until the vulnerability id disclosed! 

## Case Analysis: Spam
Spam is a costly nuisance. Delivering and storing spam takes resource costs, annoys users who are receiving it, and can lead to malware infections / fraud.

How do we fight it? Well, let's try to understand why it exists, and how it works! 

Spammers will generally use botnets to send spam, to prevent spam from being blocked at a single source. 
> We can block the URLs that spam contains. But they can work around this by having lots of URLs, using URL shorteners, or by redirecting victims!

> [!Info] Fighting Botnets
> So how do we fight the botnets?
> 
> We could prevent the initial infection, but this is really hard as it requires we secure everyone's machine!
> 
> Instead, we generally try to take down the bot herder. Botnets generally rely on a **Command and Control (C&C) server**, otherwise known as a **Bot Herder**. If we can take down the bot herder, then the botnet will go idle!
> 
> Note that because there's good economic incentives for this, botnet managers are really good at building robust distributed systems! That way, their herder can avoid being taken down.

What other techniques do spammers employ? 

### Bulletproof Hosts
Most people generally do not like spam. So, oftentimes, the spammers' host, name service, or domain registration can be taken down. However, for enough money, you can buy **Bulletproof Hosting**, whose services won't do this! 

These are services frequently associated with organized crime, but are also legitimately used by dissident groups and whistleblowers! As both bad guys and good guys use the service, stoppine one also stops the other!

### Fast-Flux DNS
DNS records have a Time-To-Live, which lets cache records be invalidated.

In **Fast-Flux DNS**, this Time-To-Live is small, making the hostname to IP address binding change rapidly, which is hard to filter against! A spammer acn use proxies as spam URLs, which are stored as Fast-Flux proxy records, and redirect to more-stable addresses.
> Fast-Flux DNS can also be used for good! For example, Google uses it to do load balancing.

### Affiliate Networks
Many things require tons of people with different skills. For example, to build a house, you need architects, roofers, carpenters, etc.

This is the same in scams and black markets! Not everyone is able to / willing to do everything. So, what we do is focus on what we're good at, and hire out your services!
> In a black market, you don't have organizations that do everything! Instead, we hire each other out.

This forms what we call **affiliate networks**. These are networks that hiring out multiple different parties to do a variety of services for an individual! These services include:
- Domain purchasing
- Web storefronts and analytics

For advertising, affiliate networks can use spammers. These spammers will generally pay bot herder to send spam and get a commission from their affiliate program for completed sales.

### Tying it All Together
Based on all of this, let's see how everything ties together.
1. First, the spammer delivers spam to a user with the botnet.
2. The user, interested in the spam, clicks on the URL.
3. The URL directs the user to some storefront for purchasing, which is associated with the affiliate network.
4. After the user purchases the goods, the affiliate network will have the goods shipped through a supplier.

These users often buy goods like pharmaceuticals, replica luxury goods, and counterfeit software. Interestingly, there are not a lot of affiliate programs in this business! They're all highly concentrated into a few groups. 

We can exploit this at the payment step! Not too many banks are willing to work with criminals, and making one take a black market vendors out reduces their options, and discourages other banks from similar behavior!


# Human Behavior 
## Overview
In any cryptosystem, one of the biggest threats is **humans**.
- Malicious humans who want to cause harm
- Humans who don't know what to do when they get specific warnings
- Humans who don't care about security policies

In general, humans, with their inherent limitations, are a weak link of cryptosystems.
- Security is often a secondary priority for most people
- Security concepts are hard to understand
- Human capabilities are limited (ex. remembering strong passwords for every account)
- Humans have misaligned priorities, and if security hinders their workflow they may actively work against the security
- Frequent false positives can eventually cause all alerts to be ignored (**habituation**)

We need to design our systems with this in mind!

## Habituation
Habituation is an issue that can happen all the time with security. If we see something so often, we tend to not remember or care about it.

This can cause important alerts to be ignored by users! We need to combat this by making sure the important things actually stand out.

## Economic Behaviors
People are economical. Given two paths to a goal, they will generally take the shorter one with less steps. 

This presents a problem with security. Oftentimes, making people's systems more secure may also add more steps for them to do, and if subverting the security is easier, then people will generally do just that. Just because the security is in place and practices are recommended, does not mean that all people will use it.

## Password Expiration
Password expiration has been a standard of security policy. But does it help?

It was found that users typically just transform passwords in small ways, suggesting that attackers could just predict future passwords from old ones!
> Researchers did a study on this, and with some salt on the passwords (a bit of randomness), they were able to crack a lot of accounts!

Another analogous idea is security images. Many organizations report that if users do not see their security image / caption, then they should not log in. Theoretically, this provides a simple way for users to not log in to fake sites. 

However, a study found that most users would log in anyways! Some key takeaways from this:
- We need to account fo attention failure
- Users have misaligned priorities and take the shortest path to achieve their goal
- Users commonly misunderstand security concepts.

## Improving Security
Some tips to improve security:
- Limit what people have to remember
- Only grab attention when you need it. Make critical information stand out to avoid habituation
- Minimize user effort as much as possible. If users need to take action, make it easy. If something is dangerous, make it difficult.
- Make warnings understandable, and make the easy decisions for the user.
