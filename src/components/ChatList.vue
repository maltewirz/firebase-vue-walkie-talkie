<template>
    <div>
        <ul>
            <li v-for="chat of chats" :key="chat.id">
                <router-link :to="{ name: 'chat', params: { id: chat.id } }">{{ chat.id }}</router-link>
            </li>
        </ul>
        <button @click="createChatRoom()">Create New Chat Room</button>
    </div>
</template>

<script>
import { db } from '../firebase';
export default {
    data() {
        return {
            chats: []
        }
    },
    // vuefire firestore component manages the real-time stream to that reactive data property
    firestore() {
        return {
            chats: db.collection('chats').where('members', 'array-contains', this.uid)
        }
    },
    methods: {
        async createChatRoom() {
            await db.collection('chats').add({
                createdAt: Date.now(),
                owner: this.uid,
                members: [this.uid]
            })                
        }
    },
    props: ['uid']
}
</script>
