<template>
  <div class="flex flex-col w-4/5 mx-auto">
    <div>
      <input
        type="text"
        placeholder="Search Items"
        v-model="Search"
        class="border h-12 w-96 mt-5 mb-10 pl-4 rounded-lg"
      />
    </div>
    <div class="-my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
      <div class="py-2 align-middle inline-block min-w-full sm:px-6 lg:px-8">
        <div class="shadow overflow-hidden border-b border-gray-200 sm:rounded-lg">
          <table class="min-w-full divide-y divide-gray-200">
            <thead class="bg-gray-50">
              <tr>
                <th
                  scope="col"
                  class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider"
                >
                  Item Name
                </th>
                <th
                  scope="col"
                  class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider"
                >
                  Price
                </th>
                <th
                  scope="col"
                  class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider"
                >
                  stock
                </th>
                <th
                  scope="col"
                  class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider"
                >
                  Stock remaining
                </th>
                <th scope="col" class="relative px-6 py-3">
                  <span class="sr-only">Add to Cart</span>
                </th>
              </tr>
            </thead>
            <tbody class="bg-white divide-y divide-gray-200">
              <tr v-for="book in searchfilters" :key="book.name">
                <td class="px-6 py-4 whitespace-nowrap">
                  <div class="flex flex-row mr-3">
                    <input
                      type="checkbox"
                      name="book"
                      :id="book.name"
                      v-bind:value="book"
                      v-model="addedbooks"
                    />
                    <div>
                      <div class="flex items-center">
                        <div class="flex-shrink-0 h-10 w-10">
                          <img class="h-10 w-10 rounded-full" :src="book.image" alt="" />
                        </div>
                        <div class="ml-4">
                          <div class="text-sm font-medium text-gray-900" v-changecolor>
                            {{ book.name }}
                          </div>
                          <div class="text-sm text-gray-500">
                            {{ book.stocks }} Items Received
                          </div>
                        </div>
                      </div>
                    </div>
                  </div>
                </td>
                <td class="px-6 py-4 whitespace-nowrap">
                  <div class="text-sm text-gray-900">{{ book.price }}</div>
                </td>
                <td class="px-6 py-4 whitespace-nowrap">
                  <span
                    class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full bg-green-100 text-green-800"
                  >
                    In Stock
                  </span>
                </td>
                <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">
                  {{ book.remainingstock }} items remianing
                </td>
                <td class="px-6 py-4 whitespace-nowrap text-right text-sm font-medium">
                  <a
                    href="#"
                    @click="addbooks(itemtable)"
                    class="text-indigo-600 hover:text-indigo-900"
                    >Add to cart</a
                  >
                </td>
              </tr>
            </tbody>
          </table>
        </div>
        <div>
          <h1>they are: {{ allbooks }}</h1>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    books: {
      type: Array,
    },
    addedbooks: {
      type: Array,
    },
    book: {
      type: Object,
    },
    addbooks: {
      type: Function,
    },
    Search: {
      type: String,
    },
  },

  data() {
    return {};
  },
  computed: {
    allbooks() {
      //return this.addedbooks.length;
      return this.addedbooks.map((addedbook) => addedbook.name).join(", ");
      //return this.addedbooks.join(", ");
      //return "Welcome";
      //for (var i = 0; i < this.addedbooks.length; i++) {
      // return this.addedbooks[i].name;
      // }
    },
    searchfilters() {
      return this.books.filter((book) => {
        return book.name.match(this.Search);
      });
    },
  },
  directives: {
    changecolor: {
      bind(el, binding, vnode) {
        el.style.color = "#" + Math.random().toString(16).slice(2, 8);
      },
    },
  },
};
</script>
