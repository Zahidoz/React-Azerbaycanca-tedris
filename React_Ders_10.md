# memo, useCallback, useMemo
React-ın əsas xüsusiyyətlərindən də biri veb səhifədə tez-tez istifadə olunan vəya təkrarlanan taqları komponentə ayırmağıdır. Və səhifədə bir komponentdə dəyişiklik olduğu zamanı digər komponentlərin **yenidən render olmaması** üçün memo, useCallBack və useMemo istifadə edilir.
Gəlin sadə bir misal üzərindən başlayaq. 
2 dənə komponentimiz olsun
* Nav - sadə formada rafce yazın, geriyə nav taqı qaytarsın.
* Footer - sadə formada rafce yazın, geriyə footer taqı qaytarsın.

```jsx
// Nav.jsx faylı
import React from  'react'

console.log("Nav Render edildi");
const  Nav  =  ()  =>  {
	return (
		<nav>Nav</nav>
	)
}

export  default Nav
```
```jsx
// Footer.jsx faylı
import React from  'react'
  
console.log("Footer Render edildi");
const Footer = () => {
	return (
		<footer>Footer</footer>
	)
}

export default Footer
```
Və App.jsx faylında bu komponentləri import edək.
```jsx
import React from  'react'
import Footer from  './Components/Footer';
import Nav from  './Components/Nav';
  
const  App  =  ()  =>  {
	console.log("App Render edildi");
	return (
		<>
			<h1>useMemo useCallback</h1>
			<Nav/>
			
			<Footer/>
		</>
	);
}

export  default App
```

Veb səhifəni start etdikdən sonra inspect-dən console-a baxsaq. Hər üç komponentin render olduğunu görərik. Bu normaldır. Ekrana ilk dəfə çıxanda render olmuş sayılır. Ümumiyyətlə komponent ilk dəfə ekrana çıxırsa vəya həmin komponentdə dəyişiklik olursa **render** olmalıdır.

O zaman gəlin sadə bir misala baxaq. Nav ilə Footer arasında section yazıb **Todo Task** quraq.

```jsx
import React from  'react'
import Footer from  './Components/Footer';
import Nav from  './Components/Nav';
  
const  App  =  ()  =>  {
	console.log("App Render edildi");
	const  [todos,  setTodos]  =  useState([]);
	const  [todoItem,  setTodoItem]  =  useState("");
	
	const  inputHandle  =  (e)  =>  {
		setTodoItem(e.target.value);
	}	

	const  addTodoHandle  =  (e)  =>  {
		e.preventDefault()
		let newTodo =  {
			name: todoItem,
		};
		setTodos([...todos, newTodo]);
		setTodoItem("");
	};

	return (
		<>
			<h1>useMemo useCallback</h1>
			<Nav/>
			<section>
				<h1>---------------------</h1>
				
				<form>
					<input
					value={todoItem}
					onChange={inputHandle}
					type="text"
					placeholder="Write Todo"
					/>
				
					<button  onClick={addTodoHandle}>Add</button>
				</form>
				
				<ul>
					{
						todos?.map((todo)  =>  {
							return  <li>{todo.name}</li>;
						})
					}
				</ul>
				
				<h1>---------------------</h1>
			</section>
			<Footer/>
		</>
	);
}

export  default App
```

Todo Task hazırdır. İndi isə gəlin inspect-dən console-a baxaraq input taqına nəsə yazaq. Fikir verdinizsə siz input-da birşeylər yazdıqca App, Nav və Footer  komponentləri render oldu. App-in render olmağı normaldır. Çünki içərisində hansısa dəyərlər dəyişir, lakin ( Nav və Footer ) -da **heç bir şey dəyişməməsinə baxmayaraq boş-boşuna render olur.**
Bunun qarşısını almaq üçün **memo** - dan istifadə edirik.

İçərisində heçbir dəyər dəyişməməyinə baxmayaraq render olan komponentlərimizi memo metoduna salaq. 

```jsx
// Nav.jsx faylı
import React, {memo} from  'react'

console.log("Nav Render edildi");
const  Nav  =  ()  =>  {
	return (
		<nav>Nav</nav>
	)
}

export  default memo(Nav)
```
```jsx
// Footer.jsx faylı
import React, {memo} from  'react'
  
console.log("Footer Render edildi");
const Footer = () => {
	return (
		<footer>Footer</footer>
	)
}

export default memo(Footer)
```

Artıq yenə input-da nəsə yazsanız ( Nav və Footer ) daxilində birşeylər dəyişmədikcə render olmayacaq. Bu da bizi **sürət olaraq qabağa salır.**

İndi isə App.jsx faylında qurduğumuz
*  **form** taqını **AddTodo.jsx** 
* **li** taqını **TodoItem.jsx** komponentinə çevirək
* **ul** taqını isə **Todos.jsx** komponentinə çevirək


```jsx
// AddTodo.jsx
import React from  'react'

console.log("AddTodo Render edildi");
const  AddTodo  =  ({addTodoHandle,  inputHande,  todoItem  })  =>  { 
	return (
		<form>
			<input
				value={todoItem}
				onChange={inputHande}
				type="text"
				placeholder="Write Todo"
			/>
			  
			<button  onClick={addTodoHandle}>Add</button>
		</form>
	);
};
export  default AddTodo
```
```jsx 
// TodoItem.jsx
import React from  'react'
  
const  TodoItem  =  ({todo})  =>  {
	console.log("TodoItem Render oldu");
  
	return  <li>{todo.name}</li>;
}
  
export  default TodoItem
```
```jsx
// Todos.jsx
import React from  'react'
import TodoItem from  './TodoItem';

console.log("Todos Render edildi");
const  Todos  =  ({todos})  =>  {
	return (
		<ul>
			{todos?.map((todo)  =>  {
				return  <TodoItem  todo={todo}/>
			})}
		</ul>
	);
}

export  default Todos
```


form və ul taqlarını komponentlərinə ayırdıq və lazım olan parametrləri qəbul etdik.
App.jsx faylında Komponentləri çağıraq və lazım olan parametrləri göndərək.

```jsx
// App.jsx
import React from  'react'
import Footer from  './Components/Footer';
import Nav from  './Components/Nav';

import AddTodo from  "./Components/AddTodo";
import Todos from  "./Components/Todos";  

const  App  =  ()  =>  {
	console.log("App Render edildi");
	const  [todos,  setTodos]  =  useState([]);
	const  [todoItem,  setTodoItem]  =  useState("");
	
	const  inputHandle  =  useCallback(e  =>  {
		setTodoItem(e.target.value);
	},[])	

	const  addTodoHandle  =  (e)  =>  {
		e.preventDefault()
		let newTodo =  {
			name: todoItem,
		};
		setTodos([...todos, newTodo]);
		setTodoItem("");
	};

	return (
		<>
			<h1>useMemo useCallback</h1>
			<Nav/>
			<section>
				<h1>---------------------</h1>
		
				<AddTodo
					addTodoHandle={addTodoHandle}
					inputHande={inputHande}
					todoItem={todoItem}
				/>
				 
				<Todos  todos={todos}/>
				
				<h1>---------------------</h1>
			</section>
			<Footer/>
		</>
	);
}

export  default App
```

Əla artıq hər biri komponent kimi dinamik formada işləyir.
Lakin input-da nəsə yazdıqda Todos komponentində heçnə dəyişməsə belə yenə render olur. Bunun da qarşısını almaq üçün Todos komponentini memo metodu ilə export edəcik.
```jsx
// Todos.jsx
import React,{memo} from  'react'
import TodoItem from  './TodoItem';

console.log("Todos Render edildi");
const  Todos  =  ({todos})  =>  {
	return (
		<ul>
			{todos?.map((todo)  =>  {
				return <TodoItem todo={todo}/>
			})}
		</ul>
	);
}

export  default memo(Todos)
```

Əla. Artıq input-da birşeylər yazanda Todos render olmayacaq. 
Kodumuzda hələki dəyişiklik AddTodo komponentində olur. Bəs başqa yerdə dəyişiklik olsa AddTodo boş-boşuna render olar?
Footer-dən aşağıda sadə bir **counter** quraq.

```jsx
import React, { useState } from  'react'
import Footer from  './Components/Footer';
import Nav from  './Components/Nav';

import AddTodo from  "./Components/AddTodo";
import Todos from  "./Components/Todos";  

const  App  =  ()  =>  {
	console.log("App Render edildi");
	const  [todos,  setTodos]  =  useState([]);
	const  [todoItem,  setTodoItem]  =  useState("");
	
	const  [counter,setCounter]  =  useState(0)	

	const  inputHandle  =  useCallback(e  =>  {
		setTodoItem(e.target.value);
	},[])

	const  addTodoHandle  =  (e)  =>  {
		e.preventDefault()
		let newTodo =  {
			name: todoItem,
		};
		setTodos([...todos, newTodo]);
		setTodoItem("");
	};

	return (
		<>
			<h1>useMemo useCallback</h1>
			<Nav/>
			<section>
				<h1>---------------------</h1>
		
				<AddTodo
					addTodoHandle={addTodoHandle}
					inputHande={inputHande}
					todoItem={todoItem}
				/>
				 
				<Todos  todos={todos}/>
				
				<h1>---------------------</h1>
			</section>
			<Footer/>
			
			<h1>{counter}</h1>
			<button  onClick={()=>setCounter(counter+1)}>Add</button>
			
		</>
	);
}

export  default App
```

Counter-də button-a click etdikdə eded 1 vahid artır, Lakin console-a diqqətlə baxsanız. Button-a click edəndə yalnız counterin artmağına baxmayaraq AddTodo komponentim render oldu. O zaman gəlin memo ilə qarşısını alaq.

```jsx
// AddTodo.jsx
import React, {memo} from  'react'

const  AddTodo  =  ({addTodoHandle,  inputHande,  todoItem  })  =>  { 
	console.log("AddTodo Render edildi");
	
	return (
		<form>
			<input
				value={todoItem}
				inputHande={inputHande}
				type="text"
				placeholder="Write Todo"
			/>
			  
			<button  onClick={addTodoHandle}>Add</button>
		</form>
	);
};

export  default memo(AddTodo)
```

AddTodo komponentimi memo metoduna salaraq lazımsız render olmasını əngəllədik.
Lakin counter-də button-a click etdikdə yenə AddTodo komponenti ehtiyyac olmadan render oldu. Bəs memo niyə qarşısını almadı?
## useCallBack
Komponentlərin ehtiyyac olmadıqca render olmamağı üçün komponenti memo metodunun daxilində export edirlər. Lakin bayaq AddTodo komponentində işə yaramadı. Bunun səbəbi komponentin Non-Privimite data type göndərməyidir. Əgər biz komponentdə prop olaraq metod göndəririksə, bu halda biz prop olaraq göndərilən metodları useCallback daxilində yazmalıyıq.
```jsx
// Funksiyaları useCallback metodunun içərisində yazıldı
const  inputHandle  =  useCallback(e  =>  {
	setTodoItem(e.target.value);
},[])
  
const  addTodoHandle  =  useCallback(e  =>  {
	e.preventDefault()
	let newTodo =  {
	name: todoItem,
	};
	setTodos([...todos, newTodo]);
	setTodoItem("");
},[])
```

```jsx
import React, { useState, useCallback } from  'react'
import Footer from  './Components/Footer';
import Nav from  './Components/Nav';

import AddTodo from  "./Components/AddTodo";
import Todos from  "./Components/Todos";  

const  App  =  ()  =>  {
	console.log("App Render edildi");
	const  [todos,  setTodos]  =  useState([]);
	const  [todoItem,  setTodoItem]  =  useState("");
	
	const  [counter,setCounter]  =  useState(0)	

	const  inputHandle  =  useCallback(e  =>  {
		setTodoItem(e.target.value);
	},[])
	  
	const  addTodoHandle  =  useCallback(e  =>  {
		e.preventDefault()
		let newTodo =  {
		name: todoItem,
		};
		setTodos([...todos, newTodo]);
		setTodoItem("");
	},[])

	return (
		<>
			<h1>useMemo useCallback</h1>
			<Nav/>
			<section>
				<h1>---------------------</h1>
		
				<AddTodo
					addTodoHandle={addTodoHandle}
					inputHande={inputHande}
					todoItem={todoItem}
				/>
				 
				<Todos  todos={todos}/>
				
				<h1>---------------------</h1>
			</section>
			<Footer/>
			
			<h1>{counter}</h1>
			<button  onClick={()=>setCounter(counter+1)}>Add</button>
			
		</>
	);
}

export  default App
```
Artıq counter-də button-a click etdikdə AddTodo komponentim render olmur.
Lakin input taqında todo yazıb əlavə etsəniz boş string əlavə edir. Bunun səbəbi addTodoHandle funksiyası todoİtem dəyişdikcə hesaba alınmalıdır.
```jsx
// addTodoHandle funksiyasında [todoItem] yazırıq
const  addTodoHandle  =  useCallback(e  =>  {
	e.preventDefault()
	let newTodo =  {
	name: todoItem,
	};
	setTodos([...todos, newTodo]);
	setTodoItem("");
},[todoItem])
```

Artıq input-da nəsə yazanda todos array-inə əlavə olunur. İndi isə gəlin TodoItem-ların render məsələsinə baxaq. Hətta hansı todoItem-ın render olmasını bilmək üçün todo-nu da console-a çıxaraq.

```jsx 
// TodoItem.jsx
import React from  'react'
  
const  TodoItem  =  ({todo})  =>  {
	console.log(`${todo.name} Render oldu`);	
  
	return  <li>{todo.name}</li>;
}
  
export  default TodoItem
```

console-a baxaraq input-a todo1 və todo2 yazaq. todo1-i əlavə edərkən todo1 render olur, bu normal haldır. Lakin todo2 əlavə edərkən todo1  yenə render oldu. Axı todo1-də heçnə dəyişmədi. 
Bunun üçün sadə şəkildə TodoItem komponentini memo içərisində yazaq.
```jsx 
// TodoItem.jsx
import React, {memo} from  'react'
  
const  TodoItem  =  ({todo})  =>  {
	console.log(`${todo.name} Render oldu`);	
  
	return  <li>{todo.name}</li>;
}
  
export  default memo(TodoItem)
```
Artıq console-da gördüyünüz kimi yalnız əlavə olunan todo render olur. 
Bunun üçün input taqı qurub, taqda olan dəyəri [search] adında useState-də saxlayaq.


## useMemo
useMemo-nun işləmə prinsipini öyrənmək üçün sadə bir filter sistemi quraq.
```jsx
import React, { useState, useCallback } from  'react'
import Footer from  './Components/Footer';
import Nav from  './Components/Nav';

import AddTodo from  "./Components/AddTodo";
import Todos from  "./Components/Todos";  

const  App  =  ()  =>  {
	console.log("App Render edildi");
	const  [todos,  setTodos]  =  useState([]);
	const  [todoItem,  setTodoItem]  =  useState("");
	
	const  [counter,setCounter]  =  useState(0)	
	
	const  [search,setSearch]  =  useState('')

	const  filteredTodos  =  ()  =>  {
		todos.filter((item)  =>  {
		return item.includes(search.toLowerCase());
	});

}

	const  inputHandle  =  useCallback(e  =>  {
		setTodoItem(e.target.value);
	},[])
	  
	const  addTodoHandle  =  useCallback(e  =>  {
		e.preventDefault()
		let newTodo =  {
		name: todoItem,
		};
		setTodos([...todos, newTodo]);
		setTodoItem("");
	},[])

	return (
		<>
			<h1>useMemo useCallback</h1>
			<Nav/>
			<section>
				<h1>---------------------</h1>
				<input  value={search}  onChange={(e)=>setSearch(e.target.value)}  type="text"  placeholder="Search"  />
				
				<AddTodo
					addTodoHandle={addTodoHandle}
					inputHande={inputHande}
					todoItem={todoItem}
				/>
				 
				<Todos  todos={todos}/>
				
				<h1>---------------------</h1>
			</section>
			<Footer/>
			
			<h1>{counter}</h1>
			<button  onClick={()=>setCounter(counter+1)}>Add</button>
			
		</>
	);
}

export  default App
```


Hazırladı - **Zahid Vahabzadə**
Video dərslər üçün Youtube kanalım - **[Biraz Kod Yazaq](https://www.youtube.com/channel/UCRlKqhooswsmfkxnokxcB0g
)**










