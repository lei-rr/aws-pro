<script setup lang="ts">
import { ref } from 'vue'
import { Check, Copy } from '@lucide/vue'
import { Button } from '@/shared/ui/button'
import { AppTooltip } from '@/shared/ui/tooltip'
import { copyText } from '@/shared/lib/clipboard'

const props = defineProps<{ value?: string | number | null; tooltip?: string }>()

const copied = ref(false)

async function onCopy() {
  await copyText(props.value)
  copied.value = true
  setTimeout(() => {
    copied.value = false
  }, 2000)
}
</script>

<template>
  <AppTooltip :content="copied ? '已复制！' : tooltip || '复制'">
    <Button
      type="button"
      variant="ghost"
      size="icon"
      class="size-7 shrink-0 cursor-pointer text-muted-foreground hover:text-foreground"
      @click.stop="onCopy"
    >
      <Check v-if="copied" class="size-3.5 text-emerald-500" />
      <Copy v-else class="size-3.5" />
    </Button>
  </AppTooltip>
</template>
