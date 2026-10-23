# Midnight at Marvello’s

A two-player escape game for the browser. The gates of Marvello’s Carnival of Wonders locked at midnight with the two of you still inside, and ten attractions stand between you and the way out: a ticket booth, a hall of mirrors, a carousel, a fortune teller’s tent, a ghost train, a candy factory, a puppet theatre, a big wheel, a clock tower and, last, Marvello’s vault. Each room has fifteen or more things to find, read, solve or do, and every one of them is built so that two people have to talk: some clues only one of you can see, some levers need two hands at once, and some things have to be handed from one of you to the other.

It runs on the same free Firebase project, the same accounts and the same friends list as Fold & Press. Nothing in this file gives a puzzle away.

## 1. Put it online (ten minutes)

You already have the Firebase project, so this is mostly copying.

1. On GitHub, make a **new repository** (for example `marvellos`), public, with no README.
2. Upload these files into it: `index.html`, `manifest.webmanifest`, `icon-192.png`, `icon-512.png`, `database.rules.json`.
3. Also upload **your real `firebase-config.js`**: copy it from your Fold & Press repository. (The one in this folder is a blank placeholder; the game shows a setup note if it finds that.)
4. Repository → Settings → Pages → Source: *Deploy from a branch*, branch `main`, folder `/ (root)`. Save. A minute later the game is at `https://<your-username>.github.io/marvellos/`.
5. In the Firebase console → Realtime Database → Rules: paste the contents of `database.rules.json` and publish. This one file covers **both** games (it has everything Fold & Press needs plus the new `rooms` branch and the `escapes` list), so paste the same file into the Fold & Press repo too when you next update it.

Nothing else changes: same email/password accounts, same usernames, same friends, and the authorised domain (`<your-username>.github.io`) already covers the new repo.

Free-tier headroom is fine: a game in progress is a few kilobytes, and chat is pruned after ten minutes.

## 2. Play

Sign in with your Fold & Press account (or create one; the username is shared).

**Lobby.**
- **Your escapes**: games you are part of, with the room you are in and whether your partner is inside right now. Tap to go back in; everything you have solved stays solved, and either of you can keep going alone.
- **Start with a friend**: picks a friend from your list and drops the game into both of your lists. You are seat A, they are seat B. Some clues are for one seat only.
- **Share a code**: a five-letter code (or link) for anyone to join. Two players only.
- **Look around alone**: a solo wander with everything visible and the two-handed things reduced to one hand. Saved on your phone, never counted in your record.
- **Progress** tab: the ten rooms (names appear as you reach them), your best time per room, and you and your friends ranked by rooms done and total time.

**In a room.**
- Tap the ground to walk. Tap a thing to walk over and use it. A label appears on anything you are standing next to.
- **Hold your finger on the ground** to drop a marker your partner sees (“look here”).
- The chat bar at the bottom. Messages appear in the corner and as a speech bubble over the sender’s head.
- Top left: the room and how many of its things you have done (`7/18`). Tap the list button for what you have done so far; the rest is counted, not named.
- Top right: the room clock. Hints add to it (below). Your best time per room is kept on your profile.
- Items you pick up sit on the right. Tap one to read about it or, if your partner is standing next to you, hand it over. Each of you carries your own things.
- Some things are held rather than pressed: **press and hold** the big button while your partner does their part. A door with two plates wants two people; a lever that keeps something moving wants one person holding while the other goes.
- One room is dark. A carried light shows what is near whoever holds it; stand next to your partner and they can read by your light.

**Hints.** Every lock has a hint button: hint 1 nudges (+1:00 on the clock), hint 2 is a real push (+2:00), hint 3 is the answer (+5:00). The clock turns red once a hint has been taken, so you both know.

**Finishing a room.** When the exit opens you both see a card with the time and a line of the story, and the next room loads for whoever taps Continue. The run is shared, so the other person follows when they are ready. After the tenth room, the gate.

## 3. What is in the rooms (without spoilers)

Each room has its own look and its own kind of trick: things written to be read in a mirror, symbols that stand for letters, blinking lights, arm signals, numbers hidden in lights, locks that take words, digits, colours, arrows, switches, wires, a dial, a clock or an order, and a few plain riddles. Nothing needs arithmetic beyond counting and a bit of adding up. Every room ends in something you have to do together.

The answers are not written anywhere in the game’s files in plain text: the page stores a scrambled form of each answer and checks what you type against that, so even reading the source gives nothing away. The only way to see an answer is hint 3, and it costs you five minutes.

## 4. How it is built (in case you want to change things)

- One file, `index.html`: the page, styles and script, like Fold & Press. The rooms are plain data at the bottom of the script (`ROOMS`), one object per thing in the room: where it is, how it is drawn (`type`), what it says when looked at (`look`, `clue`), what it needs (`requires`, `use`, `lock`, `hold`, `holdAll`, `visibleTo`), and what happens when it is solved (`onSolve`, `onTake`, `onLook` effects such as `reveal:id`, `open:id`, `give:item`). Adding a thing to a room is adding an object to that list; adding a task is giving it a `task:` line.
- Answers are stored as `H('…')` hashes. To change an answer, change the text inside `H()`; the game hashes what the player types the same way. Hints are plain text, three per lock.
- Drawing is canvas 2D: a backdrop per room (`pal`, `deco`, `floorDeco`), a library of props (`ART`), and the two jelly people (`drawPersonShape`). Each player picks a look in Settings.
- Live play: `rooms/<code>` in the Realtime Database holds the run (`seats`, `players` with positions and inventories, `lv/<n>` with each thing’s state, hints and penalties, `chat`, `ping`). Positions are written about eight times a second while you move and smoothed on the other side. Held things carry a timestamp per holder that is refreshed while held, so “at the same time” means within a couple of seconds.
- Solo play keeps the same structure in `localStorage` (`mm.solo`).
- Progress goes to `profiles/<uid>/escape` (`done`, and a best `time` per room), readable by friends for the Progress tab.
- Rules: `rooms/<code>` readable and writable by any signed-in player (friends-grade, like games); `users/<uid>/escapes/<code>` writable by you or a friend (so a friend can start a game that appears in your list).
- `window.Marvello` in the browser console exposes the live state for debugging (`G`, `ROOMS`, `enterSolo()`, `teleport(x, y)`, `openSheet(obj)`).
