# calculator

## To run:
- clone this repo
- run:
```
npm install
```
- Then run:
```
npm run serve
```
- Go to the localhost port shown in your terminal

## Notes:
- This calculator demo app is built with Vue, stylus & pug
- Used Vue [component naming conventions](https://v2.vuejs.org/v2/style-guide/?redirect=true#Single-instance-component-names-strongly-recommended), pug class naming conventions
- Styling stolen from the Mac OS calculator :/
- I started off using JS eval() function and changed to Function based on [this documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/eval#never_use_eval!)
- Added a clear functionality that wasn't in the wireframe for a better user experience (otherwise users would have to clear the calc by refreshing the page)

## With more time:
I gave myself 90 mins to deliver an MVP of the calculator from the wireframe supplied. With more time I would:
- Add a testing framework and a unit test for the TheCalculator component
- Fix edge-case bugs, e.g. if a user enters '6//' and then presses equals the output is not correct
- Nicer styling & a better place for the Clear button. Perhaps by adding another row to the calc and stretching out key buttons
