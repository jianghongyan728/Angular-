## Angular做的小例子
#### 安装Angular

```
npm install -g @angular/cli //安装angular
ng new my-app --skip-install  //创建项目
cd my-app //跳转mhy-app项目下
cnpm install
ng serve
```
#### 安装完angular后，接着安装webpack

```
cnpm install webpack --save //安装webpack
npm satrt  //运行项目
```

#### 安装完之后，就开始我们的项目吧
###### index.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <title>Angular 2 快速上手</title>
    <base href="/">
    <style>
      html {font-family:'Microsoft Yahei';background-color:#F7F48B;}
      p {margin:8px 0;padding:0;}
      h1 {font-size:20px;}
      button,input {font-size:16px;}
      .cmp-1 {background:#A1DE93;border-radius:5px;width:500px;height:300px;margin:100px auto;padding:20px;}
      .cmp-2 {border:1px solid #ccc;border-radius:5px;background-color:#70A1D7;padding: 10px;margin:20px 0;}
    </style>
  </head>
  <body>
    <my-app>加载中...</my-app>
    <script src="bundle.js"></script>
  </body>
</html>

```
###### main.ts

```javascript
import 'zone.js';

import 'core-js/es6/reflect';
import 'core-js/es7/reflect';

import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';

import { AppModule } from './app/app.module';

platformBrowserDynamic().bootstrapModule(AppModule);

```

###### app.module.ts

```javascript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { FormsModule } from '@angular/forms';

import { AppComponent }  from './app.component';
import { ChildComponent } from './child.component';
import { HighlightDirective } from './highlight.directive';
import { LoggerService } from './logger.service';

@NgModule({
  imports: [ BrowserModule, FormsModule ],
  declarations: [ AppComponent, ChildComponent, HighlightDirective ],
  providers: [ LoggerService ],
  bootstrap: [ AppComponent ]
})
export class AppModule { }

```
###### app.component.html

```javascript
<div class="cmp-1">
  <h1>根组件</h1>
  <p>
    嘿嘿，{{ greeting }}！
    <label>
      <input type="checkbox" [(ngModel)]="isShowMore">
      是否显示详细信息
    </label>
  </p>
  <p highlight *ngIf="isShowMore">Angular 2 是 Google 推出的新一代的Web开发框架</p>
  <my-child [message]="msgToChild" (outer)="receive($event)"></my-child>
  <p>从子组件获得的消息：{{ msgFromChild || '暂无' }}</p>
</div>


```
###### app.component.ts

```javascript
import { Component } from '@angular/core';

import { LoggerService } from './logger.service';

@Component({
  selector: 'my-app',
  templateUrl: './app/app.component.html'
})
export class AppComponent {
  private greeting: string;
  private isShowMore: boolean;
  private msgToChild: string;
  private msgFromChild: string;

	constructor(private logger: LoggerService) {	}

  ngOnInit() {
    this.greeting = 'Angular 2';
    this.msgToChild = 'message from parent';
    this.logger.debug('应用已初始化');
  }

  receive(msg: string) {
    this.msgFromChild = msg;
  }
}

```
###### child.component.html

```html
<div class="cmp-2">
  <h1>子组件</h1>
  <p>嘿嘿，我从父组件获取的值是：{{ message }}</p>
  <button (click)="sendToParent()">发送到父组件</button>
</div>
```

###### child.component.ts

```javascript
import { Component, Input, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'my-child',
  templateUrl: './app/child.component.html'
})
export class ChildComponent {
  @Input() private message: string;
  @Output() private outer = new EventEmitter<string>();
	constructor() {	}
  
  sendToParent() {
    this.outer.emit('message from child');
  }
}

```
###### highlight.directive.ts

```javascript
import { Directive, ElementRef, Renderer } from '@angular/core';

@Directive({
  selector: "[highlight]"
})
export class HighlightDirective {
  constructor(
    private el: ElementRef, 
    private renderer: Renderer
  ) { 
    renderer.setElementStyle(el.nativeElement, 'backgroundColor', 'yellow');
  }
}


```
###### logger.service.ts

```javascript
import { Injectable } from '@angular/core';

@Injectable() 
export class LoggerService {
  constructor() { }

  debug(msg: string) {
    console.log(msg);
  }
}
```
###### webpack.config.js
```javascript
module.exports = {
  entry: './main.ts',

  output: {
    filename: './bundle.js'
  },

  resolve: {
    extensions: ['.ts', '.js']
  },

  module: {
    rules: [
      {
        test: /\.ts$/,
        loader: 'ts-loader'
      }
    ]
  }
};

```
### 接下来总结一下

1.  移除controller+$scope设计，改用组件式开发(更容易上手)
2. 性能更好(渲染更快，变化监测效率更高)
3. 优先为移动应用设计(Angular Mobile Toolkit)
4. 更加贴合未来的标准

## Angular
![image](D:\姜\学习\angular\angular2-demo-master\an.png)

## Angular的组件
![image](D:\姜\学习\angular\angular2-demo-master\kk.png)

## 数据绑定
![image](D:\姜\学习\angular\angular2-demo-master\shu.png)

## Angular的指令

![image](D:\姜\学习\angular\angular2-demo-master\zhi.png)



