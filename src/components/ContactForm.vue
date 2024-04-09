<template lang="">
  <div>
    <h2 class="text-[#0ea5e9] font-semibold text-3xl">
      ¿Te ha gustado lo que has visto?
    </h2>
    <p class="text-gray-200 text-2xl mb-5">¡Pues trabajemos juntos! 🙂</p>

    <form @submit.prevent="sendMail()" class="flex flex-col justify-center">
      <h1 class="text-white">Hola {{ name }}</h1>
      <div class="flex flex-col">
        <input
          type="text"
          name="name"
          id="name"
          v-model="formData.name"
          placeholder="Nombre y apellido"
          class="w-100 mt-2 py-3 px-3 rounded-lg bg-gray-800 dark:bg-gray-800 border border-gray-400 text-white font-semibold focus:border-[#0ea5e9] focus:outline-none"
        />
      </div>

      <div class="flex flex-col mt-2">
        <input
          type="email"
          name="email"
          id="email"
          v-model="formData.email"
          placeholder="Correo electrónico"
          class="w-100 mt-2 py-3 px-3 rounded-lg bg-gray-800 dark:bg-gray-800 border border-gray-400 text-white font-semibold focus:border-[#0ea5e9] focus:outline-none"
        />
      </div>

      <div class="flex flex-col mt-2">
        <textarea
          rows="5"
          name="message"
          id="message"
          v-model="formData.message"
          placeholder="Mensaje"
          class="w-100 mt-2 py-3 px-3 rounded-lg bg-gray-800 dark:bg-gray-800 border border-gray-400 text-white font-semibold focus:border-[#0ea5e9] focus:outline-none"
        ></textarea>
      </div>

      <div class="relative inline-flex group mt-8 w-full lg:w-[200px]">
        <div
          class="absolute transition-all duration-1000 opacity-70 -inset-px bg-gradient-to-r from-[#44BCFF] via-[#FF44EC] to-[#FF675E] rounded-xl blur-lg group-hover:opacity-100 group-hover:-inset-1 group-hover:duration-200 animate-tilt"
        ></div>
        <button
          class="relative inline-flex items-center justify-center w-full px-8 py-4 text-lg text-white font-semibold transition-all duration-200 bg-gray-900 font-pj rounded-xl focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-gray-900"
          type="submit"
        >
          Enviar
        </button>
      </div>
    </form>
  </div>
</template>
<script setup>
import { ref } from "vue";

const formData = ref({
  name: "",
  email: "",
  message: "",
});

async function sendMail() {
  fetch("http://localhost:3000/send-mail", {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify(formData.value),
  })
    .then((response) => {
      if (response.status === 200) {
        alert("Mensaje enviado correctamente");
      }
    })
    .catch((error) => {
      console.error("Error:", error);
    });
}
</script>
