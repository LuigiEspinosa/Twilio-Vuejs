Twilio-Vuejs
==============
Twilio integration for Webcat

## Credits to
```
https://www.twilio.com/blog/build-a-video-chat-with-vue-js
```

## Node Backend
```
https://github.com/dongido001/TwilioNodeServer.git
```

# video-chat

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).

## Features
* *Room:* This represents a real-time audio, video, and/or screen-share session.
* *Peer-to-peer Room:* This is a type of room in which media flows directly between participants. It supports up to 10 participants.
* *Group Room:* This is a type of room in which media is routed through Twilio's Media Servers. Up to 50 participants can be accomodated in this room.
* *Participants:* This represents client applications that are connected to a room and sharing audio and/or video media with one another.
* *Tracks:* This represents the individual audio and video media streams that are shared within a Room.
* *LocalTracks:* This represents the audio and video captured from the local microphone and camera.
* *RemoteVideoTracks:* This represents the audio and video tracks from other participants connected to the room.