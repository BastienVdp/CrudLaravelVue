<template>
    <div class="flex flex-col">
        <router-link :to="{ name: 'companies.create' }" class="text-sm font-medium">Create company</router-link>
        <div class="overflow-x-auto w-full">
            <div class="py-2 inline-block min-w-full">
                <div class="overflow-hidden">
                <table class="min-w-full">
                    <thead class="bg-white border-b">
                        <tr>
                            <th scope="col" class="text-sm font-medium text-gray-900 px-6 py-4 text-left">
                                #
                            </th>
                            <th scope="col" class="text-sm font-medium text-gray-900 px-6 py-4 text-left">
                                Name
                            </th>
                            <th scope="col" class="text-sm font-medium text-gray-900 px-6 py-4 text-left">
                                Email
                            </th>
                            <th scope="col" class="text-sm font-medium text-gray-900 px-6 py-4 text-left">
                                Address
                            </th>
                            <th scope="col" class="text-sm font-medium text-gray-900 px-6 py-4 text-left">
                                Website
                            </th>
                        </tr>
                    </thead>
                    <tbody>
                        <template v-for="item in companies" :key="item.id">
                        <tr class="bg-white border-b transition duration-300 ease-in-out hover:bg-gray-100">
                            <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900">
                                {{ item.id }}
                            </td>
                            <td class="text-sm text-gray-900 font-light px-6 py-4 whitespace-nowrap">
                                {{ item.name }}
                            </td>
                            <td class="text-sm text-gray-900 font-light px-6 py-4 whitespace-nowrap">
                                {{ item.address }}
                            </td>
                            <td class="text-sm text-gray-900 font-light px-6 py-4 whitespace-nowrap">
                                {{ item.website }}
                            </td>
                            <td class="text-sm text-gray-900 font-light px-6 py-4 whitespace-nowrap">
                                <router-link :to="{ name: 'companies.edit', params: { id: item.id} } ">
                                    Edit
                                </router-link>
                                <button @click="deleteCompany(item.id)">Delete</button>
                            </td>
                        </tr>
                        </template>
                    </tbody>
                </table>
            </div>
          </div>
        </div>
      </div>
</template>

<script>
    import useCompanies from '../../composables/companies'
    import { onMounted } from 'vue'

    export default {
        setup() {
            const { companies, getCompanies, destroyCompany } = useCompanies()

            onMounted(getCompanies)

            const deleteCompany = async (id) => {
                if(!window.confirm('Delete ?')) {
                    return
                }

                await destroyCompany(id)
                await getCompanies()
            }

            return {
                companies,
                deleteCompany
            }
        }
    }
</script>
