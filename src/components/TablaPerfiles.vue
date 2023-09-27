<template>
    <div class="contenedor_formulario">
        <h1>Tabla de Perfiles</h1>
        <table>
            <thead>
                <tr>
                    <th>Nombre</th>
                    <th>Email</th>
                    <th>Telefono</th>
                    <th>País</th>
                    <th>Ciudad</th>
                    <th>Localidad</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="perfil in perfiles" :key="perfil.id">
                    <td>{{ perfil.nombre }}</td>
                    <td>{{ perfil.email }}</td>
                    <td>{{ perfil.telefono }}</td>
                    <td>{{ perfil.pais }}</td>
                    <td>{{ perfil.ciudad }}</td>
                    <td>{{ perfil.localidad }}</td>
                </tr>
                <RouterView/>
            </tbody>
        </table>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    data() {
        return {
            perfiles: [],
        };
    },
    methods: {
        obtenerPerfiles(){
            //Método para obtener la lista de todos los perfiles
            axios.get("http://localhost:8080/api/perfiles/listar")
            .then((Response) => {
                this.perfiles = Response.data;
            })
            .catch((error) => {
                console.error("Error al obtener usuarios:", error);
            });
        },
    },
    mounted() {
        //Llamar al método para obtener la lista de usuarios al cargar el componente
        this.obtenerPerfiles();
    },
};
</script>