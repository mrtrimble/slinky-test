<script setup>
import { ref } from "vue";
import gsap from "gsap";
import MyButton from "./MyButton.vue";

const props = defineProps({
  header: {
    type: String,
    default: "My Modal",
    required: true,
  },
});

const isOpen = ref(false);

const toggleModal = () => (isOpen.value = !isOpen.value);

const modalEnter = (el, done) => {
  const mediaQuery = window.matchMedia(
    "(prefers-reduced-motion: no-preference)"
  );

  if (mediaQuery.matches) {
    const innerEl = el.firstChild;

    gsap.set([el, innerEl], {
      opacity: 0,
    });

    gsap.set(innerEl, {
      y: 40,
    });

    gsap.to(el, {
      opacity: 1,
      duration: 0.15,
    });

    gsap.to(innerEl, {
      opacity: 1,
      y: 0,
      duration: 0.25,
      ease: "back.out(2)",
      delay: 0.15,
    });
  } else {
    gsap.from(el, {
      opacity: 0,
      duration: 0.125,
    });
  }
};

const modalExit = (el, done) => {
  gsap.to(el, {
    opacity: 0,
    duration: 0.125,
    onComplete: done,
  });
};
</script>

<template>
  <my-button @click="toggleModal"> Modal Trigger </my-button>

  <Teleport to="#portal">
    <transition @enter="modalEnter" @leave="modalExit">
      <div v-if="isOpen" class="modal">
        <div class="modal-inner">
          <section class="modal-inner__header">
            <h2>{{ header }}</h2>
          </section>
          <section class="modal-inner__content">
            <slot></slot>
          </section>
          <section class="modal-inner__footer">
            <my-button color="red" @click="toggleModal">
              Close Trigger
            </my-button>
          </section>
        </div>
      </div>
    </transition>
  </Teleport>
</template>