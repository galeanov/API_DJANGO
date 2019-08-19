<template lang="html">
  <div class="container">
    <div class="row">
      <div class="col">
        <h3>¿Estas seguro que deseas elininar este libro?</h3>
        <p>Titulo : {{ this.element.title}}</p>
        <p>Descripcion : {{ this.element.description}}</p>
      </div>
    </div>

    <div class="row">
      <div class="col">

        <b-button v-on:click="deleteDatos" variant="danger">Eliminar

        </b-button>

      </div>

    </div>
  </div>
</template>

<script>

    import axios from 'axios'
    import swal from 'sweetalert'

export default{
    data () {
        return {
            datoId: this.$route.params.datoId,
            element: {
                title: '',
                description: ''
            }
        }
    },

    methods:{
        getDatos(){
            const path = `http://localhost:8000/api/v1.0/datos/${this.datoId}/`

            axios.get(path).then((response)=>{
                this.element.title = response.data.title
                this.element.description = response.data.description
            })
                .catch((error)=>{
                    console.log(error)
                })
        },

        deleteDatos(){
            const path = `http://localhost:8000/api/v1.0/datos/${this.datoId}/`

            axios.delete(path).then((response)=> {
                location.href = '/datos'
            })
                .catch((error)=>{
                    swal("No es posible eliminar el libro", "", "error")

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
