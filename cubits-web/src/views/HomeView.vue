<script setup lang="ts">
import DataTable from 'primevue/datatable';
import Column from 'primevue/column';
import { ref, onMounted } from 'vue';
import 'primeicons/primeicons.css';


const userList = ref([]);
const dateFrom = '01-01-2022';
const dateTo = '01-01-2025';


const getUserList = async () => {
  const url = `http://localhost:5000/api/users?From=${dateFrom}&To=${dateTo}`;

  try {
    const response = await fetch(url);
    // Procesar la respuesta
    const data = await response.json();
    userList.value = data.userList;
    console.log(data);

  } catch (error) {
    console.error('Error al obtener los datos:', error);
  }
}


onMounted(async () => {
  await getUserList();

});

</script>

<template>
  <main>
  <h3 style="text-align: center;">Cubits Clade Code</h3>
    <div>
      <DataTable :value="userList" class="custom-table" stripedRows>
        <Column field="userId" header="Google ID" :sortable="true" class="google-column"></Column>
        <Column field="roleName" header="Role Name" class="role-column"></Column>
      </DataTable>
    </div>
  </main>
</template>

<style>
/* Estilos CSS */
h3 {
  color: #101bb9;
}

.custom-table {
  border: 1px solid #000000;
  border-radius: 5px;
  overflow: hidden;
}

.google-column {
  font-weight: bold;
  border: 0.1px solid #000000;
  color: #020813; /* Color azul de Google */
}

.role-column {
  border: 0.1px solid #000000;
  font-weight: bold;
  text-transform: capitalize; /* Convertir texto a mayúsculas al inicio de cada palabra */
}
</style>
