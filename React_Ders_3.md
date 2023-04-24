## Component ilə Veb səhifə qurmaq
Artıq component yaratmağı da öyrəndiyimizə görə, başlanğıc üçün çox sadə bir veb səhifə qura bilərik.
Sadə bir veb səhifədə Nav, Hero, bir-iki section və Footer olur.
Təkrarlanan elementləri componentlərə ayırmalıyıq. Və bu saydıqlarımızdan adətən Nav, Hero və Footer component olaraq yazılır.
O zaman sonuncu dəfə qaldığımız App.jsx faylından davam edək.
```jsx
// App.jsx faylı
import React from  'react'

const  App  =  ()  =>  {
	return (
		<div>
			App
		</div>
	)
}

export  default App
```

Və siz React-da işləyirsinizsə artıq SCSS vəya SASS bilməlisiniz.
Bunun üçün Terminal-da **npm install sass** və ya **npm i sass** yazıb sass yükləməlisiniz. Extentions hissəsindən **sass** yazıb onu da yükləyin.



```
npm i sass
``` 
npm paketinin yuklendiyinden emin olmaq ucun package.json-da dependencies hissəsindən yoxlaya bilərsiz. Əgər adı və qarşısında versiyası varsa deməli yüklənib.
Başlaya bilərik.
1-ci src folderi daxilində style.scss faylı qururuq. Bura sırf App.jsx üçün lazım olan dizayn kodlarını yazacıq. Nav Hero Footer kimi komponentlərin özlərinin ayrıca style.scss faylları olacaq.

<img width="840" alt="Screenshot 2023-04-19 at 15 46 06" src="https://user-images.githubusercontent.com/83206656/234082997-0982981b-cfdf-4062-b4e5-078b4940e0eb.png">


Hələkilik ilk layihəmizdir deyə reset kodlarını da bura yazacıq.
```scss
//style.scss faylı
*{
	margin:  0;
	padding:  0;
	list-style:  none;
	text-decoration:  none;
	border:  none;
	outline:  none;
	box-sizing:  border-box;
}
html{
	font-size:  10px;
}
button{
	cursor:  pointer;
}
.container{
	max-width:  1440em;
}
```
Əgər responsive dizaynda istifadə edilən (em, rem, vh, vw) ölçü vahidlərini bilmirsinizsə bu layihədə hələki em istifadə edəcəm və normalda px olaraq yazdıqlarımızı 10-a bölüb em olaraq yazacıq. 
Misal... 
padding: 20px 12px; əvəzinə padding: 2em 1.2em;

İndi isə yazdığımız style.scss - i  App.jsx-ə import edək.
```jsx
// App.jsx faylı
import React from  'react'
import  './style.scss'

const  App  =  ()  =>  {
	return (
		<div>
			App
		</div>
	)
}

export  default App
```
- SRC folderi daxilində Component adında bir Folder qururuq.
(Folder qurmaq üçün sağ düyməyə click edib New Folder seçin)

- Və həmin folderin daxilində Nav Footer və Hero adında Folder qururuq. 

- Nav folderinin içərisində index.jsx və sytle.scss falylı qurun.

<img width="357" alt="Screenshot 2023-04-21 at 13 09 24" src="https://user-images.githubusercontent.com/83206656/234083218-77c14624-85f5-4024-85a8-84a2af29e004.png">


- index.jsx faylında **rafce** yazıb, Funksiyanın adı və export default hissəsində index əvəzinə **Nav** yazın ki, digər faylda komponenti çağıranda Nav adı ilə import edəsiniz.

```jsx
// index.jsx faylı (Nav folderinde olan)
import React from  'react'

const  Nav  =  ()  =>  {
	return (
		<div>Nav</div>
	)
}

export  default Nav
```

Və Nav folderində olan index.jsx faylına özünə aid olan style.scss faylını import edək.

```jsx
// index.jsx faylı (Nav folderinde olan)
import React from  'react'
import  './style.scss'

const  Nav  =  ()  =>  {
	return (
		<div>Nav</div>
	)
}

export  default Nav
```
İndi isə Nav komponentinin HTML strukturunu quraq.
```jsx
// index.jsx faylı (Nav folderinde olan)
import React from  'react'
import  './style.scss'

const  Nav  =  ()  =>  {
	return (
		<nav>
			<div  className="contaier">
				<h1>IT İnnovations</h1>
				<ul>
					<li>Home</li>
					<li>About</li>
					<li>Contact</li>
					<li>FAQ</li>
				</ul>
				<button>Join Team</button>
			</div>
		</nav>
	)
}

export  default Nav
```
Və HTML struktundaki elementləri Nav folderinin içərisindəki style.scss faylında dizayn edək. 
```scss
// style.scss faylı (Nav folderinde olan)
nav{
	.container{
		padding:  2em  4em;
		display:  flex;
		align-items:  center;
		justify-content:  space-between;
		gap:  1em;
		h1{
			font-size:  3em;
			color:  royalblue;
		}
		ul{
			display:  flex;
			align-items:  center;
			gap:  2.5em;
			li{
				font-size:  1.8em;
				transition:  .2s;
				cursor:  pointer;
				&:hover{
					color:  royalblue;
				}
			}
		}
		button{
			font-size:  1.6em;
			padding:  .6em  1.2em;
			border:  .1em  solid  royalblue;
			background:  #fff;
			color:  royalblue;
			transition:  .2s;
			&:hover{
				background:  royalblue;
				color:  #fff;
			}
		}
	}
}
```
Nav komponentimiz hazırdı lakin ekranda görsənmir, çünki biz komponenti App.jsx faylında hələ import etməmişik. Gəlin App.jsx faylına daxil olub import edək.

- 1) Yuxarıda **import Nav from  './Components/Nav'** yazırıq.
- 2) return daxilində  **\<Nav>\</Nav>** və ya **\<Nav/>** yazırıq.

```jsx
// App.jsx faylı
import React from  'react'
import  './style.scss'
import Nav from  './Components/Nav'

const  App  =  ()  =>  {
	return (
		<div>
			<Nav/>
		</div>
	)
}

export  default App
```

İndi isə gəlin həmin qaydada çox sadə dizaynda Hero hissəsini hazırlayaq.


Hero folderi içərisində index.jsx və sytle.scss falylı qurun.
- index.jsx faylında **rafce** yazıb. Funksiyanın adı və export default hissəsində index əvəzinə **Hero** yazın ki, digər faylda komponenti çağıranda Hero adı ilə import edəsiniz.

```jsx
// index.jsx faylı (Hero folderinde olan)
import React from  'react'

const  Hero  =  ()  =>  {
	return (
		<div>Hero</div>
	)
}

export  default Hero
```

Və Hero folderində olan index.jsx faylına özünə aid olan style.scss faylını import edək.

```jsx
// index.jsx faylı (Hero folderinde olan)
import React from  'react'
import  './style.scss'

const  Hero  =  ()  =>  {
	return (
		<div>Hero</div>
	)
}

export  default Hero
```
İndi isə Hero komponentinin HTML strukturunu quraq.
```jsx
// index.jsx faylı (Hero folderinde olan)
import React from  'react'
import  './style.scss'

const  Hero  =  ()  =>  {
	return (
		<div  className="hero">
			<div  className="container">
				<h1>Hero Hero Hero Hero Hero</h1>
				<p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Dicta nihil, enim quam pariatur aperiam natus corrupti deleniti qui ad blanditiis!</p>
				<button>Join Team</button>
			</div>
		</div>
	)
}

export  default Hero
```
Və HTML struktundaki elementləri Hero folderinin içərisindəki style.scss faylında dizayn edək. 
```scss
// style.scss faylı (Hero folderinde olan)
.hero  {
	.container  {
		padding:  6em  1em;
		display:  flex;
		flex-direction:  column;
		align-items:  center;
		gap:  5em;
		h1{
			font-size:  5em;
			color:  cornflowerblue;
		}
		p{
			font-size:  1.8em;
			letter-spacing:  .1em;
			color:  gray;
			max-width:  40em;
			text-align:  center;
		}
		button{
			padding:  .5em  1em;
			background:  cornflowerblue;
			color:  #fff;
			font-size:  3em;
		}
	}
}
```
Hero komponentimiz hazırdı lakin ekranda görsənmir, çünki biz komponenti App.jsx faylında hələ import etməmişik. Gəlin App.jsx faylına daxil olub import edək.

- 1) Yuxarıda **import Hero from  './Components/Hero'** yazırıq
- 2) return daxilində  **\<Hero>\</Hero>** və ya **\<Hero/>** yazırıq.

```jsx
// App.jsx faylı
import React from  'react'
import './style.scss'
import Nav from  './Components/Nav'
import Hero from  './Components/Hero';

const  App  =  ()  =>  {
	return (
		<div>
			<Nav />
			<Hero />
		</div>
	)
}

export  default App
```

Bu qaydada Footer yazaq. Footer folderinin içərisinə index.jsx və style.scss faylı qururuq.
```jsx
// index.jsx faylı (Footer folderinde olan)
import React from  "react";
import  "./style.scss";

const  Footer  =  ()  =>  {
	return (
		<footer>
			<div  className="container">
				<div  className="footer-logo">
					<h1>IT Innovations</h1>
					<p>
					Lorem ipsum dolor sit, amet consectetur adipisicing elit. Eum minima
					commodi suscipit nisi debitis veritatis ex placeat consequuntur
					quisquam quia!
					</p>
				</div>
				<div  className="links-c">
					<ul>
						<li>Home</li>
						<li>About</li>
						<li>Contact</li>
						<li>FAQ</li>
					</ul>
					<ul>
						<li>Instagram</li>
						<li>Linkedin</li>
						<li>Youtube</li>
						<li>Pinterest</li>
					</ul>
					<ul>
						<li>+994 50 703 37 33</li>
						<li>IT Innovations</li>
						<li>Biraz Kod Yazaq</li>
					</ul>
				</div>
			</div>
		</footer>
	);
};

export  default Footer;
```

```scss
// style.scss faylı (Footer folderinde olan)
footer  {
	.container  {
		display:  flex;
		align-items:  start;
		justify-content:  space-between;
		padding:  5em  10em;
		gap:  2em;
		.footer-logo  {
			h1  {
				font-size:  4em;
				color:  cornflowerblue;
				margin-bottom:  .5em;
			}
			p{
				font-size:  1.8em;
				letter-spacing:  .01em;
				color:  gray;
				max-width:  30em;
			}
		}
		
		.links-c  {
			display:  flex;
			gap:  8em;
			align-items:  start;
			ul  {
				display:  flex;
				flex-direction:  column;
				gap:  1em;
				align-items:  start;
				li  {
					cursor:  pointer;
					color:  gray;
					font-size:  2em;
					letter-spacing:  0.01em;
				}
			}
		}
		
	}
}
```
Footer komponenti hazırdır. Gəlin komponentimizi App.jsx-ə import edək.
```jsx
// App.jsx faylı
import React from  'react'
import  './style.scss'
import Nav from  './Components/Nav'
import Hero from  './Components/Hero';
import Footer from  './Components/Footer';

const  App  =  ()  =>  {
	return (
		<div>
			<Nav />
			<Hero />
			<Footer/>
		</div>
	)
}

export  default App
```

Artıq səhifəmiz hazırdır. Növbəti mövzuda dinamik Component (yəni Component-ə məlumat göndərmək) öyrənəcik.
