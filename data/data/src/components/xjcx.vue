<template>
  <div class="container">
    <div class="header left">
        <div class="left nav">
            <ul>
              <li ><i class="nav_1"></i><router-link to="/">首页</router-link></li>
              <li><i class="nav_3"></i><router-link to="/fltj">分类统计</router-link></li>
              <li><i class="nav_2"></i><router-link to="/xzqyt">行政区域图</router-link></li>
              <li><i class="nav_4"></i><router-link to="/sqhz">诉求汇总</router-link></li>
              <li><i class="nav_5"></i><router-link to="/xztj">行政统计</router-link></li>
            </ul>
        </div>
        <div class="header_center left" style="position:relative">
            <h2><strong>海城8890民生大数据展示</strong></h2>
        </div>
        <div class="right nav text_right">
          <ul>
            <li><i class="nav_5"></i><router-link to="/wygl">物业管理</router-link></li>
            <li><i class="nav_6"></i><router-link to="/csgn">城市供暖</router-link></li>
            <li  ><i class="nav_7"></i><router-link to="/sbtj">省表统计</router-link></li>
            <li><i class="nav_9"></i><router-link to="/tjyb">诉求统计</router-link></li>
            <li class="nav_active"><i class="nav_10"></i><router-link to="/xjcx">星级查询</router-link></li>
          </ul>
        </div>
    </div>
    <!--内容部分-->
    <div class="con left">
      <!--数据总概-->
      <div class="con_div">
        <div class="con_div_text">
          <span>请选择开始时间:</span><input type="text" id="year" v-model="start"  readonly><span>-</span>
          <span>请选择结束时间:</span><input type="text" id="month" v-model="end"  readonly>
          <span>请选择星级:</span><select class="" name="" value="0星" v-on:change="starSelect($event)">
          <option v-for="item in stars" v-bind:value="item.id">{{item.name}}</option>
          </select>
          <button type="button" name="button" @click="search()">确定</button>
        </div>

      </div>
        <!--统计分析图-->
        <div class="div_any">
            <div class="left div_left_any02">
                <div class="div_any_child">
                    <div class="div_any_title"><img src="../../static/images/title_1.png">星级查询
                      <button type="button" name="button" class="downexcel_xj" @click="exportExcel" style="display:inline">下载</button>
                    </div>
                    <div class="div_any_title"><img src="../../static/images/title_1.png">星级查询
                      <button type="button" name="button" class="downexcel_xj_fh" @click="returnTo_table" style="display:inline">返回</button>
                    </div>

                    <div class="roate-container">
                      <div class="screen-bg"></div>
                      <div id="roate1">
                        <div class="roate-item icon-roate-1"></div>
                        <div class="roate-item"></div>
                        <div class="roate-item"></div>
                        <div class="roate-item"></div>
                        <div class="roate-item icon-roate-2"></div>
                        <div class="roate-item"></div>
                        <div class="roate-item"></div>
                        <div class="roate-item"></div>
                        <div class="roate-item icon-roate-3"></div>
                        <div class="roate-item"></div>
                        <div class="roate-item"></div>
                        <div class="roate-item"></div>
                        <div class="roate-item icon-roate-4"></div>
                        <div class="roate-item"></div>
                        <div class="roate-item"></div>
                        <div class="roate-item"></div>
                      </div>
                      <div id="roate2">
                        <div class="roate-item icon-sq-1"></div>
                        <div class="roate-item"></div>
                        <div class="roate-item"></div>
                        <div class="roate-item"></div>
                        <div class="roate-item"></div>
                        <div class="roate-item"></div>
                        <div class="roate-item icon-sq-2"></div>
                        <div class="roate-item"></div>
                        <div class="roate-item"></div>
                        <div class="roate-item"></div>
                        <div class="roate-item"></div>
                        <div class="roate-item"></div>
                      </div>
                    </div>
                    <div class="table">
                    <table id="tbs1" border="0" align="center" cellpadding="0" cellspacing="1" style="width:1803px">
                      <tr class="ttr" bgcolor="07296d" height="50" align="center" >
                        <td>名次</td>
                        <td>受理单位</td>
                            <td>{{xj}}星</td>
                      </tr>
                      <!-- 数据表格开始 -->
                      <tr align="center" height="36" v-for="item in table1">
                        <td>{{item.ranking}}</td>
                        <td><a  @click="table10($event)" :data-name="item.acceptingUnit">{{item.acceptingUnit}}</a></td>
                            <td>{{item.xx}}</td>
                      </tr>
                      <!-- 数据表格结束 -->
                    </table>
                    <!--二级-->
                    <table  id="tbs20" border="0" align="center" cellpadding="0" cellspacing="1" style="width:1803px">
                      <tr  bgcolor="07296d" height="50" align="center">
                        <td  bgcolor="#07296d" >名次</td>
                        <td  bgcolor="#07296d" >受理单位</td>
                        <td bgcolor="#07296d" >诉求来源</td>
                        <td  bgcolor="#07296d" >诉求日期</td>
                        <td bgcolor="#07296d" >诉求人所在地址</td>
                        <td  bgcolor="#07296d">被诉求单位名称</td>
                        <td  bgcolor="#07296d" >诉求标题</td>
                        <td  bgcolor="#07296d" >诉求定性</td>
                        <td  bgcolor="#07296d" >结案日期</td>
                        <td  bgcolor="#07296d" >群众满意度</td>
                        <td  bgcolor="#07296d" >是否回访</td>
                        <td  bgcolor="#07296d" >最终评星情况</td>
                      </tr>
                      <tr  align="center" height="36" v-for="item in table2">
                        <td >{{item.ranking}}</td>
                        <td><a @click="table20($event)" :data-id="item.id">{{item.sldw}}</a></td>
                        <td >{{item.sqly}}</td>
                        <td >{{item.sqrq}}</td>
                        <td >{{item.sqrszdz}}</td>
                        <td>{{item.bsqdwmc}}</td>
                        <td >{{item.sqbt}}</td>
                        <td >{{item.sqdx}}</td>
                        <td>{{item.jarq}}</td>
                        <td>{{item.qzmyd}}</td>
                        <td>{{item.sfhf}}</td>
                        <td>{{item.zzpxqk}}</td>
                      </tr>
                    </table>
                    <!--三级-->
                    <table  id="tbs30" border="0" align="center" cellpadding="0" cellspacing="1" style="width:1803px">
                      <tr  bgcolor="07296d" height="50" align="center">
                        <td height="70" colspan="2" bgcolor="#07296d" >诉求详细内容</td>
                      </tr>
                      <tr  align="center" height="36" bgcolor="265ca5">
                        <td width="289" align="right" >诉求来源：</td>
                        <td width="1078" align="left" >{{table3['诉求来源']}}</td>
                      </tr>
                      <tr  align="center" height="36" bgcolor="18468e">
                        <td width="289" align="right" >诉求日期：</td>
                        <td align="left" >{{table3['诉求日期']}}</td>
                      </tr>
                      <tr  align="center" height="36" bgcolor="265ca5">
                        <td width="289" align="right" >诉求人姓名：</td>
                        <td align="left" >{{table3['诉求人姓名']}}</td>
                      </tr>
                      <tr  align="center" height="36" bgcolor="18468e">
                        <td width="289" align="right" >诉求人电话：</td>
                        <td align="left" >{{table3['诉求人电话']}}</td>
                      </tr>
                      <tr  align="center" height="36" bgcolor="265ca5">
                        <td width="289" align="right" >诉求人电邮：</td>
                        <td align="left" >{{table3['诉求人电邮']}}</td>
                      </tr>
                      <tr  align="center" height="36" bgcolor="18468e">
                        <td width="289" align="right" >诉求人所在地址：</td>
                        <td align="left" >{{table3['诉求人所在地址']}}</td>
                      </tr>
                      <tr  align="center" height="36" bgcolor="265ca5">
                        <td width="289" align="right" >被诉求单位名称：</td>
                        <td align="left" >{{table3['被诉求单位名称']}}</td>
                      </tr>
                      <tr  align="center" height="36" bgcolor="18468e">
                        <td width="289" align="right" >被诉求单位地址：</td>
                        <td align="left" >{{table3['被诉求单位地址']}}</td>
                      </tr>
                      <tr  align="center" height="36" bgcolor="265ca5">
                        <td width="289" align="right" >诉求标题：</td>
                        <td align="left" >{{table3['诉求标题']}}</td>
                      </tr>
                      <tr  align="center" height="36" bgcolor="18468e">
                        <td width="289" align="right" >诉求内容：</td>
                        <td align="left" class="sqnr">{{table3['诉求内容']}}</td>
                      </tr>
                      <tr  align="center" height="36" bgcolor="265ca5">
                        <td width="289" align="right" >承办人：</td>
                        <td align="left" >{{table3['承办人']}}</td>
                      </tr>
                      <tr  align="center" height="36" bgcolor="18468e">
                        <td width="289" align="right" >诉求性质：</td>
                        <td align="left" >{{table3['诉求性质']}}</td>
                      </tr>
                      <tr  align="center" height="36" bgcolor="265ca5">
                        <td width="289" align="right" >办理方式：</td>
                        <td align="left" >{{table3['办理方式']}}</td>
                      </tr>
                      <tr  align="center" height="36" bgcolor="18468e">
                        <td width="289" align="right" >办理部门：</td>
                        <td align="left" >{{table3['办理部门']}}</td>
                      </tr>
                      <tr  align="center" height="36" bgcolor="265ca5">
                        <td width="289" align="right" >办理分类：</td>
                        <td align="left" >{{table3['办理分类']}}</td>
                      </tr>
                      <tr  align="center" height="36" bgcolor="18468e">
                        <td width="289" align="right" >被诉求单位的行业主管部门：</td>
                        <td align="left" >{{table3['被诉求单位的行业主管部门']}}</td>
                      </tr>
                      <tr  align="center" height="36" bgcolor="265ca5">
                        <td width="289" align="right" >一级定性：</td>
                        <td align="left" >{{table3['一级定性']}}</td>
                      </tr>
                      <tr  align="center" height="36" bgcolor="18468e">
                        <td width="289" align="right" >二级定性：</td>
                        <td align="left" >{{table3['二级定性']}}</td>
                      </tr>
                      <tr  align="center" height="36" bgcolor="265ca5">
                        <td width="289" align="right" >三级定性：</td>
                        <td align="left" >{{table3['三级定性']}}</td>
                      </tr>
                      <tr  align="center" height="36" bgcolor="18468e">
                        <td width="289" align="right" >是否重复反应问题：</td>
                        <td align="left" >{{table3['是否重复反应问题']}}</td>
                      </tr>
                      <tr  align="center" height="36" bgcolor="265ca5">
                        <td width="289" align="right" >是否为无效件：</td>
                        <td align="left" >{{table3['是否为无效件']}}</td>
                      </tr>
                      <tr  align="center" height="36" bgcolor="18468e">
                        <td width="289" align="right" >分派时间：</td>
                        <td align="left" >{{table3['分派时间']}}</td>
                      </tr>
                      <tr  align="center" height="36" bgcolor="265ca5">
                        <td width="289" align="right" >报结案时间：</td>
                        <td align="left" >{{table3['报结案时间']}}</td>
                      </tr>
                      <tr  align="center" height="36" bgcolor="18468e">
                        <td width="289" align="right" >解决情况详情：</td>
                        <td align="left" class="jjqkxq">{{table3['解决情况详情']}}</td>
                      </tr>
                      <tr  align="center" height="36" bgcolor="265ca5">
                        <td width="289" align="right" >公示内容：</td>
                        <td align="left" class="gsnr">{{gsnr}}</td>
                      </tr>
                      <tr  align="center" height="36" bgcolor="18468e">
                        <td width="289" align="right" >群众满意度：</td>
                        <td align="left" >{{table3['群众满意度']}}</td>
                      </tr>
                      <tr  align="center" height="36" bgcolor="265ca5">
                        <td width="289" align="right" >回访内容：</td>
                        <td align="left" class="hfnr">{{hfnr}}</td>
                      </tr>
                      <tr  align="center" height="36" bgcolor="18468e">
                        <td width="289" align="right" >审核状态：</td>
                        <td align="left" >{{table3['审核状态']}}</td>
                      </tr>
                      <tr  align="center" height="36" bgcolor="265ca5">
                        <td width="289" align="right" >评星：</td>
                        <td align="left" >{{table3['评星']}}</td>
                      </tr>
                      <tr  align="center" height="36" bgcolor="18468e">
                        <td width="289" align="right" >加星：</td>
                        <td align="left" >{{table3['加星']}}</td>
                      </tr>
                      <tr  align="center" height="36" bgcolor="265ca5">
                        <td width="289" align="right" >减星：</td>
                        <td align="left" >{{table3['减星']}}</td>
                      </tr>
                      <tr  align="center" height="36" bgcolor="18468e">
                        <td width="289" align="right" >推荐选项：</td>
                        <td align="left" >{{table3['推荐选项']}}</td>
                      </tr>
                      <tr  align="center" height="36" bgcolor="265ca5">
                        <td width="289" align="right" >延期申请日期：</td>
                        <td align="left" >{{table3['延期申请日期']}}</td>
                      </tr>
                      <tr  align="center" height="36" bgcolor="18468e">
                        <td width="289" align="right" >延期结束日期：</td>
                        <td align="left" >{{table3['延期结束日期']}}</td>
                      </tr>
                      <tr  align="center" height="36" bgcolor="265ca5">
                        <td width="289" align="right" >延期理由：</td>
                        <td align="left" >{{table3['延期理由']}}</td>
                      </tr>
                      <tr  align="center" height="36" bgcolor="18468e">
                        <td width="289" align="right" >退件标志：</td>
                        <td align="left" >{{table3['退件标志']}}</td>
                      </tr>
                      <tr align="center" height="36" bgcolor="265ca5">
                        <td width="289" align="right">退件理由：</td>
                        <td align="left" >{{table3['退件理由']}}</td>
                      </tr>
                      <tr align="center" height="36" bgcolor="18468e">
                        <td width="289" align="right">退件日期：</td>
                        <td align="left">{{table3['退件日期']}}</td>
                      </tr>
                      <tr align="center" height="36" bgcolor="265ca5">
                        <td width="289" align="right" >最终办理部门：</td>
                        <td align="left">{{table3['最终办理部门']}}</td>
                      </tr>
                    </table>
                  </div>
                    </div>

                </div>
            </div>
        </div>
    </div>
  </div>
</template>
<script>
import {getNowFormatDate,getLastFormatDate} from "../utils/utils.js"
import {get} from "../utils/request.js"
import {loading} from "../../static/js/index.js"
import {loading_01} from "../../static/js/jquery.min.js"
import {export_table_to_excel} from "../excel/Export2Excel.js"
export default {
  name: 'xjcx',
  data () {
    return {
      current:0,
      start: '2019-05-13',
      end: '2019-06-13',
      laydate_month:window.laydate,
      reportForm:[],
      laydate_month:window.laydate,
      stars:[{id:0,name:'0星'},{id:1,name:'1星'},{id:2,name:'2星'},{id:3,name:'3星'},{id:4,name:'4星'},{id:5,name:'5星'},
            {id:10,name:'10星'},{id:15,name:'15星'},{id:20,name:'20星'},{id:25,name:'25星'},
      ],
      star:0,
      xj:0,
      table1:[],
      table2:[],
      table3:[],
      type_table:1,
      cid:121312,
      sldw:'',
      gsnr:'',
      hfnr:'',
    }
  },

  mounted(){
      this.loading();
      this.loading_01();
      $('.roate-container').show();
      $("#tbs1").hide();
      $("#tbs20").hide();
      $("#tbs30").hide();
      $(".downexcel_xj").hide();
      $(".downexcel_xj_fh").hide();

    this.start = this.getLastFormatDate();
    this.end = this.getNowFormatDate();

    //8890海城各部门诉求办理情况汇总报表
    this.get(host.url+'/starlevel',{start:this.start,end:this.end,star:this.star}).then((res)=>{
      $('.roate-container').hide();
      $(".downexcel_xj").show();
      $(".downexcel_xj_fh").show();
      $("#tbs1").show();
      for(var i =0;i<res.data.length;i++){
        res.data[i] = {
          ranking:res.data[i]['名次'],
          acceptingUnit:res.data[i]['受理单位'],
          xx:res.data[i]['星'],
        };
      }
      this.table1 = res.data

    })

    this.laydate_month.render({
        elem: '#year',
        type: 'date',
        theme: '#034c6a',
        done: (value) => {
          this.start = value
        }
    })
    this.laydate_month.render({
        elem: '#month',
        type: 'date',
        theme: '#034c6a',
        done: (value) => {
          this.end = value
        }
    })
  },
  updated(){
    this.rows();
    this.tablecolor();
  },
  //updated:{},
  methods:{
    get,
    getLastFormatDate,
    getNowFormatDate,
    loading,
    loading_01,
    export_table_to_excel,
    //表格颜色
    //二级分类
    table10(e){
      this.loading();
      this.loading_01();
      $('.roate-container').show();
      $('.table').show();
      this.type_table = 2;
      this.tablecolor();
      this.sldw = e.target.dataset.name;
      $("#tbs1").hide();
      $("#tbs30").hide();

      this.get(host.url+'/starlevellist',{start:this.start,end:this.end,sldw:e.target.dataset.name,star:this.star}).then((res)=>{
        $(".downexcel_xj_fn").show();
        $(".downexcel_xj").show();
        //console.log('yta',res)
        this.loading();
        this.loading_01();
        $('.roate-container').hide();
        $('.table').show();
        if(res.data[1] == '暂无数据'){
          $(".wsj").show();
          $("#tbs20").hide();
        }else{
          $(".wsj").hide();
          $("#tbs20").show();
          for(var i =0;i<res.data.length;i++){
            res.data[i] = {
              id:res.data[i].id,
              ranking:res.data[i]['名次'],
              sldw:res.data[i]['受理单位'],
              sqly:res.data[i]['投诉来源'],
              sqrq:res.data[i]['诉求日期'],
              sjrszdz:res.data[i]['诉求人所在地址'],
              bsqdwmc:res.data[i]['被诉求单位名称'],

              sqbt:res.data[i]['诉求标题'],
              sqdx:res.data[i]['三级定性'],
              jarq:res.data[i]['结案日期'],
              qzmyd:res.data[i]['群众满意度'],
              sfhf:res.data[i]['是否回访'],
              zzpxqk:res.data[i]['最终评星情况'],
            };
          }
          this.table2 = res.data
          //console.log('112131',res)
        }

      })
    },
    //三级分类
    table20(e){
      this.loading();
      this.loading_01();
      $('.roate-container').show();
      $('.table').show();
      this.type_table = 3;
      this.cid = e.target.dataset.id;
      $("#tbs1").hide();
      $("#tbs20").hide();
      $("#tbs30").hide();

      //console.log('id',e);
      this.get(host.url+'/starlevelinfo',{id:e.target.dataset.id}).then((res)=>{
        $(".downexcel_xj_fn").show();
        $(".downexcel_xj").show();
        this.loading();
        this.loading_01();
        $('.roate-container').hide();
        $("#tbs30").show();
          //console.log('yta',res)
          $('.gsnr').html(res.data['公示内容'])
          $('.hfnr').html(res.data['回访内容'])
          $('.jjqkxq').html(res.data['解决情况详情'])
          $('.sqnr').html(res.data['诉求内容'])
          this.table3 = res.data
      })
    },
    rows:function(){
      var tbs = document.getElementById("tbs1");
      var rows = tbs.getElementsByTagName("tr");
      for(let i=1;i<rows.length;i++){
        if(i%2==0) {
          rows[i].style.backgroundColor="#18468e";

        } else  {
          rows[i].style.backgroundColor="#265ca5";
        }
      }
    },
    tablecolor:function (){
      var tbs20 = document.getElementById("tbs20");
      var rows20 = tbs20.getElementsByTagName("tr");
      for(let i=1;i<rows20.length;i++){
        if(i%2==0) {
          rows20[i].style.backgroundColor="#18468e";
        } else  {
          rows20[i].style.backgroundColor="#265ca5";
        }
      }
    },
    starSelect(e){
      this.star = event.target.value
      //console.log(this.star)
    },
      //点击确定查询
      search:function(){
        this.type_table = 1
        $('.roate-container').show();
        $('.downexcel').hide();
        this.xj = this.star;
        //星级查询
        this.get(host.url+'/starlevel',{start:this.start,end:this.end,star:this.star}).then((res)=>{
          $('.roate-container').hide();
          $(".downexcel_xj").show();
          $(".downexcel_xj_fh").show();
          $("#tbs1").show();
          for(var i =0;i<res.data.length;i++){
            res.data[i] = {
              ranking:res.data[i]['名次'],
              acceptingUnit:res.data[i]['受理单位'],
              xx:res.data[i]['星'],
            };
          }
          this.table1 = res.data

        })
        this.rows();

      },
      //返回
      returnTo_table(e){
        if(this.type_table == 1){
          return
        }else if(this.type_table == 2){
          $(".wsj").hide();

          $('.table').show();
          $('.roate-container').show();
          this.rows();
          this.type_table = 1
          $("#tbs1").hide();
          $("#tbs20").hide();
          $("#tbs30").hide();

          this.get(host.url+'/starlevel',{start:this.start,end:this.end,star:this.star}).then(res=>{
            $(".downexcel_xj_fh").show();
            $(".downexcel_xj").show();
            this.loading();
            this.loading_01();
            $('.roate-container').hide();
            if(res.data[1] == '暂无数据'){
              $(".wsj").show();
              $("#tbs1").hide();
            }else{
              $(".wsj").hide();
              $("#tbs1").show();
              for(var i =0;i<res.data.length;i++){
                res.data[i] = {
                  ranking:res.data[i]['名次'],
                  acceptingUnit:res.data[i]['受理单位'],
                  xx:res.data[i]['星'],
                };
              }
              this.table1 = res.data
              //console.log('112131',res)
            }

          })

        }else if(this.type_table == 3){
          $(".wsj").hide();
          this.loading();
          this.loading_01();
          $('.table').show();
          $('.roate-container').show();

          this.tablecolor();
          this.type_table = 2
          $("#tbs1").hide();
          $("#tbs20").hide();
          $("#tbs30").hide();

          this.get(host.url+'/starlevellist',{start:this.start,end:this.end,sldw:this.sldw,star:this.star}).then((res)=>{
            $(".downexcel_xj_fh").show();
            $(".downexcel_xj").show();
            //console.log('yta',res)
            this.loading();
            this.loading_01();
            $('.roate-container').hide();
            if(res.data[1] == '暂无数据'){
              $(".wsj").show();
              $("#tbs20").hide();
            }else{
              for(var i =0;i<res.data.length;i++){
                $("#tbs20").show();
                res.data[i] = {
                  id:res.data[i].id,
                  ranking:res.data[i]['名次'],
                  sldw:res.data[i]['受理单位'],
                  sqly:res.data[i]['投诉来源'],
                  sqrq:res.data[i]['诉求日期'],
                  sjrszdz:res.data[i]['诉求人所在地址'],
                  bsqdwmc:res.data[i]['被诉求单位名称'],

                  sqbt:res.data[i]['诉求标题'],
                  sqdx:res.data[i]['三级定性'],
                  jarq:res.data[i]['结案日期'],
                  qzmyd:res.data[i]['群众满意度'],
                  sfhf:res.data[i]['是否回访'],
                  zzpxqk:res.data[i]['最终评星情况'],
                };
              }
              this.table2 = res.data
              //console.log('112131',res)
            }

          })
        }
      },
      //导出cxcel
      exportExcel(){

        if(this.type_table == 1){
          require.ensure([], () => {
            const { export_json_to_excel } = require('../excel/Export2Excel'); //这里必须使用绝对路径
            const tHeader = ['名次','受理单位', this.star + '星'
                              ]//表头信息
            const filterVal = ['ranking','acceptingUnit','xx'
                              ]//对应表头的字段名
            const list = this.table1;
            const data = this.formatJson(filterVal, list);
            export_json_to_excel(tHeader, data, '海城市各单位分类表（一级定性）');// 导出的表格名称，根据需要自己命名
          })
        }else if(this.type_table == 2){
          require.ensure([], () => {
            const { export_json_to_excel } = require('../excel/Export2Excel'); //这里必须使用绝对路径
            const tHeader = ['名次','受理单位','诉求来源', '诉求日期', '诉求人所在地址', '被诉求单位名称','诉求标题',
                              '诉求定性', '结案日期', '群众满意度', '是否回访', '最终评星情况'
                              ]//表头信息
            const filterVal = ['ranking','sldw','sqly', 'sqrq', 'sqrszdz', 'bsqdwmc','sqbt',
                              'sqdx', 'jarq', 'qzmyd', 'sfhf', 'zzpxqk'
                              ]//对应表头的字段名
            const list = this.table2;
            const data = this.formatJson(filterVal, list);
            export_json_to_excel(tHeader, data, '海城市各单位分类表（二级定性）');// 导出的表格名称，根据需要自己命名
          })
        }else if(this.type_table == 3){
          require.ensure([], () => {
            this.export_table_to_excel('tbs30');// 导出的表格名称，根据需要自己命名
          })

        }
     },
     formatJson(filterVal, jsonData){
     	return jsonData.map(v =>{
    	  return filterVal.map(j => v[j])
        })
     },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style src="" scoped>
  @import "../../static/css/style.css";
    @import '../../static/css/index.css';
</style>
