<template>
  <div class="slidev-layout default">
    <img src="/logo.png" alt="DB1" class="deck-logo-corner" />
    <slot />
  </div>
  <footer class="absolute bottom-5 left-0 right-7 text-right"><SlideCurrentNo/>/<SlidesTotal/></footer>
</template>
