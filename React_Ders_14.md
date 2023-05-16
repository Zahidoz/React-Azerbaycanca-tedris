# SEO Helmet
Bu mövzuya çatmışıqsa artıq siz istədiyiniz veb səhifələri rahat formada hazırlaya bilirsiniz. Lakin Veb səhifəni hazırladıqdan sonra domain və hosting alıb qlobala yüklədikdə veb səhifənizə giriş edən istifadəçilərin sayı çox az olacaq. Bunun üçün www Google axtarış motoruna açar sözlər yazmalıyıq **(SEO)**. Bunun üçün React-da Helmet paketindən istifadə edəcik. Yükləmək üçün terminalda **npm i react-helmet** yazırsırsınız. Paket yükəndəndikdən sonra package.json-dan dependecy hissəsindən yükləndiyindən əmin olun.

Gəlin sadə bir router sistemi quraq.
1) Linklərə keçid etmək üçün sadə bir Nav komponenti quraq.
```jsx
//Nav.jsx
import React from  'react'
import  { Link }  from  'react-router-dom'
  
const  Nav  =  ()  =>  {
	return (
		<nav>
			<Link  to="/">Home</Link>
			<Link  to="/contact">Contact</Link>
			<Link  to="/location">Location</Link>
		</nav>
	);
}
  
export  default Nav
```

2) Pages folderində HomePage.jsx, ContactPage.jsx və LocationPage.jsx qurub daxilində rafce yazaq.
```jsx
//HomePage
import React from  'react'
import Nav from  '../Components/Nav'
  
const  HomePage  =  ()  =>  {
	return (
		<div>
			<Nav  />
			<h1>HomePage</h1>
		</div>
	);
}

export  default HomePage
```
```jsx
//ContactPage
import React from  'react'
import Nav from  '../Components/Nav'
  
const  ContactPage  =  ()  =>  {
	return (
		<div>
			<Nav  />
			<h1>ContactPage</h1>
		</div>
	);
}

export  default ContactPage
```
```jsx
//LocationPage
import React from  'react'
import Nav from  '../Components/Nav'
  
const  LocationPage  =  ()  =>  {
	return (
		<div>
			<Nav  />
			<h1>LocationPage</h1>
		</div>
	);
}

export  default LocationPage
```
3) routes.jsx faylı qurub Linklərdən keçid zamanı açılacaq səhifələri qeyd edək.
```jsx
//routes.jsx
import  { createBrowserRouter }  from  "react-router-dom";
import ContactPage from  "../Pages/ContactPage";
import HomePage from  "../Pages/HomePage";
import LocationPage from  "../Pages/LocationPage";
  
export  const  routes  =  createBrowserRouter([
	{
		path:  "/",
		element:  <HomePage  />,
	},
	{
		path:  "/contact",
		element:  <ContactPage  />,
	},
	{
		path:  "/location",
		element:  <LocationPage  />,
	}
]);
```
4) son olaraq main.jsx vəya index.js faylında RouterProvider ilə routes faylımıza bağlayaq.
```jsx
//main.jsx vəya index.js
import ReactDOM from  'react-dom/client'
import  {RouterProvider}  from  'react-router-dom'
import  { routes }  from  './routes'
  
ReactDOM.createRoot(document.getElementById('root')).render(
<RouterProvider  router={routes}/>
)
```
Artıq router sistemim hazırdır. Daha ətraflı əvvəlki mövzularda izah olunub.
İndi isə keçək SEO məsələsinə.
## Helmet SEO
Diqqət yetirdinizsə HomePage, ContactPage və LocationPage səhifələrində yuxarıda olan title eyni qalır.(adətən React App vəya Vite+React olur).
Gəlin ana səhifədə Helmet mövzusunu öyrənib sonra digər səhifələrdə də bunu tətbiq edək.
Bunun üçün Helmet paketini import edib. return edilən taqın içərisində yuxarıda Helmet komponentini çağırırıq.

```jsx
//HomePage
import React from  'react'
import Nav from  '../Components/Nav'
import  { Helmet }  from  'react-helmet';

const  HomePage  =  ()  =>  {
	return (
		<div>
			<Helmet>

			</Helmet>
			
			<Nav  />
			<h1>HomePage</h1>
		</div>
	);
}

export  default HomePage
```
Helmet komponentinə head taqı kimi baxa bilərsiniz. Eyni head taqı kimi içərisində **<title\> , <meta\> , <style\>**   taqları yaza bilərik.
**title** -  vasitəsi ilə veb səhifənin **adını**
**meta** -  taqında **description** ilə həmin səhifənin **kommenti**,
**meta** - taqında **keywords** ilə həmin səhifənin **açar** sözlərini,
**style** -  ilə həmin səhiyə uyğun **əlavə dizaynlar** yaza bilərsiz.
```jsx
//HomePage
import React from  'react'
import Nav from  '../Components/Nav'
import  { Helmet }  from  'react-helmet';

const  HomePage  =  ()  =>  {
	return (
		<div>
			<Helmet>
				<title>Vahabzadeh | Web Programming</title>
				<meta
					name="descripttion"
					content="Web Programming"
				/>
				<meta
					name="keywords"
					content="programming, html, css, js, javascript, lesson, course, frontend, backend"
				/>
				<style>
					{`
						body{
							background: #bbd3ec;
						}
					`}
				</style>
			</Helmet>
			
			<Nav  />
			<h1>HomePage</h1>
		</div>
	);
}

export  default HomePage
```
Yuxarıdakı kodu izah edək...
- **veb səhifənin adı:** Vahabzadeh | Web Programming
- **komment adı:**  Web Programming
- **açar sözlər:** programming, html, css, js, javascript . . . . 
- **əlavə dizayn:** background dəyişdirildi.

İndi isə HomePage-də yazdığımız kimi Contact və Location səhifələrimizə də SEO məlumatlarını əlavə edək.
```jsx
//ContactPage
import React from  'react'
import Nav from  '../Components/Nav'
import  { Helmet }  from  'react-helmet';

const  ContactPage  =  ()  =>  {
	return (
		<div>
			<Helmet>
				<title>Vahabzadeh | Contact</title>
				<meta
					name="descripttion"
					content="Contact"
				/>
				<meta
					name="keywords"
					content="contact, phone, call, dialog, programming, lesson, course"
				/>
				<style>
					{`
						body{
							background: #d5ecbb;
						}
					`}
				</style>
			</Helmet>
			
			<Nav  />
			<h1>ContactPage</h1>
		</div>
	);
}

export  default ContactPage
```
```jsx
//LocationPage
import React from  'react'
import Nav from  '../Components/Nav'
import  { Helmet }  from  'react-helmet';

const  LocationPage  =  ()  =>  {
	return (
		<div>
			<Helmet>
				<title>Vahabzadeh | Location</title>
				<meta
					name="descripttion"
					content="Location"
				/>
				<meta
					name="keywords"
					content="location, map, direction, programming, lesson, course"
				/>
				<style>
					{`
						body{
							background: #ecbfbb;
						}
					`}
				</style>
			</Helmet>
			
			<Nav  />
			<h1>ContactPage</h1>
		</div>
	);
}

export  default ContactPage
```

Əgər kommersial saytdırsa title, description vəya açar sözlər hissəsində  product.vendor, product.model tipli əsas məlumatlarını qoya bilərsiz. Veb səhifəni tipinə uyğun SEO yazsanız səhifənizə click sayını artıra bilərsiniz.
Praktika etməyi unutmayın.

Hazırladı - **Zahid Vahabzadə** Video dərslər üçün Youtube kanalım - **[Biraz Kod Yazaq](https://www.youtube.com/channel/UCRlKqhooswsmfkxnokxcB0g)**
