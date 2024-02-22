<script lang="ts">
	// Импортируем на типы и функционал Svelte
	import { onMount } from 'svelte';
  
	// Пример типа данных, которые ожидаются от API
	interface ApiResponse {
	  message: string;
	}
  
	// Переменная для хранения полученных данных
	let data: ApiResponse[] | null = null;
  
	// Переменная для хранения возможной ошибки
	let error: string | null = null;
  
	// Функция для выполнения запроса к API
	async function fetchData() {
	  try {
		const response = await fetch('https://mlstudy.pythonanywhere.com/hello/?name=Fedos');
		if (!response.ok) {
		  throw new Error('Ошибка запроса: ' + response.statusText);
		}
		const jsonData: ApiResponse[] = await response.json();
		data = jsonData;
		console.log(data.message);
	  } catch (err) {
		error = err.message;
	  }
	}
  
	// Выполняем запрос при монтировании компонента
	onMount(() => {
	  fetchData();
	});
  </script>

<div class="container h-full mx-auto flex justify-center items-center">
	<div class="space-y-5">
		<h1 class="h1">Let's get cracking bones!</h1>
		<p>Start by exploring:</p>
		<ul>
			<li><code class="code">/src/routes/+layout.svelte</code> - barebones layout</li>
			<li><code class="code">/src/app.postcss</code> - app wide css</li>
			<li>
				<code class="code">/src/routes/+page.svelte</code> - this page, you can replace the contents
			</li>
		</ul>
	</div>
	<h1>{data?.message}</h1>
</div>
