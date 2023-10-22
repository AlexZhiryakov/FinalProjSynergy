<template>
    <div class="container">
        <nav>
            <router-link class="router" to="/">Home page</router-link>
            <router-link class="router" to="/chat">Chat page</router-link>
            <router-link class="router" to="/test">Test API page</router-link>
        </nav>
    </div>
</template>

<script>
    export default {
    name: 'NavComp'
}
</script>

<style scoped>
.container {
    background-color: black;
    width: 100%;
    height: 60px;
    display: flex;
    justify-content: center;
}
nav {
    width: 400px;
    height: 100%;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 20px;
}

.router {
    text-decoration: none;
    color: whitesmoke;
}
</style>