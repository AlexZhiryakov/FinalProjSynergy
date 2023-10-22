<template>
  <div class="container">
    <div class="title">Commands</div>
    <div v-if="isLoad" class="loading">loading data</div>
    <div v-else class="data">
        <div v-for="(el, i) in teamData" :key="el.id">
            {{i + 1}}, {{el.abbrevation}}{{el.city}}
            <img 
            src='https://avatars.mds.yandex.net/i?id=e51c0bb71789882fb6fc9e3608f8c47904342b10-7593510-images-thumbs&n=13&exp=1'
            style='width: 15px; height: 15px'
            @click="removeTeam(el.id)"/>
        </div>
    </div>
  </div>
</template>

<script>
export default {
    name: 'TestApi',
    data() {
        return{
            teamData: [],
            isLoad: true
        }
    },
    methods: {
        removeTeam(id) {
            this.teamData = this.teamData.filter((el) => el.id !== id)
        }
    },
    mounted() {
    const url = "https://free-nba.p.rapidapi.com/teams?page=0";
    const options = {
    method: "GET",
    headers: {
    "X-RapidAPI-Key": "488f437511msh2d3854838388c55p13692cjsn135921cfebdf",
    "X-RapidAPI-Host": "free-nba.p.rapidapi.com",
    },
    };
    fetch(url, options)
    .then((res) => res.json())
    .then((res) => {
        this.teamData = res.data
        this.isLoad = false
    })
    }
    }
</script>

<style>
.container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-content: center;
}

.title {
    font-size: 2em;
    color: grey;
    margin: 15px;
    font-weight: bold;
}

.data {
    padding: 20px;
}

.loading {
    padding-bottom: 30px;
}

img {
    cursor: pointer;
    margin-left: 15px;
}
</style>