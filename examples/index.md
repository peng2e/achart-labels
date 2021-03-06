# Demo

---

## Normal usage

````html

<div id="c1"></div>

````

````javascript
seajs.use(['index','achart-canvas'], function(Labels,Canvas) {
  
  var canvas = new Canvas({
    id : 'c1',
    width : 500,
    height : 200
  });

  var labels = canvas.addGroup(Labels,{
    items : [
      {x : 10,y : 20,text : "1"},
      {x : 10,y : 40,text : "2"},
      {x : 10,y : 60,text : "3"},
      {x : 10,y : 80,text : "4"},
      {x : 10,y : 100,text : "5",font : "10px Arial",stroke : "red"},
      {x : 10,y : 120,text : "6"},
      {x : 10,y : 140,text : "7"},
      {x : 10,y : 160,text : "8"}
    ],
    label : {
      font : '20px/1.5 "Helvetica Neue",Helvetica,Arial,sans-serif',
      stroke : '#333',
      x : 10,
      y : 10,
      rotate : 90
    },
    renderer : function(value,item,index){
      if(index % 2 == 0){
        item.rotate = 45;
      }
      return value;
    }
  });

});
````


## html labels



````html

<div id="c2"></div>

````

````javascript
seajs.use(['index','achart-canvas'], function(Labels,Canvas) {
  
  var canvas = new Canvas({
    id : 'c2',
    width : 500,
    height : 200
  });

  var labels = canvas.addGroup(Labels,{
    items : [
      {x : 10,y : 20,text : "1",'text-anchor' : 'start'},
      {x : 10,y : 40,text : "2"},
      {x : 10,y : 60,text : "3"},
      {x : 10,y : 80,text : "4"},
      {x : 10,y : 100,text : "5"},
      {x : 10,y : 120,text : "6"},
      {x : 10,y : 140,text : "7"},
      {x : 10,y : 160,text : "8"}
    ],
    custom : true,
    label : {
      x : 10,
      y : 10,
      custom : true
    },
    renderer : function(value){
      return '<span>' + value + '</span>'
    }
  });

});
````


## show labels mixin



````html

<div id="c3"></div>

````

````javascript
seajs.use(['index','achart-canvas','achart-util','achart-plot'], function(Labels,Canvas,Util,Plot) {
  
  var canvas = new Canvas({
    id : 'c3',
    width : 500,
    height : 200
  });

  var A = function(cfg){
    A.superclass.constructor.call(this,cfg);
  };

  Util.extend(A,Plot.Item);

  Util.mixin(A,[Labels.ShowLabels]);
  
  Util.augment(A,{

    renderUI : function(){
      A.superclass.renderUI.call(this);
      this.renderLabels(); //调用入口文件
    },
    remove : function(){
      this.removeLabels();//清理文本
      A.superclass.remove.call(this);
    }

  });

  var a = canvas.addGroup(A,{
      labels : {
        items : [
          {x : 10,y : 20,text : "1"},
          {x : 10,y : 40,text : "2"},
          {x : 10,y : 60,text : "3"},
          {x : 10,y : 80,text : "4"},
          {x : 10,y : 100,text : "5",font : "10px Arial",stroke : "red"},
          {x : 10,y : 120,text : "6"},
          {x : 10,y : 140,text : "7"},
          {x : 10,y : 160,text : "8"}
        ],
        label : {
          font : '20px/1.5 "Helvetica Neue",Helvetica,Arial,sans-serif',
          stroke : '#333',
          x : 10,
          y : 10,
          rotate : 90
        }
      }
    });

});
````
