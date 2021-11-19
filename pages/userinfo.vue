<template>
	<div>
		<el-form :model="ruleForm" :rules="rules" ref="ruleForm">
			<el-form-item label="UserName" prop="userName" label-width="100px">
				<el-input v-model="ruleForm.userName" placeholder="please enter the userName." clearable></el-input>
			</el-form-item>
			<br>
			<el-form-item label="Age" prop="age" label-width="100px">
				<el-input type="age" v-model.number="ruleForm.age" placeholder="please enter the age." clearable></el-input>
			</el-form-item>
			<br>
			<el-form-item label="Count" prop="count" label-width="100px">
				<el-input-number v-model="ruleForm.count" controls-position="right" :min="1"></el-input-number>
			</el-form-item>
			<br>
			<el-form-item label="Sex" prop="sex" label-width="100px">
				<el-radio v-model="ruleForm.sex" label="man"></el-radio>
				<el-radio v-model="ruleForm.sex" label="women"></el-radio>
			</el-form-item>		
			<br>
			<el-form-item label="Domicile" prop="city" label-width="100px">
				<el-select v-model="ruleForm.city">
					<el-option v-for="item in ruleForm.cities" :key="item" :value="item" :label="item"></el-option>
				</el-select>
			</el-form-item>		
			<br>
			<el-form-item label="Hobby" prop="checkedHobbies" label-width="100px">
				<el-checkbox :indeterminate="ruleForm.isIndeterminate" v-model="ruleForm.checkAll" @change="handleCheckAllChange">Select all</el-checkbox>
				<el-checkbox-group v-model="ruleForm.checkedHobbies" @change="handleCheckedCitiesChange">
					<el-checkbox v-for="hobby in ruleForm.hobbyOptions" :label="hobby" :key="hobby">{{hobby}}</el-checkbox>
				</el-checkbox-group>
			</el-form-item>	
			<el-form-item label-width="100px">
				<el-button type="primary" @click="submitForm('ruleForm')">Save</el-button>
				<el-button @click="resetForm('ruleForm')">Reset</el-button>
			</el-form-item>
		</el-form>
	</div>
</template>
<script>
import { Form,FormItem,Radio,Select,Option,CheckboxGroup,Checkbox,Button } from 'element-ui';

export default {
  name: 'userinfo',
  components:{
	  [Form.name]:Form,
	  [FormItem.name]:FormItem,
	  [Radio.name]:Radio,
	  [Select.name]:Select,
	  [Option.name]:Option,
	  [CheckboxGroup.name]:CheckboxGroup,
	  [Checkbox.name]:Checkbox,
	  [Button.name]:Button
  },
  layout:"editUserInfo",
  data() {
	  return {
		  ruleForm:{
			userName:'',
			age:'',
			count:1,
			sex:'man',
			cities:['Shenzhen','Guangzhou','Shanghai','Beijing','Tianjin','Taiyuan','Chengdu','Changsha'],
			city:'',
			hobbyOptions:['Sing','Dance','Draw','Swim','Play basketball','Play football','Play tennis','Archery'],
			checkedHobbies:[],
			checkAll:false,
			isIndeterminate:true 
		  },
		  rules:{
			  userName:[
				  {required:true,message:'Please enter username!',trigger:'blur'},
				  { min: 1, max: 20, message: 'The length must be between 3 and 10 characters.', trigger: 'blur' }
			  ],
			  age:[
				  {required:true,message:'Please enter age!',trigger:'blur'},
				  {type:'number',message:'Age must be a numeric value.',trigger:'blur'}
			  ]
		  }	  
	  }
  },
  methods:{
	  handleCheckAllChange(val){
		  this.ruleForm.checkedHobbies = val ? this.ruleForm.hobbyOptions : [];
		  this.ruleForm.isIndeterminate = false;
	  },
	  handleCheckedCitiesChange(val){
		  let checkedCount = val.length;
		  this.ruleForm.checkAll = checkedCount === this.ruleForm.hobbyOptions.length;
		  this.ruleForm.isIndeterminate = checkedCount > 0 && checkedCount < this.ruleForm.hobbyOptions.length;
	  },
	  submitForm(ruleForm){
		  this.$refs[ruleForm].validate((valid) => {
			  if(valid){
				  alert("Submitted successfully.");
			  }else{
				  alert("Verification failed.");
				  return false;
			  }
		  });
	  },
	  resetForm(ruleForm){
		  this.$refs[ruleForm].resetFields();
	  }
  }
};
</script>

