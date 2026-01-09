<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from "vue";

const navLinks = [
  { href: "#hero", label: "Home" },
  { href: "#problems", label: "Problems" },
  { href: "#services", label: "Services" },
  { href: "#process", label: "Process" },
];

const isScrolled = ref(false);
const isMobileMenuOpen = ref(false);

onMounted(() => {
  const handleScroll = () => {
    isScrolled.value = window.scrollY > 50;
  };
  window.addEventListener("scroll", handleScroll);

  onBeforeUnmount(() => {
    window.removeEventListener("scroll", handleScroll);
  });
});

const handleNavClick = (href: string) => {
  isMobileMenuOpen.value = false;
  const element = document.querySelector(href);
  element?.scrollIntoView({ behavior: "smooth" });
};
</script>

<template>
  <nav
    :class="[
      'fixed top-0 left-0 right-0 z-50 transition-all duration-300',
      isScrolled
        ? 'bg-background/80 backdrop-blur-xl border-b border-border/50'
        : 'bg-transparent'
    ]"
  >
    <UiContainer>
      <div class="flex items-center justify-between h-16 md:h-20">
        <!-- Logo -->
        <a
          class="flex items-center gap-2 text-foreground text-sm"
        >
          <Icon name="lucide:rocket" class="size-5" />
          <span class="text-sm font-bold text-foreground">Starter App</span>
        </a>

        <!-- Desktop Menu -->
        <div class="hidden lg:flex items-center gap-8">
          <a
            v-for="link in navLinks"
            :key="link.href"
            :href="link.href"
            class="text-muted-foreground hover:text-foreground transition-colors duration-200 text-sm font-medium"
            @click.prevent="handleNavClick(link.href)"
          >
            {{ link.label }}
          </a>
        </div>

        <!-- CTA Desktop -->
        <div class="hidden lg:block">
          <UiButton
            size="sm"
          >
            Get a Quote
          </UiButton>
        </div>

        <!-- Mobile Menu Button -->
         <UiButton
          class="lg:hidden p-2"
          @click="isMobileMenuOpen = !isMobileMenuOpen"
        >
          <Icon :name="isMobileMenuOpen ? 'lucide:x' : 'lucide:menu'" class="size-6" />
        </UiButton>
      </div>

      <!-- Mobile Menu -->
      <div
        v-if="isMobileMenuOpen"
        class="lg:hidden bg-card/95 backdrop-blur-xl border-t border-border/50 animate-fade-up"
      >
        <div class="py-4 space-y-2">
          <a
            v-for="link in navLinks"
            :key="link.href"
            :href="link.href"
            class="block px-4 py-3 text-muted-foreground hover:text-foreground hover:bg-secondary/50 transition-colors duration-200"
            @click.prevent="handleNavClick(link.href)"
          >
            {{ link.label }}
          </a>
        </div>
      </div>
    </UiContainer>
  </nav>
</template>
