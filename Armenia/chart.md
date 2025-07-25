
```dataviewjs // PS. remove backslash \ at the very beginning!

dv.span("** 🇦🇲 Armenian Learning Heatmap **")
 /* optional ⏹️💤⚡⚠🧩↑↓⏳📔💾📁📝🔄📝🔀⌨️🕸️📅🔍✨ */
const calendarData = {
	year: 2025,  // (optional) defaults to current year
	colors: {    // (optional) defaults to green
		blue:        ["#8cb9ff", "#69a3ff", "#428bff", "#1872ff", "#0058e2"], // first entry is considered default if supplied
		green:       ["#c6e48b", "#7bc96f", "#49af5d", "#2e8840", "#196127"],
		red:         ["#ff9e82", "#ff7b55", "#ff4d1a", "#e73400", "#bd2a00"],
		orange:      ["#ffa244", "#fd7f00", "#dd6f00", "#bf6000", "#9b4e00"],
		pink:        ["#ff96cb", "#ff70b8", "#ff3a9d", "#ee0077", "#c30062"],
		orangeToRed: ["#ffdf04", "#ffbe04", "#ff9a03", "#ff6d02", "#ff2c01"]
	},
	showCurrentDayBorder: true, // (optional) defaults to true
	defaultEntryIntensity: 4,   // (optional) defaults to 4
	intensityScaleStart: 10,    // (optional) defaults to lowest value passed to entries.intensity
	intensityScaleEnd: 100,     // (optional) defaults to highest value passed to entries.intensity
	entries: [],                // (required) populated in the DataviewJS loop below
}

//DataviewJS loop
for (let page of dv.pages('"Armenia/daily notes"').where(p => p.armenian)) {
	//dv.span("<br>" + page.file.name) // uncomment for troubleshooting
	calendarData.entries.push({
		date: page.file.name,     // (required) Format YYYY-MM-DD
		intensity: page.armenian, // (required) the data you want to track, will map color intensities 
		content: "🏋️",           // (optional) Add text to the date cell
		color: "blue",          // (optional) Reference from *calendarData.colors*. If no color is supplied; colors[0] is used
	})
}

renderHeatmapCalendar(this.container, calendarData)

```



```dataviewjs

dv.span("** 🇦🇲 Armenian Learning Heatmap **")

const calendarData = {
	year: 2025,
	colors: {
		blue: ["#8cb9ff", "#69a3ff", "#428bff", "#1872ff", "#0058e2"],
	},
	showCurrentDayBorder: true,
	defaultEntryIntensity: 1,
	intensityScaleStart: 1,
	intensityScaleEnd: 5,
	entries: [],
}

// تابع تبدیل ساعت به شدت رنگ
function mapHoursToIntensity(hours) {
	if (hours <= 2) return 1;
	else if (hours <= 4) return 2;
	else if (hours <= 6) return 3;
	else if (hours <= 8) return 4;
	else return 5;
}

// جمع‌آوری اطلاعات از صفحات روزانه
for (let page of dv.pages('"Armenia/daily notes"').where(p => p.armenian)) {
	let hours = parseFloat(page.armenian); // فرض بر اینکه مقدار عددی یا رشته‌ی عددی هست
	if (isNaN(hours)) continue;

	calendarData.entries.push({
		date: page.file.name,
		intensity: mapHoursToIntensity(hours),
		content: "📚",  // می‌تونی هر ایموجی دیگه‌ای بذاری
		color: "blue",
	})
}

renderHeatmapCalendar(this.container, calendarData)

```