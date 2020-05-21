<template>
    <div>
        <h3>Welcome to ChatRoom {{ chatId }}</h3>
    </div>
</template>

<script>
    export default {
        computed: {
            chatId() {
                return this.$route.params.id;
            }
        }
    }
</script>

<style scoped>

</style>