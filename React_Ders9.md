# useReducer
State-də olan dəyərlər qrup halında tez-tez dəyişirsə rahat formada idarə etmək üçün useReducer istifadə olunur. 
Gəlin sadə bir misal üzərində izah edək.
Bir button olsun və button-a click etdikdə API-dən gələn datanı ekrana çıxartsın.

Bizim 3 state dəyərə ehtiyyacımız olacaq.
* **loading** - button-a click etdikdə API-dən **cavab gələnə qədər** true olacaq.
* **error** - API-dən **yanlış** response gəlsə true olacaq.
* **data** - API-dən **doğru** gələn dataya bərabər olacaq.

Fake API olan JSON placeholder-ə **/posts/1** -linkinə request göndərək.

```jsx
//App.jsx faylı
import React,  {useState}  from  'react'

const  App  =  ()  =>  {

const  [loading,  setLoading]  =  useState(false);
const  [data,  setData]  =  useState({});
const  [error,  setError]  =  useState(false);

const  HandleFetch  =  async()  =>  {
	setData({});
	setError(false)
	setLoading(true);
	
	fetch("https://jsonplaceholder.typicode.com/posts/1")
		.then(res  => res.json())
		.then(data  =>  {
			setData(data)
			setLoading(false)
		})
		.catch(err=>  {
			setError(true)
			setLoading(false);
		})
}

	return (
		<div>
			<h1>UseReducer</h1>
			<button  onClick={HandleFetch}>{loading ?  "Loading"  :  "Fetch Post"}</button>
			<h2>{data?.title}</h2>
			<span>{error &&  "FETCH ERROR"}</span>
		</div>
	);
}

export  default App
```

Misalda button-a click etdikdə APİ-dən məlumat(data) gəlir, əgər data gəlsə title propert-si ekrana çıxır, data gəlməsə error ekrana çıxır.
Lakin HandleFetch funksiyasının kod blokunda 3 qrupa ayrılmış 7 dənə set metodu işlətmişik. 
```jsx
setData({});
setError(false)
setLoading(true);

setData(data)
setLoading(false)

setError(true)
setLoading(false);
```

bu 3 dənə qrup formasında olan kodların hərəsini useReducer vasitəsi ilə **bir sətirə** yaza bilərik.

useReducer istifadə etmək üçün src folder-i daxilində **postReducer.js** adında bir fayl quraq.
* Başlanğıc dəyrlərimizi **İNİTİAL_STATE** adında bir dəyişəndə saxlayaq. useState-dəki birinci parametr kimidir.
```jsx
export  const  INITAL_STATE  =  {
	loading:  false,
	data:  {},
	error:  false
};
```
Əlavə olaraq state-də olan dəyişənlərimizi qrup halında dəyişmək üçün bir set metodumuz olacaq. useState-dəki ikinci parametrdə olan set metodu kimidir.

Aşağıdakı postReducer funksiyamız parametr olaraq **state** və **action** alıblar. 
* state bildiyimiz həmin 3 dəyərdir.
* action isə dəyərləri qrup halında dəyişərkən **qoyduğumuz addır**.

O zaman həmin 3 qrupa bölünmüş set metodunu action.type vasitəsi ilə ad verək və artıq həmin ad ilə çağıranda yazdığımız set metodları biryerdə işləyəcək.

```jsx 
// postReducer.js faylı
export  const  INITAL_STATE  =  {
	loading:  false,
	data:  {},
	error:  false
};

export  const  postReducer  =  (state,  action)  =>  {
	switch (action.type) {
		case  "FETCH_START":
			return  {
				loading:  true,
				data:  {},
				error:  false,
			};
		case  "FETCH_SUCCESS":
			return  {
				loading:  false,
				data: action.payload,
				error:  false,
			};
		case  "FETCH_ERROR":
			return  {
				loading:  false,
				data:  {},
				error:  true,
			};
		default:
			return state
	}
};
```
Gördüyünüz kimi **action.type** vasitəsi ilə state-lərin qrup halda dəyişməsinə **ad veririk**. Və həmin FETCH_START,  FETCH_SUCCESS, FETCH_ERROR - dan istidadə etdikdə state-dəki dəyərlər qeyd etdiyimiz kimi dəyişəcək.  
Bu hazırlağımız İNİTİAL_VALUE və postReducer - i App.jsx faylında çağıraq useReducer quraq.
*  İNİTİAL_VALUE və postReducer - i import edək.
* const  [state,dispatch]  =  useReducer(postReducer,  INITAL_STATE) yazaq.
* state yazıb nöqtə qoyaraq dəyərləri çağıraq. 
* dispatch  yazıb set metodunun adını  yazaraq dəyərləri qrup halında dəyişə bilərik.
* dispatch daxilində parametr göndərərək istənilən dəyəri parametrə bərabər edə bilərik. Aşağıda FETCH_SUCCESS metoduna **payload** adı ilə data-nı göndərdik **( payload: data )** Və Yuxarıdakı kodda postReducer funksiyasın FETCH_SUCCESS metodunda **( action.payload ) ** yazaraq data-ya bərabər edirik.

Aşağıda request-dən gələn data-nı  yazaraq göndərdik.
```jsx
//App.jsx faylı
import React,  {useState}  from  'react'

import  { useReducer }  from  'react'
import  { INITAL_STATE, postReducer }  from  './postReducer'

const  App  =  ()  =>  {

const  [state,dispatch]  =  useReducer(postReducer,  INITAL_STATE);

const  HandleFetch  =  async()  =>  {
	dispatch({ type: "FETCH_START" });
	
	fetch("https://jsonplaceholder.typicode.com/posts/1")
		.then(res  => res.json())
		.then(data  =>  {
			dispatch({ type: "FETCH_SUCCESS", payload: data });
		})
		.catch(err=>  {
			dispatch({ type: "FETCH_ERROR"});
		})
}

	return (
		<div>
			<h1>UseReducer</h1>
			<button  onClick={HandleFetch}>{state.loading ?  "Loading"  :  "Fetch Post"}</button>
			<h2>{state.data?.title}</h2>
			<span>{state.error &&  "FETCH ERROR"}</span>
		</div>
	);
}

export  default App
```

Kodumuzun daha səliqəli olması üçün actionTypes adında js faylı quraq, bu action-lar postlar ilə əlaqəlidir deyə fayl adını postActionTypes.qoyaq. SRC folderi daxilində postActionTypes.jsx faylıq qurun və ACTION_TYPES adında bir dəyişəni export edək.
```js
// postActionTypes.js faylı

export  const  ACTION_TYPES  =  {
	FETCH_START:  "FETCH_START",
	FETCH_SUCCESS:  "FETCH_SUCCESS",
	FETCH_ERROR:  "FETCH_ERROR"
};
```

Və App.jsx faylında Action adlarını bu fayldan çağıraq.

```jsx
//App.jsx faylı
import React,  {useReducer}  from  'react'
import  {ACTION_TYPES}  from  './postActionTypes'
import  { INITAL_STATE, postReducer }  from  './postReducer'

const  App  =  ()  =>  {

const  [state,dispatch]  =  useReducer(postReducer,  INITAL_STATE);

const  HandleFetch  =  async()  =>  {
	dispatch({ type: ACTION_TYPES.FETCH_START });
	
	fetch("https://jsonplaceholder.typicode.com/posts/1")
		.then(res  => res.json())
		.then(data  =>  {
			dispatch({ type: ACTION_TYPES.FETCH_SUCCESS, payload: data });
		})
		.catch(err=>  {
			dispatch({ type: ACTION_TYPES.FETCH_ERROR});
		})
}

	return (
		<div>
			<h1>UseReducer</h1>
			<button  onClick={HandleFetch}>{state.loading ?  "Loading"  :  "Fetch Post"}</button>
			<h2>{state.data?.title}</h2>
			<span>{state.error &&  "FETCH ERROR"}</span>
		</div>
	);
}

export  default App
```

Və beləliklə istədiyimiz state-ləri qruplaşdırıb 1 metod istifadə edərək dəyişə bilərik. Praktika etməyi unutmayın.

Hazırladı - **Zahid Vahabzadə**
Video dərslər üçün Youtube kanalım - **[Biraz Kod Yazaq](https://www.youtube.com/channel/UCRlKqhooswsmfkxnokxcB0g
)**






