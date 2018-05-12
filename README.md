# Learning Javascript :: ES6로 제대로 입문하는 모던 자바스크립트 웹 개발
  
책을 진행하면서 테스트용 파일 업로드
<br>
<br>
<br>
<br>
<br>
---------------------------------------
  
## gulp, babel, ESLint
  
### gulp(걸프)
- 자동화도구 (grunt도 많이 쓰임)
- package name : gulp
```
$ npm install --save-dev gulp
```
  
### babel(바벨)
- ES6로 트랜스컴파일(transcompile)하는 패키지. 트레이서(traceur)도 많이 쓰임
- package name : babel-preset-es2015
```
$ npm install --save-dev babel-preset-es2015
```
- .babelrc 파일 : 이 프로젝트에서 바벨을 사용할 때 ES6(ES2015, ECMA2015)를 사용한다는 것을 인식
```
{ "presets": ["es2015"] }
```
  
#### 바벨(babel)을 걸프(gulp)와 함께 사용하기
- 바벨을 걸프에 연결할 패키지를 설치
```
$ npm install --save-dev gulp-babel
```
- **는 '서브디렉토리를 포함한 모든 디렉토리'
1. es6 폴더에 있는 모든 .js 파일을 선택
2. 선택한 파일을 바벨(babel)에 파이프로 연결 ==> 바벨은 ES5 코드로 변형(트랜스컴파일)
3. 컴파일된 ES5 코드를 dist 디렉토리에 저장
```
gulp.src("es6/**/*.js")
	.pipe(babel())
	.pipe(gulp.dest("dist"));
```
- gulp 명령을 내리면 위 과정을 거친다. 여기서 책에서는 나오지 않았지만, `cannot find module 'babel-core'` 라고 에러가 뜬다. 뭐.. 설치하고 gulp 명령어 내리면 정상 실행된다.
```
$ npm install --save-dev babel-core
```
```
$ gulp
```
  
### ESLint
- Javascript의 문법을 체크하는 패키지
```
$ npm install -g eslint
```
1. eslint --init 로 체크할 문법의 기본 스타일을 설정한다.
2. 설정이 끝나면 자동으로 .eslintrc 파일이 생성되고 마지막 설정에 따라 javascript라면 .eslintrc.js 파일로 생성된다.
```
$ eslint --init
```
- y/n 선택하는 것 말고는 선택을 어떻게 하는지를 모르겠다... 어떻게 겨우겨우 함..
- ESLint를 사용하는 방법은 여러가지
	1. 직접 실행하는 방법 : `eslint es6/test.js`
	2. 에디터에 통합하는 방법 : 에디터 이름 뒤에 eslint를 붙여 검색
	3. gulpfile.js에 추가하는 방법
- gulfile.js에 추가하는 방법은 아래와 같다.
```
$ npm install --save-dev gulp-eslint
```
- 문법 규칙 설정은 .eslintrc.js 파일에 들어가서 수정이 가능하다. (`"rules"` 값 수정)
- 0은 "off"와 같고, 1은 "warn"(경고), 2는 "error"로 잡아낸다.
- 내가 추가한 규칙은 아래와 같다. (콘솔과 참조 기능을 끔)
```
"no-console": "off",
"no-undef": "off"
```
  
  
여기까지 최종 설치된 패키지의 목록은 다음과 같다. (package.json 참고)
```
"babel-core": "^6.26.3",
"babel-preset-es2015": "^6.24.1", // 트랜스컴파일할 때 프리셋 설정(es2015를 사용할 것이라는 명시)
"gulp": "^3.9.1", // gulp(자동화도구) 
"gulp-babel": "^7.0.1", // babel(트랜스컴파일)을 gulp에 연결하는 패키지
"gulp-eslint": "^4.0.2" // eslint(문법체크)를 gulp에 연결하는 패키지
// 추가로, 전역으로 설치한 eslint도 있음
```
(책에는 테스트용으로 underscore 패키지도 설치했지만, 난 설치하지 않음)
