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
  <section class="mx-auto max-w-5xl px-4 py-16 sm:px-6 sm:py-24">
    <div class="mb-12 text-center">
      <p
        class="mb-2 text-sm font-semibold tracking-widest text-indigo-600 uppercase dark:text-indigo-400"
      >
        Contact
      </p>
      <h1 class="mb-4 text-4xl font-extrabold tracking-tight sm:text-5xl">
        Let's <span class="text-gradient">work together</span>
      </h1>
      <p class="mx-auto max-w-xl text-lg text-slate-500 dark:text-slate-400">
        Have a question or an idea? Send me a message and I'll get back to you.
      </p>
    </div>

    <div class="grid gap-8 lg:grid-cols-[1fr_2fr]">
      <aside
        class="flex flex-col justify-between gap-6 rounded-2xl bg-gradient-to-br from-indigo-600 via-violet-600 to-fuchsia-600 p-8 text-white shadow-xl shadow-indigo-500/20"
      >
        <div>
          <h2 class="mb-3 text-2xl font-bold">Say hello 👋</h2>
          <p class="leading-relaxed text-indigo-100">
            I'm open to new opportunities, collaborations, and chats about data, scraping, and web development.
          </p>
        </div>
        <ul class="space-y-3 text-indigo-50">
          <li class="flex items-center gap-3">
            <span class="text-xl">📍</span> Based in Cambodia
          </li>
          <li class="flex items-center gap-3">
            <span class="text-xl">🗣️</span> Korean · Japanese · English at work
          </li>
        </ul>
      </aside>

      <div
        class="rounded-2xl border border-slate-200 bg-white p-6 sm:p-8 dark:border-slate-800 dark:bg-slate-900"
      >
        <Transition
          enter-from-class="opacity-0 -translate-y-2"
          enter-active-class="transition duration-300"
          leave-to-class="opacity-0"
          leave-active-class="transition duration-300"
        >
          <p
            v-if="showSuccess"
            class="mb-6 flex items-center gap-2 rounded-xl bg-emerald-50 p-4 font-medium text-emerald-700 dark:bg-emerald-500/15 dark:text-emerald-300"
          >
            ✅ Thank you! Your message has been sent.
          </p>
        </Transition>

        <form class="flex flex-col gap-5" novalidate @submit.prevent="handleSubmit">
          <div class="grid gap-5 sm:grid-cols-2">
            <div>
              <label
                for="name"
                class="mb-1.5 block text-sm font-medium text-slate-700 dark:text-slate-200"
                >Name</label
              >
              <input
                id="name"
                v-model="formData.name"
                type="text"
                placeholder="Your name"
                class="input"
              />
              <p v-if="errors.name" class="mt-1.5 text-sm text-red-600 dark:text-red-400">
                {{ errors.name }}
              </p>
            </div>
            <div>
              <label
                for="email"
                class="mb-1.5 block text-sm font-medium text-slate-700 dark:text-slate-200"
                >Email</label
              >
              <input
                id="email"
                v-model="formData.email"
                type="email"
                placeholder="you@example.com"
                class="input"
              />
              <p v-if="errors.email" class="mt-1.5 text-sm text-red-600 dark:text-red-400">
                {{ errors.email }}
              </p>
            </div>
          </div>

          <div>
            <label
              for="subject"
              class="mb-1.5 block text-sm font-medium text-slate-700 dark:text-slate-200"
              >Subject</label
            >
            <input
              id="subject"
              v-model="formData.subject"
              type="text"
              placeholder="What is this about?"
              class="input"
            />
            <p v-if="errors.subject" class="mt-1.5 text-sm text-red-600 dark:text-red-400">
              {{ errors.subject }}
            </p>
          </div>

          <div>
            <label
              for="message"
              class="mb-1.5 block text-sm font-medium text-slate-700 dark:text-slate-200"
              >Message</label
            >
            <textarea
              id="message"
              v-model="formData.message"
              rows="5"
              placeholder="Tell me about your project..."
              class="input resize-none"
            ></textarea>
            <p v-if="errors.message" class="mt-1.5 text-sm text-red-600 dark:text-red-400">
              {{ errors.message }}
            </p>
          </div>

          <button
            type="submit"
            class="rounded-xl bg-gradient-to-r from-indigo-600 to-violet-600 px-6 py-3.5 font-semibold text-white shadow-lg shadow-indigo-500/30 transition hover:-translate-y-0.5 hover:shadow-xl hover:shadow-indigo-500/40"
          >
            Send Message →
          </button>
        </form>
      </div>
    </div>
  </section>
</template>
