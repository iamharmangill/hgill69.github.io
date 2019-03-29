# Tutorial for Monster-Slayer
## A simple game with Vue

Vue.js is an open-source JavaScript framework for building user interfaces and single-page applications. Main features of vue are components, template and its reactivity. Vue  makes it so easy to make single page components with their own scripts and styles that can be used in other components very easily just by importing them.

However, in this project we will be making a simple game using the basic vue directives and methods to make the code really clean and small.

To get started, the user will need to know the basic HTML and CSS. Also, it would be great if you have seen the introductory tutorial provided on the vue website. It would be a good practise to know and apply the basic features that you just watched in this application.

To begin with, download the basic template provided which contains the html and css pages with buttons and some styles added with no functionality. Here is the [link](https://drive.google.com/file/d/1KRAHMiiCiJWcB4Vwxt6oPby5PZ6yIFfl/view?usp=sharing)


![Image](/images/MS-10.png)

#### index.html
```
<!DOCTYPE html>
<html>

<head>
    <title>Monster Slayer</title>
    <script src="https://npmcdn.com/vue/dist/vue.js"></script>
    <link href="css/foundation.min.css" rel="stylesheet">
    <link href="css/app.css" rel="stylesheet">
</head>
```
Here is the head section of HTML page in which we have title, script of vue and links to css and css stylesheets.
#### index.html
```
<body>
    <div id="app">
        <h1 class="mons">Monster Slayer</h1>
        <section class="row">
            <div class="small-6 columns">
                <h1 class="text-center">YOU</h1>
                <div class="healthbar">
                    <div class="healthbar text-center" 
                    style="background-color: green; margin: 0; color: white;">
                    
                    </div>
                </div>
            </div>
            <div class="small-6 columns">
                <h1 class="text-center">MONSTER</h1>
                <div class="healthbar">
                    <div class="healthbar text-center" style="background-color: green; margin: 0; color: white;">
                    </div>
                </div>
            </div>
        </section>
        <section class="row controls">
            <div class="small-12 columns">
                <button id="start-game">START NEW GAME</button>
            </div>
        </section>
        <section class="row controls">
            <div class="small-12 columns">
                <button id="attack">ATTACK</button>
                <button id="special-attack"">SPECIAL ATTACK</button>
                <button id="heal">HEAL</button>
                <button id="give-up">GIVE UP</button>
            </div>
        </section>
        <section class="row log">
            <div class="small-12 columns">
                <ul>
                    <li 
                    </li>
                </ul>
            </div>
        </section>
    </div>
</body>
```

Here is the body element of the HTML file where we have different sections representing rows and columns. We have used bootstrap in HTML to make it look nice and is really fast and easy to use. Inside the sections, we have different div elements and buttons that creats the basic template of pur app without any functionalities.

Now, create an app.js file in your project folder. And import your app.js file in your HTML file using Script tag just above the body end tag “</body>” as shown below:
```
       </section>
   </div>
   <script src="app.js"></script>
</body>
</html>
```

```
Note: You can choose any name for your javaScript file, but be very careful while importing.
As of now, we can start writing in app.js file.
```
#### App.js
```
new Vue({
   el: '#app',
});
```

In the app.js file, we’ll have to create an instance of Vue using the “new Vue()” function.

In the Vue instance, that we just created, we will connect it with specific element in the DOM that we want to manipulate. Here we are connecting this Vue instance with the div element with id:app as shown above.
```
Note: ‘el’ stands for element.
```
Now, let’s store some data in this vue instance.
```
new Vue({
   el: '#app',
   data: {
       playerHealth: 100,
       monsterHealth: 100,
       gameIsRunning: false,
       turns: []
   },
});
```

We’ll store playerHealth and set its value initially to 100. Similarly we’ll add monsterHealth and set its value to 100. These data properties will track the health of player and monster. We’ll also add ‘gameIsRunning’ to track the state of game and set it to false initially which means that the game is not running by default.
And, let’s also add turns which we’’ll use to log the actions of our player or monster in our game.

Now let’s use these data properties in our html.

#### Index.html
```
<div class="small-6 columns">
   <h1 class="text-center">YOU</h1>
   <div class="healthbar">
      <div class="healthbar text-center"
           style="background-color: green; margin: 0; color: white;"
           :style="{width: monsterHealth + '%'}">
              {{ monsterHealth }}
      </div>
   </div>
</div>
```
We’ll bind the data using the “Mustache” syntax (double curly braces). Bind playerHealth in the div body. If you refresh the page now, you’ll see value intial value display in the health bar but the width is not set properly according to health. So now, we’ll bind the “playerHealth” with the width property of style using “v-bind” directive to adjust the width of container according to player’s health. We use ‘%’ to make sure it fills its parent container according to percentage, otherwise, vue will use pixels.



Similarly, modify the template of Monster.
```
<div class="small-6 columns">
   <h1 class="text-center">MONSTER</h1>
   <div class="healthbar">
      <div class="healthbar text-center"
           style="background-color: green; margin: 0; color: white;"
           :style="{width: playerHealth + '%'}">
              {{ playerHealth }}
      </div>
   </div>
</div>
```

Now, refresh the page again and you’ll see the entire width is filled.

![Image](/images/MS-9.png)

Now, we’ll use v-if and v-else directives of view in our html template to show different parts conditionally.

Before:

![Image](/images/MS-7.png)

#### index.html
```
<section class="row controls" v-if="!gameIsRunning">
    <div class="small-12 columns">
        <button id="start-game">START NEW GAME</button>
    </div>
</section>

<section class="row controls" v-else>
    <div class="small-12 columns">
        <button id="attack">ATTACK</button>
        <button id="special-attack">SPECIAL ATTACK</button>
        <button id="heal">HEAL</button>
        <button id="give-up">GIVE UP</button>
    </div>
</section>
```
Take a look at the first section in the code above, it has v-if="!gameIsRunning" which makes sure that this section is only displayed when the game is not running, hence the ‘!’ sign. Similarly, we have used v-else in the next section that means that this section will get displayed if game is running. Here we can also use v-if="gameIsRunning" instead of using v-else. As of now, if you’ll refresh the page, you’ll only see the section with “START NEW GAME” button.

![Image](/images/MS-6.png)
```
Note: In order to use v-if and v-else, it’s important that both the elements should follow each other and should have the same type as well.
```
Now let’s add some functionalities to the buttons that we have. In order to do so, we will use event listener. This can be done using “v-on” directive of vue. Instead of writing “v-on”, we can simply use ‘@’ symbol. Here we’ll use click event listener which can be used by writing “v-on:click” or by simply using “@click”.


#### index.html
```
<section class="row controls" v-if="!gameIsRunning">
    <div class="small-12 columns">
        <button id="start-game"
        @click="startGame">START NEW GAME</button>
    </div>
</section>

<section class="row controls" v-else>
    <div class="small-12 columns">
        <button id="attack"
                @click="attack">ATTACK</button>
        <button id="special-attack"
                @click="specialAttack">SPECIAL ATTACK</button>
        <button id="heal"
                @click="heal">HEAL</button>
        <button id="give-up"
                @click="giveUp">GIVE UP</button>
    </div>
</section>
```
As you can see in the code above, we’ve attached click events to all the buttons with some functions attached to them like ‘startGame’, ‘attack’ which are still to be created.

So, let’s start creating functions. To start creating functions, we’ll add methods object in app.js file.

#### app.js
```
methods: {
    //add functions here
}
```

Now, let’s create startGame function.

#### app.js
```
methods: {
    startGame: function () {
        this.gameIsRunning = true;
        this.playerHealth = 100;
        this.monsterHealth = 100;
        this.turns = []
    }
}
```
This function is applied on “START NEW GAME” button. So, firstly this button sets the state of game to running, resets player and monster health to 100 (in case the game was running) and resets the turns. 

Save your files, refresh the page again and press the “START NEW GAME” button. You’ll notice that the section with attack buttons shows up. GOOD WORK!


![Image](/images/MS-5.png)

Before, we move on to create functions to attack we’ll create two more functions that we’ll use in other functions.

First one is to calculate the damage.

#### app.js
```
calculateDamage: function (min, max) {
   return Math.random();
}
```
In this function, we use random number generator to generate a random number. As random number generator, generates number between 0 and 1, excluding 1. We’re creating this method such that the number generated is between min and max which are values that we’ll provide later. So, we’ll multiply the number generated with the ‘max’ and also add 1 to include the max number.

As of now the number that we generated is something like ‘5.55555’, so we’ll use floor function to get an integer.
```
calculateDamage: function (min, max) {
   return Math.floor(Math.random() * max + 1);
}
```
Now we’ll use the Math.max function which will either select the values that is in between the max and min values that we’ll set.
```
calculateDamage: function (min, max) {
   return Math.max(Math.floor(Math.random() * max + 1), min);
}
```
Now, we’ll create the checkWin function that will check who win after each attack.
```
checkWin: function () {
    if (this.monsterHealth <= 0) {
        if (confirm('You Won! New Game?')) {
            this.startGame();
        } else {
            this.gameIsRunning = false;
        }
        return true;
    } else if (this.playerHealth <= 0) {
        if (confirm('You Lost! New Game?')) {
            this.startGame();
        } else {
            this.gameIsRunning = false;
        }
        return true;
    }
    return false;
}
```
Here, we use if else statements to check the winner. If the monster health becomes 0, this shows a message of winning and a confirmation if you want to start a new game. Similarly, it checks the monster health and returns a lose message and a confirmation if you want to play again. 
// explain propel afterwards

Before we begin with attack function, let’s create monsterAttack function because with every click of the user, monster will also deal some damage to the user.
```
monsterAttack: function() {
    var damage = this.calculateDamage(5, 12);
    this.playerHealth -= damage;
    this.checkWin();
    this.turns.unshift({
             isPlayer: false,
             text: 'Monster hits Player by ' + damage
    });
},
```
We make a function named monsterAttack to which deals damage to the player. First of all, we use the calculateDamage function that we created earlier in this tutorial and use it here to calculate damage randomly by providing argument values of min(5) and max(12) and store it in a variable. Then we deduct the damage from the player’s health. 

Also, we use the checkWin function here that checks if the monster wins or not. At the very end, we use turns to log the actions and display them. We have “turns.unshift” which moves the turns a step down and adds one on the to the turns. In this, we have isPlayer property to make sure if its the player or the monster. After that, there is text that we’ll display in the log area with the damage that the monster has dealt to the player.

```
Note: We have stored the value of calculateDamage function in the variable named damage to make sure we use the same value while attacking and logging. If we use the calculateDamage function everywhere, it’ll generate random values everytime and our data won’t match.    
```
Now let’s begin with attack function to attack the monster and deal damage.
```
attack: function () {
    var damage = this.calculateDamage(3, 10);
    this.turns.unshift({
             isPlayer: true,
             text: 'Player hits Monster by ' + damage
    });
    this.monsterHealth -= damage;
    if (this.checkWin()) {
             return;
    }
    this.monsterAttack();
},
```
As we have created the monsterattack function, in a similar way we will create this function with few modifications. Here we will deal damage to the monster and log the player turn. Also, we’ll run the monsterAttack function here as we’re the one clicking the buttons.

![Image](/images/MS-4.png)

```
specialAttack: function () {
           var damage = this.calculateDamage(7, 15);
           this.monsterHealth -= damage;
           this.turns.unshift({
               isPlayer: true,
               text: 'Player hits Monster hard by ' + damage
           });
           if (this.checkWin()) {
               return;
           }
           this.monsterAttack();  
       },
```

![Image](/images/MS-3.png)

This function is also similar to attack function but we have made this a special attack by increasing the damage that we’ll deal to the monster and modifies the lof text to display “hits hard” instead of “hard” in attack fucntion.
```
heal: function () {
           if (this.playerHealth < 90) {
               this.playerHealth += 10;
           }
           else {
               this.playerHealth = 100;
           }
           this.turns.unshift({
               isPlayer: true,
               text: 'Player heals by 10'
           });
          
           this.monsterAttack();
       },
```

![Image](/images/MS-2.png)

Now let,s create the heal function. As it is clear from the name that this function will heal the user i.e. will add to user’s health bar. we have selected a constant value of 10 to heal. We’ll execute this statement in “if” statement to make sure that the value of playerHealth doesn’t increase more than 100. And we’ll execute the monsterAttack as the monster will continue to attack us even when we’re healing.
```
giveUp: function () {
           this.gameIsRunning = false;
       },
```

![Image](/images/MS-1.png)

We should never give up in life. But in case you decide to give up, this function will help you in doing so. In this function, we just set the gameIsRunning to false and it stops the game.
