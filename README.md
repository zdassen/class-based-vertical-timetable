# class-based-vertical-timetable
Class based D3 timetable (vertical layout)

# Example
```JavaScript
/* create random number within the range min ~ max */
function randn(min, max) {
  let span = (max - min) + 1;
  return Math.floor(Math.random() * span) + min;
}

/* create timestamps with random offset */
let start = new Date("2018-06-19 12:55:55");
let data = [start];
let i = 0
const N = 195;
while (i < N) {
  
  // add timestamp after random minutes
  let elapsedMillisec = randn(1, 90) * 60 * 1000;
  let millisecAfter = new Date(start.getTime() + elapsedMillisec);
  data.push(millisecAfter);

  start = millisecAfter;
  i++;
}

/* log titles */
let titles = ["sleep", "eat", "write code"];

/* "partition by" every 2 timestamps (e.g. "start" & "finish") */
let pairs = [];
i = 0;
while (i < N) {
  pairs.push([
    data[i],    // start
    data[i + 1],    // finish
    titles[randn(0, titles.length - 1)],    // log title
  ]);
  i += 2;
}

class MyVerticalTimetable extends VerticalTimetable {

  /* override setter of bar color */
  setBarColor(d, i) {
    let title = d[2];
    if (title === "sleep") return "steelblue";
    else if (title === "eat") return "crimson";
    else if (title === "write code") return "springgreen";
    else return "lightgray";
  }

}

let svgId = "graphArea";
let vtt = new MyVerticalTimetable(svgId, pairs, 7);
```
![vtimetable-sample-1](https://user-images.githubusercontent.com/24271672/41829640-e30f1114-7876-11e8-9398-7dcfc28c8444.JPG)
