<template>
  <div class="col-md-3 rooms">
      <div class="room" v-for="room in rooms" v-bind:key="room.id" @click="showRoom(room.name)">
          {{room.name}}
      </div>

      <AddRoom />
  </div>
</template>

<script>
    import { EventBus } from '../Event'
    import AddRoom from '../components/AddRoom'

    export default {
        name: "Rooms",

        data() {
            return {
                rooms: [
                    {id: 1, name: 'PHP Room'},
                    {id: 2, name: 'Python Room'},
                    {id: 3, name: 'Daily Room'},
                ],
                roomCount: 3, // Keep track of the number of rooms present
                loading: false, // Indicate when tracks in a room is being loaded
            }
        },

        components: {
            AddRoom
        },

        created() {
            EventBus.$on('new_room', (data) => {
                this.roomCount++;
                this.rooms.push({
                    id: this.roomCount,
                    name: data
                })
            })
        },

        methods: {
            showRoom(room) {
                EventBus.$emit('show_room', room);
            }
        }
    }
</script>

<style scoped>
    .rooms > .room {
        border: 1px solid #7c817c;
        padding: 13px;
        margin: 3px 0px;
        color: #f8f8ff;
    }

    .rooms {
        border: 1px solid #404440;
        cursor: pointer;
    }
</style>