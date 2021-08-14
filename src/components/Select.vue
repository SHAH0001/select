<template>
    <div v-if="!disabled" class="select">
        <div @click="isOpen = !isOpen" class="select-name">
            {{ selectedItem }}
        </div>
        <transition name="fade">
            <div v-if="isOpen" class="select-menu--wrapper">
                <div 
                    v-for="(item, key) in itemsData"
                    :key="key"
                    class="select-menu"
                >
                    <p
                        class="select-menu--item"
                        @click="selectItem(item)"
                    >
                        {{ item.itemText }}
                    </p>
                </div>
            </div>
        </transition>
    </div>
    <div class="select" v-else>
        <div class="select-disabled">
            {{ selectedItem }}
        </div>
    </div>
</template>
<script>
export default {
    data() {
        return {
            isOpen: false,
            selectedItem: null
        }
    },
    props: {
        items: {
            type: Array,
            required: true,
            default: () => []
        },
        itemText: {
            type: String,
            require: false,
            default: ''
        },
        disabled: {
            type: Boolean,
            require: false,
            default: false
        },
        label: {
            type: String,
            required: false,
            default: 'Select option'
        }
    },
    computed: {
        itemsData() {
            if (this.itemText) {
                return this.items.map(i => {
                    return {
                        ...i,
                        itemText: i[this.itemText]
                    }
                })
            }
            return this.items.map(i => {
                return {
                    value: i,
                    itemText: i
                }
            })
        }
    },
    methods: {
        selectItem(item) {
            this.$emit('select', item)
            this.isOpen = false
            this.selectedItem = item.itemText
        }
    },
    mounted() {
        this.selectedItem = this.label
    }
}
</script>
<style scoped>
.select {
    width: 300px;
}
.select-name {
    padding: 12px 8px;
    cursor: pointer;
}
.select-name:hover { 
    background: #EBEBEB;
    border-radius: 4px;
    transition: all .5s;
}

.select-menu--wrapper {
    box-shadow: 0px 4px 20px rgba(0, 0, 0, 0.16);
    border-radius: 8px;
    padding: 12px 8px;
    margin-top: 10px;
}

.select-menu {
    padding: 12px 8px;
}

.select-menu:hover {
    background: #F7F7F7;
    border-radius: 4px;
    transition: all .5s;
}
.select-menu--item {
    margin: 0;
    cursor: pointer;
}

.select-disabled {
    background: #F7F7F7;
    border: 1px solid #EBEBEB;
    box-sizing: border-box;
    border-radius: 10px;
    padding: 12px 8px;
    cursor: pointer;
    color: #9C9C9C;
    font-size: 16px;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}

.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>