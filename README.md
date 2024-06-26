# Earth rescue
_This is a submission for [Frontend Challenge v24.04.17](https://dev.to/devteam/join-us-for-the-next-frontend-challenge-earth-day-edition-52e4), CSS Art: Earth Day._

## Inspiration
The gift from the DEV shop 🙂🙃🙂🙃

## Demo
Check out the game on [GitHub Pages](https://boris-schwarz.github.io/earth-day/)!

<small>If it's laggy, hit the toggle animation button in the top left corner.</small>

> Where CodePen?

Unfortunately, CodePen doesn't allow refreshing the `iframe` it's running in. I'm using it to re-start the game, when the player either won or lost the game.

If you want, you can peek into the source code in the [GitHub Repository](https://github.com/boris-schwarz/earth-day/).

## Journey
I started with the game's background and I wanted to create something spacey and I had no inspiration at all. Until I found Temani Afif's article about [wavy shapes & patterns in CSS](https://css-tricks.com/how-to-create-wavy-shapes-patterns-in-css/) on css-tricks.com. Space has waves, so I thought and it was the most painful part of the project.

### Waves... waves everywhere!
I have never been great in physics, math, geometry and anything number related and circles and accelleration of falling objects have been my bane in school. I spent a full day trying to understand how to generate waves in CSS, but my short attention span lead me to build a villager farm in minecraft instead, giving me enought momentum to create a somewhat spacey background with some depth.

### Gotta stay organized
After I had created space, the code was as spaghetti as it can get. I decided to switch to SCSS and finally read into the [BEM Pattern for CSS](https://getbem.com/) and after wasting another 4 hours, I decided that I could not decide wether the HUD is an element of the game and the button is an element of the HUD and the text is an element of the button and someone else also thought about this and called it the [BEM grandchildren problem](https://scalablecss.com/bem-nesting-grandchild-elements/). I decided to go with a half-assed approach of BEM and that's what you will find in my code.

### There's no earth
Space is nice, but it's not space day, it's earth day. So an earth had to be made. I had this abstracted earth-design of [Kurzgesagt](https://kurzgesagt.org/) in my mind, so I tried to go for it. However I wanted the landmasses to resemble those our planet earth and not just some green-blue ball in space, so I implemented earth using a [CSS grid](https://css-tricks.com/snippets/css/complete-guide-grid/) which I have never used before (flex does the job in most cases, right?). Also, if there's a question mark at the end of a sentence within parenthesis, do you put a dot after the closing parenthesis?

I also have to mention Kevin Powell's great video about [advanced usage of CSS grids](https://www.youtube.com/watch?v=cf-J4ffMBfo).

### There's an earth, but it's slooooow
I have used Firefox Developer Edition and because YouTube is always slow using this browser, I had tinkered with it in the past. My CSS animations were slow and laggy. I had moving clouds with opacity and stars with a blur-filter. I imagined it would be also laggy on older phones, and upon researching, I stumbled across Web Dev Simplified's video about [Performant CSS Animations](https://www.youtube.com/watch?v=4PStxeSIL9I).

It helped changing animations from `left: 100vw;` to `transform: translateX(100vw);`, but eventually I added a toggle button to disable unneeded animations.

### CHATEOAS
How did I toggle animations and other states of the game, you ask? **CHeckboxes As The Engine Of Application State** of course. The checkboxes are hidden and interactions are done with the `label` element. Since you can only ever change one element's state at once, the game is quite linear.

### Too much text
In the beginning I only had buttons to click, but then I guessed I could make small icons for the ecological disasters and I found Bennett Feely's [CSS clip-path maker](https://bennettfeely.com/clippy/). Altough I know Adobe Illustrator and also wrote some SVG by hand, I was lazy to figure out all the shapes and I didn't want to include any images or vector graphics at all in this project. So that website came in very handy.

### A good friend
There you are, saving earth from outer space all by yourself. Wouldn't it be nice to have some companion? And who doesn't like robots? I had used quite some CSS grid in the project (earth, clouds, icons for ecological disasters), so I thought why not make a whole 16x16 pixel robot in CSS? I did the math and I had no intention of creating 256 HTML elements (yes, I could have used VS Code's emmet functionality, e.g. `div*5`), so I kind of reduced the size and used the `grid-column` and `grid-row`'s `span` attribute. You can also stack grid elements following the default CSS z-index behaviour. Nice! I quickly made a design on [Pixilart](https://www.pixilart.com/) and then created the CSS code using the image as a visual guide.

### Worth mentioning
If you're wondering how I added a "timer" to the game's goals - it's just an animation.

Let's say the event "deforestation" begins, because the player has clicked on "Start game":

1. "Start game" is the label for the checkbox `state_deforestation_happening`
2. When `state_deforestation_happening` is checked, the following elements get an animation:

	1. The "goal" - A container displaying some text what's happening. The trick: The container is a grid with two equal sized columns. The lower column contains the "game over" message, but is off screen.
	The animation shows the top half of the "goal" container for a while and then shows the full container, while using `clip-path` to hide the top part of the container.

	1. The "goal timer bar" - Basically just a div that grows from `with: 0;` to `with: 100%;`.

	1. The "deforestation"-icons. Labels for checkboxes. If all icons are clicked, the next event (e.g. oil spill) begins.