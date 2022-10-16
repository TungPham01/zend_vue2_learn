<template>
  <header>
    <h1>{{ title }}</h1>
    <button @click="changeTitle">Thay đổi title từ header component </button>
</header>
</template>

<script>
export default {
    name: 'header-component',
    props: {
        title: String
    },
    data() {
        return {
            text: 'Header text'
        }
    },
    methods: {
        changeTitle(e) {
            console.log('trước khi kích hoạt trong header component')
            var data = {
                title:  'test  -> data gửi lên' 
            }
            this.$emit('changeTitleEvent', data)
        }
    }
}   
</script>
 
<style>

</style>