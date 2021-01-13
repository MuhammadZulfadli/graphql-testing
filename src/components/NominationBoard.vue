<template>
  <div
    class="h-100 w-full flex items-center justify-center bg-teal-lightest font-sans"
  >
    <div class="bg-white rounded shadow p-6 m-4 w-full lg:w-3/4 lg:max-w-lg">
      <div class="mb-4">
        <h1 class="text-grey-darkest">Todo List</h1>
        <div class="flex mt-4">
          <input
            class="shadow appearance-none border rounded w-full py-2 px-3 mr-4 text-grey-darker"
            placeholder="Add Todo"
          />
          <button
            class="flex-no-shrink p-2 border-2 rounded text-teal border-teal hover:text-white hover:bg-teal"
          >
            Add
          </button>
        </div>
      </div>
      <div v-for="todos in todo" :key="todos.id">
        <div class="flex mb-4 items-center">
          <span class="w-full text-grey-darkest">
            {{ todos.title }}
          </span>
          <button
            class="flex-no-shrink p-2 ml-2 border-2 rounded text-red border-red hover:text-white hover:bg-red"
          >
            Remove
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "NominationBoard",
  data() {
    return {
      todo: []
    };
  },

  async mounted() {
    try {
      const result = await axios({
        method: "POST",
        url: "https://graphql-tresting.hasura.app/v1/graphql",
        data: {
          query: `
                {
                    todos {
                        id,
                        title,
                         user {
                            name,
                            last_seen
                         }
                    }
                }
            `
        }
      });
      this.todo = result.data.data.todos;
    } catch (error) {
      console.log(error);
    }
  }
};
</script>
