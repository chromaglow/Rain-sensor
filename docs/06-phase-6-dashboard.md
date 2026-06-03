# Phase 6 — The Dashboard
### A live web page at a real URL. Open it on your phone during a performance.

---

**What you have coming in:**
- ESP32 connected to Wi-Fi and posting sensor data as JSON every few seconds
- An understanding of what that JSON looks like
- VS Code, Terminal, git all working

**What you'll have by the end:**
- A permanent server on Cloudflare that receives your sensor data and stores it
- A live dashboard at a real public URL that shows your data updating in real time
- The ability to open that URL on any device, anywhere

---

## How This Works

This phase has two parts that work together:

**Part A — The Worker** (the server side)
A small program running on Cloudflare's infrastructure that listens for incoming data from your ESP32, stores it, and serves it back when the dashboard asks.

**Part B — The Dashboard** (the display side)
A web page that fetches the latest readings from the Worker every few seconds and displays them. This is what you'll open on your phone.

Cloudflare hosts both for free. You don't manage a server, you don't pay for hosting, and it scales automatically if you end up with dozens of sensor units.

> 🛠 **New tool: Cloudflare**
> A platform that runs your server code and hosts your web pages at the edge — meaning your dashboard loads fast from anywhere in the world. The free tier is more than enough for this project.
> **Sign up free at:** cloudflare.com
> **When you use it:** Deploying your Worker and dashboard. Once deployed, it runs on its own.

> 🛠 **New tool: Wrangler**
> Cloudflare's command-line tool. You use it from Terminal to deploy your Worker and dashboard without needing to click through a web interface every time.
> **Install it after setting up Cloudflare below.**
> **When you use it:** Deploying updates to your Worker or dashboard.

---

## Step 1 — Set Up Cloudflare

1. Go to **cloudflare.com** and create a free account
2. Once you're in, you don't need to add a domain or configure anything yet — just having the account is enough for now
3. In Terminal, install Wrangler:

```
npm install -g wrangler
```

4. Log in to Cloudflare from Terminal:

```
wrangler login
```

This opens a browser window asking you to authorise Wrangler. Click Allow. You'll see a success message in Terminal.

---

## Step 2 — Create the Worker

Open Claude with your spec and ask it to build the Worker for you:

---

> Here's my project spec: [paste spec]
>
> I want to build a Cloudflare Worker that does the following:
> - Receives HTTP POST requests from my ESP32 containing sensor data as JSON
> - Stores the latest reading from each unit in Cloudflare KV storage (keyed by a unit ID)
> - Responds to HTTP GET requests by returning all stored readings as JSON so a dashboard can fetch them
> - Has CORS headers so a browser-based dashboard can access it
>
> Please write the Worker code and tell me how to set up the KV namespace and deploy it with Wrangler. I'm a beginner so please include the exact commands to run.

---

Claude will give you a Worker script and step-by-step deployment instructions. Follow them in order. The key steps will be:

1. Create a new Worker project folder
2. Create a KV namespace (where your data gets stored)
3. Paste Claude's Worker code into the right file
4. Deploy with `wrangler deploy`

When it's deployed, Cloudflare gives you a URL like `https://rain-worker.your-username.workers.dev`. Copy it — this is where your ESP32 will send its data from now on.

**Update your ESP32 firmware** to post to this new URL instead of webhook.site:

---

> *"My Cloudflare Worker is deployed at [your worker URL]. Can you update my ESP32 firmware to post sensor data to this new endpoint? The Worker expects JSON with a `unit_id` field so it knows which unit is sending — add a field called `unit_id` with the value `"unit-1"` for now."*

---

Flash the updated firmware and check your Worker is receiving data by opening the Worker URL in a browser — it should return JSON showing your latest readings.

---

## Step 3 — Build the Dashboard

Now ask Claude to build the dashboard:

---

> My Cloudflare Worker is running at [your worker URL] and returning sensor readings as JSON when I visit it in a browser. I can see the data.
>
> Can you build a simple dashboard as a single HTML file that:
> - Fetches from my Worker URL every 5 seconds
> - Displays the latest readings for each connected unit — temperature, humidity, pressure, and any other values I'm sending
> - Shows a timestamp of when each reading was received
> - Works well on a phone screen as well as a desktop
> - Looks clean and simple — nothing fancy, just readable at a glance
>
> Please make it a single self-contained HTML file with all CSS included.

---

Save the HTML file Claude gives you as `dashboard.html` in a new folder in your project called `/dashboard`.

---

## Step 4 — Deploy the Dashboard

You have two options here. Pick whichever feels simpler:

**Option A — Cloudflare Pages (recommended)**
Cloudflare Pages hosts static web pages for free with a real URL.

1. Go to **dash.cloudflare.com → Workers & Pages → Create → Pages**
2. Connect your GitHub account when it asks
3. Select your project repository
4. Set the build output directory to `dashboard`
5. Deploy

Cloudflare builds it and gives you a URL like `https://rain-dashboard.pages.dev`. That's your live dashboard.

**Option B — Deploy from Terminal with Wrangler**

```
wrangler pages deploy dashboard
```

Wrangler will ask you to name the project and then deploy. Same result.

---

## Step 5 — Your First Win ✓

Open your dashboard URL on your phone. Watch the numbers update on their own.

- ✅ Cloudflare Worker is receiving and storing your ESP32's sensor data
- ✅ Dashboard is live at a real public URL
- ✅ Data updates every 5 seconds without refreshing
- ✅ It works on your phone

Take a screenshot. This is the first thing that looks like the finished project.

---

## Going Further in This Phase

Once the basic dashboard is working, there's a lot you can do to make it more expressive. Some things to try — each one is a conversation with Claude:

**Add a map:** If you're going to have units in multiple locations, a map that shows where each unit is adds a lot. Ask Claude to add a simple map using Leaflet.js showing each unit's location.

**Add simple data visualisation:** Even just a colour that changes with temperature or humidity makes the dashboard feel alive. Ask Claude to make a value's background colour shift based on its reading.

**Add a unit name:** Instead of "unit-1" on the dashboard, give each unit a location name. Ask Claude how to add a `location` field to the JSON your ESP32 sends.

Each of these is the loop — describe it to Claude, get code back, deploy it, see what changed.

---

## What's Next

Phase 7 is where it becomes a performance instrument. You'll route your sensor data into your synthesizer — making a real connection between the environmental network and the music. What that looks like depends on what you're using to make sound.

Open `07-phase-7-synth-integration.md` when you're ready — and bring notes on what synthesizer or software you're working with, because Phase 7 is entirely specific to your setup.

---

> 💡 **Tip:** Every time you update your dashboard HTML, redeploy with `wrangler pages deploy dashboard` or push to GitHub if you connected via Pages. The URL stays the same — only the content updates.
