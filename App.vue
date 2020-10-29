<template>
    <div>
        <div class="row mr-0">
            <div class="col-xl-2 col-sm-12 col-md-0 pr-0 border-right shadow pl-0">       
                    <div  class="row pt-2 m-0" style="width:100%;text-align: center">
                        <button @click="link('registro')">Registro de Comprador</button>
                        <button @click="link('disponibilidad')">Boletas disponible</button>
                        <button @click="link('reservar')">Reservar boleta</button>
                    </div>
                
            </div>
            <div class="col-xl-10 col-sm-12 col-md-10 pt-3" style="text-align: center">
                <div class="row mt-3 mb-4" v-show="accion === 'disponibilidad'">
                    <table  align="center">
                    <tbody>
                        <tr>Boletas Disponible</tr>
                        <tr v-for="allTicket in allTickets" :key="allTicket.id">
                            <td>{{allTicket.names}}</td>
                        </tr>
                    </tbody>
                    </table>
                </div>
                <div class="row mt-3 mb-4" v-show="accion === 'registro'">
                    <div class="col-xl-10 col-sm-12 col-md-10 p-2 pb-2 offset-1 border rounded">       
                        <form>
                            <div class="form-group row mb-3 ml-0 mr-0">
                                <br>
                                <table align="center">
                                <tr>
                                    <td>
                                        <label class="col-md-2 col-form-label text-left" for="namesfor">
                                            {{'REGISTRO DE COMPRADOR'}} :
                                        </label>
                                    </td>
                                </tr>
                                </table>
                                <br>                                  
                            </div>
                                
                            <div class="form-group row mb-3 ml-0 mr-0">
                                <br>
                                <table align="center">
                                <tr>
                                    <td>
                                        <label class="col-md-2 col-form-label text-left" for="namesfor">
                                            {{'Nombres'}} :
                                        </label>
                                    </td>
                                    <td>
                                        <div class="col-md-10 p-0">
                                            <input type="text" class="form-control" id="names" placeholder="Ingresar Nombres" v-model="buyer.names" required>
                                        </div>
                                    </td>
                                </tr>
                                </table>                                 
                            </div>
                            <div class="form-group row mb-3 ml-0 mr-0">
                                <table align="center">
                                <tr>
                                    <td>
                                        <label class="col-md-2 col-form-label text-left" for="surnamesfor">
                                            {{'Apellidos'}} :</label>
                                    </td>
                                    <td>
                                        <div class="col-md-10 p-0">
                                            <input type="text" class="form-control" id="names" placeholder="Ingresar Apellidos" v-model="buyer.surnames" required>
                                        </div>  
                                    </td>
                                </tr>
                                </table> 
                                    
                            </div>
                            <div class="form-group row mb-3 ml-0 mr-0">
                                <table align="center">
                                <tr>
                                    <td>
                                        <label class="col-md-2 col-form-label text-left " for="descripcion">
                                            {{'Identificacion'}}:</label>
                                    </td>
                                    <td>
                                        <div class="col-md-10 p-0">
                                            <input type="number" class="form-control" id="identification" placeholder="Ingresar Identificacion" v-model="buyer.identification" required>
                                        </div> 
                                    </td>
                                </tr>
                                </table> 
                            </div>
                            <div class="form-group row mb-3 ml-0 mr-0">
                                <table align="center">
                                <tr>
                                    <td>
                                        <label class="col-md-2 col-form-label text-left" for="emailfor">
                                            {{'Correo'}} :</label>
                                    </td>
                                    <td>
                                        <div class="col-md-10 p-0">
                                            <input type="text" class="form-control" id="email" placeholder="Ingresar Correo" v-model="buyer.email" required>
                                        </div>
                                    </td>
                                </tr>
                                </table>   
                            </div>
                            <div class="col-md-5 p-0 mt-2">
                                <br>
                                    <button class="btn btn-success"  @click="insertBuyers">
                                        <span >Guardar comprador</span>
                                    </button>
                            </div>
                            
                        </form>
                    </div>
                </div>
                <div class="row mt-3 mb-4" v-show="accion === 'reservar'">
                    <div class="col-xl-10 col-sm-12 col-md-10 p-2 pb-2 offset-1 border rounded">       
                        <form>
                            <div class="form-group row mb-3 ml-0 mr-0">
                                <br>
                                <table align="center">
                                <tr>
                                    <td>
                                        <label class="col-md-2 col-form-label text-left" for="namesfor">
                                            {{'RESERVA DE BOLETAS'}} :
                                        </label>
                                    </td>
                                </tr>
                                </table>
                                <br>                                  
                            </div>
                            <table align="center">
                                <tr>
                                    <td>
                                        <label class="col-md-2 col-form-label text-left pt-3 " for="buysfor">
                                                {{'Comprador'}}:</label>
                                    </td>
                                    <td>
                                        <div class="col-md-10 p-0">
                                                <select v-model="Reservafm.buyer" class="form-control">
                                                    <option :value="allBuyer.id" :key="allBuyer.id" v-for="allBuyer in allBuyers">{{ allBuyer.names }}</option>                                
                                                </select>
                                        </div>
                                    </td>
                                </tr>
                                <tr>
                                    <td>
                                        <label class="col-md-2 col-form-label text-left pt-3 " for="ticketfor">
                                                {{'Boletas Disponibles'}}:</label>
                                    </td>
                                    <td>
                                        <div class="col-md-10 p-0">
                                                <select v-model="Reservafm.ticket" class="form-control">
                                                    <option :value="allTicket.id" :key="allTicket.id" v-for="allTicket in allTickets">{{ allTicket.names }}</option>                                
                                                </select>
                                        </div>
                                    </td>
                                </tr>
                            </table>


                            <div class="col-md-5 p-0 mt-2">
                                <br>
                                    <button class="btn btn-success"  @click="insertReservation">
                                        <span >Guardar reserva</span>
                                    </button>
                            </div>
                        </form>
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
            todos:null,
            accion:"disponibilidad",
            Reservafm:{
                buyer:null,
                ticket:null
            },
            buyer:{
                names:null,
                surnames:null,
                identification:null,
                email:null
            }
        }
    },
    mounted(){
            this.getAllTicketsAvailable();
            this.getAllBuyers();
    },
    created() {
        this.getAllTicketsAvailable()
    },
    methods: {
        getAllTicketsAvailable(){
            console.log('aca va el codigo get todos')
            axios
            .get('http://127.0.0.1:8000/api/tickets')
            .then(response=>{
                this.allTickets=response.data
                console.log(response)
            })
            .catch( e=> console.log(e))
        },
        getAllBuyers(){
            axios
            .get('http://127.0.0.1:8000/api/buyers')
            .then(response=>{
                this.allBuyers=response.data
                console.log(response)
            })
            .catch( e=> console.log(e))
        },
        insertBuyers(){
            let insertTableB = {
                names:this.buyer.names,
                surnames:this.buyer.surnames,
                identification:this.buyer.identification,
                email:this.buyer.email
            }
            console.log(insertTableB)
            axios
            .post('http://127.0.0.1:8000/api/buyers',insertTableB)
            .then(response=>{
                console.log("pruebas1"+response)
            })
            .catch( e=> console.log("pruebas2"+e))
        },
        insertReservation(){
            let insertTableR = {
                id_buyer:this.Reservafm.buyer,
                id_ticket:this.Reservafm.ticket
            }
            axios
            .post('http://127.0.0.1:8000/api/ticket_assignments',insertTableR)
            .then(response=>{
                console.log(response)
            })
            .catch( e=> console.log(e))
        },
        link(accion = "reserva"){
            console.log("Pruebass "+accion)
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
