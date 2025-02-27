<script setup>
  import { ref, reactive, onMounted, watch } from "vue";
  import { uid } from "uid";
  import Header from "./components/Header.vue";
  import Formulario from "./components/Formulario.vue";
  import Paciente from "./components/Paciente.vue";

  const pacientes = ref([]);

  const paciente = reactive({
    id: null,
    nombre: "",
    edad: "",
    email: "",
    telefono: "",
    fecha: "",
    sintomas: "",
  });

  onMounted(() => {
    if (localStorage.getItem("pacientes")) {
      pacientes.value = JSON.parse(localStorage.getItem("pacientes"));
    }
  });

  watch((pacientes), () => {
      guardarPacientes();
  },{
      deep: true
  });

  const guardarPacientes = () => {
    localStorage.setItem("pacientes", JSON.stringify(pacientes.value));
  };

  const agregarPaciente = () => {
    if (paciente.id) { //edición
      const index = pacientes.value.findIndex( pacienteState => pacienteState.id === paciente.id);
      pacientes.value[index] = { ...paciente };
      paciente.id = null;
    } else {
      pacientes.value.push({ ...paciente, id: uid() });
    }

    paciente.nombre = "";
    paciente.edad = "";
    paciente.email = "";
    paciente.telefono = "";
    paciente.fecha = "";
    paciente.sintomas = "";
    paciente.id = null;
  };

  const actualizarPaciente = (id) => {
    const pacienteEditar = pacientes.value.filter( (paciente) => paciente.id === id)[0];
    Object.assign(paciente, pacienteEditar);
  };


  const eliminarPaciente = (id) => {
    pacientes.value = pacientes.value.filter( (paciente) => paciente.id != id)
  };
  

</script>

<template>
  <div class="container mx-auto mt-30">
      <Header />

      <div class="mt-12 md:flex">
          <Formulario
            v-model:nombre="paciente.nombre"
            v-model:edad="paciente.edad"
            v-model:email="paciente.email"
            v-model:telefono="paciente.telefono"
            v-model:fecha="paciente.fecha"
            v-model:sintomas="paciente.sintomas"
            @guardar-paciente="agregarPaciente"
            :id = "paciente.id"
          />
      
          <div class="md:w-1/2 md:h-screen overflow-y-auto">
            <h3 class="font-black text-3xl text-center">
              Administra tus Pacientes
            </h3>
            <div v-if="pacientes.length > 0">
              <p class="text-lg mt-4 text-center mb-10">
                Información de
                <span class="text-lime-600 font-bold">Pacientes</span>
              </p>
              <Paciente
                v-for="paciente in pacientes"
                :paciente="paciente"
                @eliminar-paciente="eliminarPaciente"
                @actualizar-paciente="actualizarPaciente"
              />
            </div>
            <p v-else class="mt-20 text-2xl text-center">No hay pacientes</p>
          </div>
      </div>
  </div>
</template>
