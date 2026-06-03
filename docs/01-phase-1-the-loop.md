# Phase 1 — The Loop
### Wire one sensor. Write firmware with Claude. Flash it. See real data. Understand the process everything else is built on.

---

**What you have coming in:**
- Claude desktop installed and running
- A GitHub account
- Your own project repository

**What you'll have by the end:**
- An ESP32 wired to a BME280 sensor showing live temperature and humidity on your screen
- A clear understanding of the loop that drives everything in this curriculum

---

## The Loop

Before you touch anything, read this once. This is the single most important thing in the whole curriculum:

```
Describe what you want
       ↓
Claude writes the code
       ↓
You paste it into Arduino IDE and flash it to the ESP32
       ↓
See what happens on your screen
       ↓
Change something, describe it to Claude, repeat
```

That's it. You're not learning to write code from scratch. You're learning to describe what you want clearly, test whether it worked, and iterate. That skill — describe, test, iterate — is what this whole phase is about.

---

## Step 1 — Get the Parts

You need two pieces of hardware. If you don't have them yet, order them now — they're cheap and widely available.

**ESP32-WROOM-32 development board** (~$5–8)
The brain. A small Wi-Fi-enabled computer you can program. Search "ESP32-WROOM-32 dev board" on Amazon, Adafruit, or SparkFun. Any dev board version works — it'll have two rows of pins along the sides.

**BME280 sensor breakout board** (~$3–8)
Measures temperature, humidity, and air pressure. Search "BME280 breakout board I2C." Adafruit, SparkFun, or generic versions all work fine.

**You'll also need:**
- A breadboard (the white grid board that holds components without soldering)
- A few short jumper wires (male-to-male)
- A USB-A to Micro-USB cable (to connect the ESP32 to your computer)

If you're not sure what any of those look like, ask Claude: *"What does a breadboard look like and what is it for?"*

---

## Step 2 — Install Arduino IDE

> 🛠 **New tool: Arduino IDE**
> The software that takes code and sends ("flashes") it onto the ESP32. Think of it like a bridge between what Claude writes and what the hardware does. You don't write code here — you paste Claude's code in and press upload.
> **Download free at:** arduino.cc/en/software
> **When you use it:** Every time you flash new code to the ESP32.

**What to do:**

1. Go to **arduino.cc/en/software** and download the version for your operating system
2. Install it and open it — you'll see a blank editor window
3. Now add ESP32 support (Arduino IDE doesn't know about ESP32 by default):
   - Go to **Arduino IDE → Preferences** (Mac: Arduino IDE menu → Settings; Windows: File → Preferences)
   - Find the field that says **"Additional boards manager URLs"**
   - Paste this in: `https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json`
   - Click OK
4. Open **Tools → Board → Boards Manager**
5. Search for **esp32** and install the one by Espressif Systems
6. Once installed, go to **Tools → Board → ESP32 Arduino** and select **ESP32 Dev Module**

If anything in those steps doesn't work, describe exactly what you see to Claude and it will walk you through it.

---

## Step 3 — Wire It Up

Plug your ESP32 into the breadboard (straddle it across the center gap so the pins go into holes on both sides). Then connect the BME280 using four jumper wires:

| BME280 pin | ESP32 pin |
|-----------|-----------|
| VIN or VCC | 3.3V |
| GND | GND |
| SDA | GPIO 21 |
| SCL | GPIO 22 |

The pins on the ESP32 are labeled. Look for the tiny text printed along the sides — 3V3, GND, 21, 22. If the text is too small, search "ESP32-WROOM-32 pinout" in Google Images and zoom in — there are clear diagrams showing where every pin is.

**Before moving on:** Ask Claude to double-check your wiring. Describe what you've done:

> *"I've wired a BME280 to an ESP32. VIN goes to 3.3V, GND to GND, SDA to GPIO 21, SCL to GPIO 22. Does that sound right? Anything I should check before powering it on?"*

---

## Step 4 — Write the Firmware With Claude

Now you're going to do the loop for the first time. Open Claude and paste this in:

---

> I have an ESP32-WROOM-32 wired to a BME280 sensor. SDA is on GPIO 21, SCL is on GPIO 22. I'm using Arduino IDE.
>
> Can you write me firmware that:
> - Reads temperature, humidity, and air pressure from the BME280 every 2 seconds
> - Prints those values to the Serial Monitor so I can see them on my screen
> - Includes comments explaining what each section does
>
> Please also tell me if I need to install any libraries before running this, and how to install them.

---

Claude will give you a block of code and probably tell you to install a library (the BME280 library). Follow those instructions first, then:

1. Copy the code Claude gives you
2. Open Arduino IDE
3. Select all the default text in the editor and delete it
4. Paste Claude's code in
5. Plug the ESP32 into your computer via USB
6. Go to **Tools → Port** and select the port that appeared when you plugged in the ESP32 (it'll be something like `/dev/cu.usbserial...` on Mac or `COM3` on Windows)
7. Click the **Upload** button (the arrow pointing right →)
8. Wait for it to say "Done uploading"
9. Open **Tools → Serial Monitor**, set the baud rate to **115200** in the bottom right dropdown
10. Watch your data appear

---

## Step 5 — Your First Win ✓

You should see something like this scrolling in the Serial Monitor:

```
Temperature: 21.4 °C
Humidity: 58.2 %
Pressure: 1013.1 hPa

Temperature: 21.5 °C
Humidity: 58.1 %
...
```

Real data. From a real sensor. That you wired and programmed.

That's the loop. You described what you wanted, Claude wrote the code, you flashed it, and you can see it working. Every single thing you build from here uses this exact same process — just with more complexity added one piece at a time.

**If it didn't work:** Don't skip ahead. Tell Claude what happened — copy any error messages you see and paste them in. Error messages look scary but they're just information. Claude will tell you what they mean and how to fix them.

---

## Step 6 — Change Something

Now that it's working, do the loop one more time — not because you need to, but because doing it twice is how you understand it's a process, not a trick.

Ask Claude:

> *"The firmware is working and I can see temperature, humidity, and pressure in the Serial Monitor. Can you modify it to also print a simple message like 'Reading...' before each set of values, and add the current reading number so I can see how many readings have happened?"*

Paste the new code in, flash it, see the change. That's iteration.

---

## What's Next

You've proven the loop works. In Phase 2, you step back from the hardware for a bit and have a bigger conversation with Claude — about your own artistic vision, what you actually want to build, and what a first real version of your project looks like. The sensor options, the data streams, the performance setup — all of that is yours to define.

To kick off Phase 2, open a fresh Claude conversation and paste this in:

---

> I've just completed my first hardware loop — I wired an ESP32 to a BME280 sensor, wrote firmware with Claude's help, flashed it, and I can see live temperature, humidity, and pressure data on my screen. I understand the process now.
>
> I want to step back and think about what I actually want to build. I'm an artist and musician. I have a project in mind involving environmental sensors feeding data into a live music performance — but I haven't made any firm decisions yet about which sensors to use, what the data should do, or what a first version looks like.
>
> Can you help me think through what I want to build? I'd like to start by exploring what kinds of environmental data feel interesting or meaningful to me as a musician, and then work toward defining a simple first version.

---

*Open `02-phase-2-your-project.md` when you're ready.*

---

> 💡 **Toolkit reminder:** If you encounter a tool name you don't recognise in this phase, check [`00-your-toolkit.md`](00-your-toolkit.md) for a quick lookup.
