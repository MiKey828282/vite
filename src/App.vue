<template>
  <div>
    <div  class="form-container">
    <h2>Formulario de Registro</h2>

    <!-- Formulario -->
    <form @submit.prevent="registrarUsuario">
      <div>
        <label for="nombre">Nombre:  </label>
        <input type="text" id="nombre" v-model="nuevoUsuario.nombre">
        <p v-if="errores.nombre" style="color: red;">{{ errores.nombre }}</p>
      </div>

      <div>
        <label for="edad">Edad:  </label>
        <input type="number" id="edad" v-model="nuevoUsuario.edad">
        <p v-if="errores.edad" style="color: red;">{{ errores.edad }}</p>
      </div>

      <div>
        <label for="email">Email:  </label>
        <input type="email" id="email" v-model="nuevoUsuario.email">
        <p v-if="errores.email" style="color: red;">{{ errores.email }}</p>
      </div>

      <div>
        <p><label for="genero">Género:</label></p>
        <div class="radio-group">
          <input type="radio" id="hombre" value="Hombre" v-model="nuevoUsuario.genero">
          <label for="hombre">Hombre</label>
          <input type="radio" id="mujer" value="Mujer" v-model="nuevoUsuario.genero">
          <label for="mujer">Mujer</label>
        </div>
        <!-- Mensaje de error del campo género -->
        <p v-if="errores.genero" style="color: red;">{{ errores.genero }}</p>
      </div>

      <button type="submit">Registrarse</button>
    </form>
  </div>

    <!-- Tabla -->
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
      usuarios: [],
      errores: {
        nombre: '',
        edad: '',
        email: '',
        genero: ''
      }
    };
  },
  methods: {
    registrarUsuario() {
      // quitar los mensajes
      this.errores = {
        nombre: '',
        edad: '',
        email: '',
        genero: ''
      };

      let esValido = true;

      if (!this.nuevoUsuario.nombre) {
        this.errores.nombre = 'El campo "Nombre" es obligatorio.';
        esValido = false;
      }

      if (!this.nuevoUsuario.edad) {
        this.errores.edad = 'El campo "Edad" es obligatorio.';
        esValido = false;
      }

      if (!this.nuevoUsuario.email) {
        this.errores.email = 'El campo "Email" es obligatorio.';
        esValido = false;
      }

      if (!this.nuevoUsuario.genero) {
        this.errores.genero = 'Selecciona un "Género" es obligatorio.';
        esValido = false;
      }

      // Si todos los campos son válidos, agregar el usuario
      if (esValido) {
        this.usuarios.push({...this.nuevoUsuario});

        // pa limpiar el formulario
        this.nuevoUsuario.nombre = '';
        this.nuevoUsuario.edad = '';
        this.nuevoUsuario.email = '';
        this.nuevoUsuario.genero = '';
      }
    }
  }
};
</script>

<style scoped>

h2 {
    text-align: center;
    margin-bottom: 1em;
}

.form-container {
    background: #191E29;
    padding: 2em;
    border-radius: 10px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    max-width: 400px;
    width: 100%;
}
form {
  margin-bottom: 20px;
}

form div {
  display:block;
  align-items: center; /* Alinea verticalmente el contenido dentro de cada div */
  margin-bottom: 30px;
}

p {
  margin: 0;
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

label {
    margin-bottom: 0.5em;
    margin-right: 10px;
    font-weight: bold;
    width: 100px;
}

input, select {
    padding: 0.5em;
    margin-bottom: 1em;
    border: transparent;
    border-radius: 5px;
    background-color: #696e79;
}
button {
    padding: 0.75em;
    border: none;
    border-radius: 5px;
    background: #01c38d;
    color: white;
    font-weight: bold;
     
}

</style>
