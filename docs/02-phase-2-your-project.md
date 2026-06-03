# Phase 2 — Your Project
### Stop following instructions. Start making decisions.

---

**What you have coming in:**
- The loop: you can describe something, have Claude write the firmware, flash it, and see results
- A working ESP32 + BME280 reading environmental data
- No idea yet what you actually want to build — and that's exactly right

**What you'll have by the end:**
- A clear description of your own project in your own words
- A defined MVP — the simplest version that would still feel real and meaningful
- A spec document you wrote with Claude that will guide everything from Phase 3 onward

---

## This Phase Is Different

Every other phase in this curriculum is about *doing* something — wiring, flashing, deploying. This one is about *deciding* something. There are no steps to follow. There's just a conversation with Claude that you steer.

That might feel uncomfortable if you're used to following instructions. Sit with it. The discomfort is part of it.

---

## Step 1 — Read the Project Brief With Claude

In the `/assets` folder of this repo there's a PDF called `rain-sensor-project-brief.pdf`. Download it and read through it — not to understand every technical detail, but to get a feel for the *scale* and *ambition* of one version of this kind of project.

Then open Claude and share it:

---

> I'm going to share a project brief with you for an environmental sensor network — a global network of handbuilt units that capture rain, temperature, humidity, and pressure data and stream it into a live music performance. I didn't write this. I'm reading it as inspiration.
>
> Can you read it and then help me think about what parts of this feel exciting or resonant to me as a musician — and what parts feel like someone else's idea? I want to figure out what *my* version of something like this would look like.

---

Attach the PDF and send it. Don't rush the conversation that follows. Ask follow-up questions. Push back if something doesn't feel right. This is a thinking session, not a briefing.

---

## Step 2 — Explore What Data Feels Interesting

Once you've talked through the brief, shift the conversation toward your own instincts. There's no right answer here — you're an artist, trust what you find interesting.

Some prompts to try if the conversation stalls:

---

> *"What kinds of environmental data do you think would be most interesting to a musician? Not technically — emotionally or texturally."*

---

> *"If I could only use one sensor to influence my music in real time, what would make the most interesting choice and why?"*

---

> *"What's the difference between data that would be useful as a control signal versus data that would just be noise?"*

---

> *"I want the sensor data to feel like it's shaping the music, not just triggering things. What does that distinction mean technically?"*

---

You don't have to use these exact prompts. They're just doors. Walk through whichever ones feel relevant.

---

## Step 3 — Define Your MVP

At some point in the conversation, Claude will probably start reflecting back what you seem to care about. Pay attention to that. When it feels close, ask:

---

> *"Based on everything we've talked about, what would you say the simplest version of my project is that would still feel meaningful? Can you describe it in one paragraph?"*

---

Read what it says. Edit it. Push back on anything that doesn't sound like you. Keep going until the paragraph sounds like something you'd actually say to someone at a show.

That paragraph is your MVP definition.

---

## Step 4 — Write Your Spec Document

Now you're going to turn that MVP definition into a short spec document — a written plan that you'll use in every phase from here on to tell Claude exactly what you're building.

Ask Claude to help you write it:

---

> *"Can you help me write a short spec document for my project based on what we've talked about? It should cover: what the project does in plain language, what hardware I'll need, what the data flow looks like from sensor to performance, and what the first version needs to do to count as working. Keep it short — this is something I'll read at the start of every Claude conversation to give context."*

---

Once Claude produces a draft, read it carefully. It should feel like *your* project, not a generic hardware project. Edit anything that doesn't fit. Add anything that's missing.

When it feels right, save it as a new file in your own GitHub repo — call it something like `project-spec.md`. This document will live at the root of your repo alongside your README.

---

## Step 5 — Your First Win ✓

You've done something harder than wiring a sensor: you've made decisions.

- ✅ You've read the project brief and figured out what resonates vs. what doesn't
- ✅ You have an MVP definition in your own words
- ✅ You have a spec document saved in your repo

From now on, every conversation you start with Claude begins with: *"Here's my project spec — [paste it]. Now I want to..."* That single habit will make every phase go faster and produce better results.

---

## What's Next

Phase 3 is about upgrading your working environment — installing tools that let you work faster and give Claude more direct access to your project. VS Code replaces pasting code by hand. The Terminal lets you run commands directly. Claude Code turns Claude from a chat window into an agent that can write, edit, and manage your actual files.

When you're ready, open `03-phase-3-environment-setup.md`.

---

> 💡 **Note:** There's no seed prompt for Phase 3 — it starts with a tool install, not a Claude conversation. Just open the next doc and follow the steps.
