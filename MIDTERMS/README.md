## ok, cool! i think that midterm wasn't too bad after all! 
### [midterm link here](https://editor.p5js.org/lilithmode/full/hjE0nFSZn)

## but let's break it down first. i think there was already a lot to handle but if there's one thing i took away from this whole ordeal, i'm very grateful for the codealongs and everything that was included in such. i surprisingly enjoyed the optimization a lot!

`let sound1, sound2, sound3; 

function preload() {
  sound1 = loadSound('Kick (mushi).wav');
  sound2 = loadSound('Snare (blapish2).wav');
  sound3 = loadSound('Go To Pierre Chant.wav');
}

function setup() {
  createCanvas(400, 200);
  background(50);
  fill(255);
  textAlign(CENTER, CENTER);
  textSize(18);
  text("Click on me and press a, s, or d to play sounds!", width / 2, height / 2);
}

function keyPressed() {
  console.log("Key pressed:", key);
  if (key === 'a') {
    console.log("kick!");
    sound1.stop();
    sound1.play();
  } else if (key === 's') {
    console.log("snare!");
    sound2.stop();
    sound2.play();
  } else if (key === 'd') {
    console.log("unh!");
    sound3.stop();
    sound3.play();
  } else {
    console.log("sorry, I got lazy [no sound]")
  }
}

`

### alright here's the code. as you can notice already i made a couple of adjustments to how i had wanted the code to be perceived. i wrote everything down in a notebook before i did anything, using the boolean logic and whatnot (half joking when i say this)

### one of the biggest things that i had run into was purely thinking about how i could make the code be concise within just a couple of lines. sure i could've probably just, copied pasted the code but i had to get deeper than that. 

#### being able to define the sounds at the beginning immidiately made thing easier, as i could've just used the preload function and nestled everything into one nice little lump. 

### then came the console logs! i just used the code along to put two and two together, and added the logs to each else if function in the keyPressed section. I wanted to have a little fun with it, so with some common sense i ended up just putting things in there. i wonder if i can make this even more efficent...

### coding is fun! - lilith