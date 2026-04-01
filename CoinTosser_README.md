# Electronic Coin Tosser

A hardware random binary output using a 555 timer oscillator feeding a D flip-flop. Press and hold a button to start the oscillator, release to freeze — one LED lights: Heads or Tails. No microcontroller, no code.

![TinkerCAD Circuit](tinkercad.png)

🔗 [View & Simulate on TinkerCAD](https://www.tinkercad.com/things/4sfJJk3QaNf-an-electronic-coin-tosser) · 🎥 [Demo Video](https://drive.google.com/file/d/1KQEllmfrdiKHDcCR0U9tdxpBOYMev8sn/view?usp=drive_link)

---

## How It Works

A **555 timer** runs in astable mode at ~690 Hz — far faster than human reaction time. Its output clocks a **74HC74 D flip-flop** wired in toggle mode (Q-bar fed back to D input), which divides the clock by 2 and continuously alternates between HIGH and LOW. Holding the button connects pin 4 (RESET) to VCC, enabling the oscillator; releasing it pulls pin 4 LOW via a pull-down resistor, stopping the clock and freezing the flip-flop at whatever state it held at that exact moment. Since Q and Q-bar are always opposite, exactly one LED is always on.

---

## Specs

| Property | Value |
|---|---|
| Oscillator IC | 555 Timer (astable) |
| Memory IC | 74HC74 D flip-flop |
| Clock frequency | ~690 Hz |
| Trigger | Button release (falling edge on pin 4) |
| Output | 2× LEDs — Q (Heads) and Q-bar (Tails) |
| Supply | 9V battery |

---

## Components

- 555 Timer IC (NE555)
- D flip-flop IC (74HC74)
- Resistors: 100kΩ (R1), 10kΩ (R2), 1kΩ (pull-down), 220Ω ×2 (LEDs)
- Capacitor: 1µF electrolytic
- Push-button (momentary)
- LEDs: 1× red (Heads), 1× green (Tails)
- Breadboard, jumper wires, 9V battery

---

## Lessons Learned

- 74HC74 is rated for 2–6V; running it from 9V risks damaging the IC — a voltage regulator or 74HCT variant is safer
- The Q-bar → D feedback connection is the entire toggle trick — took a while to understand why this creates a divide-by-2 rather than a latch
- Button debounce matters here more than usual; contact bounce can register as multiple clock edges and skew results
- Oscillator frequency has a big effect on randomness — below ~100 Hz you can visibly see the LEDs alternate

---

## Future Improvements

- Add a 5V regulator (7805) to safely power the 74HC logic from the 9V battery
- Add RC debounce on the button to eliminate false clock edges from contact bounce
- Chain 3 flip-flops in toggle mode for an 8-outcome dice roller (3 bits = 0–7)
- Replace the button with a tilt switch for a more coin-like interaction
