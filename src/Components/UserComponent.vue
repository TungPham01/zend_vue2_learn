<template>
    <div class="user">
        <h4 v-for="user in users" v-bind:key="user.id">
             {{ user.email }}
            <button
                @click="handleDelete"
            >
                Delete
            </button>
        </h4>
    </div>
</template>

<script>
export default {
    name : 'user',
    props: {
        users: Array
    },
    data () {
        return {

        }
    },
    methods: {
        handleDelete (e) {
            console.log('User', e )
        }
    }
}
</script>

<style>

</style>