<!--  展现pdf的预览，和输出pdf，输出pdf的逻辑都在exportAsPdf方法中 -->

<template>
    <div class="wrap clearfix" ref="pdfContent">
        <div class="top">
            <h3>不动产登记信息查询记录</h3>
            <div class="QRcodeBox">
                <div class="QRcode">
                  <canvas ref="qrcodeCanvas"></canvas>
                </div>
            <div class="songBolder cdbh">查档编号:<span>{{ receivedMain.number }}</span></div>
            </div>
        </div>
        <div class="dataTable">
            <div class="searchMan"><span>依</span><span class="manName" style="font-weight: bold;">{{ receivedMain.name }}</span><span class="stableSpan">的申请，经查询不动产登记信息平台，结果如下:</span></div>
            <table width="742" class="table1" border="1" cellspacing="0" cellpadding="0">
  <tr>
    <td class="w102"><span class="t3l2">被查询人</span></td>
    <td class="w59"><span class="t3l2">姓名</span></td>
    <td class="w313 valueStyle"><span>{{ receivedMain.name }}</span></td>
    <td class="w78"><span class="t3l2">证件号</span></td>
    <td class="valueStyle"><span>{{ receivedMain.id }}</span></td>
  </tr>
  <tr>
    <td colspan="5" class="tl b0"><span class="t3l2" id="bold">本次不动产信息查询共{{ receivedEstate.length }}条记录，详情如下表：</span></td>
  </tr>
</table>
<table v-for="(item, index) in receivedEstate" :key="index" class="table2"  cellspacing="0" border="1" cellpadding="0">
  <tr>
    <td class="w102"><span class="t3l2">房 {{ index + 1 }} 坐落</span></td>
    <td colspan="4" class="valueStyle"><span >{{ item.estateLocation }}</span></td>
  </tr>
  <tr>
    <td class="w102"><span class="t3l2">权证号</span></td>
    <td colspan="4"  class="valueStyle"><span>{{ item.rightNumber }}</span></td>
  </tr>
  <tr>
    <td><span class="t3l2">不动产单元号</span></td>
    <td colspan="2" class="w89 valueStyle"><span>{{ item.elementNumber }}</span></td>
    <td class="w148"><span class="t3l2">省编号</span></td>
    <td class="w205 valueStyle"><span>{{ item.nationNumber }}</span></td>
  </tr>
  <tr>
    <td rowspan="10"><span class="t3l2 bdczk">不动产状况</span></td>
    <td class="w106"><span class="t3l2">权利人</span></td>
    <td colspan="3" class="valueStyle"><span>{{ item.rightMan }}</span></td>
  </tr>
  <tr>
    <td><span class="t3l2">证件号</span></td>
    <td colspan="3" class="valueStyle"><span>{{ item.rightManId }}</span></td>
  </tr>
  <tr>
    <td><span class="t3l2">面积（㎡）</span></td>
    <td colspan="3" class="valueStyle"><span>{{ item.estateSquare }}</span></td>
  </tr>
  <tr>
    <td><span class="t3l2">用途</span></td>
    <td class="valueStyle">
      <span>{{ 
        item.estatePurpose === 'city' ? '城镇住宅用地/住宅' :
          item.estatePurpose === 'home' ? '住宅' :
          item.estatePurpose === 'nothome' ? '非住宅' : ''
    }}</span></td>
    <td><span class="t3l1">共有情况</span></td>
    <td class="valueStyle">
      <span>
      {{ item.ownershipState === 'only' ? '单独所有' :
         item.ownershipState === 'piece' ? '按份共有' : ''
    }}</span></td>
  </tr>
  <tr>
    <td><span class="t3l2">登记时间</span></td>
    <td class="valueStyle"><span>{{ item.registerStartTime }}</span></td>
    <td><span class="t3l1">转移/注销时间</span></td>
    <td class="valueStyle"><span>{{ item.endTime }}</span></td>
  </tr>
  <tr>
    <td><span class="t3l2">权利状态</span></td>
    <td class="valueStyle"><span>{{ item.rightState }}</span></td>
    <td><span class="t3l1">权利性质</span></td>
    <td class="valueStyle"><span>{{ item.rightProp }}</span></td>
  </tr>
  <tr>
    <td><span class="t3l2">权利类型</span></td>
    <td colspan="3" class="valueStyle"><span>{{ item.rightOption }}</span></td>
  </tr>
  <tr>
    <td><span class="t3l2">使用期限</span></td>
    <td colspan="3" class="valueStyle"><span>{{ item.deadline }}</span></td>
  </tr>
  <tr>
    <td><span class="t3l2">限制状态</span></td>
    <td colspan="3" class="valueStyle"><span>{{ item.limitState }}</span></td>
  </tr>
  <tr>
    <td><span class="t3l2">附记</span></td>
    <td colspan="3" class="valueStyle"><span>{{ item.estateAppendix }}</span></td>
  </tr>
  <tr v-if="item.haveMortgage">
    <td rowspan="5"><span class="dyzk">抵押状况</span></td>
    <td class="h49"><span class="t3l2">抵押权人</span></td>
    <td class="valueStyle"><span>{{ item.banker }}</span></td>
    <td><span class="t3l1">抵押证明号</span></td>
    <td class="valueStyle"><span>{{ item.mortgageNumber }}</span></td>
  </tr>
  <tr v-if="item.haveMortgage">
    <td><span class="t3l2">抵押方式</span></td>
    <td class="valueStyle"><span>{{ item.mortgageWay }}</span></td>
    <td><span class="t3l1">债权数额（万元）</span></td>
    <td class="valueStyle"><span>{{ item.mortgageMoney }}</span></td>
  </tr>
  <tr v-if="item.haveMortgage">
    <td class="h49"><span class="t3l2">登记时间</span></td>
    <td class="valueStyle"><span>{{ item.mortgageStartTime }}</span></td>
    <td><span class="t3l1">债务履行时间</span></td>
    <td class="valueStyle" ><span v-if="item.mortgageRange">{{ formatDateRange(item.mortgageRange) }}</span></td>
  </tr>
  <tr v-if="item.haveMortgage">
    <td colspan="3" class="tl l25"><span class="limit">是否存在禁止或限制转让抵押不动产的约定</span></td>
    <td class="valueStyle"><span>{{ item.limitSell }}</span></td>
  </tr>
  <tr v-if="item.haveMortgage">
    <td><span class="t3l2">附记</span></td>
    <td colspan="3" class="valueStyle"><span>{{ item.mortgageAppendix }}</span></td>
  </tr>
  <tr v-else>
    <td><span class="t3l2">抵押状况</span></td>
    <td colspan="4" class="valueStyle"><span>无</span></td>
  </tr>
  <tr >
    <td><span class="t3l2">查封状况</span></td>
    <td colspan="4" class="valueStyle"><span>{{ item.sealUpState }}</span></td>
  </tr>
  <tr>
    <td><span class="t3l2">居住权状况</span></td>
    <td colspan="4" class="valueStyle"><span>{{ item.liveRight }}</span></td>
  </tr>
</table>
        </div>
        <div class="tl sqyy print">
            <span>该记录依申请用于 
              <span class="purpose">
                {{ receivedMain.searchPurpose == 'xxcx'? '信息查询':
                      receivedMain.searchPurpose == 'znrx'? '子女入学':
                      receivedMain.searchPurpose == 'dk'? '贷款':
                      receivedMain.searchPurpose == 'cq'? '拆迁':
                      receivedMain.searchPurpose == 'hkqy'? '户口迁移':
                      receivedMain.searchPurpose == 'qsjn'? '契税缴纳':
                      receivedMain.searchPurpose == 'sqtc'? '社区停车':
                      receivedMain.searchPurpose == 'ysbz'? '遗失补证':
                      receivedMain.searchPurpose == 'dbcb'? '低保、残保、困难家庭':
                      receivedMain.searchPurpose == 'bdlzf'? '本地廉租房':
                      receivedMain.searchPurpose == 'bzxzf'? '保障性住房':
                      receivedMain.searchPurpose == 'dcqz'? '调查取证':
                      receivedMain.searchPurpose == 'cfzx'? '春风助学': 
                      receivedMain.searchPurpose == 'others'? '其他':'信息查询'       
                }}
              </span>
          </span>
        </div>
        <div class="illustration tl clearfix">
<p>说明</p>
<p>1、本记录查询范围为杭州市不动产登记数据库中的不动产登记信息，本次查询结果与不动产登记簿记载内容不一致的，以不动产登记簿记载内容为准，查询范围：杭州市上城区、拱墅区、西湖区、钱塘区、滨江区、萧山区、余杭区、临平区、富阳区、临安区和淳安县、桐庐县、建德市；</p>
<p>2、本查询记录涉及到萧山区、余杭区、临平区、富阳区、临安区、淳安县、桐庐县、建德市属地不动产查封的，请至属地进一步核实不动产信息。</p>
<p>3、申请人请当场核实以上身份信息和结果信息，如信息有误请及时联系线下不动产登记窗口， 如隐瞒不报或提供虚假信息的，需自行承担法律责任；</p>
<p>4、申请人对以上查询中涉及国家秘密、个人隐私和商业秘密的信息负有保密义务，不得泄漏给他人，也不得不正当使用。</p>
<p>5、本查询记录可通过“浙江政务服务网（http://www.zjzwfw.gov.cn）” 搜索 “不动产智治”，“我要查-权属证明真伪查询 ”功能进行在线验证。</p>
<div class="theEnd clearfix">
  <p class="time">{{ formattedDate }}</p>
  <p class="location">杭州市规划和自然资源局</p>
</div>
</div>
<el-dialog title="生成截图" :visible.sync="iphonepicDialogVisible">
  <pdfViewer />
</el-dialog>
    </div>
    
</template>
  
  <script>
// 导入 jsPDF
import jsPDF from 'jspdf';
import QRCode from 'qrcode'
import 'jspdf-autotable';
import html2canvas from 'html2canvas';
// import pdfViewer from './pdfViewer.vue';

  export default {
    name: 'pdfWeb',
    components: {
      // pdfViewer
  },
    data() {
      return {
        totalPages: 0,     // 总页码
        currentPage: 1,    // 当前页码
        iphonepicDialogVisible: false, //生成图片
    };
  },
  methods:{
    //生成二维码
    generateQRCode() {
    if (this.receivedMain && this.receivedMain.number) {
      setTimeout(() => {
        const canvas = this.$refs.qrcodeCanvas;

        // 设置二维码的宽度和高度限制
        const maxWidth = 70;  // 你想要的最大宽度
        const maxHeight = 70; // 你想要的最大高度

        QRCode.toCanvas(canvas, this.receivedMain.number, {
          width: maxWidth,
          height: maxHeight,
          margin: 0,    // 设置 margin 为 0 去掉白边
          padding: 0,   // 设置 padding 为 0 去掉白边
        }, (error) => {
          if (error) {
            console.error(error);
          } else {
            console.log('QR Code generated successfully');
          }
        });
    }, 0);
    }
  },
  exportAsIphonepic(){
    //打开弹窗
    this.iphonepicDialogVisible = true;
    //初始化数据，文件地址，电池电量，时间
  },
  redrawComponent() {
    // 强制更新组件
    this.$forceUpdate();
  },
  formatDateRange(dateArray) {
      const item = this.receivedEstate[0]; // 假设 receivedEstate 是一个数组
      if (!item || 
          !item.mortgageStartTime || 
          !item.mortgageRange) {
        return "数据加载中...";
      }

      const startDate = new Date(dateArray[0]);
      const endDate = new Date(dateArray[1]);

      const startYear = startDate.getFullYear();
      const startMonth = startDate.getMonth() + 1;
      const startDay = startDate.getDate();

      const endYear = endDate.getFullYear();
      const endMonth = endDate.getMonth() + 1;
      const endDay = endDate.getDate();

      const formattedStartDate = `${startYear}年${startMonth}月${startDay}日`;
      const formattedEndDate = `${endYear}年${endMonth}月${endDay}日`;

      return `${formattedStartDate}至${formattedEndDate}止`;
    },

    async loadData() {
          /* eslint-disable no-unused-vars */
      // For example, you can log the receivedMain and receivedEstate values
      console.log('receivedMain:', this.receivedMain);
      console.log('receivedEstate:', this.receivedEstate);
    },

    //导出pdf
    async exportAsPDF() {
  try {
    this.totalPages = 0;
    this.currentPage = 1;
    const content = this.$refs.pdfContent;

    html2canvas(content, {
      logging: false,
      allowTaint: true,
      taintTest: false,
      useCORS: true,
      dpi: 300,
      scale: 2
    }).then((canvas) => {
      var pdf = new jsPDF('p', 'mm', 'a4');
      //设置页码字体
      
      var ctx = canvas.getContext('2d'),
        a4w = 188, a4h = 275,
        imgHeight = Math.floor(a4h * canvas.width / a4w),
        renderedHeight = 0;

      const totalPages = Math.ceil(canvas.height / imgHeight);
      this.totalPages = totalPages;

      var sealImage = new Image();
      sealImage.src = 'yz.png';

      var bgImage = new Image();
      bgImage.src = 'sy.png';
      //水印bgImage压在图片上，先注释生成没有水印
      
      var numberPages = new Image();

      while (renderedHeight < canvas.height) {
        var page = document.createElement("canvas");
        page.width = canvas.width;
        page.height = Math.min(imgHeight, canvas.height - renderedHeight);
        //page.getContext('2d').globalAlpha = 0.5;

        page.getContext('2d').putImageData(ctx.getImageData(0, renderedHeight, canvas.width, Math.min(imgHeight, canvas.height - renderedHeight)), 0, 0);

        // pdf.setTextColor(0, 0, 0);
        // pdf.text(`${this.currentPage} / ${this.totalPages}`, 170, 290, { font: "song" });
        pdf.addImage(page.toDataURL('image/png', 1), 'PNG', 12, 10, a4w, Math.min(a4h, a4w * page.height / page.width));
        pdf.addImage(bgImage, 'PNG', 12, 15, a4w, a4h - 15);
        
        numberPages.src = `${this.currentPage}-${this.totalPages}.png`;
        pdf.addImage(numberPages, 'PNG', 170, 288, 20, 5.4);

        this.currentPage++;
        renderedHeight += imgHeight;
        
        // 在非最后一页添加章的图片
        if (this.currentPage <= totalPages) {
          pdf.addImage(sealImage, 'PNG', 141, 230, 50, 50);
          pdf.addPage();
        }//最后一页章要在落款上
        else{
          pdf.addImage(sealImage, 'PNG',
          139, 
          Math.floor(Math.min(a4h, a4w * page.height / page.width) - 23 * totalPages + 12) % a4h, 50, 50);
        }
      }
      pdf.save('download.pdf');
    });

  } catch (error) {
    console.error('Error exporting PDF:', error);
  }
},


},
  computed:{
    receivedMain() {
      return this.$store.state.mainMsg;
    },
    receivedEstate() {
      return this.$store.state.estateArr;
    },
    formattedDate() {
    const search_time = this.receivedMain.searchTime;
    const date = new Date(search_time);

    const year = date.getFullYear();
    const month = String(date.getMonth() + 1).padStart(2, '0'); // 月份是从0开始的，所以要加1
    
    const day = date.getDate();
    const hours = String(date.getHours()).padStart(2, '0');
    const minutes = String(date.getMinutes()).padStart(2, '0');
    const seconds = String(date.getSeconds()).padStart(2, '0');

    return `${year}年${month}月${day}日  ${hours}时${minutes}分${seconds}秒`;
  }
    
  },
  watch: {
    /* eslint-disable no-unused-vars */
    'receivedMain.number'(newValue, oldValue) {
      /* eslint-disable no-unused-vars */
      // receivedMain.number 变化时执行 generateQRCode 方法
      this.generateQRCode();
    },
    receivedMain: {
      handler: 'loadData',
      immediate: true // 立即调用加载数据
    },
    receivedEstate: {
      handler: 'loadData',
      immediate: true // 立即调用加载数据
    }
  },
  created() {
    // 在组件挂载后手动设置初始值
    this.$store.commit('setMainMsg', {
      searchPurpose: 'xxcx',
      searchSealup: 'yes',
      name: '',
      id: '',
      number: '',
      searchTime: '',
    });

    // 设置 estateArr 的初始值
    this.$store.commit('setEstateArr', [{
      estateLocation: '',
      rightNumber: '',
      elementNumber: '',
      nationNumber: '',
      rightMan: '',
      rightManId: '',
      estateSquare: '',
      estatePurpose: 'city',
      ownershipState: 'only',
      registerStartTime: '',
      endTime: '/',
      rightState: '',
      rightProp: '',
      rightOption: '',
      deadline: '',
      limitState: '',
      estateAppendix: '',
      haveMortgage:true,
      banker: '',
      mortgageNumber: '',
      mortgageWay: '',
      mortgageMoney: 0,
      mortgageStartTime: "",
      mortgageRange: "",
      mortgageAppendix: "",
      sealUpState: '无',
      limitSell: '/',
      liveRight: '无',
    }]);
  },
  mounted() {
    // 页面加载完毕后生成二维码
    this.generateQRCode();
  }
}
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>
  p{
    margin:0;
    padding:0;
  }
  .wrap{
    height:auto;
    margin: 0 auto;
    width: 742px;
    font-family: song, serif;
    position: relative;
    /* background: url(../assets/sy.jpg);
    background-size: 256px 305px;
    background-position: 229px 208px; */
    border: 1px transparent solid;
    /* border: 1px red solid; */
    font-size: 14.6px;
    /* background: url(../assets/logo.png) no-repeat;
    background-size: 815px 1121px;
    color:red; */
  }
  .exportFix{
    position: absolute;
    top: 0px;
    background: steelblue;
    padding: 7px;
    z-index: 1;
  }
  .exportFix button {
    justify-content: center;
  }
  .exportFix .pagination {
    justify-content: center;
  }
  .top{
    position: relative;
    height:98px;
    padding-top:14px;
  }
  .top h3 {
    margin-top: 30px;
    font-family: song, serif;
    font-size: 21.3px;
    position: relative;
    left: 1px;
    top: 3px;
    font-weight: bold;
  }
  .top .cdbh span{
    margin-top:10px;
    margin-left: 10px;
  }

  .QRcodeBox{
    position: absolute;
    left: 0;
    top: 0px;
    width: 740px;
    height: 106px;
  }
  .QRcodeBox .QRcode{
    width: 70px;
    height:70px;
    display: block;
    right: 22px;
    top: 2px;
    position: absolute;
  }
  .QRcodeBox canvas {
    opacity: 0.8;
  }
  .dataTable {
    position:relative;
    margin-top:12px;
    letter-spacing: 1.1px;
    font-weight:light;
  }
  .dataTable > .searchMan{
    display: flex;
    justify-content: flex-start;
    padding-left: 2px;
    letter-spacing: .1px;
    padding-top: 1px;
  }
  .dataTable > .searchMan span{
    display:inline-flex;
  }
  .dataTable > .searchMan span.stableSpan{
    margin-right: 62px;
  }
  .dataTable > .searchMan .manName{
    height: 20px;
    margin: 0 auto;
  }
  .dataTable table{
    width:742px;
    margin:0;
    line-height:31.5px;
  }
  .dataTable table tr{
    width:742px;
  }
  .dataTable table td{
    position:relative;
    border:.5px solid black;
    margin:0px;
    padding:0;
  }
  .dataTable table td.valueStyle span{
    font-size: 13.3px;
    letter-spacing: 0.3px;
    display: block;
    /* line-height: 1.2; */
    /* word-break: keep-all; */
    /* overflow: hidden; */
    position: relative;
    top:1px;
  }
  .dataTable .table1{
    border-bottom:0px; 
  }
  .dataTable .table1 td.b0{
    /* border-bottom:0px; */
  }
  .dataTable .table2 {
    /* position: relative;
    top:-1px;
    border:0; */
    /* border: 0; */
    border-top: 1px;
    border-bottom: 0;
  }
  .dataTable table:last-child {
    border-bottom: 1px solid black;
  }
  .dataTable td{
    height:31px;
    /* overflow:hidden; */
  }
  .songBolder{
    position: absolute;
    right: 0;
    font-weight: bold;
    font-size: 13.4px;
    bottom: 5px;
  }
  td.w102{
    width:103px;
  }
  td.w59{
    width:59px;
  }
  td.w313{
    width:315px;
  }
  td.w78{
    width:79px;
  }
  td.w217{
    width:217px;
  }
  td.w89{
    width:89px;
  }
  td.w205{
    width:206px;
  }
  td.w148{
    width: 150px;
  }
  td.w106{
    width: 108px;
  }
  td.h49{
    height:49px;
  }
  td.tl, .tl{
    text-align:left;
  }
  td.l25{
    padding-left: 25px;
  }
  .t3l2{
    position: relative;
    top: 3px;
    left: 2px;
    letter-spacing: 1.5px;
  }
  .t3l1{
    position: relative;
    top: 3px;
    left: 1px;
    letter-spacing: 1.5px;
  }
  #bold{
    font-weight:bold;
    letter-spacing:1.2px;
  }
  .bdczk{
    position: relative;
    top: -31px;
    left: 2px;
    letter-spacing: 1.4px;
  }
  .dyzk{
    position: relative;
    top: -4px;
    left: 2px;
    letter-spacing: 1.4px;
  }
  .limit{
    position: relative;
    left: 24px;
    top: 3px;
    letter-spacing: 1.4px;
  }
  .dataStyle{
    position: relative;
    top: 2px;
  }
  .sqyy{
    position: relative;
    margin-top: 12px;
    left: 2px;
  }
  .purpose{
    font-size: 16px;
    font-weight: bold;
    position: relative;
    left: 8px;
    top: -1px;
  }
  .illustration{
    position:relative;
    margin-top: 9px;
    font-size: 13.23px;
    width: 740px;
    border: 1px transparent solid;
  }
  .illustration p{
    letter-spacing: 0.1px;
    line-height:1.22;
    word-wrap: break-word;
  }
  .clearfix::after {
  content: "";
  display: table;
  clear: both;
}
.theEnd{
  position: relative;
    /* right: 0; */
    font-weight: bold;
    text-align: right;
    display: flex;
    flex-direction: column;
    min-height: 120px
}
.theEnd p{ 
  margin-top:5px;
}
.theEnd .time{

}
.theEnd .location {

}
* {
    page-break-before: always;
    page-break-after: always;
    page-break-inside: avoid;
}
@font-face {
  font-family: song;
  src: url(../assets/song.ttf) format("truetype");
  font-weight: normal;
  font-style: normal;
}
      /* eslint-disable no-unused-vars */
  </style>
  
