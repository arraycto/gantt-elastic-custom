<!--
/**
 * @fileoverview ItemColumn component
 * @license MIT
 * @author Rafal Pospiech <neuronet.io@gmail.com>
 * @package GanttElastic
 */
-->
<template>
  <div
    class="gantt-elastic__task-list-item-column"
    :style="root.style('task-list-item-column', column.style['task-list-item-column'], {width:column.finalWidth+'px',height:column.height+'px'})"
  >
    <div
      class="gantt-elastic__task-list-item-value-wrapper"
      :style="root.style('task-list-item-value-wrapper',column.style['task-list-item-value-wrapper'])"
    >
      <slot></slot>
      <div
        class="gantt-elastic__task-list-item-value-container"
        :style="root.style('task-list-item-value-container', column.style['task-list-item-value-container'])"
      >
        <div
          v-if="!html"
          class="gantt-elastic__task-list-item-value"
          :style="root.style('task-list-item-value',column.style['task-list-item-value'])"
        >{{value}}</div>
        <div
          v-if="html"
          class="gantt-elastic__task-list-item-value"
          :style="root.style('task-list-item-value',column.style['task-list-item-value'])"
          v-html="value"
        ></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  inject: ["root"],
  props: ["column", "task"],
  data () {
    return {};
  },
  computed: {
    /**
     * Should we display html or just text?
     *
     * @returns {boolean}
     */
    html () {
      if (typeof this.column.html !== "undefined" && this.column.html === true) {
        return true;
      }
      return false;
    },

    /**
     * Get column value
     *
     * @returns {any|string}
     */
    value () {
      if (typeof this.column.value === "function") {
        return this.column.value(this.task);
      }
      return this.task[this.column.value];
    }
  }
};
</script>
