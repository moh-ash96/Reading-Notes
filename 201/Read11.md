# Images
Images can be added to the webpage as a *foreground* or *background images*, for the foreground images, we can add them to the HTML using the **< img >** tag and add the relative link of the image to the ***src*** attribute.
We can control the size of the image in CSS using the width property and we can put the width as a size or percentage. 
To align an image, we can use text align in the section that the image is inside using text-align, or by controlling the margins of the image itself, e.g. we can center the image by making the left and right margins as *auto*.
## Background images 
We can add an image as a background to the whole page or to a section in the page using the background-image: url (  the link of the image will be here ); as a default in CSS the background will repeat to fill the whole section, but that can be controlled using the background-repeat as follows:
* Repeat, it will repeat to fit the whole page.
* Repeat-x, it will repeat only vertically.
* Repeat-y, it will repeat horizontally.
* No-repeat, it will not repeat.
* Fixed, it will stay at its position on the page.
* Scroll, it will move up and down when the user scrolls.
## Background position
Background-position property can be used when the background image is set on no-repeat and it has nine values:
1. Left top
2. Left center
3. Left bottom
4. Center top
5. Center center
6. Center bottom
7. Right top
8. Right center
9. Right bottom

# Practical information 
## Search engine optimization
Search engine optimization is a way that allows you to have more opportunity to appear in search engines when a relevant search is in progress,
There are two types of techniques for that purpose:
1. On-page technique, which is all about keywords.
2. Off-page technique, which is adding you links in external websites.
### On-page technique:
It is all about key words and how relevant to what people usually search and the repeat of them, and there are seven key places that keywords can be added to on the webpage
1. Page title.
2. URL/web address.
3. Headings.
4. Text.
5. Link text.
6. Image alt text.
7. Page description.
 #### How to identify keywords
* Brainstorm.
* Organize.
* Research.
* Compare.
* Refine.
* Map.
#### Learning about your visitors:
You can track for who visited your webpage by suing google analytics, which is a free service that can be used by signing in to google account and getting a tracking code that will be added to the head of the HTML page.
Google analytics gives you a lot of information about your visitors including:
* How many people are coming to your site?
* What are your visitors looking at?
* Where are your visitors coming from?
#### Domain name and hosting
In order to put your site on the web, you need a domain name and web hosting.
* Domain name, which is the website address that the users will use to get into your website.
* Web hosting, uploading your website to a web server, while web servers are special computers that are connected constantly to the internet.
In order to transfer your code and images to the computer of the hosting company, is to use something known as the File Transfer Protocol (FTP).

## Video and audio APIs
We have for videos an HTML structure, CSS style and JS functions.
HTML structure consists of < div > that has the whole player, < video > element that has two < source > elements to have two formats to work with any kind of browsers, and four < button >s – play/pause, stop, rewind, and fast forward.
Each button has class name, data-icon attribute for the icon as “p” for play, “S” for stop, “B” for rewind, and “F” for forward, and aria-label attribute to provide readable description of the button. 
And also another < div > and < span > elements for the timer.
We use the CSS to style the controls as in visibility, icons and opacity and also the timer position.
For JS we start in assigning ( const )s for video, controls, paly, stop, rwd, fwd, timerwrapper, timer span, and timer bar ( timer div ).
Then we should remove the browser’s default controls from the video and make the custome controls visible using: 
<pre><code>media.removeAttribute(‘controls’);
Controls.style.visibility = ‘visible’;</code></pre>
* Playing, and Pausing the video
We make a function called playPauseMedia(), and add an event listener at the bottom of the code, the function has an if statement to check whether the video is paused, the HTMLMediaElement.paused will return true if the media is paused, which is any time the media is not playing, even when the media has not been started yet. So if it Is paused we set the data-icon on the play button as “u” which refers to pause, and invoke the HTMLMediaElement.paly() method to play the media.
On the second click the play icon will be shown again and the video will be paused with HTMLMediaElement.pause().
* Stopping the video
We add a function that will return the video into the value of ‘0’ in seconds when the stop button is pressed or the video has ended and also add an event listener.
* Fast forward and the reward functions, and we add event listener to them.

* Updating the elapsed time, it is the last step and emplements the time elapsed displays.
The whole code will be the following:
<pre><code>function playPauseMedia() {
  if(media.paused) {
    play.setAttribute('data-icon','u');
    media.play();
  } else {
    play.setAttribute('data-icon','P');
    media.pause();
  }
}
function stopMedia() {
  media.pause();
  media.currentTime = 0;
  play.setAttribute('data-icon','P');
}
let intervalFwd;
let intervalRwd;

function mediaBackward() {
  clearInterval(intervalFwd);
  fwd.classList.remove('active');

  if(rwd.classList.contains('active')) {
    rwd.classList.remove('active');
    clearInterval(intervalRwd);
    media.play();
  } else {
    rwd.classList.add('active');
    media.pause();
    intervalRwd = setInterval(windBackward, 200);
  }
}

function mediaForward() {
  clearInterval(intervalRwd);
  rwd.classList.remove('active');

  if(fwd.classList.contains('active')) {
    fwd.classList.remove('active');
    clearInterval(intervalFwd);
    media.play();
  } else {
    fwd.classList.add('active');
    media.pause();
    intervalFwd = setInterval(windForward, 200);
  }
}
function windBackward() {
  if(media.currentTime <= 3) {
    rwd.classList.remove('active');
    clearInterval(intervalRwd);
    stopMedia();
  } else {
    media.currentTime -= 3;
  }
}

function windForward() {
  if(media.currentTime >= media.duration - 3) {
    fwd.classList.remove('active');
    clearInterval(intervalFwd);
    stopMedia();
  } else {
    media.currentTime += 3;
  }
}
function setTime() {
  let minutes = Math.floor(media.currentTime / 60);
  let seconds = Math.floor(media.currentTime - minutes * 60);
  let minuteValue;
  let secondValue;

  if (minutes < 10) {
    minuteValue = '0' + minutes;
  } else {
    minuteValue = minutes;
  }

  if (seconds < 10) {
    secondValue = '0' + seconds;
  } else {
    secondValue = seconds;
  }

  let mediaTime = minuteValue + ':' + secondValue;
  timer.textContent = mediaTime;

  let barLength = timerWrapper.clientWidth * (media.currentTime/media.duration);
  timerBar.style.width = barLength + 'px';
}
Play.addEventListener(‘click’, playPauseMedia);
stop.addEventListener('click', stopMedia);
media.addEventListener('ended', stopMedia);
rwd.addEventListener('click', mediaBackward);
fwd.addEventListener('click', mediaForward);
media.addEventListener('timeupdate', setTime);</code></pre>
Finally there is a problem will face us when pressing play/pause when the fwd, or rwd buttons are active, that will lead to an error, so we need to disable these buttons using:
<pre><code>rwd.classList.remove(‘active’);
fwd.classList.remove(‘active’);
clearInterval(intervalRwd);
clearInterval(intervalFwd);</code></pre>
