# Ushering Chapter 1

A short conversation game for store staff (APCs). It is **mandatory**: staff play it before the LMS opens.
There is no Later button and no close button.

Customers walk into the store one at a time and stop in front of the player, who is the APC at the entrance.
Some speak (a speech bubble), some say nothing (a "…" bubble). The player picks the best reply from four.
Every answer, right or wrong, shows a line from Ushering Chapter 1 in Chapter 1's own words, with its page.
A round is 6 customers, then a confetti burst with "You have successfully cleared this level." and the end card.

It takes about 1½ minutes. The first visit adds one practice customer, so about 2 minutes.
English only. No sound. No glasses product facts. Nothing from Chapters 2 and 3.

## What the player sees

1. **Start screen.** The name, Ushering Chapter 1, the usher definition (Chapter 1 p.4), "Notice them. Welcome them.
   Help them begin." (p.3) and **Start**.
2. **First visit on this device only: practice.** A short card ("PRACTICE · NOT SCORED"), **Got it**, then one practice
   customer with coach lines in the yellow strip ("A customer is walking in.", "She said something. Tap your best reply.").
   Not scored. Then "Now the real round. 6 customers." (it stays at least 2.5 seconds, even when the first customer of the
   round is a silent one).
3. **The round.** 6 customers: 4 who speak and 2 who say nothing, drawn from a set of 9, in a new order every round.
   The four replies are in a new order every time.
   Each customer walks in from the glass door and stops in front of the player. Two of them are already on the floor:
   one half turned to the signs (he turns to face the player when the replies appear), one side-on at the headphone
   shelf (he turns to the player once he has been helped).
   One is a family of three who walk in together. A short scene line under the signs says what else is happening, for
   those four. A silent customer gets "She isn't saying anything. What would you do now?" at once (He, or No one for the
   family); the first silent customer of a visit adds "Not every customer talks. Pick what you would do."
4. **Hints, for every customer, every round.** The hint clock starts when all four replies are on screen; the bulb at the
   top fills.
   - **5 seconds:** one wrong reply is crossed out and a hint question shows. The bulb lights. No marks lost.
   - **10 seconds:** the right reply glows, the others dim, a hand points at it and its Chapter 1 line types out word by word
     (about 2.5 words a second). "Tap it to go on". Only the lit reply responds. No marks for this customer.
5. **A wrong reply** turns red, the other two step aside, and the Chapter 1 line it breaks shows under it ("A do-not of
   ushering · p.11", for example). The right reply lights up; the player taps it, it turns green with its line, then
   **Next customer**. The lit reply answers taps 0.7 seconds after the wrong one, and Next customer 0.6 seconds after it
   appears, so a double tap cannot skip the red card or the green one.
   **A right reply** turns green with "Right first time" (or "Right" after the 5-second hint) and its Chapter 1 line.
   Nothing moves on by itself. If Next customer is not tapped in 4 seconds, it pulses. A tap on the customer or the floor
   while the replies are up shows "Tap one of the four replies." While the answer is lit, a tap anywhere else (the floor,
   or a dimmed reply) gives the "Tap it to go on" pill a small shake.
6. **End of the round:** confetti over the whole screen (about 2.5 seconds) and a centred card, "You have successfully
   cleared this level." About 2 seconds later (or on a tap) the end card slides in under the last of the confetti, with
   the same sentence on top:
   score, 1 to 3 stars, a line, how many were right, how many hints were used, one line **To remember**,
   **Play again** and **Enter LMS**.

The customers: practice = a young woman (TV). A student (laptop), a woman with a fan (smartphone; the phone promoter is
walking over), a young man who is not sure yet, an elderly lady (washing machine), a retired gentleman (just browsing)
speak. A young woman in a teal kurta with a tote bag, a man in a checked shirt reading the signs, a family of three, and a
teenager at the headphone shelf say nothing. No names on screen. Nobody wears glasses (glasses are the product).

## Files

| File | What it is |
| --- | --- |
| `ushering-ch1.html` | The game. One file with everything inside: styles, script and art (about 170 KB). |
| `demo.html` | A plain sample LMS page with the mandatory gate in front of it. Open it in a browser to try it. |
| `README.md` | This file. |
| `content.json` | The approved questionnaire, word for word. The game carries a copy of it (see "Change the texts"). |
| `shots/` | Screenshots at 300 x 360, 320 x 400, 390 x 844 and 1280 x 800: start, practice, a customer speaking, the 5-second hint, the 10-second answer, a wrong reply, a right reply, a silent customer, the confetti moment, the end card. Plus the gate on desktop and on a phone. |

Upload `ushering-ch1.html` to a place your LMS can serve a web page. The same server as the LMS is best.

## Try the demo

Open `demo.html`. The gate covers the page at once. Play a round and tap Enter LMS: the gate fades away.
Reload the page: it goes straight in, because the round is done for today.

**Reset demo** (bottom right, marked "Demo only") clears today's pass and the game's saved flags,
so the gate and the practice customer show again. It is only for testing. Do not copy it into the LMS.

It works best from a web server. It also works as a local file in Chrome.

## Add the gate to your LMS

The idea: when the page loads, cover it with the game. When the game says `enter`, remove the cover.

1. Wrap your LMS page in one element, for example `<div id="lms-root">`.
2. When the user still has to play, render the page with `<html class="uc-gated">` and the gate below, right after `<body>`.
   (Rendering the class on the server means the LMS never flashes before the gate.)
3. When the user does not have to play, leave all of this out. The game is then not loaded at all.

```html
<style>
  html.uc-gated, html.uc-gated body { overflow: hidden; height: 100%; }
  html.uc-gated body { position: fixed; left: 0; right: 0; top: 0; }
  html.uc-gated #lms-root { filter: blur(6px); pointer-events: none; }
  #uc-gate { position: fixed; inset: 0; z-index: 2147483000; display: flex; align-items: center;
             justify-content: center; background: rgba(16, 12, 52, .58); transition: opacity .4s; }
  #uc-gate.leaving { opacity: 0; }
  #uc-frame { width: 320px; height: 400px; border: 0; border-radius: 22px; background: #5B4BDB; }
  @media (max-width: 600px), (max-height: 440px) {
    #uc-frame { width: 100%; height: 100%; border-radius: 0; }   /* phones: full screen */
  }
</style>

<div id="uc-gate" role="dialog" aria-modal="true" aria-label="Play Ushering Chapter 1 to enter the LMS">
  <iframe id="uc-frame" src="ushering-ch1.html" title="Ushering Chapter 1 game"></iframe>
</div>

<!-- at the end of <body> -->
<script>
(function () {
  var gate = document.getElementById('uc-gate');
  var frame = document.getElementById('uc-frame');
  var lms = document.getElementById('lms-root');
  var html = document.documentElement;
  if (!gate) return;

  html.classList.add('uc-gated');
  lms.setAttribute('inert', '');      // nothing behind the gate can be clicked or tabbed to
  frame.focus();                      // so the keyboard works at once

  function noEsc(e) { if (e.key === 'Escape') e.preventDefault(); }
  document.addEventListener('keydown', noEsc, true);

  window.addEventListener('message', function (e) {
    if (e.source !== frame.contentWindow) return;          // only messages from the game
    var d = e.data;
    if (!d || d.type !== 'ushering-ch1') return;
    if (d.event === 'complete') {
      // Send it to your server here: d.score (0 to 100), d.stars (1 to 3), d.right (0 to 6), d.hints, d.round.
    }
    if (d.event === 'enter') {
      document.removeEventListener('keydown', noEsc, true);
      lms.removeAttribute('inert');
      html.classList.remove('uc-gated');
      gate.classList.add('leaving');
      setTimeout(function () { gate.remove(); }, 400);     // also stops the game
    }
  });
})();
</script>
```

`demo.html` does the same and adds a few extras you can copy:
a line of text above and under the game on desktop, a focus loop that keeps the keyboard inside the gate (it tells the game
which edge Tab wrapped from, with `{type: 'ushering-ch1-focus', edge: 'start' | 'end'}`, so focus lands on the game's last
or first control), the "once a day" memory in the browser, a small "Ushering Chapter 1 done today" note on the LMS page,
and the demo-only reset.

If the game is on a different web address than the LMS, also check `e.origin` against the game's address.

## How often to show it

The LMS decides. Pick one:

- **Every login.** Show the gate every time the user logs in.
- **Once a day.** Show the gate if the user has no `complete` recorded today. This is what `demo.html` does, to show the idea.
- **Once ever.** Show the gate until the user's first `complete` is recorded.

**Our advice for this version: once a day at most, or a few times a week.** A round draws 6 of 9 customers in a new order
with the replies shuffled, but the set is small: a player who plays every login will soon know every answer.

Decide it on the LMS server if you can. `demo.html` keeps the date in the browser (local storage) only to show the idea.
To try each one: `demo.html?gate=login`, `demo.html?gate=day`, `demo.html?gate=ever`.

## Sizes

- Smallest: 300 x 360 px.
- Best: 320 x 400 px, or larger in the same shape (4:5). It scales up cleanly.
- Other shapes work too. The spare space is filled with the game's violet.
- Phones: full screen, the game fills the width. `demo.html` switches to full screen below 600 px wide (or 440 px tall).

The game is drawn at 320 x 400 and scaled to fit. Every reply is a full-width button, 40.5 px tall on the design.
Measured on screen:

| Window | Game | One reply | Next customer | Enter LMS, Play again | Start |
| --- | --- | --- | --- | --- | --- |
| 300 x 360 (smallest) | 288 x 360 | 270 x 36.5 px | 36 px | 37.8 px | 39.6 px |
| 320 x 400 | 320 x 400 | 300 x 40.5 px | 40 px | 42 px | 44 px |
| 390 x 844 (a phone) | 390 x 488 | 366 x 49.4 px | 48.8 px | 51.2 px | 53.6 px |
| 1280 x 800 (desktop) | 640 x 800 | 600 x 81 px | 80 px | 84 px | 88 px |

At 300 x 360 a reply is 36.5 px tall. That is the approved design (four full-width replies under the store scene, at
least 40 px on the 320 x 400 design); the buttons are the full width of the game, so they are easy to hit. On a phone they
are 49 px. The close X (only with `?close=1`) is drawn small, but it answers taps in a square of 45 px at 300 x 360
(60 px on a phone).

## URL options

Add these to the game's address, for example `ushering-ch1.html?pass=60`.

| Option | What it does |
| --- | --- |
| `?pass=60` | Below 60% the end card offers only "Play again", with the line "Score 60% or more to enter. Play again." Without it, any finished round can enter. Use with care: a high bar can keep staff out of work. A round below the pass mark has not cleared the level, so it skips the confetti and "You have successfully cleared this level." and goes straight to the end card (no headline, and no 1-star line, so "Play again" is not repeated). At or above the pass mark it gets the confetti and the sentence as usual. |
| `?practice=always` | Always show the practice customer first (start of the visit only; Play again never repeats it). |
| `?practice=never` | Never show the practice customer. |
| `?close=1` | Shows a close X that sends `close`, on the start screen and in the top bar during play. Only for a later, optional (not mandatory) use. Do not use it in the gate. |
| `?shuffle=0` | For testing only: always customers A, B, C, D, F, G in that order, replies in the questionnaire's order. |
| `?seed=42` | For testing only: the same "random" rounds and reply orders every time for the same number. |

`demo.html` passes `?pass`, `?practice`, `?shuffle` and `?seed` on to the game, for testing: `demo.html?pass=60&practice=always`.

## Events (postMessage)

The game sends these messages to the page that holds it (`window.parent`):

| Message | When |
| --- | --- |
| `{type: 'ushering-ch1', event: 'start'}` | The player tapped Start. |
| `{type: 'ushering-ch1', event: 'complete', score, stars, round, right, hints}` | The player tapped Enter LMS on the end card. `score` is 0 to 100, `stars` 1 to 3, `right` how many of the 6 customers were right, `hints` how many hints showed (5-second hints and lit answers), `round` counts the rounds played since the game opened (1, 2, ...). |
| `{type: 'ushering-ch1', event: 'enter'}` | Right after `complete`. Remove the gate. |
| `{type: 'ushering-ch1', event: 'close'}` | Only with `?close=1`. The gate ignores it. |

The messages carry no personal data. Check `e.source === iframe.contentWindow` so you only act on messages from the game.

## Score

- Each customer: 100 if the player picks the right reply before the answer is lit (with or without the 5-second hint),
  0 for a wrong reply or once the answer is lit at 10 seconds.
- Round score: the average of the 6, rounded (5 of 6 right = 83%).
- Stars: 3 when all 6 are right, 2 for 4 or 5 right, 1 otherwise. The line: 3 stars "Every customer got a good start.",
  2 stars "Good welcomes. A few slips.", 1 star "Play again. The hints will help."
- "Hints used" counts the 5-second hints and the lit answers, for information. The silent-customer line and the practice
  coach lines are not hints.
- **To remember:** the Chapter 1 line of the first miss (for a wrong reply, the line it breaks; for a lit answer, the
  right reply's line). With no miss, it takes turns: "Notice them. Welcome them. Help them begin." (p.3), "Customer first.
  Product later." (p.5), "A good first interaction makes the customer feel welcome — not sold to." (p.5).
- The practice is not scored.

This version has no SCORM. To keep scores in the LMS, listen for `complete` and save it on your server.
The game keeps the best score, whether the practice was done, and which "To remember" line is next in the browser's
local storage (`usheringCh1.best`, `usheringCh1.practiced`, `usheringCh1.remIdx`). It still works if storage is blocked;
it just shows the practice again.

## How strict is the gate? (please read)

The gate runs in the browser. It stops normal use: there is no button, link or key that gets past it.
But someone who knows how can get past it, for example with the browser's developer tools
(remove the cover, or send a fake `enter` message).
Clearing browser storage does not help them: it only makes them play again.

For real enforcement, record the `complete` event on the LMS server, with the user and the time,
and let the server decide whether to show the gate. Even then, a determined user could fake the message.
Treat the game as a training step, not an exam.

Also:
- Esc does nothing in the game or the gate. Inside the gate the browser's Back button leaves the page as usual (the game
  adds no history entry there); the gate shows again on the next visit until a round is done. Opened on its own as a
  pop-up (not in a frame), the game holds the first Back press so it is not closed by accident.
- If the game file cannot load, the gate stays up. Keep a quick way to switch the gate off on the server.

## Offline and fonts

The game works without internet once the page is open. It asks Google Fonts for Poppins. The request does not hold the
game up: if it fails or hangs, the game starts at once with the device's own font (every screen was checked with a
fallback font too). Nothing else is loaded from outside. There are no sound files and no sound.
`demo.html` loads nothing from outside.

## Browser support

- Desktop: current Chrome, Edge, Firefox and Safari.
- Phones: Chrome on Android, Safari on iPhone.
- Internet Explorer is not supported.
- `inert` (which blocks the page behind the gate) needs Chrome 102, Safari 15.5 or Firefox 112 or newer.
  On older browsers the cover still blocks clicks.

## Keyboard, screen readers, motion

- Tab and Shift+Tab move through the replies and buttons; Enter or Space chooses; the keys 1 to 4 choose a reply (top to
  bottom). The focus ring is always visible. Focus moves to the lit reply after a wrong answer and to Next customer after
  an answer, so a keyboard player never has to hunt for it. Esc never exits.
- The replies are real buttons with their text. A screen reader hears each customer's line (or that they say nothing),
  the hints, the lit answer, the feedback with its Chapter 1 line, the cleared sentence and the end card.
- Reduced motion: customers fade in and out instead of walking, the replies fade in instead of sliding, the lit line types
  word by word as usual (it is text, not motion), and the confetti is a still scatter that fades. Next customer still
  pulses after 4 seconds, by changing colour instead of growing, and the "Tap it to go on" pill flashes instead of
  shaking. The timings are the same.
- A hidden tab pauses the game, including the hint clock: no hint ever fires while the player is away.
- No scrolling, zoom, text selection, long-press menu or pull-to-refresh.

## Change the texts

Open `ushering-ch1.html` in a text editor. All the words are near the top of the script:

- **`CONTENT`** is `content.json`, the approved questionnaire, word for word: the Chapter 1 lines with their pages
  (`ch1`), the practice customer and customers A to I (what they say, the silent line, the scene line, the four replies,
  which one is right, the Chapter 1 line and label shown after each reply, the reply crossed out at 5 seconds and the
  5-second hint question). If the questionnaire changes, paste the new `content.json` over this block.
- **`UI`** holds the other words on screen (start screen, practice card, coach lines, buttons, end card), all from the
  approved overview.
- **`TIMING`** holds the timings (walk-in 1.5 s, hint 5 s, answer 10 s, typing speed, confetti, and the short waits that
  stop a double tap: `wrongArm` 0.7 s, `nextArm` 0.6 s, `endArm` 0.6 s; `roundCoach` 2.5 s).

Rules when editing:
- Change only the text inside the quotes. Keep the commas and brackets.
- No exclamation marks. Never "solutions". No glasses product facts, no store names. English only.
- The Chapter 1 lines (`ch1` and every option's `line`) are Chapter 1's exact words. Change them only if Chapter 1 changes.
- "Ray-Ban Meta" appears only where Chapter 1 has it (two replies and three Chapter 1 lines).

Save, then open `demo.html` to check.

## Content source

Ushering · Level 1 · Chapter 1, "Ushering Foundations" (12 pages) only, through the approved questionnaire
(`content.json`, from `overview/content.py`) and the approved overview (`doc/Ushering-Chapter-1-Game-Overview.pdf`).
Every reply is tied to one Chapter 1 line: a part of ushering (p.3) or the Say line (p.5) for a right reply; one of the
seven do-nots (p.6 to 12), the Don't say line (p.5), "Don't assume…" (p.2) or a missed part of ushering (p.3) for a wrong one.

## Testing done

Headless Chrome, driven over the DevTools protocol, with window sizes set by device emulation, at 300 x 360, 320 x 400,
390 x 844 (mobile, touch) and 1280 x 800:

- A full first visit at each size with real taps or clicks: Start, the practice card, the practice customer with the real
  5-second hint (measured 4.98 to 5.02 s) and the real 10-second answer (9.96 to 10.04 s), the line typing out, a tap on
  the crossed-out and on a dimmed reply (ignored), Next customer pulsing after 4 s; then a round mixing a right reply, a
  wrong reply then the lit one, a right reply after the 5-second hint, a lit answer, a tap on the scene ("Tap one of the
  four replies.") and silent customers (with the first-visit extra line); the confetti and the cleared card; the end card
  numbers (4 of 6 right, 67%, 2 stars, 3 hints used, the first miss as To remember); Enter LMS (`complete` then `enter`);
  Play again (round 2, no practice).
- Keyboard only: Tab to Start, Enter, Space, the keys 1 to 4, Tab and Shift+Tab through the replies, focus on the lit
  reply and on Next customer, Enter LMS and Play again; Esc ignored.
- `?practice=never` and `always`, the returning-visit text (about 1½ minutes), `?shuffle=0` (A, B, C, D, F, G, replies in
  order), `?seed` (repeatable, different seeds differ), 300 random rounds (always 4 speakers and 2 silent, all 9 used),
  `?pass=60` (50%: only Play again with the line; 67%: Enter LMS), `?close=1` (the X fits and sends `close`).
- Every customer with every wrong reply, after the 5-second hint, and lit: nothing overflows, the hand never covers the lit
  reply's text, the pill stays on screen; with Poppins and with a fallback font.
- Reduced motion; a hidden tab (the hint clock stops and resumes without a jump); the Back guard when opened on its own.
- `demo.html` as the gate on desktop and phone: blocked until Enter LMS, Esc and clicks outside do nothing, the focus loop,
  the "done today" note, a same-day reload goes straight in, options passed through.
- No console errors. No "!" on any screen.
- After three playtests (a newcomer, QA, content), a second pass with real taps on a phone (390 x 844, touch) and at
  300 x 360: double taps on a wrong reply 0.15 to 0.68 s apart (the red card always stays; a tap 0.83 s later goes on),
  Next customer tapped 0.3 s after it appears (ignored) and 0.75 s (goes on), "Now the real round." held 2.5 s before
  each silent first customer (G, I, H, F) and 3 s before a speaking one, a tap on a dimmed reply while the answer is lit
  (the pill shakes), confetti gone 2.6 s after the round ends, reduced motion (Next customer changes colour at 4 s),
  the close X's hit area (45 px at 300 x 360), and every customer in every state with no overlaps.

- Final pass (13 November 2026): the `?close=1` X now also works on the start screen; a round below `?pass` skips the confetti and the cleared sentence; customer A stands 5 px lower so his hair clears the "Laptop" sign. Re-checked at 300 x 360 and 390 x 844 with no console errors, and the screenshots in `shots/` were retaken.

Test hooks for QA (in the browser console): `UC_DEBUG.state()`, `answer(i)`, `answerRight()`, `answerWrong()`,
`skipWalk()`, `advanceClock(sec)`, `finishRound(n)`, `resetStorage()`, `content()` and a few more listed in the script.
