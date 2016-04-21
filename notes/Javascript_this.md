## Javacript  : this
---

`this` �Ƕ�ָ̬���ģ�ȡ���ڷ��������õ�`object`�� ������`this`������ʱ���ڵ�`object`. 

`this`ʹ�ò����������


###1. ���õ�object��Ԥ��Ĳ�ͬ 
```
$("gfw").click(byr.coding);  //byr.coding �е�this����byr
```
���������`bind`�����ı� context 
```
$("gfw").click(byr.coding.bind(byr));  //����byr�ҽ��� 
```
���Ľ̳� [�й���bind call apply][1]  


###2.��thisʹ����һ�����������е���ֵ����ʱ
`this` inside the anonymous function cannot access the outer function's `this`, so it is bound to the global window object. When use in `strict mode`, `this` holds the value of undefined in global functions and in anonymous functions that are not bound to any object.

``` 
var daddy = "window";
var byrSon = {
               daddy  : "byr", 
               backHome : function( baby ){
                     baby();
               },
               coding : function(){
                     this.backHome(function () {
                          console.log(this.daddy);   //this : object Window
                     });
               }
            }             //byr �ؼҺ����� baby ��daddy �д���w

```
�������
```
   var daddy = "window";
   var byrSon = {
                   daddy  : "byr", 
                   backHome : function( baby ){
                         baby();
                   },
                   coding : function(){
                         var mySon = this;
                         this.backHome(function () {
                              console.log(mySon.daddy);   //this : byrSon
                         });
                   }
                }             //��νж���
```
###3.ĳobject��function������ȫ�ֱ���
```
var daddy = "window";
var byrSon = {
               daddy  : "byr", 
               cry : function(){
                    console.log(this.daddy);
               }
            };   
var whosYourDaddy = byrSon.cry;
whosYourDaddy();  //�쳤���˱��˵�����
```
�������
```
var whosYourDaddy = byrSon.cry.bind(byrSon);  //bind �Ժ�ͺ���
whosYourDaddy();
```
###4.Borrow method
���ڴӱ��`object`�跽������
```
var oldWang = {
     name : "����"
}

var bob = {
     name : "Сͷ�ְ�",
     Daddy : function(){
            console.log(this.name);
      }
}

oldWang.Daddy = bob.Daddy.bind(oldWang);
oldWang.Daddy();   // ���������

//call �� apply Ҳ����
bob.Daddy.call(oldWang);
bob.Daddy.apply(oldWang);
```



[1]: http://javascriptissexy.com/javascript-apply-call-and-bind-methods-are-essential-for-javascript-professionals/