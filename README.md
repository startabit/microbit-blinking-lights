# Blinking lights: police car and traffic light

### @explicitHints false

## Introduction @showdialog

Four LEDs and a button on a breadboard: red on **pin 1**, yellow on **pin 2**, green on **pin 8**, blue on **pin 13**,
and the button on **pin 14**. Each LED has a 220 Ω resistor.

![Wire it: the Micro:bit, 4 LEDs and a button on a breadboard](https://www.startabit.com/projects/blinking-lights/images/wiring-microbit.png)

## Step 1: Make it blink

The pin blocks are under **Advanced**, then ``||pins:Pins||``. In ``||basic:forever||``:
pin **P1** to **1**, pause **500**, pin **P1** to **0**, pause **500**.

```blocks
basic.forever(function () {
    pins.digitalWritePin(DigitalPin.P1, 1)
    basic.pause(500)
    pins.digitalWritePin(DigitalPin.P1, 0)
    basic.pause(500)
})
```

## Step 2: Download and look

**Download**: the red LED blinks.
Dark? Turn the LED round: the **long leg** goes to the resistor.

## Step 3: Flash like a police car

Now red and blue take turns. In ``||basic:forever||``: **P1** to **1** and **P13** to **0**, pause **300**,
then **P1** to **0** and **P13** to **1**, pause **300**.

```blocks
basic.forever(function () {
    pins.digitalWritePin(DigitalPin.P1, 1)
    pins.digitalWritePin(DigitalPin.P13, 0)
    basic.pause(300)
    pins.digitalWritePin(DigitalPin.P1, 0)
    pins.digitalWritePin(DigitalPin.P13, 1)
    basic.pause(300)
})
```

## Step 4: A function for the traffic lights

Make a function **lights** with three numbers: **red**, **yellow**, **green**.
Inside: **P1** to **red**, **P2** to **yellow**, **P8** to **green**.

```blocks
function lights (red: number, yellow: number, green: number) {
    pins.digitalWritePin(DigitalPin.P1, red)
    pins.digitalWritePin(DigitalPin.P2, yellow)
    pins.digitalWritePin(DigitalPin.P8, green)
}
```

## Step 5: The traffic light order

Empty ``||basic:forever||``. Then ``||functions:call lights||`` **1 0 0**, pause **3000**, **1 1 0**, pause **1000**,
**0 0 1**, pause **3000**, **0 1 0**, pause **1000**.

```blocks
function lights (red: number, yellow: number, green: number) {
    pins.digitalWritePin(DigitalPin.P1, red)
    pins.digitalWritePin(DigitalPin.P2, yellow)
    pins.digitalWritePin(DigitalPin.P8, green)
}
basic.forever(function () {
    lights(1, 0, 0)
    basic.pause(3000)
    lights(1, 1, 0)
    basic.pause(1000)
    lights(0, 0, 1)
    basic.pause(3000)
    lights(0, 1, 0)
    basic.pause(1000)
})
```

## Step 6: Download and check

**Download**: red, red and yellow, green, yellow, and red again.
That is the order of a Swedish traffic light.

## Step 7: Get the button ready

In ``||basic:on start||``: ``||pins:set pull pin P14 to up||``.
Now pin 14 reads **1** while the button is not pressed, and **0** when you press it.

```blocks
pins.setPull(DigitalPin.P14, PinPullMode.PullUp)
```

## Step 8: Wait for the button

In ``||basic:forever||``: call lights **0 0 1**, then ``||loops:while||`` ``||pins:digital read pin P14||`` **= 1**:
pause **20**. After the loop: pause **1000**, lights **0 1 0**, pause **1000**.

```blocks
function lights (red: number, yellow: number, green: number) {
    pins.digitalWritePin(DigitalPin.P1, red)
    pins.digitalWritePin(DigitalPin.P2, yellow)
    pins.digitalWritePin(DigitalPin.P8, green)
}
pins.setPull(DigitalPin.P14, PinPullMode.PullUp)
basic.forever(function () {
    lights(0, 0, 1)
    while (pins.digitalReadPin(DigitalPin.P14) == 1) {
        basic.pause(20)
    }
    basic.pause(1000)
    lights(0, 1, 0)
    basic.pause(1000)
})
```

## Step 9: Red for the pedestrians

Add at the end: lights **1 0 0**, pause **4000**, lights **1 1 0**, pause **1000**.

```blocks
function lights (red: number, yellow: number, green: number) {
    pins.digitalWritePin(DigitalPin.P1, red)
    pins.digitalWritePin(DigitalPin.P2, yellow)
    pins.digitalWritePin(DigitalPin.P8, green)
}
pins.setPull(DigitalPin.P14, PinPullMode.PullUp)
basic.forever(function () {
    lights(0, 0, 1)
    while (pins.digitalReadPin(DigitalPin.P14) == 1) {
        basic.pause(20)
    }
    basic.pause(1000)
    lights(0, 1, 0)
    basic.pause(1000)
    lights(1, 0, 0)
    basic.pause(4000)
    lights(1, 1, 0)
    basic.pause(1000)
})
```

## Step 10: Press the button

**Download**. The light stays green until you press the button.
Then yellow, red for the pedestrians, and green again.

## Well done! @showdialog

Your traffic light listens to a pedestrian button.
More challenges, like an emergency mode with the blue LED, are on the
[project page](https://www.startabit.com/projects/blinking-lights/#challenges).
