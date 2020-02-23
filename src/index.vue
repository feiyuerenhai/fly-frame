<template></template>

<script>
import scriptjs from "scriptjs"
export default {
  name: "fly-frame",
  props: {
    jquery: {
      required: true,
      type: String
    },
    flyui: {
      required: true,
      type: String
    }
  },
  methods: {
    async popup(options, event = "close") {
      const _options = Object.assign(
        {
          padding: "10px 10px",
          width: 800,
          height: 450
        },
        options
      )
      return new Promise((resolve, reject) => {
        window.fly.top.fly.dialog(_options).bind(event, data => {
          resolve(data.sender.data, data)
        })
      })
    },
    init() {
      if (!window.$ || !window.fly) {
        scriptjs(this.jquery, () => {
          scriptjs(this.flyui)
        })
      }
    }
  },
  mounted() {
    this.init()
  }
}
</script>

<style lang="less">
div.popup-modal div.dialog {
  .dialog-grid {
    margin: 0;
    border-spacing: 0;
    .dialog-header {
      background: #2963ff;
      border-radius: 6px 6px 0 0;
      .dialog-title {
        color: white;
        padding: 6px 15px;
        line-height: 30px;
        font-size: 14px;
        height: 42px;
      }
      .dialog-close {
        position: absolute;
        cursor: pointer;
        border: none;
        top: 0;
        right: 0;
        width: 46px;
        height: 42px;
        color: #ffffff;
        font-size: 18px;
        background: transparent;
      }
    }
    .dialog-body {
      border-radius: 0 0 6px 6px;
      padding: 15px 20px !important;
      background: white;
    }
  }
}
</style>