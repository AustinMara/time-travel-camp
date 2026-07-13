# Dino Dash 🦕
### @explicitHints true

## {Welcome, Time Traveler! @showdialog}

WHOOSH! Your time machine lands **66 million years in the past** — the age of dinosaurs!

A silly banana-yellow robot buddy came along to help you collect dino eggs.

Click **Start** to build your first game!

## {Step 1}

Let's paint the prehistoric sky.

- :tree: Open the ``||scene:Scene||`` drawer. Drag ``||scene:set background color to||`` into the middle of the ``||loops(noclick):on start||`` block.
- :mouse pointer: Click the color circle and pick a **green** — dino jungle green!

#### ~ tutorialhint
```blocks
scene.setBackgroundColor(7)
```

## {Step 2}

Now add YOU — a little dinosaur explorer.

- :paper plane: Open the ``||sprites:Sprites||`` drawer. Drag ``||variables(sprites):set mySprite to sprite of kind Player||`` into ``||loops(noclick):on start||``, right **under** the background block.
- :paint brush: Click the **gray square**. In the editor, click **Gallery** and pick a creature you like — or draw your own dino! Then click **Done**.

#### ~ tutorialhint
```blocks
let mySprite = sprites.create(img`
. . . . . . . . . 7 7 7 7 . . .
. . . . . . . . 7 7 7 7 7 7 . .
. . . . . . . . 7 7 f 7 7 7 . .
. . . . . . . . 7 7 7 7 7 7 . .
. . 7 . . . . 7 7 7 7 7 . . . .
. . 7 7 . . 7 7 7 7 7 . . . . .
. . 7 7 7 7 7 7 7 7 7 . . . . .
. . 7 7 7 7 7 7 7 7 7 7 . . . .
. . . 7 7 7 7 7 7 7 7 7 . . . .
. . . 7 7 7 7 7 7 7 7 . . . . .
. . . 7 7 7 7 7 7 7 . . . . . .
. . . 7 7 . 7 7 7 . . . . . . .
. . . 7 7 . 7 7 . . . . . . . .
. . . 7 . . . 7 . . . . . . . .
. . . 7 . . . 7 . . . . . . . .
. . 7 7 . . 7 7 . . . . . . . .
`, SpriteKind.Player)
```

## {Step 3}

Let's make your dino move with the arrow buttons.

- :game: Open the ``||controller:Controller||`` drawer. Drag ``||controller:move mySprite with buttons||`` into ``||loops(noclick):on start||``, under the sprite block.
- :binoculars: Press the **arrow buttons** on the game screen — your dino moves!

#### ~ tutorialhint
```blocks
let mySprite: Sprite = null
//@highlight
controller.moveSprite(mySprite)
```

## {Step 4}

Oops — your dino can run right off the screen! Let's stop that.

- :paper plane: From ``||sprites:Sprites||``, drag ``||sprites:set mySprite stay in screen on||`` into ``||loops(noclick):on start||``, at the bottom.

#### ~ tutorialhint
```blocks
let mySprite: Sprite = null
//@highlight
mySprite.setStayInScreen(true)
```

## {Step 5}

Every game needs a score! Let's start it at 0.

- :id card: Open the ``||info:Info||`` drawer. Drag ``||info:set score to 0||`` into ``||loops(noclick):on start||``, at the bottom.

#### ~ tutorialhint
```blocks
info.setScore(0)
```

## {Step 6}

Now for the dino eggs! We want a new egg to appear again and again, so we need a **loop that repeats forever**.

- :clock: Open the ``||game:Game||`` drawer. Drag ``||game:on game update every 500 ms||`` into an **empty spot** on the workspace (NOT inside ``||loops(noclick):on start||``).

This block runs everything inside it every half second.

#### ~ tutorialhint
```blocks
game.onUpdateInterval(500, function () {

})
```

## {Step 7}

Let's make an egg appear inside that loop.

- :paper plane: From ``||sprites:Sprites||``, drag another ``||variables(sprites):set mySprite to sprite of kind Player||`` and drop it **inside** the ``||game(noclick):on game update every 500 ms||`` block.
- :mouse pointer: Click the **mySprite** dropdown (the little triangle) and pick **Rename variable…**. Type **egg** and click Ok.
- :mouse pointer: Click the **Player** dropdown at the end of the block and change it to **Food**.
- :paint brush: Click the gray square and draw a small white egg (or pick one from the Gallery). Click **Done**.

#### ~ tutorialhint
```blocks
let egg: Sprite = null
game.onUpdateInterval(500, function () {
    egg = sprites.create(img`
. . e e e e . .
. e 1 1 1 1 e .
e 1 1 1 1 1 1 e
e 1 1 1 1 1 1 e
e 1 1 1 1 1 1 e
e e 1 1 1 1 e e
. e e 1 1 e e .
. . e e e e . .
`, SpriteKind.Food)
})
```

## {Step 8}

Right now every egg appears in the middle of the screen. Let's add a block that can move it.

- :paper plane: From ``||sprites:Sprites||``, drag ``||sprites:set mySprite position to x 0 y 0||`` and drop it **inside** the ``||game(noclick):on game update||`` loop, right **under** the egg block.
- :mouse pointer: Click the **mySprite** dropdown on this new block and change it to **egg**.

The **x** number is how far **left/right** the egg goes. The **y** number is how far **up/down** it goes.

#### ~ tutorialhint
```blocks
let egg: Sprite = null
game.onUpdateInterval(500, function () {
    //@highlight
    egg.setPosition(0, 0)
})
```

## {Step 9}

Now let's make the position **random**, so every egg lands somewhere new!

- :calculator: Open the ``||math:Math||`` drawer. Drag ``||math:pick random 0 to 10||`` and drop it **right on top of the first 0** — the **x** slot. It should click in like a puzzle piece.
- :mouse pointer: Change its numbers to **10** and **150**.
- :calculator: Drag a **second** ``||math:pick random 0 to 10||`` on top of the other 0 — the **y** slot.
- :mouse pointer: Change its numbers to **10** and **110**.

Now eggs pop up all over the screen!

#### ~ tutorialhint
```blocks
let egg: Sprite = null
game.onUpdateInterval(500, function () {
    //@highlight
    egg.setPosition(randint(10, 150), randint(10, 110))
})
```

## {Step 10}

Time to collect! We need the game to notice when your dino **touches** an egg.

- :paper plane: From ``||sprites:Sprites||``, drag ``||sprites:on sprite of kind Player overlaps otherSprite of kind Player||`` into an **empty spot** on the workspace.
- :mouse pointer: Click the **second** dropdown (the one after "otherSprite of kind") and change it from **Player** to **Food**.

"Overlaps" is coder-talk for "touches"!

#### ~ tutorialhint
```blocks
sprites.onOverlap(SpriteKind.Player, SpriteKind.Food, function (sprite, otherSprite) {

})
```

## {Step 11}

When you touch an egg: the egg disappears, and you get a point!

- :paper plane: From ``||sprites:Sprites||``, drag ``||sprites:destroy mySprite||`` **inside** the overlap block. Click its dropdown and change it to **otherSprite** (that's the egg!).
- :id card: From ``||info:Info||``, drag ``||info:change score by 1||`` **inside** the overlap block, under the destroy block.

#### ~ tutorialhint
```blocks
sprites.onOverlap(SpriteKind.Player, SpriteKind.Food, function (sprite, otherSprite) {
    otherSprite.destroy()
    info.changeScoreBy(1)
})
```

## {Step 12}

One more friend — your silly yellow robot helper!

- :paper plane: From ``||sprites:Sprites||``, drag ``||variables(sprites):set mySprite to sprite of kind Player||`` into ``||loops(noclick):on start||``, at the bottom. Rename the variable to **helper**.
- :paint brush: Draw a **banana-yellow robot** with big goggle eyes (use the yellow color!). Click **Done**.
- :paper plane: From ``||sprites:Sprites||``, drag ``||sprites:say hi||`` under it. Change the dropdown to **helper** and the words to **Grab the eggs!**

#### ~ tutorialhint
```blocks
let helper = sprites.create(img`
. . . . f f f f f f f f . . . .
. . . f 5 5 5 5 5 5 5 5 f . . .
. . f 5 5 5 5 5 5 5 5 5 5 f . .
. f 5 5 f f f f f f f f 5 5 f .
. f 5 f 9 9 1 f f 1 9 9 f 5 f .
. f 5 f 9 1 1 f f 1 1 9 f 5 f .
. f 5 f f f f f f f f f f 5 f .
. f 5 5 5 5 5 5 5 5 5 5 5 5 f .
. f 5 5 5 5 5 5 5 5 5 5 5 5 f .
. f 5 5 f 5 5 5 5 5 5 f 5 5 f .
. f 5 5 f 5 5 5 5 5 5 f 5 5 f .
. . f 5 5 f f f f f f 5 5 f . .
. . f 5 5 5 5 5 5 5 5 5 5 f . .
. . . f 5 5 f . . f 5 5 f . . .
. . . f 5 5 f . . f 5 5 f . . .
. . . f f f f . . f f f f . . .
`, SpriteKind.Player)
helper.say("Grab the eggs!")
```

## {Step 13}

- :binoculars: **Play your game!** Use the arrows to run around and gobble up eggs. Watch your score climb!

You built a whole game — amazing work, Time Traveler! 🦕

## {Challenge Time! 🏆}

Done early? Try one of these:

1. **Beat the clock:** From ``||info:Info||``, add ``||info:start countdown 30||`` into ``||loops(noclick):on start||``. Now the game ends in 30 seconds!
2. **Sound FX:** From ``||music:Music||``, add ``||music:play sound||`` inside your overlap block so eggs make a noise.
3. **Slow down the eggs:** Change **500** to **1000** so eggs appear slower — or **300** for egg madness!
4. **Danger rock:** Make a new sprite of kind **Enemy** and a new overlap block that does ``||info:change score by -1||`` when you touch it.