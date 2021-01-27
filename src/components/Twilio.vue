<template>
    <wc-video :username="username">
        <div class="wc-twilio-wrapper">
            <div class="wc-twilio-remoteTrack">
                <slot name="remoteTrack"></slot>
            </div>

            <div class="wc-twilio-localTrack">
                <slot name="localTrack"></slot>
            </div>

            <div class="wc-twilio-leaveTrack">
                <slot name="leaveTrack"></slot>
            </div>
            
            <div class="wc-twilio-controls">
                <slot name="audio">
                    <b-button
                        v-if="this.microphone == true"
                        variant="primary"
                        size="sm"
                        class="border-0"
                        style="top: 5px, left: 5px"
                        @click="muteAudio"
                        ><i class="fa fa-microphone"></i
                    ></b-button>

                    <b-button
                        v-if="this.microphone == false"
                        variant="primary"
                        size="sm"
                        class="border-0"
                        style="top: 5px, left: 5px"
                        @click="unmuteAudio"
                        >
                        <i class="fas fa-microphone-slash"></i
                    ></b-button>
                </slot>

                <div class="wc-twilio-control-spacing"></div>

                <slot name="camera">
                    <b-button
                        v-if="this.camera == true"
                        variant="primary"
                        size="sm"
                        class="border-0"
                        style="top: 5px, left: 5px"
                        @click="muteVideo"
                        ><i class="fas fa-video"></i
                    ></b-button>

                    <b-button
                        v-if="this.camera == false"
                        variant="primary"
                        size="sm"
                        class="border-0"
                        style="top: 5px, left: 5px"
                        @click="unmuteVideo"
                        ><i class="fas fa-video-slash"></i
                    ></b-button>
                </slot>
            </div>
        </div>
    </wc-video>
</template>

<script>
    import Video from './Video'

    export default {
        name: "TwilioChat",

        data() {
            return {
                microphone: true,
                camera: true,
            }
        },

        // props: ['token'], 
        props: ['username'], 

        components: {
            'wc-video':Video
        },

        methods: {
            // mute audio of video chat
            muteAudio() {
                this.activeRoom.localParticipant.audioTracks.forEach(function(
                    audioTrack
                ) {
                    console.log("audioTrack-- " + audioTrack);
                    audioTrack.disable();
                });

                this.microphone = false;
            },

            // unmute audio of video chat
            unmuteAudio() {
                this.activeRoom.localParticipant.audioTracks.forEach(function(
                    audioTrack
                ) {
                    console.log("audioTrack-- " + audioTrack);
                    audioTrack.enable();
                });
                
                this.microphone = true;
            },

            // mute video
            muteVideo() {
                this.activeRoom.localParticipant.videoTracks.forEach(function(
                    videoTrack
                ) {
                    console.log("videoTrack-- " + videoTrack);
                    videoTrack.disable();
                });
                
                this.camera = false;
            },

            // unmute video
            unmuteVideo() {
                this.activeRoom.localParticipant.videoTracks.forEach(function(
                    videoTrack
                ) {
                    console.log("videoTrack-- " + videoTrack);
                    videoTrack.enable();
                });

                this.camera = true;
            },
        }
    }
</script>

<style>
    .wc-twilio-wrapper {
        position: relative;
        min-width: 300px;
        min-height: 200px;
    }

    .wc-twilio-remoteTrack {
        position: absolute;
        top: 0;
        bottom: 0;
        left: 0;
        right: 0;
    }

    .wc-twilio-localTrack {
        position: absolute;
        top: 0;
        left: 0;
        z-index: 5;
        width: 20%;
        height: 20%;
        margin: 1rem;
    }

    .wc-twilio-controls {
        position: absolute;
        top: 0;
        right: 0;
        z-index: 5;
        width: 20%;
        height: 20%;
        margin: 1rem;
        display: flex;
        flex-flow: row nowrap;
        justify-content: center;
        align-items: center;
    }

    .wc-twilio-control-spacing {
        width: 1rem;
    }

    .wc-twilio-leaveTrack {
        position: absolute;
        bottom: 0;
        left: 0;
        right: 0;
        margin: 1rem;
        display: flex;
        flex-flow: row nowrap;
        justify-content: center;
        align-items: center;
    }
</style>
