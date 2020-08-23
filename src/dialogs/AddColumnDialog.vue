<template>
    <v-dialog v-model="show" persistent width="400">
        <v-card>
            <v-card-title>
                Карточка столбца
            </v-card-title>
            <v-card-text>
                <v-text-field
                        label="Название"
                        v-model="title"
                        counter
                        maxlength="30"
                />
            </v-card-text>
            <v-card-actions>
                <v-spacer/>
                <v-btn
                        @click="addColumn()"
                        class="success"
                        :disabled="!title"
                >
                    Добавить
                </v-btn>
                <v-btn
                        class="error"
                        @click="closeDialog()"
                >
                    Отмена
                </v-btn>
            </v-card-actions>
        </v-card>
    </v-dialog>
</template>

<script>
    export default {
        name: "AddBlockDialog",
        props: {
            value: {
                type: Boolean,
            }
        },
        data: () => ({
            title: ''
        }),
        computed: {
            show: {
                get() {
                    return this.value
                },
                set(value) {
                    this.$emit('close', value)
                },
            },
        },
        methods: {
            addColumn() {
                this.$emit('addColumn', {
                    id: Date.now(),
                    title: this.title,
                    blocks: []
                })
                this.closeDialog()
            },
            closeDialog() {
                this.show = false
                this.title = ''
            }
        }
    }
</script>