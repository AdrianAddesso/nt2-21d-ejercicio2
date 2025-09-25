<template>
    <div class="row">
        <div class="col-8">
            <h1>🎉Bienvenidos al buscador del TP2 de Nuevas Tech 2 🎉</h1>
        </div>
    </div>
    <div class="row">
        <div class=" col-4">
            <h4>🔎 Busqueda por Nombre y/o Apellido
                <span class="bi bi-info-circle-fill text-muted ms-0" id="tt-nombre" data-bs-toggle="tooltip" data-bs-placement="right" title="Ingresá parte del nombre o apellido para buscar.">🛈</span>
            </h4>
            <input type="text" class="form-control" v-model.trim="busquedaPorNombre" placeholder="Ingresar nombre a buscar..."></input>
        </div>
        <div class="col-4">
            <h4>🔎 Busqueda por DNI
                <span class="bi bi-info-circle-fill text-muted ms-0" id="tt-nombre" data-bs-toggle="tooltip" data-bs-placement="right" title="Ingresá el DNI sin puntos ni comas.">🛈</span>
            </h4>
            <input type="text" class="form-control" v-model.trim="busquedaPorDni" placeholder="Ingresar DNI a buscar..."></input>
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
    <!--<div>
        <img style ="margin-top: 100px" :src="imagenDogo()" width="150px"></img>
    </div>-->
</template>


<script>
export default {
    name: 'Estructura',
    data() {
        return {
            busquedaPorNombre: '',
            busquedaPorDni: '',
            //Aquí, en este array es donde tienen que agregar su información
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
                    apellido: "Diaz",
                    correo: "f.diaz@gmail.com",
                    dni: "66778899"
                },
                {
                    nombre: "Valentina",
                    apellido: "Martinez",
                    correo: "valentina.martinez@gmail.com",
                    dni: "77889900"
                },
            ],
            dogoFeliz: "https://i.pinimg.com/736x/04/7b/54/047b5491771ba7d54b33179e04164b22.jpg",
            dogoTriste: "https://content.imageresizer.com/images/memes/cheems-meme-3nzkub.png",
        }
    },
    computed: {
        personasFiltradas() {
            const filtroNombre = this.busquedaPorNombre.toLowerCase();
            const filtroDni = this.busquedaPorDni;

            if (filtroNombre === '' && filtroDni === '') {
                return [];
            }
        return this.personas.filter((persona) => {
            const registroNombre = `${persona.nombre} ${persona.apellido}`.toLowerCase();
            const coincideNombre = filtroNombre === '' || registroNombre.includes(filtroNombre);
            const coincideDni = filtroDni === '' || persona.dni.includes(filtroDni);
            return coincideNombre && coincideDni;
            });
        }
    },
        methods: {
            getNombreCompleto(persona) {
                return `${persona.nombre} ${persona.apellido}`
            },
            /*imagenDogo(){
                return this.criterioDeBusqueda.trim() !== '' ? this.dogoFeliz: this.dogoTriste;
            }*/
        }
    }
</script>

<style scoped>
input, h4, #card-container {
    margin-left: 15px;
    margin-bottom: 15px;
}

h1 {
    margin-left: 15px;
    margin-bottom: 35px
}
</style>