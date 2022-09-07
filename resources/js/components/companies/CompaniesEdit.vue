<template>

    <form class="w-full max-w-sm" @submit.prevent="saveCompany">
        <div class="md:flex md:items-center mb-6">
          <div class="md:w-1/3">
            <label class="block text-gray-500 font-bold md:text-right mb-1 md:mb-0 pr-4" for="inline-full-name">
              Name
            </label>
          </div>
          <div class="md:w-2/3">
            <input
                class="bg-gray-200 appearance-none border-2 border-gray-200 rounded w-full py-2 px-4 text-gray-700 leading-tight focus:outline-none focus:bg-white focus:border-purple-500"
                type="text"
                v-model="company.name">
                <span class="mt-2 mb-6 text-sm text-red-600" v-if="errors.name !== ''">
                    {{ errors.name }}
                </span>
          </div>
        </div>
        <div class="md:flex md:items-center mb-6">
          <div class="md:w-1/3">
            <label class="block text-gray-500 font-bold md:text-right mb-1 md:mb-0 pr-4" for="inline-password">
              Email
            </label>
          </div>
          <div class="md:w-2/3">
            <input
                class="bg-gray-200 appearance-none border-2 border-gray-200 rounded w-full py-2 px-4 text-gray-700 leading-tight focus:outline-none focus:bg-white focus:border-purple-500"
                type="email"
                v-model="company.email">
                <span class="mt-2 mb-6 text-sm text-red-600" v-if="errors.email !== ''">
                    {{ errors.email }}
                </span>
          </div>
        </div>
        <div class="md:flex md:items-center mb-6">
            <div class="md:w-1/3">
              <label class="block text-gray-500 font-bold md:text-right mb-1 md:mb-0 pr-4" for="inline-full-name">
                Address
              </label>
            </div>
            <div class="md:w-2/3">
              <input
                class="bg-gray-200 appearance-none border-2 border-gray-200 rounded w-full py-2 px-4 text-gray-700 leading-tight focus:outline-none focus:bg-white focus:border-purple-500"
                type="text"
                v-model="company.address">
                <span class="mt-2 mb-6 text-sm text-red-600" v-if="errors.address !== ''">
                    {{ errors.address }}
                </span>
            </div>
        </div>
        <div class="md:flex md:items-center mb-6">
            <div class="md:w-1/3">
              <label class="block text-gray-500 font-bold md:text-right mb-1 md:mb-0 pr-4" for="inline-full-name">
                Website
              </label>
            </div>
            <div class="md:w-2/3">
              <input
                class="bg-gray-200 appearance-none border-2 border-gray-200 rounded w-full py-2 px-4 text-gray-700 leading-tight focus:outline-none focus:bg-white focus:border-purple-500"
                type="text"
                v-model="company.website">
                <span class="mt-2 mb-6 text-sm text-red-600" v-if="errors.website !== ''">
                    {{ errors.website }}
                </span>
            </div>
        </div>
        <div class="md:flex md:items-center">
          <div class="md:w-1/3"></div>
          <div class="md:w-2/3">
            <button class="shadow bg-purple-200 hover:bg-purple-300 focus:shadow-outline focus:outline-none text-white font-bold py-2 px-4 rounded" type="submit">
              Create
            </button>
          </div>
        </div>
      </form>
</template>

<script>
import { onMounted, reactive } from 'vue'
import useCompanies from '../../composables/companies'

export default {
    props: {
        id: {
            required: true,
            type: String
        }
    },

    setup(props) {

        const { errors, company, getCompany, updateCompany } = useCompanies()

        onMounted(getCompany(props.id))

        const saveCompany = async () => {
            await updateCompany(props.id)
        }
        return {
            company,
            errors,
            saveCompany
        }
    }


}
</script>
