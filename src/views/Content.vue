<template>
  <h1 class="course-title">{{ Title }}</h1>

  <!-- <video-player></video-player> -->

  <div class="root">
    <div class="content">
      <!-- Папки в корне урока -->
      <lesson-folders
        @find="findIndex"
        @open="openFolder"
        :courseRootFiles="courseRootFiles"
      ></lesson-folders>

      <!-- Файлы по дефолту в корне -->
      <files-in-root
        :inRootFiles="inRootFiles"
        @find="findIndex"
        @srcCreate="sourceCreator"
      ></files-in-root>
    </div>

    <!-- Файлы и папки внутри папки урока -->
    <files-in-folders
      :has_files="has_files"
      :folderName="folderName"
      :courseRootFiles="courseRootFiles"
      :inFolderFiles="inFolderFiles"
      :inFolderFolders="inFolderFolders"
      :targetIndex="targetIndex"
      @findSubFiles="findSubFiles"
      @srcCreate="sourceCreator"
      :emits="['find', 'default']"
    ></files-in-folders>

    <!-- TODO: Подапки -->
    <subfolders-in-folders
      :filtredSubFiles="filtredSubfolderContentFiles"
      :filtredSubFolders="filtredSubfolderContentFolders"
    ></subfolders-in-folders>
  </div>
</template>

<script>
import videoPlayer from "@/components/videoPlayer.vue";
import lessonFolders from "@/components/lessonFolders.vue";
import filesInRoot from "@/components/filesInRoot.vue";
import filesInFolders from "@/components/filesInFolders.vue";
import subfoldersInFolders from "@/components/subfoldersInFolders.vue";
import defaultPopup from "@/components/defaultPopup.vue";
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
    filesInFolders,
    filesInRoot,
    lessonFolders,
    subfoldersInFolders,
    defaultPopup,
  },
  data() {
    return {
      Title: "Default Title",
      // Data-файл
      courseData: [],
      // Корень курса: Папки и Файлы
      courseRootFiles: [],
      // Только файлы в корне
      inRootFiles: [],
      // файлы в папке
      inFolderFiles: [],
      // Папки внутри папки курса
      inFolderFolders: [],
      // Контент в подпапке
      subfolderContentFiles: [],
      // Отфильтрованное содержимое подпапки
      filtredSubfolderContentFiles: [],
      filtredSubfolderContentFolders: [],
      // Индекс файла или папки
      fileIndex: null,
      targetIndex: null,
      fileName: "",
      folderName: "",
      subfolderName: "",
      rootDirectory: "./assets/data/Курсы",
      source: "",
      has_files: false,
      has_more_folders: false,
    };
  },
  mounted() {
    if (this.$route.path != "/") {
      window.removeEventListener("wheel", this.onSlideChange, this.onSwiper);
    }

    this.Title = this.pageName;

    let arr = this.courses.categories;
    let content = this.courseData;

    for (let i = 0; i < arr.length; i++) {
      let courseData = arr[i];

      let fullContent = Object.entries(courseData[1]);
      content.push(fullContent);
    }

    this.courseData.forEach((item) => {
      for (let i = 0; i < item.length; i++) {
        let lesson = item[i];

        if (lesson[0] === this.pageName) {
          this.courseRootFiles = lesson[1];

          if (lesson[1]["Файлы"]) {
            this.inRootFiles = lesson[1]["Файлы"];
          }
        }
      }
    });
  },
  methods: {
    findIndex(index) {
      this.targetIndex = index;

      if (typeof index === "number") {
        console.log("its file");
        this.fileIndex = this.courseRootFiles["Файлы"][index];
        this.fileName = this.fileIndex;
        this.source = `${this.rootDirectory}/${this.Title}/${this.fileName}`;
      } else {
        console.log("its folder");

        // Если внутри папки есть ещё папки
        if (Object.entries(this.courseRootFiles[index]).length > 2) {
          console.log("Есть подпапки");

          // Находим подпапки
          let moreFolders = Object.keys(this.courseRootFiles[index]).filter(
            (item) => item !== "Папка" && item !== "Файлы"
          );

          this.inFolderFolders = moreFolders;
          this.has_more_folders = true;
          // moreFolders.forEach((folder) => {
          //   console.log(this.courseRootFiles[index][folder]["Папка"]);
          // });
        } else {
          this.has_more_folders = false;
          this.inFolderFolders = null;
        }

        this.folderName = this.courseRootFiles[index]["Папка"];
        this.inFolderFiles = this.courseRootFiles[index]["Файлы"];
      }
    },
    openFolder(i, folder) {
      console.log("Открыта папка " + i);
      this.subfolderContentFiles = folder;

      console.log(this.courseRootFiles);
      //TODO: Возможна ошибка связанная с sub-folders
      this.has_files = true;
    },
    sourceCreator(i, marker, item) {
      this.subfolderName = item;

      if (marker === "subfile") {
        this.fileName = this.inFolderFiles[i];
        this.source = `${this.rootDirectory}/${this.Title}/${this.folderName}/${this.fileName}`;
      } else if (marker === "subfolder") {
        this.source = `${this.rootDirectory}/${this.Title}/${this.subfolderName}/ИМЯ ФАЙЛА`;
      }

      // logger
      console.log(this.source);
    },
    findSubFiles(i, item) {
      // console.log(this.subfolderContentFiles[item]);
      let mutation = Object.entries(this.subfolderContentFiles[item]);
      let subContentFiles = [],
        subContentFolders = [];

      for (const [key, value] of mutation) {
        if (key !== "Папка") {
          if (key == "Файлы") {
            subContentFiles.push(value);
          } else {
            subContentFolders.push(value);
          }
        }
      }

      this.filtredSubfolderContentFiles = subContentFiles;
      this.filtredSubfolderContentFolders = subContentFolders;
    },
  },
};
</script>

<style lang="scss" scoped>
.content {
  width: 100%;
  position: relative;
}

.root {
  display: flex;
  flex-direction: column;
  width: 100%;
  max-width: 100%;
}

.course-title {
  font-size: 4rem;
  text-align: center;
  margin-bottom: 45px;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
