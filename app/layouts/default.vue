<script setup lang="ts">
import type { NavigationMenuItem } from '@nuxt/ui'

const route = useRoute()

const open = ref(false)

const links = [[{
  label: 'Home',
  icon: 'i-lucide-house',
  to: '/',
  onSelect: () => {
    open.value = false
  }
}, {
  label: 'Brands',
  icon: 'i-lucide-package',
  type: 'trigger',
  defaultOpen: true,
  children: [{
    label: 'Habito',
    icon: 'i-lucide-check-circle',
    to: '/brands/habito',
    onSelect: () => {
      open.value = false
    }
  }, {
    label: 'Quests',
    icon: 'i-lucide-target',
    to: '/brands/quests',
    onSelect: () => {
      open.value = false
    }
  }, {
    label: 'Vegy',
    icon: 'i-lucide-leaf',
    to: '/brands/vegy',
    onSelect: () => {
      open.value = false
    }
  }, {
    label: 'Nouri',
    icon: 'i-lucide-apple',
    to: '/brands/nouri',
    onSelect: () => {
      open.value = false
    }
  }, {
    label: 'FlowFocus',
    icon: 'i-lucide-timer',
    to: '/brands/flowfocus',
    onSelect: () => {
      open.value = false
    }
  }]
}, {
  label: 'Settings',
  to: '/settings',
  icon: 'i-lucide-settings',
  onSelect: () => {
    open.value = false
  }
}], [{
  label: 'codeCave',
  icon: 'i-lucide-code',
  to: 'https://codecave.ar',
  target: '_blank'
}, {
  label: 'GitHub',
  icon: 'i-simple-icons-github',
  to: 'https://github.com/codecavear',
  target: '_blank'
}]] satisfies NavigationMenuItem[][]

const groups = computed(() => [{
  id: 'links',
  label: 'Go to',
  items: links.flat()
}])
</script>

<template>
  <UDashboardGroup unit="rem">
    <UDashboardSidebar
      id="default"
      v-model:open="open"
      collapsible
      resizable
      class="bg-elevated/25"
      :ui="{ footer: 'lg:border-t lg:border-default' }"
    >
      <template #header="{ collapsed }">
        <TeamsMenu :collapsed="collapsed" />
      </template>

      <template #default="{ collapsed }">
        <UDashboardSearchButton :collapsed="collapsed" class="bg-transparent ring-default" />

        <UNavigationMenu
          :collapsed="collapsed"
          :items="links[0]"
          orientation="vertical"
          tooltip
          popover
        />

        <UNavigationMenu
          :collapsed="collapsed"
          :items="links[1]"
          orientation="vertical"
          tooltip
          class="mt-auto"
        />
      </template>

      <template #footer="{ collapsed }">
        <UserMenu :collapsed="collapsed" />
      </template>
    </UDashboardSidebar>

    <UDashboardSearch :groups="groups" />

    <slot />

    <NotificationsSlideover />
  </UDashboardGroup>
</template>
