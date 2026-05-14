<template>
  <div class="ticking-counter" :class="size">
    <div class="value-wrap">
      <div class="value" :style="{ color }">
        <span class="prefix">{{ prefix }}</span>{{ display }}<span class="suffix">{{ suffix }}</span>
      </div>
    </div>
    <div class="label">{{ label }}</div>
    <div v-if="rateLabel" class="rate">{{ rateLabel }}</div>
  </div>
</template>

<script setup lang="ts">
import { computed, onBeforeUnmount, onMounted, ref } from 'vue'

const props = withDefaults(defineProps<{
  // Annual rate (units / year). Counter ticks at this rate from `start`.
  perYear: number
  // YYYY-MM-DD start; defaults to Jan 1 of current year.
  start?: string
  // Value at `start`. Defaults to 0 (so prorated from Jan 1). Use to anchor
  // a counter at a known YTD value as of `start`, then tick from there at
  // `perYear`. Useful when historical data isn't flat-rate (e.g. NJSP
  // fatalities concentrate in summer).
  startValue?: number
  label: string
  rateLabel?: string
  prefix?: string
  suffix?: string
  // Number of significant digits to display. 0 = integer.
  digits?: number
  size?: 'sm' | 'md' | 'lg'
  color?: string
}>(), {
  start: '',
  startValue: 0,
  rateLabel: '',
  prefix: '',
  suffix: '',
  digits: 0,
  size: 'md',
  color: '',
})

const startMs = computed(() => {
  const s = props.start || `${new Date().getUTCFullYear()}-01-01`
  return Date.parse(s + 'T00:00:00')
})
const ratePerSec = computed(() => props.perYear / (365.25 * 86400))

const now = ref(Date.now())
let timer: number | undefined

onMounted(() => {
  // tick every 100ms for smooth-ish updates
  timer = window.setInterval(() => { now.value = Date.now() }, 100)
})
onBeforeUnmount(() => {
  if (timer) window.clearInterval(timer)
})

const value = computed(() => {
  const elapsedSec = (now.value - startMs.value) / 1000
  return Math.max(0, props.startValue + elapsedSec * ratePerSec.value)
})

const display = computed(() => {
  const v = value.value
  const d = props.digits
  return v.toLocaleString('en-US', { maximumFractionDigits: d, minimumFractionDigits: d })
})
</script>

<style scoped>
.ticking-counter {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  font-family: var(--hccs-font-sans);
  min-width: 0;
  max-width: 100%;
}
.value-wrap {
  width: 100%;
  display: flex;
  justify-content: center;
}
.value {
  font-variant-numeric: tabular-nums;
  font-weight: 700;
  letter-spacing: -0.02em;
  line-height: 1;
  color: var(--hccs-accent);
  white-space: nowrap;
  max-width: 100%;
}
.prefix, .suffix {
  font-weight: 600;
  opacity: 0.85;
}
.label {
  margin-top: 0.35em;
  font-size: 0.85em;
  opacity: 0.9;
  line-height: 1.25;
  /* Wide enough that "Spent on car ownership in NJ" stays on one line at
   * the parent container width; if the parent is too narrow it'll still
   * wrap naturally. */
  max-width: 36ch;
}
.rate {
  margin-top: 0.2em;
  font-size: 0.62em;
  opacity: 0.55;
  font-style: italic;
}

/* Auto-fit value font size based on its container width using cqi (container
 * inline %) so very wide numbers shrink to fit, while small ones stay big. */
.ticking-counter { container-type: inline-size; }
.sm .value { font-size: clamp(1.4rem, 11cqi, 2.6rem); }
.md .value { font-size: clamp(1.6rem, 13cqi, 3.6rem); }
.lg .value { font-size: clamp(2rem, 16cqi, 5rem); }
.sm .label { font-size: 0.78rem; }
.md .label { font-size: 0.95rem; }
.lg .label { font-size: 1.1rem; }
</style>
