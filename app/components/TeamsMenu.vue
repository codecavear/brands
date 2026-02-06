<script setup lang="ts">
defineProps<{
  collapsed?: boolean
}>()

const team = {
  label: 'codeCave',
  icon: 'i-lucide-code'
}
</script>

<template>
  <UButton
    v-bind="{
      icon: team.icon,
      label: collapsed ? undefined : team.label
    }"
    color="neutral"
    variant="ghost"
    block
    :square="collapsed"
    :class="[!collapsed && 'py-2']"
    :ui="{
      leadingIcon: 'text-primary'
    }"
  />
</template>
