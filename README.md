# text-reader
# 1- Step
## Html
```
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Speech Text Reader</title>
  <link rel="stylesheet" href="style.css">
</head>

<body>
  <div class="container">
    <h1>Speech Text Reader</h1>
    <button id="toggle-btn">Toggle Text Box</button><br>
        <!-- Modal -->
        <div id="myModal" class="modal">
          <div class="modal-content">
              <span class="close" id="closeModal">&times;</span>
              <textarea id="text-input" placeholder="Enter text to read ..."></textarea>
              <br>
              <button id="start-btn">Read Text</button>
          </div>
      </div>
    <div id="output">
      <div class="image" data-text="I'm Thirsty">
        <img
          src="https://github.com/bradtraversy/vanillawebprojects/blob/master/speech-text-reader/img/drink.jpg?raw=true"
          alt="img">
        <p>I'm Thirsty</p>
      </div>
      <div class="image" data-text="I'm Hungry">
        <img
          src="https://github.com/bradtraversy/vanillawebprojects/blob/master/speech-text-reader/img/food.jpg?raw=true"
          alt="img">
        <p>I'm Hungry</p>
      </div>
      <div class="image" data-text="I'm Tired">
        <img
          src="https://github.com/bradtraversy/vanillawebprojects/blob/master/speech-text-reader/img/tired.jpg?raw=true"
          alt="img">
        <p>I'm Tired</p>
      </div>
      <div class="image" data-text="I'm Hurt">
        <img
          src="https://github.com/bradtraversy/vanillawebprojects/blob/master/speech-text-reader/img/hurt.jpg?raw=true"
          alt="img">
        <p>I'm Hurt</p>
      </div>
      <div class="image" data-text="I'm Happy">
        <img
          src="https://github.com/bradtraversy/vanillawebprojects/blob/master/speech-text-reader/img/happy.jpg?raw=true"
          alt="img">
        <p>I'm Happy</p>
      </div>
      <div class="image" data-text="I'm Angry">
        <img
          src="https://github.com/bradtraversy/vanillawebprojects/blob/master/speech-text-reader/img/angry.jpg?raw=true"
          alt="img">
        <p>I'm Angry</p>
      </div>
      <div class="image" data-text="I'm Sad">
        <img
          src="https://github.com/bradtraversy/vanillawebprojects/blob/master/speech-text-reader/img/sad.jpg?raw=true"
          alt="img">
        <p>I'm Sad</p>
      </div>
      <div class="image" data-text="I'm Scared">
        <img
          src="https://github.com/bradtraversy/vanillawebprojects/blob/master/speech-text-reader/img/scared.jpg?raw=true"
          alt="img">
        <p>I'm Scared</p>
      </div>
      <div class="image" data-text="I wanna go to School">
        <img
          src="https://github.com/bradtraversy/vanillawebprojects/blob/master/speech-text-reader/img/school.jpg?raw=true"
          alt="img">
        <p>I wanna go to School</p>
      </div>
    </div>
  </div>
  <script src="index.js"></script>
</body>

</html>
```
# 2 Step
## Js
```
const textInput = document.getElementById('text-input');
const toggleBtn = document.getElementById('toggle-btn');
const startBtn = document.getElementById('start-btn');
const output = document.getElementById('output');
const synth = window.speechSynthesis;
let speaking = false;

const modal = document.getElementById('myModal');
const closeModalBtn = document.getElementById('closeModal');

toggleBtn.addEventListener('click', () => {
  modal.style.display = 'block';
});

closeModalBtn.addEventListener('click', () => {
  modal.style.display = 'none';
});

startBtn.addEventListener('click', () => {
  if (!speaking) {
    const text = textInput.value;
    if (text) {
      const utterance = new SpeechSynthesisUtterance(text);
      synth.speak(utterance);
      speaking = true;
      utterance.onend = () => {
        speaking = false;
      };
    }
  }
});

const imageContainers = document.querySelectorAll('.image');

imageContainers.forEach((container) => {
  container.addEventListener('click', () => {
    const textToRead = container.getAttribute('data-text');
    if (textToRead) {
      const utterance = new SpeechSynthesisUtterance(textToRead);
      synth.speak(utterance);
    }
  });
});
```
# 3-Step
## CSS
```
body {
    font-family: Arial, sans-serif;
    background-color: #F4F4FB;
  }
  
  .container {
    text-align: center;
    padding: 20px;
  }
  
  h1 {
    color: #333;
  }
  #start-btn {
    margin-top: 1em;
  }
  
  textarea {
    width: 90%;
    height: 150px;
    margin: 1em 0 0 0;
    padding: 10px;
    /* margin-bottom: -1em; */
  }
  /* Modal */
  .modal {
    display: none;
    position: fixed;
    z-index: 1;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    border-radius: 30px;
    overflow: auto;
    background-color: rgba(0,0,0,0.7);
  }
  
  .modal-content {
    background-color: #fefefe;
    margin: 15% auto;
    padding: 20px;
    border: 1px solid #888;
    width: 50%;
    box-shadow: 0px 0px 15px rgba(0, 0, 0, 0.2);
  }
  .close {
    color: #aaa;
    float: right;
    font-size: 28px;
    font-weight: bold;
    cursor: pointer;
  }
  
  .close:hover,
  .close:focus {
    color: black;
    text-decoration: none;
    cursor: pointer;
  }
  
  button {
    background-color: rgb(84, 79, 116);
    color: white;
    border: 0;
    border-radius: 10px;
    font-size: 1rem;
    font-family: inherit;
    font-weight: bold;
    padding: 0.75rem 2rem;
    cursor: pointer;
  }
  
  #output {
    margin-top: 20px;
    font-size: 18px;
    width: 100%;
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
  }
  
  .image {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
  
  .image img {
    border-radius: 10px;
    height: 250px;
    width: 300px;
    margin: 1em;
    margin-bottom: 0;
    cursor: pointer;
  }
  .centered-element {
    margin: 0 auto;
    display: block;
    margin-top: 1.5em;
  }
  .image p {
    background-color: rgb(84, 79, 116);
    color: white;
    margin-top: -0.3em;
    width: 283px;
    border-radius: 0 0 10px 10px;
    padding: 0.5em;
    cursor: pointer;
  }
```
