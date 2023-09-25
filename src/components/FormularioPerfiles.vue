<template>
    <div class="contenedor_formulario">
        <h1>Formulario de usuarios</h1>
        <form id="formulario_perfiles" @submit.prevent ="guardar">
            <div class="linea_formulario">
                <label for="codigo">C&oacute;digo</label>
                <input type="text" id="codigo" name="codigo" required v-model="codigo" />
            </div>
            <div class="linea_formulario">
                <label for="nombre">Nombre</label>
                <input type="text" id="nombre" name="nombre" required v-model="nombre" />
            </div>
            <div class="linea_formulario">
                <label for="apellido">Apellido</label>
                <input type="text" id="apellido" name="apellido" required v-model="apellido" />
            </div>
            <div class="linea_formulario">
                <label for="edad">Edad</label>
                <input type="number" id="edad" name="edad" required v-model="edad" />
            </div>

            <button type="submit" id="guardar" name="guardar">Guardar</button><br>
            <button type="button" id="eliminar" name="eliminar" @click="eliminar">Eliminar</button><br>
            <button type="button" id="actualizar" name="actualizar" @click="actualizar">Actualizar</button><br>
            <button type="button" id="consultar" name="consultar" @click="consultar">Consultar</button><br>
        </form>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    data(){
        return {
            codigo: "",
            nombre: "",
            apellido: "",
            edad: null,
        };
    },

    methods: {
        guardar() {
            axios
                .post("http://localhost:8080/api/usuarios", {
                    codigo: this.codigo,
                    nombre: this.nombre,
                    apellido: this.apellido,
                    edad: this.edad,
                })
                .then((response) => {
                    console.log("Usuario registrado con éxito:", response.data);
                    alert("Usuario registrado con éxito");
                    this.codigo = '';
                    this.nombre = '';
                    this.apellido = '';
                    this.edad = '';
                })
                .catch((error) => {
                    console.error("Error registrando el usuario", error);
                });
        },

        consultar() {
            axios
                .get("http://localhost:8080/api/usuarios/"+this.codigo)
                .then((response) => {
                    //Actualizar los campos del formulario con los datos del estudiante consultado
                    this.nombre = response.data.nombre;
                    this.apellido = response.data.apellido;
                    this.edad = response.data.edad;
                })
                .catch((error) => {
                    console.error("Error al consultar usuario", error);
                });
        },

        actualizar() {
            axios
                .put("http://localhost:8080/api/usuarios/actualizar/"+this.codigo, {
                    codigo: this.codigo,
                    nombre: this.nombre,
                    apellido: this.apellido,
                    edad: this.edad,
                })
                .then((response) => {
                    console.log("Usuario actualizado con éxito", response.data);
                })
                .catch((error) => {
                    console.error("Error al actualizar el usuario", error);
                });
        },

        eliminar() {
            axios
                .delete("http://localhost:8080/api/usuarios/"+this.codigo)
                .then(() => {
                    console.log("Usuario eliminado con éxito");
                    //Limpiar los campos del formulario después de eliminar
                    this.codigo = "";
                    this.nombre = "";
                    this.apellido = "";
                    this.edad = null;
                })
                .catch((error) => {
                    console.error("Error al eliminar el usuario", error);
                });
        },
    }
}
</script>