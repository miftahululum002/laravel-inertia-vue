<script setup>
import AuthenticatedLayout from "@/Layouts/AuthenticatedLayout.vue";
import TextInput from "@/Components/TextInput.vue";
import PrimaryButton from "@/Components/PrimaryButton.vue";
import InputLabel from "@/Components/InputLabel.vue";
import InputError from "@/Components/InputError.vue";
import { Link, Head, useForm } from "@inertiajs/vue3";

const props = defineProps({
    blogs: {
        type: Object,
        default: () => ({}),
    },
});

const form = useForm({
    title: "",
    content: "",
});

const submit = () => {
    form.post(route("blogs.store"));
};
</script>

<template>
    <Head title="Blog Create" />

    <AuthenticatedLayout>
        <template #header>
            <h2 class="text-xl font-semibold leading-tight text-gray-800">
                Form Tambah Blog
            </h2>
        </template>

        <div class="py-12">
            <div class="mx-auto max-w-7xl">
                <div class="overflow-hidden bg-white shadow-sm sm:rounded-lg">
                    <div class="p-6 bg-white border-b border-gray-200">
                        <form @submit.prevent="submit">
                            <div>
                                <InputLabel for="title" value="Title" />
                                <TextInput
                                    id="title"
                                    type="text"
                                    class="mt-1 block w-full"
                                    v-model="form.title"
                                    required
                                    autofocus
                                    placeholder="Title"
                                    autocomplete="username"
                                />
                                <InputError
                                    class="mt-2"
                                    :message="form.errors.title"
                                />
                            </div>

                            <div class="my-6">
                                <label
                                    for="content"
                                    class="block mb-2 text-sm font-medium text-gray-900"
                                    >Content</label
                                >
                                <textarea
                                    type="text"
                                    v-model="form.content"
                                    name="content"
                                    id=""
                                    placeholder="Content"
                                    class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
                                ></textarea>

                                <div
                                    v-if="form.errors.content"
                                    class="text-sm text-red-600"
                                >
                                    {{ form.errors.content }}
                                </div>
                            </div>
                            <div class="flex">
                                <PrimaryButton
                                    type="submit"
                                    class="rounded-none"
                                    :class="{ 'opacity-25': form.processing }"
                                    :disabled="form.processing"
                                >
                                    Simpan
                                </PrimaryButton>
                                <Link
                                    :href="route('blogs.index')"
                                    class="px-4 py-2 bg-slate-300 text-white rounded-none"
                                >
                                    Kembali
                                </Link>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>
