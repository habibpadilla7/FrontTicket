<template>
    <div>
        <div class="row mr-0">
            <div class="col-xl-2 col-sm-12 col-md-0 pr-0 border-right shadow pl-0">       
                    <div  class="row pt-2 m-0" style="width:100%">
                        <button v-on-click="getTodos">Registro de Comprador</button>
                        <button v-on-click="link('disponibilidad')">Boletas disponible</button>
                    </div>
                
            </div>
            <div class="col-xl-10 col-sm-12 col-md-10 pt-3">
                <div class="row mt-3 mb-4" v-show="accion === 'disponibilidad'">
                    <table>
                    <tbody>
                        <tr v-for="todo in todos" :key="todo.id">
                            <td>{{todo.id}}</td>
                            <td>{{todo.names}}</td>
                        </tr>
                    </tbody>
                    </table>
                </div>
                <div class="row mt-3 mb-4" v-show="accion === 'reservar'">
                    <div class="col-xl-10 col-sm-12 col-md-10 p-2 pb-2 offset-1 border rounded">       
                        <form @submit.prevent="update">
                            <div class="row mt-3 offset-1 text-left">
                                <div class="col-md-12 mb-4 text-left text-primary"><h4><span class="nav-bar-icon mr-2 mdi mdi-36px mdi-book-open-outline"></span>{{$t('Reservar Salones')}}</h4></div>
                            </div>
                            <div class="form-group row mb-4 ml-0 mr-0">
                                <label class="col-md-2 col-form-label text-left pt-3 " for="residente">
                                    <span class="nav-bar-icon mr-2 mdi mdi-calendar"></span>{{$t('Residente')}}:</label>
                                <div class="col-md-10 p-0">
                                    <select v-model="Reservafm.residente" class="form-control">
                                        <option :value="residen.id" :key="residen.id" v-for="residen in resid">{{ residen.name }}</option>                                
                                    </select>
                                </div> 
                            </div>
                            
                            <div class="form-group row mb-4 ml-0 mr-0 mt-4">  
                               <div class="col-md-4 p-0"></div>
                                <div class="col-md-5 p-0 mt-2">
                                    <button class="btn btn-success"  @click="insert">
                                        <span >Guardar reserva del salon</span>
                                    </button>
                                </div>
                                <div class="col-md-3 p-0"></div>
                            </div>
                            
                        </form>
                    </div>
                    <div class="col-xl-11 col-sm-11 col-md-11 pr-0 ml-5">       
                        <div class="pl-3 pt-3 ml-1">                
                            <pagination :isPagination="isPagination" :actions="actions" :searchable="searchable" :uri="uri6" :columns="columns6">                          
                            </pagination>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
        
</template>


<script>
import axios from 'axios'

export default {
    data(){
        return {
            todos:null
        }
    },
    mounted(){
            console.log('Hola mundo desde mounted')
            this.getTodos();
    },
    methods: {
        getTodos(){
            console.log('aca va el codigo get todos')
            axios
            .get('http://127.0.0.1:8000/api/tickets')
            .then(response=>{
                this.todos=response.data
                console.log(response)
            })
            .catch( e=> console.log(e))
        },
        link(accion = "general"){
            console.log("Prueba")
            this.accion = accion
        },
    }
    
}
</script>
<style scoped >
    .height-conf{
        min-height: 450px;
    }
    
    input[type="number"]{
        margin-top:10px
    }
</style>
