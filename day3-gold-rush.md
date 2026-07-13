# Gold Rush ⛏️
### @explicitHints true

## {Yeehaw — the Wild West! @showdialog}

WHOOSH! It's **1849** — the California Gold Rush! Thousands of people are racing to find gold.

Today you'll build a **map to explore**, with a camera that follows you and a countdown clock. Giddy up!

## {Step 1}

First, let's build your desert world with a **tilemap** — a map made of little squares.

- :mountain: From ``||scene:Scene||``, drag ``||scene:set tilemap to||`` into ``||loops(noclick):on start||``.
- :paint brush: Click the **gray square** to open the map editor.
- :mouse pointer: Pick a **sand-colored tile** on the left, then click the **paint bucket** tool and click the map to fill it all with sand.
- :mouse pointer: Pick a **darker tile** and click a few squares to add rocks. Click **Done**.

#### ~ tutorialhint
```blocks
tiles.setTilemap(tilemap`level`)
```

## {Step 2}

Add your gold prospector.

- :paper plane: From ``||sprites:Sprites||``, drag ``||variables(sprites):set mySprite to sprite of kind Player||`` into ``||loops(noclick):on start||``.
- :paint brush: Pick a hero from the **Gallery** or draw a cowboy. Click **Done**.
- :game: From ``||controller:Controller||``, drag ``||controller:move mySprite with buttons||`` under it.

#### ~ tutorialhint
```blocks
let mySprite = sprites.create(sprites.castle.heroWalkFront1, SpriteKind.Player)
controller.moveSprite(mySprite)
```

## {Step 3}

Your map is bigger than the screen — so let's make the camera follow you!

- :binoculars: From ``||scene:Scene||``, drag ``||scene:camera follow sprite mySprite||`` into ``||loops(noclick):on start||``, at the bottom.
- :binoculars: Try walking around — the world scrolls with you!

#### ~ tutorialhint
```blocks
let mySprite: Sprite = null
//@highlight
scene.cameraFollowSprite(mySprite)
```

## {Step 4}

Gold rushes are a race! Add a **countdown**, a score, and 3 lives.

- :id card: From ``||info:Info||``, drag ``||info:start countdown 10||`` into ``||loops(noclick):on start||``. Change **10** to **45**.
- :id card: Add ``||info:set score to 0||`` under it.
- :id card: Add ``||info:set life to 3||`` under that.

#### ~ tutorialhint
```blocks
info.startCountdown(45)
info.setScore(0)
info.setLife(3)
```

## {Step 5}

Now let's make gold nuggets appear!

- :clock: From ``||game:Game||``, drag ``||game:on game update every 500 ms||`` into an **empty spot**. Change **500** to **800**.
- :paper plane: From ``||sprites:Sprites||``, drag ``||variables(sprites):set mySprite to sprite of kind Player||`` **inside** the loop.
- :mouse pointer: Click the **mySprite** dropdown, pick **Rename variable…**, and rename it to **gold**.
- :mouse pointer: Change the kind dropdown from **Player** to **Food**.
- :paint brush: Draw a shiny gold nugget (yellow and orange!). Click **Done**.

#### ~ tutorialhint
```blocks
let gold: Sprite = null
game.onUpdateInterval(800, function () {
    gold = sprites.create(img`
. 4 4 4 . .
4 5 5 5 4 .
4 5 1 5 5 4
. 4 5 5 5 4
. . 4 4 4 .
. . . . . .
`, SpriteKind.Food)
})
```

## {Step 6}

Scatter the gold to random spots — just like the eggs on Day 1!

- :paper plane: From ``||sprites:Sprites||``, drag ``||sprites:set mySprite position to x 0 y 0||`` **inside** the loop, under the gold block. Change the dropdown to **gold**.
- :calculator: From ``||math:Math||``, drag ``||math:pick random 0 to 10||`` onto the **x** slot (the first 0). Change it to **10** and **150**.
- :calculator: Drag another ``||math:pick random 0 to 10||`` onto the **y** slot (the second 0). Change it to **10** and **110**.

#### ~ tutorialhint
```blocks
let gold: Sprite = null
game.onUpdateInterval(800, function () {
    //@highlight
    gold.setPosition(randint(10, 150), randint(10, 110))
})
```

## {Step 7}

Grab that gold!

- :paper plane: From ``||sprites:Sprites||``, drag ``||sprites:on sprite of kind Player overlaps otherSprite of kind Player||`` into an empty spot. Change the **second** dropdown to **Food**.
- :paper plane: Inside, add ``||sprites:destroy mySprite||`` set to **otherSprite**.
- :id card: From ``||info:Info||``, add ``||info:change score by 1||``.

#### ~ tutorialhint
```blocks
sprites.onOverlap(SpriteKind.Player, SpriteKind.Food, function (sprite, otherSprite) {
    otherSprite.destroy()
    info.changeScoreBy(1)
})
```

## {Step 8}

Uh oh — tumbleweeds! They roll in from the right.

- :clock: From ``||game:Game||``, drag another ``||game:on game update every 500 ms||`` into an empty spot. Change **500** to **1500**.
- :paper plane: From ``||sprites:Sprites||``, drag ``||variables(sprites):set projectile to projectile from side with vx 50 vy 50||`` **inside** it.
- :paint brush: Draw a round brown tumbleweed. Click **Done**.
- :mouse pointer: Change **vx** to **-60** and **vy** to **0**.
- :paper plane: Add ``||sprites:set mySprite kind to Player||`` under it — set the dropdown to **projectile** and the kind to **Enemy**.
- :paper plane: Add ``||sprites:set mySprite x to 0||`` — set the dropdown to **projectile**, change **x** to **y**, and drop a ``||math:pick random 0 to 10||`` in the number slot. Change it to **10** and **110**.

#### ~ tutorialhint
```blocks
let projectile: Sprite = null
game.onUpdateInterval(1500, function () {
    projectile = sprites.createProjectileFromSide(img`
. . 4 4 4 . .
. 4 e 4 e 4 .
4 e 4 e 4 e 4
. 4 e 4 e 4 .
. . 4 4 4 . .
`, -60, 0)
    projectile.setKind(SpriteKind.Enemy)
    projectile.y = randint(10, 110)
})
```

## {Step 9}

Tumbleweeds hurt! Lose a life if one hits you.

- :paper plane: Drag another ``||sprites:on sprite of kind Player overlaps otherSprite of kind Player||`` into an empty spot. Change the **second** dropdown to **Enemy**.
- :paper plane: Inside, add ``||sprites:destroy mySprite||`` set to **otherSprite**.
- :id card: From ``||info:Info||``, add ``||info:change life by -1||``.

#### ~ tutorialhint
```blocks
sprites.onOverlap(SpriteKind.Player, SpriteKind.Enemy, function (sprite, otherSprite) {
    otherSprite.destroy()
    info.changeLifeBy(-1)
})
```

## {Step 10}

- :binoculars: **Play!** Explore the desert, grab gold before the timer hits zero, and dodge those tumbleweeds!

You struck it rich, partner! 🤠

## {Challenge Time! 🏆}

1. **Walls:** Open your tilemap again and use the **wall tool** (the brick icon) to make the rocks solid — now you can't walk through them!
2. **More time... or less!** Change the countdown to 60 for an easy game, or 20 for a speedrun.
3. **Big nugget bonus:** Change ``||info:change score by 1||`` to **2** — or make a second, bigger gold sprite worth even more.
4. **Faster feet:** In ``||controller:move mySprite with buttons||``, click the **plus (+)** and make the speed **150** — a true gold-rush sprint!