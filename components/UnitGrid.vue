<!-- Unit chart ("isotype"): one mark per N people, packed to fill the parent
     box. All rows that share a box size become directly comparable by colored-
     area, so the *composition* (which road users) reads across severities even
     as the absolute counts span ~70x. Canvas, so 10k+ marks stay cheap. -->
<template>
  <canvas ref="cv" class="unit-grid" />
</template>

<script setup lang="ts">
import { onBeforeUnmount, onMounted, ref, watch } from 'vue'

const props = withDefaults(defineProps<{
  // people per type, e.g. { driver: 301, passenger: 92, ... }
  counts: Record<string, number>
  colors: Record<string, string>
  // draw order; defaults to Object.keys(counts)
  types?: string[]
  // null/empty = all types; otherwise only these are drawn
  selected?: string[] | null
  // cell aspect ratio (w/h). >1 = landscape marks.
  ar?: number
  // gap between marks as a fraction of cell size.
  gap?: number
  // corner radius as a fraction of the mark's short side.
  radius?: number
}>(), {
  selected: null,
  ar: 1.4,
  gap: 0.22,
  radius: 0.35,
})

const cv = ref<HTMLCanvasElement>()
let ro: ResizeObserver | undefined
let io: IntersectionObserver | undefined
let raf = 0
let pending = 0

function activeTypes() {
  const ts = props.types ?? Object.keys(props.counts)
  if (!props.selected || props.selected.length === 0) return ts
  return ts.filter(t => props.selected!.includes(t))
}

function draw() {
  const canvas = cv.value
  if (!canvas) return
  const parent = canvas.parentElement
  if (!parent) return
  const W = parent.clientWidth
  const H = parent.clientHeight
  if (W < 2 || H < 2) {
    // Box isn't laid out yet — slidev mounts the slide (cold load / preload)
    // before sizing it. Retry next frame until it has size, so the canvas
    // never gets stuck blank waiting on a ResizeObserver tick that may lag.
    if (pending++ < 180) raf = requestAnimationFrame(() => { raf = 0; draw() })
    return
  }
  pending = 0

  const dpr = window.devicePixelRatio || 1
  canvas.width = Math.round(W * dpr)
  canvas.height = Math.round(H * dpr)
  canvas.style.width = `${W}px`
  canvas.style.height = `${H}px`
  const ctx = canvas.getContext('2d')!
  ctx.setTransform(dpr, 0, 0, dpr, 0, 0)
  ctx.clearRect(0, 0, W, H)

  const perType = activeTypes()
    .map(t => ({ t, n: Math.round(props.counts[t] || 0) }))
    .filter(x => x.n > 0)
  const N = perType.reduce((s, x) => s + x.n, 0)
  if (N === 0) return

  // Pick a column count so N cells of aspect `ar` tile the W×H box. From
  // cols/rows = (W/cellW)/(H/cellH) with cellW/cellH = ar: cols = sqrt(N·W·ar/H).
  let cols = Math.max(1, Math.round(Math.sqrt((N * W * props.ar) / H)))
  cols = Math.min(cols, N)
  const rows = Math.ceil(N / cols)
  const cellW = W / cols
  const cellH = H / rows
  const mw = Math.max(0.5, cellW * (1 - props.gap))
  const mh = Math.max(0.5, cellH * (1 - props.gap))
  const offX = (cellW - mw) / 2
  const offY = (cellH - mh) / 2
  const r = Math.min(mw, mh) * props.radius

  // Center the (possibly short) last row's block vertically within the box.
  const usedH = rows * cellH
  const padY = (H - usedH) / 2

  let idx = 0
  const rounded = mw > 3 && mh > 3 && r > 0.5
  for (const { t, n } of perType) {
    ctx.fillStyle = props.colors[t]
    for (let k = 0; k < n; k++, idx++) {
      const c = idx % cols
      const row = (idx - c) / cols
      const x = c * cellW + offX
      const y = padY + row * cellH + offY
      if (rounded) {
        ctx.beginPath()
        ctx.roundRect(x, y, mw, mh, r)
        ctx.fill()
      }
      else {
        ctx.fillRect(x, y, mw, mh)
      }
    }
  }
}

function schedule() {
  if (raf) return
  raf = requestAnimationFrame(() => { raf = 0; draw() })
}

onMounted(() => {
  const parent = cv.value?.parentElement
  ro = new ResizeObserver(schedule)
  // Redraw when the slide is revealed (slidev toggles slide visibility rather
  // than remounting, so a slide drawn while offscreen needs a re-trigger).
  io = new IntersectionObserver(schedule)
  if (parent) {
    ro.observe(parent)
    io.observe(parent)
  }
  schedule()
})
onBeforeUnmount(() => {
  ro?.disconnect()
  io?.disconnect()
  if (raf) cancelAnimationFrame(raf)
})
watch(() => [props.counts, props.selected, props.ar, props.gap], schedule, { deep: true })
</script>

<style scoped>
.unit-grid {
  display: block;
  width: 100%;
  height: 100%;
}
</style>
