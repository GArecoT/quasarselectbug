<template>
  <div class="q-pa-md">
    <q-select
      label="Select Teste"
      v-model="select"
      :options="options2"
      dense
      options-dense
      option-label="nome"
      use-input
      @filter="
        (val, update) => {
          options2 = filtrar(val, update, options1, 'nome');
        }
      "
    >
    </q-select>
  </div>
</template>

<script setup>
import { onMounted, ref, toRaw } from "vue";

const options1 = ref([{nome: 'cerveja'},{nome:  'pinga'},{nome: 'cachaça'},{nome: 'óleo de borogodó'},{nome: 'cigarrinho do capeta'}])
const options2 = ref(options1.value)

 function filtrar(val, update, store, nome) {
  let lista = structuredClone(toRaw(store));
  if (val === "") {
    update(() => {
      return;
    });

    return lista;
  }
  update(() => {
    const needle = val.toLowerCase();
    lista = Object.values(
      lista.filter(
        (v) => v[nome].toLowerCase().indexOf(needle) > -1,
      ),
    );
  });
  return lista;
}


</script>
