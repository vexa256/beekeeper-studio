<template>
  <div class="list-item schema">
    <a class="list-item-btn" v-bind:class="{'open': expanded}" role="button" @click.prevent="manuallyExpanded = !manuallyExpanded">
      <span class="btn-fab open-close" >
        <i class="dropdown-icon material-icons">keyboard_arrow_right</i>
      </span>
      <i title="Schema" class="schema-icon item-icon material-icons">folder</i>
      <span class="table-name truncate expand">{{title}}</span>
    </a>
    <div v-show="expanded" class="sub-items">
      <slot></slot>
    </div>
  </div>
</template>

<script type="text/javascript">

	export default {
    props: ["title", "forceExpand", "forceCollapse", "expandedInitially"],
    data() {
      return {
        manuallyExpanded: false,
      }
    },
    mounted() {
      this.manuallyExpanded = this.expandedInitially
    },
    computed: {
      expanded() {
        return this.manuallyExpanded
      }
    },
    watch: {
      forceExpand() {
        this.manuallyExpanded = this.forceExpand
      },
      forceCollapse() {
        if (this.forceCollapse) {
          this.manuallyExpanded = false
        }
      },
    },
    methods: {
      tableSelected(table) {
        this.$emit("tableSelected", table)
      }
    }
	}
</script>

<style scoped>
  .schema > .sub-items {
    padding-left: 18px!important;
  }
</style>
