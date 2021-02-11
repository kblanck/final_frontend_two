<template>
<form @submit="addGlasses" method="post">
        <input 
            type="text" 
            id="name" 
            placeholder="name"
            v-model="newGlasses.name"
        />
        <br/>
        <input 
            type="text" 
            id="price" 
            placeholder="price"
            v-model="newGlasses.price"
        />
        <br/>
        <input 
            type="textarea" 
            id="description" 
            placeholder="description"
            v-model="newGlasses.description"
        />
        <br/>
        <input 
            type="text" 
            id="img_url" 
            placeholder="image URL"
            v-model="newGlasses.img_url"
        />
        <br/>
        <button type="submit">Add</button>
        </form>
</template>


<script>
import axios from 'axios'

export default {
    props: [],
    name: 'AddGlasses',
    data() {
        return {
            glasses: [],
            newGlasses: {
                name: null,
                price: null,
                description: null,
                img_url: null
            }
        }
    },
    methods: {
        addGlasses(e) {
          e.preventDefault();
          axios.post('http://localhost:3000/glasses', this.newGlasses)
          .then(response => {
              this.glasses = response.data;
          })
        }  
    },
    mounted() {
        axios.get('http://localhost:3000/glasses')
        .then(response => {
            this.glasses = response.data;
        })
        .catch(error => {
            console.log(error)
        })
    }      
}
</script>

<style scoped>

input[type=textarea] {
    height: 10vh;
}

</style>