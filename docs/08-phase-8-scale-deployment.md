# Phase 8 — Scale and Deployment
### Send units into the world. The planet becomes the instrument.

---

**What you have coming in:**
- A working sensor unit that reads environmental data and sends it to your Cloudflare backend
- A live dashboard showing incoming data
- A bridge connecting that data to your synthesizer
- An understanding of the full chain from sensor to sound

**What you'll have by the end:**
- Units that any non-technical person can set up by plugging them in
- A recipient experience so simple it needs almost no explanation
- Multiple units running in different locations, all visible on your dashboard
- A performance-ready system you've tested end to end

---

## The Problem With Your Current Firmware

Right now your firmware has your Wi-Fi network name and password hardcoded in `config.h`. That worked perfectly for your own setup — but you can't mail a unit to someone in another country with your home Wi-Fi credentials in it. Their network is different. And you can't ask them to edit code.

The solution is a **captive portal** — a pattern where, on first boot, the unit creates its own temporary Wi-Fi hotspot. The recipient connects to that hotspot from their phone, a simple web page appears asking for their Wi-Fi name and password, they fill it in, and the unit saves it and connects automatically. From that point on it just works.

This is the industry-standard approach for any connected device designed for non-technical users. Your router uses it. Smart home devices use it. You're going to add it to your units.

---

## Step 1 — Add WiFiManager to Your Firmware

> 🛠 **New library: WiFiManager**
> An Arduino library that handles the captive portal setup flow automatically. You add a few lines to your firmware, and it handles everything — creating the hotspot, serving the setup page, saving credentials, and connecting. You write almost nothing.

Open Claude with your spec and your current firmware:

---

> Here's my project spec: [paste spec]
>
> Here's my current firmware: [paste it]
>
> I need to update this firmware so that recipients can set up their own Wi-Fi credentials without editing any code. I've heard the WiFiManager library handles this. Can you:
> 1. Show me how to integrate WiFiManager into my existing firmware
> 2. Explain what the setup experience will feel like for someone who receives a unit
> 3. Make sure the unit still posts sensor data to my Cloudflare Worker after connecting
> 4. Tell me how to install the WiFiManager library

---

Flash the updated firmware to a unit and test the setup flow yourself first — connect to the hotspot it creates, go through the Wi-Fi setup, and confirm it joins your network and starts posting data. If that works, recipients will have the same experience.

---

## Step 2 — Give Each Unit a Unique Identity

Your dashboard needs to know which unit is sending which data. Right now you may have a hardcoded `unit_id` like `"unit-1"`. That's fine for one unit, but doesn't scale.

The cleanest solution: use the ESP32's MAC address as a unique ID. Every chip has a different one, built in at manufacture. No configuration needed — each unit identifies itself automatically.

Ask Claude:

---

> *"Can you update my firmware to use the ESP32's MAC address as the unit_id in the JSON it posts to Cloudflare, instead of a hardcoded string? The MAC address should be formatted as a clean string like `aa:bb:cc:dd:ee:ff`."*

---

Once this is in, every unit you ship will appear on your dashboard with its own unique identifier the moment it connects — no setup on your end.

If you want human-readable names on the dashboard (like "Oslo" or "Friend in Tokyo" instead of a MAC address), you can build a simple lookup table. Ask Claude:

---

> *"Can I add a way to map MAC addresses to friendly location names on my dashboard? I'd like to be able to add entries like `{ "aa:bb:cc:dd:ee:ff": "Oslo" }` somewhere and have the dashboard show the location name instead of the MAC address."*

---

---

## Step 3 — Write the Recipient Instructions

The card or note that goes in the box with each unit needs to be the simplest thing you've ever written. The person receiving it may have never set up a connected device. They need to succeed in under five minutes with no prior knowledge.

Ask Claude to help you write it:

---

> *"Can you help me write a short setup card for someone receiving one of my sensor units? They have no technical knowledge. The process is: plug in the USB power cable, wait 30 seconds, connect their phone to a Wi-Fi network called 'RainSensor-Setup', a page will appear asking for their Wi-Fi details, they fill it in and submit, and then the unit joins their network and starts working automatically. The card should fit on a small printed card, use simple language, and tell them what success looks like."*

---

Print these cards. Put one in every box. Keep the language warmer than instructional — these are people doing you a favour by hosting a node in your network. That should come through in the tone.

---

## Step 4 — Test With a Remote Person

Before shipping to strangers, test the full recipient experience with someone you know — ideally someone who genuinely won't ask you for help beyond the card. A friend or family member in a different location.

Ship them a unit. Don't brief them beyond the card. Watch your dashboard. The moment their unit appears, you know the experience works.

If they get stuck, find out exactly where — that's the thing to fix before you ship to people you can't easily call.

---

## Step 5 — Dashboard Updates for Multiple Units

Once you have more than one unit posting data, your dashboard needs to handle multiple units gracefully. Go back to Claude:

---

> *"My dashboard currently shows one unit's data. I now have multiple units sending data, each with a unique MAC address as their unit_id. Can you update the dashboard to show each unit in its own section, with its location name if I've assigned one, and the time since its last reading so I can see if a unit has gone offline?"*

---

"Time since last reading" is particularly useful during a performance — you can see at a glance which units are live and which have gone quiet.

---

## Step 6 — Performance Readiness Checklist

Before your first live performance using the network, run through this list. Do it the day before, not the day of.

**Hardware**
- [ ] All units powered and posting data — confirmed on dashboard
- [ ] Bridge script running and sending to synth — confirmed with a parameter moving
- [ ] Dashboard open on the device you'll use during performance
- [ ] Backup: know what happens if a unit drops off mid-show (the others keep going — that's fine)

**Network**
- [ ] Cloudflare Worker responding — visit your Worker URL and confirm JSON is coming back
- [ ] Dashboard loading and updating — leave it open for 30 minutes and watch for issues
- [ ] Know the URL by heart or have it bookmarked on your performance device

**Synth**
- [ ] Bridge has been running for at least an hour without issues
- [ ] All mapped parameters responding as expected
- [ ] You've played through the sensor ranges and know what they sound like

**The performance itself**
- [ ] You've done at least one full run-through combining sensor data with your live playing
- [ ] You have a plan for what to do if the network drops entirely (can you still perform without it?)
- [ ] Someone in the room knows what the sensor network is and can point to it if the audience asks

---

## Step 7 — Your Final Win ✓

- ✅ Units ship with captive portal firmware — no technical setup needed from recipients
- ✅ Each unit identifies itself by MAC address — no manual ID assignment
- ✅ At least 3 units running in different locations and visible on your dashboard
- ✅ The performance readiness checklist is complete
- ✅ You've performed — or rehearsed — with live network data shaping your sound

---

## What Comes After This

This curriculum ends here, but the project doesn't. Some things you'll likely iterate on as you go:

**More sensors.** Now that you know the loop, adding any new sensor is just another conversation with Claude — wire it, describe what you want, flash it, see it.

**Better enclosures.** The project brief mentions 3D-printed weatherproof cases. That's a whole design process — Claude can help you think through requirements and even generate basic OpenSCAD models to start from.

**Richer data mapping.** The more you perform with this, the more specific your ideas about mapping will get. What worked as a first attempt rarely stays as the final answer. Keep iterating.

**More units, wider distribution.** The infrastructure you've built scales — Cloudflare handles more traffic automatically, and every new unit is just another box to ship.

The loop is the same. It always was.

---

> *"The planet becomes the instrument."*
>
> You built that.

---

> 💡 **Keep your spec doc updated** as your project evolves. It's the anchor for every Claude conversation. If it's out of date, your conversations will drift. Take five minutes after every significant change to update it.
