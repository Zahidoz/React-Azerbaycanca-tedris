# Events | onClick(), onChange()
Bu mövzu JS-dəki addEventListener mövzusu kimidir. Sadəcə biraz sintaksis fərqləri var.
Əgər Veb səhifədə hansısa input taqında klaviatura ilə nəsə yazdıqda vəya hansısa taqa mouse ilə click etdikdə, scroll etdikdə və s. əməliyyatlar apardıqda hansısa kod blokunun işləməyini istəyiriksə taq daxilində onChange(), onClick(), onScroll və s kimi keyword istifadə olunur.

Misal - bir button quraq və button-a click etdikdə console-a "click edildi" yazısı çıxsın. Bunun üçün
* bir funksiya olacaq içərisində console.log olacaq
* button taqı olacaq, button-a click etdikdə funksiyanı çağırsın.

Sadə bir App.jsx faylı quraq. 
```jsx
import React from  'react'

const  App  =  ()  =>  {

	const  ShowConsole  =  ()  =>  {
		console.log('click edildi')
	}
	
	return (
		<div>
			<h1>Event Movzusu</h1>
			<button  onClick={ShowConsole}>Click Here</button>
		</div>
	)
	
}

export  default App
```
Bu event-lər parametr olaraq JavaScript-də olan addEventListener kimi funksiya istəyir. Ona görə də event adını yazdıqdan sonra scope içərisində funksiya çağırırıq( **onClick={ShowConsole}** ). Burada sadə funksiya, Arrow funksiya və callback funksiya yaza bilərik. Gəlin əvvəlki kodu sadə yox callback funksiya kimi çağıraq.

```jsx
import React from  'react'

const  App  =  ()  =>  {
	return (
		<div>
			<h1>Event Movzusu</h1>
			<button  onClick={()=>{console.log('click edildi')}}>Click Here</button>
		</div>
	)
	
}

export  default App
```

indi isə bir taq seçək və taqa click etdikdə həmin taqı və taqın içərisindəki məlumatlarını götürək.
```jsx
import React from  'react'

const  App  =  ()  =>  {
	const  TagInfo  =  (e)  =>  {
		console.log(e.target);
		console.log(e.target.innerHTML);
	};

	return (
		<div>
			<h1>Event Movzusu</h1>
			<p  onClick={TagInfo}>Burada paraqraf var</p>
		</div>
	)
}

export  default App
```
Gördüyünüz kimi paraqraf taqına click etdikdə p taqını və taq içərisindəki yazını console-a çıxartdıq.
Əlavə olaraq onChange event də var. Əslində çoxlu event-lər var, sadəcə çox istifadə olunanlardan bir ikisinə misal yazacıq. 
Misal - İnput taqında nəsə yazdıqda funksiya işə düşsün. Və funksiya yazdığımı console-a çıxartsın.

```jsx
import React from  'react'

const  App  =  ()  =>  {
	const  InputHandle  =  (e)  =>  {
		console.log(e.target.innerHTML);
	};

	return (
		<div>
			<h1>Event Movzusu</h1>
			<input  onChange={InputHandle}  type="text"  />
		</div>
	)
}

export  default App
```
Gəlin bu kodu da callback function ilə yazaq)

```jsx
import React from  'react'

const  App  =  ()  =>  {
	return (
		<div>
			<h1>Event Movzusu</h1>
			<input  onChange={(e)=>console.log(e.target.innerHTML)} />
		</div>
	)
}

export  default App
```

Digər event-lər haqda öyrənmək üçün react-ın şəxsi veb səhifəsinin dokumentasiyalarına baxa bilərsiniz. Burda sadəcə işləmə prinsipini öyrəndik.
