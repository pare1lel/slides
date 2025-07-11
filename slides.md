---
# You can also start simply with 'default'
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://img.loliapi.com/i/pc/img324.webp
# some information about your slides (markdown enabled)
title: My Slides Collection
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
# enable download-as-pdf with clicks
download: true
---

# My Slides Collection

Dongwu Chen (PKU EECS)

<div @click="$slidev.nav.next" class="mt-12 py-1" hover:bg="white op-10">
  Press Space for next page <carbon:arrow-right />
</div>

<div class="absolute bottom-2 left-2 text-xs">
  {{ new Date().toLocaleDateString() }}
</div>

<div class="abs-br m-6 text-xl">
  <a href="https://github.com/pare1lel/slides" target="_blank" class="slidev-icon-btn">
    <carbon:logo-github />
  </a>
</div>

---

# Table of Contents

1. [Linear Algebra in OI](https://pare1lel.github.io/slides/la/)

<div class="absolute top-2 right-2 text-xs">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<style> h1 { color: #2B90B6; } </style>