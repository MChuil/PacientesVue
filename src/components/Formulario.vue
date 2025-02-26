<script setup>
    import {reactive} from 'vue';
    import Alerta from './Alerta.vue';

    const alerta = reactive({
        titulo: '',
        mensaje: '',
        color: ''
    });

    const emit = defineEmits([
        'update:nombre',
        'update:edad',
        'update:email',
        'update:telefono',
        'update:fecha',
        'update:sintomas',
        'guardar-paciente',
        'id'
    ]);


    const props = defineProps({
        nombre: {
            type: String,
            required: true
        },
        edad: {
            type: String,
            required: true
        },
        email: {
            type: String,
            required: true
        },
        telefono: {
            type: String,
            required: true
        },
        fecha: {
            type: String,
            required: true
        },
        sintomas: {
            type: String,
            required: true
        },
        id:{
            type: Number,
            required: false
        }
    });
    

    const validar = e => {
        if(Object.values(props).includes('')){
            alerta.titulo = 'Atención';
            alerta.mensaje = 'Todos los campos son obligatorios';
            alerta.color = 'red';
            return;
        }

        emit('guardar-paciente');
        sintomas.value = '';
        alerta.titulo = 'Paciente registrado';
        alerta.mensaje = 'El paciente se ha registrado correctamente';
        alerta.color = 'green';
        setTimeout(() => {
            alerta.titulo = '';
            alerta.mensaje = '';
            alerta.color = '';
        }, 3000);
    }
</script>

<template>
    <div class="md:w-1/2">
        <h2 class="text-3xl text-center font-black">Seguimiento pacientes</h2>

        <p class="text-lg mt-4 text-center mb-10">
            Añada Pacientes y 
            <span class="text-lime-600 font-bold">Administralos</span>
        </p>
        <form class="bg-white shadow-md rounded-lg py-10 px-5 mb-10" @submit.prevent="validar">
            <Alerta 
                v-if="alerta.mensaje"
                :alerta="alerta" 
            />
            <div class="mb-5">
                <label for="nombre" class="block text-gray uppercase font-bold">Nombre del paciente</label>
                <input type="text" id="nombre" placeholder="Nombre del paciente" class="w-full p-2 border-2 placeholder-gray-400 rounded-md border-gray-200"
                :value = "nombre"
                @input ="$emit('update:nombre', $event.target.value)"
                />
            </div>
            <div class="mb-5">
                <label for="edad" class="block text-gray uppercase font-bold">Edad</label>
                <input type="number" id="edad" placeholder="Edad del paciente" class="w-full p-2 border-2 placeholder-gray-400 rounded-md border-gray-200"
                :value = "edad"
                @input ="$emit('update:edad', $event.target.value)"
                />
            </div>
            <div class="mb-5">
                <label for="email" class="block text-gray uppercase font-bold">Correo electronico</label>
                <input type="email" id="email" placeholder="Correo del paciente" class="w-full p-2 border-2 placeholder-gray-400 rounded-md border-gray-200"
                :value = "email"
                @input ="$emit('update:email', $event.target.value)"
                />
            </div>
            <div class="mb-5">
                <label for="telefono" class="block text-gray uppercase font-bold">Telefono</label>
                <input type="number" id="telefono" placeholder="Telefono del paciente" class="w-full p-2 border-2 placeholder-gray-400 rounded-md border-gray-200"
                :value = "telefono"
                @input ="$emit('update:telefono', $event.target.value)"
                />
            </div>
            <div class="mb-5">
                <label for="fecha" class="block text-gray uppercase font-bold">Fecha</label>
                <input type="date" id="fecha" class="w-full p-2 border-2 placeholder-gray-400 rounded-md border-gray-200"
                :value = "fecha"
                @input ="$emit('update:fecha', $event.target.value)"
                />
            </div>
                <div class="mb-5">
                    <label for="sintomas" class="block text-gray uppercase font-bold">Sintomas o causa de la consulta</label>
                    <textarea 
                        id="sintomas" 
                        class="w-full p-2 border-2 placeholder-gray-400 rounded-md border-gray-200 h-45"
                        :value = "sintomas"
                        @input ="$emit('update:sintomas', $event.target.value)"
                        palceholder="Describe los sintomas" 
                    ></textarea>
                </div>
                <button type="sumbit"class="bg-lime-600 text-center text-white uppercase font-bold py-2 px-5 rounded-md w-full hover:bg-lime-800 cursor-pointer transition-color">{{ (id) ? 'Actualizar paciente': 'Registrar paciente' }}</button>
        </form>
    </div>
</template>

<style lang="scss" scoped>

</style>