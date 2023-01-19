<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12">
        <v-img
          :src="require('../assets/logo.png')"
          class="my-3"
          contain
          height="90"
        />
      </v-col>
    </v-row>
    <v-row class="d-flex justify-center align-center ma-0 pt-5 main-inputs">
      <v-col cols="3">
        <v-text-field
          label="Nombre del paciente"
          persistent-hint
          variant="outlined"
          :rules="[rules.nombre,rules.required]"
        ></v-text-field>
      </v-col>
      <v-col cols="2" class="pb-5 pa-0 mr-2" >
        <Datepicker
        class="text-center"
        v-model="picked"
        placeholder="Fecha de nacimiento"
        style="height: 56px; border: lightgray solid; border-radius: 0.3rem; border-width: revert;"
        >
      </Datepicker>


      </v-col>
      <v-col cols="2">
        <v-select label="Sexo" :items="['Femenino', 'Masculino']"></v-select>
      </v-col>
      <v-col cols="2">
        <v-text-field
          label="Empresa"
          persistent-hint
          variant="outlined"
        ></v-text-field>
      </v-col>
      <v-col cols="2">
        <v-text-field
          label="No. Empleado"
          persistent-hint
          variant="outlined"
          :rules="[rules.empleado,rules.required]"
          type="number"
        ></v-text-field>
      </v-col>
    </v-row>
    <div class="main-inputs mt-6 pa-3">
      <v-row class="d-flex justify-center mt-6 pa-3">
        <v-col >
          <v-combobox
            label="Medicamento"
            v-model="pack_product.medicamento"
            :items="['Paracetamol', 'Aspirina', 'Naproxen']"
          >
          </v-combobox>
        </v-col>
        <v-col >
        <v-select v-model="pack_product.selected"
        label="Grupo" 
        :items="['Grupo 1', 'Grupo 2', 'Grupo 3', 'Grupo 4']"
        >
      </v-select>
      </v-col>
        <v-col >
          <v-text-field
            label="Cantidad"
            type="number"
            persistent-hint
            v-model="pack_product.cantidad"
            variant="outlined"
            :rules="[rules.cantidad,rules.required]"
          ></v-text-field>
        </v-col>
        <v-col >
          <v-combobox
            label="Cantidad cada..."
            v-model="pack_product.rango_tiempo"
            :items="['6 hrs', '8 hrs', '12 hrs', '24 hrs']"
          >
          </v-combobox>
        </v-col>
        <v-col >
          <v-text-field
            label="Durante"
            persistent-hint
            variant="outlined"
            v-model="pack_product.periodo"
            :rules="[rules.durante,rules.required]"
            type="number"
          ></v-text-field>
        </v-col>
        <v-col >
          <v-select
            label="tiempo"
            v-model="pack_product.tipo_periodo"
            :items="['Días', 'Semanas']"
          >
          </v-select>
        </v-col>
        <v-btn
          color="#4CABD3"
          size="x-large"
          style="height: 56px"
          class="mt-3 text-white"
          v-on:click="add_product()"
          v-bind:disabled="medication_check"
          >Añadir</v-btn
        >
      </v-row>

      <v-table height="100%">
        <thead>
          <tr>
            <th class="text-left">Medicamento</th>
            <th class="text-left">Grupo</th>
            <th class="text-left">Cantidad</th>
            <th class="text-left">Cantidad cada</th>
            <th class="text-left">Durante</th>
            <th class="text-left">Genérico</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) in array_recipe" :key="index">
            <td>{{ item.medicamento }}</td>
            <td>{{ item.selected }}</td>
            <td>{{ item.cantidad }}</td>
            <td>{{ item.rango_tiempo }}</td>
            <td>{{ item.periodo }} {{ item.tipo_periodo }}</td>
            <td>
              <v-checkbox class="d-flex align-center"
                :value="item.medicamento"
                v-on:click="generic_check(index)"
              ></v-checkbox>
            </td>
          </tr>
        </tbody>
      </v-table>
    </div>
  </v-container>
  <div class="d-flex justify-end mr-16 text-center">
    <v-dialog v-model="dialog" persistent>
      <template v-slot:activator="{ props }">
        <v-row class="d-flex justify-end mr-10">
          <v-btn
            color="#4CABD3"
            size="x-large"
            style="height: 56px"
            class="mt-3 mr-16 text-white"
            v-bind="props"
          >
            Crear Receta
          </v-btn>
        </v-row>
      </template>

      <v-row justify="center">
        <v-card class="h-50 w-25">
          <v-card-text class="text-center">
            ¿Estás seguro que quieres crear la receta?
          </v-card-text>

          <v-card-actions class="justify-center">
            <v-btn color="#49B59F" @click="dialog = false"> Cancelar </v-btn>
            <v-btn color="#4CABD3" @click="enviar_receta()"> Crear Receta </v-btn>
          </v-card-actions>
        </v-card>
      </v-row>
    </v-dialog>
    <v-snackbar
        v-model="snackbar"
        color="success"
        timeout="2000"
      >
      ¡Receta creada exitosamente!
      </v-snackbar>
  </div>
</template>

<script setup>
import Datepicker from 'vue3-datepicker'
import { ref } from 'vue'
const picked = ref(new Date())
</script>

<script>

import '@vuepic/vue-datepicker/dist/main.css'
import 'v-calendar/dist/style.css';


export default {
  components: { Datepicker },
  data() {
    return {
      date: null,
      dialog: false,
      snackbar:false,
      array_recipe: [],
      pack_product: {selected: 'Grupo 1'},
      rules: {
        requerido: value => !!value || 'Requerido',
        cantidad: value => {
          const pattern =/([0-9])*\d+/g
          return pattern.test(value) || 'Inválido'
        },
        nombre: value => {
          const pattern =/^[a-zA-Z ]*$/g
          return pattern.test(value) || 'Inválido'
        },
        empleado: value => {
          const pattern =/([0-9])*\d+/g
          return pattern.test(value) || 'Inválido'
        },
        durante: value => {
          const pattern =/([0-9])*\d+/g
          return pattern.test(value) || 'Inválido'
        },
      }
    };
  },
  computed:{
    medication_check(){
      var flag = null;
      if(Object.keys(this.pack_product).length <6){
        flag= true;
      }else{
        flag= false;
      }
      return flag;
    }
  },
  methods: {
   
    enviar_receta(){
      if (this.array_recipe.length>0) {
        this.snackbar=true;
        console.log(this.array_recipe);
        this.array_recipe= [];
        this.dialog=false;
      }
    },
    generic_check(index) {
      if (this.array_recipe[index].generico == 1) {
        this.array_recipe[index].generico = 0;
      } else {
        this.array_recipe[index].generico = 1;
      }
    },
    add_product() {
      this.array_recipe.push(this.pack_product);
      this.pack_product = {selected: 'Grupo 1'};
    },
  },
};
</script>
<style scoped>
.main-inputs {
  border: solid 1px;
  border-radius: 1rem;
}

</style>