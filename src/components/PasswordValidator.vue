<template>
  <div>
    <h2>Validador de Contraseña</h2>
    <input type="password" v-model="password" placeholder="Escribe tu contraseña" />

    <ul>
      <li>
        <span>{{ hasUpperLower ? "✔" : "❌" }}</span>
        Contiene mayúscula y minúscula
      </li>
      <li>
        <span>{{ hasNumber ? "✔" : "❌" }}</span>
        Contiene un número
      </li>
      <li>
        <span>{{ hasSpecial ? "✔" : "❌" }}</span>
        Contiene un carácter especial (!@#$%^)
      </li>
      <li>
        <span>{{ hasMinLength ? "✔" : "❌" }}</span>
        Al menos 8 caracteres
      </li>
    </ul>

    <div v-if="isValid" style="color: green; font-weight: bold;">
      Contraseña válida
    </div>
  </div>
</template>

<script>
import { ref, computed } from "vue";

export default {
  name: "PasswordValidator",
  setup() {
    const password = ref("");

    const hasUpperLower = computed(() => /(?=.*[a-z])(?=.*[A-Z])/.test(password.value));
    const hasNumber = computed(() => /[0-9]/.test(password.value));
    const hasSpecial = computed(() => /[!@#$%^]/.test(password.value));
    const hasMinLength = computed(() => password.value.length >= 8);

    const isValid = computed(() => hasUpperLower.value && hasNumber.value && hasSpecial.value && hasMinLength.value);

    return { password, hasUpperLower, hasNumber, hasSpecial, hasMinLength, isValid };
  }
};
</script>

<style scoped>
input {
  margin-bottom: 1em;
  padding: 0.5em;
}
li {
  margin: 0.3em 0;
}
</style>

//Por qué usamos computed:

//Cada validación depende de la contraseña y se actualiza 
//automáticamente cuando el usuario escribe.

//isValid combina todas las validaciones para mostrar el 
//mensaje final solo si todo es correcto.