<template>
    <div>
        <v-btn @click="dialog = true">Valid Guesses</v-btn>

        <v-dialog v-model="dialog" max-width="500">
            <v-card>
                <v-card-title>Valid Guesses</v-card-title>
                <v-card-text>
                    <v-select
                        :items="options"
                        item-value="value"
                        item-text="label"
                        label="Select"
                        dense
                        chips
                        solo-inverted
                        :menu-props="{ maxHeight: '250' }"
                    >
                    </v-select>
                </v-card-text>
                <v-card-actions>
                    <v-spacer></v-spacer>
                    <v-btn color="primary" @click="dialog = false">Close</v-btn>
                </v-card-actions>
            </v-card>
        </v-dialog>
    </div>
</template>

<script lang="ts">
    const props = defineProps<{
        validGuesses: string[]
    }>()

    let numberOfGuesses = props.validGuesses.length

    export default {
        data() {
            return {
                dialog: false,
                options: props.validGuesses
            }
        }
    }
</script>