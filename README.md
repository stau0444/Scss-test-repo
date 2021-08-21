#
## SCSS
#

> CSS 전처리 라이브러리이다 여러가지 기능으로 css를 더욱 편하게 사용할 수 있도록      
도와준다 . 기본적으로 SCSS , Sass 두가지 문법을 갖고 있다 . Sass가 생기고      
기존 css와의 호환성 문제가 있어 SCSS가 생겼다 기본적인 문법은 거의 동일하다(중괄호 세미콜론 ,Mixins 제외)    
호환성 때문에 Sass보다는 SCSS가 선호된다 . 
 SCSS로 쓰여진 코드들은 CSS로 변환(compile)이 필요하다 .    

```scss
//간단한 예시

 //변수를 선언,사용할 수 있다.
$color:coral;

//중첩을 통해 반복되는 코드를 줄인다.
.container{
    h1 {
        color: $color;
        font-size: 60px;
        background-color:royalblue;
    }
}

//위의 scss 코드는 css코드로 아래와 같이 컴파일 된다.
.container h1 {
  color: coral;
  font-size: 60px;
  background-color: royalblue;
}

```


 #
 ## SCSS의 기능들
 #

 
 ### 1.주석
 #

 >SCSS에서는 기존의 표준 css의 주석인 /**/와 한줄 주석인 //을 제공한다. 

```scss

$color:coral;

.container{
    h1 {
        color: $color;
        /*font-size: 60px;*/
        //background-color:royalblue;
    }
}

//위의 코드는 아래와 같이 css로 변경된다

.container h1 {
  color: coral;
  /*font-size: 60px;*/
}

// 한줄주석인 '//'는 컴파일시 아예 지워지는 걸 알 수 있다.
// 반면에 표준 css 주석인 '/**/'는 잘 변환된다. (변환된 후에도 남아 있어야 한다면 사용)
```

#
### 2.중첩
#


>선택자를 {}로 감싸고 그 안에 요소들을 지정하여 css를 코드를 작성할 수 있게 해준다 .
#

```html
<body>
    <div class="container">
        <ul>
            <li>
                <div class="name">UGO</div>
                <div class="age">400</div>
            </li>
        </ul>
    </div>
</body>
<!--위와 같은 html 코드가 있다면 scss 로는 아래와 같이 표현할 수 있다.-->
```

```scss

.container{
    ul{
        li{
            font-size:40px;
            .name{
                color:royalblue
            }
            .age{
                color:coral
            }
        }
    }
}
//위의 scss는 아래의 css 로 컴파일 된다

//css
.container ul li {
  font-size: 40px;
}
.container ul li .name {
  color: royalblue;
}
.container ul li .age {
  color: coral;
}

//반복적인 부분들이 많이 줄어든다.

```

#
>자식 선택자 '>' 사용
#
```scss

//scss
.container{
    >ul{
        li{
            font-size:40px;
            .name{
                color:royalblue
            }
            .age{
                color:coral
            }
        }
    }
}

//css
.container > ul li {
  font-size: 40px;
}
.container > ul li .name {
  color: royalblue;
}
.container > ul li .age {
  color: coral;
}
```
#
>상위(부모) 선택자 참조
#
```scss

.btn{
    position:absolute;
    &.active{
        color:red;
    }
}
.list{
    li{
        &:last-child{
            margin-right: 0;
        }
    }
}
//'&'는 상위 선택자를 참조한다.
```
#
>중첩된 속성
#
```scss
.box{
    font: {
        weight:bold;
        size: 40px;
        family: san-serif;
    };
    margin: {
        top:40px;
        bottom: 30px;
    };
    padding: {
        top: 10px;
        bottom: 40px;
        left: 40px;
        right: 30px;
    };
}
//반복되는 속성들을 위의 코드 처럼 묶어서 사용할 수 있다 
//namespace 뒤에 : 을 붙히고 스페이스를 하나 둔 뒤에 {}로 묶어서 사용할 수 있다.
//위의 scss 는 아래의 css로 변환된다


.box {
  font-weight: bold;
  font-size: 40px;
  font-family: san-serif;
  margin-top: 40px;
  margin-bottom: 30px;
  padding-top: 10px;
  padding-bottom: 40px;
  padding-left: 40px;
  padding-right: 30px;
}
```


 

