<template>
    <div class="container mt-5">
      <!-- Título de la Aplicación -->
      <h1 class="text-center mb-5 text-primary">Gestión de Personajes de Arcane</h1>
  
      <!-- Formulario para añadir personajes -->
      <div class="card shadow-lg border-light p-4 mb-5 rounded">
        <h2 class="h4 mb-4 text-dark">Añadir Personaje</h2>
        <form @submit.prevent="addCharacter">
          <div class="mb-4">
            <label for="name" class="form-label text-muted">Nombre</label>
            <input type="text" v-model="newCharacter.name" id="name" class="form-control form-control-lg" placeholder="Ejemplo: Jinx" required />
          </div>
  
          <div class="mb-4">
          <label for="origin" class="form-label text-muted">Origen</label>
          <select v-model="newCharacter.origin" id="origin" class="form-control form-control-lg" required>
            <option value="Aguas Estancadas">Aguas Estancadas</option>
            <option value="Ciudad de Bandle">Ciudad de Bandle</option>
            <option value="Demacia">Demacia</option>
            <option value="El Vacio">El Vacío</option>
            <option value="Freljord">Freljord</option>
            <option value="Islas de las Sombras">Islas de las Sombras</option>
            <option value="Ixtal">Ixtal</option>
            <option value="Jonia">Jonia</option>
            <option value="Noxus">Noxus</option>
            <option value="Piltover">Piltover</option>
            <option value="Shurima">Shurima</option>
            <option value="Targon">Targon</option>
            <option value="Zaun">Zaun</option>
          </select>
        </div>
  
          <div class="mb-4">
            <label for="specialAbility" class="form-label text-muted">Habilidad Especial</label>
            <input type="text" v-model="newCharacter.specialAbility" id="specialAbility" class="form-control form-control-lg" placeholder="Ejemplo: Manipulación de explosivos" required />
          </div>
  
          <div class="mb-4">
            <label for="allies" class="form-label text-muted">Lista de Aliados</label>
            <input type="text" v-model="newCharacter.allies" id="allies" class="form-control form-control-lg" placeholder="Separados por coma (Ejemplo: Ekko, Caitlyn)" />
          </div>
  
          <div class="form-check mb-4">
            <input type="checkbox" v-model="newCharacter.missionComplete" id="missionComplete" class="form-check-input" />
            <label class="form-check-label text-muted" for="missionComplete">¿Cumplió su misión principal?</label>
          </div>
  
          <button type="submit" class="btn btn-primary btn-lg w-100">Añadir Personaje</button>
        </form>
      </div>
  
   <!-- Tabla de personajes registrados -->
   <div class="card shadow-lg border-light p-4 rounded">
        <h2 class="h4 mb-4 text-dark">Personajes Registrados</h2>
        <table class="table table-hover table-bordered table-striped">
          <thead class="thead-dark">
            <tr>
              <th>Nombre</th>
              <th>Origen</th>
              <th>Habilidad Especial</th>
              <th>Aliados</th>
              <th>Misión Cumplida</th>
            </tr>
          </thead>
          <tbody>
            <!--utilizamos v-for para iterar sobre los personajes y crear una fila para cada uno-->
            <tr v-for="(character, index) in characters" :key="index">
              <td>{{ character.name }}</td>
              <td>{{ character.origin }}</td>
              <td>{{ character.specialAbility }}</td>
              <td>{{ character.allies }}</td>
              <!-- si el personaje cumplió su misión principal, mostrar "Sí", de lo contrario mostrara "No" -->
              <td><span class="badge" :class="character.missionComplete ? 'bg-success' : 'bg-danger'">{{ character.missionComplete ? 'Sí' : 'No' }}</span></td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </template>
  
  <script>
  import { ref } from 'vue';
  
  export default {
    name: 'App',
    setup() {
      const newCharacter = ref({
        name: '',
        origin: '',
        specialAbility: '',
        allies: '',
        missionComplete: false,
      });
  
      const characters = ref([]);
  
      const addCharacter = () => {
        characters.value.push({ ...newCharacter.value });
        newCharacter.value = {
          name: '',
          origin: '',
          specialAbility: '',
          allies: '',
          missionComplete: false,
        };
      };
  
      return {
        newCharacter,
        characters,
        addCharacter,
      };
    },
  };
  </script>
  
  <style scoped>
  /* Estilos generales */
  body {
    font-family: 'Roboto', sans-serif;
    background-color: #f8f9fa;
  }
  
  .container {
    max-width: 960px;
    margin: 0 auto;
  }
  
  h1 {
    font-weight: 700;
    color: #0d6efd;
    font-size: 2.5rem;
  }
  
  h2 {
    font-weight: 600;
    color: #343a40;
  }
  
  .card {
    background-color: #ffffff;
    border-radius: 12px;
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
  }
  
  .form-label {
    font-weight: 500;
  }
  
  .form-control-lg {
    border-radius: 10px;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  }
  
  .form-check-input {
    border-radius: 5px;
  }
  
  button.btn {
    font-weight: 600;
    padding: 12px;
    border-radius: 10px;
    transition: all 0.3s;
  }
  
  button.btn:hover {
    background-color: #0056b3;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  }
  
  .table th, .table td {
    vertical-align: middle;
    text-align: center;
  }
  
  .table th {
    background-color: #007bff;
    color: white;
  }
  
  .table td {
    background-color: #ffffff;
  }
  
  .table-hover tbody tr:hover {
    background-color: #f1f1f1;
  }
  
  .badge {
    font-size: 0.85rem;
    padding: 8px 15px;
  }
  
  .bg-success {
    background-color: #28a745 !important;
  }
  
  .bg-danger {
    background-color: #dc3545 !important;
  }
  </style>
  