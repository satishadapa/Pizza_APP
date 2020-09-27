<template>
<div>
    <section class="section">
        <div class="container">

            <b-table :data="orders">
                <template slot-scope="orders">
                    <b-table-column field="id" label="ID" width="40">
                        {{ orders.row.id }}
                    </b-table-column>

                    <b-table-column field="customerName" label="customer Name">
                        {{ orders.row.customerName }}
                    </b-table-column>
                    <b-table-column field="NumberofItems" label="Number of Items">
                        {{ orders.row.NumberofItems }}
                    </b-table-column>
                    <b-table-column field="order" label="Order Item">
                        {{ orders.row.order }}
                    </b-table-column>

                    <b-table-column field="status" label="status">
                        {{ orders.row.status }}
                    </b-table-column>

                    <b-table-column label="Change status">
                        <b-button type="is-text" icon-left="settings-outline" @click="openEditModal(orders.row)"></b-button>
                    </b-table-column>

                </template>
            </b-table>
        </div>
    </section>

    <b-modal :active.sync="isEditModalActive" has-modal-card>
        <OrderStatus :order="selectedorder" :priorities="priorities" @edit-order="onEditorder"></OrderStatus>
    </b-modal>
</div>
</template>

<script>
import OrderStatus from "@/components/OrderStatus";
export default {
    name: "orderList",
    components: {
        OrderStatus
    },
    data() {
        return {
            orderListData: [{
                    id: 1,
                    order: "Double Cheese Margherita",
                    status: "Order Received",
                    customerName: "Jhon",
                    NumberofItems: "55"

                },
                {
                    id: 2,
                    order: "Farm House",
                    status: "Preparing",
                    customerName: "Peter",
                    NumberofItems: "55"
                },
                {
                    id: 3,
                    order: "Peppy Paneer",
                    status: "Order Received",
                    customerName: "clerk",
                    NumberofItems: "55"
                },
                {
                    id: 4,
                    order: "Deluxe Veggie",
                    status: "Preparing",
                    customerName: "bush imalual",
                    NumberofItems: "55"
                },
                {
                    id: 5,
                    order: "Indi Tandoori Paneer",
                    status: "Order Received",
                    customerName: "avenger",
                    NumberofItems: "55"
                }
            ],
            orders: [],
            priorities: [{
                    id: 1,
                    name: "Order Received"
                },
                {
                    id: 2,
                    name: "Preparing"
                },
                {
                    id: 3,
                    name: "Ready to serve"
                }
            ],
            isEditModalActive: false,
            selectedorder: {},
            isAddModalActive: false
        };
    },
    mounted() {
        if (localStorage.getItem("orders")) {
            this.orders = JSON.parse(localStorage.getItem("orders"));
        } else {
            this.orders = this.orderListData;
        }
    },
    methods: {
        openEditModal(order) {
            this.selectedorder = order;
            this.isEditModalActive = true;
        },

        onEditorder(item) {
            const order = this.findorder(item);
            // Apply the updated values
            order.order = item.order;
            order.status = item.status;
            // save the updated array in localstorage
            this.saveLocalStorageorders();
            // close the modal
            this.isEditModalActive = false;
        },

        findorder(item) {
            return this.orders.find(order => order.id === item.id);
        },
        saveLocalStorageorders() {
            localStorage.setItem("orders", JSON.stringify(this.orders));
            this.orders = JSON.parse(localStorage.getItem("orders"));
        }
    }
};
</script>

<style lang="scss" scoped></style>
