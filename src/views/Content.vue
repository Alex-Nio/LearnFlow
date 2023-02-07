<template>
  <h1 class="course-title">{{ Title }}</h1>
  <!-- <video-player></video-player> -->

  <div class="lesson">
    <div class="content">
      <!-- Папки -->
      <lesson-folders
        @find="findIndex"
        @open="openFolder"
        :contentFolders="contentFolders"
      ></lesson-folders>

      <!-- Подпапки -->
      <sub-folders
        :has_files="has_files"
        :folderName="folderName"
        :contentFolders="contentFolders"
        :SubFolders="contentSubFolders"
        :targetIndex="targetIndex"
        @find="findIndex"
        @default="defaultOpen"
        :emits="['find', 'default']"
      ></sub-folders>

      <!-- Файлы -->
      <lesson-files
        :contentFiles="contentFiles"
        @find="findIndex"
        @default="defaultOpen"
      ></lesson-files>
    </div>
  </div>
</template>

<script>
import videoPlayer from "@/components/videoPlayer.vue";
import lessonFolders from "@/components/lessonFolders.vue";
import lessonFiles from "@/components/lessonFiles.vue";
import subFolders from "@/components/subFolders.vue";

export default {
  props: {
    courses: {
      type: Object,
      required: true,
    },
    pageName: {
      type: String,
    },
  },
  components: {
    videoPlayer,
    subFolders,
    lessonFiles,
    lessonFolders,
  },
  data() {
    return {
      Title: "Default Title",
      courseContent: [],
      contentFolders: [],
      contentFiles: [],
      contentSubFolders: [],
      contentSubFiles: [],
      fileIndex: null,
      targetIndex: null,
      fileName: "",
      folderName: "",
      rootDirectory: "./assets/data/Курсы",
      source: "",
      has_files: false,
    };
  },
  mounted() {
    this.Title = this.pageName;

    let arr = this.courses.categories;
    let content = this.courseContent;

    for (let i = 0; i < arr.length; i++) {
      let courseContent = arr[i];

      let fullContent = Object.entries(courseContent[1]);
      content.push(fullContent);
    }

    this.courseContent.forEach((item) => {
      for (let i = 0; i < item.length; i++) {
        let lesson = item[i];

        if (lesson[0] === this.pageName) {
          this.contentFolders = lesson[1];

          if (lesson[1]["Файлы"]) {
            this.contentFiles = lesson[1]["Файлы"];
          } else {
            this.contentFiles = ["Файлов нет"];
          }
        }
      }
    });
  },
  methods: {
    findIndex(index) {
      this.targetIndex = index;

      if (typeof index === "number") {
        // console.log("its file");
        this.contentSubFiles = this.contentFolders["Файлы"];
        this.fileIndex = this.contentFolders["Файлы"][index];
        this.fileName = this.fileIndex;
        this.source = `${this.rootDirectory}/${this.Title}/${this.fileName}`;
      } else {
        // console.log("its folder");
        this.folderName = this.contentFolders[index]["Папка"];
        this.contentSubFolders = this.contentFolders[index]["Файлы"];
      }
    },
    openFolder() {
      //TODO: Возможна ошибка связанная с sub-folders
      this.has_files = true;
    },
    defaultOpen(i, marker) {
      if (marker === "folder") {
        this.fileName = this.contentSubFolders[i];
        this.source = `${this.rootDirectory}/${this.Title}/${this.folderName}/${this.fileName}`;
      } else {
        this.source = `${this.rootDirectory}/${this.Title}/${this.fileName}`;
      }

      // logger
      console.log(this.fileName);
    },
  },
};
</script>

<style lang="scss" scoped>
.content {
  position: relative;
}

.course-title {
  font-size: 6rem;
  text-align: center;
}
</style>
