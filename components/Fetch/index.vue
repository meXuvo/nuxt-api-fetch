<template>
  <div>
    <div class="w-full flex justify-center items-center">
      <div class="w-4/5 bg-purple-500 text-white px-10 py-10 capitalize">
        <div class="flex justify-center mb-5">
          <h1 class="text-lg font-extrabold">user information</h1>
        </div>
        <div class="mb-5">
          <form method="post" @submit.prevent="submitForm">
            <div>
              <div>
                <label for="first_name">title</label>
              </div>
              <div>
                <input
                  id="first_name"
                  v-model="form.first_name"
                  placeholder="first name"
                  name="first_name"
                  type="text"
                  class="border border-gray-500 w-full text-blue-900"
                />
              </div>
            </div>
            <div>
              <div>
                <label for="last_name">title</label>
              </div>
              <div>
                <input
                  id="last_name"
                  v-model="form.last_name"
                  placeholder="last name"
                  name="last_name"
                  type="text"
                  class="border border-gray-500 w-full text-blue-900"
                />
              </div>
            </div>
            <div>
              <div>
                <label for="email">title</label>
              </div>
              <div>
                <input
                  id="email"
                  v-model="form.email"
                  placeholder="email"
                  name="email"
                  type="text"
                  class="border border-gray-500 w-full text-blue-900"
                />
                <span v-if="has('email')" class="text-red-500">{{
                  errors.email[0]
                }}</span>

                {{ has('email') }}
              </div>
            </div>
            <div>
              <div>
                <label for="password">title</label>
              </div>
              <div>
                <input
                  id="password"
                  v-model="form.password"
                  placeholder="password"
                  name="password"
                  type="password"
                  class="border border-gray-500 w-full text-blue-900"
                />
              </div>
              <span v-if="has('password')" class="text-red-500">{{
                errors.password[0]
              }}</span>
            </div>
            <div>
              <button
                type="submit"
                class="capitalize px-3 py-3 bg-purple-700 text-white"
              >
                submit
              </button>
            </div>
          </form>
        </div>
        <div>
          <table class="w-full">
            <thead class="border border-purple-700 bg-purple-600">
              <tr>
                <th class="w-1/3">title</th>
                <th class="w-1/3">action</th>
              </tr>
            </thead>
            <tbody class="border border-purple-700 bg-purple-400">
              <tr v-for="user in users" :key="user.id" class="text-center">
                <td>{{ user.name }}</td>
                <td class="px-2 py-2">
                  <div class="flex justify-center">
                    <div>
                      <span
                        class="px-2 py-2 capitalize bg-blue-500 text-white rounded mr-2 select-none cursor-pointer"
                        >edit</span
                      >
                    </div>
                    <div>
                      <span
                        class="px-2 py-2 capitalize bg-red-500 text-white rounded select-none cursor-pointer"
                        >delete</span
                      >
                    </div>
                  </div>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      users: [],
      form: {
        first_name: '',
        last_name: '',
        email: '',
        password: '',
      },
      errors: null,
    }
  },
  async fetch() {
    const { data } = await this.$axios.$get(
      'http://facebook-api.suvo/api/v1/users'
    )
    this.users = data
  },
  methods: {
    async submitForm() {
      await this.$axios
        .$post('http://facebook-api.suvo/api/v1/users', this.form)
        .then((res) => {
          this.$nuxt.refresh()
        })
        .catch((error) => {
          this.errors = error.response.data.errors
        })
    },
    has(filed) {
      if (this.errors !== null) {
        // in operator
        return filed in this.errors
      }
      return false
    },
  },
}
</script>

<style scoped></style>
