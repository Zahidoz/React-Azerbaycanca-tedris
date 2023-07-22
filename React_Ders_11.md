# Form , useForm, FormData

Web səhifələr ilk dəfə yarananda(web1 texnologiyasında) yalnız məlumatları oxumaq olurdu. Lakin artıq (web2 texnologiyasında) istifadəçilər web səhifəyə **məlumat daxil edə bilirlər**. Misal Facebook-da hərkəs öz adını yaşını və s. məlumatlarını  web səhifəyə daxil edə bilirdi və insanlar bir-biri ilə mesaj vasitəsi ilə əlaqə qurur. Və ən standart vəya özəl anlarında şəkillərini paylaşır və digərləri postu bəyənə və comment yaza bilər. Yəni qısa desək istifadəçilər öz məlumatlarını veb səhifəyə **yükləyə** bilir. Hal-hazırda artıq bütün demək olar ki, bütün veb səhifələrdə accaunt sistemləri var. Və həmin veb səhifəni istifadə edənlər öz məlumatlarını daxil edir. 

Və bu məlumatlar form taqları vasitəsi ilə daxil edilir. Və bu formların idarə olunmasını yəni - ad xanasında hərf olmalı, yaş yerində yalnız rəqəm olmalı, email xanasında mütləq @ işarəsi olmalı, bəzi xanalar mütləq doldurulmalı və s. qaydalar qoyulur.

Gəlin sadə bir form məsələsi quraq.
src folder-i daxilində style.scss faylı qurub form taqı üçün dizayn kodumuzu yazaq.
```scss
*{
	margin:  0;
	padding:  0;
	border:  none;
	outline:  none;
	box-sizing:  border-box;
	font-family:  Arial, Helvetica, sans-serif;
}
html{
	font-size:  10px;
}
body{
	display:  flex;
	align-items:  center;
	justify-content:  center;
	min-height:  100vh;
	background:  rgb(235,  235,  235);
}
  
form{
	padding:  3em  2em;
	display:  flex;
	flex-direction:  column;
	align-items:  center;
	gap:  1.5em;
	border-radius:  1.5em;
	background:  #fff;
	box-shadow:  0  0  20px  rgba(0,  0,  0,  0.098);
	input{
		width:  20em;
		border:  1px  solid  rgb(206,  206,  206);
		padding:  .4em  .8em;
		font-size:  1.6em;
		transition:  .2s;
		&:focus{
			border:  1px  solid  rebeccapurple;
			border-radius:  .5em;
		}
			&:hover{
			transform:  scale(1.03);
		}
	}
	button{
		background:  #fff;
		color:  rebeccapurple;
		padding:  .5em  1em;
		font-size:  1.5em;
		border:  1px  solid  rebeccapurple;
		cursor:  pointer;
		transition:  .2s;
		&:hover{
			background:  rebeccapurple;
			border-radius:  .5em;
			color:  #fff;
		}
	}
}
```
App.jsx faylına daxil olub scss faylını import edək və form strukturunu quraq.
```jsx
import React from  'react'
import  './style.scss'

const  App  =  ()  =>  {
	const  HandleSubmit  =  (e)  =>  {
		e.preventDefault();
		const  data  =  new  FormData(e.target);
		const  formProperties  = Object.fromEntries(data);
		console.log(formProperties)
	}
	return (
		<form  onSubmit={HandleSubmit}>
			<input  required  name='name'  type="text"  placeholder="enter name"  />
			<input  required  name='email'  type="email"  placeholder="enter email"  />
			<input  name='age'  type="number"  placeholder="enter age"  />
			<input  required  name='username'  type="text"  placeholder="enter username"  />
			<input  required  name='password'  type="password"  placeholder="enter password"  />
			<button  type='submit'>Submit Registration</button>
		</form>
	);
}
export  default App
```


Yuxarıdakı misalda istifadəçi üçün bəzi şərtlər qoysaq belə tam istədiyimiz şərtlər qoya bilmirik.  Misal- ad xanasında minimum 3 hərf olsun vəya yaş xanasında minimum 16-100 arası olsun, vəya təkrar parol düzgün olsun və s.

Bunun üçün React-da **react-hook-form** paketini yükləyək.
Dependency hissesinden yükləndiyindən əmin olun. Başlayaq.

useForm-u import edək.
**import  { useForm }  from  "react-hook-form";**

useForm-dan lazım olan propları çağıraq.
**const  {register, watch, handleSubmit, formState:  {  errors  } }  =  useForm();**

- **register** - daxilində şərtlərimizi yazacıq, şərtlərə əməl edilmədikdə error qaytaracaq.
- **watch**-  id-yə  uyğun input taqını götürür. e.target kimidir.
- **formState: {errors}** - register-dən error qayıdanda xətanı ekrana çıxaracaq.
- **handleSubmit** - form daxilində hərşey düzgündürsə onSubmit aktiv olacaq.

Gəlin bu dediklərimizi kodda yazaq. import edək, dəyişənləri çağıraq, və onSubmit funksiyamızı useForm-un handleSubmit funksiyasına bağlayaq.
```jsx
//App.jsx 
import React from  'react'
import  { useForm }  from  "react-hook-form";

const  App  =  ()  =>  {

	const  {  register,  handleSubmit,  watch, formState:  {  errors  }  }  =  useForm();
	
	const  onSubmit  =  (data)  =>  {
		console.log(data)
	}

	return (
		<form  onSubmit={handleSubmit(onSubmit)}>
			
			<button type="submit">
		</form>
	)
}

export  default App
```
İndi isə sadə bir input taqını necə useForm ilə işlədəcəyimizə baxaq. 
register vasitəsi ilə şərtlərimizi qoyacıq. Və əgər şərtlərə əməl edilməsə error qaytaracaq.
```jsx
<input id="name"
	{...register("name",  { required:  true, maxLength:  15, pattern: /^[A-Za-z]+$/i, })}
	className="txt-ipnt"
	type="text"
	placeholder="Ad"
></input>
```
Yuxarıdakı kodda 
* **required** - xananın mütləq doldurulmalıdır.
* **maxLength** - xananın maksimum simvol sayıdır.
* **minLength** - xananın minimum simvol sayıdır.
* **max** - maksimum ədəd limitidir.
* **min** - minimum ədəd limitidir.
* **pattern** - xananın hansı simvollardan istifadə edəcəyimizi deyir.
* **validate** - manual bir şərtə uyğunlaşmasını yoxlamaq üçündür.
* **valueAsDate** - tarixin qeyd edildiyini yoxlamaq üçündür.
* **valueAsNumber** - simvolların rəqəmlərdən olduğunu yoxlamaq üçündür.

```jsx
{errors.name && errors.name.type ===  "required"  && (
	<span  className="errorSpan">Ad hissəsi doldurulmalıdır.</span>
)}
{errors.name && errors.name.type ===  "pattern"  && (
	<span  className="errorSpan">Yalnız hərflərdən istifadə edin.</span>
)}
{errors.name && errors.name.type ===  "maxLength"  && (
	<span  className="errorSpan">Ad uzunluğu maksimum 15 olar.</span>
)}
```
Yuxarıdakı kodda əgər register-dən error gəlibsə həmin errora uyğun müvafiq xətanı ekrana çıxardlr.

Gəlin register və error-u tam formada yazaq.
```jsx
import React from  'react'
import  { useForm }  from  "react-hook-form";

const  App  =  ()  =>  {

	const  {  register,  handleSubmit,  watch, formState:  {  errors  }  }  =  useForm();
	
	return (
		<form  action="">
		
			<input id="name"
				{...register("name",  { required:  true, maxLength:  15, pattern: /^[A-Za-z]+$/i, })}
				className="txt-ipnt"
				type="text"
				placeholder="Ad"
			></input>
			{errors.name && errors.name.type ===  "required"  && (
				<span  className="errorSpan">Ad hissəsi doldurulmalıdır.</span>
			)}
			{errors.name && errors.name.type ===  "pattern"  && (
				<span  className="errorSpan"> Yalnız hərflərdən istifadə edin.</span>
			)}
			{errors.name && errors.name.type ===  "maxLength"  && (
				<span  className="errorSpan">Ad uzunluğu maksimum 15 olar.</span>
			)}
			
			<button type="submit">
			
		</form>
	)
}

export  default App
```

Artıq useForm ilə validation hazırdır. Bayaqkı misalda pattern sintaksisi yalnız hərflərdən istifadə edilməli olduğunu göstərir. İndi isə digər pattern-lərə diqqət yetirək.
```
 pattern: /^[A-Za-z]+$/i (yalnız böyük və kiçik hərflər)
 pattern: /\S+@\S+\.\S+/ (yalnız email sintaksisi)
 pattern: /^[0-9]+$/i (yalnız 0-9 arası rəqəmlər) vəya valueAsNumber
 pattern: /^[A-Za-z0-9]+$/i (yalnız hərflər və rəqəmlər) 
```

\
**Email**-ə uyğun input taqı quraq.
```jsx
<input id="email"
	{...register("email",  {required:  true,pattern: /\S+@\S+\.\S+/,})}
	className="txt-ipnt"
	type="text"
	placeholder="Email"
></input>
{errors.email && errors.email.type ===  "required"  && (
	<span  className="errorSpan">Email hissəsi doldurulmalıdır.</span>
)}
{errors.email && errors.email.type ===  "pattern"  && (
	<span  className="errorSpan">Email sintaksisini düzgün yazın.</span>
)}
```

**Yaş**-a uyğun input taqı quraq.
```jsx
<input id="age"
	{...register("age",  {required:  true,pattern: /^[0-9]+$/i,min: 18,max:  130,})}
	className="txt-ipnt"
	type="number"
	placeholder="Yaş"
></input>
{errors.age && errors.age.type ===  "required"  && (
	<span  className="errorSpan">Yaş hissəsi doldurulmalıdır</span>
)}
{errors.age && errors.age.type ===  "pattern"  && (
	<span  className="errorSpan">Yalnız rəqəmlərdən istifadə edin</span>
)}
{errors.age && errors.age.type ===  "min"  && (
	<span  className="errorSpan">Yaş uzunluğu minimum 18 olmalıdır</span>
)}
{errors.age && errors.age.type ===  "max"  && (
	<span  className="errorSpan">Yaş uzunluğu maksimum 130 olmalıdır.</span>
)}
```
Əlavə olaraq parol və parolun təkrarını istəyə bilərik. Bu tip məsələləri validate ilə edirlər.
```jsx
<input
	id="password"
	{...register("password",  { required:  true, minLength:  8  })}
	className="txt-ipnt"
	type="password"
	placeholder="Parol"
></input>
{errors.password && errors.password.type ===  "required"  && (
	<span  className="errorSpan">Parol hissəsi doldurulmalıdır.</span>
)}
{errors.password && errors.password.type ===  "minLength"  && (
	<span  className="errorSpan">Parol uzunluğu 8 olmalıdır</span>
)}
  
<input id="rpassword"
	{...register("rpassword",  {
		required:  true,
		validate:  (val)  =>  {
			if (watch("password") !== val) {
				return  "Parolun təkrarı düzgün deyil";
			}
		}
	})}

	className="txt-ipnt"
	type="password"
	placeholder="Parol (təkrar)"
></input>
{errors.rpassword && errors.rpassword.type ===  "required"  && (
	<span  className="errorSpan">Təkrar parolu yazın.</span>
)}
{errors.rpassword && errors.rpassword.type ===  "validate"  && (
	<span  className="errorSpan">Təkrar parolu düzgün yazın.</span>
)}
```
useForm-un öz veb səhifəsindən daha ətraflı araşdıra bilərsiz. Çox maraqlı dokumentasiyası var. Hətta videodərsləri də var.

---

Hazırladı - **Zahid Vahabzadə**
Video dərslər üçün Youtube kanalım - **[Biraz Kod Yazaq](https://www.youtube.com/channel/UCRlKqhooswsmfkxnokxcB0g
)**
