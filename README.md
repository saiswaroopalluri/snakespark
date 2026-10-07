# SnakeSpark

A self-contained neon arena snake game. The interface and rendering use HTML, CSS, vanilla JavaScript, and the HTML5 canvas. Firebase provides anonymous player sign-in and the realtime leaderboard.

## Run locally

From this folder, run:

```bash
npm start
```

Then open `http://localhost:4173`. The game uses Firebase Authentication and Realtime Database, so an internet connection is required for live rooms and the leaderboard. The local arena itself still renders if Firebase is unavailable.

If port 4173 is already in use, stop the older local preview first, or start a server on another available port and open that address in your browser.

## Deploy to Firebase Hosting

This project is configured to deploy to the Firebase project `neon-nomads-live`. The deployment settings are stored in `firebase.json` and `.firebaserc`.

### First-time setup

1. Install the Firebase command-line tool:

   ```bash
   npm install -g firebase-tools
   ```

2. Sign in with an account that has access to the Firebase project:

   ```bash
   firebase login
   ```

3. Enable Firebase Hosting in the Firebase console if it is not already enabled.

4. Confirm that the Firebase project is selected:

   ```bash
   firebase use neon-nomads-live
   ```

### Deploy an update

Run:

```bash
npm run deploy
```

The command copies the current `index.html`, `style.css`, and `game.js` files into `dist/`, then publishes that folder to Firebase Hosting.

The live game is available at [https://neon-nomads-live.web.app](https://neon-nomads-live.web.app).

If you edit the game files, always run `npm run deploy` again so the live version matches your changes.

### Deploy database rules

The multiplayer leaderboard rules are stored in `database.rules.json`. Deploy them separately after changing that file:

```bash
firebase deploy --only database
```

### Verify a release

After deployment, open the Firebase Hosting URL in a new tab or use a hard refresh. Hosting responses are configured to avoid stale game files, but an already-open browser tab can still need one refresh.

## Project files

- `index.html` — game interface, startup panels, and analytics tag
- `style.css` — responsive desktop and mobile layout
- `game.js` — Canvas gameplay, pickups, rooms, Firebase presence, and leaderboard syncing
- `firebase.json` — Firebase Hosting cache configuration and database-rules path
- `database.rules.json` — Realtime Database access rules
- `dist/` — generated deployment folder; rebuilt automatically by `npm run deploy`

## Controls

- Mouse or `WASD` to steer
- Hold `Space` to boost (at the cost of mass)
- Touch/drag on mobile

The game can run locally for development. Arena bots are lightweight local AI, while player presence, rooms, voting, and the leaderboard use Firebase Realtime Database.
