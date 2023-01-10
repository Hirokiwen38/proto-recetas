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
        ></v-text-field>
      </v-col>
      <v-col cols="2">
        <v-text-field
          label="Fecha de Nacimiento"
          persistent-hint
          variant="outlined"
        ></v-text-field>
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
        ></v-text-field>
      </v-col>
    </v-row>
    <div class="main-inputs mt-6 pa-3">
      <v-row class="d-flex justify-center mt-6">
        <v-col cols="2">
          <v-combobox
            label="Medicamento"
            v-model="pack_product.medicamento"
            :items="['Paracetamol', 'Aspirina', 'Naproxen']"
          >
          </v-combobox>
        </v-col>
        <v-col cols="2">
          <v-text-field
            label="Cantidad"
            persistent-hint
            v-model="pack_product.cantidad"
            variant="outlined"
          ></v-text-field>
        </v-col>
        <v-col cols="2">
          <v-combobox
            label="Cantidad cada..."
            v-model="pack_product.rango_tiempo"
            :items="['6 hrs', '8 hrs', '12 hrs', '24 hrs']"
          >
          </v-combobox>
        </v-col>
        <v-col cols="2">
          <v-text-field
            label="Durante"
            persistent-hint
            variant="outlined"
            v-model="pack_product.periodo"
          ></v-text-field>
        </v-col>
        <v-col cols="2">
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
          >Añadir</v-btn
        >
      </v-row>

      <v-table height="100%">
        <thead>
          <tr>
            <th class="text-left">Medicamento</th>
            <th class="text-left">Cantidad</th>
            <th class="text-left">Cantidad cada</th>
            <th class="text-left">Durante</th>
            <th class="text-left">Genérico</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) in array_recipe" :key="index">
            <td>{{ item.medicamento }}</td>
            <td>{{ item.cantidad }}</td>
            <td>{{ item.rango_tiempo }}</td>
            <td>{{ item.periodo }} {{ item.tipo_periodo }}</td>
            <td>
              <v-checkbox
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
        Receta creada exitosamente!
      </v-snackbar>
  </div>
</template>

<script>
export default {
  data() {
    return {
      dialog: false,
      snackbar:false,
      array_recipe: [],
      pack_product: {},
    };
  },
  methods: {
    enviar_receta(){
      if (this.array_recipe.length>0) {
        this.snackbar=true;
        console.log(this.array_recipe);
        // this.array_recipe= [];
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
      this.pack_product = {};
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
