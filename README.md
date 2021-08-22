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


#
### 3. 변수
#

>변수를 사용하여 데이터를 재활용할 수 있다. 변수는 선언된 범위에서   유효범위를 갖는다. 

```scss
//전역변수
$size  = 100px;

.container {
    //로컬 변수 (중괄호 안에서만 사용 가능)
    //값이 재할당 된다
    $size  = 200px; 
    position : fixed;
    top:100px;
    .item{
        $size  = 200px; 
        width:100px;
        height:100px;
        transform : translateX(100px);
    }
    //위에서 재할당 된 값이 출력된다(200px)
    left : $size 
}
.box {
    width: $size
}
```


#
### 4.연산
#

> 사칙연산과 % 기호를 사용하여 값을 계산하여 정의할 수 있다.
나누기 연산은 '/' css에서 단축속성을 구분할때 사용되기 때문에
사용할 수 없다. 나누기 기호를 사용할 때는 ()소괄호로 묶거나 
변수를 통해 값을 나누면 연산이 된다. 

```scss
div{
    $size = 30px;
    width:20px + 20px;
    height: 40px - 10px;
    font-size: 10px *2;
    //연산이 안된다.
    margin: 30px / 2;
    //괄호로 묶어서 연산
    margin: (30px / 2);
    //변수 사용하여 연산
    margin: $size/2;
    //다른 산술 연산과 함께 사용한다
    margin: (15px + 15px) / 2;
    padding: 20px %7;
}

```
 
 #
 ### 5.Mixin(재활용)
 #

 > @mixin 키워드 + 이름을 사용해서 재활용될 코드를 지정할 수 있고   
 사용하는 곳에서는 @include +  이름으로 사용할 수 있다. 인수를 넘겨서 들어온 값에 따라 mixin이   동작하도록 할 수 있다.

 ```scss
 @mixin center{
     display: flex;
     justify-content: center;
 }

 .container{
     @include center
     .item{
         @include center
     }
 }
 
 .box {
     @include center;
 }

 //컴파일된 css

 .container {
  display: flex;
  justify-content: center;
  align-items: center;
}
.container .item {
  display: flex;
  justify-content: center;
  align-items: center;
}

.box {
  display: flex;
  justify-content: center;
  align-items: center;
}

//파라미터 , 기본값 사용
//- 키워드 인수를 사용해서 특정 파라미터를 지칭할 수도 있다.


@mixin box ($size :100px){
    width: $size;
    height: 100px;
    background-color: tomato;
}

.container{
    @include box;
    .item{
        //키워드 인수
        @include box($color : red);    
    }
}

.box{
    @include box;
}
 ```

 #
 ### 6. 반복문
 #

 >@for로 반복문을 사용하여 특정 css 코드를 반복적으로 생성할 수 있고 , 보간을 사용하여 for 문 안에서 실행될 로직에 
 인덱스값을 사용할 수 있다. scss의 보간은 #{$변수명}으로 사용할 수 있다. scss에서는 0부터 시작하지 않고 1부터 시작한다.

 ```scss
 //scss 반복문 사용
@for $i from 1 through 5{
    .box:nth-child(#{$i}){
        width: 100px * $i;
    }
}

//컴파일된 css

.box:nth-child(1) {
  width: 100px;
}

.box:nth-child(2) {
  width: 200px;
}

.box:nth-child(3) {
  width: 300px;
}

.box:nth-child(4) {
  width: 400px;
}

.box:nth-child(5) {
  width: 500px;
}


 ```


 #
 ### 7. 함수
 #
 >@mixin이 단지 코드들의 모음을 재활용하는 용도 였다면
 @function은 함수의 역할을 한다 파라미터로 받은 값을  
 로직에 맞게 계산하여 리턴할 수 있다.

```scss
@mixin center {
    display: flex;
    justify-content: center;
    align-items: center;
}

@function ratio($size, $ratio){
    @return $size * $ratio
}


.box {
    $width: 100px;
    width: $width;
    //16:9 비율을 갖게 된다.
    height: ratio($width, 9/16);
    @include center;
}
```

#
### 8.색상 내장 함수
#

>scss에서 기본적으로 색상 조작에 관련된 내장 함수를 제공한다.

```scss
//색상 내장 함수
$color: royalblue;
.container {
    .box {
        width: 200px;
        height: 100px;
        margin: 20px;
        border-radius: 10px;
        background-color: $color;
        &.built-in {
           
            //mix()는 scss 내장함수이다 색상을 섞어준다
            //background-color: mix($color,red ,50%);
           
            //lighten() 은 첫번째 파라미터로 지정한 색상에서 , 
            //두번째 파라미터의 수치만큼 더 밝은 색상을 리턴한다
            //background-color: lighten($color ,20%);

            //darken() 은 더 어두운 색상을 리턴한다
            //background-color: darken($color ,20%);

            //saturate()는 채도를 올려준다
            //background-color: saturate($color ,20%);

            //desaturate()는 채도를 낮춰준다
            //background-color: desaturate($color ,40%);

            //grayscale()는 색상을 회색으로 만들어 준다
            //background-color: grayscale($color);

            //invert()는 색상을 반전시킨다
            //background-color: invert($color);

            //rgba()는 투명도를 지정한다.
            background-color: rgba($color,.5);
        }
        &:hover{
            background-color: darken($color ,20%);
        }
    }
}


```

#
### 그 외
#


```scss
//SCSS 데이터 종류

$number :1;
$string : bold;
$color:red;
$boolean: true;
$null: null;
$list: orange,royalblue , yellow;
$map: (
    o: orange,
    r: royalblue,
    y: yellow
);


//@each 를 통한 배열 ,맵 반복
@each $k, $v in $map {
    .box-#{$k}{
        color: $v;
    }    
}
```



