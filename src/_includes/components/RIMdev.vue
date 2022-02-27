<template>
  <section class="team-grid">
    <TeamMember
      v-for="teamMember in sortedTeam"
      :key="teamMember.name"
      :team-member="teamMember"
    />
  </section>
</template>

<script setup>
import { computed } from "@vue/runtime-core";
import TeamMember from "./TeamMember.vue";

const props = defineProps({
  rimdev: {
    type: Object,
    required: true,
  },
});

const sortedTeam = computed(() =>
  props.rimdev.frontend.sort((a, b) =>
    a.name.localeCompare(b.name, "en", { numeric: true })
  )
);
</script>