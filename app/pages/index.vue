<template>
  <div>
    <!-- Random Buy Toast -->
    <Transition name="toast">
      <div
        v-if="showToast"
        class="fixed bottom-6 left-6 z-50 bg-white dark:bg-zinc-800 border border-zinc-200 dark:border-zinc-700 rounded-xl shadow-lg px-4 py-3 flex items-center gap-3 max-w-sm"
      >
        <div class="size-9 rounded-full bg-primary/10 flex items-center justify-center shrink-0">
          <UIcon name="i-lucide-shopping-cart" class="size-4 text-primary" />
        </div>
        <div class="min-w-0">
          <p class="text-sm font-medium truncate">{{ currentBuyer.name }} comprou o {{ currentBuyer.kit }}</p>
          <p class="text-xs text-muted">{{ currentBuyer.city }}, {{ currentBuyer.state }} • {{ currentBuyer.time }}</p>
        </div>
        <UButton
          icon="i-lucide-x"
          size="xs"
          variant="ghost"
          color="neutral"
          class="shrink-0 -mr-1"
          @click="dismissToast()"
        />
      </div>
    </Transition>

    <div class="bg-primary/10 border-b border-primary/20 px-4 py-2">
      <div class="max-w-7xl mx-auto flex items-center justify-center gap-2 text-sm text-primary-600 dark:text-primary-400">
        <UIcon name="i-lucide-zap" class="size-4" />
        <span>Milhares já estão completando o álbum sem gastar com pacotinhos repetidos.</span>
      </div>
    </div>

    <!-- Hero Section -->
    <section class="relative overflow-hidden">
      <div class="max-w-4xl mx-auto px-4 py-16 md:py-24 text-center">
        <div class="inline-flex items-center gap-2 bg-primary/10 text-primary-600 dark:text-primary-400 px-4 py-1.5 rounded-full text-sm font-medium mb-6">
          <UIcon name="i-lucide-trophy" class="size-4" />
          Figurinhas da Copa 2026 Imprimíveis
        </div>

        <h1 class="text-4xl md:text-6xl font-extrabold tracking-tight text-balance mb-6">
          Pare de gastar dinheiro com pacotinho repetido
        </h1>

        <p class="text-lg md:text-xl text-muted max-w-2xl mx-auto mb-10">
          Receba exatamente as figurinhas que faltam — prontas para imprimir — e complete seu álbum da Copa 2026 sem depender da sorte.
        </p>

        <!-- Hero Video -->
        <div class="max-w-xs mx-auto mb-10">
          <div class="relative rounded-2xl overflow-hidden shadow-2xl border border-zinc-200 dark:border-zinc-700 bg-black">
            <video
              ref="heroVideo"
              autoplay
              muted
              playsinline
              class="w-full aspect-[9/16] cursor-pointer"
              @click="toggleVideo"
            />
            <button
              v-if="showSoundOverlay"
              class="absolute inset-0 flex flex-col items-center justify-center gap-3 bg-black/50 cursor-pointer transition-opacity"
              @click="unmuteVideo"
            >
              <div class="size-16 rounded-full bg-white/20 backdrop-blur flex items-center justify-center">
                <UIcon name="i-lucide-volume-2" class="size-7 text-white" />
              </div>
              <span class="text-white font-medium text-sm">Clique para ouvir</span>
            </button>
          </div>
        </div>

        <div class="flex flex-col sm:flex-row items-center justify-center gap-4">
          <UButton
            to="#kits"
            size="xl"
            class="text-base font-bold px-8"
          >
            <UIcon name="i-lucide-download" class="size-5" />
            Quero as figurinhas que faltam
          </UButton>
        </div>

        <div class="flex items-center justify-center gap-4 mt-6 text-sm text-muted">
          <span class="flex items-center gap-1"><UIcon name="i-lucide-shield-check" class="size-4" /> Pagamento seguro</span>
          <span class="hidden sm:inline">•</span>
          <span class="flex items-center gap-1"><UIcon name="i-lucide-zap" class="size-4" /> Acesso imediato</span>
          <span class="hidden sm:inline">•</span>
          <span class="flex items-center gap-1"><UIcon name="i-lucide-printer" class="size-4" /> Fácil de imprimir</span>
        </div>
      </div>
    </section>

    <!-- Problem Section -->
    <section class="bg-zinc-50 dark:bg-zinc-900/50">
      <div class="max-w-4xl mx-auto px-4 py-16 md:py-20">
        <div class="text-center mb-10">
          <span class="inline-flex items-center gap-1.5 text-primary text-sm font-semibold mb-3">
            <UIcon name="i-lucide-star" class="size-4" /> O problema
          </span>
          <h2 class="text-3xl md:text-4xl font-bold tracking-tight text-balance">
            Quantas repetidas você já tirou?
          </h2>
        </div>

        <p class="text-center text-lg text-muted mb-10">
          Você compra vários pacotinhos…<br>E sempre acontece a mesma coisa:
        </p>

        <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 max-w-lg mx-auto">
          <div class="flex items-center gap-3 bg-white dark:bg-zinc-800 rounded-xl p-4 border border-zinc-200 dark:border-zinc-700">
            <UIcon name="i-lucide-x-circle" class="size-5 text-red-500 shrink-0" />
            <span class="text-sm">Figurinha repetida</span>
          </div>
          <div class="flex items-center gap-3 bg-white dark:bg-zinc-800 rounded-xl p-4 border border-zinc-200 dark:border-zinc-700">
            <UIcon name="i-lucide-x-circle" class="size-5 text-red-500 shrink-0" />
            <span class="text-sm">Dinheiro indo embora</span>
          </div>
          <div class="flex items-center gap-3 bg-white dark:bg-zinc-800 rounded-xl p-4 border border-zinc-200 dark:border-zinc-700">
            <UIcon name="i-lucide-x-circle" class="size-5 text-red-500 shrink-0" />
            <span class="text-sm">Álbum nunca completa</span>
          </div>
          <div class="flex items-center gap-3 bg-white dark:bg-zinc-800 rounded-xl p-4 border border-zinc-200 dark:border-zinc-700">
            <UIcon name="i-lucide-x-circle" class="size-5 text-red-500 shrink-0" />
            <span class="text-sm">Faltam poucas e elas simplesmente não vêm</span>
          </div>
        </div>
      </div>
    </section>

    <!-- How It Works -->
    <section>
      <div class="max-w-4xl mx-auto px-4 py-16 md:py-20">
        <div class="text-center mb-12">
          <span class="inline-flex items-center gap-1.5 text-primary text-sm font-semibold mb-3">
            <UIcon name="i-lucide-star" class="size-4" /> Simples assim
          </span>
          <h2 class="text-3xl md:text-4xl font-bold tracking-tight text-balance">
            Como funciona?
          </h2>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-4 gap-6">
          <div v-for="step in steps" :key="step.number" class="text-center">
            <div class="inline-flex items-center justify-center size-14 rounded-full bg-primary/10 text-primary font-bold text-xl mb-4">
              {{ step.number }}
            </div>
            <p class="font-medium text-sm">{{ step.text }}</p>
          </div>
        </div>

        <div class="mt-12 text-center">
          <UButton
            to="#kits"
            size="xl"
            class="text-base font-bold px-8"
          >
            <UIcon name="i-lucide-trophy" class="size-5" />
            Quero completar meu álbum
          </UButton>
        </div>
      </div>
    </section>

    <!-- Preview Section -->
    <section class="bg-zinc-50 dark:bg-zinc-900/50">
      <div class="max-w-6xl mx-auto px-4 py-16 md:py-20">
        <div class="text-center mb-12">
          <h2 class="text-3xl md:text-4xl font-bold tracking-tight text-balance mb-4">
            O que você vai receber!
          </h2>
          <p class="text-muted">
            Veja como as figurinhas ficarão no seu álbum da Copa 2026.
          </p>
        </div>

        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
          <div v-for="preview in previews" :key="preview.title" class="group">
            <div class="rounded-xl overflow-hidden border border-zinc-200 dark:border-zinc-700 bg-white dark:bg-zinc-800 shadow-sm">
              <img :src="preview.img" :alt="preview.title" class="w-full h-48 object-cover">
            </div>
            <p class="text-center text-sm font-medium mt-3">{{ preview.title }}</p>
          </div>
        </div>

        <div class="mt-10 text-center">
          <UButton
            to="#kits"
            size="xl"
            class="text-base font-bold px-8"
          >
            <UIcon name="i-lucide-download" class="size-5" />
            Baixar figurinhas
          </UButton>
        </div>
      </div>
    </section>

    <!-- Comparison Section -->
    <section>
      <div class="max-w-4xl mx-auto px-4 py-16 md:py-20">
        <div class="text-center mb-12">
          <span class="inline-flex items-center gap-1.5 text-primary text-sm font-semibold mb-3">
            <UIcon name="i-lucide-star" class="size-4" /> Comparativo
          </span>
          <h2 class="text-3xl md:text-4xl font-bold tracking-tight text-balance">
            O que faz mais sentido?
          </h2>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
          <!-- Traditional -->
          <div class="bg-red-50 dark:bg-red-950/20 border border-red-200 dark:border-red-900/50 rounded-2xl p-6">
            <h3 class="flex items-center gap-2 text-lg font-bold text-red-600 dark:text-red-400 mb-5">
              <UIcon name="i-lucide-x-circle" class="size-5" />
              Pacotinhos tradicionais
            </h3>
            <ul class="space-y-3">
              <li v-for="item in traditionalItems" :key="item" class="flex items-start gap-2.5">
                <UIcon name="i-lucide-x" class="size-4 text-red-500 mt-0.5 shrink-0" />
                <span class="text-sm">{{ item }}</span>
              </li>
            </ul>
          </div>

          <!-- Solution -->
          <div class="bg-primary-50 dark:bg-primary-950/20 border border-primary-200 dark:border-primary-900/50 rounded-2xl p-6">
            <h3 class="flex items-center gap-2 text-lg font-bold text-primary-600 dark:text-primary-400 mb-5">
              <UIcon name="i-lucide-check-circle" class="size-5" />
              Sua solução
            </h3>
            <ul class="space-y-3">
              <li v-for="item in solutionItems" :key="item" class="flex items-start gap-2.5">
                <UIcon name="i-lucide-check" class="size-4 text-primary mt-0.5 shrink-0" />
                <span class="text-sm">{{ item }}</span>
              </li>
            </ul>
          </div>
        </div>

        <div class="mt-10 text-center">
          <UButton
            to="#kits"
            size="xl"
            class="text-base font-bold px-8"
          >
            <UIcon name="i-lucide-flag" class="size-5" />
            Quero completar meu álbum
          </UButton>
        </div>
      </div>
    </section>

    <!-- Pricing Section -->
    <section id="kits" class="bg-zinc-50 dark:bg-zinc-900/50 scroll-mt-24">
      <div class="max-w-5xl mx-auto px-4 py-16 md:py-20">
        <div class="text-center mb-12">
          <span class="inline-flex items-center gap-1.5 text-primary text-sm font-semibold mb-3">
            <UIcon name="i-lucide-star" class="size-4" /> Oferta especial
          </span>
          <h2 class="text-3xl md:text-4xl font-bold tracking-tight text-balance">
            Escolha o seu kit
          </h2>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 gap-8 max-w-3xl mx-auto">
          <!-- Kit Bronze -->
          <div class="bg-white dark:bg-zinc-800 rounded-2xl border border-zinc-200 dark:border-zinc-700 overflow-hidden">
            <div class="p-6">
              <div class="flex items-center gap-2 mb-4">
                <span class="text-2xl">🥉</span>
                <h3 class="text-xl font-bold">Kit Bronze</h3>
              </div>

              <div class="mb-6">
                <img src="/images/kit-bronze-Dhl_RMNB-Dhl_RMNB.png" alt="Kit Bronze" class="w-full rounded-lg">
              </div>

              <div class="mb-4">
                <span class="text-sm text-muted line-through">De R$ 39,90</span>
                <p class="text-3xl font-extrabold text-primary">R$ 17,90</p>
              </div>

              <ul class="space-y-2.5 mb-6">
                <li v-for="item in kitBronzeItems" :key="item.text" class="flex items-start gap-2.5">
                  <UIcon :name="item.included ? 'i-lucide-check' : 'i-lucide-x'" :class="[item.included ? 'text-primary' : 'text-zinc-300 dark:text-zinc-600', 'size-4 mt-0.5 shrink-0']" />
                  <span :class="['text-sm', !item.included ? 'text-zinc-400 dark:text-zinc-500' : '']">{{ item.text }}</span>
                </li>
              </ul>

              <UButton
                to="https://pay.kiwify.com.br/TjxdKGj"
                target="_blank"
                block
                size="xl"
                class="font-bold"
              >
                <UIcon name="i-lucide-zap" class="size-5" />
                Quero o Kit Bronze
              </UButton>
            </div>
          </div>

          <!-- Kit Ouro -->
          <div class="bg-white dark:bg-zinc-800 rounded-2xl border-2 border-primary ring-4 ring-primary/10 overflow-hidden relative">
            <div class="absolute top-0 left-1/2 -translate-x-1/2 bg-primary text-primary-foreground text-xs font-bold px-4 py-1 rounded-b-lg">
              <UIcon name="i-lucide-star" class="size-3 inline" /> Mais escolhido
            </div>

            <div class="p-6 pt-10">
              <div class="flex items-center gap-2 mb-4">
                <span class="text-2xl">🥇</span>
                <h3 class="text-xl font-bold">Kit Ouro</h3>
              </div>

              <div class="mb-6">
                <img src="/images/kit-ouro-DzEcEHea-DzEcEHea.png" alt="Kit Ouro" class="w-full rounded-lg">
              </div>

              <div class="mb-4">
                <span class="text-sm text-muted line-through">De R$ 59,90</span>
                <p class="text-3xl font-extrabold text-primary">R$ 37,90</p>
              </div>

              <ul class="space-y-2.5 mb-6">
                <li v-for="item in kitOuroItems" :key="item" class="flex items-start gap-2.5">
                  <UIcon name="i-lucide-check" class="size-4 text-primary mt-0.5 shrink-0" />
                  <span class="text-sm">{{ item }}</span>
                </li>
              </ul>

              <UButton
                to="https://pay.kiwify.com.br/eMBEORl"
                target="_blank"
                block
                size="xl"
                class="font-bold"
              >
                <UIcon name="i-lucide-trophy" class="size-5" />
                Quero o Kit Ouro
              </UButton>
            </div>
          </div>
        </div>

        <div class="mt-8 text-center">
          <UButton
            to="https://wa.me/5598999850510"
            target="_blank"
            variant="ghost"
            color="neutral"
            size="lg"
          >
            <UIcon name="i-lucide-message-circle" class="size-5" />
            Ficou alguma dúvida? Chame no WhatsApp
          </UButton>
        </div>
      </div>
    </section>

    <!-- Testimonials Section -->
    <section>
      <div class="max-w-6xl mx-auto px-4 py-16 md:py-20">
        <div class="text-center mb-12">
          <span class="inline-flex items-center gap-1.5 text-primary text-sm font-semibold mb-3">
            <UIcon name="i-lucide-star" class="size-4" /> Quem já completou
          </span>
          <h2 class="text-3xl md:text-4xl font-bold tracking-tight text-balance">
            O que estão dizendo
          </h2>
        </div>

        <div class="overflow-x-auto pb-4">
          <div class="flex gap-4 min-w-max px-4">
            <img
              v-for="i in 6"
              :key="i"
              :src="`/images/feedback-${i}-${feedbackHashes[i - 1]}.png`"
              :alt="`Depoimento ${i}`"
              class="h-96 w-auto rounded-xl shadow-lg shrink-0"
            >
          </div>
        </div>

        <p class="text-center text-sm text-muted mt-4">
          ← Arraste →
        </p>
      </div>
    </section>

    <!-- FAQ Section -->
    <section class="bg-zinc-50 dark:bg-zinc-900/50">
      <div class="max-w-2xl mx-auto px-4 py-16 md:py-20">
        <div class="text-center mb-12">
          <h2 class="text-3xl md:text-4xl font-bold tracking-tight text-balance">
            <span class="inline-flex items-center gap-2">
              <UIcon name="i-lucide-help-circle" class="size-8 text-primary" />
              Perguntas Frequentes
            </span>
          </h2>
        </div>

        <UAccordion
          :items="faqItems"
          multiple
          size="lg"
        />
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import Hls from 'hls.js'

const heroVideo = useTemplateRef('heroVideo')
const hlsUrl = 'https://vz-6232ce16-132.b-cdn.net/b0452988-f917-4c1f-9660-0052159faf3b/playlist.m3u8'
const showSoundOverlay = ref(true)

function unmuteVideo() {
  showSoundOverlay.value = false
  const video = heroVideo.value
  if (!video) return
  video.muted = false
  video.currentTime = 0
  video.play()
}

function toggleVideo() {
  if (showSoundOverlay.value) return
  const video = heroVideo.value
  if (!video) return
  if (video.paused) {
    video.play()
  } else {
    video.pause()
  }
}

onMounted(() => {
  const video = heroVideo.value
  if (!video) return

  if (Hls.isSupported()) {
    const hls = new Hls()
    hls.loadSource(hlsUrl)
    hls.attachMedia(video)
  } else if (video.canPlayType('application/vnd.apple.mpegurl')) {
    video.src = hlsUrl
  }
})

const buyers = [
  { name: 'Lucas M.', city: 'São Paulo', state: 'SP' },
  { name: 'Ana C.', city: 'Rio de Janeiro', state: 'RJ' },
  { name: 'Pedro H.', city: 'Belo Horizonte', state: 'MG' },
  { name: 'Mariana S.', city: 'Salvador', state: 'BA' },
  { name: 'João V.', city: 'Fortaleza', state: 'CE' },
  { name: 'Camila R.', city: 'Brasília', state: 'DF' },
  { name: 'Rafael O.', city: 'Curitiba', state: 'PR' },
  { name: 'Beatriz L.', city: 'Recife', state: 'PE' },
  { name: 'Felipe A.', city: 'Manaus', state: 'AM' },
  { name: 'Juliana P.', city: 'Porto Alegre', state: 'RS' },
  { name: 'Gustavo N.', city: 'Florianópolis', state: 'SC' },
  { name: 'Larissa D.', city: 'Goiânia', state: 'GO' },
  { name: 'Bruno T.', city: 'Belém', state: 'PA' },
  { name: 'Amanda F.', city: 'Vitória', state: 'ES' },
  { name: 'Thiago C.', city: 'São Luís', state: 'MA' },
  { name: 'Fernanda M.', city: 'Natal', state: 'RN' },
  { name: 'Diego S.', city: 'Campo Grande', state: 'MS' },
  { name: 'Patrícia W.', city: 'Cuiabá', state: 'MT' },
  { name: 'André K.', city: 'Aracaju', state: 'SE' },
  { name: 'Carolina B.', city: 'Campinas', state: 'SP' }
]

const kits = ['Kit Ouro', 'Kit Ouro', 'Kit Ouro', 'Kit Bronze']

const showToast = ref(false)
const currentBuyer = ref({ name: '', city: '', state: '', kit: '', time: '' })
let toastTimer: ReturnType<typeof setTimeout> | null = null

function dismissToast() {
  showToast.value = false
  if (toastTimer) clearTimeout(toastTimer)
  scheduleNextToast()
}

function scheduleNextToast() {
  const delay = 8000 + Math.random() * 18000
  toastTimer = setTimeout(showRandomToast, delay)
}

function showRandomToast() {
  const buyer = buyers[Math.floor(Math.random() * buyers.length)]
  const kit = kits[Math.floor(Math.random() * kits.length)]
  const mins = Math.floor(Math.random() * 5)
  const time = mins === 0 ? 'há instantes' : `há ${mins} min`

  currentBuyer.value = {
    name: buyer.name,
    city: buyer.city,
    state: buyer.state,
    kit,
    time
  }
  showToast.value = true

  toastTimer = setTimeout(() => {
    showToast.value = false
    scheduleNextToast()
  }, 5000)
}

onMounted(() => {
  setTimeout(showRandomToast, 3000)
})

onUnmounted(() => {
  if (toastTimer) clearTimeout(toastTimer)
})

const steps = [
  { number: '01', text: 'Acesse o link que você receberá no email' },
  { number: '02', text: 'Baixe as figurinhas que você deseja' },
  { number: '03', text: 'Imprima as figurinhas em casa ou na gráfica mais perto' },
  { number: '04', text: 'Cole as figurinhas e complete seu álbum' }
]

const previews = [
  { img: '/images/preview-easy-print-BqVgS4p5-BqVgS4p5.jpg', title: 'Fácil de Imprimir' },
  { img: '/images/preview-selections-CBkELAn6-CBkELAn6.jpg', title: 'Todas as seleções' },
  { img: '/images/preview-legends-BunQcgt0-BunQcgt0.jpg', title: 'Figurinhas Legends inclusas' },
  { img: '/images/preview-neymar-aPq8apoG-aPq8apoG.jpg', title: 'Figurinhas do Neymar' }
]

const traditionalItems = [
  'Vem cheio de repetidas',
  'Gasta muito dinheiro',
  'Demora meses para completar',
  'Depende totalmente da sorte',
  'Frustração toda semana'
]

const solutionItems = [
  'Escolhe exatamente as faltantes',
  'Muito mais econômico',
  'Completa em poucos dias',
  'Sem depender da sorte',
  'Resultado garantido'
]

const kitBronzeItems = [
  { text: 'Todas as figurinhas do Álbum de 2026', included: true },
  { text: 'Guia ensinando Como Imprimir', included: true },
  { text: 'Álbum da Copa 2026', included: false },
  { text: 'Todas as figurinhas do Álbum da Coca Cola 2026', included: false },
  { text: 'Todas as figurinhas Legends', included: false },
  { text: 'Todas as figurinhas Holográficas', included: false },
  { text: 'Figurinhas extra Dourada', included: false },
  { text: 'Controle de figurinhas', included: false },
  { text: 'Pacote de figurinhas', included: false },
  { text: 'Calendário de data e horários dos jogos', included: false }
]

const kitOuroItems = [
  'Todas as figurinhas do Álbum de 2026',
  'Álbum da Copa 2026',
  'Todas as figurinhas do Álbum da Coca Cola 2026',
  'Todas as figurinhas Legends',
  'Todas as figurinhas Holográficas',
  'Figurinhas extra Dourada',
  'Controle de figurinhas',
  'Pacote de figurinhas',
  'Calendário de data e horários dos jogos',
  'Guia ensinando Como Imprimir'
]

const feedbackHashes = [
  'BF-289rg-BF-289rg',
  'DAFk2xE6-DAFk2xE6',
  'nXT0rkg0-nXT0rkg0',
  'tqUR_uOW-tqUR_uOW',
  'vl-lT86b-vl-lT86b',
  'C_lM6PJ3-C_lM6PJ3'
]

const faqItems = [
  {
    label: 'Qual o papel correto para imprimir?',
    content: 'Recomendamos papel adesivo fosco A4 (couché ou similar) — ele garante boa aderência no álbum e cores vibrantes. Também funciona em papel sulfite comum + cola bastão.'
  },
  {
    label: 'As figurinhas são do tamanho certo do álbum?',
    content: 'Sim! Todas as figurinhas já vêm no tamanho exato do álbum oficial da Copa 2026. Basta imprimir, recortar e colar.'
  },
  {
    label: 'Como recebo o material após o pagamento?',
    content: 'O acesso é imediato. Logo após a confirmação do pagamento, você recebe o link de download por email para baixar todas as figurinhas.'
  },
  {
    label: 'Tem figurinhas Legends e atualizações?',
    content: 'Sim! O Kit Ouro inclui Legends, Holográficas, Douradas e todas as atualizações lançadas durante a Copa, sem custo adicional.'
  }
]
</script>
