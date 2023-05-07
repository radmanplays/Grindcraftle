# Advanced use of the Grindcraft Game Maker tool

To add custom function and variables to your game, you first have to know how all the player stats are being saved.

### The player object

Everything in your game is saved in the `player` object. Knowing how it looks and how it works is useful for creating advanced games.

```
player = {
    // Player stats
    currentArea: 0,                                         // The location in the areaList of your current area (0 is the first value.)
    resources: {                                            // List of all your resources
        dirt: {
            image: "images/dirt.png",
            amount: 3,
        },
        stick: {
            image: "images/stick.png",
            amount: 1,
        },
        planks: {
            image: "images/planks.png",
            amoun: 0,
        },
    },
    variables: {                                            // List of your custom variables
        coolVariableName: 2,
    },
    areaList: ["c", "i", "b"],                              // List of all the areaIDs

    // Areas
    c: {                                                    // All the area info is saved here
        name: "City State",
        image: "images/areas/cityState.png",
        unlocked: true,
        updateWhileUnactive: true,

        grinds: [
            // etc.
        ],

        crafts: [
            // etc.
        ],

        update(diff) {

        },
    }

    i: {
        // etc.
    }

    b: {
        // etc.
    }

    // FPS counter
    currentTicks: 53,
    currentTime: 436,
    lastScreenUpdate: 1657816061456,

    // Settings
    maxFPS: 100,
    showGrindMats: true,
    showCraftRecipes: true,
    enableAutobuys: true,
    autoSave: true,

    // Checks
    saveGotten: true,                                       // Will be true when your save has been received
    switchArea: false,                                      // Will be true while switching area
};
```

 - If you for example want to check how much dirt the player has, you could get it by typing `player.resources.dirt.amount`.
   - For multiple words in the resource name, type `player.resources["crafting table"].amount`.
 - If you want to access the different grinds/crafts, and maybe change them, you could type `player.areaID.grinds` or `player.areaID.crafts`.
   - To access a specific grind, you just add the location of the grind in the `grinds` list: `player.areaID.grinds[0]`. The same goes for crafts.
     - (Counting in lists starts at 0, meaning the first item has an *index* of 0, the second an index of 1, etc.)

### Custom variables

For more advanced games, it might be useful to create your own variables to store different stats/values for even more functionality. If you want to create a variable, you have to use the `addVariables` function:
```
addVariables({
    coolVariableName: 2,
});
```
Here, i've added a variable named `coolVariableName`, with the value 2. The value can be anything you want, from text, to numbers, to arrays, and even objects or functions.

To access a variable, you just type `player.variables.variableName`!

### The update function & custom functions

Each area has its own `update` function that will be run every frame, as long as the `updateWhileUnactive` property is true:

```
update(diff) {                  // diff is the time in milliseconds since last time the update function was run.
    console.log(diff);
},
```

If `updateWhileUnactive` is false, the function will only run while you're currently in this area.

This can be used for anything you want, and is useful for checking the current amount of resources, or checking if the player is currently grinding a resource.

Of course, you can also make your own functions. Just add them to your [areas.js](/js/areas.js) file, or make a separate .js file for your own functions.
Then, you can use either the `update` function, or the `runFunction` property in crafts, to run the function.

### Other useful functions

Some other useful functions that you can use in your game are the `randomRange`, `randomFloat` and the `randomRound` functions:

 - `randomRange` has two parameters: `(min, max)` and will return a random integer from `min` to `max`
   - Example: `randomRange(2, 5)` returns a random number from 2 to 5
 - `randomFloat` also has the same parameters, but it will instead return a random number with two decimal digits
   - Example: `randomFloat(1.2, 3.5)` returns a random number from 1.20 to 3.50
 - `randomRound` only has one parameter: `(number)`. It will randomly round the number up or down, depending on the decimal digits
   - Example: `randomRound(1.3)` has a 30% chance of rounding up to 2 and a 70% chance of rounding down to 1