<template>
<div class="home">
  
    <button @click="agregarDatos({nombre, apellido,dni})" class="bg-red-600 text-white px-2 py-2">agregar</button>
    <input v-model="nombre" class="border border-gray-400 px-2 py-1 " type="text">
    <input v-model="apellido" class="border border-gray-400 px-2 py-1 " type="text">
    <input v-model="dni" class="border border-gray-400 px-2 py-1 " type="text">

</div>
</template>

<script>
import {
    db
} from "../firebase"
import {
    collection,
    addDoc
} from "firebase/firestore";

export default {
    name: 'HomeView',
    components: {

    },
    data() {
        return {
            nombre: "",
            apellido: "",
            dni: ""
        }
    },
    methods: {
        async agregarDatos(payload) {
            try {
                const docRef = await addDoc(collection(db, "users"), {
                    nombre:payload.nombre,
                    apellido:payload.apellido,
                    dni:payload.dni
                });
                this.nombre=""
                this.apellido=""
                this.dni=""
                console.log("Document written with ID: ", docRef.id);
            } catch (e) {
                console.error("Error adding document: ", e);
            }
        }
    },
}
</script>
