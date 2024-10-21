<template>
    <q-layout view="hHh lpR fFf"> <!-- QLayout ao redor do QPage -->
        <q-page class="q-pa-md">
            <q-card class="q-ma-md" style="max-width: 400px; margin: auto;">
                <q-card-section class="text-center">
                    <div class="text-h6">Login</div>
                </q-card-section>

                <q-card-section>
                    <q-form @submit="onSubmit" class="q-gutter-md">
                        <q-input v-model="form.email" filled label="Email" type="email"
                            :rules="[val => !!val || 'Email é obrigatório', val => /.+@.+\..+/.test(val) || 'Email inválido']" />
                        <q-input v-model="form.password" filled label="Senha" type="password"
                            :rules="[val => !!val || 'Senha é obrigatória']" />
                        <q-btn label="Login" type="submit" color="primary" class="full-width" />
                    </q-form>
                </q-card-section>

                <q-card-actions align="center">
                    <q-btn flat label="Esqueceu sua senha?" color="primary" @click="forgotPassword" />
                </q-card-actions>
            </q-card>
        </q-page>
    </q-layout>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import { Notify } from 'quasar'

const form = ref({
    email: '',
    password: ''
})

const router = useRouter()

const onSubmit = () => {
    if (form.value.email === 'admin@example.com' && form.value.password === '123456') {
        Notify.create({
            type: 'positive',
            message: 'Login bem-sucedido!',
        })
        router.push('/dashboard')
    } else {
        Notify.create({
            type: 'negative',
            message: 'Credenciais inválidas, tente novamente!',
        })
    }
}

const forgotPassword = () => {
    Notify.create({
        type: 'info',
        message: 'Funcionalidade de recuperação de senha ainda não implementada.',
    })
}
</script>

<style scoped>
.full-width {
    width: 100%;
}
</style>