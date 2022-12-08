---
layout: template
title: works.md
permalink: /works
filename: works.md
---

<link rel="stylesheet" href="./faq/style.css">

<script> 
        'use strict';

var _createClass = function () { function defineProperties(target, props) { for (var i = 0; i < props.length; i++) { var descriptor = props[i]; descriptor.enumerable = descriptor.enumerable || false; descriptor.configurable = true; if ("value" in descriptor) descriptor.writable = true; Object.defineProperty(target, descriptor.key, descriptor); } } return function (Constructor, protoProps, staticProps) { if (protoProps) defineProperties(Constructor.prototype, protoProps); if (staticProps) defineProperties(Constructor, staticProps); return Constructor; }; }();

function _classCallCheck(instance, Constructor) { if (!(instance instanceof Constructor)) { throw new TypeError("Cannot call a class as a function"); } }

var Balls = function () {
  function Balls(context, buffer) {
    _classCallCheck(this, Balls);

    this.context = context;
    this.buffer = buffer;
  }

  _createClass(Balls, [{
    key: 'setup',
    value: function setup() {
      this.gainNode = this.context.createGain();
      this.source = this.context.createBufferSource();
      this.source.buffer = this.buffer;
      this.source.connect(this.gainNode);
      this.gainNode.connect(this.context.destination);
      this.gainNode.gain.setValueAtTime(1, this.context.currentTime);
    }
  }, {
    key: 'play',
    value: function play() {
      this.setup();
      this.source.start(this.context.currentTime);
    }
  }, {
    key: 'stop',
    value: function stop() {
      var ct = this.context.currentTime + 1;
      this.gainNode.gain.exponentialRampToValueAtTime(.1, ct);
      this.source.stop(ct);
    }
  }]);

  return Balls;
}();

var Buffer = function () {
  function Buffer(context, urls) {
    _classCallCheck(this, Buffer);

    this.context = context;
    this.urls = urls;
    this.buffer = [];
  }

  _createClass(Buffer, [{
    key: 'loadSound',
    value: function loadSound(url, index) {
      var request = new XMLHttpRequest();
      request.open('get', url, true);
      request.responseType = 'arraybuffer';
      var thisBuffer = this;
      request.onload = function () {
        thisBuffer.context.decodeAudioData(request.response, function (buffer) {
          thisBuffer.buffer[index] = buffer;
          if (index == thisBuffer.urls.length - 1) {
            thisBuffer.loaded();
          }
        });
      };
      request.send();
    }
  }, {
    key: 'getBuffer',
    value: function getBuffer() {
      var _this = this;

      this.urls.forEach(function (url, index) {
        _this.loadSound(url, index);
      });
    }
  }, {
    key: 'loaded',
    value: function loaded() {
      _loaded = true;
    }
  }, {
    key: 'getSound',
    value: function getSound(index) {
      return this.buffer[index];
    }
  }]);

  return Buffer;
}();

var balls = null,
    preset = 0,
    _loaded = false;
var path = 'catalog/view/theme/skylight/stylesheet/hnw/audio/';
var sounds = [path + 'sound1.mp3', path + 'sound2.mp3', path + 'sound3.mp3', path + 'sound4.mp3', path + 'sound5.mp3', path + 'sound6.mp3', path + 'sound7.mp3', path + 'sound8.mp3', path + 'sound9.mp3', path + 'sound10.mp3', path + 'sound11.mp3', path + 'sound12.mp3', path + 'sound13.mp3', path + 'sound14.mp3', path + 'sound15.mp3', path + 'sound16.mp3', path + 'sound17.mp3', path + 'sound18.mp3', path + 'sound19.mp3', path + 'sound20.mp3', path + 'sound21.mp3', path + 'sound22.mp3', path + 'sound23.mp3', path + 'sound24.mp3', path + 'sound25.mp3', path + 'sound26.mp3', path + 'sound27.mp3', path + 'sound28.mp3', path + 'sound29.mp3', path + 'sound30.mp3', path + 'sound31.mp3', path + 'sound32.mp3', path + 'sound33.mp3', path + 'sound34.mp3', path + 'sound35.mp3', path + 'sound36.mp3'];
var context = new (window.AudioContext || window.webkitAudioContext)();

function playBalls() {
  var index = parseInt(this.dataset.note) + preset;
  balls = new Balls(context, buffer.getSound(index));
  balls.play();
}

function stopBalls() {
  balls.stop();
}

var buffer = new Buffer(context, sounds);
var ballsSound = buffer.getBuffer();
var buttons = document.querySelectorAll('.b-ball_bounce');
buttons.forEach(function (button) {
  button.addEventListener('mouseenter', playBalls.bind(button));
  button.addEventListener('mouseleave', stopBalls);
});

function ballBounce(e) {
  var i = e;
  if (e.className.indexOf(" bounce") > -1) {
    return;
  }
  toggleBounce(i);
}

function toggleBounce(i) {
  i.classList.add("bounce");
  function n() {
    i.classList.remove("bounce");
    i.classList.add("bounce1");
    function o() {
      i.classList.remove("bounce1");
      i.classList.add("bounce2");
      function p() {
        i.classList.remove("bounce2");
        i.classList.add("bounce3");
        function q() {
          i.classList.remove("bounce3");
        }
        setTimeout(q, 300);
      }
      setTimeout(p, 300);
    }
    setTimeout(o, 300);
  }
  setTimeout(n, 300);
}

var array1 = document.querySelectorAll('.b-ball_bounce');
var array2 = document.querySelectorAll('.b-ball_bounce .b-ball__right');

for (var i = 0; i < array1.length; i++) {
  array1[i].addEventListener('mouseenter', function () {
    ballBounce(this);
  });
}

for (var i = 0; i < array2.length; i++) {
  array2[i].addEventListener('mouseenter', function () {
    ballBounce(this);
  });
}

var l = ["49", "50", "51", "52", "53", "54", "55", "56", "57", "48", "189", "187", "81", "87", "69", "82", "84", "89", "85", "73", "79", "80", "219", "221", "65", "83", "68", "70", "71", "72", "74", "75", "76", "186", "222", "220"];
var k = ["90", "88", "67", "86", "66", "78", "77", "188", "190", "191"];
var a = {};
for (var e = 0, c = l.length; e < c; e++) {
  a[l[e]] = e;
}
for (var _e = 0, _c = k.length; _e < _c; _e++) {
  a[k[_e]] = _e;
}

document.addEventListener('keydown', function (j) {
  var i = j.target;
  if (j.which in a) {
    var index = parseInt(a[j.which]);
    balls = new Balls(context, buffer.getSound(index));
    balls.play();
    var ball = document.querySelector('[data-note="' + index + '"]');
    toggleBounce(ball);
  }
});
</script>


<!-- новогодняя мотня 2.1 -->
<div class="b-page_newyear">
    <div class="b-page__content">
        <i class="b-head-decor">
      <i class="b-head-decor__inner b-head-decor__inner_n1">
        <div class="b-ball b-ball_n1 b-ball_bounce" data-note="0"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n2 b-ball_bounce" data-note="1"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n3 b-ball_bounce" data-note="2"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n4 b-ball_bounce" data-note="3"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n5 b-ball_bounce" data-note="4"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n6 b-ball_bounce" data-note="5"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n7 b-ball_bounce" data-note="6"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n8 b-ball_bounce" data-note="7"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n9 b-ball_bounce" data-note="8"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i1"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i2"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i3"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i4"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i5"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i6"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        </i>
            <i class="b-head-decor__inner b-head-decor__inner_n2">
        <div class="b-ball b-ball_n1 b-ball_bounce" data-note="9"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n2 b-ball_bounce" data-note="10"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n3 b-ball_bounce" data-note="11"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n4 b-ball_bounce" data-note="12"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n5 b-ball_bounce" data-note="13"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n6 b-ball_bounce" data-note="14"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n7 b-ball_bounce" data-note="15"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n8 b-ball_bounce" data-note="16"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n9 b-ball_bounce" data-note="17"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i1"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i2"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i3"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i4"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i5"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i6"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
      </i>
            <i class="b-head-decor__inner b-head-decor__inner_n3">
        <div class="b-ball b-ball_n1 b-ball_bounce" data-note="18"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n2 b-ball_bounce" data-note="19"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n3 b-ball_bounce" data-note="20"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n4 b-ball_bounce" data-note="21"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n5 b-ball_bounce" data-note="22"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n6 b-ball_bounce" data-note="23"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n7 b-ball_bounce" data-note="24"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n8 b-ball_bounce" data-note="25"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n9 b-ball_bounce" data-note="26"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i1"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i2"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i3"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i4"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i5"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i6"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
      </i>
            <i class="b-head-decor__inner b-head-decor__inner_n4">
        <div class="b-ball b-ball_n1 b-ball_bounce" data-note="27"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n2 b-ball_bounce" data-note="28"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n3 b-ball_bounce" data-note="29"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n4 b-ball_bounce" data-note="30"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n5 b-ball_bounce" data-note="31"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n6 b-ball_bounce" data-note="32"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n7 b-ball_bounce" data-note="33"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n8 b-ball_bounce" data-note="34"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n9 b-ball_bounce" data-note="35"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i1"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i2"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i3"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i4"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i5"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i6"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
      </i>
            <i class="b-head-decor__inner b-head-decor__inner_n5">
        <div class="b-ball b-ball_n1 b-ball_bounce" data-note="0"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n2 b-ball_bounce" data-note="1"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n3 b-ball_bounce" data-note="2"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n4 b-ball_bounce" data-note="3"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n5 b-ball_bounce" data-note="4"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n6 b-ball_bounce" data-note="5"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n7 b-ball_bounce" data-note="6"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n8 b-ball_bounce" data-note="7"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n9 b-ball_bounce" data-note="8"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i1"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i2"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i3"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i4"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i5"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i6"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
      </i>
            <i class="b-head-decor__inner b-head-decor__inner_n6">
        <div class="b-ball b-ball_n1 b-ball_bounce" data-note="9"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n2 b-ball_bounce" data-note="10"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n3 b-ball_bounce" data-note="11"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n4 b-ball_bounce" data-note="12"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n5 b-ball_bounce" data-note="13"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n6 b-ball_bounce" data-note="14"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n7 b-ball_bounce" data-note="15"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n8 b-ball_bounce" data-note="16"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n9 b-ball_bounce" data-note="17"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i1"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i2"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i3"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i4"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i5"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i6"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
      </i>
            <i class="b-head-decor__inner b-head-decor__inner_n7">
        <div class="b-ball b-ball_n1 b-ball_bounce" data-note="18"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n2 b-ball_bounce" data-note="19"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n3 b-ball_bounce" data-note="20"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n4 b-ball_bounce" data-note="21"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n5 b-ball_bounce" data-note="22"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n6 b-ball_bounce" data-note="23"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n7 b-ball_bounce" data-note="24"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n8 b-ball_bounce" data-note="25"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_n9 b-ball_bounce" data-note="26"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i1"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i2"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i3"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i4"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i5"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
        <div class="b-ball b-ball_i6"><div class="b-ball__right"></div><div class="b-ball__i"></div></div>
      </i>
        </i>
    </div>
</div>




# WORKS & TASKS

## Works


| Название |[021а][021a]|[021б][021b]| [031а][031a] | [031б][031b] | [041б][041b] | [051б][051b] | [122а][122a] | [122б][122b] | [132б][132b] |[142а][142a]| [142б][142b] | 152аб |
| :---     |:---: | :--: |:--:  | :--:     | :--:     | :--:     | :--:     | :--:     | :--:     | :--:   | :--:     | :--:      |
| ВК       |      |      |      |      |      |      |      |      |      |    |      |       |
| CC xls | |  |||  |  |  ||  ||  ||
| CC py | |  |||  |  |  ||  ||  ||
| Морзе xls | |  |||  |  |  ||  ||  ||
| Морзе py | |  |||  |  |  ||  ||  ||
| Хэмминг | |  |||  |  |  ||  ||  ||
| GH+markdown | |  |||  |  |  ||  ||  ||
| GH Сайт | |  |||  |  |  ||  ||  ||
| SQL DB | |  |||  |  |  ||  ||  ||
| Консп.СА | |  |||  |  |  ||  ||  ||
| Консп.SQL | |  |||  |  |  ||  ||  ||
| Консп.Кодир.Инф. | |  |||  |  |  ||  ||  ||
| Wordpress | |  |||  |  |  ||  ||  ||
| Miro/Lucid | |  |||  |  |  ||  ||  ||
| Genilly | |  |||  |  |  ||  ||  ||
| Логика xls | |  |||  |  |  ||  ||  ||
| Логика py | |  |||  |  |  ||  ||  ||
| Latex логика | |  |||  |  |  ||  ||  ||
| Latex формулы | |  |||  |  |  ||  ||  ||
| УРЗ | |  |||  |  |  ||  ||  ||
| Слайдшоу | |  |||  |  |  ||  ||  ||
| Викторина | |  |||  |  |  ||  ||  ||
| Генератор имен | |  |||  |  |  ||  ||  ||
| Чемпионат | |  |||  |  |  ||  ||  ||
| ЕГЭ викт.+TAB | |  |||  |  |  ||  ||  ||
| Inkscape рис. | |  |||  |  |  ||  ||  ||
| MidJourney | |  |||  |  |  ||  ||  ||
| Кнопка+codepen | |  |||  |  |  ||  ||  ||
| mermaid в GH | |  |||  |  |  ||  ||  ||
| Flask | |  |||  |  |  ||  ||  ||
| Самостоят. | |  |||  |  |  ||  ||  ||
| С | Н | О |В|Ы|М  |  |Г  |О|Д  |О| М ||
| Квест | |  |||  |  |  ||  ||  ||
|py в Minecraft| |  |||  |  |  ||  ||  ||
|3d modelling| |  |||  |  |  ||  ||  ||

------


<a class="iksweb" href="https://hackertyper.net/#" target="_blank"  title="{coder==True}">{coder==True}</a>

---------------------------

## Tasks



[122a]: <http://89234422454.ru/wp-content/uploads/2022/11/122a.html>
[122b]:<http://89234422454.ru/wp-content/uploads/2022/11/122b.html>
[132b]:<http://89234422454.ru/wp-content/uploads/2022/11/132b.html>
[142a]:<http://89234422454.ru/wp-content/uploads/2022/11/142a.html>
[142b]:<http://89234422454.ru/wp-content/uploads/2022/11/142b.html>
[021a]:<http://89234422454.ru/wp-content/uploads/2022/11/021a.html>
[021b]:<http://89234422454.ru/wp-content/uploads/2022/11/021b.html>
[031a]:<http://89234422454.ru/wp-content/uploads/2022/11/031a.html>
[031b]:<http://89234422454.ru/wp-content/uploads/2022/11/031b.html>
[041b]:<http://89234422454.ru/wp-content/uploads/2022/11/041b.html>
[051b]:<http://89234422454.ru/wp-content/uploads/2022/11/051b.html>

### 122

| ИМЯ | SITE| УРЗ | PyVIDEO  |
| :---|:---:| :--:|:--:|
|[1. Бакеев Тимур][12211] | [![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://grad154.github.io)|  |  |
|[2. Балаганский Дмитрий][12212] |[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://Dimakek2.github.io) | | |
|[3. Вайс Максим Константинович][12213] |[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://weissok.github.io)|||
|[4. Воронин Вячеслав][12214] |[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://VoroninVaycheslav.github.io)|||
|[5. Давыдов Никита Алексеевич][12215] |[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://NikitaDavydov11.github.io)|||
|[6. Демьянчук Андрей][12216] |[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://AndreDem135.github.io)|||
|[7. Егоров Юрий][12217] |[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://Prostochell-228.github.io)|||
|[8. Иванов Николай][12218] |[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://schukchu.github.io)|||
|[9. Козлова Карина Константиновна][12219] |[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://evgrfg.github.io)|||
|[10. Кукина Анна][122110] |[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://Aakookie.github.io)|||
|[11. Малахов Кирилл Антонович][122111] |[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://kirmala.github.io)|||
|[12. Никитин Павел Николаевич][122112] |[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://pxnandi.github.io)|||
|[13. Осипов Вячеслав][122113] |[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://NightSkymbry.github.io)|||
|[1. Пешков Матвей Андреевич][122114] |[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https:///churka1488.github.io)|||
|[2. Пирогов Егор Максимович][122115] |[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://sosiska256.github.io)|||
|[3. Семёнов Алексей Павлович][122116] |[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://katela2006.github.io)|||
|[4. Силков Александр Максимович][122117] |[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://W1zard70r.github.io)|||
|[5. Скачкаускас Матвей Александрович][122118] |[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://Mavaro1.github.io)|||
|[6. Соболев Егор Викторович][122119] |[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://ennseg.github.io)|||
|[7. Степанов Михаил Сергеевич][122120] |[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://LostnightRX.github.io)|||
|[8. Толстов Илья Александрович][122121] |[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://ltlstv.github.io)|||
|[9. Фурсова Анна Станиславовна][122122] |[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://afursovaa.github.io)|||
|[10. Хузеев Кирилл Юрьевич ][122123] |[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://kirusha02301.github.io)|||
|[11. Шабанова Галина Алексеевна][122124] |[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://Galua122.github.io)|||
|[12. Шаманина Виктория Максимовна][122125] |[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://Shhamann.github.io)|||
|[13. Шандриков Виктор][122126] |[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://viktorblaming.github.io)|||
|[14. Эков Илья Андреевич][122127] |[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://ilyechubanu.github.io)|||


[12211]: <https://github.com/grad154/timurbakeev154>
[12212]: <https://github.com/Dimakek2/work>
[12213]: <https://github.com/weissok/-22>
[12214]: <https://github.com/VoroninVaycheslav/LearnOfInvormatic>
[12215]: <https://github.com/NikitaDavydov11/FirstRepository>
[12216]: <https://github.com/AndreDem135/FirstRepository>
[12217]: <https://github.com/Prostochell-228/UltraloxIT>
[12218]: <https://github.com/schukchu/figushkiFiguli>
[12219]: <https://github.com/evgrfg/123456>
[122110]: <https://github.com/Aakookie/Kot>
[122111]: <https://github.com/kirmala/school>
[122112]: <https://github.com/pxnandi/tpu-learn>
[122113]: <https://github.com/NightSkymbry/tpu-lic-Osipov-Slava>
[122114]: <https://github.com/churka1488/zzzzzzz/tree/main>
[122115]: <https://github.com/sosiska256/Pirogov-Egor-Maksimovich-122>
[122116]: <https://github.com/katela2006/Alexey>
[122117]: <https://github.com/W1zard70r/Miniature-chainsaw>
[122118]: <https://github.com/Mavaro1/Matvey-Skachkauskas-122b>
[122119]: <https://github.com/ennseg/-122>
[122120]: <https://github.com/LostnightRX/repositorii>
[122121]: <https://github.com/ltlstv/sverchok_ltlstv_420/issues/1>
[122122]: <https://github.com/afursovaa/itworks>
[122123]: <https://github.com/kirusha02301/kirusha02301>
[122124]: <https://github.com/Galua122/works>
[122125]: <https://github.com/Shhamann/11>
[122126]: <https://github.com/viktorblaming/dungeon>
[122127]: <https://github.com/ilyechubanu/itworks>

### 132

| ИМЯ | SITE| УРЗ | PyVIDEO  |
| :---|:---:| :--:|:--:|
|[1. Назарова Юлия Романовна][13211] ||||
|[2. Новиков Михаил][13212] ||||
|[3. Одегов Илья Алексеевич][13213] ||||
|[4. Прохоров Арсений Олегович][13214] ||||
|[5. Пустовалов Михаил][13215] ||||
|[6. Рейс Ангелина][13216] ||||
|[7. Романов Сергей Александрович][13217] ||||
|[8. Рощупкин Максим][13218] ||||
|[9. Трофимова Анастасия Андреевна][13219] ||||
|[10. Тюляндина Яна Александровна][132110] ||||
|[11. Федоров Артем Сергеевич][132111] ||||
|[12. Худобец Надежда Андреевна][132112] ||||
|[13. Черноскутов Артем Вячеславович][132113] ||||
|[14. Шабалина Алёна Руслановна][132114] ||||


[13211]: <https://github.com/meowwoofwoof/nazarova>
[13212]: <https://github.com/nmt132/132-NOVIKOV>
[13213]: <https://github.com/At3K1/132-files>
[13214]: <https://github.com/lssibb/ARS2022>
[13215]: <https://github.com/Mihalk2700/Mihalktrud>
[13216]: <https://github.com/angelina132rais/angelina132rais>
[13217]: <https://github.com/geniusatthemoment/I-am-barbie-girl-in-a-barbie-world>
[13218]: <https://github.com/MaxThePooh/Class>
[13219]: <https://github.com/AnastasiaTrofimova/132>
[132110]: <https://github.com/Yanchik71/->
[132112]: <https://github.com/Yanchik71/->
[132113]: <https://github.com/Artemonchill/shkolnik>
[132114]: <https://github.com/alyonkaww/132-alyonka>


### 142

| ИМЯ | SITE| УРЗ | PyVIDEO  |
| :---|:---:| :--:|:--:|
|[1. Аверин Владимир Андреевич](https://github.com/Averin973/repos142)|[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://grad154.github.io)||
|[2. Барабанова Наталия Дмитриевна](https://github.com/Natunka/bober228)|[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://grad154.github.io)||
|[3. Баранова Софья Александровна](https://github.com/BaranovaSonya/-)|[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://grad154.github.io)||
|[4. Истомина Полина](https://github.com/Vertigro/IstominaPolina)|[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://grad154.github.io)||
|[5. Каллас Данил Сергеевич](https://github.com/KuWka-KTZPG/Shlepa2008)|[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://grad154.github.io)||
|[6. Клименов Илья Иванович](https://github.com/blakktheme)|[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://grad154.github.io)||
|[7. Корзун Никита Александрович](https://github.com/leavingSoSoon)|[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://grad154.github.io)||
|[8. Мельник Ульяна Владимировна](https://github.com/UMelnik/Xin45)|[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://grad154.github.io)||
|[9. Могильный Борислав Евгеньевич](https://github.com/Elittok/Merci-beaucoup)|[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://grad154.github.io)||
|[10. Морозов Никита Юрьевич](https://github.com/nikokastr/main-inform)|[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://grad154.github.io)||
|[11. Шелепов Артём Юрьевич](https://github.com/bymyshagg1bark/bazakormit)|[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://grad154.github.io)||
|[12. Чойнзонов Алексей Элханович](https://github.com/K1m-Taehyung/TPUliceumInformatique)|[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://grad154.github.io)||
|[1. Бельков Вячеслав]()	|[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://grad154.github.io)||
|[2. Наумов Сергей](https://github.com/Napv2900/Napv)|[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://grad154.github.io)||
|[3. Петров Роман Ильич](https://github.com/romchkkk/repos142)|[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://grad154.github.io)||
|[4. Пипина Алина](https://github.com/PleasePomogite/142)|[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://grad154.github.io)||
|[5. Попова Анастасия Сергеевна](https://github.com/oxxrayy/popova142)|[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://grad154.github.io)||
|[6. Потапова Софья](https://github.com/Ethryna/InfTasks)|[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://grad154.github.io)||
|[7. Рибсам Эдуард Евгеньевич](https://github.com/yeryerix/inf)|[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://grad154.github.io)||
|[8. Сподина Анастасия](https://github.com/spodinaanastacia/ihatethissite-)|[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://grad154.github.io)||
|[9. Стариков Арсений Дмитриевич](https://github.com/murphyqwek/python_lyceum)|[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://grad154.github.io)||
|[10. Трущук Артём Максимович](https://github.com/artyomTM/TAM168-142)|[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://grad154.github.io)||
|[11. Тухватулин Ахат Александрович](https://github.com/ahattuhva/public)|[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://grad154.github.io)||
|[12. Уйманова Валерия Дмитриевна](https://github.com/vvlera/inf)|[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://grad154.github.io)||
|[13. Шендеров Владислав Юрьевич](https://github.com/VladOsIkkkk/Reposit142)|[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://grad154.github.io)||
|[14. Шипачев Никита Егорович](https://github.com/1nikov7/-.-.-)|[![](https://user-images.githubusercontent.com/114549805/203996559-8eb67bc7-0eb2-4137-b2cf-40582ba8f531.png)](https://grad154.github.io)||

## Future

<https://www.svgmator.com/>
<https://svgartista.net/>
<https://maxwellito.github.io/vivus-instant/>
<https://svgcircus.com/>
<https://loading.io/>

Mobile Proj

Шахматные этюды
