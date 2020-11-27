<template>
  <div class="HomePage container mt-3 mb-3">
    <div v-if="fileUploaded">
      <AnnotationsPage v-bind:json="json"/>
    </div>
    <div v-else>
    <img
		dir="right"
		align="right"
        src="../assets/bigdata.jpg"
        height="50"
        width="50"
      >
      <h1>cdQA-annotator</h1>
      
      <hr>
      
      <p align="right" dir="rtl"font="bnazanin">
به سیستم تولید مجموعه داده پرسش‌پاسخ (پ-پ) زبان فارسی خوش آمدید.
        نسخه اولیه این ابزار را میتوان در آدرس
        <a
          href="https://github.com/cdqa-suite/cdQA-annotator"
        >cdQA-annotator</a> مشاهده کرد.
      </p>
      <p align="right" dir="rtl"font="bnazanin">
        برای شروع فایلی مانند 
        <a href="https://rajpurkar.github.io/SQuAD-explorer/">SQuAD v2.0</a>-که هر سند به تعدادی پاراگراف تقسیم شده است نیاز است.
        
      </p>
      <p>
        
      <br>
      <div class="uploadBar">
        <b-form-file
          v-model="file"
          :state="Boolean(file)"
          placeholder="Upload a JSON file..."
          accept=".json"
        ></b-form-file>
      </div>
      <br>
      <b-button :size="''" :variant="'primary'" v-on:click="readFile()">Upload</b-button>
    </div>
  </div>
</template>

<script>
import AnnotationsPage from "./AnnotationsPage.vue";

export default {
  name: "HomePage",
  data: function() {
    return {
      jsonData: {
        data: [
          {
            title: "Question answering",
            paragraphs: [
              {
                context:
                  "Question answering (QA) is a computer science discipline within the fields of information retrieval and natural language processing (NLP), which is concerned with building systems that automatically answer questions posed by humans in a natural language.",
                qas: []
              },
              {
                context:
                  "A QA implementation, usually a computer program, may construct its answers by querying a structured database of knowledge or information, usually a knowledge base. More commonly, QA systems can pull answers from an unstructured collection of natural language documents.",
                qas: []
              }
            ]
          },
          {
            title: "Natural language processing",
            paragraphs: "[...]"
          }
        ]
      },
      fileUploaded: false,
      file: null,
      json: null
    };
  },
  methods: {
    readFile: function() {
      var reader = new FileReader();
      reader.onload = function(event) {
        this.json = JSON.parse(event.target.result);
        this.fileUploaded = true;
      }.bind(this);
      reader.readAsText(this.file);
    }
  },
  components: {
    AnnotationsPage
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.uploadBar {
  max-width: 300px;
  
  height: 100%;
  
  direction:"rtl";
  align:"right";

  
  
}
</style>
