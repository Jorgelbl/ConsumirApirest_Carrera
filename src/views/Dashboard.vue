<template>
     <div>
          <Header />
          <div class="container izquierda">

                <button class="btn btn-primary" v-on:click="nuevo()" >Nueva Carrera</button>
                <br><br>

              <table class="table table-hover">
                <thead>
                    <tr>
                        <th scope="col">ID</th>
                        <th scope="col">Carrera</th>
                        <th scope="col">Reticula</th>
                        <th scope="col">Nivel Escolar</th>
                        <th scope="col">Clave Oficial</th>
                        <th scope="col">Nombre Carrera</th>
                        <th scope="col">Nombre Reducido</th>
                        <th scope="col">Carga Maxima</th>
                        <th scope="col">Creditos Totales</th>
                        <th scope="col">Nivel</th>
                        <th scope="col">Modalidad</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="carrera in Listacarreras" :key="carrera.ID_CARRERA" v-on:click="editar(carrera.ID_CARRERA)">
                        <th scope="row">{{ carrera.ID_CARRERA}}</th>
                        <td>{{ carrera.CARRERA }}</td>
                        <td>{{ carrera.RETICULA }}</td>
                        <td>{{ carrera.NIVEL_ESCOLAR }}</td>
                        <td>{{ carrera.CLAVE_OFICIAL }}</td>
                        <td>{{ carrera.NOMBRE_CARRERA }}</td>
                        <td>{{ carrera.NOMBRE_REDUCIDO }}</td>
                        <td>{{ carrera.CARGA_MAXIMA }}</td>
                        <td>{{ carrera.CREDITOS_TOTALES }}</td>
                        <td>{{ carrera.NIVEL }}</td>
                        <td>{{ carrera.MODALIDAD }}</td>
                    </tr>
                </tbody>
                </table>
          </div>       

         <Footer />
     </div>
</template>

<script>
import Header from '@/components/Header.vue';
import Footer from '@/components/Footer.vue';
import axios from 'axios';

export default {
    name:"Dashboard",
    data(){
        return{
            Listacarreras:null,
            pagina:1
        }

    },
    components:{
        Header,
        Footer
    },
    methods:{
        editar(id){
            this.$router.push('/editar/' + id);
        },
        nuevo(){
            this.$router.push('/nuevo');
            }

    },
    mounted:function(){
        let direccion = "http://apirest-carrera.com/?page=" + this.pagina;
        axios.get(direccion).then( data =>{
            this.Listacarreras = data.data;
        });
    }
    
}
</script>

<style  scoped>
    .izquierda{
        text-align: left;
    }
</style>