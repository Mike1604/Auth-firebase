<template>
    <div>
        <Navbar/>
        <div class="container my-5">
            <div class="row row-cols-1 row-cols-md-3 g-4">
                <div class="col" v-for="(item, index) in usuarios" :key="index">
                    <div class="card">
                    <img :src= "item.foto" class="card-img-top">
                    <div class="card-body">
                        <h5 class="card-title text-center"> {{item.nombre}}</h5>
                        <p class="card-text text-center"> {{item.correo}}</p>
                    </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>


import Navbar from '../components/Navbar.vue'
import { collection, getDocs } from 'firebase/firestore/lite';
import { db } from "../main";
import To_do from '../components/to_do.vue';
export default {
    name: 'Home',
    components: {
    Navbar,
    To_do
},
    data() {
        return {
          usuarios: [],
          usuario: {
            nombre: '',
            correo: '',
            foto: ''
          }
        }
    },
    methods:{
  // GET
    async obtenerDatos () { 
      const querySnapshot = await getDocs(collection(db, "usuarios"));
        querySnapshot.forEach((doc) => {
        let usuario = doc.data()
        usuario.id = doc.id
        this.usuarios.push(usuario)
        console.log(usuario)
      });
    }
    },
    mounted() {
        this.obtenerDatos();
    },
}
</script>
