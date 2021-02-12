<template>

        <div class="nav">
            <div class="blue-light">
                <!-- Blue-light-filtering lenses for any pair -->
            </div>
            <div class="nav-right">
                <span id="nav-command">
                    Sign In
                </span>
                <span id="nav-command">
                    Locations
                </span>
                <span id="nav-command">
                    Cart ({{ cart.length }})
                </span>
            </div>
        </div>

        <h1>DORBY BARKER</h1>

        <div id="img-container">
            <!-- <img id="splash" src="https://images.pexels.com/photos/2710178/pexels-photo-2710178.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=650&w=940"> -->
        </div>

        <div class="main-container">
            <div id="glasses-div" v-for="glass in glasses" :key="glass.id">
                <img id="glasses-show" 
                        :src="glass.img_url" />
                <h3>{{ glass.name }}</h3>
                <h4>${{ glass.price }}</h4>
                    <!-- {{ glass.description }} -->
                <br/>
                
                <details><summary>Edit</summary>
              <form @submit="updateGlasses" :id="glass.id" method="put">
                <label htmlFor="name">Name</label>
                <br />
                <input
                  type="text"
                    v-model="updatedGlasses.name"
                />
                <br />
                <label htmlFor="price">Price</label>
                <br />
                <input
                  type="text"
                    v-model="updatedGlasses.price"
                />
                <br />
                <label htmlFor="description">Description</label>
                <br />
                <input
                  type="text"
                    v-model="updatedGlasses.description"
                />
                <br />
                <label htmlFor="img_url">Image URL</label>
                <br />
                <input
                  type="text"
                    v-model="updatedGlasses.img_url"
                />
                <br />
                <button type="submit">Edit</button>
              </form>
            </details>

                <button class="button" id="delete-button" v-on:click="deleteGlasses(glass.id)">
                    Delete
                </button>
                <button class="button" id="add-to-cart" v-on:click="addToCart(glass.id)">
                    Add to Cart
                </button>
            </div>
            
            </div>

</template>

<script>
import axios from 'axios'

export default {
    name: 'Glasses',
    data() {
        return {
            glasses: [],
            updatedGlasses: {
                name: null,
                price: null,
                description: null,
                img_url: null
            },
            cart: []
        }
    },
    methods: {
        getGlasses() {
            axios.get('http://localhost:3000/glasses')
            .then(response => {
                this.glasses = response.data;
            })
            .catch(error => {
                console.log(error)
            })
        },
        deleteGlasses(id) {
            if (confirm("Are you sure you want to delete?")) {
                axios.delete('http://localhost:3000/glasses/' + id)
                .then((response) => {
                    console.log(response)
                    this.getGlasses();
                })
            } else {
                return;
            }
        },
        updateGlasses(event) {
            event.preventDefault();
            const id = event.target.id
            axios.put('http://localhost:3000/glasses/' + id, this.updatedGlasses)
            .then(response => {
                console.log(response)
                this.getGlasses();
            }).catch(error => {
                console.log(error.message)
            })
        },
        addToCart(id){
            alert('Added to cart!')
            this.cart.push(id);
            console.log(this.cart)
        }
    },
    mounted() {
            this.getGlasses()
        }
}
</script>

<style scoped>

body {
    text-align:center;
}

.nav {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    margin: -.5em -1em 1.5em -1em;
    width: 100vw;
    height: 28px;
    background-color: rgb(236, 235, 235);
}

.blue-light {

}

.nav-right {
    margin-top: .25em;
    margin-right: .5em;
}

#nav-command {
    margin-top: 0;
    padding: 1em;
    font-size: .8em;
}

#img-container {
    width: 97vw;
    height: 50vh;
    /* background-color: red; */
    background-image: url('https://images.pexels.com/photos/2710178/pexels-photo-2710178.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=650&w=940');
    background-size: cover;
    background-position: center;
    border-radius: 3px;
}

.main-container {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
}

#glasses-div {
    width: 20vw;
    padding: 1em;
    margin: 1em;
    /* border: 1px solid rgb(194, 194, 194); */
    border-radius: 5px;
}

#glasses-show {
    width: 15vw;
}

h1 {
    padding-top: 0; 
    margin-top: 0;
    margin-bottom: .5em;
    letter-spacing: .3em;
    font-size: 3em;
}

h3, h4 {
    margin: 0;
    padding: 0;
}

#edit-button {
    background-color: #eee;
    color: #2c3e50;
    border: 1px solid #2c3e50;
    border-radius: 3px;
    margin: .5em;
}

#delete-button {
    background-color: red;
    color: white;
    border: 1px solid red;
    border-radius: 3px;
}

#add-to-cart {
    margin-left: .5em;
    background-color:#eee;
    color: #2c3e50;
    border: 1px solid#eee;
    border-radius: 3px;
}

</style>