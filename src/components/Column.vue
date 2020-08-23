<template>
    <v-container>
        <div class="pl-3 title">
            <div class="column-title d-inline-block">
                {{columnData.title}}
            </div>
            <v-btn
                    icon
                    title="Удалить"
                    class="float-right mr-1"
                    @click="deleteColumn()"
            >
                <v-icon>
                    mdi-close
                </v-icon>
            </v-btn>
        </div>
        <div class="mt-2 pl-3 pr-3">
            <v-btn
                    color="primary"
                    class="column-btn"
                    title="Добавить блок"
                    @click="openAddBlockDialog()"
            >
                <v-icon>
                    mdi-plus
                </v-icon>
            </v-btn>
        </div>
        <div class="container">
            <block-list
                    :items="blocks"
                    @setBlocks="setBlocks"
                    @deleteBlock="deleteBlock"
            />
        </div>

        <add-block-dialog
                :value="showAddBlockDialog"
                @close="value => showAddBlockDialog = value"
                @addBlock="addBlock"
        />
    </v-container>
</template>

<script>
    export default {
        name: "Column",
        props: {
            columnData: {
                type: Object,
                required: true
            }
        },
        components: {
            BlockList: () => import('./BlockList'),
            AddBlockDialog: () => import('../dialogs/AddBlockDialog')
        },
        data: () => ({
            showAddBlockDialog: false
        }),
        computed: {
            blocks() {
                return this.columnData.blocks ? this.columnData.blocks : []
            },
        },
        methods: {
            openAddBlockDialog() {
                this.showAddBlockDialog = true
            },
            setBlocks(payload) {
               this.columnData.blocks = payload
            },
            addBlock(payload) {
                this.columnData.blocks.unshift(payload)
            },
            deleteBlock(block) {
                let delIndex = this.columnData.blocks.findIndex(item => item.id === block.id)
                this.columnData.blocks.splice(delIndex, 1)
            },
            deleteColumn() {
                this.$emit('deleteColumn')
            }
        }
    }
</script>

<style scoped>
    .column-btn {
        width: 100%;
    }

    .column-title {
        word-break: break-all;
        max-width: 70%;
    }
</style>