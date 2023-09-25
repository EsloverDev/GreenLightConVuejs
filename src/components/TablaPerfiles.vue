<template>
    <div class="contenedor_formulario">
        <h1>Tabla de usuarios</h1>
        <table>
            <thead>
                <tr>
                    <th>C&oacute;digo</th>
                    <th>Nombre</th>
                    <th>Apellido</th>
                    <th>Edad</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="perfil in perfiles" :key="perfil.codigo">
                    <td>{{ perfil.codigo }}</td>
                    <td>{{ perfil.nombre }}</td>
                    <td>{{ perfil.apellido }}</td>
                    <td>{{ perfil.edad }}</td>
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
            axios.get("http://localhost:8080/api/usuarios/listar")
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