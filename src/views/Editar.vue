<template>
        <div>
            <Header />
                <div class="container">
                     <form action="" class="form-horizontal">
                        <div class="form-group left row">
                            <div class="col">
                                <label for="" class="control-label col-sm-3">Carrera</label>
                                <div class="col-sm-7">
                                    <input type="text" class="form-control" name="CARRERA" id="NIVEL" v-model="form.CARRERA">
                               </div>
                            </div>

                        <div class="col">
                            <label for="" class="control-label col-sm-5">Reticula</label>
                            <div class="col-sm-7">
                                <input type="text" class="form-control" name="RETICULA" id="RETICULA" v-model="form.RETICULA">
                            </div>
                        </div>
                        </div>

                        <div class="form-group left row">
                            <div class="col">
                                <label for="" class="control-label col-sm-3">Nivel Escolar</label>
                                <div class="col-sm-7">
                                    <input type="text" class="form-control" name="NIVEL_ESCOLAR" id="NIVEL_ESCOLAR" v-model="form.NIVEL_ESCOLAR">
                               </div>
                            </div>
                        <div class="col">
                            <label for="" class="control-label col-sm-5">Clave Oficial</label>
                            <div class="col-sm-7">
                                <input type="text" class="form-control" name="CLAVE_OFICIAL" id="CLAVE_OFICIAL" v-model="form.CLAVE_OFICIAL">
                            </div>
                        </div>
                        </div>

                        <div class="form-group left row">
                            <div class="col">
                                <label for="" class="control-label col-sm-3">Nomb Carrera</label>
                                <div class="col-sm-7">
                                    <input type="text" class="form-control" name="NOMBRE_CARRERA" id="NOMBRE_CARRERA" v-model="form.NOMBRE_CARRERA">
                               </div>
                            </div>
                        <div class="col">
                            <label for="" class="control-label col-sm-5">Nombre Reducido</label>
                            <div class="col-sm-7">
                                <input type="text" class="form-control" name="NOMBRE_REDUCIDO" id="NOMBRE_REDUCIDO" v-model="form.NOMBRE_REDUCIDO">
                            </div>
                        </div>
                        </div>
                         

                        <div class="form-group left row">
                            <div class="col">
                                <label for="" class="control-label col-sm-3">Carga Maxima</label>
                                <div class="col-sm-7">
                                    <input type="text" class="form-control" name="CARGA_MAXIMA" id="CARGA_MAXIMA" v-model="form.CARGA_MAXIMA">
                               </div>
                            </div>
                        <div class="col">
                            <label for="" class="control-label col-sm-5">Creditos Totales</label>
                            <div class="col-sm-7">
                                <input type="text" class="form-control" name="CREDITOS_TOTALES" id="CREDITOS_TOTALES" v-model="form.CREDITOS_TOTALES">
                            </div>
                        </div>
                        </div>

                        <div class="form-group left row">
                            <div class="col">
                                <label for="" class="control-label col-sm-3">Nivel</label>
                                <div class="col-sm-7">
                                    <input type="text" class="form-control" name="NIVEL" id="NIVEL" v-model="form.NIVEL">
                               </div>
                            </div>
                        <div class="col">
                            <label for="" class="control-label col-sm-5">Modalidad</label>
                            <div class="col-sm-7">
                                <input type="text" class="form-control" name="MODALIDAD" id="MODALIDAD" v-model="form.MODALIDAD">
                            </div>
                        </div>
                        </div>

                        <div class="form-group">
                        <button type="button" class="btn btn-primary" v-on:click="editar()" >Editar</button>
                        <button type="button" class="btn btn-danger margen" v-on:click="eliminar()" >Eliminar</button>
                        <button type="button" class="btn btn-dark margen" v-on:click="salir()"  >Salir</button>
                        </div>

                                
                    
                     </form>
                </div>
            <Footer />
        </div>
    
</template>

<script>
import Header from '@/components/Header.vue';
import Footer from '@/components/Footer.vue';
import axios from 'axios';

export default {
    name:"Editar",
    components:{
        Header,
        Footer
    },
    data:function(){
        return{
            form:{
                "ID_CARRERA":"",
                "CARRERA":"",
                "RETICULA":"",
                "NIVEL_ESCOLAR":"",
                "CLAVE_OFICIAL":"",
                "NOMBRE_CARRERA":"",
                "NOMBRE_REDUCIDO":"",
                "CARGA_MAXIMA":"",
                "CREDITOS_TOTALES":"",
                "NIVEL":"",
                "MODALIDAD":"",
                "token" : ""          
            }

        }
    },
    methods:{
      editar(){
          axios.put("http://apirest-carrera.com/carrera",this.form)
          .then( data =>{
              console.log(data);
          })
      
    },
    salir(){
        this.$router.push("/dashboard");
        
    },
    eliminar(){
        var enviar = {
            "ID_CARRERA" : this.form.ID_CARRERA,
            "token" : this.form.token
        };
        axios.delete("http://apirest-carrera.com/carrera", { headers : enviar})
        .then( datos => {
            console.log(datos);
           this.$router.push("/dashboard");
           });
        
        }
    
    },

    mounted:function(){
        this.form.ID_CARRERA = this.$route.params.id;
        axios.get("http://apirest-carrera.com/?page=" + this.form.ID_CARRERA)
        .then(datos => {
            this.form.CARRERA = datos.data.CARRERA;
            this.form.RETICULA = datos.data.RETICULA;
            this.form.NIVEL_ESCOLAR = datos.data.NIVEL_ESCOLAR;
            this.form.CLAVE_OFICIAL = datos.data.CLAVE_OFICIAL;
            this.form.NOMBRE_CARRERA = datos.data.NOMBRE_CARRERA;
            this.form.NOMBRE_REDUCIDO = datos.data.NOMBRE_REDUCIDO;
            this.form.CARGA_MAXIMA = datos.data.CARGA_MAXIMA;
            this.form.CREDITOS_TOTALES = datos.data.CREDITOS_TOTALES;
            this.form.NIVEL = datos.data.NIVEL;
            this.form.MODALIDAD = datos.data.MODALIDAD;
            this.form.token = localStorage.getItem("token");
            console.log(this.form)
        })    

    }
}
        
</script>

<style scoped>
 .left{
   text-align: left;
 };
 .margen{
   margin-left: 15px;
   margin-right: 15px;;
 }
</style>
