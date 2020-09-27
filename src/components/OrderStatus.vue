<template>
<div class="modal-card" style="width: auto">
    <header class="modal-card-head">
        <p class="modal-card-title">Change order status {{ order.order }}</p>
    </header>
    <section class="modal-card-body">
        <b-field label="status">
            <b-select placeholder="Select a status" v-model="status">
                <option v-for="option in priorities" :value="option.name" :key="option.id">
                    {{ option.name }}
                </option>
            </b-select>
        </b-field>
    </section>
    <footer class="modal-card-foot">
        <button class="button" type="button" @click="$parent.close()">
            Close
        </button>
        <button class="button is-primary" @click="editorder">Save</button>
    </footer>
</div>
</template>

<script>
export default {
    name: "orderEditModal",
    props: {
        order: {
            type: Object,
            required: true
        },
        priorities: {
            type: Array,
            required: true
        }
    },
    data() {
        return {
            title: "",
            status: ""
        };
    },
    mounted() {
        this.title = this.order.order;
        this.status = this.order.status;
    },
    methods: {
        editorder() {
            const payload = {
                id: this.order.id,
                order: this.title,
                status: this.status
            };
            this.$emit("edit-order", payload);
        }
    }
};
</script>

<style scoped></style>
