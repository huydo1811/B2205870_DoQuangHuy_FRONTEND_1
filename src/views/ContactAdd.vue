<template>
    <div class="page">
        <h4>Thêm Liên hệ</h4>
        <ContactForm :contact="contact" @submit:contact="addContact" @delete:contact="goBack" />
    </div>
</template>

<script>
import ContactForm from "@/components/ContactForm.vue";
import ContactService from "@/services/contact.service";

export default {
    components: {
        ContactForm,
    },
    data() {
        return {
            contact: {
                name: "",
                email: "",
                address: "",
                phone: "",
                favorite: false,
            },
        };
    },
    methods: {
        async addContact(data) {
            try {
                await ContactService.create(data);
                this.$router.push({ name: "contactbook" });
            } catch (error) {
                console.log("Lỗi thêm liên hệ:", error);
            }
        },
        goBack() {
            this.$router.push({ name: "contactbook" });
        },
    },
};
</script>

<style scoped>
.page {
    max-width: 650px;
    margin: auto;
    padding: 20px;
}
</style>
