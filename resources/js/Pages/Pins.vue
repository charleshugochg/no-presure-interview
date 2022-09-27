<template>
    <AppLayout title="Dashboard">
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Pins
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <h1 class="text-xl">Create your pins</h1>
                <div class="text-right">
                    <button @click="addPin" class="inline-flex justify-center rounded-md border border-transparent bg-indigo-600 py-2 px-4 text-sm font-medium text-white shadow-sm hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2">Create New</button>
                </div>
                <Create 
                    v-for="pin in pins"
                    :key="pin.id"
                    :id="pin.id"
                    :title="pin.title"
                    :description="pin.description"
                    @update:title="(msg) => pin.title = msg" 
                    @update:description="(msg) => pin.description = msg"
                    @delete="() => removePin(pin.id)"
                />
                <div v-if="pins.length > 0" class="py-6">
                    <button @click="submit" class="inline-flex justify-center rounded-md border border-transparent bg-indigo-600 py-2 px-4 text-sm font-medium text-white shadow-sm hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2">Submit</button>
                </div>
            </div>
        </div>
    </AppLayout>
</template>

<script>
import AppLayout from '@/Layouts/AppLayout.vue';
import Welcome from '@/Components/Welcome.vue';
import Create from '@/Pages/Pins/Create.vue'

let id = 0

export default {
    setup() {
        
    },
    components: {
        AppLayout,
        Welcome,
        Create
    },
    data() {
        return {
            pins: []
        }
    },
    methods: {
        addPin() {
            this.pins.push({ id: id++, title: '', description: ''})
        },
        removePin(id) {
            this.pins = this.pins.filter(p => p.id !== id)
        },
        submit() {
            window.axios.all(
                this.pins.map(pin => window.axios.post('/pins/store', pin))
            ).then(() => {
                // can not find frontend inertia redirection
                // backend redirect is inapplicable by design
                window.location.href = '/'
            }).catch(err => {
                alert('Something went wrong:', err)
            })
        }
    }
}
</script>