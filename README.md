# jQuery Countdown Timer plugin

Creates a countdown timer on the selected elements which counts down by seconds until 0. Timers can be started automatically or manually and can also be paused and resumed. Display of the countdown can be controlled by using an optional template of the users' choice.  A user specified function can also be performed when the countdown finishes.

## Usage

Countdown timers are instantiated by passing in options to the plugin.

Instantiate and start a timer that counts down from 108 minutes:

```js
$("#selector").countdown({autostart: true, m: 108});
```

## Options

Options are normally passed into the init method.

### autostart 
Automatically start the countdown when instantiated on a selector. default: false

### done
An optional function to run when the countdown reaches 0.

### y

Integer to use for years. default: 0

### d

Integer to use for days. default: 0
### h

Integer to use for hours. default: 0
### m

Integer to use for minutes. default: 0

### s

Integer to use for seconds. default: 0

### tpl(el,opts)

An optional function to handle updating display of the counter instead of the minimal presentation baked into the plugin. Parameters `el` and `opts` are passed into the function and reference the element and the options assigned to it.

## Methods

### init
Instantiates a countdown on each element in the selector. Uses default values for any options not passed in.

### pause
Pauses any active countdowns on the selected elements.  Essentially an alias for the stop method.

```js
$("#selector").countdown('pause');
```
### resume
Resumes a paused/stopped countdown from where it left off. Essentially an alias for the start method.

```js
$("#selector").countdown('resume');
```
### start
Starts a countdown on each selected element.

```js
$("#selector").countdown('start');
```
### stop
Stops any countdowns on the selected elements.

```js
$("#selector").countdown('stop');
```

## Examples

Create a countdown timer on #my-countdown that automatically starts counting down 1 minute and 30 seconds using an undesrcore template.  Display a message when the countdown has finished.

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8">
	<title>countdown</title>
</head>
<body>
	<div id="my-countdown">
		<!-- display the countdown timer here -->
	</div>
	
	<!-- include jQuery -->
	<script src="//ajax.googleapis.com/ajax/libs/jquery/1.9.1/jquery.min.js"></script>

	<!-- include underscore.js for template -->
	<script src="//cdnjs.cloudflare.com/ajax/libs/underscore.js/1.4.4/underscore-min.js"></script>
	
	<!-- include the countdown plugin -->
	<script src="/js/jquery.countdown.js"></script>

	<!-- create the template to use for this example -->
	<script type="text/template" id="countdown-tpl">
		<table>
			<tr>
				<th>years</th>
				<th>days</th>
				<th>hours</th>
				<th>minutes</th>
				<th>seconds</th>
			</tr>
			<tr>
				<td><%= y %></td>
				<td><%= d %></td>
				<td><%= h %></td>
				<td><%= m %></td>
				<td><%= s %></td>
			</tr>
		</table>
	</script>

</body>
</html>
```

```js
// define what options to use
var options = {
	autostart: true,
	m: 1,
	S: 30,
	// show a message after the countdown timer once the countdown has ended
	done: function() {
		$('#my-countdown').after("<p>Time's up!</p>");
	},
	// el and opts will refer to the element the countdown is running on and opts are the options assigned to it
	tpl: function(el,opts) {
		// use underscore to generate the markup to be displayed from the countdown-tpl template
		var template = _.template(
			$('#countdown-tpl').html()
		);
		// display the template
		$(el).html(template(opts));
	}
}
// instantiate the countdown
$("#my-countdown").countdown(options);
```


## MIT License

Copyright (C) 2013 Lucas Myers

Permission is hereby granted, free of charge, to any person obtaining a copy of
this software and associated documentation files (the "Software"), to deal in
the Software without restriction, including without limitation the rights to
use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of
 the Software, and to permit persons to whom the Software is furnished to do so,
subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS
FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR
COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER
IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.