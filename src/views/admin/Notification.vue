<template>
  <div class="">
    <div class="crumbs">
      <el-breadcrumb separator="/">
        <el-breadcrumb-item><i class="el-icon-lx-copy"></i> Notification</el-breadcrumb-item>
      </el-breadcrumb>
    </div>
    <el-row :gutter="20">
      <el-col :span="24">
        <div class="container">
          <div class="plugins-tips">
            Writing Notifications with CMS
          </div>
          <quill-editor ref="myTextEditor" v-model="content" :options="editorOption"></quill-editor>
          <el-button class="editor-btn" type="primary" @click="submit">Submit</el-button>
        </div>
      </el-col>
    </el-row>

  </div>
</template>

<script>
import 'quill/dist/quill.core.css';
import 'quill/dist/quill.snow.css';
import 'quill/dist/quill.bubble.css';
import {quillEditor} from 'vue-quill-editor';
import bus from "@/components/common/bus";

export default {
  inject: ['reload'],
  name: "Notification",
  data() {
    return {
      message: 'second',
      showHeader: false,
      draft: [],
      unread: [{
        date: '2018-04-19 20:00:00',
        title: 'test1',
      },
        {
          date: '2018-04-19 21:00:00',
          title: 'test2',
        }],
      read: [{
        date: '2018-04-19 20:00:00',
        title: 'test3'
      }],
      recycle: [{
        date: '2018-04-19 20:00:00',
        title: 'test4'
      }],

      content: '',
      editorOption: {
        placeholder: 'Hello World'
      },
    }
  },
  components: {
    quillEditor
  },
  methods: {
    handleRead(index) {
      const item = this.unread.splice(index, 1);
      console.log(item);
      this.read = item.concat(this.read);
    },
    handleDel(index) {
      const item = this.read.splice(index, 1);
      this.recycle = item.concat(this.recycle);
    },
    handleRestore(index) {
      const item = this.recycle.splice(index, 1);
      this.read = item.concat(this.read);
    },
    onEditorChange({editor, html, text}) {
      this.content = html;
    },
    submit() {
      console.log(this.content);
      this.$message.success('Success！');
    }
  },
  computed: {
    unreadNum() {
      return this.unread.length;
    }
  },
  created() {
  }
}
</script>

<style scoped>
.message-title {
  cursor: pointer;
}

.handle-row {
  margin-top: 30px;
}

.container {
  height: 700px;
}

.editor-btn {
  margin-top: 20px;
}
</style>