<template>
  <div class="shadow mt-5 sm:overflow-hidden sm:rounded-md">
      <div class="space-y-6 bg-white px-4 py-2 sm:p-6">
          <h4 class="text-md font-medium leading-6 text-gray-900">Pin {{ id }}</h4>

          <div class="grid grid-cols-3 gap-6">
              <div class="col-span-3 sm:col-span-2">
                  <label :for="`title-${id}`" class="block text-sm font-medium text-gray-700">Title</label>
                  <input :value="title" @input="$emit('update:title', $event.target.value)" type="text" name="title" :id="`title-${id}`" class="mt-1 block w-full flex-1 rounded-md border-gray-300 focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm" />
              </div>
          </div>

          <div>
              <label :for="`description-${id}`" class="block text-sm font-medium text-gray-700">Description</label>
              <div class="mt-1">
                  <textarea :value="description" @input="$emit('update:description', $event.target.value)" :id="`description-${id}`" name="description" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm"></textarea>
              </div>
          </div>

          <div class="bg-gray-50 px-4 py-3 text-right sm:px-6">
            <button @click="$emit('delete')" class="inline-flex justify-center rounded-md border border-transparent bg-red-600 py-2 px-4 text-sm font-medium text-white shadow-sm hover:bg-red-700 focus:outline-none focus:ring-2 focus:ring-red-500 focus:ring-offset-2">Delete</button>
          </div>
      </div>
  </div>
</template>

<script>
  export default{
    emits: ['update:title', 'update:description', 'delete'],
    props: ['id', 'title', 'description']
  }
</script>