<template>
    <div class="container mt-5">
        <div class="row">
            <div class="col-lg-8 offset-lg-2">
                <input class="form-control form-control-lg" placeholder="Ingresar Tarea..." v-model="nombreTarea"
                    v-on:keyup.enter="agregarTarea()" />
                <br>
            </div>
            <div class="col-lg-6 offset-lg-3">
                <div class="card p-2" v-if="tareas.length === 0">
                    <h6>No hay tareas</h6>
                </div>
                <ul class="list-group" v-for="(tarea, index) in tareas" v-bind:key="index">
                    <li class="list-group-item d-flex justify-content-between">
                        <span class="cursor" v-on:click="actualizarTarea(tarea, index)">
                            <i v-bind:class="[tarea.estado === true ? '' : '']"/>
                        </span>
                        <h5>
                            {{ tarea.nombre }}
                        </h5>
                        <span class="cursor text-danger" v-on:click="eliminarTarea(index)">
                            <font-awesome-icon icon="fa-solid fa-trash" />
                        </span>
                    </li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>


export default {
    data() {
        return {
            tareas: [],
            nombreTarea: ''
        }
    },
    methods: {
        agregarTarea() {
            const tarea = {
                nombre: this.nombreTarea,
                estado: false //Inicializamos la tarea como falso
            }
            this.tareas.push(tarea);
            this.nombreTarea = '';
        },
        eliminarTarea(index) {
            this.tareas.splice(index, 1); //FUNCION PARA ELIMINAR TAREAS
        },
        actualizarTarea(tarea, index) {
            this.tareas[index].estado = !tarea.estado;
        }
    },
}
</script>

<style scoped>
input {
    text-align: center;
}

.form-control-lg {
    font-size: 1.7rem;
}

.cursor {
    cursor: pointer;
}
</style>