<template>
    <section class="chat container row">
        <div class="col-3 text-center">
            <div class="chat__foto" v-if="usuario1.picture">
                <img :src="usuario1.picture.large" alt="Foto usuario 1">
            </div>
            <h5 class="chat" v-if="usuario1.name">
                {{ usuario1.name.title }} {{ usuario1.name.first }}
            </h5>
            <div class="chat__mens d-flex flex-column">
                <textarea v-model="mensajeUsuario1" placeholder="Escribe un mensaje..."></textarea>
                <button class="chat__boton1 m-1" @click="enviarMensaje(usuario1.name.first, mensajeUsuario1, 'usuario1')">Enviar</button>
            </div>
        </div>

        <div class="col-6">
            <SalaDeChat :mensajes="mensajes" />
        </div>

        <div class="col-3 text-center">
            <div class="chat__foto" v-if="usuario2.picture">
                <img :src="usuario2.picture.large" alt="Foto usuario 2">
            </div>
            <h5 class="chat" v-if="usuario2.name">
                {{ usuario2.name.title }} {{ usuario2.name.first }}
            </h5>
            <div class="chat__mens d-flex flex-column">
                <textarea v-model="mensajeUsuario2" placeholder="Escribe un mensaje..."></textarea>
                <button class="chat__boton2 m-1" @click="enviarMensaje(usuario2.name.first, mensajeUsuario2, 'usuario2')">Enviar</button>
            </div>
        </div>
    </section>
</template>

<script>
import axios from 'axios';
import SalaDeChat from './SalaDeChat.vue';

export default {
    name: 'Mensajes',
    components: {
        SalaDeChat
    },
    data() {
        return {
            usuario1: {},
            usuario2: {},
            mensajeUsuario1: '',
            mensajeUsuario2: '',
            mensajes: []
        };
    },
    created() {
        this.obtenerUsuarios();
    },
    methods: {
        obtenerUsuarios() {
            Promise.all([
                axios.get('https://randomuser.me/api/'),
                axios.get('https://randomuser.me/api/')
            ])
            .then(([response1, response2]) => {
                this.usuario1 = response1.data.results[0];
                this.usuario2 = response2.data.results[0];
            })
            .catch(error => {
                console.log('Error en la obtención de Usuarios', error);
            });
        },
        enviarMensaje(nombre, texto, autor) {
            if (texto.trim() !== '') {
                this.mensajes.push({ nombre, texto, autor });
                if (autor === 'usuario1') this.mensajeUsuario1 = '';
                if (autor === 'usuario2') this.mensajeUsuario2 = '';
            }
        }
    }
};
</script>

<style>
.container {
    background-color: #f2f2ff; /* Fondo suave */
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    padding: 20px;
}

.chat__foto img {
    border: 3px solid #ff9ecb; /* Bordes de la foto */
    border-radius: 50%; /* Fotos redondas */
    width: 100px;
    height: 100px;
}

h5 {
    color: #ff9ecb; /* Títulos en color rosa */
    font-family: 'Dancing Script', cursive; /* Fuente estilizada */
}

.chat__mens textarea {
    border: 1px solid #ff9ecb;
    border-radius: 5px;
    padding: 10px;
}

.chat__boton1, .chat__boton2 {
    background-color: #8ac1ff; /* Botón de envío en azul claro */
    color: white;
    border: none;
    border-radius: 5px;
    padding: 5px 10px;
    cursor: pointer;
    transition: background-color 0.3s;
}

.chat__boton1:hover, .chat__boton2:hover {
    background-color: #4da1ff; /* Color de hover */
}
</style>
