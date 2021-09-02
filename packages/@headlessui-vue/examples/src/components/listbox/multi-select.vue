<template>
  <div class="flex justify-center w-screen h-full p-12 bg-gray-50">
    <div class="w-full max-w-4xl mx-auto">
      <div class="space-y-1">
        <Listbox v-model="activePersons">
          <ListboxLabel class="block text-sm font-medium leading-5 text-gray-700"
            >Assigned to</ListboxLabel
          >

          <div class="relative">
            <span class="inline-block w-full rounded-md shadow-sm">
              <ListboxButton
                class="relative w-full py-2 pl-3 pr-10 text-left transition duration-150 ease-in-out bg-white border border-gray-300 rounded-md cursor-default focus:outline-none focus:shadow-outline-blue focus:border-blue-300 sm:text-sm sm:leading-5"
              >
                <span className="block flex flex-wrap gap-2">
                  <span
                    v-for="(active, index) in activePersons"
                    :key="index"
                    class="px-2 py-0.5 bg-blue-50 rounded flex gap-1 items-center"
                  >
                    <span>{{ active.name }}</span>
                  </span>
                </span>
                <span class="absolute inset-y-0 right-0 flex items-center pr-2 pointer-events-none">
                  <svg
                    class="w-5 h-5 text-gray-400"
                    viewBox="0 0 20 20"
                    fill="none"
                    stroke="currentColor"
                  >
                    <path
                      d="M7 7l3-3 3 3m0 6l-3 3-3-3"
                      strokeWidth="1.5"
                      strokeLinecap="round"
                      strokeLinejoin="round"
                    />
                  </svg>
                </span>
              </ListboxButton>
            </span>

            <div class="absolute w-full mt-1 bg-white rounded-md shadow-lg">
              <ListboxOptions
                class="py-1 overflow-auto text-base leading-6 rounded-md shadow-xs max-h-60 focus:outline-none sm:text-sm sm:leading-5"
              >
                <ListboxOption
                  v-for="person in people"
                  :key="person.id"
                  :value="person"
                  :disabled="person.disabled"
                  v-slot="{ active, selected }"
                  as="template"
                >
                  <li :class="[
                      active ? 'text-white bg-indigo-600' : 'text-gray-900',
                      'cursor-default select-none relative py-2 pl-10 pr-4',
                    ]"
                  >
                    <span
                    :class="[
                      selected ? 'font-medium' : 'font-normal',
                      'block truncate',
                    ]"
                    >
                      {{ person.name }}
                    </span>
                    <span
                      v-if="selected"
                      :class="
                        classNames(
                          'absolute inset-y-0 right-0 flex items-center pr-4',
                          active ? 'text-white' : 'text-indigo-600'
                        )
                      "
                    >
                      <svg class="w-5 h-5" viewbox="0 0 20 20" fill="currentColor">
                        <path
                          fillRule="evenodd"
                          d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z"
                          clipRule="evenodd"
                        />
                      </svg>
                    </span>
                  </li>
                </ListboxOption>
              </ListboxOptions>
            </div>
          </div>
        </Listbox>
      </div>
    </div>
  </div>
</template>

<script>
import { defineComponent, h, ref, onMounted, watchEffect, watch } from 'vue'
import {
  Listbox,
  ListboxLabel,
  ListboxButton,
  ListboxOptions,
  ListboxOption,
} from '@headlessui/vue'

function classNames(...classes) {
  return classes.filter(Boolean).join(' ')
}

export default {
  components: { Listbox, ListboxLabel, ListboxButton, ListboxOptions, ListboxOption },
  setup(props, context) {
    let people = [
      { id: 1, name: 'Wade Cooper' },
      { id: 2, name: 'Arlene Mccoy' },
      { id: 3, name: 'Devon Webb' },
      { id: 4, name: 'Tom Cook' },
      { id: 5, name: 'Tanya Fox', disabled: true },
      { id: 6, name: 'Hellen Schmidt' },
      { id: 7, name: 'Caroline Schultz' },
      { id: 8, name: 'Mason Heaney' },
      { id: 9, name: 'Claudie Smitham' },
      { id: 10, name: 'Emil Schaefer' },
    ]

    let activePersons = ref([people[2], people[9]])

    return {
      people,
      activePersons,
      classNames,
      resolveListboxOptionClassName({ active, disabled }) {
        return classNames(
          'relative py-2 pl-3 cursor-default select-none pr-9 focus:outline-none',
          active ? 'text-white bg-indigo-600' : 'text-gray-900',
          disabled && 'bg-gray-50 text-gray-300'
        )
      },
    }
  },
}
</script>

