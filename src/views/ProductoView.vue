<script setup lang="ts">
import ProductoList from '@/components/producto/ProductoList.vue'
import ProductoSave from '@/components/producto/ProductoSave.vue'
import { Button } from 'primevue'
import { ref } from 'vue'

const mostrarDialog = ref(false)
const productoListRef = ref<typeof ProductoList | null>(null)
const productoEdit = ref<any>(null)

function handleCreate() {
  productoEdit.value = null
  mostrarDialog.value = true
}

function handleEdit(producto: any) {
  productoEdit.value = producto
  mostrarDialog.value = true
}

function handleCloseDialog() {
  mostrarDialog.value = false
}

function handleGuardar() {
  productoListRef.value?.obtenerLista()
  mostrarDialog.value = false
}
</script>

<template>
  <div class="m-7 fade-in">
    <h2>Productos</h2>
    <Button label="Nuevo Producto" icon="pi pi-plus" @click="handleCreate" class="mb-3" />
    <ProductoList ref="productoListRef" @edit="handleEdit" />
    <ProductoSave
      :mostrar="mostrarDialog"
      :producto="productoEdit"
      :modoEdicion="!!productoEdit"
      @guardar="handleGuardar"
      @close="handleCloseDialog"
    />
  </div>
</template>

<style scoped></style>
