Hazırladı. **Zahid Vahabzadə**, Video dərslərimə baxmaq üçün
Youtube kanalım - Biraz Kod Yazaq
# Niyə React? 
React təkrar istifadə edilə bilən istifadəçi interfeysi (UI) yaratmaq üçün JavaScript kitabxanasıdır.React Facebook tərəfindən 2013-cü ildə yaradılıb. React UI komponentlərini yaratmağı çox asanlaşdırır. React ilə işləyərkən biz birbaşa DOM ilə əlaqə saxlamırıq. React-in DOM manipulyasiyasını idarə etmək üçün öz yolu var. React yeni dəyişikliklər etmək üçün virtual DOM-dan istifadə edir və yalnız dəyişdirilməsi lazım olan elementi yeniləyir. Və sizinlə bu dokumentlərdə 10-15 veb səhifə işləyəcik. ))

**Qısa olaraq desək..**
* React Facebook tərəfindən yaradılıb
* React istifadəçi interfeyslərinin qurulması üçün JavaScript kitabxanasıdır
* React **tək səhifəli** proqramlar yazmaq üçündür və yalnız bir HTML səhifəsi olur.
* React bizə **təkrar** istifadə edilə bilən UI komponentləri yaratmağa imkan verir.

## JSX (JavaScript XML)
JSX JavaScript XML deməkdir. JSX bizə HTML elementlərini JavaScript kodu ilə yazmağa imkan verir. JSX  bizə React-da HTML elementlərini yazmağı və əlavə etməyi asanlaşdırır. JSX transpilerdən istifadə etməklə brauzerdə JavaScript-ə çevriləcək. Babel, JSX-i təmiz JavaScript-ə köçürən bir kitabxanadır. Aşağıdakı JSX koduna baxın.
```jsx
// JSX sintaksis
// bizim dırnaq istifadə etməyimizə ehtiyyac yoxdur.

const jsxElement = <h1>I am a JSX element</h1>
const welcome = <h1>Welcome to 30 Days of React Challenge</h1>
const data = <small>Oct 2, 2020</small>
```
Yuxarıdakı qəribə görünüşlü kod JavaScript kimi görünür, lakin bu JavaScript deyil və HTML kimi görünür, lakin tamamilə HTML elementi də deyil. JavaScript və HTML elementlərinin qarışığıdır. JSX bizə JavaScript-də HTML-dən istifadə etməyə icazə verir.
## React qurulumu
Bayaq biz JSX haqqında öyrəndik və CDN-dən istifadə edərək React və ReactDOM paketinə daxil olmaq olur. Bununla belə, CDN əvəzinə real layihələrdə biz React layihəsinin yaratmaq üçün ( create-react-app ) paketindən istifadə edəcik. İlkin create-react-app 22 iyul 2016-cı ildə buraxıldı. Bu vaxta qədər tərtibatçılar veb paketi JavaScript modul paketi, babel və bütün lazımi paketləri əl ilə konfiqurasiya edirdilər və bu, yarım saat və ya bəlkə də daha çox vaxt aparırdı. İndi create-react-app ilə siz layihələrin konfiqurasiyasına çox vaxt sərf etmək əvəzinə, yalnız məhsulun hazırlanması ilə məşğul olacaqsınız. Fərqli alətlərdən istifadə etməyə başlamazdan əvvəl gəlin istifadə edəcəyimiz bütün vasitələrlə qısa tanış olaq. React ilə işləyərkən istifadə etdiyimiz bəzi alətlər və texnologiyalar haqqında çox qısa məlumat verməyə çalışacağam.

## Node
Node JavaScript-in serverdə işləməsinə imkan verən JavaScript işləmə mühitidir. Node 2009-cu ildə yaradılmışdır. Node JavaScript-in inkişafı üçün böyük rol oynamışdır. React proqramı defolt olaraq localhost 3000-də başlayır (3000-ci port). 

Əgər node.js yoxdursa, **mütləq** [node.js quraşdırın.](https://nodejs.org/en/download/)

Yükləyərkən əməlliyyat sistemini(Windows,Macos,Linux) seçdikdən sonra **Recomended** - yəni məsləhət görülən versiyanı yükləyin. 

Cihaza Node.js in yükləndiyindən əmin olmaq üçün 
* **Windows** -> Windows və R click edib ( node -v ) yazıb enter edin.
* **Macos** -> Terminal-a daxil olub ( node -v ) yazıb enter edin.

```
node -v
v16.17.0
```
Node versiyalarımlz fərqli ola bilər. Böyük ehtimal sizdə yeni versiya olacaqdır. 


## Module
Lazım olduqda ixrac (export) və idxal (import) edilə bilən tək və ya çoxlu funksiyalar layihəyə ola bilər. React-da biz modullara və ya paketlərə daxil olmaq üçün linkdən istifadə etmirik, əvəzində modul istifadə edirik. Modul və ya modulların necə import və export olunduğuna baxaq:
```jsx
// file1.js
export const addTwo = (a, b) => a + b
export const multiply = (a, b) => a * b
export const subtract = (a, b) => a - b

export default (function transferFile() {
  return {
    addTwo,
    multiply,
    subtract,
  }
})()
```
```jsx
// index.js
// index.js-ə file1.js faylından transferFile import(idxal) edilir
import transferFile from './file1.js'

// to import the other modules
// bu modullar defolt olaraq ixrac edilmədiyi üçün biz 
// istədiklərimizi desctructure edirik 
import { addTwo, multiply, subtract } from './file1.js'

// file1.js-dən hər şeyi import etmək
import * as everything from './file1.js' 

console.log(addTwo(5, 5))
console.log(doSomeMath.addTwo(5, 5))
console.log(everything)
```

**Package (Paket)**
Paket bir modul və ya modullar toplusudur. Məsələn, React, ReactDOM paketlərdir.
## Node Package Manager(NPM)
NPM 2010-cu ildə yaradılmışdır. NPM-ni ayrıca quraşdırmaq lazım deyil - node quraşdırdığınız zaman sizdə NPM də olacaq. NPM Node.js üçün defolt paket meneceridir. O, istifadəçilərə reyestrdə mövcud olan JavaScript modullarını import etməyə imkan verir. Hazırda NPM reyestrində 350 000-dən çox paket var. 


## Visual Studio Code
Və bizə kodlarımızı yazacaq bir mühit lazımdır. bu kodları [Visual Studio Code](https://code.visualstudio.com/) -da yazacıq.  HTML CSS JS bilirsizsə yəqin ki VS Code komputerinizdə yüklənibdi )))
Browser olaraq **Google** işlədəcik.
## ## Visual Studio Extensions
Bu extentions (uzantıları) VS Code -a quraşdırmağı məsləhət görürəm.
-   Prettier
-   ESLint
-   Bracket Pair Colorizer
-   ES7 React/Redux/GraphQL/React-Native snippets

## Create React App
React layihəsi yaratmaq üçün aşağıdakı yollardan birini istifadə edə bilərsiniz. Nəzərinizə çatdırmaq istəyirəmki node quraşdırımış olmalıdır. 
* VS Code-a daxil olun və open folder hissəsindən bir folder açın.
* Terminal hissədən yeni bir terminal açın
* Mən faylın adını client qoyacam. Siz istədiyiniz adı seçə bilərsiniz.
* **npx create-react-app client**  yazın. 
* Paket yükləndikdən sonra öz folder-nizə daxil olun **cd client** yazın.
* və folder-i run etmək (işlətmək) üçün **npm start** yazın.

**Təbriklər..** Siz ilk REACT faylinizi qurub işə saldınız.
İndi React tətbiqiniz localhost 3000-də işləməlidir. App.js-ə gedin və bir az mətn yazaraq məzmunu dəyişdirin, avtomatik brauzerinizdə (Google-da) etdiyiniz dəyişiklikləri görəcəksiniz. Serveri dayandırmaq üçün VS Code terminalında Ctr + C düymələrini basın.
 




