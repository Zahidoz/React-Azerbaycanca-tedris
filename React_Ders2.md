Hazırlandı. **Zahid Vahabzadə**, Video derslerime baxmaq üçün
Youtube kanalım - Biraz Kod Yazaq
# Folder Strükturu və JSX məntiqi
Artıq React aplikasiyasında Folder strükturumuz HTML CSS JS kimi deyil, nisbətən daha fərqlidir. Biraz daha qarışıq görsənə bilər, lakin bu fayllar default olaraq yüklənir, yəni bizə bu faylların 90%-i lazım deyil. Onun üçün də eyni CSS-də reset etdiyimiz kimi, burda da fayllarımızı təmizləyirik.
Client folderinin içərisində bizim 3 folder-imiz var.
* **node-modules** - bu hissə react-ın işləməyi üçün lazımi molullardır. Bura dəyməyin )
* **public** - hamıya açıq olan bir folderdir
* **src** - HTML-dəki body taqı kimidir, bütün kodlarımız bu folder-də olacaq

Əlavə olaraq isə  kodumuzu github-a yükləmək üçün **.gitignore** və proyektimizə xaricdən yükləyəcəyimiz npm paketlərini görmək üçün isə  **package.json, package-lock.json** fayllarımız var.

İndi isə gəlin src folderinin daxilində olan artıq faylları silək. Başlanğıc üçün src folderinin içərisində yalnız **index.js** faylı lazımdır. 

Hərşey index.js faylından başlayır. Burada React və ReactDom paketləri import edilir. React-da idarəedici **root** adlanır. Və biz createRoot deyərək body taqının içərisində id-si root olan taqı götürüb onu render edirik. (Render - yəni ekrana çıxartmaq)

```jsx
// index.js faylı
import React from  'react';
import ReactDOM from  'react-dom/client';

const  root  = ReactDOM.createRoot(document.getElementById('root'));
root.render(
	<h1>Hello React</h1>
);
```
 
! ! ! Onu bilmək lazımdır ki, root.render( ) geriyə **1 bütöv taq** qaytarmalıdır. 

```jsx
// index.js faylı
import React from 'react';
import ReactDOM from 'react-dom/client';

const  root  = ReactDOM.createRoot(document.getElementById('root'));
root.render(
	<h1>Hello React</h1>
	<h2>Hello React</h1>
	<h3>Hello React</h1>
);
```
ERROR olacaq çünki biz 3 taqı render etdik. Bəs necə edək ki, hər 3-ü də render olsun.
Bayaq da, dediyimiz kimi geriyə yalnız bir taq qaytarmalıdır. O zaman bütün taqları **bir taq içərisinə alaq**.
```jsx
// index.js faylı
import React from 'react';
import ReactDOM from 'react-dom/client';

const  root  = ReactDOM.createRoot(document.getElementById('root'));
root.render(
	<div>
		<h1>Hello React</h1>
		<h2>Hello React</h2>
		<h3>Hello React</h3>
	</div>

);
```

<img width="365" alt="Screenshot 2023-04-17 at 14 33 15" src="https://user-images.githubusercontent.com/83206656/233043411-470ca1cd-69fb-4abd-82da-65a288a29243.png">



Artıq geriyə 1 taq qaytardığımız üçün ekrana yazdığımız h1,h2,h3 taqları çıxacaq. 

## JSX məntiqi
root.render daxilində bu qədər kod yazmaq çox da məqsədə uyğun deyi. Əslində root geriyə bir komponent (component) qaytarmalıdır. Bəs **component** nədir?
Əslində bildiyimiz kimi React komponentlərdən ibarətdir. Və biz səhifəni və içərisindəki təkrarlaran hissələri komponentlərə ayırmaqlıyıq. Gəlin ilk App adında komponentimizi quraq.
Bunun üçün src folderinə click edib sonra sağ düyməyə click edib, **New File** seçirik. Və faylımızın adı. App.jsx olacaq. JSX faylında biz HTML və Javascript kodunu birlikdə istifadə edə bilirik. Bəs bunu necə edirik. 

```jsx
// App.jsx faylı
function  App(){
	// Burada JS kodu yazılır
	// Burada JS kodu yazılır
	// Burada JS kodu yazılır
	return (
		<div>
			<h1>Return daxilində HTML kodu yazılır</h1>
			<h2>Və Return geriyə bir taq qaytarır !!!</h2>
		</div>
	);
}

export  default App
```
JSX strukturu bu formada olur. 
- Funksiya yazılır və funksiya daxilində HTML kodu return edilir. **(1 taq içərisində)**
- Funksiya sadə function və ya arrow function ola bilər.
- Və bu funksiyanı başqa faylda çağırmaq(istifadə etmək) üçün onu export edirik. 
- export - yəni bu faylı hansı adda və formada çağıraq.

Bu strükturu daha qısa vaxtda yazmaq üçün 
1-ci Extentions hissəsindən ES7 React yazıb (install) yükləyirik.
Sonra isə boş App.jsx faylında **rafce** yazıb enter edirik.
```jsx
rafce
```
```jsx
// App.jsx faylı
import React from 'react'

const App = () => {
	return (
		<div>App</div>
	)
}

export default App
```
Diqqət yetirdinizsə bu dəfə arrow funtion formasında oldu. Adətən 99% JSX strükturu arrow funtion formasında yazırlar.
Artıq component-i yazdıq. Bəs bu komponenti necə render edək?
Bunun üçün root-un render olduğu index.js faylına qayıdaq.

- Birinci . 
- **import App from  './App';** yazaraq JSX faylımızı index.js faylına daxil edək.
- render daxilində **\<App/>** yazaraq həmin JSX faylını çağıraq.
```jsx
// index.js faylı
import React from  'react';
import ReactDOM from  'react-dom/client';
import App from './App';

const  root  = ReactDOM.createRoot(document.getElementById('root'));
root.render(
	<App/>
);
```

JSX komponentlərini import və export edərkən diqqət yetirməli olduğumuz nüanslar var.
- JSX faylda funksiyanın adı **böyük hərflə** başlamalıdır,

Fayl **default** formada export edilədə bilər, edilməyə də bilər.
Əgər default export olunubsa çağıranda **normal** formada çağırılır (import edilir)

```jsx
export default App
```
```jsx
import App from './App';
```

 Əgər default export olunmayıbsa çağıranda **scope** daxilində çağırılır (import edilir)
```jsx
export {App}
```
```jsx
import {App} from './App';
```
****
Hazırlandı. **Zahid Vahabzadə**, Video derslerime baxmaq üçün
**Youtube** kanalım - Biraz Kod Yazaq


