<script setup>

</script>

<template>
    <div class="md:w-1/2">
        <h2 class="text-3xl text-center font-black">Seguimiento pacientes</h2>

        <p class="text-lg mt-4 text-center mb-10">
            Añada Pacientes y 
            <span class="text-lime-600 font-bold">Administralos</span>
        </p>

        <form 
            class="bg-white shadow-md rounded-lg py-10 px-5 mb-10"
            action="">
                <div class="mb-5">
                    <label for="paciente" class="block text-gray uppercase font-bold">Nombre del paciente</label>
                    <input type="text" id="paciente" placeholder="Nombre del paciente" class="w-full p-2 border-2 placeholder-gray-400 rounded-md border-gray-200" />
                </div>
                <div class="mb-5">
                    <label for="edad" class="block text-gray uppercase font-bold">Edad</label>
                    <input type="number" id="edad" placeholder="Edad del paciente" class="w-full p-2 border-2 placeholder-gray-400 rounded-md border-gray-200" />
                </div>
                <div class="mb-5">
                    <label for="email" class="block text-gray uppercase font-bold">Correo electronico</label>
                    <input type="email" id="email" placeholder="Correo del paciente" class="w-full p-2 border-2 placeholder-gray-400 rounded-md border-gray-200" />
                </div>
                <div class="mb-5">
                    <label for="telefono" class="block text-gray uppercase font-bold">Telefono</label>
                    <input type="text" id="telefono" placeholder="Telefono del paciente" class="w-full p-2 border-2 placeholder-gray-400 rounded-md border-gray-200" />
                </div>
                
        </form>
    </div>
</template>

<style lang="scss" scoped>

</style>