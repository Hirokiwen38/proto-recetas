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
      <v-row class="mt-10">
         <v-col cols="6" sm="3">
            <v-text-field label="Nombre del paciente" persistent-hint variant="outlined"></v-text-field>
          </v-col>
          <v-col cols="6" sm="3">
            <v-text-field label="Fecha de Nacimiento" persistent-hint variant="outlined"></v-text-field>
          </v-col>
          <v-select cols="3" sm="3"
          label="Sexo"
          :items="['Femenino', 'Masculino']"></v-select>
          <v-col cols="3" sm="2">
            <v-text-field label="Empresa" persistent-hint variant="outlined"></v-text-field>
          </v-col>
          <v-col cols="3" sm="3">
            <v-text-field label="No. Empleado" persistent-hint variant="outlined"></v-text-field>
          </v-col>
          <v-select cols="3" sm="3"
          label="Medicamento"
          :items="['Paracetamol', 'Aspirina', 'Naproxen']"></v-select>
          <v-col cols="3" sm="2">
            <v-text-field label="Cantidad" persistent-hint variant="outlined"></v-text-field>
          </v-col>
          <v-select cols="3" sm="3"
          label="Cantidad cada..."
          :items="['6 hrs', '8 hrs', '12 hrs', '24 hrs']"></v-select>
          <v-col cols="3" sm="2">
            <v-text-field label="Durante" persistent-hint variant="outlined"></v-text-field>
          </v-col>
          <v-btn color="#11B1BE" class="mt-2">Añadir</v-btn>
        </v-row> 
        
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
    <v-btn color="#11B1BE" class="mt-2">Crear Receta</v-btn>
  </v-container>
</template>

<script>
</script>
