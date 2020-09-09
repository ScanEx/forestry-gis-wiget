# API
* Объект: Map
  * Инициализация:
	```js
	var map = new Map(mapContainer, {hostName: 'lv.scanex.ru:8080', serviceEndPoint: 'http://lv.scanex.ru:9999', center: [51.331898, 111.28051], zoom: 9});
	```
  	* mapContainer - DOM-элемент, содержащий карту
	* hostName - имя хоста сервера карты
	* serviceEndPoint - корневой адрес серверного API
  	* center - координаты начального центра карты (широта, долгота в градусах)
  	* zoom - начальный масштаб
  * Методы:
    * асинхронная загрузка карты
		```js
		async load ();
		```
	* включить состояние по умолчанию
		```js
		showMain();
		```
	* показать сводную аналитику	
		```js
		showAnalytics();
		```
	* показать данные пользователя
		```js
		showUploaded();
		```
	* показать список заявок
		```js
		async showRequests();
		```
  * События:
  	* создать заявку - ``request:create``
  	* рубка - связанные документы - ``cut:docs``
  	* рубка - снимок с БПЛА - ``cut:image``
  	* гарь - связанные документы - ``fire:docs``
  	* гарь - снимок с БПЛА - ``fire:image``
  	* патология - связанные документы - ``disease:docs``
  	* патология - снимок с БПЛА - ``disease:image``
# Пример
```js
	import './forestry.css';
	import Map from './forestry.js';

	window.addEventListener('load', async () => {
		try {
			// получение контейнера карты
			let mapContainer = document.getElementById('map');
			
			// инициализация
			let map = new Map(mapContainer, {hostName: 'lv.scanex.ru:8080'});
			
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