<template>
    <div class="selected-items">
        <div class="selected-items__list">
            <div
                v-for="item in selectedItems"
                :key="item.id"
                class="selected-items__item"
                @click="emit('remove', item.id)"
            >
                {{ item.name }}
            </div>
        </div>
        <span>selected: {{ selectedItems.length }} / {{ max }}</span>
    </div>
</template>

<script setup>
defineProps({
    selectedItems: Array,
    max: Number
})
const emit = defineEmits(['remove'])
</script>

<style scoped lang="scss">
@use '@/assets/mixins.scss' as *;

.selected-items {
    @include border;
    width: 200px;
    height: 200px;
    margin-bottom: 40px;
    display: flex;
    justify-content: space-between;
    flex-direction: column;

    &__list {
        @include grid-layout(2);
        gap: 8px;
        display: grid;
        grid-template-columns: repeat(2, 1fr);
        align-content: start;
    }

    &__item {
        @include item-box;
    }
}
</style>
