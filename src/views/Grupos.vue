<template>
    <div id="Titulo">
        <h4> Grupos</h4>
        <h6>Aquí se podrá consultar,crear, editar y eliminar grupos </h6>
        <button @click="VentanaCrearGrupo = true" class="CustomBTN">
            Crear Grupo
        </button>
                <button @click="VentanaCrearGrupo = true" class="CustomBTN">
            Consultar Grupo
        </button>
        <button @click="VentanaCrearGrupo = true" class="CustomBTN">
            Eliminar Grupo
        </button>
                <button @click="VentanaCrearGrupo = true" class="CustomBTN">
            Consultar Grupo
        </button>
        <Transition name="fade">
            <div class="modal-overlay" v-if="VentanaCrearGrupo">
                <div>
                    <button @click="VentanaCrearGrupo = false" class="CerrarBTN">
                        Cerrar
                    </button>
                </div>

            </div>
        </Transition>
        <div>
            <form class="formEnOverlay" action="" v-if="VentanaCrearGrupo" v-on:submit.prevent="CrearGrupo">
                <h4 class="h4Tittle">Crear Grupo</h4>
                <input type="text" name="estudiante" placeholder="cédula estudiante" class="form-control" v-model="estudianteid" required/>
                <input type="text" name="docente" placeholder="cédula docente" class="form-control"  v-model="docenteid" required/>
                <input type="text" name="curso" placeholder="código del curso" class="form-control"  v-model="cursoid" required />
                <input type="text" name="aula" placeholder="código del aula" class="form-control"  v-model="aula" />
                <input type="text" name="horario" placeholder="horario del grupo" class="form-control"   v-model="horario" />
                <input type="submit" class="CrearBTN" value="Crear">
            </form>
        </div>



    </div>
</template>


<script>
import Axios from 'axios';
export default {
    name: 'Grupos',
    components: {
    },
    data: function () {
        return {
        VentanaCrearGrupo: false,
        estudianteid : "",
        docenteid:"",
        cursoid:"",
        aula:"",
        horario:""
        }
    },
    methods: {
    CrearGrupo() {
      let json = {
        estudianteid : this.estudianteid,
        docenteid:this.docenteid,
        cursoid:this.cursoid,
        aula:this.aula,
        horario:this.horario
      };
console.log("Enviando Datos al servidor")
Axios.post('http://localhost:3000/crear/grupo',json)
.then (data =>{
  console.log(data)
  alert("Se ha creado el grupo");
})
}
    }
}
</script>



<style scoped>
.CustomBTN {
    display: inline-block;
    padding: 15px 25px;
    font-size: 22px;
    cursor: pointer;
    text-align: center;
    text-decoration: none;
    outline: none;
    color: #fff;
    background-color: #4CAF50;
    border: none;
    border-radius: 10px;
    box-shadow: 0 9px #999;
}

.CustomBTN:hover {
    background-color: #3e8e41
}

.CustomBTN:active {
    background-color: #3e8e41;
    box-shadow: 0 5px #666;
    transform: translateY(4px);
}

div.fixed {
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
    width: 100px;
    height: 100px;
    border: 3px solid #73AD21;
    margin: auto;
    display: flex;
}

.modal-overlay {
    position: absolute;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
    z-index: 100;
    background: rgba(0, 0, 0, 0.4)
}

.modal {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    left: 0;
    transform: translate(-50%, -50%);
    background: white;
    padding: 20px;
    border-radius: 15px;
    z-index: 101;
}

.CerrarBTN {
    display: inline-block;
    padding: 15px 25px;
    font-size: 22px;
    cursor: pointer;
    text-align: center;
    text-decoration: none;
    outline: none;
    color: #fff;
    background-color: #4c5eaf;
    border: none;
    border-radius: 10px;
    box-shadow: 0 9px #999;
    position: absolute;
    bottom: 25%;
    right: 31%;
}

.CrearBTN {
    display: inline-block;
    padding: 15px 25px;
    font-size: 22px;
    cursor: pointer;
    text-align: center;
    text-decoration: none;
    outline: none;
    color: #fff;
    background-color: purple;
    border: none;
    border-radius: 10px;
    box-shadow: 0 9px #999;
    position:relative;
    top:16%;
    left:20%;
}

.formEnOverlay {
    position: absolute;
    width: 50vw;
    height: 50vh;
    z-index: 150;
    padding: 80px 100px;
    box-sizing: border-box;
    transition: top 500ms ease-in-out,
        opacity 500ms ease-in-out,
        height 0ms ease-in-out 500ms;
    border-radius: 15px;
    top: 20%;
    left: 25%;
}

.h4Tittle {
    text-align: center;
    padding: 5px;
    background-color: lightcyan
}
</style>