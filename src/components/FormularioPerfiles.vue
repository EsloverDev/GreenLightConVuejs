<template>
    <div class="contenedor_formulario">
        <h1>Formulario de perfiles</h1>
        <form id="formulario_perfiles" @submit.prevent ="guardar">
            <div class="linea_formulario">
                <label for="nombre">Nombre</label>
                <input type="text" id="nombre" name="nombre" required v-model="nombre" />
            </div>
            <div class="linea_formulario">
                <label for="password">Contraseña</label>
                <input type="text" id="password" name="password" required v-model="password" />
            </div>
            <div class="linea_formulario">
                <label for="email">E-mail</label>
                <input type="text" id="email" name="email" required v-model="email" />
            </div>
            <div class="linea_formulario">
                <label for="telefono">Tel&eacute;fono</label>
                <input type="text" id="telefono" name="telefono" required v-model="telefono" />
            </div>
            <div class="linea_formulario">
                <label for="pais">Pa&iacute;s</label>
                <input type="text" id="pais" name="pais" required v-model="pais" />
            </div>
            <div class="linea_formulario">
                <label for="ciudad">Ciudad</label>
                <input type="text" id="ciudad" name="ciudad" required v-model="ciudad" />
            </div>
            <div class="linea_formulario">
                <label for="localidad">Localidad</label>
                <input type="text" id="localidad" name="localidad" required v-model="localidad" />
            </div>
            <div class="linea_formulario">
                <label for="documento">Documento</label>
                <input type="text" id="documento" name="documento" required v-model="documento" />
            </div>
            <button type="submit" id="guardar" name="guardar">Guardar</button><br>
            <button type="button" id="eliminar" name="eliminar" @click="eliminar">Eliminar</button><br>
            <button type="button" id="actualizar" name="actualizar" @click="actualizar">Actualizar</button><br>
            <button type="button" id="consultar" name="consultar" @click="consultar">Buscar por Email</button><br>
        </form>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    data(){
        return {
            id: "",
            nombre: "",
            password: "",
            email: "",
            telefono: "",
            pais: "",
            ciudad: "",
            localidad: "",
            documento: "",
        };
    },

    methods: {
        guardar() {
            axios
                .post("http://localhost:8080/api/perfiles", {
                    nombre: this.nombre,
                    password: this.password,
                    email: this.email,
                    telefono: this.telefono,
                    pais: this.pais,
                    ciudad: this.ciudad,
                    localidad: this.localidad,
                    documento: this.documento
                })
                .then((response) => {
                    console.log("Usuario registrado con éxito:", response.data);
                    alert("Usuario registrado con éxito");
                    this.nombre = '';
                    this.password = '';
                    this.email = '';
                    this.telefono = '';
                    this.pais = '';
                    this.ciudad = '';
                    this.localidad = '';
                    this.documento = '';
                })
                .catch((error) => {
                    console.error("Error registrando el usuario", error);
                });
        },

        consultar() {
            axios
                .get("http://localhost:8080/api/perfiles/"+this.email)
                .then((response) => {
                    //Actualizar los campos del formulario con los datos del estudiante consultado
                    this.nombre = response.data.nombre;
                    this.password = response.data.password;
                    this.email = response.data.email;
                    this.telefono = response.data.telefono;
                    this.pais = response.data.pais;
                    this.ciudad = response.data.ciudad;
                    this.localidad = response.data.localidad;
                    this.documento = response.data.documento;
                })
                .catch((error) => {
                    console.error("Error al consultar usuario", error);
                });
        },

        actualizar() {
            axios
                .put("http://localhost:8080/api/perfiles/actualizar/"+this.email, {
                    nombre: this.nombre,
                    password: this.password,
                    email: this.email,
                    telefono : this.telefono,
                    pais: this.pais,
                    ciudad: this.ciudad,
                    localidad: this.localidad,
                    documento: this.documento,
                })
                .then((response) => {
                    console.log("Usuario actualizado con éxito", response.data);
                    alert("Usuario actualizado con éxito");
                })
                .catch((error) => {
                    console.error("Error al actualizar el usuario", error);
                    alert("Error al actualizar el usuario");
                });
        },

        eliminar() {
            axios
                .delete("http://localhost:8080/api/perfiles/"+this.email)
                .then(() => {
                    console.log("Usuario eliminado con éxito");
                    alert("Usuario eliminado con éxito");
                    //Limpiar los campos del formulario después de eliminar
                    this.nombre = "";
                    this.password = "";
                    this.email = "";
                    this.telefono = "";
                    this.pais = "";
                    this.ciudad = "";
                    this.localidad = "";
                    this.documento = "";
                })
                .catch((error) => {
                    console.error("Error al eliminar el usuario", error);
                    alert("Error al eliminar el usuario");
                });
        },
    }
}
</script>