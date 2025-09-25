<template>
    <div class="row">
        <div class="col-8">
            <h1>🎉Bienvenidos al buscador del TP2 de Nuevas Tech 2 🎉</h1>
        </div>
    </div>
    <div class="row">
        <div class="col-4">
            <div v-show="cantCharsNombre" class="alert alert-danger" role="alert">{{textoAlerta}}</div>
            <h4>🔎 Busqueda por Nombre y/o Apellido
                <span class="bi bi-info-circle-fill text-muted ms-0" id="tt-nombre" data-bs-toggle="tooltip" data-bs-placement="right" title="Ingresá parte del nombre o apellido para buscar.">🛈</span>
            </h4>
            <input type="text" class="form-control" v-model.trim="busquedaPorNombre" placeholder="Ingresar nombre a buscar..."></input>
            <div v-show="cantCharsNombre" class="alert alert-danger" role="alert">{{textoAlerta}}</div>
        </div>
        <div class="col-4">
            <h4>🔎 Busqueda por DNI
                <span class="bi bi-info-circle-fill text-muted ms-0" id="tt-nombre" data-bs-toggle="tooltip" data-bs-placement="right" title="Ingresá el DNI sin puntos ni comas.">🛈</span>
            </h4>
            <input type="text" class="form-control" v-model.trim="busquedaPorDni" placeholder="Ingresar DNI a buscar..."></input>
            <div v-show="cantCharDni" class="alert alert-danger" role="alert">{{textoAlerta}}</div>
        </div>
    </div>
    <div class="row row-cols-1 row-cols-md-3" >
        <div id="card-container" class="col-4" v-for="persona in personasFiltradas" :key="persona.dni">
            <div class="card h-100" style="padding-left:0px">
                <div class="card-body">
                    <h5 class="card-title">{{ getNombreCompleto(persona) }}</h5>
                    <p class="card-text">DNI {{ persona.dni }}</p>
                    <a href="#" class="card-link">{{ persona.correo }}</a>
                </div>
            </div>
        </div>
    </div>
</template>


<script>
export default {
    name: 'Estructura',
    data() {
        return {
            busquedaPorNombre: '',
            busquedaPorDni: '',
            textoAlerta:"Ingrese al menos 3 caracteres",
            personas: [
                {
                    nombre: "Lucia",
                    apellido: "Gomez",
                    correo: "lucia.gomez@gmail.com",
                    dni: "33445566"
                },
                {
                    nombre: "Carlos",
                    apellido: "Ramirez",
                    correo: "c.ramirez@hotmail.com",
                    dni: "44556677"
                },
                {
                    nombre: "Mariana",
                    apellido: "Lopez",
                    correo: "mariana.lopez@yahoo.com",
                    dni: "55667788"
                },
                {
                    nombre: "Federico",
                    apellido: "Ramirez",
                    correo: "f.Ramirez@gmail.com",
                    dni: "66778899"
                },
                {
                    nombre: "Valentina",
                    apellido: "Martinez",
                    correo: "valentina.martinez@gmail.com",
                    dni: "77889900"
                },
            ],
        }
    },
    computed: {
        personasFiltradas() {
            const filtroNombre = this.busquedaPorNombre.toLowerCase();
            const filtroDni = this.busquedaPorDni;

            if ((filtroNombre === '' || this.cantCharsNombre) && (filtroDni === '' || this.cantCharDni)) {
                return [];
            }
        return this.personas.filter((persona) => {
            const registroNombre = `${persona.nombre} ${persona.apellido}`.toLowerCase();
            const coincideNombre = filtroNombre === '' || registroNombre.includes(filtroNombre);
            const coincideDni = filtroDni === '' || persona.dni.includes(filtroDni);
            return coincideNombre && coincideDni;
            });
        },
        cantCharsNombre(){
            return this.busquedaPorNombre.length > 0 && this.busquedaPorNombre.length < 3
        },
        cantCharDni(){
            return this.busquedaPorDni.length > 0 && this.busquedaPorDni.length < 3
        }
    },
        methods: {
            getNombreCompleto(persona) {
                return `${persona.nombre} ${persona.apellido}`
            },
        }
    }
</script>

<style scoped>
input, h4, #card-container,.alert{
    margin-left: 15px;
    margin-bottom: 15px;
}

h1 {
    margin-left: 15px;
    margin-bottom: 35px
}
</style>