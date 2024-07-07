/ Create a new Phaser game instance
const game = new Phaser.Game({
  type: Phaser.CANVAS,
  parent: 'game-container',
  width: 400,
  height: 600,
  scene: {
    preload: preload,
    create: create,
    update: update
  }
});

// Preload assets
function preload() {
  this.load.image('bird', 'assets/bird.png');
  this.load.image('pipe', 'assets/pipe.png');
  this.load.image('ground', 'assets/ground.png');
}

// Create game objects
function create() {
  // Create the bird
  this.bird = this.add.sprite(100, 250, 'bird');
  this.bird.setScale(2);
  this.bird.body = this.physics.add.body(this.bird);
  this.bird.body.gravity.y = 1000;

  // Create the pipes
  this.pipes = this.add.group();
  this.pipeTimer = this.time.addEvent({
    delay: 1500,
    callback: () => {
      const pipe = this.pipes.create(400, Phaser.Math.Between(100, 500), 'pipe');
      pipe.setScale(2);
      pipe.body = this.physics.add.body(pipe);
      pipe.body.velocity.x = -200;
    },
    loop: true
  });

  // Create the ground
  this.ground = this.add.sprite(0, 550, 'ground');
  this.ground.setScale(2);
  this.ground.body = this.physics.add.body(this.ground);
  this.ground.body.immovable = true;

  // Add collision detection
  this.physics.add.collider(this.bird, this.pipes, () => {
    this.gameOver();
  });
  this.physics.add.collider(this.bird, this.ground, () => {
    this.gameOver();
  });
}

// Update game logic
function update(time, delta) {
  // Update bird movement
  if (this.input.keyboard.down(Phaser.Input.Keyboard.SPACE)) {
    this.bird.body.velocity.y = -300;
  }

  // Update pipe movement
  this.pipes.getChildren().forEach(pipe => {
    pipe.x -= 2;
    if (pipe.x < -100) {
      pipe.destroy();
    }
  });
}

// Game over function
function gameOver() {
  this.bird.body.velocity.y = 0;
  this.pipes.getChildren().forEach(pipe => {
    pipe.body.velocity.x = 0;
  });
  this.add.text(150, 250, 'Game Over!', { fontSize: 36, fill: '#fff' });
}
/ Create a new Phaser game instance
const game = new Phaser.Game({
  type: Phaser.CANVAS,
  parent: 'game-container',
  width: 400,
  height: 600,
  scene: {
    preload: preload,
    create: create,
    update: update
  }
});

// Preload assets
function preload() {
  this.load.image('bird', 'assets/bird.png');
  this.load.image('pipe', 'assets/pipe.png');
  this.load.image('ground', 'assets/ground.png');
}

// Create game objects
function create() {
  // Create the bird
  this.bird = this.add.sprite(100, 250, 'bird');
  this.bird.setScale(2);
  this.bird.body = this.physics.add.body(this.bird);
  this.bird.body.gravity.y = 1000;

  // Create the pipes
  this.pipes = this.add.group();
  this.pipeTimer = this.time.addEvent({
    delay: 1500,
    callback: () => {
      const pipe = this.pipes.create(400, Phaser.Math.Between(100, 500), 'pipe');
      pipe.setScale(2);
      pipe.body = this.physics.add.body(pipe);
      pipe.body.velocity.x = -200;
    },
    loop: true
  });

  // Create the ground
  this.ground = this.add.sprite(0, 550, 'ground');
  this.ground.setScale(2);
  this.ground.body = this.physics.add.body(this.ground);
  this.ground.body.immovable = true;

  // Add collision detection
  this.physics.add.collider(this.bird, this.pipes, () => {
    this.gameOver();
  });
  this.physics.add.collider(this.bird, this.ground, () => {
    this.gameOver();
  });
}

// Update game logic
function update(time, delta) {
  // Update bird movement
  if (this.input.keyboard.down(Phaser.Input.Keyboard.SPACE)) {
    this.bird.body.velocity.y = -300;
  }

  // Update pipe movement
  this.pipes.getChildren().forEach(pipe => {
    pipe.x -= 2;
    if (pipe.x < -100) {
      pipe.destroy();
    }
  });
}

// Game over function
function gameOver() {
  this.bird.body.velocity.y = 0;
  this.pipes.getChildren().forEach(pipe => {
    pipe.body.velocity.x = 0;
  });
  this.add.text(150, 250, 'Game Over!', { fontSize: 36, fill: '#fff' });
}
