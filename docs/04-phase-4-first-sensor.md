# Phase 4 — Adding Your Sensors
### The loop is the same. Now you're building your thing.

---

**What you have coming in:**
- The loop working and understood
- A spec document describing your project
- VS Code, Terminal, git workflow in place
- A BME280 reading temperature, humidity, and pressure

**What you'll have by the end:**
- At least one sensor from your spec wired up and reading data
- An understanding of how multiple sensors can share the same two wires (I2C)
- A habit of using your spec doc as the anchor for every Claude conversation

---

## Start Here: Open Your Spec Doc

Before doing anything else, open your `project-spec.md` and read it. Then open Claude and start your session with this:

---

> Here's my project spec: [paste the full contents of your spec doc]
>
> I've completed Phase 3 of my curriculum — I have VS Code, Terminal, and git set up, and I understand the basic loop. My BME280 is already wired and reading data.
>
> In this phase I want to add the next sensor from my spec. Can you help me figure out which sensor to prioritize, what I need to order if I don't have it, and how to wire it up alongside the BME280?

---

This is the habit from now on: every Claude session starts with your spec. It gives Claude the context it needs to give you answers that are actually about your project instead of generic ones.

---

## What Is I2C and Why Does It Matter

Your BME280 talks to the ESP32 using a protocol called **I2C** (sometimes written I²C, pronounced "I-squared-C"). I2C is a two-wire communication system — SDA and SCL — and the elegant thing about it is that you can connect many sensors to those same two wires at once. They all share the bus.

That's why wiring a second sensor is simpler than it might seem. If your new sensor also uses I2C (most common sensors do), it plugs into the same SDA (GPIO 21) and SCL (GPIO 22) pins you already used. The ESP32 talks to each sensor by its unique address.

Ask Claude to confirm this for your specific sensor:

---

> *"I want to add a [your sensor name] to my ESP32 alongside the BME280. Does this sensor use I2C? If so, can it share the SDA/SCL pins I'm already using, and what is its I2C address?"*

---

If Claude says yes — great, it's just more wires to the same pins. If your sensor uses a different protocol (I2S for audio, SPI for some displays), Claude will explain what that means and how to wire it.

---

## Step 1 — Get Your Sensor

If you don't have the next sensor from your spec yet, order it now and come back to this phase when it arrives. Knowing what you're waiting for is useful — it means you can start reading about it while you wait.

Ask Claude:

---

> *"I'm going to order a [sensor name]. Where's the best place to get it, and are there any versions or breakout boards I should look for specifically? Any I should avoid?"*

---

Good sources: **Adafruit**, **SparkFun**, **Amazon** for common sensors. For more variety or bulk eventually: **Mouser**, **Digikey**, **AliExpress**.

---

## Step 2 — Wire It

When your sensor arrives, before connecting anything, ask Claude for wiring instructions specific to the breakout board you have:

---

> *"I have a [sensor name] breakout board. I already have a BME280 on GPIO 21 (SDA) and GPIO 22 (SCL) sharing 3.3V and GND. Can you tell me exactly how to wire this new sensor alongside it? Please describe which pins on the breakout board connect to which pins on the ESP32."*

---

If you can, find the product page for your specific breakout board (the Adafruit or SparkFun page usually has a clear pinout diagram) and tell Claude which board version you have. The more specific you are, the more accurate the wiring instructions.

Wire it up. Double-check every connection before plugging in USB. Then ask Claude to verify:

---

> *"Here's what I've wired: [describe each connection you made]. Does this look right? Anything to check before I power it on?"*

---

---

## Step 3 — Write the Firmware

Now do the loop. Ask Claude to write firmware that reads from both sensors:

---

> *"Here's my current firmware that reads from the BME280: [paste your existing code]*
>
> Can you update it to also read from the [new sensor name] and print its values to the Serial Monitor alongside the BME280 readings? Please include any library I need to install and tell me how to install it."*

---

Giving Claude your existing firmware means it builds on what's already working instead of starting from scratch — and it keeps the code in one place so you're always working with one file.

Flash it. Open the Serial Monitor. You should see both sensors printing.

---

## Step 4 — Something Goes Wrong (And That's Fine)

It is genuinely normal for the first flash of new sensor code to not work. Common things that happen:

**Library not found error:** Claude told you to install a library but it's not installed yet, or the name is slightly off. Copy the error and paste it back to Claude.

**Sensor not detected / all zeros:** Usually a wiring issue. Check every connection. Make sure the sensor is getting 3.3V (not 5V). Check that SDA and SCL aren't swapped.

**I2C address conflict:** Two sensors sharing the same address. Claude can explain how to change one sensor's address — most breakout boards have a solder pad for this.

In every case, paste the error or describe the symptom to Claude. Be specific: *"The Serial Monitor shows all zeros for the new sensor but the BME280 is still reading fine"* is much more useful than *"it's not working."*

---

## Step 5 — Your First Win ✓

- ✅ At least one sensor from your spec is wired and printing data to the Serial Monitor
- ✅ You understand how I2C lets multiple sensors share the same two pins
- ✅ You used your spec doc at the start of the session
- ✅ You committed and pushed your updated firmware to GitHub

For the commit, from your project folder in Terminal:

```
git add .
git commit -m "add [sensor name] firmware"
git push
```

---

## Going Further In This Phase

If you get your first new sensor working and want to keep going, repeat the process for the next sensor in your spec. Each one follows the same pattern: ask Claude about wiring, wire it, update the firmware to include it, flash, test. The loop doesn't change — the sensors do.

When you have everything from your spec reading data in the Serial Monitor, you're ready for Phase 5.

---

## What's Next

Phase 5 is the moment the project stops being local. You'll connect the ESP32 to Wi-Fi and send your sensor data to a remote endpoint — and watch it arrive on a screen you didn't touch. That's when it starts feeling like a network.

Open `05-phase-5-getting-online.md` when you're ready.

---

> 💡 **Tip:** Save your working firmware to your GitHub repo after every sensor you add. If something breaks when you add the next one, you always have a known-good version to go back to.
