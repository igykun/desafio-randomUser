<template>
    <div class="chat__sala">
        <div v-for="(mensaje, index) in mensajes" :key="index" :class="{'mensaje--usuario1': mensaje.autor === 'usuario1', 'mensaje--usuario2': mensaje.autor === 'usuario2'}">
            <strong>{{ mensaje.nombre }}:</strong> {{ mensaje.texto }}
        </div>
    </div>
</template>

<script>
export default {
    name: 'SalaDeChat',
    props: {
        mensajes: {
            type: Array,
            required: true
        }
    }
};
</script>

<style scoped>
.chat__sala {
    background-color: #ffffff; /* Fondo blanco */
    border: 1px solid #ff9ecb; /* Bordes de la sala de chat */
    border-radius: 10px;
    padding: 10px;
    height: 300px;
    overflow-y: auto;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.mensaje--usuario1 {
    color: #ff6f9e; /* Mensajes de usuario 1 en rosa */
    text-align: left;
    background-color: #ffe5ef; /* Fondo suave */
    border-radius: 5px;
    padding: 5px;
    margin: 5px 0;
}

.mensaje--usuario2 {
    color: #8ac1ff; /* Mensajes de usuario 2 en azul claro */
    text-align: right;
    background-color: #e5f3ff; /* Fondo suave */
    border-radius: 5px;
    padding: 5px;
    margin: 5px 0;
}
</style>
