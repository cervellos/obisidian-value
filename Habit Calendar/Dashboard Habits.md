

```dataviewjs
let pages = dv.pages(`"Habit Calendar/notas diarias"`)
const year = 2024
const month = 2
const date_pattern = 'YYYY-MM-DD'
const habit_tag = '#habit'
const habits = {
	'ingles': '📜 x {habit} min', 
	'Microsft': '🦾 x {habit} min',
	'coding': '💻 x {habit} min',
	'workout': '🏃',
	'Math': '✨',
}

let data = {}
for (let page of pages) {
	let date = page.file.name
	data[date] = data[date] || ''
	for (let task of page.file.tasks.filter(task => task.tags.contains(habit_tag) && task.checked)) {
		for (let habit in habits) {
			if (task[habit]) {
				data[date] += habits[habit].replace('{habit}', task[habit]) + '\n'
			}
		}
	} 
}

let calendarData = []
for (let date in data) {
	calendarData.push({date: date, content: data[date]})
}
renderHabitCalendar(this.container, dv, {year, month, data: calendarData, date_pattern}) 
```




