<script setup lang="ts">
const { isNotificationsSlideoverOpen } = useDashboard()

const stats = ref([
  {
    label: 'Total Users',
    value: '—',
    icon: 'i-lucide-users',
    color: 'primary' as const
  },
  {
    label: 'Active Today',
    value: '—',
    icon: 'i-lucide-activity',
    color: 'green' as const
  },
  {
    label: 'Habits Created',
    value: '—',
    icon: 'i-lucide-check-circle',
    color: 'blue' as const
  },
  {
    label: 'Completion Rate',
    value: '—%',
    icon: 'i-lucide-trending-up',
    color: 'orange' as const
  }
])
</script>

<template>
  <UDashboardPanel id="habito">
    <template #header>
      <UDashboardNavbar title="Habito" :ui="{ right: 'gap-3' }">
        <template #leading>
          <UDashboardSidebarCollapse />
        </template>

        <template #right>
          <UTooltip text="Notifications" :shortcuts="['N']">
            <UButton
              color="neutral"
              variant="ghost"
              square
              @click="isNotificationsSlideoverOpen = true"
            >
              <UChip color="error" inset>
                <UIcon name="i-lucide-bell" class="size-5 shrink-0" />
              </UChip>
            </UButton>
          </UTooltip>
        </template>
      </UDashboardNavbar>
    </template>

    <template #body>
      <div class="grid grid-cols-1 gap-4 sm:grid-cols-2 lg:grid-cols-4">
        <UCard v-for="stat in stats" :key="stat.label" class="overflow-hidden">
          <div class="flex items-center gap-4">
            <UIcon :name="stat.icon" class="size-8" :class="`text-${stat.color}-500`" />
            <div class="flex-1">
              <p class="text-sm text-gray-500 dark:text-gray-400">{{ stat.label }}</p>
              <p class="text-2xl font-semibold">{{ stat.value }}</p>
            </div>
          </div>
        </UCard>
      </div>

      <div class="mt-8">
        <UCard>
          <template #header>
            <h3 class="text-lg font-semibold">Analytics</h3>
          </template>
          <div class="flex items-center justify-center h-64 text-gray-500">
            <div class="text-center">
              <UIcon name="i-lucide-bar-chart-3" class="size-12 mx-auto mb-4" />
              <p>Umami analytics will be connected here</p>
            </div>
          </div>
        </UCard>
      </div>
    </template>
  </UDashboardPanel>
</template>
