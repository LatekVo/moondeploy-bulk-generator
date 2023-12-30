# moondeploy-bulk-generator
A short snippet of code which can be used to generate multiple BNB wallets on [moondeploy](https://moondeploy.com)

Note: I've had the best results with 1 thread set to be used.

```javascript
const dom_generate = document.getElementsByClassName('button-large hide-prerender')[0];
const dataList = [];
const delay = ms => new Promise(res => setTimeout(res, ms));
let outputs = document.getElementsByClassName('output');
let dom_public = outputs[5];
let dom_private = outputs[6];
dom_generate.addEventListener('click', () => {
	setTimeout(() => {
		outputs = document.getElementsByClassName('output');
		dom_public = outputs[5];
		dom_private = outputs[6];
		try {
			dom_private.click();
		} catch (e) {
			//console.log(e);
		}
	}, 100);
});
dom_generate.click();
const loop = async (time) => {
	dom_generate.click();
	await delay(time);
	try {
		dataList.push(dom_public.innerHTML + ' ' + dom_private.innerHTML);
	} catch (e) {
		//console.log(e);
	}
}
const display = () => {
	let outputString = '';
	dataList.map(n => outputString += n + '\n'); 
	console.log(outputString);
}
const generate = async (amt, time = 200) => {
	for (let i = 0; i < amt; i++) {
		await loop(time);
	}
	display();
}
```
