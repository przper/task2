<template>
    <div class="container">
        <div class="slot">
            <slot name="field"/>
        </div>

        <div v-if="hasError" class="error">
            <span>{{ firstError }}</span>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        errors: { type: Object, required: true },
        validationKey: { type: String, required: true }
    },
    computed: {
        hasError() {
            return this.errors[this.validationKey] != null;
        },
        firstError() {
            return this.errors[this.validationKey][0];
        }
    }
}
</script>

<style scoped>
.container {
    margin-bottom: 15px;
}
.error{
    color: red;
    font-size: x-small;
    font-style: italic;
    padding-top: 2px;
}
.slot {
    display: flex;
}

@media (max-width: 584px) {
    .slot {
        display: column;
        flex-flow: wrap;
    }
}
</style>