<template>
  <div
    class="border bg-fixed h-screen flex items-center justify-items-center"
    style="background-image: url(./src/assets/4814518.jpg)"
  >
    <div class="bg-white h-auto w-2/4 mx-auto">
      <h1 class="text-center mt-6 font-semibold text-2xl mb-8">Todo Application</h1>
      <div class="h-2/3 flex items-center justify-items-center flex-col">
        <div class="mx-auto mb-8">
          <input
            type="text"
            placeholder="Add New Task"
            class="border pl-2 h-7 text-xs focus:outline-none"
            v-model="item"
          />
          <button
            class="bg-black text-white text-xs h-7 w-11 focus:outline-none hover:h-10"
            @click="additem(item)"
          >
            Add
          </button>
        </div>
        <p class="text-xs mb-5">
          You have
          <span class="text-sm font-medium text-blue-600">
            {{ taskamount }} task(s)
          </span>
          to complete today
        </p>
        <p class="text-xs text-red-600 mb-4" v-if="showerror">
          Field should not be left empty!
        </p>
        <div
          class="flex bg-gray-100 w-3/5 mx-auto pl-2 mb-3 border border-separate"
          :class="[todoitem.active ? 'opacity-100' : 'opacity-20']"
          v-for="todoitem in todoitems"
          :key="todoitem.identifier"
        >
          <p class="w-48 text-xs my-auto">{{ todoitem.identifier | trunc }}</p>
          <button
            class="bg-green-800 h-7 w-24 text-xs text-white mr-1 focus:outline-none"
            @click.once="completed(todoitem)"
          >
            Completed
          </button>
          <button
            class="bg-red-200 h-7 w-24 text-xs text-grey-800 mr-1 font-medium focus:outline-none"
            @click="deleteitem(todoitem)"
          >
            Delete
          </button>
          <button
            class="bg-white h-7 w-24 text-xs text-grey-500 font-medium focus:outline-none"
            @click="edititem(todoitem)"
            v-if="todoitem.active"
          >
            edit
          </button>
        </div>
        <p class="text-xs mb-5" v-if="completedtaskamount > 0">
          You have completed
          <span class="text-sm font-medium text-green-600">
            {{ completedtaskamount }} task(s)
          </span>
        </p>
        <div class="h-5 bg-white"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todoitems: [],
      completedtasks: [],
      pendingtasks: [],
      item: null,
      showerror: false,
      completeditem: false,
    };
  },
  methods: {
    additem: function (item) {
      if (item.replace(/\s+/g, "") == "" || this.item === "") {
        this.showerror = true;
      } else {
        this.todoitems.push({ identifier: this.item, active: true });
        this.pendingtasks.push(this.item);
        this.item = null;
        this.showerror = false;
      }
    },
    deleteitem: function (thing) {
      this.todoitems = this.todoitems.filter(
        (item) => item.identifier !== thing.identifier
      );
      this.completedtasks = this.completedtasks.filter(
        (item) => item.identifier !== thing.identifier
      );
      this.pendingtasks = this.pendingtasks.filter((item) => item !== thing.identifier);
    },
    completed: function (value) {
      this.completedtasks.push(value);
      this.pendingtasks = this.pendingtasks.filter((item) => item !== value.identifier);
      return (value.active = false);
    },
    edititem: function (thing) {
      this.item = thing.identifier;
      this.todoitems = this.todoitems.filter(
        (item) => item.identifier !== thing.identifier
      );
      this.completedtasks = this.completedtasks.filter(
        (item) => item.identifier !== thing.identifier
      );
      this.pendingtasks = this.pendingtasks.filter((item) => item !== thing.identifier);
    },
  },
  filters: {
    trunc(value) {
      if (value.length > 13) {
        return value.slice(0, 12) + "....";
      } else {
        return value;
      }
    },
  },
  computed: {
    taskamount() {
      return this.pendingtasks.length;
    },
    completedtaskamount() {
      return this.completedtasks.length;
    },
  },
  directives: {},
};
</script>
