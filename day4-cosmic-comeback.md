# Cosmic Comeback 🚀
### @explicitHints true

## {Blast to the Future! @showdialog}

Final jump! Your time machine rockets **far into the future** — deep space!

Your yellow robot buddy is riding along. Blast asteroids, dodge crashes, and **score 20 to fly home**. This game uses EVERYTHING you've learned!

## {Step 1}

Set a deep-space background.

- :tree: From ``||scene:Scene||``, drag ``||scene:set background color to||`` into ``||loops(noclick):on start||`` and pick **black**.

#### ~ tutorialhint
```blocks
scene.setBackgroundColor(15)
```

## {Step 2}

Add your rocket ship.

- :paper plane: From ``||sprites:Sprites||``, drag ``||variables(sprites):set mySprite to sprite of kind Player||`` into ``||loops(noclick):on start||``.
- :paint brush: Draw a rocket, or find one in the **Gallery**. Click **Done**.
- :game: From ``||controller:Controller||``, add ``||controller:move mySprite with buttons||``.
- :paper plane: Add ``||sprites:set mySprite stay in screen on||``.
- :paper plane: Add ``||sprites:set mySprite position to x 0 y 0||`` and change it to **x 20, y 60** — the left side.

#### ~ tutorialhint
```blocks
let mySprite = sprites.create(img`
. . . . . . . 1 1 . . . . . . .
. . . . . . 1 1 1 1 . . . . . .
. . . . . . 1 9 9 1 . . . . . .
. . . . . . 1 9 9 1 . . . . . .
. . . . . 1 1 9 9 1 1 . . . . .
. . . . . 1 9 9 9 9 1 . . . . .
. . . . 1 1 9 9 9 9 1 1 . . . .
. . . . 1 9 9 9 9 9 9 1 . . . .
. . . 1 1 9 9 9 9 9 9 1 1 . . .
. . . 1 9 9 9 9 9 9 9 9 1 . . .
. . . 1 9 9 9 9 9 9 9 9 1 . . .
. . 2 1 1 9 9 9 9 9 9 1 1 2 . .
. . 2 2 1 1 9 9 9 9 1 1 2 2 . .
. . . . 2 2 1 1 1 1 2 2 . . . .
. . . . . 2 2 4 4 2 2 . . . . .
. . . . . . 4 4 4 4 . . . . . .
`, SpriteKind.Player)
controller.moveSprite(mySprite)
mySprite.setStayInScreen(true)
mySprite.setPosition(20, 60)
```

## {Step 3}

Your yellow robot buddy comes too!

- :paper plane: From ``||sprites:Sprites||``, drag another ``||variables(sprites):set mySprite to sprite of kind Player||`` into ``||loops(noclick):on start||``. Click the dropdown, pick **Rename variable…**, and name it **buddy**.
- :paint brush: Draw your banana-yellow goggle-eyed robot. Click **Done**.
- :paper plane: Add ``||sprites:set mySprite position to x 0 y 0||`` set to **buddy**, at **x 12, y 20** — a safe corner.
- :paper plane: Add ``||sprites:say hi||`` set to **buddy**, saying **Blast the rocks!**

#### ~ tutorialhint
```blocks
let buddy = sprites.create(img`
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
buddy.setPosition(12, 20)
buddy.say("Blast the rocks!")
```

## {Step 4}

Set up the mission: score 0, 3 lives, and 60 seconds.

- :id card: From ``||info:Info||``, add ``||info:set score to 0||`` into ``||loops(noclick):on start||``.
- :id card: Add ``||info:set life to 3||`` under it.
- :id card: Add ``||info:start countdown 10||`` under that, and change **10** to **60**.

#### ~ tutorialhint
```blocks
info.setScore(0)
info.setLife(3)
info.startCountdown(60)
```

## {Step 5}

Incoming asteroids!

- :clock: From ``||game:Game||``, drag ``||game:on game update every 500 ms||`` into an empty spot. Change **500** to **900**.
- :paper plane: From ``||sprites:Sprites||``, drag ``||variables(sprites):set projectile to projectile from side with vx 50 vy 50||`` **inside** it.
- :paint brush: Click the gray square, open the **Gallery**, and pick an **asteroid**. Click **Done**.
- :mouse pointer: Change **vx** to **-80** and **vy** to **0**.
- :paper plane: Add ``||sprites:set mySprite kind to Player||`` under it — dropdown to **projectile**, kind to **Enemy**.
- :paper plane: Add ``||sprites:set mySprite x to 0||`` — dropdown to **projectile**, change **x** to **y**, then drop in ``||math:pick random 0 to 10||`` from ``||math:Math||`` and change it to **10** and **110**.

#### ~ tutorialhint
```blocks
let projectile: Sprite = null
game.onUpdateInterval(900, function () {
    projectile = sprites.createProjectileFromSide(sprites.space.spaceAsteroid0, -80, 0)
    projectile.setKind(SpriteKind.Enemy)
    projectile.y = randint(10, 110)
})
```

## {Step 6}

Lasers! Press **A** to fire.

- :game: From ``||controller:Controller||``, drag ``||controller:on A button pressed||`` into an empty spot.
- :paper plane: Inside, add ``||variables(sprites):set projectile to projectile from mySprite with vx 50 vy 50||``.
- :paint brush: Draw a short red laser line. Click **Done**.
- :mouse pointer: Change **vx** to **120** and **vy** to **0**.

#### ~ tutorialhint
```blocks
let mySprite: Sprite = null
controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
    let projectile2 = sprites.createProjectileFromSprite(img`
2 2 2 2 2
`, mySprite, 120, 0)
})
```

## {Step 7}

Laser meets asteroid — BOOM!

- :paper plane: From ``||sprites:Sprites||``, drag ``||sprites:on sprite of kind Player overlaps otherSprite of kind Player||`` into an empty spot. Change the dropdowns to **Projectile** and **Enemy**.
- :paper plane: Inside: ``||sprites:destroy mySprite||`` set to **sprite**, then another ``||sprites:destroy mySprite||`` set to **otherSprite** (click the **plus (+)** and pick the **disintegrate** effect!).
- :id card: Add ``||info:change score by 1||``.

#### ~ tutorialhint
```blocks
sprites.onOverlap(SpriteKind.Projectile, SpriteKind.Enemy, function (sprite, otherSprite) {
    sprite.destroy()
    otherSprite.destroy(effects.disintegrate, 100)
    info.changeScoreBy(1)
})
```

## {Step 8}

If an asteroid hits your ship — lose a life and SHAKE the screen!

- :paper plane: Drag another overlap block. Change the second dropdown to **Enemy**.
- :paper plane: Inside: ``||sprites:destroy mySprite||`` set to **otherSprite**.
- :id card: Add ``||info:change life by -1||``.
- :binoculars: From ``||scene:Scene||``, add ``||scene:camera shake||``.

#### ~ tutorialhint
```blocks
sprites.onOverlap(SpriteKind.Player, SpriteKind.Enemy, function (sprite, otherSprite) {
    otherSprite.destroy()
    info.changeLifeBy(-1)
    scene.cameraShake(4, 500)
})
```

## {Step 9}

The final piece — WIN when you reach 20 points!

- :clock: From ``||game:Game||``, drag ``||game:on game update||`` (the one **without** "every ms") into an empty spot.
- :flag: From ``||logic:Logic||``, drag an ``||logic:if then||`` block inside it.
- :flag: From ``||logic:Logic||``, drop a ``||logic:0 < 0||`` comparison block into the **if** slot. Click the **<** dropdown and pick **≥**.
- :id card: From ``||info:Info||``, drop the round ``||info:score||`` block into the **left** slot. Type **20** in the right slot.
- :circle: From ``||game:Game||``, drag ``||game:game over WIN||`` inside the **then** part.

#### ~ tutorialhint
```blocks
game.onUpdate(function () {
    if (info.score() >= 20) {
        game.over(true)
    }
})
```

## {Step 10}

- :binoculars: **Play the final mission!** Fly, shoot, dodge — reach 20 points before time runs out to fly home!

You traveled through ALL of history and made it back. You're officially a game developer! 🎉

## {Challenge Time! 🏆}

1. **Power-up star:** Make a **Food** sprite appear sometimes, and add an overlap block that gives ``||info:change life by 1||`` when you collect it.
2. **Meteor storm:** Change **900** to **500** — twice the asteroids!
3. **Turbo laser:** Make button **B** fire a laser going **up** (vx 0, vy -120).
4. **Level 2:** After you win, challenge a friend: who can reach 20 points fastest?