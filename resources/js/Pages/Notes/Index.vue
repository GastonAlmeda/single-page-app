<template>
    <app-layout title="Dashboard">
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Módulo de Notas
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-xl sm:rounded-lg">
                    <div class="md:grid md:grid-cols-3 md:gap-6">
                        <div class="md:col-span-1">
                            <div class="px-4 sm:px0">
                                <h3 class="text-lg text-gray-900">Listado de notas</h3>
                                <p class="text-sm text-gray-600">Toma el registro correcto y ejecuta cualquier función (ver, editar, eliminar)</p>
                            </div>
                        </div>
                        <div class="md:col-span-2 mt-5 md:mt-0">
                            <div class="shadow bg-white md:rounded-md p-4">
                                <Link 
                                    :href="route('notes.create')"
                                    class="block bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-md mb-5">
                                    Crear
                                </Link>

                                <table>
                                    <tr v-for="note in notes" :key="note.id">
                                        <td class="border px-4 py-2">
                                            {{ note.excerpt }}
                                        </td>
                                        <td class="px-4 py-2">
                                            <Link :href="route('notes.show', note.id)">
                                                Ver
                                            </Link>
                                        </td>
                                        <td class="px-4 py-2">
                                            <Link :href="route('notes.edit', note.id)">
                                                Editar
                                            </Link>
                                        </td>
                                        <td>
                                            <button 
                                                @click.prevent="destroy(note.id)"
                                                >
                                                Eliminar
                                            </button>
                                        </td>
                                    </tr>
                                </table>
                            </div>
                        </div>

                    </div>
                </div>
            </div>
        </div>
    </app-layout>
</template>

<script>
    import { defineComponent } from 'vue'
    import AppLayout from '@/Layouts/AppLayout.vue'
    import { Link } from '@inertiajs/inertia-vue3'

    export default defineComponent({
        components: {
            AppLayout,
            Link
        },
        props: {
            notes: Array,
        },
        methods: {
            destroy (id){
                if(confirm('¿Estás seguro de eliminar esta nota?')){
                    this.$inertia.delete(this.route('notes.destroy', id))
                }
            }
        }
    })
</script>
