<template>
    <h1>Form with validation</h1>
    
    <form @submit.prevent="submit" class="form">
        <input-group :errors="errors" :validationKey="'textfield'">
            <template #field>
                <label class="label">Input text</label>
                <input v-model="textfield" class="input">
            </template>
        </input-group>

        <input-group :errors="errors" :validationKey="'password'">
            <template #field>
                <label class="label">Input password</label>
                <input v-model="password" type="password" class="input">
            </template>
        </input-group>

        <input-group :errors="errors" :validationKey="'areafield'">
            <template #field>
                <label class="label">Long text field</label>
                <textarea v-model="areafield" class="textarea"></textarea>
            </template>
        </input-group>

        <button type="submit">Submit</button>
    </form>
</template>

<script>
import InputGroup from './InputGroup.vue';

export default {
    components: { InputGroup },
    data() {
        return {
            textfield: "",
            password: "",
            areafield: "",
            errors: {}
        };
    },
    methods: {
        async submit() {
            const { data } = {
                textfield: this.textfield,
                password: this.password,
                areafield: this.areafield,
            };

            await fetch("https://przper.free.beeceptor.com/", {
                headers: { 'Content-Type': 'application/json' },
                method: "POST", 
                body: JSON.stringify(data)
            })
            .then(response => response.json())
            .then(data => {
                console.log(data.message)

                if (data.errors) {
                    this.errors = data.errors;
                }
            })
            .catch(error => {
                console.log("Errors: ", error)
            });
        },
    },
}
</script>

<style scoped>
.form {
    padding: 5px;
    padding-top: 15px;
    background: white;
    color: black;
    border-radius: 5px;
}
.input {
    width: 66.67%;
    height: 30px;
    border-radius: 5px;
    outline: none;
    border: 1px solid gray;
}
.label {
    width: 33.33%;
}
.textarea {
    width: 66.77%;
    height: 120px;
    border-radius: 5px;
    outline: none;
    border: 1px solid gray;
}
h1 {
    margin-bottom: 12px;
    text-align: center;
}

@media (max-width: 584px) {
    .input, .label, .textarea {
        width: 100%;
    }
}
</style>