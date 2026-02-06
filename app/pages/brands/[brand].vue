<script setup lang="ts">
import type { DropdownMenuItem } from '@nuxt/ui'

const route = useRoute()
const brandSlug = computed(() => route.params.brand as string)

const brands: Record<string, {
  name: string
  icon: string
  color: string
  description: string
  url: string
  umamiId?: string
  status: 'active' | 'development' | 'planned'
  type: 'app' | 'landing'
}> = {
  habito: {
    name: 'Habito',
    icon: 'i-lucide-check-circle',
    color: 'green',
    description: 'Task & habit tracking app for personal productivity.',
    url: 'https://habito.ar',
    umamiId: '',
    status: 'active',
    type: 'app'
  },
  quests: {
    name: 'Quests',
    icon: 'i-lucide-target',
    color: 'amber',
    description: 'Gamified goal achievement platform.',
    url: 'https://quests.ar',
    umamiId: '55fb967b-db58-4fd1-a193-6d8d57d333e8',
    status: 'active',
    type: 'app'
  },
  vegy: {
    name: 'Vegy',
    icon: 'i-lucide-leaf',
    color: 'emerald',
    description: 'Plant-based recipe discovery and meal planning.',
    url: 'https://vegy.ar',
    umamiId: '9ba99e88-51c9-4267-9727-32fb10171f80',
    status: 'development',
    type: 'app'
  },
  nouri: {
    name: 'Nouri',
    icon: 'i-lucide-apple',
    color: 'orange',
    description: 'Nutrition tracking and healthy eating companion.',
    url: 'https://nouri.ar',
    status: 'planned',
    type: 'app'
  },
  flowfocus: {
    name: 'FlowFocus',
    icon: 'i-lucide-timer',
    color: 'blue',
    description: 'Pomodoro-style focus and productivity timer.',
    url: 'https://flowfocus.ar',
    status: 'planned',
    type: 'app'
  }
}

const brand = computed(() => brands[brandSlug.value])

const statusColors: Record<string, string> = {
  active: 'success',
  development: 'warning',
  planned: 'info'
}

const items: DropdownMenuItem[][] = [[{
  label: 'Visit site',
  icon: 'i-lucide-external-link'
}, {
  label: 'View analytics',
  icon: 'i-lucide-bar-chart-3'
}], [{
  label: 'Edit settings',
  icon: 'i-lucide-settings'
}]]
</script>

<template>
  <UDashboardPanel :id="brandSlug">
    <template #header>
      <UDashboardNavbar :title="brand?.name || 'Brand'" :ui="{ right: 'gap-3' }">
        <template #leading>
          <UDashboardSidebarCollapse />
        </template>

        <template #right>
          <UBadge :color="statusColors[brand?.status || 'planned']" variant="subtle">
            {{ brand?.status || 'unknown' }}
          </UBadge>

          <UDropdownMenu :items="items">
            <UButton icon="i-lucide-more-vertical" color="neutral" variant="ghost" />
          </UDropdownMenu>
        </template>
      </UDashboardNavbar>
    </template>

    <template #body>
      <div v-if="brand" class="p-6 space-y-6">
        <!-- Header Card -->
        <UCard>
          <div class="flex items-start gap-4">
            <div class="p-3 rounded-lg bg-primary/10">
              <UIcon :name="brand.icon" class="w-8 h-8 text-primary" />
            </div>
            <div class="flex-1">
              <h2 class="text-xl font-bold">{{ brand.name }}</h2>
              <p class="text-muted mt-1">{{ brand.description }}</p>
              <div class="flex items-center gap-4 mt-3">
                <UButton
                  :to="brand.url"
                  target="_blank"
                  icon="i-lucide-external-link"
                  variant="outline"
                  size="sm"
                >
                  {{ brand.url }}
                </UButton>
                <UBadge variant="subtle">{{ brand.type }}</UBadge>
              </div>
            </div>
          </div>
        </UCard>

        <!-- Stats Grid -->
        <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
          <UCard>
            <div class="flex items-center gap-3">
              <UIcon name="i-lucide-users" class="w-5 h-5 text-muted" />
              <div>
                <p class="text-sm text-muted">Active Users</p>
                <p class="text-2xl font-bold">--</p>
              </div>
            </div>
          </UCard>
          <UCard>
            <div class="flex items-center gap-3">
              <UIcon name="i-lucide-eye" class="w-5 h-5 text-muted" />
              <div>
                <p class="text-sm text-muted">Page Views (7d)</p>
                <p class="text-2xl font-bold">--</p>
              </div>
            </div>
          </UCard>
          <UCard>
            <div class="flex items-center gap-3">
              <UIcon name="i-lucide-trending-up" class="w-5 h-5 text-muted" />
              <div>
                <p class="text-sm text-muted">Growth</p>
                <p class="text-2xl font-bold">--</p>
              </div>
            </div>
          </UCard>
        </div>

        <!-- Analytics Placeholder -->
        <UCard>
          <template #header>
            <div class="flex items-center justify-between">
              <h3 class="font-semibold">Analytics</h3>
              <UButton
                v-if="brand.umamiId"
                :to="`https://umami.codecave.ar/websites/${brand.umamiId}`"
                target="_blank"
                icon="i-lucide-external-link"
                variant="ghost"
                size="xs"
              >
                View in Umami
              </UButton>
            </div>
          </template>
          <div class="h-48 flex items-center justify-center text-muted">
            <div class="text-center">
              <UIcon name="i-lucide-bar-chart-3" class="w-12 h-12 mx-auto mb-2 opacity-50" />
              <p>Analytics integration coming soon</p>
              <p class="text-sm">Connect to Umami API for real-time stats</p>
            </div>
          </div>
        </UCard>
      </div>

      <div v-else class="p-6">
        <UCard>
          <div class="text-center py-12">
            <UIcon name="i-lucide-alert-circle" class="w-12 h-12 mx-auto mb-4 text-muted" />
            <h3 class="text-lg font-semibold">Brand not found</h3>
            <p class="text-muted mt-1">The brand "{{ brandSlug }}" doesn't exist.</p>
            <UButton to="/" class="mt-4">Go home</UButton>
          </div>
        </UCard>
      </div>
    </template>
  </UDashboardPanel>
</template>
