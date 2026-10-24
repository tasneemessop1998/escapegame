# Escape Rooms

Two escape games for two players, in one page, on the same Firebase project and the same accounts and friends as Fold & Press:

- **Midnight at Marvello’s**: the carnival you already know, unchanged. Your progress there is kept.
- **Hollowmere**: new. A haunted house in Yorkshire, in first person and 3D, on the last night of October. Ten rooms, each with twenty or more things to find, read, open, work out or do, and a story that plays out between you as you go.

Nothing in this file gives a puzzle away.

## 1. Put it online

You already have the Marvello’s repository on GitHub Pages, so this is an update.

1. Open the repository on GitHub.
2. Replace `index.html` with the new one.
3. Upload the whole **`assets`** folder (fifteen `.glb` files: the people and the ghosts). It must sit next to `index.html`, so the site has `index.html` and `assets/pm1.glb` side by side. On GitHub: *Add file → Upload files*, then drag the `assets` folder in.
4. Replace `manifest.webmanifest`, `icon-192.png` and `icon-512.png` with the new ones (the app icon becomes a keyhole and the name *Escape Rooms*).
5. Leave **your real `firebase-config.js`** where it is. The one in this folder is a blank placeholder; do not upload it over yours.
6. `database.rules.json` has not changed. Nothing to do in the Firebase console.

A minute later the site is updated. Everyone gets it the next time they open the page (pull down to refresh if a phone still shows the old one).

Progress is not in any of these files. Marvello’s runs, best times and friends live in the database and carry straight over.

If you would rather start a fresh repository: upload everything in this folder plus your real `firebase-config.js`, switch on Pages (*Settings → Pages → Deploy from a branch → main → / (root)*), and that is all.

## 2. The lobby

Sign in as usual. At the top are the two games: tap **Midnight at Marvello’s** or **Hollowmere** to choose. Everything under it (your escapes, Start with a friend, Share a code, Look around alone, and the Progress tab) follows the game you picked, so you and a friend can be partway through both at once.

- **Start with a friend**: pick a friend, and the escape appears in both of your lists. You are the first player, they are the second. Some clues are for one of you only.
- **Share a code**: five letters anyone can type to join you.
- **Look around alone**: every room open to one person; anything meant for two hands needs one. Saved on your phone, never counted in your record.
- **Settings** (the gear): sound and vibration for both games, your Marvello’s look, and for Hollowmere: **jump scares** (Full or Softer), **music** (Off, Quiet, Normal, Loud), **graphics** (Auto, Low, Medium, High) and **who you are** (six people to choose from). The same Hollowmere settings are in the back menu inside the house.

## 3. Playing Hollowmere

You are both in the house together and you can see each other: a real person each, with a torch.

**Moving and looking.** The pad bottom left walks and turns (push it, or use the arrows). Drag anywhere on the picture to look around, up and down too. On a computer: W A S D or the arrow keys, and E or Space to use what you are looking at.

**Things.** The small ring in the middle of the screen is where you are looking. When it sits on something it names it; if you are close enough a **Use** button appears. You can also just tap the thing. Then:
- read it, take it, open it, try a code or something you are carrying on it, or turn it over in your hands to look closely;
- some things are played rather than solved: you work them with your own hands, and timing matters;
- some things need both of you at the same moment.

**Clues are split.** Some things only one of you can see. Talk. Every clue you read has a **Share** button that puts it in your partner’s journal. The journal (the book button) keeps everything either of you has read. The list button shows what you have done in this room; the rest is counted, not named.

**Things you carry** sit down the right-hand side. Tap one to read about it, look at it closely, or hand it to your partner if they are standing next to you. The **satchel** is carried by both of you, and what goes in it stays with you from room to room.

**Chat.** The bar at the bottom. A message appears over the sender’s head and as a line at the top of the screen; while you are typing, the latest messages show just above the box, so you can read and reply at the same time.

**Story.** Between and during the rooms the story plays out in front of you, with speech over the characters’ heads. These scenes happen for both of you at the same moment and cannot be skipped. Headphones help.

**Hints.** Every lock and every hands-on puzzle has a hint button: the first nudges (+1:00 on the room clock), the second pushes (+2:00), the third gives it away (+5:00).

**Scares.** There are jump scares. If it is too much, Settings → Jump scares → Softer keeps them short and quiet.

**If it feels slow** on an older phone, Settings → Graphics → Low.

**Leaving.** The back button: leave for now (everything you solved stays solved, come back from the lobby), quit this escape, or end it for both of you. Each one asks first.

## 4. What changed in the rest of the page

Marvello’s plays exactly as before. The lobby now has the game picker, and the page is called Escape Rooms.

## 5. Tested

Every Hollowmere room has been played start to finish by two simulated players on the same live game (taking things, handing them over, holding things together, playing every hands-on puzzle the way a person would, wrong answers first), and the two-person parts of the later rooms have been played alone as well. Marvello’s still passes all of its own play-throughs. The rooms were also rendered in a real browser to check how they look.

The answers are not written anywhere in the files in plain text. The page keeps a scrambled form of each answer and checks what you enter against it.

## 6. Credits

- People and ghosts: the Microsoft Rocketbox avatar library (MIT licence), including its animations.
- A head model made from the Lee Perry-Smith head scan by Infinite-Realities, licensed CC BY 3.0 (changed for this game).
- 3D: three.js (MIT licence), loaded from jsDelivr.
- Type: IM Fell English, Special Elite, Caveat, Nunito, Fredoka and Patrick Hand, from Google Fonts.
- Every sound and all the music is made in the browser as you play. There are no sound files.
