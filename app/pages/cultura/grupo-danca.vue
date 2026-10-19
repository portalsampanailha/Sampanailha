<script setup lang="ts">
import { ref } from 'vue'

useSeoMeta({
  title: 'Grupo de Dança — Portal Sampa na Ilha',
  description: 'O corpo de dança do Sampa na Ilha leva a musicalidade e a coreografia do boi-bumbá para os palcos de São Paulo.',
})

// Controla a exibição do formulário ao clicar
const mostrarFormulario = ref(false)
</script>

<template>
  <div>
    <ComumHeroPagina
      titulo="Grupo de Dança"
      descricao="O corpo de dança do Sampa na Ilha leva a musicalidade e a coreografia do boi-bumbá para os palcos de São Paulo."
      etiqueta="Cultura"
      etiqueta-icone="fas fa-music"
      etiqueta-cor="purple"
    />

    <div class="container">
      <div class="layout">
        <main class="page-content">
          <p>
            O Grupo de Dança é uma das frentes de Formação Cultural do projeto Sampa na Ilha: um espaço
            de preparação coreográfica e intercâmbio com a dança de boi-bumbá, aberto a quem quer viver
            a cultura amazônica na prática, em São Paulo.
          </p>

          <CulturaFrente />

          <!-- BLOCO DE INSCRIÇÃO (SITUA-SE ANTES DE OUTRAS FRENTES) -->
          <div class="bg-white p-6 rounded-2xl border border-gray-200 shadow-sm my-6">
            <div class="flex flex-col sm:flex-row items-start sm:items-center justify-between gap-4">
              <div class="flex items-center space-x-4">
                <div class="p-3 bg-emerald-100 text-emerald-800 rounded-xl">
                  <i class="fas fa-file-signature text-2xl"></i>
                </div>
                <div>
                  <h3 class="text-lg font-bold text-gray-900">Inscrições Abertas</h3>
                  <p class="text-xs sm:text-sm text-gray-600">Garanta a sua vaga no Grupo de Dança do Sampa na Ilha.</p>
                </div>
              </div>

              <button 
                @click="mostrarFormulario = !mostrarFormulario"
                type="button"
                class="px-5 py-2.5 bg-emerald-800 hover:bg-emerald-900 text-white font-bold rounded-xl transition shadow flex items-center gap-2 cursor-pointer text-sm"
              >
                <span>{{ mostrarFormulario ? 'Fechar Formulário' : 'Fazer Inscrição' }}</span>
                <i :class="mostrarFormulario ? 'fas fa-chevron-up' : 'fas fa-chevron-down'"></i>
              </button>
            </div>

            <!-- FORMULÁRIO EXPANSÍVEL AO CLICAR -->
            <transition name="fade">
              <div v-if="mostrarFormulario" class="mt-6 pt-6 border-t border-gray-100">
                <h4 class="text-base font-bold text-emerald-900 mb-4">Preencha os seus dados:</h4>

                <form @submit.prevent class="space-y-4">
                  <!-- Nome e Sobrenome -->
                  <div>
                    <label class="block text-sm font-semibold text-gray-700 mb-1">Nome e Sobrenome</label>
                    <input 
                      type="text" 
                      required 
                      placeholder="Digite seu nome e sobrenome"
                      class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-emerald-600 focus:outline-none text-gray-900"
                    />
                  </div>

                  <!-- E-mail e Telefone -->
                  <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                    <div>
                      <label class="block text-sm font-semibold text-gray-700 mb-1">E-mail</label>
                      <input 
                        type="email" 
                        required 
                        placeholder="seuemail@exemplo.com"
                        class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-emerald-600 focus:outline-none text-gray-900"
                      />
                    </div>
                    <div>
                      <label class="block text-sm font-semibold text-gray-700 mb-1">Telefone / WhatsApp</label>
                      <input 
                        type="tel" 
                        required 
                        placeholder="(11) 99999-9999"
                        class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-emerald-600 focus:outline-none text-gray-900"
                      />
                    </div>
                  </div>

                  <!-- Experiência com Dança -->
                  <div>
                    <label class="block text-sm font-semibold text-gray-700 mb-2">Já tem experiência com Dança?</label>
                    <div class="flex items-center space-x-6">
                      <label class="flex items-center space-x-2 cursor-pointer text-gray-800">
                        <input type="radio" name="experiencia" value="sim" required class="text-emerald-700 focus:ring-emerald-600" />
                        <span>Sim</span>
                      </label>
                      <label class="flex items-center space-x-2 cursor-pointer text-gray-800">
                        <input type="radio" name="experiencia" value="nao" required class="text-emerald-700 focus:ring-emerald-600" />
                        <span>Não</span>
                      </label>
                    </div>
                  </div>

                  <!-- Botão de Envio -->
                  <button 
                    type="submit" 
                    class="w-full sm:w-auto px-6 py-3 bg-emerald-800 hover:bg-emerald-900 text-white font-bold rounded-lg shadow transition cursor-pointer mt-4"
                  >
                    Enviar Inscrição
                  </button>
                </form>
              </div>
            </transition>
          </div>

          <!-- MANTÉM O TÍTULO E CARTOÕES DA SUA FOTO INTACTOS -->
          <ComumCabecalhoSecao titulo="Outras frentes do projeto" />
          <CulturaSubpaginas exceto="/cultura/grupo-danca" />
        </main>

        <SidebarPrincipal :tempo="false" />
      </div>
    </div>
  </div>
</template>
