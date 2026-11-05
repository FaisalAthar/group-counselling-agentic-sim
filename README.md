# Group Circle Simulator (Stage 1 prototype)

A training simulation for trainee group counsellors. The trainee facilitates a five-member support group ("Coping with University Pressure", session 3 of 8). The other roles are AI agents, and the page shows the decisions they make.

- **Members (5 agents):** Ravi (dominates the talk), Mei Ling (silent member), Daniel (sceptic), Aisyah (rescuer) and Farah (grieving). Each has a public profile and a hidden story. A member shares their hidden story only once their trust in the group is high.
- **Director (1 agent):** after each facilitator move it labels the counselling skill used, sets the group stage (forming, storming, norming, working), picks who speaks next with a private instruction, and notes silent trust changes in members who don't speak.
- **The group talks on its own:** after members respond to the facilitator, the director decides whether the conversation carries on among them (replying to each other, disagreeing, Ravi taking over) or falls quiet and turns back to the facilitator. The facilitator can jump in at any time, which stops the current speaker. **Settings → How much the group talks on its own** sets the limit: Low (no exchanges), Medium (up to 3) or High (up to 6).
- **Observer (1 agent):** writes the end-of-session debrief, with links back to specific turns.

Every agent replies in JSON (`text`, `emotion`, `gaze`, `posture`, `trust_delta`, `private_thought`, `feelings`). The circle is drawn from that JSON:
- Each figure's face and glow show its emotion.
- The eyes look at the member's gaze target.
- Posture shows as leaning in, crossed arms, turning away or looking down.
- A ring around each figure shows trust.
- Lines between members show connection and tension.
- "X-ray thoughts" shows each member's private thought next to what they say out loud.
- The "AI decisions" tab logs every director choice and its reasoning.

## 3D view

The circle is drawn in 3D with [three.js](https://threejs.org) (MIT licence), stored in `lib/` so the page does not depend on a CDN. The camera is the facilitator's seat, so members who talk to you look straight at you. Click a head or a nameplate to address that member.

## Running it

It is a single static page, so open `index.html` from GitHub Pages or any web server.

- **My model servers:** uses OpenAI-compatible endpoints (Lemonade or LM Studio). The defaults are:
  - members on `lsctdscoma003` (`qwen2.5-14b-instruct`)
  - director and observer on `lsctdscoma002` (`qwen/qwen3-4b-2507`)

  Change them under **Settings**. Open the page on a device that can reach those servers, for example one on the Tailscale network. If one model call fails, that step falls back to the scripted rules, and the decision log marks it as a "scripted fallback".
- **Demo mode (no AI):** rule-based stand-ins for the agents. Use it to show the interface offline.

Voice uses the browser's built-in speech: each member gets a different voice, pitch and rate. A 🎤 button for speaking instead of typing appears in browsers that support speech recognition (Chrome, Edge).

## Model calls per turn

Each facilitator turn makes one director call and one or two member calls. Members on the 14B model and the director on the fast 4B model keep turns reasonably quick. If the director makes poor decisions, try a larger model for it.

## Safety

- This is a training simulation with fictional people. It is not for real clients.
- Members are told not to talk about self-harm or suicide in this version.
- A fixed keyword rule, not the model, raises a risk banner if risk language appears, and the AI cannot turn it off.
- There is a content note at the start and a Pause button.

## Next stages

2. Stylized 3D avatars (VRM, toon-shaded) and local Kokoro voices, one per member.
3. Spoken input with interruptions, and a replay view for the observer.

## Versions

The version number is shown next to the title. Each build is also saved as a copy in [`versions/`](versions/), and GitHub Pages serves those too, so you can open an older build at `https://faisalathar.github.io/group-counselling-agentic-sim/versions/group-circle-sim-v1.4.html`.

| Version | What changed |
|---|---|
| v1.7 | Stylized 3D view: vinyl-toy heads with their own looks in a counselling room; heads turn to whoever they are listening or talking to, look at the floor when sad and out of the window when bored; the 2D circle is used if WebGL is not available |
| v1.6 | Version number shown next to the title; every build saved in `versions/` |
| v1.5 | The group keeps talking among themselves after answering you; you can jump in at any time; a setting for how much the group talks on its own |
| v1.4 | Several members respond when you address the whole group; non-verbal replies (e.g. a nod); speaking order shown on the circle |
| v1.3 | Structured output forces valid JSON from small models; plain-speech replies are used instead of scripted ones |
| v1.2 | Streaming replies with live progress; longer timeouts for slow models; realistic connection test with timings |
| v1.1 | Status card and timer while the group responds; model errors shown in the transcript |
| v1.0 | First Stage 1 prototype: five members, director, observer debrief, demo mode, browser voice |
