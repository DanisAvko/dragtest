<template>
    <v-container class="pa-0" fluid>
        <draggable
                class="list-group pb-13"
                v-bind="dragOptions"
                v-model="blocks"
        >
            <div
                    v-for="block in blocks"
                    :key="block.id"
                    class="column-block mt-5 mb-5 list-group-item"
            >
                <block
                        :blockData="block"
                        @deleteBlock="deleteBlock(block)"
                />
            </div>
        </draggable>
    </v-container>
</template>

<script>
    export default {
        name: "BlockList",
        props: {
            items: {
                type: Array,
                required: true
            }
        },
        components: {
            Block: () => import('./Block'),
            Draggable: () => import('vuedraggable')
        },
        computed: {
            blocks: {
                get() {
                    return this.items
                },
                set(value) {
                    this.$emit('setBlocks', value)
                },
            },
            dragOptions() {
                return {
                    animation: 200,
                    group: "blocks",
                };
            }
        },
        methods: {
            deleteBlock(block) {
                this.$emit('deleteBlock', block)
            }
        }
    }
</script>

<style scoped>
    .column-block {
        flex-flow: column nowrap;
        cursor: pointer;
    }
</style>