<script setup>
import { ref, computed } from 'vue'
import { userItems, otherItems } from '@/data.js'

import ItemList from '@/components/ItemList.vue'
import SelectedItems from '@/components/SelectedItems.vue'

const selectedUserItems = ref([])
const selectedMax = 6
const selectedItem = ref(null)

const addToSelected = (item) => {
    if (selectedUserItems.value.find(i => i.id === item.id)) return
    if (selectedUserItems.value.length >= selectedMax) {
        return alert('Max of selected items has been reached')
    }
    selectedUserItems.value.push(item)
}

const removeFromSelected = (id) => {
    selectedUserItems.value = selectedUserItems.value.filter(i => i.id !== id)
}

const selectItem = (item) => {
    selectedItem.value = item.name
}

const unSelectItem = () => {
    selectedItem.value = null
}

const filteredUserItems = computed(() => {
    return userItems.filter(item => !selectedUserItems.value.find(selected => selected.id === item.id))
})

const filteredOtherItems = computed(() => {
    return otherItems.filter(item => item.name !== selectedItem.value)
})
</script>

<template>
    <div class="items">
        <div class="items__selected">
            <SelectedItems
                :selected-items="selectedUserItems"
                :max="selectedMax"
                @remove="removeFromSelected"
            />
            <div class="items__selected-item" @click="unSelectItem">
                {{ selectedItem }}
            </div>
        </div>

        <div class="items__lists">
            <div class="items__wrapper">
                <h2>User's items</h2>
                <ItemList
                    :items="filteredUserItems"
                    @select="addToSelected"
                />
            </div>

            <div class="items__wrapper">
                <h2>Items to choose</h2>
                <ItemList
                    :items="filteredOtherItems"
                    @select="selectItem"
                />
            </div>
        </div>
    </div>
</template>

<style scoped lang="scss">
@use '@/assets/mixins.scss' as *;

.items {
    width: 920px;
    margin: 0 auto;

    &__lists {
        display: flex;
        justify-content: space-between;
        gap: 12px;
    }

    &__selected {
        display: flex;
        justify-content: space-between;
        gap: 12px;
        margin-bottom: 40px;
    }

    &__selected-item {
        @include border;
        width: 200px;
        height: 200px;
        text-align: center;
        font-size: 36px;
        text-transform: uppercase;
        display: flex;
        align-items: center;
        justify-content: center;
        cursor: pointer;
    }
}
</style>
