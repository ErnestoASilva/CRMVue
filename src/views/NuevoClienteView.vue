<script setup>
    import { useRouter } from 'vue-router'
    import { FormKit } from '@formkit/vue'
    import ClienteService from '@/services/ClienteService';
    import RouterLink from '../components/UI/RouterLink.vue'
    import Heading from '@/components/UI/Heading.vue';

    const router = useRouter();

    defineProps({
        titulo: {
            type: String  
        }
    })


    const handleSubmit = (data) => {
        data.estado = 1;
        ClienteService.agregarCliente(data)
            .then(respueta => {
                console.log(respueta);
                router.push({name: 'inicio'});
            })
            .catch(error => console.log(error))
    }

</script>

<template>
    <div>
        <div class="flex justify-end">
            <RouterLink to="inicio">
                Volver
            </RouterLink>
        </div>

        <Heading>{{ titulo }}</Heading>

        <div class="mx-auto mt-10 bg-white">
            <div class="mx-auto md:w-2/3 py-20 px-6">
                <FormKit
                    type="form"
                    :actions="true"
                    submit-label="Agregar Cliente"
                    incomplete-message="No se pudo enviar, revisa los mensajes"
                    @submit="handleSubmit"
                >
                    <FormKit
                        type="text"
                        label="Nombre"
                        name="nombre"
                        placeholder="Nombre de Cliente"
                        validation="required"
                        :validation-messages="{required: 'El Nombre del Cliente es Obligatorio'}"
                    />

                    <FormKit
                        type="text"
                        label="Apellido"
                        name="apellido"
                        placeholder="Apellido de Cliente"
                        validation="required"
                        :validation-messages="{required: 'El Apellido del Cliente es Obligatorio'}"
                    />

                    <FormKit
                        type="email"
                        label="Email"
                        name="email"
                        placeholder="Email de Cliente"
                        validation="required|email"
                        :validation-messages="{required: 'El email del Cliente es Obligatorio',
                         email: 'Ingresa un Formato de Email Correcto'   }"
                    />

                    <FormKit
                        type="text"
                        label="Telefono"
                        name="telefono"
                        placeholder="Telefono: XXX-XXX-XXXX"
                        validation="?matches:/^[0-9]{3}-[0-9]{3}-[0-9]{4}$/"
                        :validation-messages="{matches: 'El formato no es válido'}"
                    />

                    <FormKit
                        type="text"
                        label="Empresa"
                        name="empresa"
                        placeholder="Empresa de Cliente"
                    />

                    <FormKit
                        type="text"
                        label="Puesto"
                        name="puesto"
                        placeholder="Puesto de Cliente"
                    />

                </FormKit>
            </div>
        </div>

    </div>
</template>

<style>
    .formkit-wrapper{
        max-width: 100%;
            }
</style>