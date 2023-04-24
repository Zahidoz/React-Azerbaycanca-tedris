# Component-ə props göndərmək

Component-ə props(məlumat,data) göndərmək bizə nə üçün lazımdır
Gəlin bunu sadə misal üzərində başa düşək.
Düşünün ki, biz mağaza üçün məhsulların olduğu bir veb səhifə hazırlayırıq və bu məhsulları tanıtmaq üçün çoxlu card tipində component olmalıdır. Və hər bir komponentin daxilində məhsulun şəkli, adı, modeli, qiyməti və almaq üçün button lazımdır. 
O zaman Card component qurmaqla başlayaq.
* App.jsx faylı üçün src içərisində style.scss faylı quraq.
* Components adında folder qurub içərisində Card.jsx fayı quraq.
* rafce yazıb jsx strukrurunu qurun və funksiya adını və export olaraq Card yazaq

```jsx
// Card.jsx faylı
import React from  'react'

const  Card  =  ()  =>  {
	return (
		<div  className='card-wrapper'>
			<img  src="https://via.placeholder.com/600/92c952"  alt=""  />
			<h2>Product 1</h2>
			<h4>129$</h4>
			<button>Buy Now</button>
		</div>
	)
}

export  default Card
```
HTML strukturunu bitirdikdən sonra **style.scss** faylında dizayn edək.
```scss
*  {
	margin:  0;
	padding:  0;
	list-style:  none;
	text-decoration:  none;
	border:  none;
	outline:  none;
	box-sizing:  border-box;
}

.cards-c  {
	max-width:  1440px;
	margin:  auto;
	display:  flex;
	padding:  20px;
	gap:  20px;
	.card-wrapper  {
		width:  250px;
		height:  330px;
		box-shadow:  0  0  5px  rgba(109,  109,  109,  0.482);
		display:  flex;
		flex-direction:  column;
		align-items:  center;
		gap:  16px;
		img  {
			max-width:  100%;
			height:  150px;
			object-fit:  cover;
		}
		h2  {
			font-size:  28px;
			color:  rgb(31,  90,  92);
			letter-spacing:  1px;
			text-align:  center;
		}
		h4  {
			font-size:  22px;
			color:  gray;
			letter-spacing:  1px;
			text-align:  center;
		}
		button  {
			padding:  8px  16px;
			background:  rgb(31,  90,  92);
			color:  #fff;
			font-size:  18px;
			letter-spacing:  1px;
			cursor:  pointer;
		}	
	}
}
```
Card Componenti hazırdır. Artıq App.jsx faylına çağırmaq qaldı.
```jsx
import React from  'react'
import Card from  './Components/Card'

const  App  =  ()  =>  {
	return (
		<div className="cards-c">
			<Card/>
		</div>
	)
} 

export  default App
```

Əla... Card Component-imiz ekranda render olundu. Bəs mən ikinci məhsulun məlumatlarına uyğun Card hazırlamaq istəsəm... bir də yenidən Card2.jsx faylı qurmalıyam??? Bəs necə edək ki, Component dizayni və funksiyası olduğu kimi qalsın amma içərisindəki məlumatlar bizim istəyimizə uyğun dəyişsin. Bunun üçün biz Component-ə **props** - (yəni məlumat, data) göndərməliyik. Gəlin komponentimizi dinamik hala gətirək.
* product1 adında obyekt qurub məlumatları yazaq.
* Card komponentinə product adı ilə obyektimizi göndərək.
* Adını solda, göndərdiyimi scope { }  içərisində yazıdıq.

```jsx
import React from  'react'
import Card from  './Components/Card'

const  App  =  ()  =>  {
	const  product1  =  {
		img:  "https://via.placeholder.com/600/92c952",
		name:  "Product1",
		model:  "Model1",
		price:  129
	}
	return (
		<div className="cards-c">
			<Card product={product1} />
		</div>
	)
} 

export  default App
```

product1 obyektini **product** adı ilə göndərdiyimiz üçün Card Componentində həmin ad ilə qəbul etməliyik. Funksiyada parametr göndərmək kimi, yalnız burda componentə göndərdiklərimizə bir **ad qoyuruq** və componentimizdə **qoyduğumuz adda** qəbul edirik.

```jsx
// Card.jsx faylı
import React from  'react'

const  Card  =  ({product})  =>  {
	return (
		<div  className='card-wrapper'>
			<img  src={product.img}  alt=""  />
			<h2>{product.name}  {product.model}</h2>
			<h4>{product.price}$</h4>
			<button>Buy Now</button>
		</div>
	)
}

export  default Card
```
Diqqət yetirdinizsə Card komponenti prop olaraq scope içərisində {product} qəbul etdi və HTML taqları içərisində product obyektin məlumatlarını çıxarmaq üçün scope içərisində yazıldı. 

İndi isə eyni bu formada ikinci məhsulu hazırlayaq.

```jsx
import React from  'react'
import Card from  './Components/Card'

const  App  =  ()  =>  {
	const  product1  =  {
		img:  "https://via.placeholder.com/600/92c952",
		name:  "Product1",
		model:  "Model1",
		price:  129
	}
	const  product2  =  {
		img:  "https://via.placeholder.com/600/771796",
		name:  "Product2",
		model:  "Model2",
		price:  255,
	};
	return (
		<div className="cards-c">
			<Card product={product1} />
			<Card product={product2} />
		</div>
	)
} 

export  default App
```

Və ikinci məhsulumuz da hazırdır. Lakin məhsul sayı çoxaldıqca kodumuz kobud görsənəcək. Əslində bilirik ki, bu tip məlumatlar JSON faylda saxlanılır.
**JSON** - eyni tipli obyektlərin olduğu array 
O zaman 5 productun olduğu bir JSON quraq.
src folder-in daxilində products.json adında fayl quraq. Və array daxilində obyektlərimizi yerləşdirək.
```json
[
	{
		"id":  1,
		"img":  "https://via.placeholder.com/600/92c952",
		"name":  "Product1",
		"model":  "Model1",
		"price":  129
	},
	{
		"id":  2,
		"img":  "https://via.placeholder.com/600/771796",
		"name":  "Product2",
		"model":  "Model2",
		"price":  255
	},
	{
		"id":  3,
		"img":  "https://via.placeholder.com/600/24f355",
		"name":  "Product3",
		"model":  "Model3",
		"price":  410
	},
	{
		"id":  4,
		"img":  "https://via.placeholder.com/600/d32776",
		"name":  "Product4",
		"model":  "Model4",
		"price":  62
	},
	{
		"id":  5,
		"img":  "https://via.placeholder.com/600/f66b97",
		"name":  "Product5",
		"model":  "Model5",
		"price":  720
	},
	{
		"id":  6,
		"img":  "https://via.placeholder.com/600/56a8c2",
		"name":  "Product6",
		"model":  "Model6",
		"price":  400
	}
]
```

JSON faylımız hazırdır. App.jsx faylına JSON faylımızı import edək.

Products adında olan məhsullarımızı bir-bir ekrana çıxartmaq üçün **map()** metodundan istifadə edəcik. Dediyimiz kimi, HTML içərisində JS kodu yazırıqsa **scope** içərisində yazmalıyıq. Amma həmin scope içərisində təkrar HTML kodu yazmaq istəyiriksə təkrar **return()** yazıb geriyə bir taq qaytarırıq **! ! !**
```jsx
import React from  'react'
import Card from  './Components/Card'
import products from  './products.json'

const  App  =  ()  =>  {

	return (
		<div className="cards-c">
			{
				products.map(item=>{
					return(
						<Card  product={item}/>
					)
				})
			}
		</div>
	)
} 

export  default App
```

Və beləliklə bütün məhsulları JSON fayldan oxudaraq ekrana çıxartdıq. map() metodu JSON-da olan obyektlərin üzərindən bir-bir keçərkən hər dəfə yeni bir Card komponenti yaradıb prop olaraq həmin obyekti göndərdi.

Lakin veb səhifədə sağ düyməyə click edib console-u açsaq 
**Warning: Each child in a list should have a unique "key" prop.** tipində bir error olduğunu görəcik. Yəni onu demək istəyirki bu Card komponentləri bir-birindən fərqləndirmək üçün hərəsinə özəl açar olmalıdır. Biz də bunun üçün həmişə JSON faylda obyektlərə id yazırıq. Və heç bir id digəri ilə eyni ola bilməz.
O zaman gəlin key olaraq obyektin id-ni yazaq.
```jsx
import React from  'react'
import Card from  './Components/Card'
import products from  './products.json'

const  App  =  ()  =>  {

	return (
		<div className="cards-c">
			{
				products.map(item=>{
					return(
						<Card key={item.id} product={item}/>
					)
				})
			}
		</div>
	)
} 

export  default App
```

Hazırladı - **Zahid Vahabzadə**
Video dərslər üçün Youtube kanalı - **Biraz Kod Yazaq**
