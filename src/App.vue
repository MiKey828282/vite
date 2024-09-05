<template>
  <div>
    <h2>Formulario de Registro</h2>
    
    <!-- Formulario -->
    <form @submit.prevent="registrarUsuario">
      <div>
        <label for="nombre">Nombre:</label>
        <input type="text" id="nombre" v-model="nuevoUsuario.nombre" required>
      </div>

      <div>
        <label for="edad">Edad:</label>
        <input type="number" id="edad" v-model="nuevoUsuario.edad" required>
      </div>

      <div>
        <label for="email">Email:</label>
        <input type="email" id="email" v-model="nuevoUsuario.email" required>
      </div>

      <div>
        <label for="genero">Género:</label>
        <select v-model="nuevoUsuario.genero">
          <option value="Masculino">Masculino</option>
          <option value="Femenino">Femenino</option>
          <option value="Otro">Otro</option>
        </select>
      </div>

      <button type="submit">Registrarse</button>
    </form>

    <!-- Tabla que muestra los datos -->
    <h2>Usuarios Registrados</h2>
    <table v-if="usuarios.length">
      <thead>
        <tr>
          <th>Nombre</th>
          <th>Edad</th>
          <th>Email</th>
          <th>Género</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(usuario, index) in usuarios" :key="index">
          <td>{{ usuario.nombre }}</td>
          <td>{{ usuario.edad }}</td>
          <td>{{ usuario.email }}</td>
          <td>{{ usuario.genero }}</td>
        </tr>
      </tbody>
    </table>
    <p v-else>No hay usuarios registrados aún.</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      nuevoUsuario: {
        nombre: '',
        edad: '',
        email: '',
        genero: ''
      },
      usuarios: []
    };
  },
  methods: {
    registrarUsuario() {
      // Añadir el nuevo usuario a la lista de usuarios registrados
      this.usuarios.push({...this.nuevoUsuario});
      
      // Limpiar el formulario
      this.nuevoUsuario.nombre = '';
      this.nuevoUsuario.edad = '';
      this.nuevoUsuario.email = '';
      this.nuevoUsuario.genero = '';
    }
  }
};
</script>

<style scoped>
form {
  margin-bottom: 20px;
}
form div {
  margin-bottom: 10px;
}
table {
  width: 100%;
  border-collapse: collapse;
}
table, th, td {
  border: 1px solid black;
}
th, td {
  padding: 8px;
  text-align: left;
}
</style>
