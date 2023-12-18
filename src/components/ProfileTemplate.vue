<template>
  <div
    class="max-w-6xl mx-auto p-10 bg-white shadow-lg rounded-lg flex justify-between"
  >
    <!-- Professional Info Section -->
    <div class="flex flex-col justify-start">
      <div class="flex items-center space-x-4 mb-4">
        <div class="rounded-full h-48 w-48 bg-gray-300">
          <img
            src="https://images.unsplash.com/photo-1651008376811-b90baee60c1f?q=80&w=1887&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D"
            alt="Profile Picture"
            class="rounded-full w-48 h-48 object-cover"
          />
        </div>
        <div>
          <h2 class="text-xl font-semibold text-gray-700">Anna Castro</h2>
          <p class="text-gray-500 mb-1">PSICOLOGA | São Paulo</p>
          <v-rating
            v-model="rating"
            dense
            color="yellow"
            half-increments
            readonly
          ></v-rating>
          <span class="text-gray-500 text-sm mb-1">(20 reviews)</span>
          <span class="block text-lg font-semibold mb-1 text-gray-700">R$100 / 50 minutos</span>
          <p class="text-gray-500 mb-1">Idioma(s) Português </p>
        </div>
      </div>
      <div class="mt-1">
        <p class="text-gray-700 text-sm text-justify leading-normal">
          Formada pela Universidade de São Paulo (USP) em 2020. Com vasta
          experiência no campo da saúde mental, busco oferecer um cuidado
          compassivo e individualizado aos meus pacientes. Focando no tratamento
          de transtornos mentais, ansiedade, depressão e estresse
          pós-traumático. Busco sempre estar atualizada com as mais recentes
          pesquisas e terapias, meu objetivo é ajudar você a alcançar uma
          saúde mental plena e equilibrada.
        </p>
      </div>
    </div>

    <!-- Schedule Section -->
    <div class="mt-8 ml-6">
       <!-- Calendar Header -->
      <div class="bg-blue-500 text-white text-center py-2 rounded-t-lg">
        <h2 class="text-lg font-semibold">Horários Disponíveis</h2>
      </div>
      <div class="flex justify-start gap-1 bg-white ">
        <!-- Days of the week -->
        <div
          v-for="day in days"
          :key="day.date"
          class="flex flex-col items-center"
        >
        <div class="font-bold">{{ formatDay(day.date) }}</div>
          <div class="flex flex-col">
            <!-- Time slots for each day -->
            <div
              v-for="time in day.slots"
              :key="time"
              class="my-2 p-2 border rounded-lg text-center bg-green-100"
            >
              {{ time }}
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      days: [], 
      rating: 4.5, 
    };
  },
  mounted() {
    this.fetchAvailableSlots();
  },
  methods: {
    fetchAvailableSlots() {
    axios.get("http://localhost:3000/slots")
    .then((response) => {
      // Transforma o objeto de datas em um array de objetos com 'date' e 'slots'
      const formattedData = Object.keys(response.data).map((date) => {
        return {
          date: date,
          slots: response.data[date]
        };
      });
      this.days = formattedData;
    })
    .catch((error) => {
      // eslint-disable-next-line no-console
      console.error("There was an error fetching the slots:", error);
    });
    },
    formatDay(dateString) {
     return dateString.substr(8, 2); // Isso pega os dois últimos caracteres da string de data
    }
  },
};
</script>
