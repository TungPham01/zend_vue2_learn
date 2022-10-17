<template>
  <div class="list-user">
    <p>List user component</p>
    <UserComponent
        v-bind:users="users"
        v-on:deleteUser="deleteUser"
     />
  </div>
</template>

<script>
import UserComponent from './UserComponent.vue'
export default {
    name: 'list-user',
    data() {
        return {
            users: [
                {id: 1, name: 'tùng', email: 'tung@gmail.com'},
                {id: 2, name: 'linh', email: 'linh@gmail.com'},
                {id: 3, name: 'tuan', email: 'tuan@gmail.com'},
                {id: 4, name: 'hieu', email: 'hieu@gmail.com'},
                {id: 5, name: 'ha', email: 'ha@gmail.com'},
            ]
        }
    },
    components: {
        UserComponent
    },
    methods: {
        deleteUser(data) {
            this.$emit('deleteUser', data )
            console.log('deleteUser ListUserComponent.vue', data)
        }
    }
}
</script>

<style>

</style>