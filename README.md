# Websockets

List of websockets avalailable on **Inobi** platform server

## Driver
*Path: /ws/taxi/driver/*
Socket for driver to stay in contact with server. Messages will be sent to driver when: 

	- here is a trip for a driver to accept
	- ...

#### Example
```javascript
const scheme = 'ws://'
const host = 'dev.inobi.kg:12000'
const path = '/ws/taxi/drivers/'
const token = '1572d957-19e3-4a07-8519-3b04ca5c0b56'
const socket = new WebSocket(`${scheme}${host}${path}?token=${token}`)
socket.onclose = socket.onerror= console.log
socket.onmessage = function(e) {
	const data = JSON.parse(e.data)
	console.log(data)
	if (data.type == 'TRIP') {
		const { payload: trip } = data;
		alert('trip to accept', trip.name);
		console.log(trip)
	}
}
```

## Trip
*Path: /ws/taxi/trips/{trip_id}/*
Socket for getting trip messages. Messages will be sent to user/driver/manager on every trip related event. Some of them are followings:

	- trip accepted
	- driver arrived
	- driver started
	- driver sent his coordinate
	- user notified driver he's coming
	- driver paused/resumed trip
	- trip finished
	- etc

#### Example
```javascript
const scheme = 'ws://'
const host = 'dev.inobi.kg:12000'
const tripId = 1
const path = `/ws/taxi/trips/${tripId}/`
const token = '1572d957-19e3-4a07-8519-3b04ca5c0b56'
const socket = new WebSocket(`${scheme}${host}${path}?token=${token}`)
socket.onclose = socket.onerror= console.log
socket.onmessage = function(e) {
	const data = JSON.parse(e.data)
	console.log(data)
	if (data.type == 'ARRIVE') {
		const { payload: tripState } = data;
		alert('driver arrived');
		console.log(tripState)
	}
}
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbNjY4MDY2Mzk5XX0=
-->