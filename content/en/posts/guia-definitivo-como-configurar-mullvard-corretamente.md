---
title: "The Definitive Guide: How to Set Up Mullvad Correctly"
date: 2026-08-21T08:11:37-03:00
draft: false
description: "An honest guide to privacy without illusions"
tags: ["VPN", "Privacy", "Mullvad", "Security"]
categories: ["Digital Security"]
---

## Introduction: VPN is not anonymity

It's common to think that a VPN solves the privacy problem on its own. I used to have that impression too: turn on the VPN, done — nobody can see anything.

In practice, it's not quite like that.

A VPN hides your IP address and prevents your ISP from directly seeing which sites you visit. It's also useful on public Wi-Fi networks. But that doesn't mean you've become anonymous.

This guide shows what I consider a reasonable setup for using Mullvad and what precautions make sense beyond the VPN.

---

## Part 1: When to use a VPN

### Where it makes sense

| Situation | Why |
|-----------|-----|
| Public Wi-Fi | Protects your traffic from others on the same network |
| Avoiding ISP throttling | Can help when the provider limits certain types of traffic |
| Geoblocked services | Lets you use a server in another country |
| Basic privacy | Your ISP no longer sees directly which sites you visit |
| Sensitive matters | Adds a layer of protection |

### Where it can cause problems

| Situation | Problem |
|-----------|---------|
| Banks | Some may consider the VPN IP suspicious |
| Video calls | It can increase latency |
| Online games | A distant server can increase your ping |
| Torrents | You need to check whether the VPN allows P2P |

### And using a VPN all the time?

There's no rule saying you need to stay connected to the VPN 24 hours a day.

If you're logged into a Google, Facebook, or Amazon account, for example, the VPN doesn't stop the service from knowing who you are. The login itself is still an identifier.

It also doesn't make much sense to use a VPN just because "VPN is more secure", without considering what you're actually trying to protect.

For me, the most important thing is to understand **which problem the VPN is solving at that moment**.

---

## Part 2: Setting up Mullvad

Mullvad is interesting mainly because of how it handles accounts.

You don't need to provide a name, phone, or email to create an account. The account is identified by a number.

There's also plenty of public documentation about the service, along with independent audits.

### Step 1: Installation

Download the app directly from the official site:

[mullvad.net/download](https://mullvad.net/download)

When you open the app, create an account. It will generate a number that you need to keep.

That number is important. Don't lose it.

### Step 2: Kill Switch

The kill switch is one of the configurations I consider most important.

The idea is simple: if the VPN drops, the app blocks traffic instead of letting your connection fall back automatically to your normal IP.

After enabling it (if it isn't already on), run a test: connect to the VPN, kill the connection, and try to open a site.

If the internet keeps working normally, it's worth investigating the configuration.

### Step 3: DNS

In **Settings → DNS**, you can use Mullvad's own DNS.

There are also options to block ads and trackers.

I'd avoid configuring an external DNS without a specific reason. The more different services you put in the path, the harder it becomes to understand exactly where your traffic is going.

### Step 4: Protocol and Anti-Censorship

- **Protocol:** WireGuard is the best option for normal use.
- **Port:** leave it on **Automatic**. Only change it if you're facing a specific connection issue.
- **On networks that block or hinder VPNs:** go to **VPN settings → Anti-censorship** and try options like **Shadowsocks**.

**Shadowsocks** adds a layer of obfuscation that can make it harder to identify and block the VPN connection.

If the VPN works normally on your network, there's no reason to enable anti-censorship.

### Step 5: Multihop

Multihop sends your connection through more than one server before reaching the destination.

This can be interesting in situations where you want to make it harder to correlate the entry and exit servers.

The problem is simple: more servers also mean more latency.

For normal browsing or using public Wi-Fi, I don't see a need to enable this.

It makes more sense for specific situations where you really need this additional layer.

### Step 6: IPv6

If you don't use IPv6 on your network, you can consider disabling it in the app.

The important thing here is to avoid a configuration where IPv6 ends up following a different path than the rest of your traffic.

After configuring, test it. Don't just trust what shows up in the app.

---

## Part 3: A VPN isn't enough

### 1. WebRTC Leak

WebRTC can expose network information you may not want to share.

On desktop, the options depend on the browser:

| Browser | Option |
|---------|--------|
| Firefox | `about:config` → `media.peerconnection.enabled = false` |
| Chrome/Edge | Use an extension that provides WebRTC leak protection |
| Mullvad Browser | Has more restrictive privacy settings by default |

On mobile, the situation is different.

If you're using Chrome on Android, for example, you don't have the same control over WebRTC that's available in Firefox or in some desktop browser versions.

Even when a mobile browser allows installing extensions, that doesn't necessarily mean WebRTC is fully disabled.

For more sensitive activity, I prefer using a browser built with privacy in mind rather than trying to turn a regular browser into a private one with several extensions.

### 2. Cookies and Tracking

A VPN doesn't stop a site from recognizing you through cookies or your login.

Some tools that can help:

- **uBlock Origin**
- **Privacy Badger**
- **ClearURLs**
- Firefox Multi-Account Containers

It's also worth separating activities when it makes sense. Using the same account everywhere makes it much easier to build a profile about you.

### 3. Leak Tests

After configuring your VPN, run some tests.

| Site | What to check |
|------|----------------|
| [dnsleaktest.com](https://dnsleaktest.com) | DNS leak |
| [browserleaks.com](https://browserleaks.com) | IP, DNS, and WebRTC |
| [ipleak.net](https://ipleak.net) | IP address and other network info |

Run the tests first **without the VPN** and then **with the VPN**.

The expected result is that, connected to the VPN, the sites see the VPN server's IP and not your normal public IP.

---

## Part 4: FAQ

### Does a VPN slow down the internet?

It can.

You're adding a server between your device and the internet, so there's a cost in latency and processing.

The difference mainly depends on the distance to the server, the quality of your connection, and the network load.

WireGuard usually performs very well, and that's one of the reasons I prefer it.

### Can I trust Mullvad?

No VPN provider should be treated as someone you need to trust blindly.

What I consider positive about Mullvad is its transparency, its policy of not logging certain data, and the independent audits.

Even so, a VPN doesn't replace other security measures.

### Why not use a free VPN?

Because running a VPN infrastructure costs money.

Some free VPNs use advertising or other forms of monetization. That doesn't mean every free VPN is bad, but I'd be very careful before handing over all my traffic to an unknown service just because it doesn't charge anything.

### Does Mullvad log my activity?

According to the service's own policy, it doesn't log activities like browsing history and source IP addresses to identify what you're doing.

That doesn't mean a VPN can make someone invisible.

The VPN is just one part of the chain.

---

## Conclusion

After setting up a VPN, there are still several ways a person can be identified.

The browser can hand over information. Cookies can identify you. An account can link all your activity to your name. And obviously, a VPN doesn't protect against phishing, malware, or a weak password.

That's why I see privacy as a combination of several things:

1. A trustworthy VPN when it makes sense.
2. A browser with good privacy protections.
3. Unique passwords for each service.
4. Two-factor authentication.
5. Care with links and files.
6. Tests to make sure your configuration is actually working.

There's no perfect setup.

The idea is simply to make it harder for information to be collected about you than it would be using everything on the defaults.
