<template>
  <div class="min-h-screen flex flex-col bg-background text-foreground">
    <!-- Navbar -->
    <Navbar />

    <!-- Page Content -->
    <UiContainer>
      <slot />
    </UiContainer>
  </div>
</template>

<style scoped>
/* Tambahkan padding atas agar tidak ketutup navbar */
main {
  scroll-margin-top: 6rem;
}
</style>
