[YGLF](http://yougottalovefrontend.com/) conference was a well-organized two-day event, but me and David attended only the second day and here we present what came out of it. 
The first thing you notice is that the conf was organized by Wix and sponsored by Wix, with lecturers from Wix and prizes from Wix and winners from Wix (finally, got it out of my system!) After a while you relax and concentrate on presentations

[TOC]
********
### The missing slice by [Lea Verou](http://lea.verou.me/)
It was probably the best talk of the conference. It was a beautifully structured thought process on how a front-ender would tackle the issue of presenting pie charts via CSS. Her presentation was special not only in content - *actual code was written live during the talk*, but also she used something called [CSSS](http://lea.verou.me/csss/sample-slideshow.html#intro) instead of a usual boring powerpoint.
#####Key points
*  Use *pure CSS* and the code would be roughly (while the slides are still missing)
`.pie {
	    transform:  scaleX(-1); //for flipping
		rotate(-90deg);
		skew(50deg); 
		transform-origin: bottom-left;
		padding: 50%;
}` , etc....
However, this solution is hardly flexible (try adding colors or several categories), not extensible and not maintainable
* Why not *gradient and pseudo elements*?
`.pie {
	border-radius: 50%;
	background: #f06; //fucsia
	linear-gradient (to right, transparent 50%, gold 0);
	color: gold; //or define var. currentColor: gold;
	}`
`.pie::before {
	content: '';
	margin-left: 50%;
	height: 100%;
	background: green; //or better background-color: **inherit**
	border-radius: 0 100% 100% 0;
	transform: rotate (15deg); //change this for diff shapes or use 0.1turn ~ 15deg
}`
You can also do animation with @keyframes for color and spin
add in **.pie::before**
`animation: 1s spin infinite linear;
animation: 1s color infinite step-end; //not linear! `
At this point she also showed some crazy stuff with animation using *state pause* and *forwards*
This solution is much better, but still not there yet!
* Next stop is *SVG*!!!
First, you define your SVG:
`<svg>
	viewBox="0 0 64 64"
	circle r=25% cx=50% cy=50% stroke
</svg>`
The CSS looks slightly less messy:
`.pie {
}`
`.pie circle {
stroke: gold;
stroke-width: 32;
stroke-dash-array: 0 100 100; //this is the thing!!! 64 in SVG and this 100 are connected! (2*32^2*pi)
fill: none;
animation: 2s;
}`
if we need more pie chart sections - we just add more circles with diff colors and dash-array numbers
This solution is dashing and has all the major advantages - extensibility, flexibility and easy maintenance.
* There's another possibility - use conic gradients. Three lines of code, easy maintenance and really cool.
However, you can't - it is properly defined by the W3C, but not supported by all the major browsers.
#####Takeaway
Having made the journey one understands that attaining the perfect solution takes a lengthy thought process and we were lucky to witness how one of the brightest minds in business does it. But even that is not enough - Lea signed off with a call to action - she believes that we - as developers - are able to influence the web and should steer it toward solutions that we want - like conic gradients. 
******

###io.js and the future of server side JavaScript by Benjamin Gruenbaum
This lecture was a call to devs to participate in the open source movement and how even small contributions matter:

 - Opening pull requests
 - Writing documentation
 - Reporting bugs
 - Feature requests
 - Answering questions on SO
 
#####Takeaway
 - For those who care - **io.js** and **Node.js** are merging back!
 - Have a look at **Bluebird.js** a promise library
 - You can 'catch-all' unhandled promise rejection by a single line of code in **q.js** and **node.js**

    `process.on('unhandledRejection', function(reason, p){
    console.log("Possibly Unhandled Rejection at: Promise ", p, " reason: ", reason);
    // application specific logging here
    });`

*****
###Nothing else matters: Easy backend for frontend developers by Matthieu Mayran
That's an actual ad break for Google Cloud Fire base - WebSocket-based technology.
#####Takeaway
If you need something real-time, but lightweight and don't have the time to set up Kafka et al, then contact the <strike>sales</strike> author - *mayran@google.com*
****
###[React Native: Under the Hood by Alexander Kotliarskyi](https://speakerdeck.com/frantic/react-native-under-the-hood/)
The presenter is a skinny fair haired guy from Facebook who has given a good lecture on deeper plumbing of [React.js Native](https://facebook.github.io/react-native/). React is sexy, but why should we even bother? Native apps have a number of issues

 - Native apps are hard to build (don't get me started on objective c); 
 - Code sharing across other platforms with diff technologies - a big NO here
 - Slow iteration
 - Scalability is hard
 It is obvious that we have almost all these things for granted in web technologies. 
 The selling point in React Native is the principle
 $$
 UI = f^*(data)
 $$
 where * no side effects
React.js works on Virtual DOM and not directly on HTML
The underlying structure is in the diagram:
![enter image description here](https://lh3.googleusercontent.com/-76CCka1pZA0/VXvqO56LWEI/AAAAAAAAADY/hx-0i_7adLo/s0/react+native+snippet.JPG "react native snippet.JPG")
****
###[Coding Your Company Culture by Alex Wolkov](http://www.slideshare.net/altryne/coding-your-company-culture)
A Senior Web Dude from Fundbox has given some cool tips on how to make your place of work better by investing some time in side projects:
 - Use a funny [hubot](https://hubot.github.com/) in a company chat (Slack, etc), which easily customizable to become
	 * [Chat-ops](https://github.com/atmos/hubot-deploy) (deploying via Slack)
	 * [Hubot-insulter](https://github.com/altryne/hubot-insulter)
- Put a dashboard like [this](http://dashingdemo.herokuapp.com/sample), [this](http://dashboard.sidlee.com/) 
- Use extensionizr
- Build an onboarding site at your place of work for new employees with all the relevant info
****
###[Binary Data Adventures in Browser JavaScript by Or Hiltch](http://slnwww.slideshare.net/orhiltch/binary-data-adventures-in-browser-javascript)
in js all numbers are float64 but all bitwise ops are int32!
bitwise ops much faster than parseInt()
asm.js- lib for handling numbers faster
use transpilers to produce code (emscripten)
best to install from docker
webgl inspector for debugging webgl


****
###Landing your dream job as a FED by Igal Steklov
Don't even bother - you are not worthy to work at Wix, let alone sending us a CV. Be a ninja (yes, he showed pics of ninjas) and then maybe for a tiny split second we may slip and consider you as a lowly candidate to change our diapers
*****
###[BOOM Performance - the required ingredient for any successful web product by Eran Zinman](http://www.slideshare.net/zzeran/yglf-2015-boom-performance-eran-zinman-dapulse)
This is the signing off presentation that was also good. Eran tries to convince us that speed is important (wrong audience here) and how to do it.
Devs are in charge of speed
#####Key points
Don't forget the Basics
*Minify JS + CSS 
* Gzip compression
* Optimize images (PNG)
* CDN
* Remove render-blocking JS (Move to bottom of HTML)

Don’t shoot yourself in the foot - don't do stupid things with lots of re-rendering (*for* loops)
Mind the things that make the DOM Heavy 
• Use with caution: Round Corners, Box Shadows, Opacity 
• Beware of binding scroll callback events 
• Avoid using too many elements (especially in repeatable elements) 
• GPU Rendering when possible
Always keep 60fps scroll performance

Use optimistic actions
Facebook shows comments in the ui before post response returns
Instagram uploads images in first stage of share flow
Render first and if there's an error - DO NOTHING or roll back

Prerender, prefetch, preconnect
80% of user actions are recurrent, Use tracking to know what the users are doing
Typeahead.js - client lib for autocomplete
Lunr.js - client Solr/ElasticSearch alternative
Localstorage is your friend

The fastest request is “no request”

[Perceived performance](http://blog.teamtreehouse.com/perceived-performance)
Not everything should be "real", but perceived is enough
• Gradual UI loading (Facebook effect)
• Progress bars 
• Buttons hover + active state + ladda.js 
• Animations (but don’t animate for more than 100ms)

#####The takeaway
1. Boom Performance = User happiness. 
2. Don’t skip the basic optimization stuff.
3. Unless you must wait for the server – don’t! 
4. Fetch the data just before the user needs it.
5. If you can’t make it – fake it (perceived performance).
***

