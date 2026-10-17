<template>
  <div class="space-y-6 my-6">
    <!-- Bloco do Relógio / Contador Regressivo -->
    <div class="bg-gradient-to-br from-emerald-900 via-teal-900 to-slate-900 text-white p-6 sm:p-8 rounded-2xl shadow-xl border border-emerald-700/50">
      <div class="text-center max-w-xl mx-auto">
        <span class="inline-block px-3 py-1 bg-emerald-500/20 text-emerald-300 text-xs font-semibold rounded-full uppercase tracking-wider mb-2">
          Contagem Regressiva
        </span>
        <h3 class="text-xl sm:text-2xl font-black uppercase tracking-wide text-amber-400">
          Festival de Parintins 2027
        </h3>
        <p class="text-xs sm:text-sm text-emerald-100/80 mt-1 mb-6">
          Início em 25 de Junho de 2027 às 00:01 • Bumbódromo de Parintins
        </p>

        <!-- Grade dos Contadores -->
        <div class="grid grid-cols-4 gap-2 sm:gap-4 my-4">
          <div class="bg-black/40 backdrop-blur border border-white/10 p-3 sm:p-4 rounded-xl text-center">
            <span class="block text-2xl sm:text-4xl font-black text-amber-400 font-mono">{{ tempo.dias }}</span>
            <span class="text-[10px] sm:text-xs font-bold uppercase tracking-widest text-emerald-200">Dias</span>
          </div>
          <div class="bg-black/40 backdrop-blur border border-white/10 p-3 sm:p-4 rounded-xl text-center">
            <span class="block text-2xl sm:text-4xl font-black text-amber-400 font-mono">{{ tempo.horas }}</span>
            <span class="text-[10px] sm:text-xs font-bold uppercase tracking-widest text-emerald-200">Horas</span>
          </div>
          <div class="bg-black/40 backdrop-blur border border-white/10 p-3 sm:p-4 rounded-xl text-center">
            <span class="block text-2xl sm:text-4xl font-black text-amber-400 font-mono">{{ tempo.minutos }}</span>
            <span class="text-[10px] sm:text-xs font-bold uppercase tracking-widest text-emerald-200">Minutos</span>
          </div>
          <div class="bg-black/40 backdrop-blur border border-white/10 p-3 sm:p-4 rounded-xl text-center">
            <span class="block text-2xl sm:text-4xl font-black text-amber-400 font-mono">{{ tempo.segundos }}</span>
            <span class="text-[10px] sm:text-xs font-bold uppercase tracking-widest text-emerald-200">Segundos</span>
          </div>
        </div>
      </div>
    </div>

    <!-- Cards do Cronograma de Apresentações -->
    <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
      <!-- 1ª Noite -->
      <div class="bg-white p-5 rounded-xl border border-gray-200 shadow-sm hover:shadow-md transition">
        <div class="flex items-center space-x-2 text-emerald-800 font-bold mb-2">
          <i class="fas fa-calendar-day"></i>
          <span>1ª Noite — 25/06/2027</span>
        </div>
        <p class="text-sm font-semibold text-gray-900">Sexta-feira</p>
        <p class="text-xs text-gray-600 mt-1">Abertura oficial e 1ª noite de disputa na arena do Bumbódromo.</p>
      </div>

      <!-- 2ª Noite -->
      <div class="bg-white p-5 rounded-xl border border-gray-200 shadow-sm hover:shadow-md transition">
        <div class="flex items-center space-x-2 text-emerald-800 font-bold mb-2">
          <i class="fas fa-calendar-day"></i>
          <span>2ª Noite — 26/06/2027</span>
        </div>
        <p class="text-sm font-semibold text-gray-900">Sábado</p>
        <p class="text-xs text-gray-600 mt-1">2ª noite de espetáculo dos Bois Caprichoso e Garantido.</p>
      </div>

      <!-- 3ª Noite -->
      <div class="bg-white p-5 rounded-xl border border-gray-200 shadow-sm hover:shadow-md transition">
        <div class="flex items-center space-x-2 text-emerald-800 font-bold mb-2">
          <i class="fas fa-calendar-day"></i>
          <span>3ª Noite — 27/06/2027</span>
        </div>
        <p class="text-sm font-semibold text-gray-900">Domingo</p>
        <p class="text-xs text-gray-600 mt-1">Encerramento das apresentações do Festival Folclórico.</p>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

// Data configurada para 25 de Junho de 2027 às 00:01:00
const DATA_FESTIVAL = new Date(2027, 5, 25, 0, 1, 0).getTime()

const tempo = ref({
  dias: '00',
  horas: '00',
  minutos: '00',
  segundos: '00'
})

let timer: ReturnType<typeof setInterval> | null = null

const atualizarRelogio = () => {
  const agora = new Date().getTime()
  const diferenca = DATA_FESTIVAL - agora

  if (diferenca > 0) {
    const d = Math.floor(diferenca / (1000 * 60 * 60 * 24))
    const h = Math.floor((diferenca % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60))
    const m = Math.floor((diferenca % (1000 * 60 * 60)) / (1000 * 60))
    const s = Math.floor((diferenca % (1000 * 60)) / 1000)

    tempo.value = {
      dias: String(d).padStart(2, '0'),
      horas: String(h).padStart(2, '0'),
      minutos: String(m).padStart(2, '0'),
      segundos: String(s).padStart(2, '0')
    }
  } else {
    tempo.value = { dias: '00', horas: '00', minutos: '00', segundos: '00' }
    if (timer) clearInterval(timer)
  }
}

onMounted(() => {
  atualizarRelogio()
  timer = setInterval(atualizarRelogio, 1000)
})

onUnmounted(() => {
  if (timer) clearInterval(timer)
})
</script>
