<template>
    <div class="page">
        <h4>Thêm Mới Liên Hệ</h4>
        <ContactForm :contact="contact" @submit:contact="addContact" />
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
                name: '',
                email: '',
                address: '',
                phone: '',
                favorite: false,
                _id: null
            },
        };
    },
    methods: {
        async addContact(data) {
            try {
                const { _id, ...submitData } = data;
                await ContactService.create(submitData);
                alert('Liên hệ đã được thêm thành công.');
                this.$router.push({ name: "contactbook" });
            } catch (error) {
                console.log(error);
            }
        },
    },
};
</script>