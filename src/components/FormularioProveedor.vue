<script setup>
import { ref } from 'vue'

const nombreEmpresa = ref('')
const nombreContacto = ref('')
const telefono = ref('')
const correoElectronico = ref('')
const categoria = ref('')
const ciudad = ref('')
const mensaje = ref('')
const mensajeExito = ref(false)
const proveedores = ref([])

function registrarProveedor() {
  const camposObligatorios = [
    nombreEmpresa.value.trim(),
    nombreContacto.value.trim(),
    telefono.value.trim(),
    correoElectronico.value.trim(),
    categoria.value.trim(),
  ]

  if (camposObligatorios.some((campo) => campo === '')) {
    mensaje.value = 'Complete todos los campos obligatorios.'
    mensajeExito.value = false
    return
  }

  console.log({
    nombreEmpresa: nombreEmpresa.value,
    nombreContacto: nombreContacto.value,
    telefono: telefono.value,
    correoElectronico: correoElectronico.value,
    categoria: categoria.value,
    ciudad: ciudad.value,
  })

  mensaje.value = 'Proveedor registrado correctamente.'
  mensajeExito.value = true

  proveedores.value.push({
    empresa: nombreEmpresa.value,
    contacto: nombreContacto.value,
    telefono: telefono.value,
    correo: correoElectronico.value,
    categoria: categoria.value,
    ciudad: ciudad.value,
  })

  nombreEmpresa.value = ''
  nombreContacto.value = ''
  telefono.value = ''
  correoElectronico.value = ''
  categoria.value = ''
  ciudad.value = ''
}
</script>

<template>
  <form class="formulario-proveedor" @submit.prevent="registrarProveedor">
    <h2>Registrar proveedor</h2>

    <label>
      <span>Nombre de la empresa</span>
      <input v-model="nombreEmpresa" type="text" placeholder="Ej. Distribuciones Sol" required />
    </label>

    <label>
      <span>Nombre del contacto</span>
      <input v-model="nombreContacto" type="text" placeholder="Ej. Ana Pérez" required />
    </label>

    <label>
      <span>Teléfono</span>
      <input v-model="telefono" type="tel" placeholder="Ej. 555-1234" required />
    </label>

    <label>
      <span>Correo electrónico</span>
      <input v-model="correoElectronico" type="email" placeholder="Ej. contacto@empresa.com" required />
    </label>

    <label>
      <span>Categoría</span>
      <select v-model="categoria" required>
        <option value="">Seleccione una opción</option>
        <option value="Alimentos">Alimentos</option>
        <option value="Tecnología">Tecnología</option>
        <option value="Ropa">Ropa</option>
        <option value="Servicios">Servicios</option>
        <option value="Otros">Otros</option>
      </select>
    </label>

    <label>
      <span>Ciudad</span>
      <input v-model="ciudad" type="text" placeholder="Ej. Medellín" required />
    </label>

    <p v-if="mensaje" :class="mensajeExito ? 'mensaje-exito' : 'mensaje-error'">
      {{ mensaje }}
    </p>

    <button type="submit">Registrar proveedor</button>
  </form>

  <section class="lista-proveedores">
    <h3>Proveedores registrados</h3>

    <p v-if="proveedores.length === 0">No existen proveedores registrados.</p>

    <div v-else class="cards-proveedores">
      <article v-for="(proveedor, index) in proveedores" :key="index" class="card-proveedor">
        <p><strong>Empresa:</strong> {{ proveedor.empresa }}</p>
        <p><strong>Contacto:</strong> {{ proveedor.contacto }}</p>
        <p><strong>Teléfono:</strong> {{ proveedor.telefono }}</p>
        <p><strong>Correo:</strong> {{ proveedor.correo }}</p>
        <p><strong>Categoría:</strong> {{ proveedor.categoria }}</p>
        <p><strong>Ciudad:</strong> {{ proveedor.ciudad }}</p>
      </article>
    </div>
  </section>
</template>

<style scoped>
.formulario-proveedor {
  display: grid;
  gap: 0.9rem;
  background: white;
  padding: 1.25rem;
  border-radius: 1rem;
  box-shadow: 0 10px 25px rgba(15, 23, 42, 0.08);
}

.formulario-proveedor h2 {
  margin: 0 0 0.2rem;
  font-size: 1.2rem;
  color: #1e3a8a;
}

.formulario-proveedor label {
  display: grid;
  gap: 0.35rem;
  font-weight: 600;
  color: #374151;
}

.formulario-proveedor input,
.formulario-proveedor select {
  padding: 0.7rem 0.8rem;
  border: 1px solid #cbd5e1;
  border-radius: 0.7rem;
  font-size: 0.95rem;
}

.mensaje-error {
  margin: 0;
  padding: 0.7rem 0.8rem;
  border-radius: 0.7rem;
  background: #fee2e2;
  color: #b91c1c;
  font-weight: 600;
}

.mensaje-exito {
  margin: 0;
  padding: 0.7rem 0.8rem;
  border-radius: 0.7rem;
  background: #dcfce7;
  color: #166534;
  font-weight: 600;
}

.lista-proveedores {
  margin-top: 1rem;
  background: white;
  padding: 1.25rem;
  border-radius: 1rem;
  box-shadow: 0 10px 25px rgba(15, 23, 42, 0.08);
}

.lista-proveedores h3 {
  margin: 0 0 0.8rem;
  color: #1e3a8a;
}

.cards-proveedores {
  display: grid;
  gap: 0.8rem;
}

.card-proveedor {
  padding: 0.9rem;
  border: 1px solid #e5e7eb;
  border-radius: 0.8rem;
  background: #f8fafc;
}

.card-proveedor p {
  margin: 0.25rem 0;
}

.formulario-proveedor button {
  padding: 0.8rem 1rem;
  border: none;
  border-radius: 0.7rem;
  background: #2563eb;
  color: white;
  font-weight: 700;
  cursor: pointer;
}

.formulario-proveedor button:hover {
  background: #1d4ed8;
}
</style>
