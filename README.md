# ClearRoom

A single-page, GitHub-Pages-ready browser meeting room with:

- Up to 10 participants
- Peer-to-peer WebRTC audio/video
- Host-created invite links
- Host transfer, room lock, mute, remove participant
- 5–120 minute room timer
- Screen sharing
- Local room-audio recording
- Local screen/tab recording
- ALS/AAC type-to-speak
- One-tap repeat + recent typed phrases
- Responsive mobile/desktop UI
- Room chat

## Run

1. Put `index.html` in a GitHub repository.
2. Enable **Settings → Pages → Deploy from branch**.
3. Open the HTTPS GitHub Pages URL.
4. The first person creates a room and shares the generated invite link.

Camera/microphone and screen capture require HTTPS (or localhost).

## Networking note

This static build uses **PeerJS Cloud for signaling** and WebRTC for media/data. PeerJS documents that production deployments should consider a self-hosted PeerServer, and TURN is needed for peers behind restrictive/symmetric NATs.

Edit `RTC_CONFIG` near the top of the script to add your TURN service. To self-host signaling, change the `new Peer(...)` configuration to your PeerServer host/path/port.

## Recording note

Recordings are created **locally in the participant's browser** and downloaded to that participant's device. Screen/system audio availability varies by browser and operating system. Always obtain appropriate consent before recording.

## ALS/AAC TTS design

When an AAC user presses **Speak to room**, the text is sent over the room's WebRTC data channel. Each participant's own browser synthesizes the text locally with Speech Synthesis. This means the AAC user does not need to route computer-generated audio through a physical microphone.

Recent phrases are saved only in that browser's localStorage.
