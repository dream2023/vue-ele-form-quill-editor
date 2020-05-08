<template>
  <vue-editor
    :class="desc.class"
    :style="desc.style"
    @image-added="handleImageAdded"
    class="ele-form-rich-text"
    useCustomImageHandler
    v-bind="attrs"
    v-model="newValue"
    v-on="onEvents"
  />
</template>

<script>
import { VueEditor, Quill } from 'vue2-editor'
import ImageResize from 'bc-quill-image-resize-module'
import uploadMixin from 'vue-ele-form/lib/mixins/uploadMixin'
import formMixin from 'vue-ele-form/lib/mixins/formMixin'
Quill.register('modules/imageResize', ImageResize)

export default {
  name: 'quill-editor',
  mixins: [uploadMixin, formMixin],
  components: {
    VueEditor
  },
  data () {
    return {
      defaultAttrs: {
        name: 'file',
        editorToolbar: [
          ['bold', 'italic', 'underline'], // toggled buttons
          ['image', 'link'],
          [{ 'size': ['small', true, 'large', 'huge'] }], // custom dropdown
          [{ 'header': [1, 2, 3, 4, 5, 6, false] }],
          [{ 'align': [] }],
          [{ 'color': [] }, { 'background': [] }], // dropdown with defaults from theme
          [{ 'list': 'ordered' }, { 'list': 'bullet' }],
          [{ 'indent': '-1' }, { 'indent': '+1' }], // outdent/indent
          ['blockquote'],
          ['clean']
        ],
        editorOptions: {
          modules: {
            imageResize: {}
          }
        }
      }
    }
  },
  methods: {
    // 上传图片
    handleImageAdded (file, Editor, cursorLocation, resetUploader) {
      this.handleImageUpload(file, (response) => {
        Editor.insertEmbed(cursorLocation, 'image', response)
        resetUploader()
      })
    }
  }
}
</script>

<style lang="css">
.ele-form-rich-text .ql-toolbar {
  line-height: 1.5 !important;
}

.ele-form-rich-text .ql-picker-label {
  outline: none !important;
}

.ele-form-rich-text .ql-snow .ql-tooltip[data-mode="link"]:before {
  content: "请输入链接地址:" !important;
}
.ele-form-rich-text .ql-snow .ql-tooltip.ql-editing a.ql-action:after {
  border-right: 0px;
  content: "保存" !important;
  padding-right: 0px;
}

.ele-form-rich-text .ql-snow .ql-tooltip[data-mode="video"]:before {
  content: "请输入视频地址:" !important;
}

.ele-form-rich-text .ql-snow .ql-picker.ql-size .ql-picker-label:before,
.ele-form-rich-text .ql-snow .ql-picker.ql-size .ql-picker-item:before {
  content: "14px" !important;
}
.ele-form-rich-text
  .ql-snow
  .ql-picker.ql-size
  .ql-picker-label[data-value="small"]:before,
.ele-form-rich-text
  .ql-snow
  .ql-picker.ql-size
  .ql-picker-item[data-value="small"]:before {
  content: "10px" !important;
}
.ele-form-rich-text
  .ql-snow
  .ql-picker.ql-size
  .ql-picker-label[data-value="large"]:before,
.ele-form-rich-text
  .ql-snow
  .ql-picker.ql-size
  .ql-picker-item[data-value="large"]:before {
  content: "18px" !important;
}
.ele-form-rich-text
  .ql-snow
  .ql-picker.ql-size
  .ql-picker-label[data-value="huge"]:before,
.ele-form-rich-text
  .ql-snow
  .ql-picker.ql-size
  .ql-picker-item[data-value="huge"]:before {
  content: "32px" !important;
}

.ele-form-rich-text .ql-snow .ql-picker.ql-header .ql-picker-label:before,
.ele-form-rich-text .ql-snow .ql-picker.ql-header .ql-picker-item:before {
  content: "文本" !important;
}
.ele-form-rich-text
  .ql-snow
  .ql-picker.ql-header
  .ql-picker-item[data-value="1"]:before,
.ql-snow .ql-picker.ql-header .ql-picker-label[data-value="1"]:before {
  content: "标题1" !important;
}
.ele-form-rich-text
  .ql-snow
  .ql-picker.ql-header
  .ql-picker-label[data-value="2"]:before,
.ele-form-rich-text
  .ql-snow
  .ql-picker.ql-header
  .ql-picker-item[data-value="2"]:before {
  content: "标题2" !important;
}
.ele-form-rich-text
  .ql-snow
  .ql-picker.ql-header
  .ql-picker-label[data-value="3"]:before,
.ele-form-rich-text
  .ql-snow
  .ql-picker.ql-header
  .ql-picker-item[data-value="3"]:before {
  content: "标题3" !important;
}
.ele-form-rich-text
  .ql-snow
  .ql-picker.ql-header
  .ql-picker-label[data-value="4"]:before,
.ele-form-rich-text
  .ql-snow
  .ql-picker.ql-header
  .ql-picker-item[data-value="4"]:before {
  content: "标题4" !important;
}
.ele-form-rich-text
  .ql-snow
  .ql-picker.ql-header
  .ql-picker-label[data-value="5"]:before,
.ele-form-rich-text
  .ql-snow
  .ql-picker.ql-header
  .ql-picker-item[data-value="5"]:before {
  content: "标题5" !important;
}
.ele-form-rich-text
  .ql-snow
  .ql-picker.ql-header
  .ql-picker-label[data-value="6"]:before,
.ele-form-rich-text
  .ql-snow
  .ql-picker.ql-header
  .ql-picker-item[data-value="6"]:before {
  content: "标题6" !important;
}

.ele-form-rich-text .ql-snow .ql-picker.ql-font .ql-picker-label:before,
.ele-form-rich-text .ql-snow .ql-picker.ql-font .ql-picker-item:before {
  content: "标准字体" !important;
}
.ele-form-rich-text
  .ql-snow
  .ql-picker.ql-font
  .ql-picker-label[data-value="serif"]:before,
.ele-form-rich-text
  .ql-snow
  .ql-picker.ql-font
  .ql-picker-item[data-value="serif"]:before {
  content: "衬线字体" !important;
}
.ele-form-rich-text
  .ql-snow
  .ql-picker.ql-font
  .ql-picker-label[data-value="monospace"]:before,
.ele-form-rich-text
  .ql-snow
  .ql-picker.ql-font
  .ql-picker-item[data-value="monospace"]:before {
  content: "等宽字体" !important;
}
</style>
