# useEffect | Component LifeCycle

React bildiyimiz kimi komponentlərdən ibarətdir. Və bu komponentlərin yaşam dövrü var. Bütün komponentlər yaranır, dəyişir və sonda silinir. Buna **Component Lifecycle** deyirlər.

Buna misal olaraq kiçik bir login form komponentini demək olar.  Nav-da Login button-a click etdikdə Ekranın ortasında kiçik login form komponenti görsənir. Bu komponentin **yaranmasıdır**. Siz login və parolunuzu yazanda bu komponentin **dəyişməsidir**. Və sonda siz təsdiqlədiyinizdə form-un ekrandan itməsi komponentin **silinməsidir**.

Və biz **useEffect** istifadə edərkən komponent yaranma, dəyişmə və silinmədən əvvəl müəyyən bir funksiyanı işlədə bilərik. 

Misal..  Məhsulların Backend-də olduğu bir Products.jsx səhifəsi var.  Biz  backend-dən məhsulların məlumatlarını çağırmadan Products səhifəsi qura bilərik? Əlbəttə ki, xeyir. Deməli Products.jsx komponenti yaranmazdan əvvəl bəckend-də sorğu göndərməliyik. Bunun üçün useEffect istifadə edəcik.

useEffect metodu parametr olaraq funksiya və komponentin vəziyyətini alır.  Adətən funksiya olaraq callback funtion yazırlar. Komponentin vəziyyətini isə kvadrat mörtərizədə yazırlar.

Sadə bir App.jsx qurub useEffect-in sintaksisinə baxaq. 

```jsx
// App.jsx faylı
import React from  'react'

const  App  =  ()  =>  {

	useEffect(()=>{
		console.log('App.jsx faylı yarandı')
	},[])	

	return (
		<div>
			<h1>useEffect Movzusu</h1>
		</div>
	)
}

export  default App
```
useEffect-də ikinci parametr olaraq yazdığınız kvadrat mörtərizə **[ ]** funksiyanın komponent yarananda işləməyi üçündür.  

İndi isə komponentin dəyişməsinə misal yazaq. komponentin içərisində olan dəyərin **(value)** dəyişmə vəziyyətini **[ value ]** olaraq yazacıq, və ya input taqında olan text dəyərinin dəyişməsini **[ text ]** olaraq yazacıq. Value-a aid misal yazaq. 
Misal... Button-a click etdikdə useState-də saxladığımız value bir vahid artsın. Və value hər dəyişəndə müəyyən bir funksiya işləsin. 
```jsx
// App.jsx faylı
import React, {useEffect,useState} from 'react'

const  App  =  ()  =>  {
	const [value, setValue] = useState(0)
	
	useEffect(()=>{
		console.log('App.jsx faylı yarandı')
	},[])	
	
	useEffect(()=>{
		console.log('Value deyisdi')
	},[value])

	return (
		<div>
			<button  onClick={()  =>  setValue(value +  1)}>Artır</button>
			<h1>{value}</h1>
		</div>
	)
}

export  default App
```
Componentin dəyişməsinə input taqı ilə misal edək.

```jsx
// App.jsx faylı
import React, {useEffect,useState} from 'react'

const  App  =  ()  =>  {
	const [text, setText] = useState('')
	
	useEffect(()=>{
		console.log('App.jsx faylı yarandı')
	},[])	
	
	useEffect(()=>{
		console.log('Text deyisdi')
	},[text])

	return (
		<div>
			<input value={text} onChange={(e)=>setText(e.target.value)}/>
			<h1>Text:{text}</h1>
		</div>
	)
}

export  default App
```

Son olaraq komponentin silinməsi zamanı işləyən funksiyayanın sintaksisinə baxaq. Bunun üçün useEffect() metodunda return function yazırıq. Funksiya adətən callback function olur. 
Misal... İnput adında komponentimiz olsun və içərisində bir ədəd input taqı olsun. App.jsx funksiyamızda button olsun. Buntton-a click etdikdə İnput komponenti görsənsin. Təkrar click etdikdə İnput componenti görsənməsin. Və biz İnput komponenti görsənməyəndə yəni komponent silinəndə useEffect ilə funksiyamızı çağıraq.
İnput adında komponent quraq.

```jsx
// Input.jsx fayli
import React,  {useEffect}  from  'react'

const  Input  =  ()  =>  {

	useEffect(()=>{
		console.log('component yarandi')
		
		return  ()  =>  {
			console.log('component silindi')
		}
	},[])
	
	return (
		<input  type="text"/>
	)
	
}
```
App.jsx faylında button quraq, useState ilə show adında dəyər saxlayaq. Hər click edəndə true olsa false, false olsa true etsin. Və hər true olanda İnput komponentini **çağırsın**. False olanda İnput komponentini **silsin**
```jsx
import React,  { useState }  from  'react'
import Input from  './Components/Input'

const  App  =  ()  =>  {
	const  [show,setShow]  =  useState(false)

	return (
		<div>
			<button  onClick={()=>setShow(!show)}>Toggle Show</button>
			{show &&  <Input/>}
		</div>
	);
}

export  default App
```

Və beləliklə komponentin bütün hallarını nəzərdən keçirtdik. 

Hazırladı - **Zahid Vahabzadə**
Video dərslər üçün Youtube kanalı - **Biraz Kod Yazaq**






