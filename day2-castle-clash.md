# Castle Clash 🐉
### @explicitHints true

## {Jump to the Middle Ages! @showdialog}

WHOOSH! Your time machine lands at a **medieval castle** — and dragons are attacking!

Today you'll learn to **shoot** and use **lives**. Grab your magic wand, hero!

## {Step 1}

Set a stormy castle sky.

- :tree: From ``||scene:Scene||``, drag ``||scene:set background color to||`` into ``||loops(noclick):on start||``.
- :mouse pointer: Click the color circle and pick **gray**.

#### ~ tutorialhint
```blocks
scene.setBackgroundColor(11)
```

## {Step 2}

Add your hero.

- :paper plane: From ``||sprites:Sprites||``, drag ``||variables(sprites):set mySprite to sprite of kind Player||`` into ``||loops(noclick):on start||``.
- :paint brush: Click the gray square, open the **Gallery**, and pick the knight hero (or draw your own). Click **Done**.

#### ~ tutorialhint
```blocks
let mySprite = sprites.create(sprites.castle.heroWalkFront1, SpriteKind.Player)
```

## {Step 3}

Make the hero move, keep them on screen, and start them on the **left side**.

- :game: From ``||controller:Controller||``, drag ``||controller:move mySprite with buttons||`` into ``||loops(noclick):on start||``.
- :paper plane: From ``||sprites:Sprites||``, drag ``||sprites:set mySprite stay in screen on||`` under it.
- :paper plane: From ``||sprites:Sprites||``, drag ``||sprites:set mySprite position to x 0 y 0||`` under that. Change **x to 20** and **y to 60**.

#### ~ tutorialhint
```blocks
let mySprite: Sprite = null
controller.moveSprite(mySprite)
mySprite.setStayInScreen(true)
mySprite.setPosition(20, 60)
```

## {Step 4}

Heroes get more than one chance! Give yourself **3 lives** and a score of 0.

- :id card: From ``||info:Info||``, drag ``||info:set life to 3||`` into ``||loops(noclick):on start||``.
- :id card: From ``||info:Info||``, drag ``||info:set score to 0||`` under it.

See the 3 hearts at the top of the screen?

#### ~ tutorialhint
```blocks
info.setLife(3)
info.setScore(0)
```

## {Step 5}

Now the dragons! First we need a loop that keeps making them.

- :clock: From ``||game:Game||``, drag ``||game:on game update every 500 ms||`` into an **empty spot** on the workspace.
- :mouse pointer: Click the **500** and change it to **1200**.

A new dragon will appear every 1.2 seconds.

#### ~ tutorialhint
```blocks
game.onUpdateInterval(1200, function () {

})
```

## {Step 6}

Let's make a dragon that flies in from the right, all by itself.

- :paper plane: From ``||sprites:Sprites||``, drag ``||variables(sprites):set projectile to projectile from side with vx 50 vy 50||`` and drop it **inside** the ``||game(noclick):on game update||`` loop.
- :paint brush: Click the gray square and draw a small dragon. Click **Done**.
- :mouse pointer: Change **vx** to **-75** (minus means it flies **left**, toward you!). Change **vy** to **0**.

#### ~ tutorialhint
```blocks
let projectile: Sprite = null
game.onUpdateInterval(1200, function () {
    projectile = sprites.createProjectileFromSide(img`
f . . . . . . f
f f . . . . f f
f f f 2 2 f f f
. f f f f f f .
. . f f f f . .
. . . f f . . .
. . f . . f . .
. f . . . . f .
`, -75, 0)
})
```

## {Step 7}

Two finishing touches for the dragon.

- :paper plane: From ``||sprites:Sprites||``, drag ``||sprites:set mySprite kind to Player||`` **inside** the loop, under the dragon block. Change the first dropdown to **projectile** and the kind to **Enemy**.
- :paper plane: From ``||sprites:Sprites||``, drag ``||sprites:set mySprite x to 0||`` under that. Change the dropdown to **projectile** and change **x** to **y**.
- :calculator: From ``||math:Math||``, drag ``||math:pick random 0 to 10||`` on top of the number. Change it to **10** and **110**.

Now dragons appear at random heights!

#### ~ tutorialhint
```blocks
let projectile: Sprite = null
game.onUpdateInterval(1200, function () {
    projectile.setKind(SpriteKind.Enemy)
    projectile.y = randint(10, 110)
})
```

## {Step 8}

Time to fight back! Press **A** to shoot a magic bolt.

- :game: From ``||controller:Controller||``, drag ``||controller:on A button pressed||`` into an empty spot.
- :paper plane: From ``||sprites:Sprites||``, drag ``||variables(sprites):set projectile to projectile from mySprite with vx 50 vy 50||`` **inside** it.
- :paint brush: Draw a small yellow star bolt. Click **Done**.
- :mouse pointer: Change **vx** to **100** and **vy** to **0** — it flies right, toward the dragons!

#### ~ tutorialhint
```blocks
let mySprite: Sprite = null
controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
    let projectile2 = sprites.createProjectileFromSprite(img`
. . 4 . .
. 4 4 4 .
4 4 4 4 4
. 4 4 4 .
. . 4 . .
`, mySprite, 100, 0)
})
```

## {Step 9}

When a bolt hits a dragon — POOF!

- :paper plane: From ``||sprites:Sprites||``, drag ``||sprites:on sprite of kind Player overlaps otherSprite of kind Player||`` into an empty spot.
- :mouse pointer: Change the **first** dropdown to **Projectile** and the **second** to **Enemy**.
- :paper plane: Inside it, add ``||sprites:destroy mySprite||`` — set the dropdown to **sprite** (the bolt).
- :paper plane: Add another ``||sprites:destroy mySprite||`` — set it to **otherSprite** (the dragon). Click the **plus (+)** on this block and pick the **fire** effect!
- :id card: From ``||info:Info||``, add ``||info:change score by 1||`` at the bottom.

#### ~ tutorialhint
```blocks
sprites.onOverlap(SpriteKind.Projectile, SpriteKind.Enemy, function (sprite, otherSprite) {
    sprite.destroy()
    otherSprite.destroy(effects.fire, 100)
    info.changeScoreBy(1)
})
```

## {Step 10}

But if a dragon reaches YOU — you lose a life!

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

## {Step 11}

- :binoculars: **Play!** Move with arrows, press **A** to fire. Lose all 3 hearts and it's game over. Defend the castle!

You're a true medieval hero! 🏰

## {Challenge Time! 🏆}

1. **Dragon horde:** Change **1200** to **700** — more dragons, more danger!
2. **Winning:** From ``||logic:Logic||`` and ``||game:Game||``, make the game show ``||game:game over WIN||`` when ``||info:score||`` reaches 15.
3. **Power shot:** Make button **B** shoot a bolt too — but a bigger one!
4. **Castle music:** From ``||music:Music||``, play a sound every time you fire.