<template>
  <div class="my-1">
    <span>followings are {{fullname}} order:</span>
    <ul>
      <li v-if="!isOrderExist">No data found</li>
      <li v-if="isOrderExist">{{formInfo.orders.apple_count}} apples</li>
      <li
        v-if="isOrderExist"
        v-show="formInfo.orders.banana_condiments.length > 0"
      >Banana condiments
        <ul>
          <li
            v-for="condiment in formInfo.orders.banana_condiments"
            v-bind:key="condiment"
          >{{condiment}}</li>
        </ul>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  props: {
    formInfo: {
      type: Object,
      required: true,
      default() {
        return {
          personal_info: {},
          orders: {
            banana_condiments: []
          }
        };
      }
    }
  },
  computed: {
    fullname() {
      let fullname = "unknown";
      if (!this.$props.formInfo.personalInfo) {
        return fullname;
      }

      const { first_name, last_name } = this.$props.formInfo.personalInfo;
      if (first_name) {
        fullname = last_name ? `${first_name} ${last_name}` : first_name;
      } else if (last_name) {
        fullname = last_name;
      }

      return fullname;
    },
    isOrderExist() {
      return this.$props.formInfo.orders !== undefined;
    }
  }
};
</script>

