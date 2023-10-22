<template>
    <div v-if="username">
        <div class="chat">
            <h2>Chat</h2>
            <div class="text" v-for="message in messages" :key="message.id">
                {{message.username}}{{message.text}}
            </div>
            <div v-show="emptyMsg" class="empty">
                No messages
            </div>
        </div>
        <input v-model="newMessage" placeholder="Text your message"/>
        <button @click="sendMessage" @keyup.enter="sendMessage">Send</button>
        <button v-show="deleteBtn" @click="delMessage">Delete</button>
    </div>
    <div v-else class="alert">
        For auth go to <router-link :to="{name: 'Home'}"><span>Link</span></router-link>
    </div>
</template>

<script>

export default {
    name: 'ChatPage',
    data() {
        return {
            messages: [],
            newMessage: '',
            emptyMsg: true,
            deleteBtn: false,
            username: localStorage.getItem('username')
        }
    },
    computed() {
        localStorage.setItem('username', this.$route.query.username)
    },
    methods: {
        sendMessage() {
            if (!this.username) {
                this.username = 'Anonim'
            }
            if (this.newMessage !== '') {
                this.emptyMsg = false
                console.log('You entered message:', this.newMessage)
                this.messages.push(
                    {
                        id: new Date().getTime(),
                        text: this.mewMessage,
                        username: this.username
                    }
                )
                this.saveChatRecords()
                this.newMessage = ''
                this.deleteBtn = true
            } else {
               console.log('Please enter message')
               alert('Please enter message')
            }
        },
        delMessage() {
            this.messages = []
            localStorage.removeItem(`messages_${this.username}`, JSON.stringify(this.message))
            console.log('All messages deleted')
            this.emptyMsg = true
        },
        saveChatRecords() {
            const records = this.messages
            console.log(records)
            localStorage.setItem(`messages_${this.username}`, JSON.stringify(records))
        },
        loadChatRecords() {
            const records = JSON.parse(localStorage.getItem(`messages_${this.username}`))
            if (records) {
                this.messages = records
                this.emptyMsg = false
            }
        }

    },
    created() {
        this.loadChatRecords()
    }

}

</script>

<style>
h2 {
    color: black;
}

.text {
    margin-bottom: 25px;
}

.chat {
    width: 600px;
    height: 100%;
    border: 5px solid black;
    background-color: whitesmoke;
    opacity: 50%;
    color: black;
    font-weight: 20px;
    margin: 20px;
    padding: 15px;
}

.empty {
    margin-bottom: 30px;
    font-style: italic;
}

input {
    margin-right: 15px;
}

button {
    margin-left: 5px;
    margin-bottom: 20px;
}

.alert {
    padding: 30px;
}

span {
    text-decoration: none;
    color: black;
}
</style>