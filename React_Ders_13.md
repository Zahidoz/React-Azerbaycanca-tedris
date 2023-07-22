# React Router
Indiyə qədər həmişə 1 səhifədə işləmişik. İndi isə səhifələr arası keçid etməyi öyrənəcik. Bunun üçün React Router istifadə istifadə edəcik.
Başlamaq üçün terminaldan **npm i react-router-dom** yazırıq.
npm paketini yüklədikdən sonra package.json faylında dependecy hissəsindən yükləndiyini dəqiqləşdirin. Sonra isə main vəya index.js faylında(root olan) ProviderRouter-i import edək və səhifələrin keçid kodlarını yazaq. 
Veb səhifənin default  linki adətən '/' yəni http://localhost:3000/ olur. 
Misal. 
* ana səhifəsində **/** olur. yəni http://localhost:3000/
* about səhifəsində **/about** olur. yəni http://localhost:3000/about
* contact səhifəsində **/contact** olur. yəni http://localhost:3000/contact
* login səhifəsində **/login** olur. yəni http://localhost:3000/login

Əgər /about olduqda AboutPage render olmağını istəyiriksə ozaman **path** hissəsində /about , **element** hissəsində AboutPage yazacıq. Yuxarıdakı misalı kod formasında yazaq.
```js
[
	{
		path: '/',
		element: '<MainPage/>'
	},
	{
		path: '/about',
		element: '<AboutPage/>'
	},
	{
		path: '/contact',
		element: '<ContactPage/>'
	},
	{
		path: '/login',
		element: '<LoginPage/>'
	}
]
```
kodun yazılış sintaksisini bildiksə ozaman başlayaq. Root olan main.jsx vəya index.jsx faylına daxil olaq.
Normalda belə olurdu
```jsx
import React from  'react';
import ReactDOM from  'react-dom/client';
import App from  './App';
  
const  root  = ReactDOM.createRoot(document.getElementById('root'));
root.render(
	<App/>
);
```
Yəni root birbaşa App.jsx-i render edirdi. Lakin biz ProviderRouter import edib, onu render edecik, 
ProviderRouter komponentinə prop olaraq **router** adında **createBrowserRouter** metodu göndərməliyik. Və bu metod array daxilində obyektlər qəbul edir. Bu obyektlərin içərisindədə **path** və **element** qeyd edirik.( Yuxarıdakı misal kimi )

```jsx
import React from  'react';
import ReactDOM from  'react-dom/client';
import  {createBrowserRouter, RouterProvider}  from  'react-router-dom' 

const  root  = ReactDOM.createRoot(document.getElementById('root'));
root.render(
	<RouterProvider
		router={createBrowserRouter([
			{
				path:  "/",
				element:  <App  />,
			}
		])}
	/>
);
```
Gəlin src folder-i daxilində Pages adında folder qurub, içərisində HomePage.jsx, ContactPage.jsx, LoginPage.jsx, AboutPage.jsx adında fayllar qurub daxilində rafce yazaq.

```jsx
// HomePage.jsx faylı
import React from  'react'
  
const  HomePage  =  ()  =>  {
	return (
		<div>HomePage</div>
	)
}
export  default HomePage
```
```jsx
// ContactPage.jsx faylı
import React from  'react'
  
const  ContactPage  =  ()  =>  {
	return (
		<div>ContactPage</div>
	)
}
export  default ContactPage
```
```jsx
// About.jsx faylı
import React from  'react'
  
const  AboutPage  =  ()  =>  {
	return (
		<div>AboutPage</div>
	)
}
export  default AboutPage
```
```jsx
// LoginPage.jsx faylı
import React from  'react'
  
const  LoginPage  =  ()  =>  {
	return (
		<div>LoginPage</div>
	)
}
export  default LoginPage
```



Səhifələri qurduqdan sonra **createBrowserRouter** daxilində path və element formasında qeyd edək. App.jsx-ə ehtiyycat olmadığından onu silirik. Çünki ilk açılan səhifə **HomePage**. olacaq.

```jsx
import React from  'react';
import ReactDOM from  'react-dom/client';
import  {createBrowserRouter, RouterProvider}  from  'react-router-dom'
  
import AboutPage from  './Pages/AboutPage';
import ContactPage from  './Pages/ContactPage';
import HomePage from  './Pages/HomePage';
import LoginPage from  './Pages/LoginPage'; 

const  root  = ReactDOM.createRoot(document.getElementById('root'));
root.render(
	<RouterProvider
		router={createBrowserRouter([
			{
				path:  "/",
				element:  <App  />,
			},
			{
				path:  "/contact",
				element:  <ContactPage  />,
			},
			{
				path:  "/login",
				element:  <LoginPage  />,
			},
			{
				path:  "/about",
				element:  <AboutPage  />,
			}
		])}
	/>
);
```
Veb səhifənin yuxarıdakl url(link) sonuna **/contact** yazsaq **ContactPage** render olacaq. /login /about - da həmin formada uyğun səhifələr render olacaq.

Lakin router-in render etdiyi faylı daha səliqəli saxlamaq üçün createBrowserRouter kodumuzu routes adında bir faylda saxlayaq.  
src folder-i daxilində routes.jsx adında fayl quraq.
```jsx
// routes.jsx faylı
import  { createBrowserRouter }  from  "react-router-dom";

import AboutPage from  "./Pages/AboutPage";
import ContactPage from  "./Pages/ContactPage";
import HomePage from  "./Pages/HomePage";
import LoginPage from  "./Pages/LoginPage";
  
export  const  routes  =  ()  =>  createBrowserRouter([
	{
		path:  "/",
		element:  <HomePage  />,
	},
	{
		path:  "/contact",
		element:  <ContactPage  />,
	},
	{
		path:  "/login",
		element:  <LoginPage  />,
	},
	{
		path:  "/about",
		element:  <AboutPage  />,
	},
]);
```
və bu kodumuzu ProviderRouter olan faylda **createBrowserRouter**-in əvəzinə **routes** yazaq.

```jsx
//index.jsx vəya main.jsx
import React from  'react';
import ReactDOM from  'react-dom/client';
import  {RouterProvider}  from  'react-router-dom'
import  { routes }  from  './routes';

const  root  = ReactDOM.createRoot(document.getElementById('root'));
root.render(
	<RouterProvider
		router={routes}/>
);

```



Və beləliklə routes faylımızda istədiyimiz qədər səhifə əlavə edə 
## Link NavLink
Lakin səhifəni dəyişəndə hər dəfə url(link) hissəsindən dəyişmək düzgün deyil. Noramalda nav-da olan link-lərə click etdikdə avtomatik url dəyişməlidir. Bunun üçün Link komponentindən istifadə olunur.
 Gəlin sadə bir Nav komponenti quraq.

```jsx
const  Nav  =  ()  =>  {
	return (
		<nav>
			<h1>Logo</h1>
			<ul>
				<li>Home</li>
				<li>Contact</li>
				<li>Accaunt</li>
			</ul>
			<button>Login</button>
		</nav>
	);
};
export  default Nav;
```
Əgər istəsəniz özünüz dizayn edə bilərsiz. İndi isə gəlin Nav komponeniti Link komponenti ilə funksional hala gərirək.
```jsx
import  {Link}  from  'react-router-dom'
  
const  Nav  =  ()  =>  {
	return (
		<nav>
			<h1>
				<Link  to="/">Logo</Link>
			</h1>
			<ul>
				<li>
					<Link  to="/">Home</Link>
				</li>
				<li>
					<Link  to="/about">About</Link>
				</li>
				<li>
					<Link  to="/accaunt">Accaunt</Link>
				</li>
			</ul>
			<button>
				<Link  to="/login">Login</Link>
			</button>
		</nav>
	);
};
  
export  default Nav;
```

Son olaraq Nav komponentini Pages folder-ində olan bütün səhifələrə import edək.
```jsx
// HomePage.jsx faylı
import React from  'react'
import Nav from  '../Components/Nav';
  
const  HomePage  =  ()  =>  {
	return (
		<div>
			<Nav/>
			<h1>HomePage</h1>
		</div>
	)

}
export  default HomePage
```
```jsx
// ContactPage.jsx faylı
import React from  'react'
import Nav from  '../Components/Nav';
  
const  ContactPage  =  ()  =>  {
	return (
		<div>
			<Nav/>
			<h1>ContactPage</h1>
		</div>
	)

}
export  default ContactPage
```
```jsx
// About.jsx faylı
import React from  'react'
import Nav from  '../Components/Nav';
  
const  AboutPage  =  ()  =>  {
	return (
		<div>
			<Nav/>
			<h1>AboutPage</h1>
		</div>
	)
}
export  default AboutPage
```
```jsx
// LoginPage.jsx faylı
import React from  'react'
import Nav from  '../Components/Nav';
  
const  LoginPage  =  ()  =>  {
	return (
		<div>
			<Nav/>
			<h1>LoginPage</h1>
		</div>
	)

}
export  default LoginPage
```

Artıq Nav taqında olan linklərə click etdikdə lazım olan səhifələrə çata bilirik.
Bundan əlavə olaraq Link taqının əvəzinə **NavLink** taqı istifadə edə bilərik. Onun əlavə üstünlüyü odur ki, hansısa linkə click etdikdə həmin taqa **active** adında class əlavə edir. Və siz css-də  ( **.active** ) yazıb dizayn etsəniz click etdiyiniz link həmin dizaynda olacaq.

```jsx
import  {NavLink}  from  'react-router-dom'
  
const  Nav  =  ()  =>  {
	return (
		<nav>
			<h1>
				<NavLink  to="/">Logo</NavLink>
			</h1>
			<ul>
				<li>
					<NavLink  to="/">Home</NavLink>
				</li>
				<li>
					<NavLink  to="/about">About</NavLink>
				</li>
				<li>
					<NavLink  to="/accaunt">Accaunt</NavLink>
				</li>
			</ul>
			<button>
				<NavLink  to="/login">Login</NavLink>
			</button>
		</nav>
	);
};
  
export  default Nav;
```
Beləliklə artıq SinglePageApplication - da çoxlu səhifələr qura bilərsiz)
Praktika etməyi unutmayın.

---

Hazırladı - **Zahid Vahabzadə** 
Video dərslər üçün Youtube kanalım - **[Biraz Kod Yazaq](https://www.youtube.com/channel/UCRlKqhooswsmfkxnokxcB0g)** 
React-dan digər dokumentlər üçün - **[Github kanalım](https://github.com/Zahidoz/React-Azerbaycanca-tedris)**






