<template>
  <div>
    <h2>Filtrar Usuarios</h2>
    <input type="text" v-model="search" placeholder="Buscar por nombre" />

    <div v-if="loading">Cargando usuarios...</div>
    <div v-else>
      <p v-if="filteredUsers.length === 0">No se encontraron resultados</p>
      <p v-else>Mostrando {{ filteredUsers.length }} de {{ users.length }} usuarios</p>
      
      <ul>
        <li v-for="user in filteredUsers" :key="user.id">
          {{ user.name }} ({{ user.email }})
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import { ref, computed, onMounted } from "vue";

export default {
  name: "UserFilter",
  setup() {
    const users = ref([]);
    const search = ref("");
    const loading = ref(true);

    // Función para cargar los usuarios desde la API
    const fetchUsers = async () => {
      try {
        const res = await fetch("https://jsonplaceholder.typicode.com/users");
        users.value = await res.json();
      } catch (error) {
        console.error("Error al obtener usuarios:", error);
      } finally {
        loading.value = false;
      }
    };

    onMounted(fetchUsers);

    // Computed property para filtrar usuarios
    const filteredUsers = computed(() =>
      users.value.filter(user =>
        user.name.toLowerCase().includes(search.value.toLowerCase())
      )
    );

    return { users, search, loading, filteredUsers };
  }
};
</script>

<style scoped>
input {
  margin-bottom: 1em;
  padding: 0.5em;
  width: 300px;
}
ul {
  list-style: none;
  padding: 0;
}
li {
  margin: 0.3em 0;
}
</style>


//Por qué usamos computed y onMounted:

onMounted → cargamos los datos desde la API solo cuando el componente está listo.

filteredUsers → se actualiza automáticamente cuando cambias search.

loading → permite mostrar un mensaje mientras llegan los datos.

Mostramos mensajes de "No se encontraron resultados" y "Mostrando X de Y usuarios" usando computed y lógica de Vue.