<template>
  <!-- 页面容器：居中显示 -->
  <div class="container">
    <h1>河南高考志愿推荐系统</h1>
    <!-- Element Plus表单组件 -->
    <el-form 
      :model="form" 
      label-width="120px" 
      class="form-container"
    >
      <!-- 省份选择（默认河南，不可修改） -->
      <el-form-item label="高考省份">
        <el-select v-model="form.province" disabled>
          <el-option label="河南省" value="henan"></el-option>
        </el-select>
      </el-form-item>

      <!-- 分数输入 -->
      <el-form-item label="高考总分" required>
        <el-input 
          v-model="form.score" 
          placeholder="请输入你的高考总分（如580）" 
          type="number"
        ></el-input>
      </el-form-item>

      <!-- 选科选择（新高考适用，可根据实际调整） -->
      <el-form-item label="选考科目">
        <el-select v-model="form.subjects" multiple placeholder="请选择你的选考科目">
          <el-option label="物理" value="physics"></el-option>
          <el-option label="化学" value="chemistry"></el-option>
          <el-option label="生物" value="biology"></el-option>
          <el-option label="历史" value="history"></el-option>
          <el-option label="政治" value="politics"></el-option>
          <el-option label="地理" value="geography"></el-option>
        </el-select>
      </el-form-item>

      <!-- 单科成绩输入（示例：数学、英语） -->
      <el-form-item label="数学成绩">
        <el-input 
          v-model="form.mathScore" 
          placeholder="请输入数学单科成绩" 
          type="number"
        ></el-input>
      </el-form-item>
      <el-form-item label="英语成绩">
        <el-input 
          v-model="form.englishScore" 
          placeholder="请输入英语单科成绩" 
          type="number"
        ></el-input>
      </el-form-item>
      <el-form-item label="语文成绩">
        <el-input 
          v-model="form.englishScore" 
          placeholder="请输入语文单科成绩" 
          type="number"
        ></el-input>
      </el-form-item>


      <!-- 提交按钮 -->
      <el-form-item>
        <el-button type="primary" @click="submitForm">查询可报考院校</el-button>
      </el-form-item>
    </el-form>

    <!-- 新增：分数匹配结果组件 -->
    <ScoreMatch />
  </div>
</template>

<script setup>
// 引入Vue的响应式变量
import { ref } from 'vue'
// 引入Element Plus的消息提示组件
import { ElMessage } from 'element-plus'
// 导入分数匹配组件
import ScoreMatch from './components/ScoreMatch.vue';

// 表单数据：响应式变量，用户输入的内容会存在这里
const form = ref({
  province: 'henan',  // 默认河南
  score: '',          // 高考总分
  subjects: [],       // 选考科目
  mathScore: '',      // 数学成绩
  englishScore: ''    // 英语成绩
})

// 提交表单的函数：点击“查询”按钮时执行
const submitForm = () => {
  // 简单验证：总分不能为空
  if (!form.value.score) {
    ElMessage.error('请输入高考总分！')
    return
  }
  // 验证通过：这里后续会对接云函数，现在先提示输入的内容
  ElMessage.success(`已获取你的信息：总分${form.value.score}分，选科${form.value.subjects.join('、')}`)
  // TODO：后续这里会写代码，把表单数据传给云函数，获取推荐院校
}
</script>

<style scoped>
/* 页面样式：让表单居中、美观 */
.container {
  width: 80%;
  max-width: 800px;
  margin: 50px auto;
  text-align: center;
}
.form-container {
  margin-top: 30px;
  padding: 20px;
  border: 1px solid #eee;
  border-radius: 8px;
}
h1 {
  color: #333;
}
</style>