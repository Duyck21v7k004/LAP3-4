<template>
    <div v-if="status" class="page">
        <h4>Tạo mới<img src="" alt="" srcset=""> Liên hệ</h4>
        <ContactForm :contact="contact" @submit:contact="updateContact" />
        <p>{{ message }}</p>
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
            contact: {},
            message: "",
            status: true
        };
    },
    methods: {
        
        async updateContact(data) {
            try {
                await ContactService.create(data);
                this.message = "Liên hệ được tạo mới thành công.";
            } catch (error) {
                console.log(error);
            }
        },
        async deleteContact() {
            if (confirm("Bạn muốn xóa Liên hệ này?")) {
                try {
                    await ContactService.delete(this.contact._id);
                    this.$router.push({ name: "contactbook" });
                } catch (error) {
                    console.log(error);
                }
            }
        },
    },
    
};