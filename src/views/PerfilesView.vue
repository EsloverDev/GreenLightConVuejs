<template>
    <div class="perfil">
        <div class="componentes">
            <FormularioPerfiles/>
            <TablaPerfiles/>
        </div>
    </div>
</template>

<script>
import FormularioPerfiles from "@/components/FormularioPerfiles.vue";
import TablaPerfiles from "@/components/TablaPerfiles.vue";

export default {
    name: 'PerfilesView',

    components: {
        FormularioPerfiles,
        TablaPerfiles
    }
}
</script>

<style>
body {
    font-family: Arial, sans-serif;
    background-color: #457b9d;
    margin: 0;
    padding: 0;
}

.componentes {
    display: grid;
    grid-template-columns: 1fr 2fr;
    grid-auto-rows: 1fr;
}

.contenedor_formulario {
    margin: 1rem;
    padding: 1rem;
    background-color: #edede9;
    box-shadow: 0px 2px 20px 0px rgba(0,0,0,0.5);
    border-radius: 20px;
}

h1 {
    text-align: center;
    margin-bottom: 15px;
}

form {
    padding: 2%;
}

.linea_formulario {
    margin-bottom: 15px;
}

label {
    display: block;
    margin-bottom: 5px;
    font-weight: bold;
}

input {
    width: 100%;
    padding: 8px;
    border: 1px solid #457b9d;
    border-radius: 5px;
}

button {
    display: block;
    width: 100%;
    padding: 10px;
    background-color: #588157;
    font-size: 16px;
    font-weight: bold;
    border-radius: 12px;
    transition-duration: 0.4s;
    cursor: pointer;
    border: solid;
}

button:hover{
    background-color: #edede9;
    border: solid #588157;
}

table {
    width: 100%;
    border-collapse: collapse;
    margin-bottom: 20px;
}

th, td {
    padding: 10px;
    text-align: left;
    border-style: solid;
}

tr {
    border-style: solid;
}

th {
    background-color: #588157;
    text-align: center;
    border-style: solid;
    font-size: 16px;
    font-weight: bold;
}

tr:hover{
    background-color: #457b9d;
}
</style>