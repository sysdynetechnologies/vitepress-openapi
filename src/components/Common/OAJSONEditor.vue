<script setup>
import JsonEditorVue from 'json-editor-vue'
import { computed } from 'vue'
import { useTheme } from '../../composables/useTheme'

const props = defineProps({
  modelValue: {
    type: Object,
    required: true,
  },
  options: {
    type: Object,
    default: () => ({}),
  },
})

const emit = defineEmits(['update:modelValue'])

const value = computed({
  get: () => props.modelValue,
  set: val => emit('update:modelValue', JSON.parse(val)),
})

const themeConfig = useTheme()

const isDark = themeConfig.isDark
</script>

<template>
  <JsonEditorVue
    v-model="value"
    :main-menu-bar="themeConfig.getPlaygroundJsonEditorMainMenuBar()"
    :navigation-bar="themeConfig.getPlaygroundJsonEditorNavigationBar()"
    :mode="themeConfig.getPlaygroundJsonEditorMode()"
    :status-bar="themeConfig.getPlaygroundJsonEditorStatusBar()"
    class="oa-jse"
    :class="{
      'oa-jse-theme-dark': isDark,
      'oa-jse-theme-light': !isDark,
    }"
  />
</template>
