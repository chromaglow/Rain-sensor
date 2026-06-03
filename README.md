# Rain Sensor Network — Learning Curriculum

This is a learning curriculum for building a distributed environmental sensor network using an ESP32 microcontroller. It was made for an artist and musician who wanted to understand how to use AI to write and experiment with hardware code — no prior experience required.

---

## The One Thing You Need to Understand First

There is a single core process that everything in this curriculum is built around. Once you know it, you can build almost anything:

```
Describe what you want → Claude writes the code → Flash it to the ESP32 → See what happens → Change something → Repeat
```

That's it. You're not memorizing code. You're learning how to collaborate with an AI to make hardware do things. The code is the output. The skill is knowing how to describe, test, and iterate.

---

## What's In Here

```
/docs
  00-your-toolkit.md          ← tool reference, open when you need a lookup
  01-phase-1-the-loop.md      ← start here
  02-phase-2-your-project.md
  03-phase-3-environment-setup.md
  04-phase-4-first-sensor.md
  05-phase-5-getting-online.md
  06-phase-6-dashboard.md
  07-phase-7-synth-integration.md
  08-phase-8-scale-deployment.md

/assets
  rain-sensor-project-brief.pdf   ← the project that started all this, for inspiration
```

---

## The Full Arc

Here's where you're going. You don't need to understand all of it now — that's what the map is for.

**Phase 1 — The Loop**
Wire up one sensor. Write firmware with Claude. Flash it. See real data on your screen. Understand the process that everything else is built on.

**Phase 2 — Your Project**
Now that you know the loop, what do *you* want to build? Open conversation with Claude about your own ideas. Define what a first version looks like.

**Phase 3 — Environment Setup**
Install the tools that let you work faster: VS Code, the Terminal, Arduino IDE, and Claude Code. Your computer starts talking to your hardware directly.

**Phase 4 — First Sensor**
Go deeper with the hardware. Add sensors. Understand how they talk to the ESP32. Add something new to your circuit and get it working.

**Phase 5 — Getting Online**
Connect the ESP32 to Wi-Fi and send its data somewhere. Watch your sensor readings appear on a screen you didn't touch.

**Phase 6 — Dashboard**
Build a live web page that shows incoming data from your sensor units. Give it a real URL you can open on your phone.

**Phase 7 — Synth Integration**
Route sensor data into your synthesizer. Make something move. This is where it becomes a performance instrument.

**Phase 8 — Scale and Deployment**
Send units out. Design the experience for someone who receives one with no technical knowledge. Perform.

---

## Before You Open Phase 1

Do this first: **create your own GitHub repository** for your version of this project. That's where your work will live. This repo is the source — yours is where you build.

1. Go to github.com
2. Click **+** → **New repository**
3. Name it whatever feels right
4. Add a README, set it to private or public — your call
5. Create it

Once that's done, open `docs/01-phase-1-the-loop.md` and start there.

---

## Questions

Every phase guide ends with a prompt you can paste directly into Claude. If you get stuck at any point, describe what you're seeing to Claude and ask for help. That's not cheating — that's exactly the skill this curriculum is teaching.

---

*Made by Ezra · github.com/chromaglow/Rain-sensor*
