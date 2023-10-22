<template>
    <div>
        <div v-if="isAuthenticated">
            <div>Welcome <b>{{ username }}</b></div>
            <button @click="logout">Logout</button>
        </div>

        <div v-else>
            <label>Your name: </label>
            <input v-model="username" @keyup.enter="login"/>
            <button class="buttonInp" @click="login">Send</button>
        </div>
    </div>
</template>

<script>
export default {
  name: 'HomePage',
  data() {
    return {
        isAuthenticated: false,
        username: ''
    }
  },
  methods: {
    login() {
        if(this.username !== ''){ // это если инпут не пустой то перенаправляем в чат
            console.log('You entered as', this.username)
            this.isAuthenticated = true
            localStorage.setItem('isAuthenticated', true)
            localStorage.setItem('username', this.username)
            this.$router.push({
                name:'Chat',
                query: {username: this.username} 
            })
        }else { // если имя не введено
            console.log('Please, enter your name')
        }
    },
    logout() {
        this.isAuthenticated = false
        this.username = ''
        localStorage.removeItem('isAuthenticated')
        localStorage.removeItem('username')
    }
  },
  created() { // узнаем есть ли у браузера с помощью localStorage - есть ли аунтефикация на сайте и введено ли имя
    if(localStorage.getItem('isAuthenticated')) {
        this.isAuthenticated = true
        this.username = localStorage.getItem('username')
    }
  }
}
</script>

<style scoped>
div {
    padding: 20px;
    font-size: 25px;
}

label {
    margin: 1px;
}

button {
    margin-left: 10px;
}

.buttonInp {
    width: 50px;
    height: 20px;
}
</style>