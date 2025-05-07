<template>
    <div class="item-list">
        <div
            v-for="item in items"
            :key="item.id"
            class="item-list__item"
            @click="emit('select', item)"
        >
            {{ item.name }}
        </div>
    </div>
</template>

<script setup>
defineProps({
    items: Array
})
const emit = defineEmits(['select'])
</script>

<style scoped lang="scss">
@use '@/assets/mixins.scss' as *;

.item-list {
    @include border;
    @include grid-layout(4);
    gap: 16px;
    width: 410px;
    min-height: 50vh;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    align-content: start;

    &__item {
        @include item-box;
    }
}
</style>
