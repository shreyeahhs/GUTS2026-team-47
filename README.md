# Blink Duel

A sword fight you play with your face. Blink to swing your sword, open your mouth to put your shield up. Your stick figure copies your face too, so when you blink, it blinks.

Play it here: https://shreyeahhs.github.io/blink-duel/

## Where the idea came from

Made for GUTS hackathon 2026 for the JP Morgan Chase challenge, where the rule was: build something fun using only two buttons or two actions. Blinking and opening your mouth are two actions anyone can do without their hands, so those became the controls.

The screen layout comes from my own sketch, with the health bars up in the corners and a vs circle in the middle. The opening cutscene is inspired by the Shadow Fight intro, where the two warriors are just black silhouettes in front of a huge sun. Except here they're fighting over a sandwich.

## What it's made with

It's one HTML file with plain JavaScript. No build step, no framework.

- [MediaPipe Face Landmarker](https://ai.google.dev/edge/mediapipe/solutions/vision/face_landmarker) finds your face in the webcam. It gives a score for how shut your eyes are and how open your jaw is, and the game turns those into slash and shield.
- [PeerJS](https://peerjs.com) (WebRTC) connects two devices for online games. Its free server only helps the two browsers find each other. After that the game data goes straight between them.
- [Rough.js](https://roughjs.com) draws everything so it looks hand drawn.
- [Virgil](https://github.com/excalidraw/virgil) is the handwriting font (the one Excalidraw uses). It's in the `fonts` folder.
- GitHub Pages hosts it.

## Running it yourself

You need Python (or any other static file server) and Chrome or Edge.

```bash
git clone https://github.com/shreyeahhs/blink-duel.git
cd blink-duel
python -m http.server 5173
```

Open http://localhost:5173 and allow the camera. The first load needs internet to download the face tracker (around 15 MB) and the libraries. The browser keeps them after that.

Browsers only let a page use the webcam on localhost or on https. So opening `http://<your-laptop-ip>:5173` from another device won't turn the camera on. For two devices, either run a copy on each one or just use the GitHub Pages link.

## How to play

A 30 second intro plays first. Click or press any key if you want to skip it.

Pick "play vs computer" or make an online room. Face the webcam and open your mouth for a second to start. During the 3 second countdown keep your eyes open and your mouth shut; the game uses that to learn what your face looks like at rest.

- Blink to slash. The slash happens when your eyes open again.
- Open your mouth to raise your shield. It drains while it's up, and if it runs out it breaks for a bit.
- You can only do one at a time, so a blink with your mouth open doesn't count.
- 5 hits and you're out. Open your mouth (or press space) for a rematch.

The computer frowns and pulls its sword back right before it attacks, so watch its face. You can block it, or blink first and hit it before it swings.

No webcam? Press Enter on the menu to play with the keyboard. A slashes, holding S raises the shield.

If your blinks or mouth aren't picked up well, press T. That opens a small panel with sensitivity sliders and a recalibrate button.

## Playing online

One player clicks "create online room" and sends the 4 letter code (or the invite link) to the other. The other player types it in and clicks join. Each device only tracks its own player's face.

Campus wifi like eduroam blocks the direct connection, so joining fails there. Put both devices on a phone hotspot and it works. To make it work on those networks too you'd need a TURN server, which goes in the `TURN` list near the top of the script in `index.html`.

## Credits

- MediaPipe Face Landmarker by Google, Apache 2.0
- PeerJS, MIT
- Rough.js, MIT
- Virgil font by Ellinor Rapp, SIL Open Font License (its license file is in `fonts`)
