<template>
  <div class="wrapper">
    <p>民营不动产智治v1.0</p>
    <el-form :model="mainForm" :rules="rules" ref="mainForm" label-width="150px" class="demo-ruleForm">
  <el-form-item label="查档用途" prop="searchPurpose">
    <el-select v-model="mainForm.searchPurpose" placeholder="请选择">
      <el-option label="信息查询" value="xxcx"></el-option>
      <el-option label="子女入学" value="znrx"></el-option>
      <el-option label="贷款" value="dk"></el-option>
      <el-option label="拆迁" value="cq"></el-option>
      <el-option label="户口迁移" value="hkqy"></el-option>
      <el-option label="契税缴纳" value="qsjn"></el-option>
      <el-option label="社区停车" value="sqtc"></el-option>
      <el-option label="遗失补证" value="ysbz"></el-option>
      <el-option label="低保、残保、困难家庭" value="dbcb"></el-option>
      <el-option label="本地廉租房" value="bdlzf"></el-option>
      <el-option label="保障性住房" value="bzxzf"></el-option>
      <el-option label="调查取证" value="dcqz"></el-option>
      <el-option label="春风助学" value="cfzx"></el-option>
      <el-option label="其他" value="others"></el-option>
    </el-select>
  </el-form-item>
  <el-form-item label="是否查询查封" prop="searchSealup">
      <el-select v-model="mainForm.searchSealup" placeholder="请选择">
        <el-option label="是" value="yes"></el-option>
        <el-option label="否" value="no"></el-option>
      </el-select>
  </el-form-item>
  <el-form-item label="查询时间" prop="searchTime">
    <el-date-picker
      v-model="mainForm.searchTime"
      type="datetime"
      placeholder="选择日期时间"
      default-time="12:00:00">
    </el-date-picker>
  </el-form-item>
  <el-form-item label="姓名" prop="name">
    <el-input v-model="mainForm.name"></el-input>
  </el-form-item>
  <el-form-item label="身份证号" prop="id">
    <el-input v-model="mainForm.id"></el-input>
  </el-form-item>
  <el-form-item label="查档编号" prop="number">
    <el-input v-model="mainForm.number"></el-input>
  </el-form-item>
  <el-form-item>
    <el-button type="success" size="medium" round @click="dialogFormVisible = true"> 添加房产 </el-button>
  </el-form-item>
    <template>
  <el-table class="estateList" :data="estateArr"
    style="width: 100%">
    <el-table-column type="expand">
      <template slot-scope="props">
        <el-form label-position="left" inline class="demo-table-expand">
          <el-form-item label="坐落">
            <span>{{ props.row.estateLocation }}</span>
          </el-form-item>
          <el-form-item label="权证号">
            <span>{{ props.row.rightNumber }}</span>
          </el-form-item>
          <el-form-item label="权利人">
            <span>{{ props.row.rightMan }}</span>
          </el-form-item>
          <el-form-item label="证件号">
            <span>{{ props.row.rightManId }}</span>
          </el-form-item>
          <el-form-item label="面积">
            <span>{{ props.row.estateSquare }}</span>
          </el-form-item>
          <el-form-item label="用途">
            <span v-if="props.row.estatePurpose == 'city'">
              城镇住宅用地/住宅
            </span>
            <span v-if="props.row.estatePurpose == 'home'">
              住宅
            </span>
            <span v-if="props.row.estatePurpose == 'nothome'">
              非住宅
            </span>
          </el-form-item>
          <el-form-item label="共有情况">
            <span v-if="props.row.ownershipState == 'only'">
              单独所有
            </span>
          </el-form-item>
          <el-form-item label="登记时间">
            <span>{{ props.row.estateSquare }}</span>
          </el-form-item>
          <el-form-item label="转移/注销时间">
            <span>{{ props.row.estateSquare }}</span>
          </el-form-item>
          <el-form-item label="权利状态">
            <span>{{ props.row.rightState }}</span>
          </el-form-item>
          <el-form-item label="权利性质">
            <span>{{ props.row.rightProp }}</span>
          </el-form-item>
          <el-form-item label="权利类型">
            <span>{{ props.row.rightOption }}</span>
          </el-form-item>
          <el-form-item label="使用期限">
            <span>{{ props.row.deadline }}</span>
          </el-form-item>
          <el-form-item label="限制状态">
            <span>{{ props.row.limitState }}</span>
          </el-form-item>
          <el-form-item label="附记">
            <span>{{ props.row.estateAppendix }}</span>
          </el-form-item>
          <el-form-item label="抵押权人">
            <span>{{ props.row.banker }}</span>
          </el-form-item>
          <el-form-item label="抵押证明号">
            <span>{{ props.row.mortgageNumber }}</span>
          </el-form-item>
          <el-form-item label="抵押方式">
            <span>{{ props.row.mortgageWay }}</span>
          </el-form-item>
          <el-form-item label="债权数额（万元）">
            <span>{{ props.row.mortgageMoney }}</span>
          </el-form-item>
          <el-form-item label="登记时间">
            <span>{{ props.row.registerStartTime }}</span>
          </el-form-item>
          <el-form-item label="债权履行时间">
            <span>{{ props.row.mortgageRange }}</span>
          </el-form-item>
          <el-form-item label="是否存在禁止转让抵押不动产的约定">
            <span>{{ props.row.limitSell }}</span>
          </el-form-item>
          <el-form-item label="附记">
            <span>{{ props.row.mortgageAppendix }}</span>
          </el-form-item>
          <el-form-item label="查封状况">
            <span>{{ props.row.sealUpState }}</span>
          </el-form-item>
          <el-form-item label="居住权状况">
            <span>{{ props.row.liveRight }}</span>
          </el-form-item>

        </el-form>
      </template>
    </el-table-column>

    <el-table-column
      label="序号"
      type="index"
      width="50">
    </el-table-column>
    <el-table-column
      label="坐落"
      prop="estateLocation">
    </el-table-column>
    <el-table-column
      label="权证号"
      prop="rightNumber">
    </el-table-column>
    <el-table-column
      label="权利人"
      prop="rightMan">
    </el-table-column>
    <el-table-column label="操作" style="box-sizing: border-box; display: flex;flex-direction: column;align-items: baseline;">
      <template slot-scope="scope">
          <el-button type="primary" icon="el-icon-edit" size="mini"  @click="handleEdit(scope.$index, scope.row)"></el-button>
          <el-button type="danger" icon="el-icon-delete" size="mini" @click="handleDelete(scope.$index, scope.row)"></el-button>
        </template>
    </el-table-column>
  </el-table>
</template>
<el-form-item class="mt20">
    <el-button type="primary" @click="submitForm('mainForm')">立即创建</el-button>
  </el-form-item>
</el-form>
<!-- 添加不动产 -->
<el-dialog title="添加不动产" :visible.sync="dialogFormVisible">
  <el-form :model="estateForm" :rules="estateRules" ref="estateForm" label-width="50px" class="demo-ruleForm">
    <el-form-item label="坐落" :label-width="formLabelWidth" prop="estateLocation">
      <el-input v-model="estateForm.estateLocation" autocomplete="off"></el-input>
    </el-form-item>
    <el-form-item label="权证号" :label-width="formLabelWidth" prop="rightNumber">
      <el-input v-model="estateForm.rightNumber" autocomplete="off"></el-input>
    </el-form-item>
    <el-form-item label="不动产单元号" :label-width="formLabelWidth" prop="elementNumber">
      <el-input v-model="estateForm.elementNumber" autocomplete="off"></el-input>
    </el-form-item>
    <el-form-item label="省编号" :label-width="formLabelWidth" prop="nationNumber">
      <el-input v-model="estateForm.nationNumber" autocomplete="off"></el-input>
    </el-form-item>
    <el-form-item label="权利人" :label-width="formLabelWidth" prop="rightMan">
      <el-input v-model="estateForm.rightMan" autocomplete="off"></el-input>
    </el-form-item>
    <el-form-item label="（权利人）证件号" :label-width="formLabelWidth" prop="rightManId">
      <el-input v-model="estateForm.rightManId" autocomplete="off"></el-input>
    </el-form-item>
    <el-form-item label="面积（㎡）" :label-width="formLabelWidth" prop="estateSquare">
      <el-input v-model="estateForm.estateSquare" autocomplete="off"></el-input>
    </el-form-item>
    <el-form-item label="用途" :label-width="formLabelWidth" prop="estatePurpose">
      <el-select v-model="estateForm.estatePurpose" placeholder="请选择">
        <el-option label="城镇住宅用地/住宅" value="city"></el-option>
        <el-option label="住宅" value="home"></el-option>
        <el-option label="非住宅" value="nothome"></el-option>
      </el-select>
    </el-form-item>
    <el-form-item label="共有情况" :label-width="formLabelWidth" prop="ownershipState">
      <el-select v-model="estateForm.ownershipState" placeholder="请选择">
        <el-option label="单独所有" value="only"></el-option>
        <el-option label="按份共有" value="piece"></el-option>
      </el-select>
    </el-form-item>
    <el-form-item label="登记日期" :label-width="formLabelWidth" prop="registerStartTime">
      <el-input v-model="estateForm.registerStartTime" placeholder="如【2023年12月10日】" autocomplete="off"></el-input>
    </el-form-item>
    <el-form-item label="转移/注销时间" :label-width="formLabelWidth" prop="endTime">
      <el-input v-model="estateForm.endTime" autocomplete="off"></el-input>
    </el-form-item>
    <el-form-item label="权利状态" :label-width="formLabelWidth" prop="rightState">
      <el-input v-model="estateForm.rightState" autocomplete="off"></el-input>
    </el-form-item>
    <el-form-item label="权利性质" :label-width="formLabelWidth" prop="rightProp">
      <el-input v-model="estateForm.rightProp" autocomplete="off"></el-input>
    </el-form-item>
    <el-form-item label="权利类型" :label-width="formLabelWidth" prop="rightOption">
      <el-input v-model="estateForm.rightOption" autocomplete="off"></el-input>
    </el-form-item>
    <el-form-item label="使用期限" :label-width="formLabelWidth" prop="deadline">
      <el-input v-model="estateForm.deadline" autocomplete="off"></el-input>
    </el-form-item>
    <el-form-item label="限制状态" :label-width="formLabelWidth" prop="limitState">
      <el-input v-model="estateForm.limitState" autocomplete="off"></el-input>
    </el-form-item>
    <el-form-item label="附记" :label-width="formLabelWidth" prop="estateAppendix">
      <el-input v-model="estateForm.estateAppendix" autocomplete="off"></el-input>
    </el-form-item>
    <el-form-item label="查封状态" :label-width="formLabelWidth" prop="sealUpState">
      <el-input v-model="estateForm.sealUpState" autocomplete="off"></el-input>
    </el-form-item>
  <el-form-item label="居住权状况" :label-width="formLabelWidth" prop="nationNumber">
      <el-input v-model="estateForm.liveRight" autocomplete="off"></el-input>
    </el-form-item>
    <el-divider content-position="center">
      「抵押状况」
    </el-divider>
    <el-form-item label="有无抵押" :label-width="formLabelWidth" prop="haveMortgage">
      <el-switch v-model="estateForm.haveMortgage" active-color="#13ce66" inactive-color="#ff4949" active-text="有抵押" inactive-text="无抵押"></el-switch>
    </el-form-item>
      <el-form-item v-show="estateForm.haveMortgage" label="抵押权人" :label-width="formLabelWidth" prop="banker">
      <el-input v-model="estateForm.banker" autocomplete="off" :readonly = "!estateForm.haveMortgage"></el-input>
    </el-form-item>
    <el-form-item v-show="estateForm.haveMortgage" label="抵押证明号" :label-width="formLabelWidth" prop="mortgageNumber">
      <el-input v-model="estateForm.mortgageNumber" autocomplete="off" :readonly = "!estateForm.haveMortgage"></el-input>
    </el-form-item>
    <el-form-item v-show="estateForm.haveMortgage" label="抵押方式" :label-width="formLabelWidth" prop="mortgageWay">
      <el-input v-model="estateForm.mortgageWay" autocomplete="off" :readonly = "!estateForm.haveMortgage"></el-input>
    </el-form-item>
    <el-form-item v-show="estateForm.haveMortgage" label="债权数额（万元）" :label-width="formLabelWidth" prop="mortgageMoney">
      <el-input v-model="estateForm.mortgageMoney" autocomplete="off" :readonly = "!estateForm.haveMortgage"></el-input>
    </el-form-item>
    <el-form-item v-show="estateForm.haveMortgage" label="登记时间" :label-width="formLabelWidth" prop="mortgageStartTime">
      <el-input :readonly = "!estateForm.haveMortgage" v-model="estateForm.mortgageStartTime" placeholder="如【2023年12月10日】" autocomplete="off"></el-input>
    </el-form-item>
    <el-form-item v-show="estateForm.haveMortgage" label="债权履行时间" :label-width="formLabelWidth" prop="mortgageRange">
      <el-date-picker :readonly = "!estateForm.haveMortgage" v-model="estateForm.mortgageRange" type="datetimerange"
      range-separator="至"
      start-placeholder="开始日期"
      end-placeholder="结束日期"
      :default-time="['12:00:00']">
    </el-date-picker>
    </el-form-item>
    <el-form-item v-show="estateForm.haveMortgage" label="是否存在禁止转让抵押不动产的约定"  prop="limitSell" :label-width="formLabelWidth">
      <el-input :readonly = "!estateForm.haveMortgage" v-model="estateForm.limitSell" autocomplete="off"></el-input></el-form-item>
  <el-form-item v-show="estateForm.haveMortgage" label="附记" :label-width="formLabelWidth" prop="mortgageAppendix">
      <el-input  :readonly = "!estateForm.haveMortgage" v-model="estateForm.mortgageAppendix" autocomplete="off"></el-input>
  </el-form-item>
  </el-form>
  <div slot="footer" class="dialog-footer">
    <el-button @click="cancelDialog">取 消</el-button>
    <el-button v-if="this.dialogState == 1" type="primary" @click="UpdateEstate">确认修改</el-button>
    <el-button v-else type="primary" @click="addEstate">添 加</el-button>
  </div>
</el-dialog>
  </div>
</template>

<script>
import Vue from 'vue'
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
      return {
        submitState: 0,//提交过一次就变成1
        formLabelWidth: '180px',
        //estateArr:[],
        estateArr:
        [{
        "estateLocation": "杭州市余杭区中泰街道新明半岛荷园35-1号",
        "rightNumber": "浙(2020)余杭区不动产权第0130664号",
        "elementNumber": "3301101900GB00380F00160001",
        "nationNumber": "BDC330110120209049921946",
        "rightMan": "王洁",
        "rightManId": "330184199205034547",
        "estateSquare": "土地使用权面积109.4㎡/房屋所有权面积141.28㎡",
        "estatePurpose": "city",
        "ownershipState": "only",
        "registerStartTime": "2020年11月02日",
        "endTime": "/",
        "rightState": "现状",
        "rightProp": "出让/存量住房",
        "rightOption": "国有建设用地使用权/房屋（构筑物）所有权",
        "deadline": "2001年04月20日起2071年04月19日止",
        "limitState": "房产:无查封,无抵押",
        "estateAppendix": "/",
        "haveMortgage": false,
        "banker": "",
        "mortgageNumber": "",
        "mortgageWay": "",
        "mortgageMoney": 0,
        "mortgageStartTime": "",
        "mortgageRange": [
            "",
            ""
        ],
        "mortgageAppendix": "无",
        "sealUpState": "无",
        "limitSell": "/",
        "liveRight": "无"
    },
    {
        "estateLocation": "杭州市余杭区中泰街道302号",
        "rightNumber": "余房权证中移字第13219492号、余房权证中移字第13219494号、余房权证中移字第132194923号 / 杭余商用（2013）第15293号",
        "elementNumber": "330110119001GB04246F00080003",
        "nationNumber": "/",
        "rightMan": "王耀连、金文英、王洁",
        "rightManId": "330125196704084510、330125196711085327、330184199205034547",
        "estateSquare": "土地使用权㎡ / 房屋所有权面积282.33㎡",
        "estatePurpose": "nothome",
        "ownershipState": "piece",
        "registerStartTime": "2013年08月14日",
        "endTime": " ",
        "rightState": "现状",
        "rightProp": "/存量房产",
        "rightOption": "房屋（构筑物）所有权",
        "deadline": "/",
        "limitState": "房产：无查封，无抵押，宗地：无查封，无抵押",
        "estateAppendix": "/",
        "haveMortgage": false,
        "banker": "",
        "mortgageNumber": "",
        "mortgageWay": "",
        "mortgageMoney": 0,
        "mortgageStartTime": "",
        "mortgageRange": "",
        "mortgageAppendix": "无",
        "sealUpState": "无",
        "limitSell": "/",
        "liveRight": "无"
    },
    {
        "estateLocation": "余杭区中泰街道新明半岛荷园35幢35-1室",
        "rightNumber": "浙（2017）余杭区不动产证明第0017211号",
        "elementNumber": "33011019002GB00380F00160001",
        "nationNumber": "BDC3301101201705845812",
        "rightMan": "王洁",
        "rightManId": "330184199205034547",
        "estateSquare": "土地使用权面积109.4㎡ / 房屋所有权面积141.28㎡",
        "estatePurpose": "home",
        "ownershipState": "only",
        "registerStartTime": "/",
        "endTime": "/",
        "rightState": "预告登记注销",
        "rightProp": "出让/存量房产",
        "rightOption": "国有建设用地使用权",
        "deadline": "2001年04月20日起2071年04月19日",
        "limitState": "/",
        "estateAppendix": "登记日期：2017年2月8日",
        "haveMortgage": false,
        "banker": "",
        "mortgageNumber": "",
        "mortgageWay": "",
        "mortgageMoney": 0,
        "mortgageStartTime": "",
        "mortgageRange": "",
        "mortgageAppendix": "无",
        "sealUpState": "无",
        "limitSell": "/",
        "liveRight": "无"
    }
],
        mainForm: {
          searchPurpose: 'xxcx',
          searchSealup: 'yes',
          name: '',
          id: '',
          number: '',
          searchTime: '',
        },
        delRowArr: [], //删除的不动产数组
        currentRow: 1,//从1开始，代表当前编辑的是第几行，不用的时候重置1
        dialogFormVisible: false,
        dialogState: 0, //0:添加，1编辑
        // estateForm: {
        //   estateLocation: '',//坐落
        //   rightNumber: '',//权证号
        //   elementNumber: '',//单元号
        //   nationNumber: '',//省编号
        //   rightMan: '',//权利人
        //   rightManId: '',//权利人身份证
        //   estateSquare: '',//面积
        //   estatePurpose: 'city',//用途
        //   ownershipState: 'only',//单独所有
        //   registerStartTime: '',//登记日期
        //   endTime: '/',//转移/注销时间
        //   rightState: '',//权利状态
        //   rightProp:'',//权利性质
        //   rightOption: '',//全力类型
        //   deadline: '',//使用期限
        //   limitState: '',//限制状态
        //   estateAppendix: '',//不动产附记
        //   haveMortgage: true,
        //   banker: '',//债权人
        //   mortgageNumber: '',//抵押证明号
        //   mortgageWay: '',//抵押方式
        //   mortgageMoney: 0,//债权数额（万元）
        //   mortgageStartTime: "",//登记时间
        //   mortgageRange: "",//债务履约时间
        //   mortgageAppendix: "",//抵押附记
        //   sealUpState: '无',//查封状态
        //   limitSell: '/',//禁止转让不动产的约定
        //   liveRight: '无',//居住权
        // },
        estateForm: {
          estateLocation: '杭州市余杭区中泰街道新明半岛荷园35-1号',//坐落
          rightNumber: '浙(2020)余杭区不动产权第0130664号',//权证号
          elementNumber: '3301101900GB00380F00160001',//单元号
          nationNumber: 'BDC330110120209049921946',//省编号
          rightMan: '王洁',//权利人
          rightManId: '330184199205034547',//权利人身份证
          estateSquare: '土地使用权面积109.4㎡/房屋所有权面积141.28㎡',//面积
          estatePurpose: 'city',//用途
          ownershipState: 'only',//单独所有
          registerStartTime: '2020年11月02日',//登记日期
          endTime: '/',//转移/注销时间
          rightState: '现状',//权利状态
          rightProp:'出让/存量住房',//权利性质
          rightOption: '国有建设用地使用权/房屋（构筑物）所有权',//权利类型
          deadline: '2001年04月20日起2071年04月19日止',//使用期限
          limitState: '房产:无查封,无抵押',//限制状态
          estateAppendix: '/', //不动产附记
          haveMortgage: false, //true:有抵押，false:无抵押
          banker: '', //债权人
          mortgageNumber: '', //抵押证明号
          mortgageWay: '', //抵押方式
          mortgageMoney: 0, //债权数额（万元）
          mortgageStartTime: "", //登记时间
          mortgageRange: ["", ""],//债务履约时间
          mortgageAppendix: "无",//抵押-附记
          sealUpState: '无',//查封状态
          limitSell: '/',//抵押-禁止转让不动产的约定
          liveRight: '无',//居住权状况
        },

        estateRules: {
          haveMortgage: [{ required: true, message: '请选择抵押状况', trigger: 'blur' }],
          estateLocation: [{ required: true, message: '请输入坐落', trigger: 'blur' }],
          rightNumber: [{ required: true, message: '请输入权证号', trigger: 'blur' }],
          elementNumber: [{ required: true, message: '请输入单元号', trigger: 'blur' }],
          nationNumber: [{ required: true, message: '请输入省编号', trigger: 'blur' }],
          rightMan: [{ required: true, message: '请输入权利人', trigger: 'blur' }],
          rightManId: [{ required: true, message: '请输入权利人身份证', trigger: 'blur' }],
          estateSquare: [{ required: true, message: '请输入面积（㎡）', trigger: 'blur' }],
          estatePurpose: [{ required: true, message: '请输入用途', trigger: 'blur' }],
          ownershipState: [{ required: true, message: '请输入共有情况', trigger: 'blur' }],
          registerStartTime: [{ required: true, message: '请输入登记日期', trigger: 'blur' }],
          endTime: [{ required: true, message: '请输入转移/注销时间', trigger: 'blur' }],
          rightState: [{ required: true, message: '请输入权利状态', trigger: 'blur' }],
          rightProp:[{ required: true, message: '请输入权利性质', trigger: 'blur' }],
          rightOption: [{ required: true, message: '请输入权利类型', trigger: 'blur' }],
          deadline: [{ required: true, message: '请输入权利类型', trigger: 'blur' }],
          limitState: [{ required: true, message: '请输入闲置状态', trigger: 'blur' }],
          estateAppendix: [{ required: true, message: '请输入附记', trigger: 'blur' }],
          sealUpState: [{ required: true, message: '请输入权利类型', trigger: 'blur' }],
          liveRight: [{ required: true, message: '请输入权利类型', trigger: 'blur' }],
        },
        rules: {
          name: [
            { required: true, message: '请输入姓名', trigger: 'blur' },
            { min: 2, max: 8, message: '长度在 2 到 8 个字符', trigger: 'blur' }
          ],
          id: [
            { required: true, message: '请输入身份证号', trigger: 'blur' },
            { min: 18, max: 18, message: '看看填的是长度18个字符吗', trigger: 'blur' }
          ],
          number: [
            { required: true, message: '请输入查档编号QS3301开头', trigger: 'blur' }
          ],
          searchTime:[
          { required: true, message: '填写查询时间（打印在pdf最后的时间）', trigger: 'blur' }
          ],
          searchSealup: [
            { required: true, message: '选择是否查询查封', trigger: 'blur' }
          ],
          searchPurpose: [
            { required: true, message: '填写查询用途', trigger: 'change' }
          ]
        }
      };
    },

    methods: {
      redrawComponent() {
        // 强制更新组件
        this.$forceUpdate();
      },
      //提交表单
      submitForm(formName) {
        let length = this.estateArr.length;
        this.$refs[formName].validate((valid) => {
          if (valid && length != 0) {
            console.log(this.estateArr);
            console.log(this.mainForm);
            //发送数据
            this.$store.commit('setMainMsg', this.mainForm);
            this.$store.commit('setEstateArr', this.estateArr);
            this.submitState = 1;
          } else {
            console.log('error submit!!');
            return false;
          }
        });
        if(this.estateArr.length == 0){
          this.$message({
            type: 'info',
            message: "添加不动产信息后再提交"
          })
          return;
        }
        
      },
      //添加房产
      addEstate(){
        //验证整个form字段是否合法，形成json对象1，最后清空form里的值
        let estateObj;
        //校准form状态
        this.dialogState = 0;
        this.$refs["estateForm"].validate((valid) => {
          if (valid) {
            //estateObj = {...this.estateForm};
            estateObj = JSON.parse(JSON.stringify(this.estateForm))
            console.log(estateObj)
            this.estateArr.push(estateObj);
            //estateObj = {}
            this.estateForm = {
                estateLocation: '',//坐落
                rightNumber: '',//权证号
                elementNumber: '',//单元号
                nationNumber: '',//省编号
                rightMan: '',//权利人
                rightManId: '',//权利人身份证
                estateSquare: '',//面积
                estatePurpose: 'city',//用途
                ownershipState: 'only',//单独所有
                registerStartTime: '',//登记日期
                endTime: '/',//转移/注销时间
                rightState: '',//权利状态
                rightProp:'',//权利性质
                rightOption: '',//全力类型
                deadline: '',//使用期限
                limitState: '',//限制状态
                estateAppendix: '',//不动产附记
                haveMortgage: true,
                banker: '',//债权人
                mortgageNumber: '',//抵押证明号
                mortgageWay: '',//抵押方式
                mortgageMoney: 0,//债权数额（万元）
                mortgageStartTime: "",//登记时间
                mortgageRange: "",//债务履约时间
                mortgageAppendix: "",//抵押附记
                sealUpState: '无',//查封状态
                limitSell: '/',//禁止转让不动产的约定
                liveRight: '无',//居住权
        },
            this.dialogFormVisible = false;
      
          } else {
            console.log('error submit!!');
            return false;
          }
        });
      },
      handleEdit(index, row){
        //先把row这一行的对象复制给estateObj
        // let estateObj;
        this.dialogState = 1;
        this.currentRow = index;//修改的是哪一行

        this.dialogFormVisible = true;
        this.estateForm = JSON.parse(JSON.stringify(row));//复制到表格中等待修改
      },
      //编辑不动产，确认修改
      UpdateEstate() {
        let index = this.currentRow;
        this.$refs["estateForm"].validate((valid) => {
          if (valid) {
            // 使用 $set 确保 Vue 能够检测到数组元素的变化
            this.$set(this.estateArr, index, 
              JSON.parse(JSON.stringify(this.estateForm))
            );
            this.dialogFormVisible = false;
            this.$message({
              type: 'success',
              message: '修改成功!'
            })
            this.dialogState = 0;
          } else {
            console.log('error submit!!');
            return false;
          }
      });
    },
      //删除处理函数
      handleDelete(index, row){
        //出来确认框
        let delRow = JSON.parse(JSON.stringify(row));
        
        this.$confirm('此操作将删除该不动产, 是否继续?', '提示', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          type: 'warning'
        }).then(() => {
          
          this.estateArr.splice(index, 1);
          if(this.estateArr.length == 0){
            this.estateArr ={
              estateLocation: '',//坐落
                rightNumber: '',//权证号
                elementNumber: '',//单元号
                nationNumber: '',//省编号
                rightMan: '',//权利人
                rightManId: '',//权利人身份证
                estateSquare: '',//面积
                estatePurpose: 'city',//用途
                ownershipState: 'only',//单独所有
                registerStartTime: '',//登记日期
                endTime: '/',//转移/注销时间
                rightState: '',//权利状态
                rightProp:'',//权利性质
                rightOption: '',//全力类型
                deadline: '',//使用期限
                limitState: '',//限制状态
                estateAppendix: '',//不动产附记
                haveMortgage: true,
                banker: '',//债权人
                mortgageNumber: '',//抵押证明号
                mortgageWay: '',//抵押方式
                mortgageMoney: 0,//债权数额（万元）
                mortgageStartTime: "",//登记时间
                mortgageRange: "",//债务履约时间
                mortgageAppendix: "",//抵押附记
                sealUpState: '无',//查封状态
                limitSell: '/',//禁止转让不动产的约定
                liveRight: '无',//居住权
            }
          }
          this.delRowArr.push(delRow);
          this.$message({
            type: 'success',
            message: '删除成功!'
          });
        }).catch(() => {
          this.$message({
            type: 'info',
            message: '已取消删除'
          });          
        });
      },
      //取消对话框
      cancelDialog(){
        this.dialogFormVisible = false;
        //把修改，重置成添加
        this.dialogState = 0;
        //重置表单
      }
      
    },
    watch: {
       /* eslint-disable no-unused-vars */
    "estateForm.haveMortgage"(newValue, oldValue) {
      if (newValue === false) {
        // 当 haveMortgage 为 false 时，清空相关字段
        Vue.set(this.estateForm, 'banker', '');
        Vue.set(this.estateForm, 'mortgageNumber', '');
        Vue.set(this.estateForm, 'mortgageWay', '');
        Vue.set(this.estateForm, 'mortgageMoney', 0);
        Vue.set(this.estateForm, 'mortgageStartTime', '');
        Vue.set(this.estateForm, 'mortgageRange', '');
        Vue.set(this.estateForm, 'limitSell', '/');
        Vue.set(this.estateForm, 'mortgageAppendix', '无');
      }
      // 如果需要在 haveMortgage 为 true 时执行其他逻辑，可以在这里添加代码
    },
    mainForm: {
      handler(newValue, oldValue) {
        if(this.submitState == 0) return;
        //this.redrawComponent();
        this.submitForm('mainForm');
      },
      deep: true  // 这样可以深度监听对象内部属性的变化
    }
  },
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.wrapper{
  margin: 0 auto;
  padding:20px;
  background: aliceblue;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

  .demo-table-expand {
    font-size: 0;
  }
  .demo-table-expand label {
    width: 90px;
    color: #99a9bf;
  }
  .demo-table-expand .el-form-item {
    margin-right: 0;
    margin-bottom: 0;
    width: 50%;
  }
.el-form-item__label{
  font-weight: bolder;
}
table .el-form-item
{border-bottom: 1px solid #ccc;}
.mt20{
  margin-top:20px;
}

</style>
