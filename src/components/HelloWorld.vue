<template>
    <div class="cat-block">
        <article v-for="(location, idx) in locations" :key="idx">
            <img :src="location.image">
            <h1>{{ location.name }}</h1>
            <button @click="deleteLocation(location.id)">
                Delete
            </button>
        </article>
        <form @submit="addLocation(name, image)">
            <input v-model="name" placeholder="Location Name">
            <input v-model="image" placeholder="Location Image URL">
            <button type="submit">Add New Location</button>
        </form>
    </div>
</template>

<script>
  import { db } from '../main'

  export default {
    name: 'HelloWorld',
    data () {
      return {
        locations: []
      }
    },
    firestore () {
      return {
        locations: db.collection('locations').orderBy('createdAt')
      }
    },
    methods: {
      addLocation (name, image) {
        const createdAt = new Date()
        db.collection('locations').add({name, image, createdAt})
      },
      deleteLocation (id) {
        db.collection('locations').doc(id).delete()
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    h1, h2 {
        font-weight: normal;
    }

    ul {
        list-style-type: none;
        padding: 0;
    }

    li {
        display: inline-block;
        margin: 0 10px;
    }

    a {
        color: #42b983;
    }
    img {
        width: 80%;
    }
</style>
