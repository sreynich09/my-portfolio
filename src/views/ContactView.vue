<script>
export default {
  name: 'ContactView',
  data() {
    return {
      formData: {
        name: '',
        email: '',
        subject: '',
        message: '',
      },
      errors: {},
      showSuccess: false,
    }
  },
  methods: {
    validateEmail(email) {
      const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
      return emailRegex.test(email)
    },

    validateForm() {
      this.errors = {}

      if (!this.formData.name.trim()) {
        this.errors.name = 'Name is required'
      }

      if (!this.formData.email.trim()) {
        this.errors.email = 'Email is required'
      } else if (!this.validateEmail(this.formData.email)) {
        this.errors.email = 'Please enter a valid email'
      }

      if (!this.formData.subject.trim()) {
        this.errors.subject = 'Subject is required'
      }

      if (!this.formData.message.trim()) {
        this.errors.message = 'Message is required'
      } else if (this.formData.message.length < 10) {
        this.errors.message = 'Message must be at least 10 characters'
      }

      return Object.keys(this.errors).length === 0
    },

    resetForm() {
      this.formData = { name: '', email: '', subject: '', message: '' }
    },

    handleSubmit() {
      if (!this.validateForm()) {
        return
      }

      console.log('Form submitted:', this.formData)
      this.showSuccess = true

      setTimeout(() => {
        this.showSuccess = false
        this.resetForm()
      }, 3000)
    },
  },
}
</script>

<template>
  <section class="mx-auto max-w-xl px-4 py-16">
    <h1 class="mb-8 text-center text-4xl font-bold text-slate-800 dark:text-slate-100">Contact Me</h1>

    <p v-if="showSuccess" class="mb-6 rounded-lg bg-green-100 p-4 text-green-700 dark:bg-green-900 dark:text-green-300">
      Thank you! Your message has been sent.
    </p>

    <form class="flex flex-col gap-4" @submit.prevent="handleSubmit">
      <div>
        <label class="mb-1 block font-medium text-slate-700 dark:text-slate-200">Name</label>
        <input
          v-model="formData.name"
          type="text"
          class="w-full rounded-lg border border-slate-300 bg-white px-3 py-2 text-slate-900 focus:border-indigo-500 focus:outline-none dark:border-slate-600 dark:bg-slate-800 dark:text-slate-100"
        />
        <p v-if="errors.name" class="mt-1 text-sm text-red-600 dark:text-red-400">{{ errors.name }}</p>
      </div>

      <div>
        <label class="mb-1 block font-medium text-slate-700 dark:text-slate-200">Email</label>
        <input
          v-model="formData.email"
          type="email"
          class="w-full rounded-lg border border-slate-300 bg-white px-3 py-2 text-slate-900 focus:border-indigo-500 focus:outline-none dark:border-slate-600 dark:bg-slate-800 dark:text-slate-100"
        />
        <p v-if="errors.email" class="mt-1 text-sm text-red-600 dark:text-red-400">{{ errors.email }}</p>
      </div>

      <div>
        <label class="mb-1 block font-medium text-slate-700 dark:text-slate-200">Subject</label>
        <input
          v-model="formData.subject"
          type="text"
          class="w-full rounded-lg border border-slate-300 bg-white px-3 py-2 text-slate-900 focus:border-indigo-500 focus:outline-none dark:border-slate-600 dark:bg-slate-800 dark:text-slate-100"
        />
        <p v-if="errors.subject" class="mt-1 text-sm text-red-600 dark:text-red-400">{{ errors.subject }}</p>
      </div>

      <div>
        <label class="mb-1 block font-medium text-slate-700 dark:text-slate-200">Message</label>
        <textarea
          v-model="formData.message"
          rows="5"
          class="w-full rounded-lg border border-slate-300 bg-white px-3 py-2 text-slate-900 focus:border-indigo-500 focus:outline-none dark:border-slate-600 dark:bg-slate-800 dark:text-slate-100"
        ></textarea>
        <p v-if="errors.message" class="mt-1 text-sm text-red-600 dark:text-red-400">{{ errors.message }}</p>
      </div>

      <button
        type="submit"
        class="rounded-lg bg-indigo-600 px-6 py-3 font-semibold text-white transition hover:bg-indigo-700 dark:bg-indigo-500 dark:hover:bg-indigo-400"
      >
        Send Message
      </button>
    </form>
  </section>
</template>
