# API
* Объект: Map
  * Инициализация:
	```js
	var map = new Map(mapContainer, {permissions, gmxPath: '/gis', apiPath: '/service', center: [51.331898, 111.28051], zoom: 9});
	```
  	* mapContainer - DOM-элемент, содержащий карту	
  	* permissions - массив строк, содержащий разрешения для элементов интерфейса
  	* gmxPath - путь к Геомиксеру (значение по умолчанию '/gis')
  	* apiPath - путь к API (значение по умолчанию '/service')
  	* center - координаты начального центра карты (широта, долгота в градусах) (значение по умолчанию [51.331898, 111.28051])
  	* zoom - начальный масштаб (значение по умолчанию 9)
  * Методы:
    * асинхронная загрузка карты
		```js
		async load ();
		```
	* выгрузка карты
		```js
		unload ();
		```
	* включить состояние по умолчанию
		```js
		async showMain();
		```
	* показать сводную аналитику	
		```js
		async showAnalytics();
		```
	* показать данные пользователя
		```js
		async showUploaded();
		```
	* показать список заявок
		```js
		async showRequests();
		```
  * События:
  	* создать заявку - ``request:create``
  	* инцидент - связанные документы - ``incident:docs``
  	* инцидент - снимок с БПЛА - ``incident:image``  	
# Пример
```js
	import './forestry.css';
	import Map from './forestry.js';

	window.addEventListener('load', async () => {
		try {
			// получение контейнера карты
			let mapContainer = document.getElementById('map');
			
			// инициализация
			let map = new Map(mapContainer);
			
			// привязка обработчика события
			map.addEventListener('request:create', e => {
				console.log(e);
			});
			
			// загрузка карты
			await map.load();
		}
		catch(e) {
			alert(e.toString());
		}
	});
```