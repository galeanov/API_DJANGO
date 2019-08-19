<template lang="html">

<div class="container">
    <div class="row">
        <div class="col text-left">
          <div class="">
            <h2>Listado de libros</h2>
            <b-button size="sm" :to="{name: 'NuevoDatos'}" variant="primary">Nuevo Libro</b-button>

          </div>

          <br>
            <div class="col-md-12">
                <b-table striped hover :items="datos" :fields="fields">

                    <template slot="action" slot-scope="data">
                        <b-button size="sm" variant="primary" :to="{ name:'EditDatos', params: {datoId: data.item.id}}">
                        Editar
                        </b-button>
                        <b-button size="sm" variant="danger" :to="{ name:'DeletDatos', params: {datoId: data.item.id}}">
                        Eliminar
                        </b-button>

                    </template>

                </b-table>

            </div>

            </div>
        </div>
    </div>




</template>

<script>

import axios from 'axios';


export default{
    data () {
        return {
            fields: [
                { key: 'title', label: 'Titulo'},
                { key:'description', label: 'Descripcion'},
                { key:'action', label: ''}

            ],
            datos: []
        }
    },

    methods: {
        getDatos(){
            const path = 'http://localhost:8000/api/v1.0/datos'
            axios.get(path).then((response) => {
                this.datos = response.data
            } )
            .catch((error) => {
                console.log(error)
            })
        }
    },

    created(){
        this.getDatos()
    }

}
</script>

<style lang="css" scoped>

</style>
