<template>
  <div class="card" v-click-outside="null_selected">
    <div class="card_top" @click="$emit('select')">+</div>
    <div class="card_container">
      <div class="content">
        <div class="boost">BOOST</div>
        <div class="v_c">
          <div class="label">Liking</div>
          <div class="value">100</div>
        </div>
      </div>
    </div>
    <div class="card_detail">
      <div class="content">CREATE BOOST</div>
      <div class="divider">
        <div>Date Period</div>
      </div>
      <div class="date_range_title">Pick Date Range</div>
      <div class="date_range">
        <div class="first_date">
          <input
            type="text"
            :class="`custom-input-${item.id}`"
            placeholder="select date"
          />
          <custom-date-picker
            :auto-submit="true"
            v-model="date1"
            format="YYYY-MM-DD"
            display-format="jYYYY-jMM-jDD"
            :custom-input="`.custom-input-${item.id}`"
          />
        </div>
        <div class="to">To</div>
        <div class="second_date">
          <input
            type="text"
            :class="`custom-input-${item.id}_2`"
            placeholder="select date"
          />
          <custom-date-picker
            :auto-submit="true"
            v-model="date2"
            format="YYYY-MM-DD"
            display-format="jYYYY-jMM-jDD"
            :custom-input="`.custom-input-${item.id}_2`"
          />
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  data: () => ({
    date1: "",
    date2: "",
  }),
  methods: {
    null_selected(e) {},
  },
  directives: {
    "click-outside": {
      bind: function (el, binding, vNode) {
        if (typeof binding.value !== "function") {
          const compName = vNode.context.name;
          let warn = `[Vue-click-outside:] provided expression '${binding.expression}' is not a function, but has to be`;
          if (compName) {
            warn += `Found in component '${compName}'`;
          }

          console.warn(warn);
        }
        const bubble = binding.modifiers.bubble;
        const handler = (e) => {
          if (bubble || (!el.contains(e.target) && el !== e.target)) {
            binding.value(e);
            if (el.className.includes("active")) {
              vNode.context.$emit("close");
            }
          }
        };
        el.__vueClickOutside__ = handler;

        document.addEventListener("click", handler);
      },

      unbind: function (el, binding) {
        document.removeEventListener("click", el.__vueClickOutside__);
        el.__vueClickOutside__ = null;
      },
    },
  },
};
</script>
