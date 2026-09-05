# scratch-text-engine-generator-from-fonts
Converts .ttf and .otf to Scratch 3 sprites (text engines you can use to render any text with any real font).

Download the .exe and follow the instructions. You'll get a .sprite3 file. Import it into Scratch.

Before we start configuring the engine, let's have a quick look at the animations.
Animation types:
1 — simple appearing of the letters one after another. Has a fixed speed.
2 — the most customizable animation. It can smoothly change the opacity and the y position of the letters. Customizable with the variables starting with "AT2". With default values it goes down by 20, becomes invisible and then smoothly appears and moves upward.
3 — smooth change of the size. Customizable with variables starting with "AT3". My favorite one, altough it's rather expensive and can be a bit laggy. With default values it changes the size by -30 and then smoothly gets it back.
The animations use a smoothstep as the ease, but you can change it by modifying the "ease" variable in the functions.
Now let's talk about the config variables.

They are right below the welcome comment in the text engine sprite.
The top ones are pretty obvious and you can understand what they do by the animations info and the names.
The LINE_BREAK_CHARACTER variable (default=¶) is the symbol that you type when you need to go to a new line while rendering the text. For example passing "Hello¶World" (or whatever you set this variable to) will render:
Hello
World

The second one, ANIMATION_STEPS is the weirdest thing here. Don't make set it to anything below 1 or the animations will act weirdly. It basically controls the duration of the animations (except the 1st type, its speed is fixed) but not in seconds or anything, just in some abstract units. 7 seemed optimal for me, so that's the default value.

Now, how to actually USE the engine?
Well, this is done using global variables and broadcasts. Let's have a look at the variables first.
ANIMATION_TYPE (TE) — this variable controls the animation type. If set to something below 1, the text is rendered instantly. Also, when the text is rendered instantly, it doesn't play a sound.
MAX_X (TE) — that's the maximum X where a symbol can be rendered. It is used for the auto-line wrapping. If you want to disable the auto-line wrapping (please don't, I struggled to make it), just leave it empty!
START_X (TE) and START_Y (TE) are the position of the bottom left corner of the top line of the text. Sounds complicated, but really isn't.
TEXT (TE) is the text you want to render.
TEXT_SIZE (TE) is, well, the size of the text you want to render. It's also in some abstract units, not pixels, I'm sorry, but I guess that's fine.

And there are also two broadcasts:
CLEAR_ALL_TEXT — this (obviously) clears all the text on the screen. VERY IMPORTANT: USE "BROADCAST AND WAIT", NOT JUST "BROADCAST"
RENDER_TEXT — it renders the text based on the global variables.

I guess that's all. If you find any bugs, let me know (or don't, I'm rather tired, I'm writing this at 4AM).

P.S. If you are using a pixel font, go to the left of the editor and attach a piece of code up (there is a comment, you'll find it).
