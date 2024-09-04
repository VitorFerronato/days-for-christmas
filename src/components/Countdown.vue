<template>
  <main
    class="flex-grow flex flex-col items-center justify-center text-center p-4"
  >
    <h1 class="text-4xl md:text-5xl font-extrabold mb-8 text-neon-red">
      Dias para o Natal
    </h1>
    <div class="flex flex-wrap justify-center space-x-2 md:space-x-4">
      <div class="calendar-unit">
        <div class="time-value">{{ timeRemaining.days }}</div>
        <div class="time-label">Dias</div>
      </div>
      <div class="calendar-unit">
        <div class="time-value">{{ timeRemaining.hours }}</div>
        <div class="time-label">Horas</div>
      </div>
      <div class="calendar-unit">
        <div class="time-value">{{ timeRemaining.minutes }}</div>
        <div class="time-label">Minutos</div>
      </div>
      <div class="calendar-unit">
        <div class="time-value">{{ timeRemaining.seconds }}</div>
        <div class="time-label">Segundos</div>
      </div>
    </div>
    <p class="text-base md:text-lg text-gray-500 mt-6">Prepare-se para as festas!</p>
  </main>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from "vue";
import moment from "moment";

const timeRemaining = ref({
  days: 0,
  hours: 0,
  minutes: 0,
  seconds: 0,
});

const calculateTimeRemaining = () => {
  const today = moment();
  let christmas = moment(`${today.year()}-12-25`);

  if (today.isAfter(christmas)) {
    christmas = christmas.add(1, "year");
  }

  const duration = moment.duration(christmas.diff(today));

  timeRemaining.value = {
    days: Math.floor(duration.asDays()),
    hours: duration.hours(),
    minutes: duration.minutes(),
    seconds: duration.seconds(),
  };
};

let interval;
onMounted(() => {
  calculateTimeRemaining();
  interval = setInterval(calculateTimeRemaining, 1000);
});

onUnmounted(() => {
  clearInterval(interval);
});
</script>

<style scoped>
.calendar-unit {
  background-color: #2d2d2d;
  color: white;
  border-radius: 16px;
  padding: 16px;
  width: 80px;
  margin: 8px; 
  border: 2px solid #ff1e56; 
  box-shadow: 0 0 10px #ff1e56; 
  text-shadow: 0 0 5px #ff1e56; 
}

.time-value {
  font-size: 2.5rem;
  font-weight: 700;
}

.time-label {
  font-size: 1.2rem;
  margin-top: 4px;
}

h1 {
  color: #ff1e56; 
  text-shadow: 0 0 10px #ff1e56; 
}

.text-neon-red {
  color: #ff1e56;
}

@media (min-width: 768px) {
  .calendar-unit {
    width: 200px;
    padding: 24px;
  }

  .time-value {
    font-size: 3.5rem;
  }

  .time-label {
    font-size: 1.5rem;
  }
}

@media (prefers-color-scheme: dark) {
  h1, .calendar-unit {
    color: white;
  }

  .calendar-unit {
    background-color: #1a1a1a; 
  }
}
</style>
