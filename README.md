# angular-ionic
App =>

//版本不同 使用npm命令行

//卸载ionic的版本

npm uninstall ionic -g 

//安装ionic某个版本

npm install -g ionic@3.20

//新建项目文件：

$ ionic start myApp（文件名） tabs

//从gitlab下载项目 

git clone url(gitlab文件的url)

//新下载的项目 要安装 node_modules

npm install

//查看本地代码和gitlab上的代码文件状态

git status

//上传，拉代码 

git add .   //添加改动的所有文件

//上传，拉代码：如果有冲突

git commit -m "注释词语"

//拉代码，合并分支 

git pull  //一般都是用这行命令

//上传代码
git push

//获取分支 
git fetch origin master:tmp

//合并分支
git merge temp

//git回滚到任意版本
git reset --hard e377f60e28c8b84158（版本号）

//新建一个页面：
ionic g  page 文件名

//app.module.ts 引入声明组件

//引入components模块

import { ComponentsModule } from '../components/components.module'; 

//页面 自定义的组件

import { NewsPage } from '../pages/news/news';

//ios和安卓统一样式设计

//操作方法为：在根模块里面也就是app.module.ts里面设置

 imports: [
 
    BrowserModule,
    
    IonicModule.forRoot(MyApp,{
    
      backButtonText: ' ', iconMode: 'ios',//安卓icon强制使用ios的icon以及样式
      
      mode: 'ios',//样式强制使用ios样式
      
    })
  ],

//点击事件

<button ion-button (click)="goNews()">跳转到新闻页面</button>

//home.ts页面引入这个组件，跳转

import { NewsPage } from '../news/news';

goNews(){

    // this.navCtrl.push(页面)
    
    this.navCtrl.push(NewsPage);
}

//ionic html页面 跳转页面传参

[navPush] = "PaymentPage" [navParams] = "{itemId:item.id,itemType:item.type}"

//ionic3 常见的生命周期

ionViewDidLoad  （当页面加载的时候触发，仅在页面创建的时候触发一次，如果被缓存了，那么下次再打开这个页面则不会触发）

ionViewWillEnter   （顾名思义，当将要进入页面时触发）

ionViewDidEnter   （当进入页面时触发）

ionViewWillLeave    （当将要从页面离开时触发）

ionViewDidLeave    （离开页面时触发）

ionViewWillUnload   （当页面将要销毁同时页面上元素移除时触发）

使用方法 =>  ionViewDidLoad  （）{ }

//ionic3 绑定事件 =>样式

//写在html行内样式

//[style.属性]="判断值=='何值' " ？'样式一(true)' ：'样式二(false)'

[style.font-weight]="pet == 'cz' ? '600' : '400'" 

//设置不同手机显示状态

<span showWhen="ios">取消</span>

<ion-icon showWhen="android"name="md-close"></ion-icon>

//ionic3 angular 

//管道 时间戳转换 在html页面写

{{ 时间数 | date: "yyyy-MM-dd HH:mm:ss" }}

//管道 保留两位小数 在html页面写

{{ 数值 | number: "1.2-2" }}   =>2-2是最多两位数，最少两位数 

//接口要导入   

import { ApiProvider } from '../../providers/api/api'

let loader = this.api.loading() //加载框（请求数据转圈圈）

loader.dismiss() //闭加载框

//图形验证码要导入   

import { BaseuiProvider } from '../../providers/baseui/baseui'

//ionic3 接口对接  在ts文件写

接口名（）{

  this.api.接口名（）.subscribe(
  
     （res:any）=>{
     
          if(res.status === "0000"){  //0000是后台传的状态值
	  
             this.接口赋值名（自己取）= res.data.list   //list是后台传过来的参数
	     
          }
	  
       }
       
  )
  
}

//ionic3 获取图形验证码

接口名（）{

  this.api.接口名（）.subscribe（
  
      (res:any) =>{
      
         if(res.status === '0000'){
	 
	this.接口赋值名（自己取）= this.sanitizer.bypassSecurityTrustResourceUrl(res.data.base64Img)
	
	this.接口赋值名（自己取） = res.data.verifyCodeId  //verifyCodeId是后台传过来的参数
	
         }
	 
      }
      
  ）
  
}

//ionic3  返回几级页面

this.navCtrl.remove(this.viewCtrl.index-1,2)      //这是删除2个页面，index是索引，从所modal页面(比如首页)开始算

//ionic3  关闭当前modal页面

dismiss() {

    this.viewCtrl.dismiss()
    
}

//ionic3 返回首页

this.viewCtrl.dismiss().then(() => {

         setTimeout(() => {
	 
              this.navCtrl.setRoot(TabsPage) 
	      
         }, 2000);
	 
})

//银行卡号4位分隔 =>注：app打包出来有bug

[(ngModel)]="cardnum" (ngModelChange)="change(cardnum)"  =>html绑定事件

//ts写法 =>

cardnum : any = '' //卡号

change(num){

    console.log(num.length)
    
    if(num.length == 5 || num.length == 10 || num.length == 15){
    
      this.cardnum = num.replace(/[ \f\t\v]/g, '').replace(/(\d{4})(?=\d)/g, "$1 ")
      
    }
    
  }

//跳转页面传参

this.navCtrl.push('BankcardVerificationPage'
{acctname:this.acctname,idno:this.idno,acctno:this.acctno,bankId:this.bankId,mobile:this.mobile})

//跳转页面获取传参的值

this.payId = this.navParams.get('data'）

//校验 {

//手机号码的验证

if(!(/^1[34578]\d{9}$/.test(this.双向绑定的手机名称))){}

//身份证的验证

if( !(/(^\d{15}$)|(^\d{18}$)|(^\d{17}(\d|X|x)$)/.test(this.双向绑定的身份证名称)) ){}

//银行卡格式的验证

if(this.双向绑定的银行卡名称.length != 16 && this.双向绑定的银行卡名称.length != 19){}

}

 // 查询设备平台
 
 if(platform.is('android')){
 
     this.platformType = 0
     
   }else if(platform.is('ios')){
   
     this.platformType = 1
     
 }
 
 //模态框弹层
 
 modalUpdatePage(data) {
 
    const modal = this.modalCtrl.create('页面名称', { text: data})    => 传参data
    
    modal.present()
    
 }
 
 
 
//管理后台 =>   ng-alain框架 =>https://ng-alain.com/docs/getting-started/zh

//拉代码，上传代码，拉项目操作跟app端的一样


//运行管理后台

npm run start

//打包测试

ng build

要cd .\frontend\

//新增模块   

ng g ng-alain:module 模块名

//新增页面

ng g ng-alain:list 页面名 -m=模块名

//页面的模态框

ng g ng-alain:view 模态框名 -m=模块名 -t=页面名

//模块要在fribtend src app core startup 和 routes的routes-routing.module.ts  引用

//初始化菜单 =>startup.service.ts

 children: [
 
 {
 
   text: "GT版本管理",
   
   icon: "anticon anticon-sync",
   
   children: [
   
       {
       
          text: "版本控制",
	  
          link: "/gt-version/version",
	  
       }
       
   ]
   
 }
 
//业务子模块  =>

children: [

      { path: 'gt-version', loadChildren: './gt-version/gt-version.module#GtVersionModule' },
      
]
 
