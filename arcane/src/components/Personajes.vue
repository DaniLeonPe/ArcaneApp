<template>
    <div id="app">
        <form @submit="checkForm">
            
            <div>
                <label>Nombre:</label>
                <input type="text" v-model="nombre">
                <br />
                <label>Origen:</label>
                <select id="Origen">
                    <option value="AE">Aguas Estancadas</option>
                    <option value="CDB">Ciudad de bandle</option>
                    <option value="DM">Demacia</option>
                    <option value="EV">El vacio</option>
                    <option value="FJ">Freljord</option>
                    <option value="IDLS">Islas de las sombras</option>
                    <option value="IX">Ixtal</option>
                    <option value="JN">Jonia</option>
                    <option value="NX">Noxus</option>
                    <option value="PT">Piltover</option>
                    <option value="SR">Shurima</option>
                    <option value="TG">Targon</option>
                    <option value="ZN">Zaun</option>
                </select>
                <br />
                <label>Habilidad especial</label>
                <input type="text" v-model="habilidad">
                <br />
                <label>Listado de aliados</label>
                <input type="text" v-model="aliados">
                <br />
                <label>Mision Principal</label>
                <input type="checkbox" id="mision" name="mision" value="yes">
                <div>
                    <button @click.prevent="accept">Enviar</button>
                 </div>
            </div>
        </form>
    </div>
</template>


<script>
import {ref} from 'vue';

export default {
    setup(){
        const nombre = ref('');
        const habilidad = ref('');
        const aliados = ref(['']);
        const mision = ref(false);

        const checkForm = () => {
            console.log(nombre.value);
            console.log(habilidad.value);
            console.log(aliados.value);
            console.log(mision.value);
        }

        return {
            nombre,
            habilidad,
            aliados,
            mision,
            checkForm
        }
    }
}


</script>

<style>

</style>