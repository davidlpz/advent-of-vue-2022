<template>
  <div>
    <ChristmasTree v-if="size > 1" :size="size - 1">
      <template #lights>
        <slot name="lights" />
      </template>
      <template #ornaments>
        <slot name="ornaments" />
      </template>
      <template v-if="$slots.even" #even>
        <slot name="even" />
      </template>
      <template v-if="$slots.odd" #odd>
        <slot name="odd" />
      </template>
    </ChristmasTree>

    <!-- Render the different things -->
    <div class="flex flex-row justify-center">
      <!-- Create the tree sections -->
      <div v-for="i in size" class="relative rounded-full bg-green w-16 h-16 -m-2 flex justify-center items-center">
        <!-- Add lights to each section -->
        <slot name="lights" />
        <!-- Add ornaments to each section -->
        <slot v-if="!$slots.even && !$slots.odd && i % 2 === 1" name="ornaments" />
        <slot v-if="i % 2 === 0" name="even" />
        <slot v-else name="odd" />
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
withDefaults(
  defineProps<{
    size: number
  }>(),
  {
    size: 1,
  }
)
</script>
