# h2 — Cyber security Scene

Here is the second assignment for the course cyber securirty 

### a) Darknet Diaries - Podcast Chosen from Darknet Diaries is Episode 45 – Xbox Underground (Part 1)

- This episode starts by telling the story of a group of curious teenagers and young adults that are in their late 2000s who were obsessed with understanding how the original Microsoft Xbox console worked inside.

it goes further to highlights how early Xbox modifying began with people like Andrew "Bunnie" Huang, who just wanted to run their own software and custom games on hardware they legally purchased.

- Escalating to Network Breaches, the group of teens shifted from modifying physical consoles in their bedrooms to actively searching for unauthorized access points inside Microsoft's internal corporate network.

- It continued further into stealing unreleased Games & Code, as soon as they were inside, they located and downloaded unreleased video game titles (like early builds of Gears of War) and proprietary software blueprints.

- Then comes the Consequences which unravels, what began as harmless curiosity quickly spiraled out of control into federal crime, illegal sales of counterfeit developer kits, and eventual law enforcement raids.

- My Idea / Question with regards to this is Where should companies draw the line between punishing curious young hackers and inviting them into legal bug bounty programs? say for instance, If Microsoft had offered a legal channel for these kids to report security bugs, could they have turned these hackers into cybersecurity allies instead of criminals?

### b) Blog. Read one article in one of these blogs - Blog Chosen: Krebs on Security (by Brian Krebs)
## Article: Tech Firms Dismantle Botnet That Turned 1.3M TV Boxes Into Proxies

Summarizing this in terms of massive infection, security researchers and technology companies recently took down a network of over 1.3 million infected Android set-top TV streaming boxes worldwide.
- Now instead of users clicking on bad links, the manufacturer (a company called Videostrong) actually pre-installed hidden malicious code ("backdoors") onto the TV boxes directly in the factory before selling them to consumers regarded as factory backdoor in this case.
- Stealthy Proxy Network --> Cybercriminals hence bought access to these infected TV boxes to secretly route their own illegal internet traffic through everyday households, hiding their location and committing online ad fraud.
- Because the bad code was built into the physical device's core firmware, regular users had no idea their home network was being used by criminals, and standard software updates couldn't clean it resulting in difficulty in fixing.
- My Idea / Question: I was just thinking that, since low-cost IOT smart home devices are often made overseas with zero security oversight, should governments mandate strict basic security standards before hardware can be sold online to everyday buyers?

### c) Science that

Putting these real-world events into context, I connect them to two classic cybersecurity frameworks: _Defense in Depth and the Cyber Kill Chain_

1. Xbox Underground & Defense in Depth
   - The Theory here is that defense in Depth is the idea that security shouldn't rely on just one wall or door. You need multiple layers of defense (passwords, network segregation, monitoring) so if an attacker breaks through one door, they are still blocked by the next.
   - The Connection on the otherhand in the Xbox Underground incident, once the hackers gained access to one internal Microsoft server, they were able to jump across internal networks almost freely because internal systems trusted each other too much. A multi-layered defense (isolating development servers from internal staff networks) would have stopped them early.

2. Android TV Box Botnet & the Cyber Kill Chain
   - The Theory: The Cyber Kill Chain model breaks down an attack into sequential steps: Reconnaissance $\rightarrow$ Weaponization $\rightarrow$ Delivery $\rightarrow$ Exploitation $\rightarrow$ Installation $\rightarrow$ Command & Control $\rightarrow$ Actions on Objectives.
   - The Connection: By placing a backdoor directly at the factory level, the criminals completely bypassed the early steps of the kill chain (they didn't need to trick users with phishing emails or find web bugs). They jumped straight to the Installation and Command & Control stages, proving that supply chain vulnerabilities skip traditional user-side defenses.

### d) Download Debian. This is done as instructed at this point. Downloaded Debian 13-Trixie installation image on my computer

## f) Voluntary bonus: Install a feed reader and follow some RSS / Atom feeds

An RSS reader collects updates from security blogs in one place without you having to visit each website manually.
1) For Blogs (RSS Reader) i used a recommended free App Feedly.
by signing up, clicking add content/plus button, Copy and paste the feed link from your favorite blogs, for example:
Krebs on Security, then new articles will automatically show up in my inbox as soon as they are published.

3) For Podcasts: Recommended Free App was AntennaPod (Android on F-Droid / Google Play) or Apple Podcasts / Pocket Casts (Mac/iOS).
Open the app, search for Darknet Diaries or "SANS StormCast", and click on Subscribe


## References

Krebs, Brian. (2026, November 2). Tech Firms Dismantle Botnet That Turned 1.3M TV Boxes Into Proxies. Krebs on Security. https://krebsonsecurity.com/2026/11/tech-firms-dismantle-botnet-that-turned-1-3m-tv-boxes-into-proxies/

Rhysider, Jack. (Host). (2019, August). Xbox Underground (Part 1) (Ep. 45) [Audio podcast episode]. In Darknet Diaries. https://darknetdiaries.com/episode/45/

https://terokarvinen.com/cyber-security/#homework

