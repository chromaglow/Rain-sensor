# Phase 5 — Getting Online
### The ESP32 stops being a local gadget and becomes a node in a network.

---

**What you have coming in:**
- Multiple sensors reading and printing data to the Serial Monitor
- VS Code, Terminal, git workflow solid
- A spec document you start every session with

**What you'll have by the end:**
- The ESP32 connected to Wi-Fi
- Sensor data posting to a remote endpoint every few seconds
- Your data appearing on a screen you didn't touch — the moment it starts feeling like a network

---

## What's Actually Happening Here

Right now your ESP32 collects data and prints it locally — only visible if you're sitting at your computer with the Serial Monitor open. In this phase you give it a voice. It will connect to Wi-Fi, package its sensor readings as a small data packet, and send that packet to a server on the internet. The server receives it and stores or displays it.

The pattern — sensor → Wi-Fi → server → display — is the entire backbone of your project. Everything in Phase 6 and beyond is just building out that display end.

---

## One Important Thing Before You Write Any Code

You're about to write firmware that includes your Wi-Fi network name and password. **Do not commit that to GitHub.**

If your repo is public, your Wi-Fi credentials would be visible to anyone who looks at your code. Even in a private repo it's bad practice. Here's the safe way to handle it — ask Claude to show you how to use a separate config file:

---

> *"I'm about to write ESP32 firmware that connects to Wi-Fi. Can you show me how to store my Wi-Fi credentials in a separate file called `config.h` that I can keep out of GitHub using a `.gitignore` file? Please show me the config file structure and how the main firmware references it."*

---

Claude will give you a `config.h` file and show you how to add it to `.gitignore` so it never gets pushed. Do this first, before writing the networking code. It takes five minutes and saves a real problem.

---

## Step 1 — Connect to Wi-Fi

Open Claude with your spec doc and ask:

---

> Here's my project spec: [paste spec]
>
> I have my sensors reading correctly. Now I want to connect the ESP32 to Wi-Fi. My credentials are stored in `config.h` using the pattern you showed me.
>
> Can you write firmware that:
> - Connects to Wi-Fi on startup using credentials from `config.h`
> - Prints "Connected — IP: [address]" to the Serial Monitor when it succeeds
> - If it fails to connect, retries every 5 seconds and prints what it's doing
> - Still reads all my sensors and prints their values as before

---

Flash it. Open the Serial Monitor. You should see the ESP32 connecting and then printing a local IP address. That IP address is your unit's address on the network — it exists on the internet now.

**If it won't connect:** Check the Wi-Fi credentials in `config.h` — typos are the most common cause. Also check that your network is 2.4GHz. The ESP32 does not support 5GHz networks.

---

## Step 2 — Send Data to a Test Endpoint

Before building a real server, you're going to send data to a temporary test URL that shows you incoming requests in real time. This lets you confirm the ESP32 is sending correctly before worrying about the receiving end.

**Set up your test endpoint:**

1. Go to **webhook.site** in your browser
2. You'll immediately get a unique URL — something like `https://webhook.site/abc123def456`
3. Copy that URL — this is your temporary endpoint
4. Leave the webhook.site tab open

Now ask Claude to update your firmware to send data there:

---

> Here's my current firmware: [paste it]
>
> Can you update it to also send an HTTP POST request to `https://webhook.site/YOUR-UNIQUE-URL` every 10 seconds with the sensor readings formatted as JSON? The JSON should include all my sensor values and a timestamp.
>
> Please keep the Serial Monitor printing working too — I want to see locally what it's sending.

---

Flash it, open the Serial Monitor, and watch the tab you left open on webhook.site. Within a few seconds you should see requests arriving — each one containing your sensor data as JSON.

That's the moment. Data leaving your desk and arriving somewhere else on the internet.

---

## Step 3 — Understand What JSON Is

The data your ESP32 is sending looks something like this:

```json
{
  "temperature": 21.4,
  "humidity": 58.2,
  "pressure": 1013.1,
  "timestamp": 1234567890
}
```

This is **JSON** — a simple structured format for sending data between devices. Curly braces hold the data, each value has a name and a number. It's what your ESP32 sends, what your server will receive, and what your dashboard will read. You don't need to write it by hand — Claude generates it — but it's useful to be able to read it.

Ask Claude to explain yours if anything looks confusing:

> *"Can you explain what each field in my JSON payload means and why it's formatted that way?"*

---

## Step 4 — Your First Win ✓

- ✅ The ESP32 connects to Wi-Fi on boot and prints its IP address
- ✅ Sensor data is posting to webhook.site every 10 seconds
- ✅ You can see the JSON arriving in real time in your browser
- ✅ Your Wi-Fi credentials are in `config.h` and that file is in `.gitignore`
- ✅ Updated firmware committed and pushed to GitHub (without the credentials)

---

## Going Further: A Stable Endpoint

Webhook.site URLs expire after a while — they're for testing, not for real use. In Phase 6 you'll build a permanent server on Cloudflare that receives your data, stores it, and serves it to a dashboard. But you don't need that yet.

For now, if you want a slightly more stable test endpoint that lasts longer, ask Claude:

---

> *"Webhook.site is temporary. Is there a simple free service I can use as a more stable test endpoint while I work on building my real Cloudflare backend? Something that will just log and display incoming POST requests?"*

---

Claude will give you options. Pick one that sounds easy — you're just testing.

---

## What's Next

Phase 6 is building the real thing on the receiving end — a permanent server that accepts your data, and a live dashboard you can open on any device anywhere. By the end of it you'll have a real URL you can open on your phone during a performance.

Open `06-phase-6-dashboard.md` when you're ready.

---

> 💡 **Reminder:** `config.h` should never appear in a `git status` output. If it does, check your `.gitignore` before pushing anything.
