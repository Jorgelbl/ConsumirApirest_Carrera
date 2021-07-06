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
                        <button type="button" class="btn btn-primary" v-on:click="guardar()" >Guardar</button>
                        <button type="button" class="btn btn-dark margen" v-on:click="salir()"  >Salir</button>
                        </div>          
                     </form>
            </div>
        <Footer /> 
    </div>
</template>

<script>
import Header from '@/components/Header.vue'
import Footer from '@/components/Footer.vue'
import axios from 'axios';
export default {
    name:"Nuevo",
    data:function(){
        return{
            form:{
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
    components:{
        Header,
        Footer
    },
    methods:{
        guardar(){
            this.form.token = localStorage.getItem("token");
            axios.post("http://apirest-carrera.com/carrera",this.form)
            .then(data =>{
                console.log(data);
                this.makeToast("Hecho","Carrera creada","success");
                this.$router.push("/dashboard");
            }).catch( e =>{
                console.log(e);
                 this.makeToast("Error","Error al guardar","error");
            })
            
        },
        salir(){
            this.$router.push("/dashboard");
        },
        makeToast(titulo,texto,tipo) {
            this.toastCount++
            this.$bvToast.toast(texto, {
            title: titulo,
            variant: tipo,
            autoHideDelay: 5000,
            appendToast: true
            })
        }
    }
}
</script>

<style scoped>
.left{
    text-align:  left;
}
</style>