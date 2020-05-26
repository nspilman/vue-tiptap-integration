
<template>
<div>
<editor-menu-bar :editor="editor" v-slot="{ commands, isActive }">
        <button :class="{ 'is-active': isActive.bold() }" @click="commands.bold">
          Bold
        </button>
    </editor-menu-bar>
  <editor-content :editor="editor" />
  <div v-html="html"/>
  </div>
</template>

<script>
// Import the editor
import { Editor, EditorContent, EditorMenuBar } from 'tiptap'

export default {
  components: {
    EditorContent,
    EditorMenuBar
  },
  data() {
    return {
      editor: null,
      html:null,
      json: null
    }
  },
  mounted() {
    this.editor = new Editor({
      content: '<p>This is just a boring paragraph</p>',
      onUpdate: ({ getHTML, getJSON }) => {
          this.html = getHTML();
          this.json = getJSON();
    //   this.$emit('input', getHTML())
    },
    })
    //   console.log(this.editor.activeNodes)
  },
  created(){
  },
  beforeDestroy() {
    this.editor.destroy()
  },
}
</script>