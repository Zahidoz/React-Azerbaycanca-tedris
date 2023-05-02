# useRef və forwardRef
Bu mövzu Javascript-dəki querySelector kimidir. React-da Müəyyən bir taqı seçib üzərində əməliyyatlar aparmaq istəyiriksə **useRef** istifadə edirik. Əgər müəyyən bir komponenti seçib üzərində əməliyyatlar aparmaq istəyiriksə **forwardRed** istifadə edirik. 

useRef - istifadə edərək bir taqı götürmək üçün həmin götürəcəyimiz taq-a ad veririk ki, üzərində əməliyyatlar aparanda həmin addan istifadə edək. Adı **useRef** ilə yaratdıqdan sonra taq daxilində həmin adı **ref** istifadə edərək yazırıq.

```jsx 
import React from  'react'
import  { useRef }  from  'react';

const App = () => {
	const inpt = useRef()
	
	return (
		<div>
			<input ref={inpt} type="text" />
		</div>
	);
}

export  default App
```

Indi isə gəlin bir button qoyaq və button-a click edəndə taqı console-a çıxardaq. Taqı görmək üçün adını yazıb nöqtə qoyub current yazırıq.

```jsx 
import React from  'react'
import  { useRef }  from  'react';

const  App  =  ()  =>  {
	const inpt = useRef()
	
	const showInpt = () =>  {
		console.log(inpt.current)
	}
	
	return (
		<div>
			<input ref={inpt}  type="text" />
			<button onClick={showInpt}>Show Input</button>
		</div>
	);
}

export  default App
```

İndi isə button-a click edəndə input taqını focuslayaq.

```jsx 
import React from  'react'
import  { useRef }  from  'react';

const  App  =  ()  =>  {
	const inpt = useRef()
	
	const showInpt = () =>  {
		inpt.current.focus()
	}
	
	return (
		<div>
			<input ref={inpt}  type="text" />
			<button onClick={showInpt}>Show Input</button>
		</div>
	);
}

export  default App
```

Bu formada istədiyimiz taqı useRef vasitəsi ilə götürə bilərik. Bəs input taqının yerində input komponenti olsaydı?
Bunun üçün komponentlərdə əlavə olaraq forwardRef istifadə edilir. və komponent parametr olaraq ( props. ref ) qəbul edir.

```jsx
import React,  { forwardRef }  from  "react";

const  Input  =  forwardRef((props,  ref)  =>  {
	return  <input  ref={ref}  {...props}  />;
});

export  default Input;
```
Komponentrimizi qurduq indi isə App.jsx faylında çağıraq.
```jsx 
import React,  { useRef }  from  'react'
import Input from  './Components/Input'

const  App  =  ()  =>  {
	const  inpt  =  useRef()
	
	const  showInpt  =  ()  =>  {
		inpt.current.focus()
	}
	
	return (
		<div>
			<Input  type="text"  ref={inpt}/>
			<button  onClick={showInpt}>Show Input</button>
		</div>
	);
}
export  default App
```

Və komponenti də referans olaraq götürməyi öyrəndik. Praktika etməyi unutmayın.


Hazırladı - **Zahid Vahabzadə**
Video dərslər üçün Youtube kanalım - **[Biraz Kod Yazaq]
