<template>
  <div class="slidev-layout default">
    <slot />
    <img src="/logo.png" alt="DB1" class="deck-logo-corner" />
  </div>
  <footer class="absolute bottom-5 left-0 right-7 text-right footer"><SlideCurrentNo/>/<SlidesTotal/></footer>
</template>
