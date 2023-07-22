# Redux , Redux Toolkit

Redux demək olarki useContext kimidir. Yəni  dəyərləri qlobalda saxlamaq üçündür. Və iri şirkətlərdə Qlobal State Managment olaraq 90% redux istifadə olunur.

Gəlin sadə bir counter misalı ilə başlayaq. 
components folderi daxilində Counter.jsx və ChangeCounter.jsx faylları quraq.

- Counter.jsx - counter dəyərinə baxmaq üçün,
- ChangeCounter.jsx - counter dəyərini dəyişmək üçün istifadə edəcik

Hər ikisinə rafce-( jsx strukturu ) yazdıqdan sonra App.jsx faylında import edək.
```jsx
import React from  "react";
import ChangeCounter fr		om  "./components/ChangeCounter";
import Counter from  "./components/Counter";
  
const  App  =  ()  =>  {
	return (
		<div>
			<h1>Redux | Global State Management</h1>
			<Counter/>
			<ChangeCounter/>
		</div>
	);
};

export  default App;
```

Parent Componentimiz olan App.jsx faylında counter adında state quraq. 
Counter componentinə counter dəyərini göndərək.
ChangeCounter komponentinə counter dəyərini və setCounter metodunu göndərək.

```jsx
// App.jsx faylı
import React from  "react";
import  { useState }  from  "react";
import ChangeCounter from  "./components/ChangeCounter";
import Counter from  "./components/Counter";
  
const  App  =  ()  =>  {
	const  [counter,setCounter]  =  useState()
  
	return (
		<div>
			<h1>Redux | Global State Management</h1>
			<Counter  counter={counter}/>
			<ChangeCounter  counter={counter}  setCounter={setCounter}/>
		</div>
	);
};
  
export  default App;
```

```jsx
// Counter.jsx
import React from  'react'
  
const  Counter  =  ({counter})  =>  {
	return (
		<div>
			<h1>Counter: {counter}</h1>
		</div>
	)
}
  
export  default Counter
```

```jsx
// ChangeCounter.jsx
import React from  'react'

const  ChangeCounter  =  ({counter,setCounter})  =>  {
	return (
		<div>
		<button  onClick={()  =>  setCounter(counter +  1)}>Artir</button>
		<button  onClick={()  =>  setCounter(counter -  1)}>Azalt</button>
		<button  onClick={()  =>  setCounter(counter +  5)}>5 Artir</button>
		</div>
	);
}  
  
export  default ChangeCounter
```

Artıq counter-imiz hazırdır.
Gəlin counter dəyərini redux ilə qlobalda dayər kimi saxlayaq.

- Terminalda **npm i @reduxjs/toolkit react-redux** yazıb yükləyək.
- store adında folder qurub içərisində index.jsx faylı quraq.
- həmin faylda konfiqurasiya kodlarımızı yazaq
- index.js( root ) fayında Provider import edib store faylımıza bağlayaq.
- store folderi daxilində counter.js faylı quraq.
- daxilində ona aid redux kodlarını yazaq
- son olaraq store/index.js faylında reducer-ə counter-i əlavə edək.

Bu saydıqlarımızı bir-bir edək. Terminalda paketi yüklədikdən sonra store folderi qurub içərisində index.js faylı quraq. 

reducer daxili hələki boş qalacaq. counter-i yazdıqdan bu faylda yenidən birləşdirəcik.
```js
// store/index.js
import  {configureStore}  from  '@reduxjs/toolkit'
  
export  default  configureStore({
	reducer:{
	
	}
})
```

Sonra root olan index.js faylında Provider import edib store ilə bağlayaq. 
Eyni useContext-dəki kimi )
```jsx
import React from  'react';
import ReactDOM from  'react-dom/client';
import App from  './App';
  
import  { Provider }  from  'react-redux';
import store from  './store';
 
  
const  root  = ReactDOM.createRoot(document.getElementById('root'));
root.render(
	<Provider  store={store}>
		<App  />
	</Provider>
);
```
Provider ilə birləşdirib əlaqəni qurduq. Artıq qlobalda olan dəyərlərimizi yaradaq. Bunun üçün store folderi daxilində counter.js faylı quraq.
```js
import  {createSlice}  from  '@reduxjs/toolkit'
  
export  const  counter  =  createSlice({
	name:  'counter',
	initialState:  {
		value:  1
	},
	reducers:  {
		increment:  (state)=>{
			state.value+=1
		},
		decrement:  (state)=>{
			state.value-=1
		},
		incrementByAmount:  (state,action)=>{
			state.value+=action.payload
		}
	}
})
  
export  const  {increment,decrement,incrementByAmount}  = counter.actions
  
export  default counter.reducer
```
Yuxarıdakı kodda 
- initialValue - başlanğıc dəyərlər
- reducer - set metodları yazılır.
Son olaraq counter faylını store folderində olan index.js faylında import edib birləşdirək.

```js
import  {configureStore}  from  '@reduxjs/toolkit'
import counter from  './counter'
  
export  default  configureStore({
	reducer:{
		counter: counter
	}
})
```
Hər şey hazırdır. Artıq qlobal dəyəri komponentlərdə istifadə edə bilərik.
Artıq App.jsx faylında useState kodlarını silək. Komponentlərə göndərdiyimiz counter və setCounter - idə silin. 
```jsx
import React from  "react";
import ChangeCounter from  "./components/ChangeCounter";
import Counter from  "./components/Counter";
  
const  App  =  ()  =>  {
	return (
		<div>
			<h1>Redux | Global State Management</h1>
			<Counter/>
			<ChangeCounter/>
		</div>
	);
};
  
export  default App;
```
İndi isə Counter və ChangeCounter fayllarındalı prop-ları təmizləyək.
```jsx
import React from  'react'
  
const  Counter  =  ()  =>  {
	return (
		<div>
			<h1>Counter: </h1>
		</div>
	);
}
  
export  default Counter
```
```jsx
import React from  'react'
  
const  ChangeCounter  =  ()  =>  {
	return (
		<div>
			<button>Artir</button>
			<button  >Azalt</button>
			<button>5 Artir</button>
		</div>
	);
}
  
export  default ChangeCounter
```
Komponentləri yenə əvvəlki halına gətirdik. İndi isə gəlin komponentlərdə qlobalda olan counter-i çağıraq.
- dəyəri get( çağırmaq ) etmək üçün **useSelector**
- dəyəri set( dəyişmək ) etmək üçün **useDispatch** istifadə olunur.

Qısa desək useState-də solda yazılan dəyəri useSelector ilə çağıracıq. Sağda yazılan metodu useDispatch ilə dəyişəcik.

Birinci Counter.js faylında dəyəri çağırmaq üçün useSelector ilə başlayaq.

```jsx
import React from  'react'
import  {useSelector}  from  'react-redux'
  
const  Counter  =  ()  =>  {
  
const  counter  =  useSelector((state)=>state.counter.value)
  
return (
	<div>
		<h1>Counter: {counter}</h1>
	</div>
);
}
  
export  default Counter
```
useSelector geriyə state qaytarır və biz state-dən counter-i seçdik. 
Ekranda artıq dəyərimiz görünür. İndi isə gəlin ChangeCounter komponentində useDispatch ilə dəyəri dəyişək.

```jsx
import React from  'react'
  
import  {useDispatch}  from  'react-redux'
import  {increment,decrement,incrementByAmount}  from  '../store/counter'
  
const  ChangeCounter  =  ()  =>  {
  
	const  dispatch  =  useDispatch()
  
	return (
		<div>
			<button  onClick={()  =>  dispatch(increment())}>Artir</button>
			<button  onClick={()  =>  dispatch(decrement())}>Azalt</button>
			<button  onClick={()  =>  dispatch(incrementByAmount(5))}>5 Artir</button>
		</div>
	);
}
  
export  default ChangeCounter
```

useDispatch vasitəsi ilə lazımi reducer-lərdən istifadə edərək dəyəri dəyişdik.  

---

Hazırladı - **Zahid Vahabzadə** 
Video dərslər üçün Youtube kanalım - **[Biraz Kod Yazaq](https://www.youtube.com/channel/UCRlKqhooswsmfkxnokxcB0g)** 
React-dan digər dokumentlər üçün - **[Github kanalım](https://github.com/Zahidoz/React-Azerbaycanca-tedris)**
