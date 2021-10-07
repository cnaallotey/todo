<template>
  <div>
    <div class="w-1/4 mx-auto mt-10">
      <label for="Name" class="text-sm font-medium text-gray-900 mb-2"> Full Name</label
      ><br />
      <input
        type="text"
        v-model="detail.fullname"
        class="border-2 h-8 w-72 rounded-md mb-4 text-l pl-2"
      /><br />
      <label for="Name" class="text-sm font-medium text-gray-900 mb-2">
        Email Address</label
      ><br />
      <input
        type="email"
        v-model="detail.emailaddress"
        class="border-2 h-8 w-72 rounded-md mb-4 text-md pl-2"
      /><br />
      <label for="Name" class="text-sm font-medium text-gray-900 mb-2">Momo Number</label
      ><br />
      <input
        type="tel"
        v-model="detail.momonumber"
        class="border-2 h-8 w-72 rounded-md mb-4 text-md pl-2"
      /><br />
      <label for="Name" class="text-sm font-medium text-gray-900 mb-2">
        Date of Payment</label
      ><br />
      <input
        type="date"
        v-model="detail.dateofexpiration"
        class="border-2 h-8 w-72 rounded-md mb-6 text-sm font-medium pl-2"
        id="cart"
      /><br />
      <h1 class="text-sm text-red-500 font-regular italic mb-4" v-if="!emptyfield">
        Please fill required Spaces and select a book
      </h1>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    detail: {
      type: Object,
    },
    adddetails: {
      type: Function,
    },
    emptyfield: {
      type: Boolean,
    },
    details: {
      type: Array,
    },
  },
};
</script>
