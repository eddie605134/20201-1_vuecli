<template>
  <div>
    <!-- <button>upload</button> -->
    <label for="upload" class="choose-img">
      選擇圖片上傳
    </label>
    <input 
    type="file" 
    multiple id="upload" 
    style="display: none;" 
    ref="file"
    @change="onChange"
    accept="image/*"/>
    <p class="tip">提示: 一次可以選取多張圖片，最多不超過九張(單張圖片 &lt; 9M)</p>
  </div>
</template>

<script>
export default {
  methods: {
    onChange () {
      //可選鏈
      const newFile = this.$refs?.file?.files
      console.log(newFile);
      if (newFile.length > 9) {
        alert('最多只能9張')
        return false;
      }
      const files = []
      for (const file of newFile) {
        const size = file.size / 1024/ 1024 //把單位變成M
        if (size >1) {
          alert('上船太大')
          return false;
        } 
        files.push(file)
      }
      this.uploadFilesByOSS(files)
    },
    uploadFilesByOSS (files) {

    }
  }
}
</script>

<style scoped>
.choose-img {
  display: block;
  width: 150px;
  height: 50px;
  text-align: center;
  line-height: 50px;
  background-color: #42b983;
  color: aliceblue;
  border-radius: 5px;
  cursor: pointer;
}
.tip {
  color: #ccc;
}
</style>