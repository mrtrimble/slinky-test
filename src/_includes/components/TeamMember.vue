<template>
  <article class="team-card">
    <h2>{{ teamMember.name }}</h2>
    <dl>
      <div>
        <dd><strong>Position:</strong></dd>
        <dl>{{ teamMember.position }}</dl>
      </div>
      <div>
        <dd><strong>Fun Fact:</strong></dd>
        <dl>{{ teamMember.funFact }}</dl>
      </div>
    </dl>
  </article>
</template>

<script setup>
const props = defineProps({
  teamMember: {
    type: Object,
    required: true,
  },
});
</script>