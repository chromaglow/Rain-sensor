# Phase 7 — Synth Integration
### Make a sensor value move something in your performance setup. This is where it becomes music.

---

**What you have coming in:**
- Live sensor data flowing from ESP32 → Cloudflare Worker → Dashboard
- A real URL showing live environmental readings
- A working understanding of the loop

**What you'll have by the end:**
- At least one sensor value controlling at least one parameter in your synthesizer or performance software
- A working bridge between your data network and your instrument
- A clear picture of how to expand the connection as your project evolves

---

## This Phase Is Yours

Every other phase had a clear right answer — wire it this way, use this tool, run this command. This phase doesn't. What you build here depends entirely on what you make music with, and no two setups are identical.

What this guide does is explain the concept, show you the two main technical paths, and give you the prompts to let Claude figure out the specifics for your situation. You steer. Claude builds.

---

## The Bridge Concept

Your sensor data is sitting in Cloudflare — a server on the internet. Your synthesizer is a physical or software instrument on your computer or desk. Those two things don't talk to each other by default. You need a **bridge**: a small program running on your computer that pulls data from Cloudflare and translates it into a signal your synth understands.

```
ESP32 → Wi-Fi → Cloudflare Worker → Bridge (on your computer) → Synthesizer
```

The bridge is usually a short Python or JavaScript script. Claude writes it. You run it in Terminal. It sits quietly in the background, fetching new readings every few seconds and sending them to your instrument.

---

## Step 1 — Tell Claude What You're Working With

Before writing any code, have an honest conversation with Claude about your setup. Open Claude with your spec and ask:

---

> Here's my project spec: [paste spec]
>
> I've reached the point where I want to route my sensor data into my music setup. Here's what I'm working with: [describe your setup as specifically as you can — software synths, hardware synths, DAW, modular gear, anything relevant]
>
> My sensor data is currently available as JSON from a Cloudflare Worker at [your worker URL]. Can you help me figure out the best way to get that data into my setup? What protocol makes the most sense — MIDI, OSC, something else — and what does the bridge program look like?

---

Be as specific as you can about your setup. "I use Ableton with a hardware synth" and "I use a modular system and Max/MSP" will produce very different answers. Both are right — Claude just needs to know what it's working with.

---

## The Two Main Paths

Depending on what you use, Claude will likely point you toward one of these:

---

### Path A — OSC (for software instruments)

**OSC** (Open Sound Control) is a protocol designed for sending data between music software. If you use Ableton, Max/MSP, SuperCollider, VCV Rack, TouchDesigner, or most other software environments, OSC is almost certainly the right choice.

The bridge is a Python script that:
1. Fetches your latest sensor readings from Cloudflare every few seconds
2. Maps the values to a range your synth expects (e.g. temperature 0–40°C → 0.0–1.0)
3. Sends them as OSC messages to a port your software is listening on

Ask Claude:

---

> *"Can you write a Python script that fetches sensor data from [your worker URL] every 3 seconds and sends the values as OSC messages to localhost port 8000? I want temperature mapped to /sensor/temperature, humidity to /sensor/humidity, and [any other values] to their own paths. Please include how to install the required libraries."*

---

Then in your software, create an OSC receiver listening on that port. In Max/MSP this is a `udpreceive` object. In Ableton with Max for Live, there are OSC devices. In SuperCollider it's `OSCdef`. Claude can tell you exactly what to set up in your specific software:

---

> *"I want to receive OSC messages in [your software]. Can you show me how to receive messages on port 8000 and route `/sensor/temperature` to control [a specific parameter]?"*

---

### Path B — MIDI (for hardware synths and DAWs)

If your main instrument is a hardware synthesizer, or if your DAW workflow is built around MIDI, sending MIDI Control Change (CC) messages is probably the cleaner fit.

The bridge script in this case:
1. Fetches sensor readings from Cloudflare
2. Maps values to MIDI CC range (0–127)
3. Sends MIDI CC messages to a virtual MIDI port your synth or DAW can receive

Ask Claude:

---

> *"Can you write a Python script that fetches sensor data from [your worker URL] every 3 seconds and sends the values as MIDI CC messages? Map temperature to CC 1, humidity to CC 2, and [any other values] to sequential CCs. Use a virtual MIDI port so my DAW/synth can receive it. Include library install instructions."*

---

On Mac, you may need to create a virtual MIDI port in **Audio MIDI Setup** (search for it in Spotlight). On Windows, you'll need **loopMIDI** (free). Claude will walk you through whichever applies.

---

## Step 2 — Run the Bridge

Once Claude gives you the bridge script:

1. Save it as `bridge.py` in your project folder
2. Install the required libraries — Claude will tell you exactly what to run in Terminal
3. Run it:

```
python3 bridge.py
```

Leave Terminal open with the bridge running. You should see it printing something like `Sent: temperature=21.4` every few seconds. That means it's fetching and sending.

Now go to your instrument or software and confirm the signal is arriving. Assign it to something — a filter cutoff, a reverb amount, a sample playback speed. Anything. Move the sensor (breathe on it, hold it near a heat source) and watch the parameter respond.

---

## Step 3 — Your First Win ✓

- ✅ The bridge script is running in Terminal
- ✅ At least one sensor value is controlling at least one parameter in your setup
- ✅ You can influence your sound by changing the environment around the sensor

That's the connection. The planet is starting to play your instrument.

---

## Step 4 — Map It Intentionally

Getting *a* signal into your synth is the first win. Making it *musical* is the next iteration. Once the connection is working, have a deeper conversation with Claude about mapping:

---

> *"My temperature sensor is controlling [parameter] in my setup. The values I'm getting range roughly from [min] to [max]. Right now the mapping feels [too subtle / too jumpy / not musical]. Can you help me adjust the bridge script to make the mapping feel more expressive? I want [describe what you want it to feel like]."*

---

This is where the artistic decisions start compounding. Logarithmic vs linear mapping. Slew limiting (smoothing sudden jumps). Threshold gates (only react if a value crosses a point). Averaging over multiple readings. Claude knows all of these — you just have to describe what you want the music to do.

---

## Step 5 — Make the Bridge Start Automatically

Right now you have to remember to run `python3 bridge.py` in Terminal before every session. That's fine for development, but annoying for performance. When you're ready to make it more reliable, ask Claude:

---

> *"Can you help me make my bridge script start automatically when my computer boots, so I don't have to run it manually before every performance? I'm on [Mac / Windows]."*

---

Claude will give you the right approach for your OS — a Launch Agent on Mac, a Startup Task on Windows.

---

## What's Next

Phase 8 is about scale and deployment — sending units out into the world, designing the experience for someone who receives one with no technical knowledge, and preparing for a live performance with the full network.

Open `08-phase-8-scale-deployment.md` when you're ready.

---

> 💡 **Performance tip:** Before any live use, test the full chain — ESP32 powered, bridge running, instrument connected — and leave it running for an hour. You want to know now if anything drops or drifts, not during a show.
