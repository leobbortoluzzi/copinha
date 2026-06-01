<script setup>
useHead({
  meta: [
    { name: 'viewport', content: 'width=device-width, initial-scale=1' }
  ],
  link: [
    { rel: 'icon', href: '/favicon.ico' }
  ],
  htmlAttrs: {
    lang: 'pt-BR'
  }
})

const title = 'Figurinhas Copa 2026 Imprimíveis · Complete seu álbum'
const description = 'Baixe e imprima todas as figurinhas do álbum da Copa 2026: seleções, Legends, holográficas e mais. Acesso imediato.'
const ogImage = 'https://pub-bb2e103a32db4e198524a2e9ed8f35b4.r2.dev/f18d5816-68fa-4ba5-9bae-7ba371f01321/id-preview-d205a906--97a66f37-815b-41fc-b1fc-7edf900480a3.lovable.app-1778982087095.png'

useSeoMeta({
  title,
  description,
  ogTitle: title,
  ogDescription: description,
  ogImage,
  ogType: 'website',
  twitterCard: 'summary_large_image',
  twitterTitle: title,
  twitterDescription: description,
  twitterImage: ogImage
})
</script>

<template>
  <UApp>
    <UMain>
      <NuxtPage />
    </UMain>

    <UFooter>
      <template #left>
        <p class="text-sm text-muted">
          Figurinhas Copa 2026 Imprimíveis · © {{ new Date().getFullYear() }}
        </p>
      </template>

      <template #right>
        <UButton
          to="https://wa.me/5598999850510"
          target="_blank"
          icon="i-lucide-message-circle"
          color="neutral"
          variant="ghost"
          aria-label="WhatsApp"
        />
      </template>
    </UFooter>
  </UApp>
</template>
