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
      <v-row class="mt-10 main-inputs" >
         <v-col cols="3">
            <v-text-field label="Nombre del paciente" persistent-hint variant="outlined"></v-text-field>
          </v-col>
          <v-col cols="2">
            <v-text-field label="Fecha de Nacimiento" persistent-hint variant="outlined"></v-text-field>
          </v-col>
          <v-col cols="2">
          <v-select  
          label="Sexo"
          :items="['Femenino', 'Masculino']"></v-select>
        </v-col>
          <v-col cols="2">
            <v-text-field label="Empresa" persistent-hint variant="outlined"></v-text-field>
          </v-col>
          <v-col cols="2">
            <v-text-field label="No. Empleado" persistent-hint variant="outlined"></v-text-field>
          </v-col>
        </v-row>
        <div class="main-inputs mt-6 pa-3">
          <v-row class="mt-10">
            <v-col cols="2">
          <v-autocomplete
          label="Medicamento"
          :items="['Paracetamol', 'Aspirina', 'Naproxen']"></v-autocomplete>
        </v-col>
          <v-col cols="2">
            <v-text-field label="Cantidad" persistent-hint variant="outlined"></v-text-field>
          </v-col>
          <v-col cols="2">
          <v-autocomplete
          label="Cantidad cada..."
          :items="['6 hrs', '8 hrs', '12 hrs', '24 hrs']"></v-autocomplete>
        </v-col>
          <v-col cols="2">
            <v-text-field label="Durante" persistent-hint variant="outlined"></v-text-field>
          </v-col>
          <v-col cols="2">
          <v-select  
          label="tiempo"
          :items="['Días', 'Semanas']">
        </v-select>
      </v-col>
          <v-btn color="#4CABD3" class="mt-2">Añadir</v-btn>
        </v-row> 
        
   
    <v-table height="300px" >
      <thead>
        <tr>
          <th class="text-left">
            Medicamento
          </th>
          <th class="text-left">
            Cantidad
          </th>
          <th class="text-left">
            Cantidad cada
          </th>
          <th class="text-left">
            Durante
          </th>
          <th class="text-left">
            Genérico
          </th>
        </tr>
      </thead>
      <tbody>
        
      </tbody>
    </v-table>
  </div>

    <v-btn color="#4CABD3" class="mt-2">Crear Receta</v-btn>
  </v-container>
</template>

<script>
</script>
<style scoped>
.main-inputs{
  border: solid 1px;
  border-radius: 1rem;
}

</style>
