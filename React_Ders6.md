# useState 
React-da əsas dəyərlər state-də saxlanılır. State-də dəyər saxlamaq üçün React Hook-lardan biri olan useState mövzusunu öyrənəcik. 
Daha ətraflı başa düşmək üçün sintaksisinə baxaq. Sadə bir App.jsx faylı quraq. useState-i import edək və quraq.

```jsx
import React from  'react'
import  { useState }  from  'react'

const  App  =  ()  =>  {
	const  [value,setValue]  =  useState(0)
	
	return (
		<div>
			<h1>UseState Movzusu</h1>
		</div>
	)
}

export  default App
```

Sintaksisi **const  [value,setValue]  =  useState( 0 )** tipdə olur. 
useState 3 parametr qəbul edir.
* **value** dəyəri görmək üçün vəya istifadə etmək üçündür.
* **setValue**  dəyəri dəyişmək üçün metoddur.
* **( 0 )** - mörtərizə içərisində value-nun **başlanğıc qiyməti** yazılır. və burada value-nun başlanğıc qiyməti sıfırdır. 

Daha bir misal yazaq. 
**const  [ isStudent, setIsStudent ]  =  useState( false )**
* **isStudent** dəyəri görmək üçün vəya istifadə etmək üçündür.
* **setIsStudent**  dəyəri dəyişmək üçün metoddur.
* **( false )** - mörtərizə içərisində value-nun **başlanğıc qiyməti** yazılır. və burada isStudent-in başlanğıc qiyməti false - dur.

Indi isə state-də saxladığımız value dəyərini ekrana çıxardaq. 
Xatırlatma!! - Javascript kodunu HTML-də istifadə etmək üçün { } scope içərisində yazılır.


```jsx
import React from  'react'
import  { useState }  from  'react'

const  App  =  ()  =>  {
	const  [value,setValue]  =  useState(0)
	
	return (
		<div>
			<h1>UseState Movzusu</h1>
			<h1>{value}</h1>
		</div>
	)
}

export  default App
```
Value dəyərini ekrana çıxartdıq. İndi isə setValue istifadə edərək dəyəri dəyişəq. 
Misal - Bir button olsun, button-a click etdikdə state-də olan dəyəri 5 etsin. Bunun üçün ChangeNumber adında bir funksiya quraq və içərisində set kodumuzu yazaq. Və button-a click olanda funksiyamızı çağıraq.

```jsx
import React from  'react'
import  { useState }  from  'react'

const  App  =  ()  =>  {
	const  [value,setValue]  =  useState(0)
	const  ChangeNumber  =  ()  =>  {
		setValue(5)
	}
	
	return (
		<div>
			<h1>UseState Movzusu</h1>
			<h1>{value}</h1>
			<button  onClick={ChangeNumber}>Change to 5</button>
		</div>
	)
}

export  default App
```
Button-a click etdikdə **ChangeNumber** funksiyamız işə düşdü və funksiyada **setValue(5)** yazaraq value dəyərini 5-ə bərabər etdik. Value 5 olan kimi avtomatik Veb səhifədə də qiyməti dəyişdi.
İndi isə gəlin button-a hər click etdikdə value dəyərini 1 vahid artıraq. 
```jsx
import React from  'react'
import  { useState }  from  'react'

const  App  =  ()  =>  {
	const  [value,setValue]  =  useState(0)
	const  AddNumber  =  ()  =>  {
		setValue(value+1)
	}
	
	return (
		<div>
			<h1>UseState Movzusu</h1>
			<h1>{value}</h1>
			<button  onClick={AddNumber}>Change to 5</button>
		</div>
	)
}

export  default App
```
Artıq button-a hər click etdikdə value 1 vahid artdı.

## useState Component məntiqi
Gəlin useState-in Componentlərdə işləmə prinsipinə baxaq. Əvvəlki misaldakı value istifadə etdiyimiz h1 taqını və setNumber istifadə etdiyimiz button taqını ayrı-ayrı komponentlərə ayıraq. 
Bunun üçün src içərisində Components folder-i qurub içərisində Number.jsx və Button.jsx faylları qurub rafce edin(jsx strukturu qurun).



* Number.jsx də h1 taqı içərisində value görsənməlidir. Bunun üçün Number komponentinə {value} dəyərini göndərək.

```jsx
import React from  'react'
  
const  Number  =  ({value})  =>  {
	return (
		<h1>{value}</h1>
	)
}

export  default Number
```

Və App.jsx faylında h1 taqı əvəzinə  Number komponentini çağıraq. Komponenti istifadə edərkən value dəyərini göndərməyi unutmayın.

```jsx
import React from  'react'
import  { useState }  from  'react'
import Number from  './Components/Number'

const  App  =  ()  =>  {
	const  [value,setValue]  =  useState(0)
	const  AddNumber  =  ()  =>  {
		setValue(value+1)
	}
	
	return (
		<div>
			<h1>UseState Movzusu</h1>
			<Number  value={value}/>
			<button  onClick={AddNumber}>Change to 5</button>
		</div>
	)
}

export  default App
```
Əla... Number komponentimiz value dəyərini ekranda göstərdi. İndi isə Button komponentimizi hazırlayaq. Button.jsx faylına daxil olaq. Diqqət yetirsək görərik ki, buttona click olanda value və setValue dan istifadə etmişik. Deməli biz komponentdə bunları istifadə etmək üçün props olaraq {value , setValue}-nu göndərməliyik.
```jsx
import React from  "react";

const  Button  =  ({  value,  setValue  })  =>  {

	const  AddNumber  =  ()  =>  {
		setValue(value+1);
	};
	
	return  (
		<button  onClick={AddNumber}>Add Number</button>
	);
};
  
export  default Button;
```
Son olaraq Button komponentini App.jsx faylında çağıraq. Komponenti istifadə edərkən value və setValue dəyərlərini göndərməyi unutmayın. Və artıq App.jsx faylında AddNumber funksiyasına ehtiyyac qalmadı. Çünki funksiyanı artıq Button komponentində istifadə etmişik.

```jsx
import React from  'react'
import  { useState }  from  'react'
import Number from  './Components/Number'
import Button from  './Components/Button'

const  App  =  ()  =>  {
	const  [value,setValue]  =  useState(0)
	
	return (
		<div>
			<h1>UseState Movzusu</h1>
			<Number  value={value}/>
			<Button  value={value}  setValue={setValue}/>
		</div>
	)
}

export  default App
```

Arıq useState istifadə edərək Compontə state-dəki dəyəri və metodunu göndərməyi öyrəndik. Praktika etməyi unutmayın!!!












