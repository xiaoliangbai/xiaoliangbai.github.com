---
layout: post
title: "Caffe Long-Short Term Memory (LSTM) on Sin Waveform Prediction"
description: ""
category: 
tags: 
 - Deep Learning
 - LSTM
 - Neural Network
---
{% include JB/setup %}
<html>
<head><meta charset="utf-8" />
<title>Caffe_LSTM_SinWaveform_Batch_Adapted_From_Tensorflow</title>

<script src="https://cdnjs.cloudflare.com/ajax/libs/require.js/2.1.10/require.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/2.0.3/jquery.min.js"></script>

<style type="text/css">
    /*!
*
* Twitter Bootstrap
*
*/
/*!
 * Bootstrap v3.3.6 (http://getbootstrap.com)
 * Copyright 2011-2015 Twitter, Inc.
 * Licensed under MIT (https://github.com/twbs/bootstrap/blob/master/LICENSE)
 */
/*! normalize.css v3.0.3 | MIT License | github.com/necolas/normalize.css */
html {
  font-family: sans-serif;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
}
body {
  margin: 0;
}
article,
aside,
details,
figcaption,
figure,
footer,
header,
hgroup,
main,
menu,
nav,
section,
summary {
  display: block;
}
audio,
canvas,
progress,
video {
  display: inline-block;
  vertical-align: baseline;
}
audio:not([controls]) {
  display: none;
  height: 0;
}
[hidden],
template {
  display: none;
}
a {
  background-color: transparent;
}
a:active,
a:hover {
  outline: 0;
}
abbr[title] {
  border-bottom: 1px dotted;
}
b,
strong {
  font-weight: bold;
}
dfn {
  font-style: italic;
}
h1 {
  font-size: 2em;
  margin: 0.67em 0;
}
mark {
  background: #ff0;
  color: #000;
}
small {
  font-size: 80%;
}
sub,
sup {
  font-size: 75%;
  line-height: 0;
  position: relative;
  vertical-align: baseline;
}
sup {
  top: -0.5em;
}
sub {
  bottom: -0.25em;
}
img {
  border: 0;
}
svg:not(:root) {
  overflow: hidden;
}
figure {
  margin: 1em 40px;
}
hr {
  box-sizing: content-box;
  height: 0;
}
pre {
  overflow: auto;
}
code,
kbd,
pre,
samp {
  font-family: monospace, monospace;
  font-size: 1em;
}
button,
input,
optgroup,
select,
textarea {
  color: inherit;
  font: inherit;
  margin: 0;
}
button {
  overflow: visible;
}
button,
select {
  text-transform: none;
}
button,
html input[type="button"],
input[type="reset"],
input[type="submit"] {
  -webkit-appearance: button;
  cursor: pointer;
}
button[disabled],
html input[disabled] {
  cursor: default;
}
button::-moz-focus-inner,
input::-moz-focus-inner {
  border: 0;
  padding: 0;
}
input {
  line-height: normal;
}
input[type="checkbox"],
input[type="radio"] {
  box-sizing: border-box;
  padding: 0;
}
input[type="number"]::-webkit-inner-spin-button,
input[type="number"]::-webkit-outer-spin-button {
  height: auto;
}
input[type="search"] {
  -webkit-appearance: textfield;
  box-sizing: content-box;
}
input[type="search"]::-webkit-search-cancel-button,
input[type="search"]::-webkit-search-decoration {
  -webkit-appearance: none;
}
fieldset {
  border: 1px solid #c0c0c0;
  margin: 0 2px;
  padding: 0.35em 0.625em 0.75em;
}
legend {
  border: 0;
  padding: 0;
}
textarea {
  overflow: auto;
}
optgroup {
  font-weight: bold;
}
table {
  border-collapse: collapse;
  border-spacing: 0;
}
td,
th {
  padding: 0;
}
/*! Source: https://github.com/h5bp/html5-boilerplate/blob/master/src/css/main.css */
@media print {
  *,
  *:before,
  *:after {
    background: transparent !important;
    color: #000 !important;
    box-shadow: none !important;
    text-shadow: none !important;
  }
  a,
  a:visited {
    text-decoration: underline;
  }
  a[href]:after {
    content: " (" attr(href) ")";
  }
  abbr[title]:after {
    content: " (" attr(title) ")";
  }
  a[href^="#"]:after,
  a[href^="javascript:"]:after {
    content: "";
  }
  pre,
  blockquote {
    border: 1px solid #999;
    page-break-inside: avoid;
  }
  thead {
    display: table-header-group;
  }
  tr,
  img {
    page-break-inside: avoid;
  }
  img {
    max-width: 100% !important;
  }
  p,
  h2,
  h3 {
    orphans: 3;
    widows: 3;
  }
  h2,
  h3 {
    page-break-after: avoid;
  }
  .navbar {
    display: none;
  }
  .btn > .caret,
  .dropup > .btn > .caret {
    border-top-color: #000 !important;
  }
  .label {
    border: 1px solid #000;
  }
  .table {
    border-collapse: collapse !important;
  }
  .table td,
  .table th {
    background-color: #fff !important;
  }
  .table-bordered th,
  .table-bordered td {
    border: 1px solid #ddd !important;
  }
}
@font-face {
  font-family: 'Glyphicons Halflings';
  src: url('../components/bootstrap/fonts/glyphicons-halflings-regular.eot');
  src: url('../components/bootstrap/fonts/glyphicons-halflings-regular.eot?#iefix') format('embedded-opentype'), url('../components/bootstrap/fonts/glyphicons-halflings-regular.woff2') format('woff2'), url('../components/bootstrap/fonts/glyphicons-halflings-regular.woff') format('woff'), url('../components/bootstrap/fonts/glyphicons-halflings-regular.ttf') format('truetype'), url('../components/bootstrap/fonts/glyphicons-halflings-regular.svg#glyphicons_halflingsregular') format('svg');
}
.glyphicon {
  position: relative;
  top: 1px;
  display: inline-block;
  font-family: 'Glyphicons Halflings';
  font-style: normal;
  font-weight: normal;
  line-height: 1;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
.glyphicon-asterisk:before {
  content: "\002a";
}
.glyphicon-plus:before {
  content: "\002b";
}
.glyphicon-euro:before,
.glyphicon-eur:before {
  content: "\20ac";
}
.glyphicon-minus:before {
  content: "\2212";
}
.glyphicon-cloud:before {
  content: "\2601";
}
.glyphicon-envelope:before {
  content: "\2709";
}
.glyphicon-pencil:before {
  content: "\270f";
}
.glyphicon-glass:before {
  content: "\e001";
}
.glyphicon-music:before {
  content: "\e002";
}
.glyphicon-search:before {
  content: "\e003";
}
.glyphicon-heart:before {
  content: "\e005";
}
.glyphicon-star:before {
  content: "\e006";
}
.glyphicon-star-empty:before {
  content: "\e007";
}
.glyphicon-user:before {
  content: "\e008";
}
.glyphicon-film:before {
  content: "\e009";
}
.glyphicon-th-large:before {
  content: "\e010";
}
.glyphicon-th:before {
  content: "\e011";
}
.glyphicon-th-list:before {
  content: "\e012";
}
.glyphicon-ok:before {
  content: "\e013";
}
.glyphicon-remove:before {
  content: "\e014";
}
.glyphicon-zoom-in:before {
  content: "\e015";
}
.glyphicon-zoom-out:before {
  content: "\e016";
}
.glyphicon-off:before {
  content: "\e017";
}
.glyphicon-signal:before {
  content: "\e018";
}
.glyphicon-cog:before {
  content: "\e019";
}
.glyphicon-trash:before {
  content: "\e020";
}
.glyphicon-home:before {
  content: "\e021";
}
.glyphicon-file:before {
  content: "\e022";
}
.glyphicon-time:before {
  content: "\e023";
}
.glyphicon-road:before {
  content: "\e024";
}
.glyphicon-download-alt:before {
  content: "\e025";
}
.glyphicon-download:before {
  content: "\e026";
}
.glyphicon-upload:before {
  content: "\e027";
}
.glyphicon-inbox:before {
  content: "\e028";
}
.glyphicon-play-circle:before {
  content: "\e029";
}
.glyphicon-repeat:before {
  content: "\e030";
}
.glyphicon-refresh:before {
  content: "\e031";
}
.glyphicon-list-alt:before {
  content: "\e032";
}
.glyphicon-lock:before {
  content: "\e033";
}
.glyphicon-flag:before {
  content: "\e034";
}
.glyphicon-headphones:before {
  content: "\e035";
}
.glyphicon-volume-off:before {
  content: "\e036";
}
.glyphicon-volume-down:before {
  content: "\e037";
}
.glyphicon-volume-up:before {
  content: "\e038";
}
.glyphicon-qrcode:before {
  content: "\e039";
}
.glyphicon-barcode:before {
  content: "\e040";
}
.glyphicon-tag:before {
  content: "\e041";
}
.glyphicon-tags:before {
  content: "\e042";
}
.glyphicon-book:before {
  content: "\e043";
}
.glyphicon-bookmark:before {
  content: "\e044";
}
.glyphicon-print:before {
  content: "\e045";
}
.glyphicon-camera:before {
  content: "\e046";
}
.glyphicon-font:before {
  content: "\e047";
}
.glyphicon-bold:before {
  content: "\e048";
}
.glyphicon-italic:before {
  content: "\e049";
}
.glyphicon-text-height:before {
  content: "\e050";
}
.glyphicon-text-width:before {
  content: "\e051";
}
.glyphicon-align-left:before {
  content: "\e052";
}
.glyphicon-align-center:before {
  content: "\e053";
}
.glyphicon-align-right:before {
  content: "\e054";
}
.glyphicon-align-justify:before {
  content: "\e055";
}
.glyphicon-list:before {
  content: "\e056";
}
.glyphicon-indent-left:before {
  content: "\e057";
}
.glyphicon-indent-right:before {
  content: "\e058";
}
.glyphicon-facetime-video:before {
  content: "\e059";
}
.glyphicon-picture:before {
  content: "\e060";
}
.glyphicon-map-marker:before {
  content: "\e062";
}
.glyphicon-adjust:before {
  content: "\e063";
}
.glyphicon-tint:before {
  content: "\e064";
}
.glyphicon-edit:before {
  content: "\e065";
}
.glyphicon-share:before {
  content: "\e066";
}
.glyphicon-check:before {
  content: "\e067";
}
.glyphicon-move:before {
  content: "\e068";
}
.glyphicon-step-backward:before {
  content: "\e069";
}
.glyphicon-fast-backward:before {
  content: "\e070";
}
.glyphicon-backward:before {
  content: "\e071";
}
.glyphicon-play:before {
  content: "\e072";
}
.glyphicon-pause:before {
  content: "\e073";
}
.glyphicon-stop:before {
  content: "\e074";
}
.glyphicon-forward:before {
  content: "\e075";
}
.glyphicon-fast-forward:before {
  content: "\e076";
}
.glyphicon-step-forward:before {
  content: "\e077";
}
.glyphicon-eject:before {
  content: "\e078";
}
.glyphicon-chevron-left:before {
  content: "\e079";
}
.glyphicon-chevron-right:before {
  content: "\e080";
}
.glyphicon-plus-sign:before {
  content: "\e081";
}
.glyphicon-minus-sign:before {
  content: "\e082";
}
.glyphicon-remove-sign:before {
  content: "\e083";
}
.glyphicon-ok-sign:before {
  content: "\e084";
}
.glyphicon-question-sign:before {
  content: "\e085";
}
.glyphicon-info-sign:before {
  content: "\e086";
}
.glyphicon-screenshot:before {
  content: "\e087";
}
.glyphicon-remove-circle:before {
  content: "\e088";
}
.glyphicon-ok-circle:before {
  content: "\e089";
}
.glyphicon-ban-circle:before {
  content: "\e090";
}
.glyphicon-arrow-left:before {
  content: "\e091";
}
.glyphicon-arrow-right:before {
  content: "\e092";
}
.glyphicon-arrow-up:before {
  content: "\e093";
}
.glyphicon-arrow-down:before {
  content: "\e094";
}
.glyphicon-share-alt:before {
  content: "\e095";
}
.glyphicon-resize-full:before {
  content: "\e096";
}
.glyphicon-resize-small:before {
  content: "\e097";
}
.glyphicon-exclamation-sign:before {
  content: "\e101";
}
.glyphicon-gift:before {
  content: "\e102";
}
.glyphicon-leaf:before {
  content: "\e103";
}
.glyphicon-fire:before {
  content: "\e104";
}
.glyphicon-eye-open:before {
  content: "\e105";
}
.glyphicon-eye-close:before {
  content: "\e106";
}
.glyphicon-warning-sign:before {
  content: "\e107";
}
.glyphicon-plane:before {
  content: "\e108";
}
.glyphicon-calendar:before {
  content: "\e109";
}
.glyphicon-random:before {
  content: "\e110";
}
.glyphicon-comment:before {
  content: "\e111";
}
.glyphicon-magnet:before {
  content: "\e112";
}
.glyphicon-chevron-up:before {
  content: "\e113";
}
.glyphicon-chevron-down:before {
  content: "\e114";
}
.glyphicon-retweet:before {
  content: "\e115";
}
.glyphicon-shopping-cart:before {
  content: "\e116";
}
.glyphicon-folder-close:before {
  content: "\e117";
}
.glyphicon-folder-open:before {
  content: "\e118";
}
.glyphicon-resize-vertical:before {
  content: "\e119";
}
.glyphicon-resize-horizontal:before {
  content: "\e120";
}
.glyphicon-hdd:before {
  content: "\e121";
}
.glyphicon-bullhorn:before {
  content: "\e122";
}
.glyphicon-bell:before {
  content: "\e123";
}
.glyphicon-certificate:before {
  content: "\e124";
}
.glyphicon-thumbs-up:before {
  content: "\e125";
}
.glyphicon-thumbs-down:before {
  content: "\e126";
}
.glyphicon-hand-right:before {
  content: "\e127";
}
.glyphicon-hand-left:before {
  content: "\e128";
}
.glyphicon-hand-up:before {
  content: "\e129";
}
.glyphicon-hand-down:before {
  content: "\e130";
}
.glyphicon-circle-arrow-right:before {
  content: "\e131";
}
.glyphicon-circle-arrow-left:before {
  content: "\e132";
}
.glyphicon-circle-arrow-up:before {
  content: "\e133";
}
.glyphicon-circle-arrow-down:before {
  content: "\e134";
}
.glyphicon-globe:before {
  content: "\e135";
}
.glyphicon-wrench:before {
  content: "\e136";
}
.glyphicon-tasks:before {
  content: "\e137";
}
.glyphicon-filter:before {
  content: "\e138";
}
.glyphicon-briefcase:before {
  content: "\e139";
}
.glyphicon-fullscreen:before {
  content: "\e140";
}
.glyphicon-dashboard:before {
  content: "\e141";
}
.glyphicon-paperclip:before {
  content: "\e142";
}
.glyphicon-heart-empty:before {
  content: "\e143";
}
.glyphicon-link:before {
  content: "\e144";
}
.glyphicon-phone:before {
  content: "\e145";
}
.glyphicon-pushpin:before {
  content: "\e146";
}
.glyphicon-usd:before {
  content: "\e148";
}
.glyphicon-gbp:before {
  content: "\e149";
}
.glyphicon-sort:before {
  content: "\e150";
}
.glyphicon-sort-by-alphabet:before {
  content: "\e151";
}
.glyphicon-sort-by-alphabet-alt:before {
  content: "\e152";
}
.glyphicon-sort-by-order:before {
  content: "\e153";
}
.glyphicon-sort-by-order-alt:before {
  content: "\e154";
}
.glyphicon-sort-by-attributes:before {
  content: "\e155";
}
.glyphicon-sort-by-attributes-alt:before {
  content: "\e156";
}
.glyphicon-unchecked:before {
  content: "\e157";
}
.glyphicon-expand:before {
  content: "\e158";
}
.glyphicon-collapse-down:before {
  content: "\e159";
}
.glyphicon-collapse-up:before {
  content: "\e160";
}
.glyphicon-log-in:before {
  content: "\e161";
}
.glyphicon-flash:before {
  content: "\e162";
}
.glyphicon-log-out:before {
  content: "\e163";
}
.glyphicon-new-window:before {
  content: "\e164";
}
.glyphicon-record:before {
  content: "\e165";
}
.glyphicon-save:before {
  content: "\e166";
}
.glyphicon-open:before {
  content: "\e167";
}
.glyphicon-saved:before {
  content: "\e168";
}
.glyphicon-import:before {
  content: "\e169";
}
.glyphicon-export:before {
  content: "\e170";
}
.glyphicon-send:before {
  content: "\e171";
}
.glyphicon-floppy-disk:before {
  content: "\e172";
}
.glyphicon-floppy-saved:before {
  content: "\e173";
}
.glyphicon-floppy-remove:before {
  content: "\e174";
}
.glyphicon-floppy-save:before {
  content: "\e175";
}
.glyphicon-floppy-open:before {
  content: "\e176";
}
.glyphicon-credit-card:before {
  content: "\e177";
}
.glyphicon-transfer:before {
  content: "\e178";
}
.glyphicon-cutlery:before {
  content: "\e179";
}
.glyphicon-header:before {
  content: "\e180";
}
.glyphicon-compressed:before {
  content: "\e181";
}
.glyphicon-earphone:before {
  content: "\e182";
}
.glyphicon-phone-alt:before {
  content: "\e183";
}
.glyphicon-tower:before {
  content: "\e184";
}
.glyphicon-stats:before {
  content: "\e185";
}
.glyphicon-sd-video:before {
  content: "\e186";
}
.glyphicon-hd-video:before {
  content: "\e187";
}
.glyphicon-subtitles:before {
  content: "\e188";
}
.glyphicon-sound-stereo:before {
  content: "\e189";
}
.glyphicon-sound-dolby:before {
  content: "\e190";
}
.glyphicon-sound-5-1:before {
  content: "\e191";
}
.glyphicon-sound-6-1:before {
  content: "\e192";
}
.glyphicon-sound-7-1:before {
  content: "\e193";
}
.glyphicon-copyright-mark:before {
  content: "\e194";
}
.glyphicon-registration-mark:before {
  content: "\e195";
}
.glyphicon-cloud-download:before {
  content: "\e197";
}
.glyphicon-cloud-upload:before {
  content: "\e198";
}
.glyphicon-tree-conifer:before {
  content: "\e199";
}
.glyphicon-tree-deciduous:before {
  content: "\e200";
}
.glyphicon-cd:before {
  content: "\e201";
}
.glyphicon-save-file:before {
  content: "\e202";
}
.glyphicon-open-file:before {
  content: "\e203";
}
.glyphicon-level-up:before {
  content: "\e204";
}
.glyphicon-copy:before {
  content: "\e205";
}
.glyphicon-paste:before {
  content: "\e206";
}
.glyphicon-alert:before {
  content: "\e209";
}
.glyphicon-equalizer:before {
  content: "\e210";
}
.glyphicon-king:before {
  content: "\e211";
}
.glyphicon-queen:before {
  content: "\e212";
}
.glyphicon-pawn:before {
  content: "\e213";
}
.glyphicon-bishop:before {
  content: "\e214";
}
.glyphicon-knight:before {
  content: "\e215";
}
.glyphicon-baby-formula:before {
  content: "\e216";
}
.glyphicon-tent:before {
  content: "\26fa";
}
.glyphicon-blackboard:before {
  content: "\e218";
}
.glyphicon-bed:before {
  content: "\e219";
}
.glyphicon-apple:before {
  content: "\f8ff";
}
.glyphicon-erase:before {
  content: "\e221";
}
.glyphicon-hourglass:before {
  content: "\231b";
}
.glyphicon-lamp:before {
  content: "\e223";
}
.glyphicon-duplicate:before {
  content: "\e224";
}
.glyphicon-piggy-bank:before {
  content: "\e225";
}
.glyphicon-scissors:before {
  content: "\e226";
}
.glyphicon-bitcoin:before {
  content: "\e227";
}
.glyphicon-btc:before {
  content: "\e227";
}
.glyphicon-xbt:before {
  content: "\e227";
}
.glyphicon-yen:before {
  content: "\00a5";
}
.glyphicon-jpy:before {
  content: "\00a5";
}
.glyphicon-ruble:before {
  content: "\20bd";
}
.glyphicon-rub:before {
  content: "\20bd";
}
.glyphicon-scale:before {
  content: "\e230";
}
.glyphicon-ice-lolly:before {
  content: "\e231";
}
.glyphicon-ice-lolly-tasted:before {
  content: "\e232";
}
.glyphicon-education:before {
  content: "\e233";
}
.glyphicon-option-horizontal:before {
  content: "\e234";
}
.glyphicon-option-vertical:before {
  content: "\e235";
}
.glyphicon-menu-hamburger:before {
  content: "\e236";
}
.glyphicon-modal-window:before {
  content: "\e237";
}
.glyphicon-oil:before {
  content: "\e238";
}
.glyphicon-grain:before {
  content: "\e239";
}
.glyphicon-sunglasses:before {
  content: "\e240";
}
.glyphicon-text-size:before {
  content: "\e241";
}
.glyphicon-text-color:before {
  content: "\e242";
}
.glyphicon-text-background:before {
  content: "\e243";
}
.glyphicon-object-align-top:before {
  content: "\e244";
}
.glyphicon-object-align-bottom:before {
  content: "\e245";
}
.glyphicon-object-align-horizontal:before {
  content: "\e246";
}
.glyphicon-object-align-left:before {
  content: "\e247";
}
.glyphicon-object-align-vertical:before {
  content: "\e248";
}
.glyphicon-object-align-right:before {
  content: "\e249";
}
.glyphicon-triangle-right:before {
  content: "\e250";
}
.glyphicon-triangle-left:before {
  content: "\e251";
}
.glyphicon-triangle-bottom:before {
  content: "\e252";
}
.glyphicon-triangle-top:before {
  content: "\e253";
}
.glyphicon-console:before {
  content: "\e254";
}
.glyphicon-superscript:before {
  content: "\e255";
}
.glyphicon-subscript:before {
  content: "\e256";
}
.glyphicon-menu-left:before {
  content: "\e257";
}
.glyphicon-menu-right:before {
  content: "\e258";
}
.glyphicon-menu-down:before {
  content: "\e259";
}
.glyphicon-menu-up:before {
  content: "\e260";
}
* {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
*:before,
*:after {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
html {
  font-size: 10px;
  -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
}
body {
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-size: 13px;
  line-height: 1.42857143;
  color: #000;
  background-color: #fff;
}
input,
button,
select,
textarea {
  font-family: inherit;
  font-size: inherit;
  line-height: inherit;
}
a {
  color: #337ab7;
  text-decoration: none;
}
a:hover,
a:focus {
  color: #23527c;
  text-decoration: underline;
}
a:focus {
  outline: thin dotted;
  outline: 5px auto -webkit-focus-ring-color;
  outline-offset: -2px;
}
figure {
  margin: 0;
}
img {
  vertical-align: middle;
}
.img-responsive,
.thumbnail > img,
.thumbnail a > img,
.carousel-inner > .item > img,
.carousel-inner > .item > a > img {
  display: block;
  max-width: 100%;
  height: auto;
}
.img-rounded {
  border-radius: 3px;
}
.img-thumbnail {
  padding: 4px;
  line-height: 1.42857143;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 2px;
  -webkit-transition: all 0.2s ease-in-out;
  -o-transition: all 0.2s ease-in-out;
  transition: all 0.2s ease-in-out;
  display: inline-block;
  max-width: 100%;
  height: auto;
}
.img-circle {
  border-radius: 50%;
}
hr {
  margin-top: 18px;
  margin-bottom: 18px;
  border: 0;
  border-top: 1px solid #eeeeee;
}
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  margin: -1px;
  padding: 0;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  border: 0;
}
.sr-only-focusable:active,
.sr-only-focusable:focus {
  position: static;
  width: auto;
  height: auto;
  margin: 0;
  overflow: visible;
  clip: auto;
}
[role="button"] {
  cursor: pointer;
}
h1,
h2,
h3,
h4,
h5,
h6,
.h1,
.h2,
.h3,
.h4,
.h5,
.h6 {
  font-family: inherit;
  font-weight: 500;
  line-height: 1.1;
  color: inherit;
}
h1 small,
h2 small,
h3 small,
h4 small,
h5 small,
h6 small,
.h1 small,
.h2 small,
.h3 small,
.h4 small,
.h5 small,
.h6 small,
h1 .small,
h2 .small,
h3 .small,
h4 .small,
h5 .small,
h6 .small,
.h1 .small,
.h2 .small,
.h3 .small,
.h4 .small,
.h5 .small,
.h6 .small {
  font-weight: normal;
  line-height: 1;
  color: #777777;
}
h1,
.h1,
h2,
.h2,
h3,
.h3 {
  margin-top: 18px;
  margin-bottom: 9px;
}
h1 small,
.h1 small,
h2 small,
.h2 small,
h3 small,
.h3 small,
h1 .small,
.h1 .small,
h2 .small,
.h2 .small,
h3 .small,
.h3 .small {
  font-size: 65%;
}
h4,
.h4,
h5,
.h5,
h6,
.h6 {
  margin-top: 9px;
  margin-bottom: 9px;
}
h4 small,
.h4 small,
h5 small,
.h5 small,
h6 small,
.h6 small,
h4 .small,
.h4 .small,
h5 .small,
.h5 .small,
h6 .small,
.h6 .small {
  font-size: 75%;
}
h1,
.h1 {
  font-size: 33px;
}
h2,
.h2 {
  font-size: 27px;
}
h3,
.h3 {
  font-size: 23px;
}
h4,
.h4 {
  font-size: 17px;
}
h5,
.h5 {
  font-size: 13px;
}
h6,
.h6 {
  font-size: 12px;
}
p {
  margin: 0 0 9px;
}
.lead {
  margin-bottom: 18px;
  font-size: 14px;
  font-weight: 300;
  line-height: 1.4;
}
@media (min-width: 768px) {
  .lead {
    font-size: 19.5px;
  }
}
small,
.small {
  font-size: 92%;
}
mark,
.mark {
  background-color: #fcf8e3;
  padding: .2em;
}
.text-left {
  text-align: left;
}
.text-right {
  text-align: right;
}
.text-center {
  text-align: center;
}
.text-justify {
  text-align: justify;
}
.text-nowrap {
  white-space: nowrap;
}
.text-lowercase {
  text-transform: lowercase;
}
.text-uppercase {
  text-transform: uppercase;
}
.text-capitalize {
  text-transform: capitalize;
}
.text-muted {
  color: #777777;
}
.text-primary {
  color: #337ab7;
}
a.text-primary:hover,
a.text-primary:focus {
  color: #286090;
}
.text-success {
  color: #3c763d;
}
a.text-success:hover,
a.text-success:focus {
  color: #2b542c;
}
.text-info {
  color: #31708f;
}
a.text-info:hover,
a.text-info:focus {
  color: #245269;
}
.text-warning {
  color: #8a6d3b;
}
a.text-warning:hover,
a.text-warning:focus {
  color: #66512c;
}
.text-danger {
  color: #a94442;
}
a.text-danger:hover,
a.text-danger:focus {
  color: #843534;
}
.bg-primary {
  color: #fff;
  background-color: #337ab7;
}
a.bg-primary:hover,
a.bg-primary:focus {
  background-color: #286090;
}
.bg-success {
  background-color: #dff0d8;
}
a.bg-success:hover,
a.bg-success:focus {
  background-color: #c1e2b3;
}
.bg-info {
  background-color: #d9edf7;
}
a.bg-info:hover,
a.bg-info:focus {
  background-color: #afd9ee;
}
.bg-warning {
  background-color: #fcf8e3;
}
a.bg-warning:hover,
a.bg-warning:focus {
  background-color: #f7ecb5;
}
.bg-danger {
  background-color: #f2dede;
}
a.bg-danger:hover,
a.bg-danger:focus {
  background-color: #e4b9b9;
}
.page-header {
  padding-bottom: 8px;
  margin: 36px 0 18px;
  border-bottom: 1px solid #eeeeee;
}
ul,
ol {
  margin-top: 0;
  margin-bottom: 9px;
}
ul ul,
ol ul,
ul ol,
ol ol {
  margin-bottom: 0;
}
.list-unstyled {
  padding-left: 0;
  list-style: none;
}
.list-inline {
  padding-left: 0;
  list-style: none;
  margin-left: -5px;
}
.list-inline > li {
  display: inline-block;
  padding-left: 5px;
  padding-right: 5px;
}
dl {
  margin-top: 0;
  margin-bottom: 18px;
}
dt,
dd {
  line-height: 1.42857143;
}
dt {
  font-weight: bold;
}
dd {
  margin-left: 0;
}
@media (min-width: 541px) {
  .dl-horizontal dt {
    float: left;
    width: 160px;
    clear: left;
    text-align: right;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
  }
  .dl-horizontal dd {
    margin-left: 180px;
  }
}
abbr[title],
abbr[data-original-title] {
  cursor: help;
  border-bottom: 1px dotted #777777;
}
.initialism {
  font-size: 90%;
  text-transform: uppercase;
}
blockquote {
  padding: 9px 18px;
  margin: 0 0 18px;
  font-size: inherit;
  border-left: 5px solid #eeeeee;
}
blockquote p:last-child,
blockquote ul:last-child,
blockquote ol:last-child {
  margin-bottom: 0;
}
blockquote footer,
blockquote small,
blockquote .small {
  display: block;
  font-size: 80%;
  line-height: 1.42857143;
  color: #777777;
}
blockquote footer:before,
blockquote small:before,
blockquote .small:before {
  content: '\2014 \00A0';
}
.blockquote-reverse,
blockquote.pull-right {
  padding-right: 15px;
  padding-left: 0;
  border-right: 5px solid #eeeeee;
  border-left: 0;
  text-align: right;
}
.blockquote-reverse footer:before,
blockquote.pull-right footer:before,
.blockquote-reverse small:before,
blockquote.pull-right small:before,
.blockquote-reverse .small:before,
blockquote.pull-right .small:before {
  content: '';
}
.blockquote-reverse footer:after,
blockquote.pull-right footer:after,
.blockquote-reverse small:after,
blockquote.pull-right small:after,
.blockquote-reverse .small:after,
blockquote.pull-right .small:after {
  content: '\00A0 \2014';
}
address {
  margin-bottom: 18px;
  font-style: normal;
  line-height: 1.42857143;
}
code,
kbd,
pre,
samp {
  font-family: monospace;
}
code {
  padding: 2px 4px;
  font-size: 90%;
  color: #c7254e;
  background-color: #f9f2f4;
  border-radius: 2px;
}
kbd {
  padding: 2px 4px;
  font-size: 90%;
  color: #888;
  background-color: transparent;
  border-radius: 1px;
  box-shadow: inset 0 -1px 0 rgba(0, 0, 0, 0.25);
}
kbd kbd {
  padding: 0;
  font-size: 100%;
  font-weight: bold;
  box-shadow: none;
}
pre {
  display: block;
  padding: 8.5px;
  margin: 0 0 9px;
  font-size: 12px;
  line-height: 1.42857143;
  word-break: break-all;
  word-wrap: break-word;
  color: #333333;
  background-color: #f5f5f5;
  border: 1px solid #ccc;
  border-radius: 2px;
}
pre code {
  padding: 0;
  font-size: inherit;
  color: inherit;
  white-space: pre-wrap;
  background-color: transparent;
  border-radius: 0;
}
.pre-scrollable {
  max-height: 340px;
  overflow-y: scroll;
}
.container {
  margin-right: auto;
  margin-left: auto;
  padding-left: 0px;
  padding-right: 0px;
}
@media (min-width: 768px) {
  .container {
    width: 768px;
  }
}
@media (min-width: 992px) {
  .container {
    width: 940px;
  }
}
@media (min-width: 1200px) {
  .container {
    width: 1140px;
  }
}
.container-fluid {
  margin-right: auto;
  margin-left: auto;
  padding-left: 0px;
  padding-right: 0px;
}
.row {
  margin-left: 0px;
  margin-right: 0px;
}
.col-xs-1, .col-sm-1, .col-md-1, .col-lg-1, .col-xs-2, .col-sm-2, .col-md-2, .col-lg-2, .col-xs-3, .col-sm-3, .col-md-3, .col-lg-3, .col-xs-4, .col-sm-4, .col-md-4, .col-lg-4, .col-xs-5, .col-sm-5, .col-md-5, .col-lg-5, .col-xs-6, .col-sm-6, .col-md-6, .col-lg-6, .col-xs-7, .col-sm-7, .col-md-7, .col-lg-7, .col-xs-8, .col-sm-8, .col-md-8, .col-lg-8, .col-xs-9, .col-sm-9, .col-md-9, .col-lg-9, .col-xs-10, .col-sm-10, .col-md-10, .col-lg-10, .col-xs-11, .col-sm-11, .col-md-11, .col-lg-11, .col-xs-12, .col-sm-12, .col-md-12, .col-lg-12 {
  position: relative;
  min-height: 1px;
  padding-left: 0px;
  padding-right: 0px;
}
.col-xs-1, .col-xs-2, .col-xs-3, .col-xs-4, .col-xs-5, .col-xs-6, .col-xs-7, .col-xs-8, .col-xs-9, .col-xs-10, .col-xs-11, .col-xs-12 {
  float: left;
}
.col-xs-12 {
  width: 100%;
}
.col-xs-11 {
  width: 91.66666667%;
}
.col-xs-10 {
  width: 83.33333333%;
}
.col-xs-9 {
  width: 75%;
}
.col-xs-8 {
  width: 66.66666667%;
}
.col-xs-7 {
  width: 58.33333333%;
}
.col-xs-6 {
  width: 50%;
}
.col-xs-5 {
  width: 41.66666667%;
}
.col-xs-4 {
  width: 33.33333333%;
}
.col-xs-3 {
  width: 25%;
}
.col-xs-2 {
  width: 16.66666667%;
}
.col-xs-1 {
  width: 8.33333333%;
}
.col-xs-pull-12 {
  right: 100%;
}
.col-xs-pull-11 {
  right: 91.66666667%;
}
.col-xs-pull-10 {
  right: 83.33333333%;
}
.col-xs-pull-9 {
  right: 75%;
}
.col-xs-pull-8 {
  right: 66.66666667%;
}
.col-xs-pull-7 {
  right: 58.33333333%;
}
.col-xs-pull-6 {
  right: 50%;
}
.col-xs-pull-5 {
  right: 41.66666667%;
}
.col-xs-pull-4 {
  right: 33.33333333%;
}
.col-xs-pull-3 {
  right: 25%;
}
.col-xs-pull-2 {
  right: 16.66666667%;
}
.col-xs-pull-1 {
  right: 8.33333333%;
}
.col-xs-pull-0 {
  right: auto;
}
.col-xs-push-12 {
  left: 100%;
}
.col-xs-push-11 {
  left: 91.66666667%;
}
.col-xs-push-10 {
  left: 83.33333333%;
}
.col-xs-push-9 {
  left: 75%;
}
.col-xs-push-8 {
  left: 66.66666667%;
}
.col-xs-push-7 {
  left: 58.33333333%;
}
.col-xs-push-6 {
  left: 50%;
}
.col-xs-push-5 {
  left: 41.66666667%;
}
.col-xs-push-4 {
  left: 33.33333333%;
}
.col-xs-push-3 {
  left: 25%;
}
.col-xs-push-2 {
  left: 16.66666667%;
}
.col-xs-push-1 {
  left: 8.33333333%;
}
.col-xs-push-0 {
  left: auto;
}
.col-xs-offset-12 {
  margin-left: 100%;
}
.col-xs-offset-11 {
  margin-left: 91.66666667%;
}
.col-xs-offset-10 {
  margin-left: 83.33333333%;
}
.col-xs-offset-9 {
  margin-left: 75%;
}
.col-xs-offset-8 {
  margin-left: 66.66666667%;
}
.col-xs-offset-7 {
  margin-left: 58.33333333%;
}
.col-xs-offset-6 {
  margin-left: 50%;
}
.col-xs-offset-5 {
  margin-left: 41.66666667%;
}
.col-xs-offset-4 {
  margin-left: 33.33333333%;
}
.col-xs-offset-3 {
  margin-left: 25%;
}
.col-xs-offset-2 {
  margin-left: 16.66666667%;
}
.col-xs-offset-1 {
  margin-left: 8.33333333%;
}
.col-xs-offset-0 {
  margin-left: 0%;
}
@media (min-width: 768px) {
  .col-sm-1, .col-sm-2, .col-sm-3, .col-sm-4, .col-sm-5, .col-sm-6, .col-sm-7, .col-sm-8, .col-sm-9, .col-sm-10, .col-sm-11, .col-sm-12 {
    float: left;
  }
  .col-sm-12 {
    width: 100%;
  }
  .col-sm-11 {
    width: 91.66666667%;
  }
  .col-sm-10 {
    width: 83.33333333%;
  }
  .col-sm-9 {
    width: 75%;
  }
  .col-sm-8 {
    width: 66.66666667%;
  }
  .col-sm-7 {
    width: 58.33333333%;
  }
  .col-sm-6 {
    width: 50%;
  }
  .col-sm-5 {
    width: 41.66666667%;
  }
  .col-sm-4 {
    width: 33.33333333%;
  }
  .col-sm-3 {
    width: 25%;
  }
  .col-sm-2 {
    width: 16.66666667%;
  }
  .col-sm-1 {
    width: 8.33333333%;
  }
  .col-sm-pull-12 {
    right: 100%;
  }
  .col-sm-pull-11 {
    right: 91.66666667%;
  }
  .col-sm-pull-10 {
    right: 83.33333333%;
  }
  .col-sm-pull-9 {
    right: 75%;
  }
  .col-sm-pull-8 {
    right: 66.66666667%;
  }
  .col-sm-pull-7 {
    right: 58.33333333%;
  }
  .col-sm-pull-6 {
    right: 50%;
  }
  .col-sm-pull-5 {
    right: 41.66666667%;
  }
  .col-sm-pull-4 {
    right: 33.33333333%;
  }
  .col-sm-pull-3 {
    right: 25%;
  }
  .col-sm-pull-2 {
    right: 16.66666667%;
  }
  .col-sm-pull-1 {
    right: 8.33333333%;
  }
  .col-sm-pull-0 {
    right: auto;
  }
  .col-sm-push-12 {
    left: 100%;
  }
  .col-sm-push-11 {
    left: 91.66666667%;
  }
  .col-sm-push-10 {
    left: 83.33333333%;
  }
  .col-sm-push-9 {
    left: 75%;
  }
  .col-sm-push-8 {
    left: 66.66666667%;
  }
  .col-sm-push-7 {
    left: 58.33333333%;
  }
  .col-sm-push-6 {
    left: 50%;
  }
  .col-sm-push-5 {
    left: 41.66666667%;
  }
  .col-sm-push-4 {
    left: 33.33333333%;
  }
  .col-sm-push-3 {
    left: 25%;
  }
  .col-sm-push-2 {
    left: 16.66666667%;
  }
  .col-sm-push-1 {
    left: 8.33333333%;
  }
  .col-sm-push-0 {
    left: auto;
  }
  .col-sm-offset-12 {
    margin-left: 100%;
  }
  .col-sm-offset-11 {
    margin-left: 91.66666667%;
  }
  .col-sm-offset-10 {
    margin-left: 83.33333333%;
  }
  .col-sm-offset-9 {
    margin-left: 75%;
  }
  .col-sm-offset-8 {
    margin-left: 66.66666667%;
  }
  .col-sm-offset-7 {
    margin-left: 58.33333333%;
  }
  .col-sm-offset-6 {
    margin-left: 50%;
  }
  .col-sm-offset-5 {
    margin-left: 41.66666667%;
  }
  .col-sm-offset-4 {
    margin-left: 33.33333333%;
  }
  .col-sm-offset-3 {
    margin-left: 25%;
  }
  .col-sm-offset-2 {
    margin-left: 16.66666667%;
  }
  .col-sm-offset-1 {
    margin-left: 8.33333333%;
  }
  .col-sm-offset-0 {
    margin-left: 0%;
  }
}
@media (min-width: 992px) {
  .col-md-1, .col-md-2, .col-md-3, .col-md-4, .col-md-5, .col-md-6, .col-md-7, .col-md-8, .col-md-9, .col-md-10, .col-md-11, .col-md-12 {
    float: left;
  }
  .col-md-12 {
    width: 100%;
  }
  .col-md-11 {
    width: 91.66666667%;
  }
  .col-md-10 {
    width: 83.33333333%;
  }
  .col-md-9 {
    width: 75%;
  }
  .col-md-8 {
    width: 66.66666667%;
  }
  .col-md-7 {
    width: 58.33333333%;
  }
  .col-md-6 {
    width: 50%;
  }
  .col-md-5 {
    width: 41.66666667%;
  }
  .col-md-4 {
    width: 33.33333333%;
  }
  .col-md-3 {
    width: 25%;
  }
  .col-md-2 {
    width: 16.66666667%;
  }
  .col-md-1 {
    width: 8.33333333%;
  }
  .col-md-pull-12 {
    right: 100%;
  }
  .col-md-pull-11 {
    right: 91.66666667%;
  }
  .col-md-pull-10 {
    right: 83.33333333%;
  }
  .col-md-pull-9 {
    right: 75%;
  }
  .col-md-pull-8 {
    right: 66.66666667%;
  }
  .col-md-pull-7 {
    right: 58.33333333%;
  }
  .col-md-pull-6 {
    right: 50%;
  }
  .col-md-pull-5 {
    right: 41.66666667%;
  }
  .col-md-pull-4 {
    right: 33.33333333%;
  }
  .col-md-pull-3 {
    right: 25%;
  }
  .col-md-pull-2 {
    right: 16.66666667%;
  }
  .col-md-pull-1 {
    right: 8.33333333%;
  }
  .col-md-pull-0 {
    right: auto;
  }
  .col-md-push-12 {
    left: 100%;
  }
  .col-md-push-11 {
    left: 91.66666667%;
  }
  .col-md-push-10 {
    left: 83.33333333%;
  }
  .col-md-push-9 {
    left: 75%;
  }
  .col-md-push-8 {
    left: 66.66666667%;
  }
  .col-md-push-7 {
    left: 58.33333333%;
  }
  .col-md-push-6 {
    left: 50%;
  }
  .col-md-push-5 {
    left: 41.66666667%;
  }
  .col-md-push-4 {
    left: 33.33333333%;
  }
  .col-md-push-3 {
    left: 25%;
  }
  .col-md-push-2 {
    left: 16.66666667%;
  }
  .col-md-push-1 {
    left: 8.33333333%;
  }
  .col-md-push-0 {
    left: auto;
  }
  .col-md-offset-12 {
    margin-left: 100%;
  }
  .col-md-offset-11 {
    margin-left: 91.66666667%;
  }
  .col-md-offset-10 {
    margin-left: 83.33333333%;
  }
  .col-md-offset-9 {
    margin-left: 75%;
  }
  .col-md-offset-8 {
    margin-left: 66.66666667%;
  }
  .col-md-offset-7 {
    margin-left: 58.33333333%;
  }
  .col-md-offset-6 {
    margin-left: 50%;
  }
  .col-md-offset-5 {
    margin-left: 41.66666667%;
  }
  .col-md-offset-4 {
    margin-left: 33.33333333%;
  }
  .col-md-offset-3 {
    margin-left: 25%;
  }
  .col-md-offset-2 {
    margin-left: 16.66666667%;
  }
  .col-md-offset-1 {
    margin-left: 8.33333333%;
  }
  .col-md-offset-0 {
    margin-left: 0%;
  }
}
@media (min-width: 1200px) {
  .col-lg-1, .col-lg-2, .col-lg-3, .col-lg-4, .col-lg-5, .col-lg-6, .col-lg-7, .col-lg-8, .col-lg-9, .col-lg-10, .col-lg-11, .col-lg-12 {
    float: left;
  }
  .col-lg-12 {
    width: 100%;
  }
  .col-lg-11 {
    width: 91.66666667%;
  }
  .col-lg-10 {
    width: 83.33333333%;
  }
  .col-lg-9 {
    width: 75%;
  }
  .col-lg-8 {
    width: 66.66666667%;
  }
  .col-lg-7 {
    width: 58.33333333%;
  }
  .col-lg-6 {
    width: 50%;
  }
  .col-lg-5 {
    width: 41.66666667%;
  }
  .col-lg-4 {
    width: 33.33333333%;
  }
  .col-lg-3 {
    width: 25%;
  }
  .col-lg-2 {
    width: 16.66666667%;
  }
  .col-lg-1 {
    width: 8.33333333%;
  }
  .col-lg-pull-12 {
    right: 100%;
  }
  .col-lg-pull-11 {
    right: 91.66666667%;
  }
  .col-lg-pull-10 {
    right: 83.33333333%;
  }
  .col-lg-pull-9 {
    right: 75%;
  }
  .col-lg-pull-8 {
    right: 66.66666667%;
  }
  .col-lg-pull-7 {
    right: 58.33333333%;
  }
  .col-lg-pull-6 {
    right: 50%;
  }
  .col-lg-pull-5 {
    right: 41.66666667%;
  }
  .col-lg-pull-4 {
    right: 33.33333333%;
  }
  .col-lg-pull-3 {
    right: 25%;
  }
  .col-lg-pull-2 {
    right: 16.66666667%;
  }
  .col-lg-pull-1 {
    right: 8.33333333%;
  }
  .col-lg-pull-0 {
    right: auto;
  }
  .col-lg-push-12 {
    left: 100%;
  }
  .col-lg-push-11 {
    left: 91.66666667%;
  }
  .col-lg-push-10 {
    left: 83.33333333%;
  }
  .col-lg-push-9 {
    left: 75%;
  }
  .col-lg-push-8 {
    left: 66.66666667%;
  }
  .col-lg-push-7 {
    left: 58.33333333%;
  }
  .col-lg-push-6 {
    left: 50%;
  }
  .col-lg-push-5 {
    left: 41.66666667%;
  }
  .col-lg-push-4 {
    left: 33.33333333%;
  }
  .col-lg-push-3 {
    left: 25%;
  }
  .col-lg-push-2 {
    left: 16.66666667%;
  }
  .col-lg-push-1 {
    left: 8.33333333%;
  }
  .col-lg-push-0 {
    left: auto;
  }
  .col-lg-offset-12 {
    margin-left: 100%;
  }
  .col-lg-offset-11 {
    margin-left: 91.66666667%;
  }
  .col-lg-offset-10 {
    margin-left: 83.33333333%;
  }
  .col-lg-offset-9 {
    margin-left: 75%;
  }
  .col-lg-offset-8 {
    margin-left: 66.66666667%;
  }
  .col-lg-offset-7 {
    margin-left: 58.33333333%;
  }
  .col-lg-offset-6 {
    margin-left: 50%;
  }
  .col-lg-offset-5 {
    margin-left: 41.66666667%;
  }
  .col-lg-offset-4 {
    margin-left: 33.33333333%;
  }
  .col-lg-offset-3 {
    margin-left: 25%;
  }
  .col-lg-offset-2 {
    margin-left: 16.66666667%;
  }
  .col-lg-offset-1 {
    margin-left: 8.33333333%;
  }
  .col-lg-offset-0 {
    margin-left: 0%;
  }
}
table {
  background-color: transparent;
}
caption {
  padding-top: 8px;
  padding-bottom: 8px;
  color: #777777;
  text-align: left;
}
th {
  text-align: left;
}
.table {
  width: 100%;
  max-width: 100%;
  margin-bottom: 18px;
}
.table > thead > tr > th,
.table > tbody > tr > th,
.table > tfoot > tr > th,
.table > thead > tr > td,
.table > tbody > tr > td,
.table > tfoot > tr > td {
  padding: 8px;
  line-height: 1.42857143;
  vertical-align: top;
  border-top: 1px solid #ddd;
}
.table > thead > tr > th {
  vertical-align: bottom;
  border-bottom: 2px solid #ddd;
}
.table > caption + thead > tr:first-child > th,
.table > colgroup + thead > tr:first-child > th,
.table > thead:first-child > tr:first-child > th,
.table > caption + thead > tr:first-child > td,
.table > colgroup + thead > tr:first-child > td,
.table > thead:first-child > tr:first-child > td {
  border-top: 0;
}
.table > tbody + tbody {
  border-top: 2px solid #ddd;
}
.table .table {
  background-color: #fff;
}
.table-condensed > thead > tr > th,
.table-condensed > tbody > tr > th,
.table-condensed > tfoot > tr > th,
.table-condensed > thead > tr > td,
.table-condensed > tbody > tr > td,
.table-condensed > tfoot > tr > td {
  padding: 5px;
}
.table-bordered {
  border: 1px solid #ddd;
}
.table-bordered > thead > tr > th,
.table-bordered > tbody > tr > th,
.table-bordered > tfoot > tr > th,
.table-bordered > thead > tr > td,
.table-bordered > tbody > tr > td,
.table-bordered > tfoot > tr > td {
  border: 1px solid #ddd;
}
.table-bordered > thead > tr > th,
.table-bordered > thead > tr > td {
  border-bottom-width: 2px;
}
.table-striped > tbody > tr:nth-of-type(odd) {
  background-color: #f9f9f9;
}
.table-hover > tbody > tr:hover {
  background-color: #f5f5f5;
}
table col[class*="col-"] {
  position: static;
  float: none;
  display: table-column;
}
table td[class*="col-"],
table th[class*="col-"] {
  position: static;
  float: none;
  display: table-cell;
}
.table > thead > tr > td.active,
.table > tbody > tr > td.active,
.table > tfoot > tr > td.active,
.table > thead > tr > th.active,
.table > tbody > tr > th.active,
.table > tfoot > tr > th.active,
.table > thead > tr.active > td,
.table > tbody > tr.active > td,
.table > tfoot > tr.active > td,
.table > thead > tr.active > th,
.table > tbody > tr.active > th,
.table > tfoot > tr.active > th {
  background-color: #f5f5f5;
}
.table-hover > tbody > tr > td.active:hover,
.table-hover > tbody > tr > th.active:hover,
.table-hover > tbody > tr.active:hover > td,
.table-hover > tbody > tr:hover > .active,
.table-hover > tbody > tr.active:hover > th {
  background-color: #e8e8e8;
}
.table > thead > tr > td.success,
.table > tbody > tr > td.success,
.table > tfoot > tr > td.success,
.table > thead > tr > th.success,
.table > tbody > tr > th.success,
.table > tfoot > tr > th.success,
.table > thead > tr.success > td,
.table > tbody > tr.success > td,
.table > tfoot > tr.success > td,
.table > thead > tr.success > th,
.table > tbody > tr.success > th,
.table > tfoot > tr.success > th {
  background-color: #dff0d8;
}
.table-hover > tbody > tr > td.success:hover,
.table-hover > tbody > tr > th.success:hover,
.table-hover > tbody > tr.success:hover > td,
.table-hover > tbody > tr:hover > .success,
.table-hover > tbody > tr.success:hover > th {
  background-color: #d0e9c6;
}
.table > thead > tr > td.info,
.table > tbody > tr > td.info,
.table > tfoot > tr > td.info,
.table > thead > tr > th.info,
.table > tbody > tr > th.info,
.table > tfoot > tr > th.info,
.table > thead > tr.info > td,
.table > tbody > tr.info > td,
.table > tfoot > tr.info > td,
.table > thead > tr.info > th,
.table > tbody > tr.info > th,
.table > tfoot > tr.info > th {
  background-color: #d9edf7;
}
.table-hover > tbody > tr > td.info:hover,
.table-hover > tbody > tr > th.info:hover,
.table-hover > tbody > tr.info:hover > td,
.table-hover > tbody > tr:hover > .info,
.table-hover > tbody > tr.info:hover > th {
  background-color: #c4e3f3;
}
.table > thead > tr > td.warning,
.table > tbody > tr > td.warning,
.table > tfoot > tr > td.warning,
.table > thead > tr > th.warning,
.table > tbody > tr > th.warning,
.table > tfoot > tr > th.warning,
.table > thead > tr.warning > td,
.table > tbody > tr.warning > td,
.table > tfoot > tr.warning > td,
.table > thead > tr.warning > th,
.table > tbody > tr.warning > th,
.table > tfoot > tr.warning > th {
  background-color: #fcf8e3;
}
.table-hover > tbody > tr > td.warning:hover,
.table-hover > tbody > tr > th.warning:hover,
.table-hover > tbody > tr.warning:hover > td,
.table-hover > tbody > tr:hover > .warning,
.table-hover > tbody > tr.warning:hover > th {
  background-color: #faf2cc;
}
.table > thead > tr > td.danger,
.table > tbody > tr > td.danger,
.table > tfoot > tr > td.danger,
.table > thead > tr > th.danger,
.table > tbody > tr > th.danger,
.table > tfoot > tr > th.danger,
.table > thead > tr.danger > td,
.table > tbody > tr.danger > td,
.table > tfoot > tr.danger > td,
.table > thead > tr.danger > th,
.table > tbody > tr.danger > th,
.table > tfoot > tr.danger > th {
  background-color: #f2dede;
}
.table-hover > tbody > tr > td.danger:hover,
.table-hover > tbody > tr > th.danger:hover,
.table-hover > tbody > tr.danger:hover > td,
.table-hover > tbody > tr:hover > .danger,
.table-hover > tbody > tr.danger:hover > th {
  background-color: #ebcccc;
}
.table-responsive {
  overflow-x: auto;
  min-height: 0.01%;
}
@media screen and (max-width: 767px) {
  .table-responsive {
    width: 100%;
    margin-bottom: 13.5px;
    overflow-y: hidden;
    -ms-overflow-style: -ms-autohiding-scrollbar;
    border: 1px solid #ddd;
  }
  .table-responsive > .table {
    margin-bottom: 0;
  }
  .table-responsive > .table > thead > tr > th,
  .table-responsive > .table > tbody > tr > th,
  .table-responsive > .table > tfoot > tr > th,
  .table-responsive > .table > thead > tr > td,
  .table-responsive > .table > tbody > tr > td,
  .table-responsive > .table > tfoot > tr > td {
    white-space: nowrap;
  }
  .table-responsive > .table-bordered {
    border: 0;
  }
  .table-responsive > .table-bordered > thead > tr > th:first-child,
  .table-responsive > .table-bordered > tbody > tr > th:first-child,
  .table-responsive > .table-bordered > tfoot > tr > th:first-child,
  .table-responsive > .table-bordered > thead > tr > td:first-child,
  .table-responsive > .table-bordered > tbody > tr > td:first-child,
  .table-responsive > .table-bordered > tfoot > tr > td:first-child {
    border-left: 0;
  }
  .table-responsive > .table-bordered > thead > tr > th:last-child,
  .table-responsive > .table-bordered > tbody > tr > th:last-child,
  .table-responsive > .table-bordered > tfoot > tr > th:last-child,
  .table-responsive > .table-bordered > thead > tr > td:last-child,
  .table-responsive > .table-bordered > tbody > tr > td:last-child,
  .table-responsive > .table-bordered > tfoot > tr > td:last-child {
    border-right: 0;
  }
  .table-responsive > .table-bordered > tbody > tr:last-child > th,
  .table-responsive > .table-bordered > tfoot > tr:last-child > th,
  .table-responsive > .table-bordered > tbody > tr:last-child > td,
  .table-responsive > .table-bordered > tfoot > tr:last-child > td {
    border-bottom: 0;
  }
}
fieldset {
  padding: 0;
  margin: 0;
  border: 0;
  min-width: 0;
}
legend {
  display: block;
  width: 100%;
  padding: 0;
  margin-bottom: 18px;
  font-size: 19.5px;
  line-height: inherit;
  color: #333333;
  border: 0;
  border-bottom: 1px solid #e5e5e5;
}
label {
  display: inline-block;
  max-width: 100%;
  margin-bottom: 5px;
  font-weight: bold;
}
input[type="search"] {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
input[type="radio"],
input[type="checkbox"] {
  margin: 4px 0 0;
  margin-top: 1px \9;
  line-height: normal;
}
input[type="file"] {
  display: block;
}
input[type="range"] {
  display: block;
  width: 100%;
}
select[multiple],
select[size] {
  height: auto;
}
input[type="file"]:focus,
input[type="radio"]:focus,
input[type="checkbox"]:focus {
  outline: thin dotted;
  outline: 5px auto -webkit-focus-ring-color;
  outline-offset: -2px;
}
output {
  display: block;
  padding-top: 7px;
  font-size: 13px;
  line-height: 1.42857143;
  color: #555555;
}
.form-control {
  display: block;
  width: 100%;
  height: 32px;
  padding: 6px 12px;
  font-size: 13px;
  line-height: 1.42857143;
  color: #555555;
  background-color: #fff;
  background-image: none;
  border: 1px solid #ccc;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  -webkit-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  -o-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
}
.form-control:focus {
  border-color: #66afe9;
  outline: 0;
  -webkit-box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
  box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
}
.form-control::-moz-placeholder {
  color: #999;
  opacity: 1;
}
.form-control:-ms-input-placeholder {
  color: #999;
}
.form-control::-webkit-input-placeholder {
  color: #999;
}
.form-control::-ms-expand {
  border: 0;
  background-color: transparent;
}
.form-control[disabled],
.form-control[readonly],
fieldset[disabled] .form-control {
  background-color: #eeeeee;
  opacity: 1;
}
.form-control[disabled],
fieldset[disabled] .form-control {
  cursor: not-allowed;
}
textarea.form-control {
  height: auto;
}
input[type="search"] {
  -webkit-appearance: none;
}
@media screen and (-webkit-min-device-pixel-ratio: 0) {
  input[type="date"].form-control,
  input[type="time"].form-control,
  input[type="datetime-local"].form-control,
  input[type="month"].form-control {
    line-height: 32px;
  }
  input[type="date"].input-sm,
  input[type="time"].input-sm,
  input[type="datetime-local"].input-sm,
  input[type="month"].input-sm,
  .input-group-sm input[type="date"],
  .input-group-sm input[type="time"],
  .input-group-sm input[type="datetime-local"],
  .input-group-sm input[type="month"] {
    line-height: 30px;
  }
  input[type="date"].input-lg,
  input[type="time"].input-lg,
  input[type="datetime-local"].input-lg,
  input[type="month"].input-lg,
  .input-group-lg input[type="date"],
  .input-group-lg input[type="time"],
  .input-group-lg input[type="datetime-local"],
  .input-group-lg input[type="month"] {
    line-height: 45px;
  }
}
.form-group {
  margin-bottom: 15px;
}
.radio,
.checkbox {
  position: relative;
  display: block;
  margin-top: 10px;
  margin-bottom: 10px;
}
.radio label,
.checkbox label {
  min-height: 18px;
  padding-left: 20px;
  margin-bottom: 0;
  font-weight: normal;
  cursor: pointer;
}
.radio input[type="radio"],
.radio-inline input[type="radio"],
.checkbox input[type="checkbox"],
.checkbox-inline input[type="checkbox"] {
  position: absolute;
  margin-left: -20px;
  margin-top: 4px \9;
}
.radio + .radio,
.checkbox + .checkbox {
  margin-top: -5px;
}
.radio-inline,
.checkbox-inline {
  position: relative;
  display: inline-block;
  padding-left: 20px;
  margin-bottom: 0;
  vertical-align: middle;
  font-weight: normal;
  cursor: pointer;
}
.radio-inline + .radio-inline,
.checkbox-inline + .checkbox-inline {
  margin-top: 0;
  margin-left: 10px;
}
input[type="radio"][disabled],
input[type="checkbox"][disabled],
input[type="radio"].disabled,
input[type="checkbox"].disabled,
fieldset[disabled] input[type="radio"],
fieldset[disabled] input[type="checkbox"] {
  cursor: not-allowed;
}
.radio-inline.disabled,
.checkbox-inline.disabled,
fieldset[disabled] .radio-inline,
fieldset[disabled] .checkbox-inline {
  cursor: not-allowed;
}
.radio.disabled label,
.checkbox.disabled label,
fieldset[disabled] .radio label,
fieldset[disabled] .checkbox label {
  cursor: not-allowed;
}
.form-control-static {
  padding-top: 7px;
  padding-bottom: 7px;
  margin-bottom: 0;
  min-height: 31px;
}
.form-control-static.input-lg,
.form-control-static.input-sm {
  padding-left: 0;
  padding-right: 0;
}
.input-sm {
  height: 30px;
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
select.input-sm {
  height: 30px;
  line-height: 30px;
}
textarea.input-sm,
select[multiple].input-sm {
  height: auto;
}
.form-group-sm .form-control {
  height: 30px;
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
.form-group-sm select.form-control {
  height: 30px;
  line-height: 30px;
}
.form-group-sm textarea.form-control,
.form-group-sm select[multiple].form-control {
  height: auto;
}
.form-group-sm .form-control-static {
  height: 30px;
  min-height: 30px;
  padding: 6px 10px;
  font-size: 12px;
  line-height: 1.5;
}
.input-lg {
  height: 45px;
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
  border-radius: 3px;
}
select.input-lg {
  height: 45px;
  line-height: 45px;
}
textarea.input-lg,
select[multiple].input-lg {
  height: auto;
}
.form-group-lg .form-control {
  height: 45px;
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
  border-radius: 3px;
}
.form-group-lg select.form-control {
  height: 45px;
  line-height: 45px;
}
.form-group-lg textarea.form-control,
.form-group-lg select[multiple].form-control {
  height: auto;
}
.form-group-lg .form-control-static {
  height: 45px;
  min-height: 35px;
  padding: 11px 16px;
  font-size: 17px;
  line-height: 1.3333333;
}
.has-feedback {
  position: relative;
}
.has-feedback .form-control {
  padding-right: 40px;
}
.form-control-feedback {
  position: absolute;
  top: 0;
  right: 0;
  z-index: 2;
  display: block;
  width: 32px;
  height: 32px;
  line-height: 32px;
  text-align: center;
  pointer-events: none;
}
.input-lg + .form-control-feedback,
.input-group-lg + .form-control-feedback,
.form-group-lg .form-control + .form-control-feedback {
  width: 45px;
  height: 45px;
  line-height: 45px;
}
.input-sm + .form-control-feedback,
.input-group-sm + .form-control-feedback,
.form-group-sm .form-control + .form-control-feedback {
  width: 30px;
  height: 30px;
  line-height: 30px;
}
.has-success .help-block,
.has-success .control-label,
.has-success .radio,
.has-success .checkbox,
.has-success .radio-inline,
.has-success .checkbox-inline,
.has-success.radio label,
.has-success.checkbox label,
.has-success.radio-inline label,
.has-success.checkbox-inline label {
  color: #3c763d;
}
.has-success .form-control {
  border-color: #3c763d;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
}
.has-success .form-control:focus {
  border-color: #2b542c;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #67b168;
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #67b168;
}
.has-success .input-group-addon {
  color: #3c763d;
  border-color: #3c763d;
  background-color: #dff0d8;
}
.has-success .form-control-feedback {
  color: #3c763d;
}
.has-warning .help-block,
.has-warning .control-label,
.has-warning .radio,
.has-warning .checkbox,
.has-warning .radio-inline,
.has-warning .checkbox-inline,
.has-warning.radio label,
.has-warning.checkbox label,
.has-warning.radio-inline label,
.has-warning.checkbox-inline label {
  color: #8a6d3b;
}
.has-warning .form-control {
  border-color: #8a6d3b;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
}
.has-warning .form-control:focus {
  border-color: #66512c;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #c0a16b;
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #c0a16b;
}
.has-warning .input-group-addon {
  color: #8a6d3b;
  border-color: #8a6d3b;
  background-color: #fcf8e3;
}
.has-warning .form-control-feedback {
  color: #8a6d3b;
}
.has-error .help-block,
.has-error .control-label,
.has-error .radio,
.has-error .checkbox,
.has-error .radio-inline,
.has-error .checkbox-inline,
.has-error.radio label,
.has-error.checkbox label,
.has-error.radio-inline label,
.has-error.checkbox-inline label {
  color: #a94442;
}
.has-error .form-control {
  border-color: #a94442;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
}
.has-error .form-control:focus {
  border-color: #843534;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #ce8483;
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #ce8483;
}
.has-error .input-group-addon {
  color: #a94442;
  border-color: #a94442;
  background-color: #f2dede;
}
.has-error .form-control-feedback {
  color: #a94442;
}
.has-feedback label ~ .form-control-feedback {
  top: 23px;
}
.has-feedback label.sr-only ~ .form-control-feedback {
  top: 0;
}
.help-block {
  display: block;
  margin-top: 5px;
  margin-bottom: 10px;
  color: #404040;
}
@media (min-width: 768px) {
  .form-inline .form-group {
    display: inline-block;
    margin-bottom: 0;
    vertical-align: middle;
  }
  .form-inline .form-control {
    display: inline-block;
    width: auto;
    vertical-align: middle;
  }
  .form-inline .form-control-static {
    display: inline-block;
  }
  .form-inline .input-group {
    display: inline-table;
    vertical-align: middle;
  }
  .form-inline .input-group .input-group-addon,
  .form-inline .input-group .input-group-btn,
  .form-inline .input-group .form-control {
    width: auto;
  }
  .form-inline .input-group > .form-control {
    width: 100%;
  }
  .form-inline .control-label {
    margin-bottom: 0;
    vertical-align: middle;
  }
  .form-inline .radio,
  .form-inline .checkbox {
    display: inline-block;
    margin-top: 0;
    margin-bottom: 0;
    vertical-align: middle;
  }
  .form-inline .radio label,
  .form-inline .checkbox label {
    padding-left: 0;
  }
  .form-inline .radio input[type="radio"],
  .form-inline .checkbox input[type="checkbox"] {
    position: relative;
    margin-left: 0;
  }
  .form-inline .has-feedback .form-control-feedback {
    top: 0;
  }
}
.form-horizontal .radio,
.form-horizontal .checkbox,
.form-horizontal .radio-inline,
.form-horizontal .checkbox-inline {
  margin-top: 0;
  margin-bottom: 0;
  padding-top: 7px;
}
.form-horizontal .radio,
.form-horizontal .checkbox {
  min-height: 25px;
}
.form-horizontal .form-group {
  margin-left: 0px;
  margin-right: 0px;
}
@media (min-width: 768px) {
  .form-horizontal .control-label {
    text-align: right;
    margin-bottom: 0;
    padding-top: 7px;
  }
}
.form-horizontal .has-feedback .form-control-feedback {
  right: 0px;
}
@media (min-width: 768px) {
  .form-horizontal .form-group-lg .control-label {
    padding-top: 11px;
    font-size: 17px;
  }
}
@media (min-width: 768px) {
  .form-horizontal .form-group-sm .control-label {
    padding-top: 6px;
    font-size: 12px;
  }
}
.btn {
  display: inline-block;
  margin-bottom: 0;
  font-weight: normal;
  text-align: center;
  vertical-align: middle;
  touch-action: manipulation;
  cursor: pointer;
  background-image: none;
  border: 1px solid transparent;
  white-space: nowrap;
  padding: 6px 12px;
  font-size: 13px;
  line-height: 1.42857143;
  border-radius: 2px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.btn:focus,
.btn:active:focus,
.btn.active:focus,
.btn.focus,
.btn:active.focus,
.btn.active.focus {
  outline: thin dotted;
  outline: 5px auto -webkit-focus-ring-color;
  outline-offset: -2px;
}
.btn:hover,
.btn:focus,
.btn.focus {
  color: #333;
  text-decoration: none;
}
.btn:active,
.btn.active {
  outline: 0;
  background-image: none;
  -webkit-box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
  box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
}
.btn.disabled,
.btn[disabled],
fieldset[disabled] .btn {
  cursor: not-allowed;
  opacity: 0.65;
  filter: alpha(opacity=65);
  -webkit-box-shadow: none;
  box-shadow: none;
}
a.btn.disabled,
fieldset[disabled] a.btn {
  pointer-events: none;
}
.btn-default {
  color: #333;
  background-color: #fff;
  border-color: #ccc;
}
.btn-default:focus,
.btn-default.focus {
  color: #333;
  background-color: #e6e6e6;
  border-color: #8c8c8c;
}
.btn-default:hover {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
.btn-default:active,
.btn-default.active,
.open > .dropdown-toggle.btn-default {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
.btn-default:active:hover,
.btn-default.active:hover,
.open > .dropdown-toggle.btn-default:hover,
.btn-default:active:focus,
.btn-default.active:focus,
.open > .dropdown-toggle.btn-default:focus,
.btn-default:active.focus,
.btn-default.active.focus,
.open > .dropdown-toggle.btn-default.focus {
  color: #333;
  background-color: #d4d4d4;
  border-color: #8c8c8c;
}
.btn-default:active,
.btn-default.active,
.open > .dropdown-toggle.btn-default {
  background-image: none;
}
.btn-default.disabled:hover,
.btn-default[disabled]:hover,
fieldset[disabled] .btn-default:hover,
.btn-default.disabled:focus,
.btn-default[disabled]:focus,
fieldset[disabled] .btn-default:focus,
.btn-default.disabled.focus,
.btn-default[disabled].focus,
fieldset[disabled] .btn-default.focus {
  background-color: #fff;
  border-color: #ccc;
}
.btn-default .badge {
  color: #fff;
  background-color: #333;
}
.btn-primary {
  color: #fff;
  background-color: #337ab7;
  border-color: #2e6da4;
}
.btn-primary:focus,
.btn-primary.focus {
  color: #fff;
  background-color: #286090;
  border-color: #122b40;
}
.btn-primary:hover {
  color: #fff;
  background-color: #286090;
  border-color: #204d74;
}
.btn-primary:active,
.btn-primary.active,
.open > .dropdown-toggle.btn-primary {
  color: #fff;
  background-color: #286090;
  border-color: #204d74;
}
.btn-primary:active:hover,
.btn-primary.active:hover,
.open > .dropdown-toggle.btn-primary:hover,
.btn-primary:active:focus,
.btn-primary.active:focus,
.open > .dropdown-toggle.btn-primary:focus,
.btn-primary:active.focus,
.btn-primary.active.focus,
.open > .dropdown-toggle.btn-primary.focus {
  color: #fff;
  background-color: #204d74;
  border-color: #122b40;
}
.btn-primary:active,
.btn-primary.active,
.open > .dropdown-toggle.btn-primary {
  background-image: none;
}
.btn-primary.disabled:hover,
.btn-primary[disabled]:hover,
fieldset[disabled] .btn-primary:hover,
.btn-primary.disabled:focus,
.btn-primary[disabled]:focus,
fieldset[disabled] .btn-primary:focus,
.btn-primary.disabled.focus,
.btn-primary[disabled].focus,
fieldset[disabled] .btn-primary.focus {
  background-color: #337ab7;
  border-color: #2e6da4;
}
.btn-primary .badge {
  color: #337ab7;
  background-color: #fff;
}
.btn-success {
  color: #fff;
  background-color: #5cb85c;
  border-color: #4cae4c;
}
.btn-success:focus,
.btn-success.focus {
  color: #fff;
  background-color: #449d44;
  border-color: #255625;
}
.btn-success:hover {
  color: #fff;
  background-color: #449d44;
  border-color: #398439;
}
.btn-success:active,
.btn-success.active,
.open > .dropdown-toggle.btn-success {
  color: #fff;
  background-color: #449d44;
  border-color: #398439;
}
.btn-success:active:hover,
.btn-success.active:hover,
.open > .dropdown-toggle.btn-success:hover,
.btn-success:active:focus,
.btn-success.active:focus,
.open > .dropdown-toggle.btn-success:focus,
.btn-success:active.focus,
.btn-success.active.focus,
.open > .dropdown-toggle.btn-success.focus {
  color: #fff;
  background-color: #398439;
  border-color: #255625;
}
.btn-success:active,
.btn-success.active,
.open > .dropdown-toggle.btn-success {
  background-image: none;
}
.btn-success.disabled:hover,
.btn-success[disabled]:hover,
fieldset[disabled] .btn-success:hover,
.btn-success.disabled:focus,
.btn-success[disabled]:focus,
fieldset[disabled] .btn-success:focus,
.btn-success.disabled.focus,
.btn-success[disabled].focus,
fieldset[disabled] .btn-success.focus {
  background-color: #5cb85c;
  border-color: #4cae4c;
}
.btn-success .badge {
  color: #5cb85c;
  background-color: #fff;
}
.btn-info {
  color: #fff;
  background-color: #5bc0de;
  border-color: #46b8da;
}
.btn-info:focus,
.btn-info.focus {
  color: #fff;
  background-color: #31b0d5;
  border-color: #1b6d85;
}
.btn-info:hover {
  color: #fff;
  background-color: #31b0d5;
  border-color: #269abc;
}
.btn-info:active,
.btn-info.active,
.open > .dropdown-toggle.btn-info {
  color: #fff;
  background-color: #31b0d5;
  border-color: #269abc;
}
.btn-info:active:hover,
.btn-info.active:hover,
.open > .dropdown-toggle.btn-info:hover,
.btn-info:active:focus,
.btn-info.active:focus,
.open > .dropdown-toggle.btn-info:focus,
.btn-info:active.focus,
.btn-info.active.focus,
.open > .dropdown-toggle.btn-info.focus {
  color: #fff;
  background-color: #269abc;
  border-color: #1b6d85;
}
.btn-info:active,
.btn-info.active,
.open > .dropdown-toggle.btn-info {
  background-image: none;
}
.btn-info.disabled:hover,
.btn-info[disabled]:hover,
fieldset[disabled] .btn-info:hover,
.btn-info.disabled:focus,
.btn-info[disabled]:focus,
fieldset[disabled] .btn-info:focus,
.btn-info.disabled.focus,
.btn-info[disabled].focus,
fieldset[disabled] .btn-info.focus {
  background-color: #5bc0de;
  border-color: #46b8da;
}
.btn-info .badge {
  color: #5bc0de;
  background-color: #fff;
}
.btn-warning {
  color: #fff;
  background-color: #f0ad4e;
  border-color: #eea236;
}
.btn-warning:focus,
.btn-warning.focus {
  color: #fff;
  background-color: #ec971f;
  border-color: #985f0d;
}
.btn-warning:hover {
  color: #fff;
  background-color: #ec971f;
  border-color: #d58512;
}
.btn-warning:active,
.btn-warning.active,
.open > .dropdown-toggle.btn-warning {
  color: #fff;
  background-color: #ec971f;
  border-color: #d58512;
}
.btn-warning:active:hover,
.btn-warning.active:hover,
.open > .dropdown-toggle.btn-warning:hover,
.btn-warning:active:focus,
.btn-warning.active:focus,
.open > .dropdown-toggle.btn-warning:focus,
.btn-warning:active.focus,
.btn-warning.active.focus,
.open > .dropdown-toggle.btn-warning.focus {
  color: #fff;
  background-color: #d58512;
  border-color: #985f0d;
}
.btn-warning:active,
.btn-warning.active,
.open > .dropdown-toggle.btn-warning {
  background-image: none;
}
.btn-warning.disabled:hover,
.btn-warning[disabled]:hover,
fieldset[disabled] .btn-warning:hover,
.btn-warning.disabled:focus,
.btn-warning[disabled]:focus,
fieldset[disabled] .btn-warning:focus,
.btn-warning.disabled.focus,
.btn-warning[disabled].focus,
fieldset[disabled] .btn-warning.focus {
  background-color: #f0ad4e;
  border-color: #eea236;
}
.btn-warning .badge {
  color: #f0ad4e;
  background-color: #fff;
}
.btn-danger {
  color: #fff;
  background-color: #d9534f;
  border-color: #d43f3a;
}
.btn-danger:focus,
.btn-danger.focus {
  color: #fff;
  background-color: #c9302c;
  border-color: #761c19;
}
.btn-danger:hover {
  color: #fff;
  background-color: #c9302c;
  border-color: #ac2925;
}
.btn-danger:active,
.btn-danger.active,
.open > .dropdown-toggle.btn-danger {
  color: #fff;
  background-color: #c9302c;
  border-color: #ac2925;
}
.btn-danger:active:hover,
.btn-danger.active:hover,
.open > .dropdown-toggle.btn-danger:hover,
.btn-danger:active:focus,
.btn-danger.active:focus,
.open > .dropdown-toggle.btn-danger:focus,
.btn-danger:active.focus,
.btn-danger.active.focus,
.open > .dropdown-toggle.btn-danger.focus {
  color: #fff;
  background-color: #ac2925;
  border-color: #761c19;
}
.btn-danger:active,
.btn-danger.active,
.open > .dropdown-toggle.btn-danger {
  background-image: none;
}
.btn-danger.disabled:hover,
.btn-danger[disabled]:hover,
fieldset[disabled] .btn-danger:hover,
.btn-danger.disabled:focus,
.btn-danger[disabled]:focus,
fieldset[disabled] .btn-danger:focus,
.btn-danger.disabled.focus,
.btn-danger[disabled].focus,
fieldset[disabled] .btn-danger.focus {
  background-color: #d9534f;
  border-color: #d43f3a;
}
.btn-danger .badge {
  color: #d9534f;
  background-color: #fff;
}
.btn-link {
  color: #337ab7;
  font-weight: normal;
  border-radius: 0;
}
.btn-link,
.btn-link:active,
.btn-link.active,
.btn-link[disabled],
fieldset[disabled] .btn-link {
  background-color: transparent;
  -webkit-box-shadow: none;
  box-shadow: none;
}
.btn-link,
.btn-link:hover,
.btn-link:focus,
.btn-link:active {
  border-color: transparent;
}
.btn-link:hover,
.btn-link:focus {
  color: #23527c;
  text-decoration: underline;
  background-color: transparent;
}
.btn-link[disabled]:hover,
fieldset[disabled] .btn-link:hover,
.btn-link[disabled]:focus,
fieldset[disabled] .btn-link:focus {
  color: #777777;
  text-decoration: none;
}
.btn-lg,
.btn-group-lg > .btn {
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
  border-radius: 3px;
}
.btn-sm,
.btn-group-sm > .btn {
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
.btn-xs,
.btn-group-xs > .btn {
  padding: 1px 5px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
.btn-block {
  display: block;
  width: 100%;
}
.btn-block + .btn-block {
  margin-top: 5px;
}
input[type="submit"].btn-block,
input[type="reset"].btn-block,
input[type="button"].btn-block {
  width: 100%;
}
.fade {
  opacity: 0;
  -webkit-transition: opacity 0.15s linear;
  -o-transition: opacity 0.15s linear;
  transition: opacity 0.15s linear;
}
.fade.in {
  opacity: 1;
}
.collapse {
  display: none;
}
.collapse.in {
  display: block;
}
tr.collapse.in {
  display: table-row;
}
tbody.collapse.in {
  display: table-row-group;
}
.collapsing {
  position: relative;
  height: 0;
  overflow: hidden;
  -webkit-transition-property: height, visibility;
  transition-property: height, visibility;
  -webkit-transition-duration: 0.35s;
  transition-duration: 0.35s;
  -webkit-transition-timing-function: ease;
  transition-timing-function: ease;
}
.caret {
  display: inline-block;
  width: 0;
  height: 0;
  margin-left: 2px;
  vertical-align: middle;
  border-top: 4px dashed;
  border-top: 4px solid \9;
  border-right: 4px solid transparent;
  border-left: 4px solid transparent;
}
.dropup,
.dropdown {
  position: relative;
}
.dropdown-toggle:focus {
  outline: 0;
}
.dropdown-menu {
  position: absolute;
  top: 100%;
  left: 0;
  z-index: 1000;
  display: none;
  float: left;
  min-width: 160px;
  padding: 5px 0;
  margin: 2px 0 0;
  list-style: none;
  font-size: 13px;
  text-align: left;
  background-color: #fff;
  border: 1px solid #ccc;
  border: 1px solid rgba(0, 0, 0, 0.15);
  border-radius: 2px;
  -webkit-box-shadow: 0 6px 12px rgba(0, 0, 0, 0.175);
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.175);
  background-clip: padding-box;
}
.dropdown-menu.pull-right {
  right: 0;
  left: auto;
}
.dropdown-menu .divider {
  height: 1px;
  margin: 8px 0;
  overflow: hidden;
  background-color: #e5e5e5;
}
.dropdown-menu > li > a {
  display: block;
  padding: 3px 20px;
  clear: both;
  font-weight: normal;
  line-height: 1.42857143;
  color: #333333;
  white-space: nowrap;
}
.dropdown-menu > li > a:hover,
.dropdown-menu > li > a:focus {
  text-decoration: none;
  color: #262626;
  background-color: #f5f5f5;
}
.dropdown-menu > .active > a,
.dropdown-menu > .active > a:hover,
.dropdown-menu > .active > a:focus {
  color: #fff;
  text-decoration: none;
  outline: 0;
  background-color: #337ab7;
}
.dropdown-menu > .disabled > a,
.dropdown-menu > .disabled > a:hover,
.dropdown-menu > .disabled > a:focus {
  color: #777777;
}
.dropdown-menu > .disabled > a:hover,
.dropdown-menu > .disabled > a:focus {
  text-decoration: none;
  background-color: transparent;
  background-image: none;
  filter: progid:DXImageTransform.Microsoft.gradient(enabled = false);
  cursor: not-allowed;
}
.open > .dropdown-menu {
  display: block;
}
.open > a {
  outline: 0;
}
.dropdown-menu-right {
  left: auto;
  right: 0;
}
.dropdown-menu-left {
  left: 0;
  right: auto;
}
.dropdown-header {
  display: block;
  padding: 3px 20px;
  font-size: 12px;
  line-height: 1.42857143;
  color: #777777;
  white-space: nowrap;
}
.dropdown-backdrop {
  position: fixed;
  left: 0;
  right: 0;
  bottom: 0;
  top: 0;
  z-index: 990;
}
.pull-right > .dropdown-menu {
  right: 0;
  left: auto;
}
.dropup .caret,
.navbar-fixed-bottom .dropdown .caret {
  border-top: 0;
  border-bottom: 4px dashed;
  border-bottom: 4px solid \9;
  content: "";
}
.dropup .dropdown-menu,
.navbar-fixed-bottom .dropdown .dropdown-menu {
  top: auto;
  bottom: 100%;
  margin-bottom: 2px;
}
@media (min-width: 541px) {
  .navbar-right .dropdown-menu {
    left: auto;
    right: 0;
  }
  .navbar-right .dropdown-menu-left {
    left: 0;
    right: auto;
  }
}
.btn-group,
.btn-group-vertical {
  position: relative;
  display: inline-block;
  vertical-align: middle;
}
.btn-group > .btn,
.btn-group-vertical > .btn {
  position: relative;
  float: left;
}
.btn-group > .btn:hover,
.btn-group-vertical > .btn:hover,
.btn-group > .btn:focus,
.btn-group-vertical > .btn:focus,
.btn-group > .btn:active,
.btn-group-vertical > .btn:active,
.btn-group > .btn.active,
.btn-group-vertical > .btn.active {
  z-index: 2;
}
.btn-group .btn + .btn,
.btn-group .btn + .btn-group,
.btn-group .btn-group + .btn,
.btn-group .btn-group + .btn-group {
  margin-left: -1px;
}
.btn-toolbar {
  margin-left: -5px;
}
.btn-toolbar .btn,
.btn-toolbar .btn-group,
.btn-toolbar .input-group {
  float: left;
}
.btn-toolbar > .btn,
.btn-toolbar > .btn-group,
.btn-toolbar > .input-group {
  margin-left: 5px;
}
.btn-group > .btn:not(:first-child):not(:last-child):not(.dropdown-toggle) {
  border-radius: 0;
}
.btn-group > .btn:first-child {
  margin-left: 0;
}
.btn-group > .btn:first-child:not(:last-child):not(.dropdown-toggle) {
  border-bottom-right-radius: 0;
  border-top-right-radius: 0;
}
.btn-group > .btn:last-child:not(:first-child),
.btn-group > .dropdown-toggle:not(:first-child) {
  border-bottom-left-radius: 0;
  border-top-left-radius: 0;
}
.btn-group > .btn-group {
  float: left;
}
.btn-group > .btn-group:not(:first-child):not(:last-child) > .btn {
  border-radius: 0;
}
.btn-group > .btn-group:first-child:not(:last-child) > .btn:last-child,
.btn-group > .btn-group:first-child:not(:last-child) > .dropdown-toggle {
  border-bottom-right-radius: 0;
  border-top-right-radius: 0;
}
.btn-group > .btn-group:last-child:not(:first-child) > .btn:first-child {
  border-bottom-left-radius: 0;
  border-top-left-radius: 0;
}
.btn-group .dropdown-toggle:active,
.btn-group.open .dropdown-toggle {
  outline: 0;
}
.btn-group > .btn + .dropdown-toggle {
  padding-left: 8px;
  padding-right: 8px;
}
.btn-group > .btn-lg + .dropdown-toggle {
  padding-left: 12px;
  padding-right: 12px;
}
.btn-group.open .dropdown-toggle {
  -webkit-box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
  box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
}
.btn-group.open .dropdown-toggle.btn-link {
  -webkit-box-shadow: none;
  box-shadow: none;
}
.btn .caret {
  margin-left: 0;
}
.btn-lg .caret {
  border-width: 5px 5px 0;
  border-bottom-width: 0;
}
.dropup .btn-lg .caret {
  border-width: 0 5px 5px;
}
.btn-group-vertical > .btn,
.btn-group-vertical > .btn-group,
.btn-group-vertical > .btn-group > .btn {
  display: block;
  float: none;
  width: 100%;
  max-width: 100%;
}
.btn-group-vertical > .btn-group > .btn {
  float: none;
}
.btn-group-vertical > .btn + .btn,
.btn-group-vertical > .btn + .btn-group,
.btn-group-vertical > .btn-group + .btn,
.btn-group-vertical > .btn-group + .btn-group {
  margin-top: -1px;
  margin-left: 0;
}
.btn-group-vertical > .btn:not(:first-child):not(:last-child) {
  border-radius: 0;
}
.btn-group-vertical > .btn:first-child:not(:last-child) {
  border-top-right-radius: 2px;
  border-top-left-radius: 2px;
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}
.btn-group-vertical > .btn:last-child:not(:first-child) {
  border-top-right-radius: 0;
  border-top-left-radius: 0;
  border-bottom-right-radius: 2px;
  border-bottom-left-radius: 2px;
}
.btn-group-vertical > .btn-group:not(:first-child):not(:last-child) > .btn {
  border-radius: 0;
}
.btn-group-vertical > .btn-group:first-child:not(:last-child) > .btn:last-child,
.btn-group-vertical > .btn-group:first-child:not(:last-child) > .dropdown-toggle {
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}
.btn-group-vertical > .btn-group:last-child:not(:first-child) > .btn:first-child {
  border-top-right-radius: 0;
  border-top-left-radius: 0;
}
.btn-group-justified {
  display: table;
  width: 100%;
  table-layout: fixed;
  border-collapse: separate;
}
.btn-group-justified > .btn,
.btn-group-justified > .btn-group {
  float: none;
  display: table-cell;
  width: 1%;
}
.btn-group-justified > .btn-group .btn {
  width: 100%;
}
.btn-group-justified > .btn-group .dropdown-menu {
  left: auto;
}
[data-toggle="buttons"] > .btn input[type="radio"],
[data-toggle="buttons"] > .btn-group > .btn input[type="radio"],
[data-toggle="buttons"] > .btn input[type="checkbox"],
[data-toggle="buttons"] > .btn-group > .btn input[type="checkbox"] {
  position: absolute;
  clip: rect(0, 0, 0, 0);
  pointer-events: none;
}
.input-group {
  position: relative;
  display: table;
  border-collapse: separate;
}
.input-group[class*="col-"] {
  float: none;
  padding-left: 0;
  padding-right: 0;
}
.input-group .form-control {
  position: relative;
  z-index: 2;
  float: left;
  width: 100%;
  margin-bottom: 0;
}
.input-group .form-control:focus {
  z-index: 3;
}
.input-group-lg > .form-control,
.input-group-lg > .input-group-addon,
.input-group-lg > .input-group-btn > .btn {
  height: 45px;
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
  border-radius: 3px;
}
select.input-group-lg > .form-control,
select.input-group-lg > .input-group-addon,
select.input-group-lg > .input-group-btn > .btn {
  height: 45px;
  line-height: 45px;
}
textarea.input-group-lg > .form-control,
textarea.input-group-lg > .input-group-addon,
textarea.input-group-lg > .input-group-btn > .btn,
select[multiple].input-group-lg > .form-control,
select[multiple].input-group-lg > .input-group-addon,
select[multiple].input-group-lg > .input-group-btn > .btn {
  height: auto;
}
.input-group-sm > .form-control,
.input-group-sm > .input-group-addon,
.input-group-sm > .input-group-btn > .btn {
  height: 30px;
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
select.input-group-sm > .form-control,
select.input-group-sm > .input-group-addon,
select.input-group-sm > .input-group-btn > .btn {
  height: 30px;
  line-height: 30px;
}
textarea.input-group-sm > .form-control,
textarea.input-group-sm > .input-group-addon,
textarea.input-group-sm > .input-group-btn > .btn,
select[multiple].input-group-sm > .form-control,
select[multiple].input-group-sm > .input-group-addon,
select[multiple].input-group-sm > .input-group-btn > .btn {
  height: auto;
}
.input-group-addon,
.input-group-btn,
.input-group .form-control {
  display: table-cell;
}
.input-group-addon:not(:first-child):not(:last-child),
.input-group-btn:not(:first-child):not(:last-child),
.input-group .form-control:not(:first-child):not(:last-child) {
  border-radius: 0;
}
.input-group-addon,
.input-group-btn {
  width: 1%;
  white-space: nowrap;
  vertical-align: middle;
}
.input-group-addon {
  padding: 6px 12px;
  font-size: 13px;
  font-weight: normal;
  line-height: 1;
  color: #555555;
  text-align: center;
  background-color: #eeeeee;
  border: 1px solid #ccc;
  border-radius: 2px;
}
.input-group-addon.input-sm {
  padding: 5px 10px;
  font-size: 12px;
  border-radius: 1px;
}
.input-group-addon.input-lg {
  padding: 10px 16px;
  font-size: 17px;
  border-radius: 3px;
}
.input-group-addon input[type="radio"],
.input-group-addon input[type="checkbox"] {
  margin-top: 0;
}
.input-group .form-control:first-child,
.input-group-addon:first-child,
.input-group-btn:first-child > .btn,
.input-group-btn:first-child > .btn-group > .btn,
.input-group-btn:first-child > .dropdown-toggle,
.input-group-btn:last-child > .btn:not(:last-child):not(.dropdown-toggle),
.input-group-btn:last-child > .btn-group:not(:last-child) > .btn {
  border-bottom-right-radius: 0;
  border-top-right-radius: 0;
}
.input-group-addon:first-child {
  border-right: 0;
}
.input-group .form-control:last-child,
.input-group-addon:last-child,
.input-group-btn:last-child > .btn,
.input-group-btn:last-child > .btn-group > .btn,
.input-group-btn:last-child > .dropdown-toggle,
.input-group-btn:first-child > .btn:not(:first-child),
.input-group-btn:first-child > .btn-group:not(:first-child) > .btn {
  border-bottom-left-radius: 0;
  border-top-left-radius: 0;
}
.input-group-addon:last-child {
  border-left: 0;
}
.input-group-btn {
  position: relative;
  font-size: 0;
  white-space: nowrap;
}
.input-group-btn > .btn {
  position: relative;
}
.input-group-btn > .btn + .btn {
  margin-left: -1px;
}
.input-group-btn > .btn:hover,
.input-group-btn > .btn:focus,
.input-group-btn > .btn:active {
  z-index: 2;
}
.input-group-btn:first-child > .btn,
.input-group-btn:first-child > .btn-group {
  margin-right: -1px;
}
.input-group-btn:last-child > .btn,
.input-group-btn:last-child > .btn-group {
  z-index: 2;
  margin-left: -1px;
}
.nav {
  margin-bottom: 0;
  padding-left: 0;
  list-style: none;
}
.nav > li {
  position: relative;
  display: block;
}
.nav > li > a {
  position: relative;
  display: block;
  padding: 10px 15px;
}
.nav > li > a:hover,
.nav > li > a:focus {
  text-decoration: none;
  background-color: #eeeeee;
}
.nav > li.disabled > a {
  color: #777777;
}
.nav > li.disabled > a:hover,
.nav > li.disabled > a:focus {
  color: #777777;
  text-decoration: none;
  background-color: transparent;
  cursor: not-allowed;
}
.nav .open > a,
.nav .open > a:hover,
.nav .open > a:focus {
  background-color: #eeeeee;
  border-color: #337ab7;
}
.nav .nav-divider {
  height: 1px;
  margin: 8px 0;
  overflow: hidden;
  background-color: #e5e5e5;
}
.nav > li > a > img {
  max-width: none;
}
.nav-tabs {
  border-bottom: 1px solid #ddd;
}
.nav-tabs > li {
  float: left;
  margin-bottom: -1px;
}
.nav-tabs > li > a {
  margin-right: 2px;
  line-height: 1.42857143;
  border: 1px solid transparent;
  border-radius: 2px 2px 0 0;
}
.nav-tabs > li > a:hover {
  border-color: #eeeeee #eeeeee #ddd;
}
.nav-tabs > li.active > a,
.nav-tabs > li.active > a:hover,
.nav-tabs > li.active > a:focus {
  color: #555555;
  background-color: #fff;
  border: 1px solid #ddd;
  border-bottom-color: transparent;
  cursor: default;
}
.nav-tabs.nav-justified {
  width: 100%;
  border-bottom: 0;
}
.nav-tabs.nav-justified > li {
  float: none;
}
.nav-tabs.nav-justified > li > a {
  text-align: center;
  margin-bottom: 5px;
}
.nav-tabs.nav-justified > .dropdown .dropdown-menu {
  top: auto;
  left: auto;
}
@media (min-width: 768px) {
  .nav-tabs.nav-justified > li {
    display: table-cell;
    width: 1%;
  }
  .nav-tabs.nav-justified > li > a {
    margin-bottom: 0;
  }
}
.nav-tabs.nav-justified > li > a {
  margin-right: 0;
  border-radius: 2px;
}
.nav-tabs.nav-justified > .active > a,
.nav-tabs.nav-justified > .active > a:hover,
.nav-tabs.nav-justified > .active > a:focus {
  border: 1px solid #ddd;
}
@media (min-width: 768px) {
  .nav-tabs.nav-justified > li > a {
    border-bottom: 1px solid #ddd;
    border-radius: 2px 2px 0 0;
  }
  .nav-tabs.nav-justified > .active > a,
  .nav-tabs.nav-justified > .active > a:hover,
  .nav-tabs.nav-justified > .active > a:focus {
    border-bottom-color: #fff;
  }
}
.nav-pills > li {
  float: left;
}
.nav-pills > li > a {
  border-radius: 2px;
}
.nav-pills > li + li {
  margin-left: 2px;
}
.nav-pills > li.active > a,
.nav-pills > li.active > a:hover,
.nav-pills > li.active > a:focus {
  color: #fff;
  background-color: #337ab7;
}
.nav-stacked > li {
  float: none;
}
.nav-stacked > li + li {
  margin-top: 2px;
  margin-left: 0;
}
.nav-justified {
  width: 100%;
}
.nav-justified > li {
  float: none;
}
.nav-justified > li > a {
  text-align: center;
  margin-bottom: 5px;
}
.nav-justified > .dropdown .dropdown-menu {
  top: auto;
  left: auto;
}
@media (min-width: 768px) {
  .nav-justified > li {
    display: table-cell;
    width: 1%;
  }
  .nav-justified > li > a {
    margin-bottom: 0;
  }
}
.nav-tabs-justified {
  border-bottom: 0;
}
.nav-tabs-justified > li > a {
  margin-right: 0;
  border-radius: 2px;
}
.nav-tabs-justified > .active > a,
.nav-tabs-justified > .active > a:hover,
.nav-tabs-justified > .active > a:focus {
  border: 1px solid #ddd;
}
@media (min-width: 768px) {
  .nav-tabs-justified > li > a {
    border-bottom: 1px solid #ddd;
    border-radius: 2px 2px 0 0;
  }
  .nav-tabs-justified > .active > a,
  .nav-tabs-justified > .active > a:hover,
  .nav-tabs-justified > .active > a:focus {
    border-bottom-color: #fff;
  }
}
.tab-content > .tab-pane {
  display: none;
}
.tab-content > .active {
  display: block;
}
.nav-tabs .dropdown-menu {
  margin-top: -1px;
  border-top-right-radius: 0;
  border-top-left-radius: 0;
}
.navbar {
  position: relative;
  min-height: 30px;
  margin-bottom: 18px;
  border: 1px solid transparent;
}
@media (min-width: 541px) {
  .navbar {
    border-radius: 2px;
  }
}
@media (min-width: 541px) {
  .navbar-header {
    float: left;
  }
}
.navbar-collapse {
  overflow-x: visible;
  padding-right: 0px;
  padding-left: 0px;
  border-top: 1px solid transparent;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.1);
  -webkit-overflow-scrolling: touch;
}
.navbar-collapse.in {
  overflow-y: auto;
}
@media (min-width: 541px) {
  .navbar-collapse {
    width: auto;
    border-top: 0;
    box-shadow: none;
  }
  .navbar-collapse.collapse {
    display: block !important;
    height: auto !important;
    padding-bottom: 0;
    overflow: visible !important;
  }
  .navbar-collapse.in {
    overflow-y: visible;
  }
  .navbar-fixed-top .navbar-collapse,
  .navbar-static-top .navbar-collapse,
  .navbar-fixed-bottom .navbar-collapse {
    padding-left: 0;
    padding-right: 0;
  }
}
.navbar-fixed-top .navbar-collapse,
.navbar-fixed-bottom .navbar-collapse {
  max-height: 340px;
}
@media (max-device-width: 540px) and (orientation: landscape) {
  .navbar-fixed-top .navbar-collapse,
  .navbar-fixed-bottom .navbar-collapse {
    max-height: 200px;
  }
}
.container > .navbar-header,
.container-fluid > .navbar-header,
.container > .navbar-collapse,
.container-fluid > .navbar-collapse {
  margin-right: 0px;
  margin-left: 0px;
}
@media (min-width: 541px) {
  .container > .navbar-header,
  .container-fluid > .navbar-header,
  .container > .navbar-collapse,
  .container-fluid > .navbar-collapse {
    margin-right: 0;
    margin-left: 0;
  }
}
.navbar-static-top {
  z-index: 1000;
  border-width: 0 0 1px;
}
@media (min-width: 541px) {
  .navbar-static-top {
    border-radius: 0;
  }
}
.navbar-fixed-top,
.navbar-fixed-bottom {
  position: fixed;
  right: 0;
  left: 0;
  z-index: 1030;
}
@media (min-width: 541px) {
  .navbar-fixed-top,
  .navbar-fixed-bottom {
    border-radius: 0;
  }
}
.navbar-fixed-top {
  top: 0;
  border-width: 0 0 1px;
}
.navbar-fixed-bottom {
  bottom: 0;
  margin-bottom: 0;
  border-width: 1px 0 0;
}
.navbar-brand {
  float: left;
  padding: 6px 0px;
  font-size: 17px;
  line-height: 18px;
  height: 30px;
}
.navbar-brand:hover,
.navbar-brand:focus {
  text-decoration: none;
}
.navbar-brand > img {
  display: block;
}
@media (min-width: 541px) {
  .navbar > .container .navbar-brand,
  .navbar > .container-fluid .navbar-brand {
    margin-left: 0px;
  }
}
.navbar-toggle {
  position: relative;
  float: right;
  margin-right: 0px;
  padding: 9px 10px;
  margin-top: -2px;
  margin-bottom: -2px;
  background-color: transparent;
  background-image: none;
  border: 1px solid transparent;
  border-radius: 2px;
}
.navbar-toggle:focus {
  outline: 0;
}
.navbar-toggle .icon-bar {
  display: block;
  width: 22px;
  height: 2px;
  border-radius: 1px;
}
.navbar-toggle .icon-bar + .icon-bar {
  margin-top: 4px;
}
@media (min-width: 541px) {
  .navbar-toggle {
    display: none;
  }
}
.navbar-nav {
  margin: 3px 0px;
}
.navbar-nav > li > a {
  padding-top: 10px;
  padding-bottom: 10px;
  line-height: 18px;
}
@media (max-width: 540px) {
  .navbar-nav .open .dropdown-menu {
    position: static;
    float: none;
    width: auto;
    margin-top: 0;
    background-color: transparent;
    border: 0;
    box-shadow: none;
  }
  .navbar-nav .open .dropdown-menu > li > a,
  .navbar-nav .open .dropdown-menu .dropdown-header {
    padding: 5px 15px 5px 25px;
  }
  .navbar-nav .open .dropdown-menu > li > a {
    line-height: 18px;
  }
  .navbar-nav .open .dropdown-menu > li > a:hover,
  .navbar-nav .open .dropdown-menu > li > a:focus {
    background-image: none;
  }
}
@media (min-width: 541px) {
  .navbar-nav {
    float: left;
    margin: 0;
  }
  .navbar-nav > li {
    float: left;
  }
  .navbar-nav > li > a {
    padding-top: 6px;
    padding-bottom: 6px;
  }
}
.navbar-form {
  margin-left: 0px;
  margin-right: 0px;
  padding: 10px 0px;
  border-top: 1px solid transparent;
  border-bottom: 1px solid transparent;
  -webkit-box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.1), 0 1px 0 rgba(255, 255, 255, 0.1);
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.1), 0 1px 0 rgba(255, 255, 255, 0.1);
  margin-top: -1px;
  margin-bottom: -1px;
}
@media (min-width: 768px) {
  .navbar-form .form-group {
    display: inline-block;
    margin-bottom: 0;
    vertical-align: middle;
  }
  .navbar-form .form-control {
    display: inline-block;
    width: auto;
    vertical-align: middle;
  }
  .navbar-form .form-control-static {
    display: inline-block;
  }
  .navbar-form .input-group {
    display: inline-table;
    vertical-align: middle;
  }
  .navbar-form .input-group .input-group-addon,
  .navbar-form .input-group .input-group-btn,
  .navbar-form .input-group .form-control {
    width: auto;
  }
  .navbar-form .input-group > .form-control {
    width: 100%;
  }
  .navbar-form .control-label {
    margin-bottom: 0;
    vertical-align: middle;
  }
  .navbar-form .radio,
  .navbar-form .checkbox {
    display: inline-block;
    margin-top: 0;
    margin-bottom: 0;
    vertical-align: middle;
  }
  .navbar-form .radio label,
  .navbar-form .checkbox label {
    padding-left: 0;
  }
  .navbar-form .radio input[type="radio"],
  .navbar-form .checkbox input[type="checkbox"] {
    position: relative;
    margin-left: 0;
  }
  .navbar-form .has-feedback .form-control-feedback {
    top: 0;
  }
}
@media (max-width: 540px) {
  .navbar-form .form-group {
    margin-bottom: 5px;
  }
  .navbar-form .form-group:last-child {
    margin-bottom: 0;
  }
}
@media (min-width: 541px) {
  .navbar-form {
    width: auto;
    border: 0;
    margin-left: 0;
    margin-right: 0;
    padding-top: 0;
    padding-bottom: 0;
    -webkit-box-shadow: none;
    box-shadow: none;
  }
}
.navbar-nav > li > .dropdown-menu {
  margin-top: 0;
  border-top-right-radius: 0;
  border-top-left-radius: 0;
}
.navbar-fixed-bottom .navbar-nav > li > .dropdown-menu {
  margin-bottom: 0;
  border-top-right-radius: 2px;
  border-top-left-radius: 2px;
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}
.navbar-btn {
  margin-top: -1px;
  margin-bottom: -1px;
}
.navbar-btn.btn-sm {
  margin-top: 0px;
  margin-bottom: 0px;
}
.navbar-btn.btn-xs {
  margin-top: 4px;
  margin-bottom: 4px;
}
.navbar-text {
  margin-top: 6px;
  margin-bottom: 6px;
}
@media (min-width: 541px) {
  .navbar-text {
    float: left;
    margin-left: 0px;
    margin-right: 0px;
  }
}
@media (min-width: 541px) {
  .navbar-left {
    float: left !important;
    float: left;
  }
  .navbar-right {
    float: right !important;
    float: right;
    margin-right: 0px;
  }
  .navbar-right ~ .navbar-right {
    margin-right: 0;
  }
}
.navbar-default {
  background-color: #f8f8f8;
  border-color: #e7e7e7;
}
.navbar-default .navbar-brand {
  color: #777;
}
.navbar-default .navbar-brand:hover,
.navbar-default .navbar-brand:focus {
  color: #5e5e5e;
  background-color: transparent;
}
.navbar-default .navbar-text {
  color: #777;
}
.navbar-default .navbar-nav > li > a {
  color: #777;
}
.navbar-default .navbar-nav > li > a:hover,
.navbar-default .navbar-nav > li > a:focus {
  color: #333;
  background-color: transparent;
}
.navbar-default .navbar-nav > .active > a,
.navbar-default .navbar-nav > .active > a:hover,
.navbar-default .navbar-nav > .active > a:focus {
  color: #555;
  background-color: #e7e7e7;
}
.navbar-default .navbar-nav > .disabled > a,
.navbar-default .navbar-nav > .disabled > a:hover,
.navbar-default .navbar-nav > .disabled > a:focus {
  color: #ccc;
  background-color: transparent;
}
.navbar-default .navbar-toggle {
  border-color: #ddd;
}
.navbar-default .navbar-toggle:hover,
.navbar-default .navbar-toggle:focus {
  background-color: #ddd;
}
.navbar-default .navbar-toggle .icon-bar {
  background-color: #888;
}
.navbar-default .navbar-collapse,
.navbar-default .navbar-form {
  border-color: #e7e7e7;
}
.navbar-default .navbar-nav > .open > a,
.navbar-default .navbar-nav > .open > a:hover,
.navbar-default .navbar-nav > .open > a:focus {
  background-color: #e7e7e7;
  color: #555;
}
@media (max-width: 540px) {
  .navbar-default .navbar-nav .open .dropdown-menu > li > a {
    color: #777;
  }
  .navbar-default .navbar-nav .open .dropdown-menu > li > a:hover,
  .navbar-default .navbar-nav .open .dropdown-menu > li > a:focus {
    color: #333;
    background-color: transparent;
  }
  .navbar-default .navbar-nav .open .dropdown-menu > .active > a,
  .navbar-default .navbar-nav .open .dropdown-menu > .active > a:hover,
  .navbar-default .navbar-nav .open .dropdown-menu > .active > a:focus {
    color: #555;
    background-color: #e7e7e7;
  }
  .navbar-default .navbar-nav .open .dropdown-menu > .disabled > a,
  .navbar-default .navbar-nav .open .dropdown-menu > .disabled > a:hover,
  .navbar-default .navbar-nav .open .dropdown-menu > .disabled > a:focus {
    color: #ccc;
    background-color: transparent;
  }
}
.navbar-default .navbar-link {
  color: #777;
}
.navbar-default .navbar-link:hover {
  color: #333;
}
.navbar-default .btn-link {
  color: #777;
}
.navbar-default .btn-link:hover,
.navbar-default .btn-link:focus {
  color: #333;
}
.navbar-default .btn-link[disabled]:hover,
fieldset[disabled] .navbar-default .btn-link:hover,
.navbar-default .btn-link[disabled]:focus,
fieldset[disabled] .navbar-default .btn-link:focus {
  color: #ccc;
}
.navbar-inverse {
  background-color: #222;
  border-color: #080808;
}
.navbar-inverse .navbar-brand {
  color: #9d9d9d;
}
.navbar-inverse .navbar-brand:hover,
.navbar-inverse .navbar-brand:focus {
  color: #fff;
  background-color: transparent;
}
.navbar-inverse .navbar-text {
  color: #9d9d9d;
}
.navbar-inverse .navbar-nav > li > a {
  color: #9d9d9d;
}
.navbar-inverse .navbar-nav > li > a:hover,
.navbar-inverse .navbar-nav > li > a:focus {
  color: #fff;
  background-color: transparent;
}
.navbar-inverse .navbar-nav > .active > a,
.navbar-inverse .navbar-nav > .active > a:hover,
.navbar-inverse .navbar-nav > .active > a:focus {
  color: #fff;
  background-color: #080808;
}
.navbar-inverse .navbar-nav > .disabled > a,
.navbar-inverse .navbar-nav > .disabled > a:hover,
.navbar-inverse .navbar-nav > .disabled > a:focus {
  color: #444;
  background-color: transparent;
}
.navbar-inverse .navbar-toggle {
  border-color: #333;
}
.navbar-inverse .navbar-toggle:hover,
.navbar-inverse .navbar-toggle:focus {
  background-color: #333;
}
.navbar-inverse .navbar-toggle .icon-bar {
  background-color: #fff;
}
.navbar-inverse .navbar-collapse,
.navbar-inverse .navbar-form {
  border-color: #101010;
}
.navbar-inverse .navbar-nav > .open > a,
.navbar-inverse .navbar-nav > .open > a:hover,
.navbar-inverse .navbar-nav > .open > a:focus {
  background-color: #080808;
  color: #fff;
}
@media (max-width: 540px) {
  .navbar-inverse .navbar-nav .open .dropdown-menu > .dropdown-header {
    border-color: #080808;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu .divider {
    background-color: #080808;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu > li > a {
    color: #9d9d9d;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu > li > a:hover,
  .navbar-inverse .navbar-nav .open .dropdown-menu > li > a:focus {
    color: #fff;
    background-color: transparent;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu > .active > a,
  .navbar-inverse .navbar-nav .open .dropdown-menu > .active > a:hover,
  .navbar-inverse .navbar-nav .open .dropdown-menu > .active > a:focus {
    color: #fff;
    background-color: #080808;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu > .disabled > a,
  .navbar-inverse .navbar-nav .open .dropdown-menu > .disabled > a:hover,
  .navbar-inverse .navbar-nav .open .dropdown-menu > .disabled > a:focus {
    color: #444;
    background-color: transparent;
  }
}
.navbar-inverse .navbar-link {
  color: #9d9d9d;
}
.navbar-inverse .navbar-link:hover {
  color: #fff;
}
.navbar-inverse .btn-link {
  color: #9d9d9d;
}
.navbar-inverse .btn-link:hover,
.navbar-inverse .btn-link:focus {
  color: #fff;
}
.navbar-inverse .btn-link[disabled]:hover,
fieldset[disabled] .navbar-inverse .btn-link:hover,
.navbar-inverse .btn-link[disabled]:focus,
fieldset[disabled] .navbar-inverse .btn-link:focus {
  color: #444;
}
.breadcrumb {
  padding: 8px 15px;
  margin-bottom: 18px;
  list-style: none;
  background-color: #f5f5f5;
  border-radius: 2px;
}
.breadcrumb > li {
  display: inline-block;
}
.breadcrumb > li + li:before {
  content: "/\00a0";
  padding: 0 5px;
  color: #5e5e5e;
}
.breadcrumb > .active {
  color: #777777;
}
.pagination {
  display: inline-block;
  padding-left: 0;
  margin: 18px 0;
  border-radius: 2px;
}
.pagination > li {
  display: inline;
}
.pagination > li > a,
.pagination > li > span {
  position: relative;
  float: left;
  padding: 6px 12px;
  line-height: 1.42857143;
  text-decoration: none;
  color: #337ab7;
  background-color: #fff;
  border: 1px solid #ddd;
  margin-left: -1px;
}
.pagination > li:first-child > a,
.pagination > li:first-child > span {
  margin-left: 0;
  border-bottom-left-radius: 2px;
  border-top-left-radius: 2px;
}
.pagination > li:last-child > a,
.pagination > li:last-child > span {
  border-bottom-right-radius: 2px;
  border-top-right-radius: 2px;
}
.pagination > li > a:hover,
.pagination > li > span:hover,
.pagination > li > a:focus,
.pagination > li > span:focus {
  z-index: 2;
  color: #23527c;
  background-color: #eeeeee;
  border-color: #ddd;
}
.pagination > .active > a,
.pagination > .active > span,
.pagination > .active > a:hover,
.pagination > .active > span:hover,
.pagination > .active > a:focus,
.pagination > .active > span:focus {
  z-index: 3;
  color: #fff;
  background-color: #337ab7;
  border-color: #337ab7;
  cursor: default;
}
.pagination > .disabled > span,
.pagination > .disabled > span:hover,
.pagination > .disabled > span:focus,
.pagination > .disabled > a,
.pagination > .disabled > a:hover,
.pagination > .disabled > a:focus {
  color: #777777;
  background-color: #fff;
  border-color: #ddd;
  cursor: not-allowed;
}
.pagination-lg > li > a,
.pagination-lg > li > span {
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
}
.pagination-lg > li:first-child > a,
.pagination-lg > li:first-child > span {
  border-bottom-left-radius: 3px;
  border-top-left-radius: 3px;
}
.pagination-lg > li:last-child > a,
.pagination-lg > li:last-child > span {
  border-bottom-right-radius: 3px;
  border-top-right-radius: 3px;
}
.pagination-sm > li > a,
.pagination-sm > li > span {
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
}
.pagination-sm > li:first-child > a,
.pagination-sm > li:first-child > span {
  border-bottom-left-radius: 1px;
  border-top-left-radius: 1px;
}
.pagination-sm > li:last-child > a,
.pagination-sm > li:last-child > span {
  border-bottom-right-radius: 1px;
  border-top-right-radius: 1px;
}
.pager {
  padding-left: 0;
  margin: 18px 0;
  list-style: none;
  text-align: center;
}
.pager li {
  display: inline;
}
.pager li > a,
.pager li > span {
  display: inline-block;
  padding: 5px 14px;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 15px;
}
.pager li > a:hover,
.pager li > a:focus {
  text-decoration: none;
  background-color: #eeeeee;
}
.pager .next > a,
.pager .next > span {
  float: right;
}
.pager .previous > a,
.pager .previous > span {
  float: left;
}
.pager .disabled > a,
.pager .disabled > a:hover,
.pager .disabled > a:focus,
.pager .disabled > span {
  color: #777777;
  background-color: #fff;
  cursor: not-allowed;
}
.label {
  display: inline;
  padding: .2em .6em .3em;
  font-size: 75%;
  font-weight: bold;
  line-height: 1;
  color: #fff;
  text-align: center;
  white-space: nowrap;
  vertical-align: baseline;
  border-radius: .25em;
}
a.label:hover,
a.label:focus {
  color: #fff;
  text-decoration: none;
  cursor: pointer;
}
.label:empty {
  display: none;
}
.btn .label {
  position: relative;
  top: -1px;
}
.label-default {
  background-color: #777777;
}
.label-default[href]:hover,
.label-default[href]:focus {
  background-color: #5e5e5e;
}
.label-primary {
  background-color: #337ab7;
}
.label-primary[href]:hover,
.label-primary[href]:focus {
  background-color: #286090;
}
.label-success {
  background-color: #5cb85c;
}
.label-success[href]:hover,
.label-success[href]:focus {
  background-color: #449d44;
}
.label-info {
  background-color: #5bc0de;
}
.label-info[href]:hover,
.label-info[href]:focus {
  background-color: #31b0d5;
}
.label-warning {
  background-color: #f0ad4e;
}
.label-warning[href]:hover,
.label-warning[href]:focus {
  background-color: #ec971f;
}
.label-danger {
  background-color: #d9534f;
}
.label-danger[href]:hover,
.label-danger[href]:focus {
  background-color: #c9302c;
}
.badge {
  display: inline-block;
  min-width: 10px;
  padding: 3px 7px;
  font-size: 12px;
  font-weight: bold;
  color: #fff;
  line-height: 1;
  vertical-align: middle;
  white-space: nowrap;
  text-align: center;
  background-color: #777777;
  border-radius: 10px;
}
.badge:empty {
  display: none;
}
.btn .badge {
  position: relative;
  top: -1px;
}
.btn-xs .badge,
.btn-group-xs > .btn .badge {
  top: 0;
  padding: 1px 5px;
}
a.badge:hover,
a.badge:focus {
  color: #fff;
  text-decoration: none;
  cursor: pointer;
}
.list-group-item.active > .badge,
.nav-pills > .active > a > .badge {
  color: #337ab7;
  background-color: #fff;
}
.list-group-item > .badge {
  float: right;
}
.list-group-item > .badge + .badge {
  margin-right: 5px;
}
.nav-pills > li > a > .badge {
  margin-left: 3px;
}
.jumbotron {
  padding-top: 30px;
  padding-bottom: 30px;
  margin-bottom: 30px;
  color: inherit;
  background-color: #eeeeee;
}
.jumbotron h1,
.jumbotron .h1 {
  color: inherit;
}
.jumbotron p {
  margin-bottom: 15px;
  font-size: 20px;
  font-weight: 200;
}
.jumbotron > hr {
  border-top-color: #d5d5d5;
}
.container .jumbotron,
.container-fluid .jumbotron {
  border-radius: 3px;
  padding-left: 0px;
  padding-right: 0px;
}
.jumbotron .container {
  max-width: 100%;
}
@media screen and (min-width: 768px) {
  .jumbotron {
    padding-top: 48px;
    padding-bottom: 48px;
  }
  .container .jumbotron,
  .container-fluid .jumbotron {
    padding-left: 60px;
    padding-right: 60px;
  }
  .jumbotron h1,
  .jumbotron .h1 {
    font-size: 59px;
  }
}
.thumbnail {
  display: block;
  padding: 4px;
  margin-bottom: 18px;
  line-height: 1.42857143;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 2px;
  -webkit-transition: border 0.2s ease-in-out;
  -o-transition: border 0.2s ease-in-out;
  transition: border 0.2s ease-in-out;
}
.thumbnail > img,
.thumbnail a > img {
  margin-left: auto;
  margin-right: auto;
}
a.thumbnail:hover,
a.thumbnail:focus,
a.thumbnail.active {
  border-color: #337ab7;
}
.thumbnail .caption {
  padding: 9px;
  color: #000;
}
.alert {
  padding: 15px;
  margin-bottom: 18px;
  border: 1px solid transparent;
  border-radius: 2px;
}
.alert h4 {
  margin-top: 0;
  color: inherit;
}
.alert .alert-link {
  font-weight: bold;
}
.alert > p,
.alert > ul {
  margin-bottom: 0;
}
.alert > p + p {
  margin-top: 5px;
}
.alert-dismissable,
.alert-dismissible {
  padding-right: 35px;
}
.alert-dismissable .close,
.alert-dismissible .close {
  position: relative;
  top: -2px;
  right: -21px;
  color: inherit;
}
.alert-success {
  background-color: #dff0d8;
  border-color: #d6e9c6;
  color: #3c763d;
}
.alert-success hr {
  border-top-color: #c9e2b3;
}
.alert-success .alert-link {
  color: #2b542c;
}
.alert-info {
  background-color: #d9edf7;
  border-color: #bce8f1;
  color: #31708f;
}
.alert-info hr {
  border-top-color: #a6e1ec;
}
.alert-info .alert-link {
  color: #245269;
}
.alert-warning {
  background-color: #fcf8e3;
  border-color: #faebcc;
  color: #8a6d3b;
}
.alert-warning hr {
  border-top-color: #f7e1b5;
}
.alert-warning .alert-link {
  color: #66512c;
}
.alert-danger {
  background-color: #f2dede;
  border-color: #ebccd1;
  color: #a94442;
}
.alert-danger hr {
  border-top-color: #e4b9c0;
}
.alert-danger .alert-link {
  color: #843534;
}
@-webkit-keyframes progress-bar-stripes {
  from {
    background-position: 40px 0;
  }
  to {
    background-position: 0 0;
  }
}
@keyframes progress-bar-stripes {
  from {
    background-position: 40px 0;
  }
  to {
    background-position: 0 0;
  }
}
.progress {
  overflow: hidden;
  height: 18px;
  margin-bottom: 18px;
  background-color: #f5f5f5;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 1px 2px rgba(0, 0, 0, 0.1);
  box-shadow: inset 0 1px 2px rgba(0, 0, 0, 0.1);
}
.progress-bar {
  float: left;
  width: 0%;
  height: 100%;
  font-size: 12px;
  line-height: 18px;
  color: #fff;
  text-align: center;
  background-color: #337ab7;
  -webkit-box-shadow: inset 0 -1px 0 rgba(0, 0, 0, 0.15);
  box-shadow: inset 0 -1px 0 rgba(0, 0, 0, 0.15);
  -webkit-transition: width 0.6s ease;
  -o-transition: width 0.6s ease;
  transition: width 0.6s ease;
}
.progress-striped .progress-bar,
.progress-bar-striped {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-size: 40px 40px;
}
.progress.active .progress-bar,
.progress-bar.active {
  -webkit-animation: progress-bar-stripes 2s linear infinite;
  -o-animation: progress-bar-stripes 2s linear infinite;
  animation: progress-bar-stripes 2s linear infinite;
}
.progress-bar-success {
  background-color: #5cb85c;
}
.progress-striped .progress-bar-success {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
}
.progress-bar-info {
  background-color: #5bc0de;
}
.progress-striped .progress-bar-info {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
}
.progress-bar-warning {
  background-color: #f0ad4e;
}
.progress-striped .progress-bar-warning {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
}
.progress-bar-danger {
  background-color: #d9534f;
}
.progress-striped .progress-bar-danger {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
}
.media {
  margin-top: 15px;
}
.media:first-child {
  margin-top: 0;
}
.media,
.media-body {
  zoom: 1;
  overflow: hidden;
}
.media-body {
  width: 10000px;
}
.media-object {
  display: block;
}
.media-object.img-thumbnail {
  max-width: none;
}
.media-right,
.media > .pull-right {
  padding-left: 10px;
}
.media-left,
.media > .pull-left {
  padding-right: 10px;
}
.media-left,
.media-right,
.media-body {
  display: table-cell;
  vertical-align: top;
}
.media-middle {
  vertical-align: middle;
}
.media-bottom {
  vertical-align: bottom;
}
.media-heading {
  margin-top: 0;
  margin-bottom: 5px;
}
.media-list {
  padding-left: 0;
  list-style: none;
}
.list-group {
  margin-bottom: 20px;
  padding-left: 0;
}
.list-group-item {
  position: relative;
  display: block;
  padding: 10px 15px;
  margin-bottom: -1px;
  background-color: #fff;
  border: 1px solid #ddd;
}
.list-group-item:first-child {
  border-top-right-radius: 2px;
  border-top-left-radius: 2px;
}
.list-group-item:last-child {
  margin-bottom: 0;
  border-bottom-right-radius: 2px;
  border-bottom-left-radius: 2px;
}
a.list-group-item,
button.list-group-item {
  color: #555;
}
a.list-group-item .list-group-item-heading,
button.list-group-item .list-group-item-heading {
  color: #333;
}
a.list-group-item:hover,
button.list-group-item:hover,
a.list-group-item:focus,
button.list-group-item:focus {
  text-decoration: none;
  color: #555;
  background-color: #f5f5f5;
}
button.list-group-item {
  width: 100%;
  text-align: left;
}
.list-group-item.disabled,
.list-group-item.disabled:hover,
.list-group-item.disabled:focus {
  background-color: #eeeeee;
  color: #777777;
  cursor: not-allowed;
}
.list-group-item.disabled .list-group-item-heading,
.list-group-item.disabled:hover .list-group-item-heading,
.list-group-item.disabled:focus .list-group-item-heading {
  color: inherit;
}
.list-group-item.disabled .list-group-item-text,
.list-group-item.disabled:hover .list-group-item-text,
.list-group-item.disabled:focus .list-group-item-text {
  color: #777777;
}
.list-group-item.active,
.list-group-item.active:hover,
.list-group-item.active:focus {
  z-index: 2;
  color: #fff;
  background-color: #337ab7;
  border-color: #337ab7;
}
.list-group-item.active .list-group-item-heading,
.list-group-item.active:hover .list-group-item-heading,
.list-group-item.active:focus .list-group-item-heading,
.list-group-item.active .list-group-item-heading > small,
.list-group-item.active:hover .list-group-item-heading > small,
.list-group-item.active:focus .list-group-item-heading > small,
.list-group-item.active .list-group-item-heading > .small,
.list-group-item.active:hover .list-group-item-heading > .small,
.list-group-item.active:focus .list-group-item-heading > .small {
  color: inherit;
}
.list-group-item.active .list-group-item-text,
.list-group-item.active:hover .list-group-item-text,
.list-group-item.active:focus .list-group-item-text {
  color: #c7ddef;
}
.list-group-item-success {
  color: #3c763d;
  background-color: #dff0d8;
}
a.list-group-item-success,
button.list-group-item-success {
  color: #3c763d;
}
a.list-group-item-success .list-group-item-heading,
button.list-group-item-success .list-group-item-heading {
  color: inherit;
}
a.list-group-item-success:hover,
button.list-group-item-success:hover,
a.list-group-item-success:focus,
button.list-group-item-success:focus {
  color: #3c763d;
  background-color: #d0e9c6;
}
a.list-group-item-success.active,
button.list-group-item-success.active,
a.list-group-item-success.active:hover,
button.list-group-item-success.active:hover,
a.list-group-item-success.active:focus,
button.list-group-item-success.active:focus {
  color: #fff;
  background-color: #3c763d;
  border-color: #3c763d;
}
.list-group-item-info {
  color: #31708f;
  background-color: #d9edf7;
}
a.list-group-item-info,
button.list-group-item-info {
  color: #31708f;
}
a.list-group-item-info .list-group-item-heading,
button.list-group-item-info .list-group-item-heading {
  color: inherit;
}
a.list-group-item-info:hover,
button.list-group-item-info:hover,
a.list-group-item-info:focus,
button.list-group-item-info:focus {
  color: #31708f;
  background-color: #c4e3f3;
}
a.list-group-item-info.active,
button.list-group-item-info.active,
a.list-group-item-info.active:hover,
button.list-group-item-info.active:hover,
a.list-group-item-info.active:focus,
button.list-group-item-info.active:focus {
  color: #fff;
  background-color: #31708f;
  border-color: #31708f;
}
.list-group-item-warning {
  color: #8a6d3b;
  background-color: #fcf8e3;
}
a.list-group-item-warning,
button.list-group-item-warning {
  color: #8a6d3b;
}
a.list-group-item-warning .list-group-item-heading,
button.list-group-item-warning .list-group-item-heading {
  color: inherit;
}
a.list-group-item-warning:hover,
button.list-group-item-warning:hover,
a.list-group-item-warning:focus,
button.list-group-item-warning:focus {
  color: #8a6d3b;
  background-color: #faf2cc;
}
a.list-group-item-warning.active,
button.list-group-item-warning.active,
a.list-group-item-warning.active:hover,
button.list-group-item-warning.active:hover,
a.list-group-item-warning.active:focus,
button.list-group-item-warning.active:focus {
  color: #fff;
  background-color: #8a6d3b;
  border-color: #8a6d3b;
}
.list-group-item-danger {
  color: #a94442;
  background-color: #f2dede;
}
a.list-group-item-danger,
button.list-group-item-danger {
  color: #a94442;
}
a.list-group-item-danger .list-group-item-heading,
button.list-group-item-danger .list-group-item-heading {
  color: inherit;
}
a.list-group-item-danger:hover,
button.list-group-item-danger:hover,
a.list-group-item-danger:focus,
button.list-group-item-danger:focus {
  color: #a94442;
  background-color: #ebcccc;
}
a.list-group-item-danger.active,
button.list-group-item-danger.active,
a.list-group-item-danger.active:hover,
button.list-group-item-danger.active:hover,
a.list-group-item-danger.active:focus,
button.list-group-item-danger.active:focus {
  color: #fff;
  background-color: #a94442;
  border-color: #a94442;
}
.list-group-item-heading {
  margin-top: 0;
  margin-bottom: 5px;
}
.list-group-item-text {
  margin-bottom: 0;
  line-height: 1.3;
}
.panel {
  margin-bottom: 18px;
  background-color: #fff;
  border: 1px solid transparent;
  border-radius: 2px;
  -webkit-box-shadow: 0 1px 1px rgba(0, 0, 0, 0.05);
  box-shadow: 0 1px 1px rgba(0, 0, 0, 0.05);
}
.panel-body {
  padding: 15px;
}
.panel-heading {
  padding: 10px 15px;
  border-bottom: 1px solid transparent;
  border-top-right-radius: 1px;
  border-top-left-radius: 1px;
}
.panel-heading > .dropdown .dropdown-toggle {
  color: inherit;
}
.panel-title {
  margin-top: 0;
  margin-bottom: 0;
  font-size: 15px;
  color: inherit;
}
.panel-title > a,
.panel-title > small,
.panel-title > .small,
.panel-title > small > a,
.panel-title > .small > a {
  color: inherit;
}
.panel-footer {
  padding: 10px 15px;
  background-color: #f5f5f5;
  border-top: 1px solid #ddd;
  border-bottom-right-radius: 1px;
  border-bottom-left-radius: 1px;
}
.panel > .list-group,
.panel > .panel-collapse > .list-group {
  margin-bottom: 0;
}
.panel > .list-group .list-group-item,
.panel > .panel-collapse > .list-group .list-group-item {
  border-width: 1px 0;
  border-radius: 0;
}
.panel > .list-group:first-child .list-group-item:first-child,
.panel > .panel-collapse > .list-group:first-child .list-group-item:first-child {
  border-top: 0;
  border-top-right-radius: 1px;
  border-top-left-radius: 1px;
}
.panel > .list-group:last-child .list-group-item:last-child,
.panel > .panel-collapse > .list-group:last-child .list-group-item:last-child {
  border-bottom: 0;
  border-bottom-right-radius: 1px;
  border-bottom-left-radius: 1px;
}
.panel > .panel-heading + .panel-collapse > .list-group .list-group-item:first-child {
  border-top-right-radius: 0;
  border-top-left-radius: 0;
}
.panel-heading + .list-group .list-group-item:first-child {
  border-top-width: 0;
}
.list-group + .panel-footer {
  border-top-width: 0;
}
.panel > .table,
.panel > .table-responsive > .table,
.panel > .panel-collapse > .table {
  margin-bottom: 0;
}
.panel > .table caption,
.panel > .table-responsive > .table caption,
.panel > .panel-collapse > .table caption {
  padding-left: 15px;
  padding-right: 15px;
}
.panel > .table:first-child,
.panel > .table-responsive:first-child > .table:first-child {
  border-top-right-radius: 1px;
  border-top-left-radius: 1px;
}
.panel > .table:first-child > thead:first-child > tr:first-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child,
.panel > .table:first-child > tbody:first-child > tr:first-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child {
  border-top-left-radius: 1px;
  border-top-right-radius: 1px;
}
.panel > .table:first-child > thead:first-child > tr:first-child td:first-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child td:first-child,
.panel > .table:first-child > tbody:first-child > tr:first-child td:first-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child td:first-child,
.panel > .table:first-child > thead:first-child > tr:first-child th:first-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child th:first-child,
.panel > .table:first-child > tbody:first-child > tr:first-child th:first-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child th:first-child {
  border-top-left-radius: 1px;
}
.panel > .table:first-child > thead:first-child > tr:first-child td:last-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child td:last-child,
.panel > .table:first-child > tbody:first-child > tr:first-child td:last-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child td:last-child,
.panel > .table:first-child > thead:first-child > tr:first-child th:last-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child th:last-child,
.panel > .table:first-child > tbody:first-child > tr:first-child th:last-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child th:last-child {
  border-top-right-radius: 1px;
}
.panel > .table:last-child,
.panel > .table-responsive:last-child > .table:last-child {
  border-bottom-right-radius: 1px;
  border-bottom-left-radius: 1px;
}
.panel > .table:last-child > tbody:last-child > tr:last-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child {
  border-bottom-left-radius: 1px;
  border-bottom-right-radius: 1px;
}
.panel > .table:last-child > tbody:last-child > tr:last-child td:first-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child td:first-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child td:first-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child td:first-child,
.panel > .table:last-child > tbody:last-child > tr:last-child th:first-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child th:first-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child th:first-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child th:first-child {
  border-bottom-left-radius: 1px;
}
.panel > .table:last-child > tbody:last-child > tr:last-child td:last-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child td:last-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child td:last-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child td:last-child,
.panel > .table:last-child > tbody:last-child > tr:last-child th:last-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child th:last-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child th:last-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child th:last-child {
  border-bottom-right-radius: 1px;
}
.panel > .panel-body + .table,
.panel > .panel-body + .table-responsive,
.panel > .table + .panel-body,
.panel > .table-responsive + .panel-body {
  border-top: 1px solid #ddd;
}
.panel > .table > tbody:first-child > tr:first-child th,
.panel > .table > tbody:first-child > tr:first-child td {
  border-top: 0;
}
.panel > .table-bordered,
.panel > .table-responsive > .table-bordered {
  border: 0;
}
.panel > .table-bordered > thead > tr > th:first-child,
.panel > .table-responsive > .table-bordered > thead > tr > th:first-child,
.panel > .table-bordered > tbody > tr > th:first-child,
.panel > .table-responsive > .table-bordered > tbody > tr > th:first-child,
.panel > .table-bordered > tfoot > tr > th:first-child,
.panel > .table-responsive > .table-bordered > tfoot > tr > th:first-child,
.panel > .table-bordered > thead > tr > td:first-child,
.panel > .table-responsive > .table-bordered > thead > tr > td:first-child,
.panel > .table-bordered > tbody > tr > td:first-child,
.panel > .table-responsive > .table-bordered > tbody > tr > td:first-child,
.panel > .table-bordered > tfoot > tr > td:first-child,
.panel > .table-responsive > .table-bordered > tfoot > tr > td:first-child {
  border-left: 0;
}
.panel > .table-bordered > thead > tr > th:last-child,
.panel > .table-responsive > .table-bordered > thead > tr > th:last-child,
.panel > .table-bordered > tbody > tr > th:last-child,
.panel > .table-responsive > .table-bordered > tbody > tr > th:last-child,
.panel > .table-bordered > tfoot > tr > th:last-child,
.panel > .table-responsive > .table-bordered > tfoot > tr > th:last-child,
.panel > .table-bordered > thead > tr > td:last-child,
.panel > .table-responsive > .table-bordered > thead > tr > td:last-child,
.panel > .table-bordered > tbody > tr > td:last-child,
.panel > .table-responsive > .table-bordered > tbody > tr > td:last-child,
.panel > .table-bordered > tfoot > tr > td:last-child,
.panel > .table-responsive > .table-bordered > tfoot > tr > td:last-child {
  border-right: 0;
}
.panel > .table-bordered > thead > tr:first-child > td,
.panel > .table-responsive > .table-bordered > thead > tr:first-child > td,
.panel > .table-bordered > tbody > tr:first-child > td,
.panel > .table-responsive > .table-bordered > tbody > tr:first-child > td,
.panel > .table-bordered > thead > tr:first-child > th,
.panel > .table-responsive > .table-bordered > thead > tr:first-child > th,
.panel > .table-bordered > tbody > tr:first-child > th,
.panel > .table-responsive > .table-bordered > tbody > tr:first-child > th {
  border-bottom: 0;
}
.panel > .table-bordered > tbody > tr:last-child > td,
.panel > .table-responsive > .table-bordered > tbody > tr:last-child > td,
.panel > .table-bordered > tfoot > tr:last-child > td,
.panel > .table-responsive > .table-bordered > tfoot > tr:last-child > td,
.panel > .table-bordered > tbody > tr:last-child > th,
.panel > .table-responsive > .table-bordered > tbody > tr:last-child > th,
.panel > .table-bordered > tfoot > tr:last-child > th,
.panel > .table-responsive > .table-bordered > tfoot > tr:last-child > th {
  border-bottom: 0;
}
.panel > .table-responsive {
  border: 0;
  margin-bottom: 0;
}
.panel-group {
  margin-bottom: 18px;
}
.panel-group .panel {
  margin-bottom: 0;
  border-radius: 2px;
}
.panel-group .panel + .panel {
  margin-top: 5px;
}
.panel-group .panel-heading {
  border-bottom: 0;
}
.panel-group .panel-heading + .panel-collapse > .panel-body,
.panel-group .panel-heading + .panel-collapse > .list-group {
  border-top: 1px solid #ddd;
}
.panel-group .panel-footer {
  border-top: 0;
}
.panel-group .panel-footer + .panel-collapse .panel-body {
  border-bottom: 1px solid #ddd;
}
.panel-default {
  border-color: #ddd;
}
.panel-default > .panel-heading {
  color: #333333;
  background-color: #f5f5f5;
  border-color: #ddd;
}
.panel-default > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #ddd;
}
.panel-default > .panel-heading .badge {
  color: #f5f5f5;
  background-color: #333333;
}
.panel-default > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #ddd;
}
.panel-primary {
  border-color: #337ab7;
}
.panel-primary > .panel-heading {
  color: #fff;
  background-color: #337ab7;
  border-color: #337ab7;
}
.panel-primary > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #337ab7;
}
.panel-primary > .panel-heading .badge {
  color: #337ab7;
  background-color: #fff;
}
.panel-primary > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #337ab7;
}
.panel-success {
  border-color: #d6e9c6;
}
.panel-success > .panel-heading {
  color: #3c763d;
  background-color: #dff0d8;
  border-color: #d6e9c6;
}
.panel-success > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #d6e9c6;
}
.panel-success > .panel-heading .badge {
  color: #dff0d8;
  background-color: #3c763d;
}
.panel-success > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #d6e9c6;
}
.panel-info {
  border-color: #bce8f1;
}
.panel-info > .panel-heading {
  color: #31708f;
  background-color: #d9edf7;
  border-color: #bce8f1;
}
.panel-info > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #bce8f1;
}
.panel-info > .panel-heading .badge {
  color: #d9edf7;
  background-color: #31708f;
}
.panel-info > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #bce8f1;
}
.panel-warning {
  border-color: #faebcc;
}
.panel-warning > .panel-heading {
  color: #8a6d3b;
  background-color: #fcf8e3;
  border-color: #faebcc;
}
.panel-warning > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #faebcc;
}
.panel-warning > .panel-heading .badge {
  color: #fcf8e3;
  background-color: #8a6d3b;
}
.panel-warning > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #faebcc;
}
.panel-danger {
  border-color: #ebccd1;
}
.panel-danger > .panel-heading {
  color: #a94442;
  background-color: #f2dede;
  border-color: #ebccd1;
}
.panel-danger > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #ebccd1;
}
.panel-danger > .panel-heading .badge {
  color: #f2dede;
  background-color: #a94442;
}
.panel-danger > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #ebccd1;
}
.embed-responsive {
  position: relative;
  display: block;
  height: 0;
  padding: 0;
  overflow: hidden;
}
.embed-responsive .embed-responsive-item,
.embed-responsive iframe,
.embed-responsive embed,
.embed-responsive object,
.embed-responsive video {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  height: 100%;
  width: 100%;
  border: 0;
}
.embed-responsive-16by9 {
  padding-bottom: 56.25%;
}
.embed-responsive-4by3 {
  padding-bottom: 75%;
}
.well {
  min-height: 20px;
  padding: 19px;
  margin-bottom: 20px;
  background-color: #f5f5f5;
  border: 1px solid #e3e3e3;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.05);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.05);
}
.well blockquote {
  border-color: #ddd;
  border-color: rgba(0, 0, 0, 0.15);
}
.well-lg {
  padding: 24px;
  border-radius: 3px;
}
.well-sm {
  padding: 9px;
  border-radius: 1px;
}
.close {
  float: right;
  font-size: 19.5px;
  font-weight: bold;
  line-height: 1;
  color: #000;
  text-shadow: 0 1px 0 #fff;
  opacity: 0.2;
  filter: alpha(opacity=20);
}
.close:hover,
.close:focus {
  color: #000;
  text-decoration: none;
  cursor: pointer;
  opacity: 0.5;
  filter: alpha(opacity=50);
}
button.close {
  padding: 0;
  cursor: pointer;
  background: transparent;
  border: 0;
  -webkit-appearance: none;
}
.modal-open {
  overflow: hidden;
}
.modal {
  display: none;
  overflow: hidden;
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 1050;
  -webkit-overflow-scrolling: touch;
  outline: 0;
}
.modal.fade .modal-dialog {
  -webkit-transform: translate(0, -25%);
  -ms-transform: translate(0, -25%);
  -o-transform: translate(0, -25%);
  transform: translate(0, -25%);
  -webkit-transition: -webkit-transform 0.3s ease-out;
  -moz-transition: -moz-transform 0.3s ease-out;
  -o-transition: -o-transform 0.3s ease-out;
  transition: transform 0.3s ease-out;
}
.modal.in .modal-dialog {
  -webkit-transform: translate(0, 0);
  -ms-transform: translate(0, 0);
  -o-transform: translate(0, 0);
  transform: translate(0, 0);
}
.modal-open .modal {
  overflow-x: hidden;
  overflow-y: auto;
}
.modal-dialog {
  position: relative;
  width: auto;
  margin: 10px;
}
.modal-content {
  position: relative;
  background-color: #fff;
  border: 1px solid #999;
  border: 1px solid rgba(0, 0, 0, 0.2);
  border-radius: 3px;
  -webkit-box-shadow: 0 3px 9px rgba(0, 0, 0, 0.5);
  box-shadow: 0 3px 9px rgba(0, 0, 0, 0.5);
  background-clip: padding-box;
  outline: 0;
}
.modal-backdrop {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 1040;
  background-color: #000;
}
.modal-backdrop.fade {
  opacity: 0;
  filter: alpha(opacity=0);
}
.modal-backdrop.in {
  opacity: 0.5;
  filter: alpha(opacity=50);
}
.modal-header {
  padding: 15px;
  border-bottom: 1px solid #e5e5e5;
}
.modal-header .close {
  margin-top: -2px;
}
.modal-title {
  margin: 0;
  line-height: 1.42857143;
}
.modal-body {
  position: relative;
  padding: 15px;
}
.modal-footer {
  padding: 15px;
  text-align: right;
  border-top: 1px solid #e5e5e5;
}
.modal-footer .btn + .btn {
  margin-left: 5px;
  margin-bottom: 0;
}
.modal-footer .btn-group .btn + .btn {
  margin-left: -1px;
}
.modal-footer .btn-block + .btn-block {
  margin-left: 0;
}
.modal-scrollbar-measure {
  position: absolute;
  top: -9999px;
  width: 50px;
  height: 50px;
  overflow: scroll;
}
@media (min-width: 768px) {
  .modal-dialog {
    width: 600px;
    margin: 30px auto;
  }
  .modal-content {
    -webkit-box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
  }
  .modal-sm {
    width: 300px;
  }
}
@media (min-width: 992px) {
  .modal-lg {
    width: 900px;
  }
}
.tooltip {
  position: absolute;
  z-index: 1070;
  display: block;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-style: normal;
  font-weight: normal;
  letter-spacing: normal;
  line-break: auto;
  line-height: 1.42857143;
  text-align: left;
  text-align: start;
  text-decoration: none;
  text-shadow: none;
  text-transform: none;
  white-space: normal;
  word-break: normal;
  word-spacing: normal;
  word-wrap: normal;
  font-size: 12px;
  opacity: 0;
  filter: alpha(opacity=0);
}
.tooltip.in {
  opacity: 0.9;
  filter: alpha(opacity=90);
}
.tooltip.top {
  margin-top: -3px;
  padding: 5px 0;
}
.tooltip.right {
  margin-left: 3px;
  padding: 0 5px;
}
.tooltip.bottom {
  margin-top: 3px;
  padding: 5px 0;
}
.tooltip.left {
  margin-left: -3px;
  padding: 0 5px;
}
.tooltip-inner {
  max-width: 200px;
  padding: 3px 8px;
  color: #fff;
  text-align: center;
  background-color: #000;
  border-radius: 2px;
}
.tooltip-arrow {
  position: absolute;
  width: 0;
  height: 0;
  border-color: transparent;
  border-style: solid;
}
.tooltip.top .tooltip-arrow {
  bottom: 0;
  left: 50%;
  margin-left: -5px;
  border-width: 5px 5px 0;
  border-top-color: #000;
}
.tooltip.top-left .tooltip-arrow {
  bottom: 0;
  right: 5px;
  margin-bottom: -5px;
  border-width: 5px 5px 0;
  border-top-color: #000;
}
.tooltip.top-right .tooltip-arrow {
  bottom: 0;
  left: 5px;
  margin-bottom: -5px;
  border-width: 5px 5px 0;
  border-top-color: #000;
}
.tooltip.right .tooltip-arrow {
  top: 50%;
  left: 0;
  margin-top: -5px;
  border-width: 5px 5px 5px 0;
  border-right-color: #000;
}
.tooltip.left .tooltip-arrow {
  top: 50%;
  right: 0;
  margin-top: -5px;
  border-width: 5px 0 5px 5px;
  border-left-color: #000;
}
.tooltip.bottom .tooltip-arrow {
  top: 0;
  left: 50%;
  margin-left: -5px;
  border-width: 0 5px 5px;
  border-bottom-color: #000;
}
.tooltip.bottom-left .tooltip-arrow {
  top: 0;
  right: 5px;
  margin-top: -5px;
  border-width: 0 5px 5px;
  border-bottom-color: #000;
}
.tooltip.bottom-right .tooltip-arrow {
  top: 0;
  left: 5px;
  margin-top: -5px;
  border-width: 0 5px 5px;
  border-bottom-color: #000;
}
.popover {
  position: absolute;
  top: 0;
  left: 0;
  z-index: 1060;
  display: none;
  max-width: 276px;
  padding: 1px;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-style: normal;
  font-weight: normal;
  letter-spacing: normal;
  line-break: auto;
  line-height: 1.42857143;
  text-align: left;
  text-align: start;
  text-decoration: none;
  text-shadow: none;
  text-transform: none;
  white-space: normal;
  word-break: normal;
  word-spacing: normal;
  word-wrap: normal;
  font-size: 13px;
  background-color: #fff;
  background-clip: padding-box;
  border: 1px solid #ccc;
  border: 1px solid rgba(0, 0, 0, 0.2);
  border-radius: 3px;
  -webkit-box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
}
.popover.top {
  margin-top: -10px;
}
.popover.right {
  margin-left: 10px;
}
.popover.bottom {
  margin-top: 10px;
}
.popover.left {
  margin-left: -10px;
}
.popover-title {
  margin: 0;
  padding: 8px 14px;
  font-size: 13px;
  background-color: #f7f7f7;
  border-bottom: 1px solid #ebebeb;
  border-radius: 2px 2px 0 0;
}
.popover-content {
  padding: 9px 14px;
}
.popover > .arrow,
.popover > .arrow:after {
  position: absolute;
  display: block;
  width: 0;
  height: 0;
  border-color: transparent;
  border-style: solid;
}
.popover > .arrow {
  border-width: 11px;
}
.popover > .arrow:after {
  border-width: 10px;
  content: "";
}
.popover.top > .arrow {
  left: 50%;
  margin-left: -11px;
  border-bottom-width: 0;
  border-top-color: #999999;
  border-top-color: rgba(0, 0, 0, 0.25);
  bottom: -11px;
}
.popover.top > .arrow:after {
  content: " ";
  bottom: 1px;
  margin-left: -10px;
  border-bottom-width: 0;
  border-top-color: #fff;
}
.popover.right > .arrow {
  top: 50%;
  left: -11px;
  margin-top: -11px;
  border-left-width: 0;
  border-right-color: #999999;
  border-right-color: rgba(0, 0, 0, 0.25);
}
.popover.right > .arrow:after {
  content: " ";
  left: 1px;
  bottom: -10px;
  border-left-width: 0;
  border-right-color: #fff;
}
.popover.bottom > .arrow {
  left: 50%;
  margin-left: -11px;
  border-top-width: 0;
  border-bottom-color: #999999;
  border-bottom-color: rgba(0, 0, 0, 0.25);
  top: -11px;
}
.popover.bottom > .arrow:after {
  content: " ";
  top: 1px;
  margin-left: -10px;
  border-top-width: 0;
  border-bottom-color: #fff;
}
.popover.left > .arrow {
  top: 50%;
  right: -11px;
  margin-top: -11px;
  border-right-width: 0;
  border-left-color: #999999;
  border-left-color: rgba(0, 0, 0, 0.25);
}
.popover.left > .arrow:after {
  content: " ";
  right: 1px;
  border-right-width: 0;
  border-left-color: #fff;
  bottom: -10px;
}
.carousel {
  position: relative;
}
.carousel-inner {
  position: relative;
  overflow: hidden;
  width: 100%;
}
.carousel-inner > .item {
  display: none;
  position: relative;
  -webkit-transition: 0.6s ease-in-out left;
  -o-transition: 0.6s ease-in-out left;
  transition: 0.6s ease-in-out left;
}
.carousel-inner > .item > img,
.carousel-inner > .item > a > img {
  line-height: 1;
}
@media all and (transform-3d), (-webkit-transform-3d) {
  .carousel-inner > .item {
    -webkit-transition: -webkit-transform 0.6s ease-in-out;
    -moz-transition: -moz-transform 0.6s ease-in-out;
    -o-transition: -o-transform 0.6s ease-in-out;
    transition: transform 0.6s ease-in-out;
    -webkit-backface-visibility: hidden;
    -moz-backface-visibility: hidden;
    backface-visibility: hidden;
    -webkit-perspective: 1000px;
    -moz-perspective: 1000px;
    perspective: 1000px;
  }
  .carousel-inner > .item.next,
  .carousel-inner > .item.active.right {
    -webkit-transform: translate3d(100%, 0, 0);
    transform: translate3d(100%, 0, 0);
    left: 0;
  }
  .carousel-inner > .item.prev,
  .carousel-inner > .item.active.left {
    -webkit-transform: translate3d(-100%, 0, 0);
    transform: translate3d(-100%, 0, 0);
    left: 0;
  }
  .carousel-inner > .item.next.left,
  .carousel-inner > .item.prev.right,
  .carousel-inner > .item.active {
    -webkit-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
    left: 0;
  }
}
.carousel-inner > .active,
.carousel-inner > .next,
.carousel-inner > .prev {
  display: block;
}
.carousel-inner > .active {
  left: 0;
}
.carousel-inner > .next,
.carousel-inner > .prev {
  position: absolute;
  top: 0;
  width: 100%;
}
.carousel-inner > .next {
  left: 100%;
}
.carousel-inner > .prev {
  left: -100%;
}
.carousel-inner > .next.left,
.carousel-inner > .prev.right {
  left: 0;
}
.carousel-inner > .active.left {
  left: -100%;
}
.carousel-inner > .active.right {
  left: 100%;
}
.carousel-control {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  width: 15%;
  opacity: 0.5;
  filter: alpha(opacity=50);
  font-size: 20px;
  color: #fff;
  text-align: center;
  text-shadow: 0 1px 2px rgba(0, 0, 0, 0.6);
  background-color: rgba(0, 0, 0, 0);
}
.carousel-control.left {
  background-image: -webkit-linear-gradient(left, rgba(0, 0, 0, 0.5) 0%, rgba(0, 0, 0, 0.0001) 100%);
  background-image: -o-linear-gradient(left, rgba(0, 0, 0, 0.5) 0%, rgba(0, 0, 0, 0.0001) 100%);
  background-image: linear-gradient(to right, rgba(0, 0, 0, 0.5) 0%, rgba(0, 0, 0, 0.0001) 100%);
  background-repeat: repeat-x;
  filter: progid:DXImageTransform.Microsoft.gradient(startColorstr='#80000000', endColorstr='#00000000', GradientType=1);
}
.carousel-control.right {
  left: auto;
  right: 0;
  background-image: -webkit-linear-gradient(left, rgba(0, 0, 0, 0.0001) 0%, rgba(0, 0, 0, 0.5) 100%);
  background-image: -o-linear-gradient(left, rgba(0, 0, 0, 0.0001) 0%, rgba(0, 0, 0, 0.5) 100%);
  background-image: linear-gradient(to right, rgba(0, 0, 0, 0.0001) 0%, rgba(0, 0, 0, 0.5) 100%);
  background-repeat: repeat-x;
  filter: progid:DXImageTransform.Microsoft.gradient(startColorstr='#00000000', endColorstr='#80000000', GradientType=1);
}
.carousel-control:hover,
.carousel-control:focus {
  outline: 0;
  color: #fff;
  text-decoration: none;
  opacity: 0.9;
  filter: alpha(opacity=90);
}
.carousel-control .icon-prev,
.carousel-control .icon-next,
.carousel-control .glyphicon-chevron-left,
.carousel-control .glyphicon-chevron-right {
  position: absolute;
  top: 50%;
  margin-top: -10px;
  z-index: 5;
  display: inline-block;
}
.carousel-control .icon-prev,
.carousel-control .glyphicon-chevron-left {
  left: 50%;
  margin-left: -10px;
}
.carousel-control .icon-next,
.carousel-control .glyphicon-chevron-right {
  right: 50%;
  margin-right: -10px;
}
.carousel-control .icon-prev,
.carousel-control .icon-next {
  width: 20px;
  height: 20px;
  line-height: 1;
  font-family: serif;
}
.carousel-control .icon-prev:before {
  content: '\2039';
}
.carousel-control .icon-next:before {
  content: '\203a';
}
.carousel-indicators {
  position: absolute;
  bottom: 10px;
  left: 50%;
  z-index: 15;
  width: 60%;
  margin-left: -30%;
  padding-left: 0;
  list-style: none;
  text-align: center;
}
.carousel-indicators li {
  display: inline-block;
  width: 10px;
  height: 10px;
  margin: 1px;
  text-indent: -999px;
  border: 1px solid #fff;
  border-radius: 10px;
  cursor: pointer;
  background-color: #000 \9;
  background-color: rgba(0, 0, 0, 0);
}
.carousel-indicators .active {
  margin: 0;
  width: 12px;
  height: 12px;
  background-color: #fff;
}
.carousel-caption {
  position: absolute;
  left: 15%;
  right: 15%;
  bottom: 20px;
  z-index: 10;
  padding-top: 20px;
  padding-bottom: 20px;
  color: #fff;
  text-align: center;
  text-shadow: 0 1px 2px rgba(0, 0, 0, 0.6);
}
.carousel-caption .btn {
  text-shadow: none;
}
@media screen and (min-width: 768px) {
  .carousel-control .glyphicon-chevron-left,
  .carousel-control .glyphicon-chevron-right,
  .carousel-control .icon-prev,
  .carousel-control .icon-next {
    width: 30px;
    height: 30px;
    margin-top: -10px;
    font-size: 30px;
  }
  .carousel-control .glyphicon-chevron-left,
  .carousel-control .icon-prev {
    margin-left: -10px;
  }
  .carousel-control .glyphicon-chevron-right,
  .carousel-control .icon-next {
    margin-right: -10px;
  }
  .carousel-caption {
    left: 20%;
    right: 20%;
    padding-bottom: 30px;
  }
  .carousel-indicators {
    bottom: 20px;
  }
}
.clearfix:before,
.clearfix:after,
.dl-horizontal dd:before,
.dl-horizontal dd:after,
.container:before,
.container:after,
.container-fluid:before,
.container-fluid:after,
.row:before,
.row:after,
.form-horizontal .form-group:before,
.form-horizontal .form-group:after,
.btn-toolbar:before,
.btn-toolbar:after,
.btn-group-vertical > .btn-group:before,
.btn-group-vertical > .btn-group:after,
.nav:before,
.nav:after,
.navbar:before,
.navbar:after,
.navbar-header:before,
.navbar-header:after,
.navbar-collapse:before,
.navbar-collapse:after,
.pager:before,
.pager:after,
.panel-body:before,
.panel-body:after,
.modal-header:before,
.modal-header:after,
.modal-footer:before,
.modal-footer:after,
.item_buttons:before,
.item_buttons:after {
  content: " ";
  display: table;
}
.clearfix:after,
.dl-horizontal dd:after,
.container:after,
.container-fluid:after,
.row:after,
.form-horizontal .form-group:after,
.btn-toolbar:after,
.btn-group-vertical > .btn-group:after,
.nav:after,
.navbar:after,
.navbar-header:after,
.navbar-collapse:after,
.pager:after,
.panel-body:after,
.modal-header:after,
.modal-footer:after,
.item_buttons:after {
  clear: both;
}
.center-block {
  display: block;
  margin-left: auto;
  margin-right: auto;
}
.pull-right {
  float: right !important;
}
.pull-left {
  float: left !important;
}
.hide {
  display: none !important;
}
.show {
  display: block !important;
}
.invisible {
  visibility: hidden;
}
.text-hide {
  font: 0/0 a;
  color: transparent;
  text-shadow: none;
  background-color: transparent;
  border: 0;
}
.hidden {
  display: none !important;
}
.affix {
  position: fixed;
}
@-ms-viewport {
  width: device-width;
}
.visible-xs,
.visible-sm,
.visible-md,
.visible-lg {
  display: none !important;
}
.visible-xs-block,
.visible-xs-inline,
.visible-xs-inline-block,
.visible-sm-block,
.visible-sm-inline,
.visible-sm-inline-block,
.visible-md-block,
.visible-md-inline,
.visible-md-inline-block,
.visible-lg-block,
.visible-lg-inline,
.visible-lg-inline-block {
  display: none !important;
}
@media (max-width: 767px) {
  .visible-xs {
    display: block !important;
  }
  table.visible-xs {
    display: table !important;
  }
  tr.visible-xs {
    display: table-row !important;
  }
  th.visible-xs,
  td.visible-xs {
    display: table-cell !important;
  }
}
@media (max-width: 767px) {
  .visible-xs-block {
    display: block !important;
  }
}
@media (max-width: 767px) {
  .visible-xs-inline {
    display: inline !important;
  }
}
@media (max-width: 767px) {
  .visible-xs-inline-block {
    display: inline-block !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .visible-sm {
    display: block !important;
  }
  table.visible-sm {
    display: table !important;
  }
  tr.visible-sm {
    display: table-row !important;
  }
  th.visible-sm,
  td.visible-sm {
    display: table-cell !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .visible-sm-block {
    display: block !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .visible-sm-inline {
    display: inline !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .visible-sm-inline-block {
    display: inline-block !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .visible-md {
    display: block !important;
  }
  table.visible-md {
    display: table !important;
  }
  tr.visible-md {
    display: table-row !important;
  }
  th.visible-md,
  td.visible-md {
    display: table-cell !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .visible-md-block {
    display: block !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .visible-md-inline {
    display: inline !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .visible-md-inline-block {
    display: inline-block !important;
  }
}
@media (min-width: 1200px) {
  .visible-lg {
    display: block !important;
  }
  table.visible-lg {
    display: table !important;
  }
  tr.visible-lg {
    display: table-row !important;
  }
  th.visible-lg,
  td.visible-lg {
    display: table-cell !important;
  }
}
@media (min-width: 1200px) {
  .visible-lg-block {
    display: block !important;
  }
}
@media (min-width: 1200px) {
  .visible-lg-inline {
    display: inline !important;
  }
}
@media (min-width: 1200px) {
  .visible-lg-inline-block {
    display: inline-block !important;
  }
}
@media (max-width: 767px) {
  .hidden-xs {
    display: none !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .hidden-sm {
    display: none !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .hidden-md {
    display: none !important;
  }
}
@media (min-width: 1200px) {
  .hidden-lg {
    display: none !important;
  }
}
.visible-print {
  display: none !important;
}
@media print {
  .visible-print {
    display: block !important;
  }
  table.visible-print {
    display: table !important;
  }
  tr.visible-print {
    display: table-row !important;
  }
  th.visible-print,
  td.visible-print {
    display: table-cell !important;
  }
}
.visible-print-block {
  display: none !important;
}
@media print {
  .visible-print-block {
    display: block !important;
  }
}
.visible-print-inline {
  display: none !important;
}
@media print {
  .visible-print-inline {
    display: inline !important;
  }
}
.visible-print-inline-block {
  display: none !important;
}
@media print {
  .visible-print-inline-block {
    display: inline-block !important;
  }
}
@media print {
  .hidden-print {
    display: none !important;
  }
}
/*!
*
* Font Awesome
*
*/
/*!
 *  Font Awesome 4.2.0 by @davegandy - http://fontawesome.io - @fontawesome
 *  License - http://fontawesome.io/license (Font: SIL OFL 1.1, CSS: MIT License)
 */
/* FONT PATH
 * -------------------------- */
@font-face {
  font-family: 'FontAwesome';
  src: url('../components/font-awesome/fonts/fontawesome-webfont.eot?v=4.2.0');
  src: url('../components/font-awesome/fonts/fontawesome-webfont.eot?#iefix&v=4.2.0') format('embedded-opentype'), url('../components/font-awesome/fonts/fontawesome-webfont.woff?v=4.2.0') format('woff'), url('../components/font-awesome/fonts/fontawesome-webfont.ttf?v=4.2.0') format('truetype'), url('../components/font-awesome/fonts/fontawesome-webfont.svg?v=4.2.0#fontawesomeregular') format('svg');
  font-weight: normal;
  font-style: normal;
}
.fa {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
/* makes the font 33% larger relative to the icon container */
.fa-lg {
  font-size: 1.33333333em;
  line-height: 0.75em;
  vertical-align: -15%;
}
.fa-2x {
  font-size: 2em;
}
.fa-3x {
  font-size: 3em;
}
.fa-4x {
  font-size: 4em;
}
.fa-5x {
  font-size: 5em;
}
.fa-fw {
  width: 1.28571429em;
  text-align: center;
}
.fa-ul {
  padding-left: 0;
  margin-left: 2.14285714em;
  list-style-type: none;
}
.fa-ul > li {
  position: relative;
}
.fa-li {
  position: absolute;
  left: -2.14285714em;
  width: 2.14285714em;
  top: 0.14285714em;
  text-align: center;
}
.fa-li.fa-lg {
  left: -1.85714286em;
}
.fa-border {
  padding: .2em .25em .15em;
  border: solid 0.08em #eee;
  border-radius: .1em;
}
.pull-right {
  float: right;
}
.pull-left {
  float: left;
}
.fa.pull-left {
  margin-right: .3em;
}
.fa.pull-right {
  margin-left: .3em;
}
.fa-spin {
  -webkit-animation: fa-spin 2s infinite linear;
  animation: fa-spin 2s infinite linear;
}
@-webkit-keyframes fa-spin {
  0% {
    -webkit-transform: rotate(0deg);
    transform: rotate(0deg);
  }
  100% {
    -webkit-transform: rotate(359deg);
    transform: rotate(359deg);
  }
}
@keyframes fa-spin {
  0% {
    -webkit-transform: rotate(0deg);
    transform: rotate(0deg);
  }
  100% {
    -webkit-transform: rotate(359deg);
    transform: rotate(359deg);
  }
}
.fa-rotate-90 {
  filter: progid:DXImageTransform.Microsoft.BasicImage(rotation=1);
  -webkit-transform: rotate(90deg);
  -ms-transform: rotate(90deg);
  transform: rotate(90deg);
}
.fa-rotate-180 {
  filter: progid:DXImageTransform.Microsoft.BasicImage(rotation=2);
  -webkit-transform: rotate(180deg);
  -ms-transform: rotate(180deg);
  transform: rotate(180deg);
}
.fa-rotate-270 {
  filter: progid:DXImageTransform.Microsoft.BasicImage(rotation=3);
  -webkit-transform: rotate(270deg);
  -ms-transform: rotate(270deg);
  transform: rotate(270deg);
}
.fa-flip-horizontal {
  filter: progid:DXImageTransform.Microsoft.BasicImage(rotation=0, mirror=1);
  -webkit-transform: scale(-1, 1);
  -ms-transform: scale(-1, 1);
  transform: scale(-1, 1);
}
.fa-flip-vertical {
  filter: progid:DXImageTransform.Microsoft.BasicImage(rotation=2, mirror=1);
  -webkit-transform: scale(1, -1);
  -ms-transform: scale(1, -1);
  transform: scale(1, -1);
}
:root .fa-rotate-90,
:root .fa-rotate-180,
:root .fa-rotate-270,
:root .fa-flip-horizontal,
:root .fa-flip-vertical {
  filter: none;
}
.fa-stack {
  position: relative;
  display: inline-block;
  width: 2em;
  height: 2em;
  line-height: 2em;
  vertical-align: middle;
}
.fa-stack-1x,
.fa-stack-2x {
  position: absolute;
  left: 0;
  width: 100%;
  text-align: center;
}
.fa-stack-1x {
  line-height: inherit;
}
.fa-stack-2x {
  font-size: 2em;
}
.fa-inverse {
  color: #fff;
}
/* Font Awesome uses the Unicode Private Use Area (PUA) to ensure screen
   readers do not read off random characters that represent icons */
.fa-glass:before {
  content: "\f000";
}
.fa-music:before {
  content: "\f001";
}
.fa-search:before {
  content: "\f002";
}
.fa-envelope-o:before {
  content: "\f003";
}
.fa-heart:before {
  content: "\f004";
}
.fa-star:before {
  content: "\f005";
}
.fa-star-o:before {
  content: "\f006";
}
.fa-user:before {
  content: "\f007";
}
.fa-film:before {
  content: "\f008";
}
.fa-th-large:before {
  content: "\f009";
}
.fa-th:before {
  content: "\f00a";
}
.fa-th-list:before {
  content: "\f00b";
}
.fa-check:before {
  content: "\f00c";
}
.fa-remove:before,
.fa-close:before,
.fa-times:before {
  content: "\f00d";
}
.fa-search-plus:before {
  content: "\f00e";
}
.fa-search-minus:before {
  content: "\f010";
}
.fa-power-off:before {
  content: "\f011";
}
.fa-signal:before {
  content: "\f012";
}
.fa-gear:before,
.fa-cog:before {
  content: "\f013";
}
.fa-trash-o:before {
  content: "\f014";
}
.fa-home:before {
  content: "\f015";
}
.fa-file-o:before {
  content: "\f016";
}
.fa-clock-o:before {
  content: "\f017";
}
.fa-road:before {
  content: "\f018";
}
.fa-download:before {
  content: "\f019";
}
.fa-arrow-circle-o-down:before {
  content: "\f01a";
}
.fa-arrow-circle-o-up:before {
  content: "\f01b";
}
.fa-inbox:before {
  content: "\f01c";
}
.fa-play-circle-o:before {
  content: "\f01d";
}
.fa-rotate-right:before,
.fa-repeat:before {
  content: "\f01e";
}
.fa-refresh:before {
  content: "\f021";
}
.fa-list-alt:before {
  content: "\f022";
}
.fa-lock:before {
  content: "\f023";
}
.fa-flag:before {
  content: "\f024";
}
.fa-headphones:before {
  content: "\f025";
}
.fa-volume-off:before {
  content: "\f026";
}
.fa-volume-down:before {
  content: "\f027";
}
.fa-volume-up:before {
  content: "\f028";
}
.fa-qrcode:before {
  content: "\f029";
}
.fa-barcode:before {
  content: "\f02a";
}
.fa-tag:before {
  content: "\f02b";
}
.fa-tags:before {
  content: "\f02c";
}
.fa-book:before {
  content: "\f02d";
}
.fa-bookmark:before {
  content: "\f02e";
}
.fa-print:before {
  content: "\f02f";
}
.fa-camera:before {
  content: "\f030";
}
.fa-font:before {
  content: "\f031";
}
.fa-bold:before {
  content: "\f032";
}
.fa-italic:before {
  content: "\f033";
}
.fa-text-height:before {
  content: "\f034";
}
.fa-text-width:before {
  content: "\f035";
}
.fa-align-left:before {
  content: "\f036";
}
.fa-align-center:before {
  content: "\f037";
}
.fa-align-right:before {
  content: "\f038";
}
.fa-align-justify:before {
  content: "\f039";
}
.fa-list:before {
  content: "\f03a";
}
.fa-dedent:before,
.fa-outdent:before {
  content: "\f03b";
}
.fa-indent:before {
  content: "\f03c";
}
.fa-video-camera:before {
  content: "\f03d";
}
.fa-photo:before,
.fa-image:before,
.fa-picture-o:before {
  content: "\f03e";
}
.fa-pencil:before {
  content: "\f040";
}
.fa-map-marker:before {
  content: "\f041";
}
.fa-adjust:before {
  content: "\f042";
}
.fa-tint:before {
  content: "\f043";
}
.fa-edit:before,
.fa-pencil-square-o:before {
  content: "\f044";
}
.fa-share-square-o:before {
  content: "\f045";
}
.fa-check-square-o:before {
  content: "\f046";
}
.fa-arrows:before {
  content: "\f047";
}
.fa-step-backward:before {
  content: "\f048";
}
.fa-fast-backward:before {
  content: "\f049";
}
.fa-backward:before {
  content: "\f04a";
}
.fa-play:before {
  content: "\f04b";
}
.fa-pause:before {
  content: "\f04c";
}
.fa-stop:before {
  content: "\f04d";
}
.fa-forward:before {
  content: "\f04e";
}
.fa-fast-forward:before {
  content: "\f050";
}
.fa-step-forward:before {
  content: "\f051";
}
.fa-eject:before {
  content: "\f052";
}
.fa-chevron-left:before {
  content: "\f053";
}
.fa-chevron-right:before {
  content: "\f054";
}
.fa-plus-circle:before {
  content: "\f055";
}
.fa-minus-circle:before {
  content: "\f056";
}
.fa-times-circle:before {
  content: "\f057";
}
.fa-check-circle:before {
  content: "\f058";
}
.fa-question-circle:before {
  content: "\f059";
}
.fa-info-circle:before {
  content: "\f05a";
}
.fa-crosshairs:before {
  content: "\f05b";
}
.fa-times-circle-o:before {
  content: "\f05c";
}
.fa-check-circle-o:before {
  content: "\f05d";
}
.fa-ban:before {
  content: "\f05e";
}
.fa-arrow-left:before {
  content: "\f060";
}
.fa-arrow-right:before {
  content: "\f061";
}
.fa-arrow-up:before {
  content: "\f062";
}
.fa-arrow-down:before {
  content: "\f063";
}
.fa-mail-forward:before,
.fa-share:before {
  content: "\f064";
}
.fa-expand:before {
  content: "\f065";
}
.fa-compress:before {
  content: "\f066";
}
.fa-plus:before {
  content: "\f067";
}
.fa-minus:before {
  content: "\f068";
}
.fa-asterisk:before {
  content: "\f069";
}
.fa-exclamation-circle:before {
  content: "\f06a";
}
.fa-gift:before {
  content: "\f06b";
}
.fa-leaf:before {
  content: "\f06c";
}
.fa-fire:before {
  content: "\f06d";
}
.fa-eye:before {
  content: "\f06e";
}
.fa-eye-slash:before {
  content: "\f070";
}
.fa-warning:before,
.fa-exclamation-triangle:before {
  content: "\f071";
}
.fa-plane:before {
  content: "\f072";
}
.fa-calendar:before {
  content: "\f073";
}
.fa-random:before {
  content: "\f074";
}
.fa-comment:before {
  content: "\f075";
}
.fa-magnet:before {
  content: "\f076";
}
.fa-chevron-up:before {
  content: "\f077";
}
.fa-chevron-down:before {
  content: "\f078";
}
.fa-retweet:before {
  content: "\f079";
}
.fa-shopping-cart:before {
  content: "\f07a";
}
.fa-folder:before {
  content: "\f07b";
}
.fa-folder-open:before {
  content: "\f07c";
}
.fa-arrows-v:before {
  content: "\f07d";
}
.fa-arrows-h:before {
  content: "\f07e";
}
.fa-bar-chart-o:before,
.fa-bar-chart:before {
  content: "\f080";
}
.fa-twitter-square:before {
  content: "\f081";
}
.fa-facebook-square:before {
  content: "\f082";
}
.fa-camera-retro:before {
  content: "\f083";
}
.fa-key:before {
  content: "\f084";
}
.fa-gears:before,
.fa-cogs:before {
  content: "\f085";
}
.fa-comments:before {
  content: "\f086";
}
.fa-thumbs-o-up:before {
  content: "\f087";
}
.fa-thumbs-o-down:before {
  content: "\f088";
}
.fa-star-half:before {
  content: "\f089";
}
.fa-heart-o:before {
  content: "\f08a";
}
.fa-sign-out:before {
  content: "\f08b";
}
.fa-linkedin-square:before {
  content: "\f08c";
}
.fa-thumb-tack:before {
  content: "\f08d";
}
.fa-external-link:before {
  content: "\f08e";
}
.fa-sign-in:before {
  content: "\f090";
}
.fa-trophy:before {
  content: "\f091";
}
.fa-github-square:before {
  content: "\f092";
}
.fa-upload:before {
  content: "\f093";
}
.fa-lemon-o:before {
  content: "\f094";
}
.fa-phone:before {
  content: "\f095";
}
.fa-square-o:before {
  content: "\f096";
}
.fa-bookmark-o:before {
  content: "\f097";
}
.fa-phone-square:before {
  content: "\f098";
}
.fa-twitter:before {
  content: "\f099";
}
.fa-facebook:before {
  content: "\f09a";
}
.fa-github:before {
  content: "\f09b";
}
.fa-unlock:before {
  content: "\f09c";
}
.fa-credit-card:before {
  content: "\f09d";
}
.fa-rss:before {
  content: "\f09e";
}
.fa-hdd-o:before {
  content: "\f0a0";
}
.fa-bullhorn:before {
  content: "\f0a1";
}
.fa-bell:before {
  content: "\f0f3";
}
.fa-certificate:before {
  content: "\f0a3";
}
.fa-hand-o-right:before {
  content: "\f0a4";
}
.fa-hand-o-left:before {
  content: "\f0a5";
}
.fa-hand-o-up:before {
  content: "\f0a6";
}
.fa-hand-o-down:before {
  content: "\f0a7";
}
.fa-arrow-circle-left:before {
  content: "\f0a8";
}
.fa-arrow-circle-right:before {
  content: "\f0a9";
}
.fa-arrow-circle-up:before {
  content: "\f0aa";
}
.fa-arrow-circle-down:before {
  content: "\f0ab";
}
.fa-globe:before {
  content: "\f0ac";
}
.fa-wrench:before {
  content: "\f0ad";
}
.fa-tasks:before {
  content: "\f0ae";
}
.fa-filter:before {
  content: "\f0b0";
}
.fa-briefcase:before {
  content: "\f0b1";
}
.fa-arrows-alt:before {
  content: "\f0b2";
}
.fa-group:before,
.fa-users:before {
  content: "\f0c0";
}
.fa-chain:before,
.fa-link:before {
  content: "\f0c1";
}
.fa-cloud:before {
  content: "\f0c2";
}
.fa-flask:before {
  content: "\f0c3";
}
.fa-cut:before,
.fa-scissors:before {
  content: "\f0c4";
}
.fa-copy:before,
.fa-files-o:before {
  content: "\f0c5";
}
.fa-paperclip:before {
  content: "\f0c6";
}
.fa-save:before,
.fa-floppy-o:before {
  content: "\f0c7";
}
.fa-square:before {
  content: "\f0c8";
}
.fa-navicon:before,
.fa-reorder:before,
.fa-bars:before {
  content: "\f0c9";
}
.fa-list-ul:before {
  content: "\f0ca";
}
.fa-list-ol:before {
  content: "\f0cb";
}
.fa-strikethrough:before {
  content: "\f0cc";
}
.fa-underline:before {
  content: "\f0cd";
}
.fa-table:before {
  content: "\f0ce";
}
.fa-magic:before {
  content: "\f0d0";
}
.fa-truck:before {
  content: "\f0d1";
}
.fa-pinterest:before {
  content: "\f0d2";
}
.fa-pinterest-square:before {
  content: "\f0d3";
}
.fa-google-plus-square:before {
  content: "\f0d4";
}
.fa-google-plus:before {
  content: "\f0d5";
}
.fa-money:before {
  content: "\f0d6";
}
.fa-caret-down:before {
  content: "\f0d7";
}
.fa-caret-up:before {
  content: "\f0d8";
}
.fa-caret-left:before {
  content: "\f0d9";
}
.fa-caret-right:before {
  content: "\f0da";
}
.fa-columns:before {
  content: "\f0db";
}
.fa-unsorted:before,
.fa-sort:before {
  content: "\f0dc";
}
.fa-sort-down:before,
.fa-sort-desc:before {
  content: "\f0dd";
}
.fa-sort-up:before,
.fa-sort-asc:before {
  content: "\f0de";
}
.fa-envelope:before {
  content: "\f0e0";
}
.fa-linkedin:before {
  content: "\f0e1";
}
.fa-rotate-left:before,
.fa-undo:before {
  content: "\f0e2";
}
.fa-legal:before,
.fa-gavel:before {
  content: "\f0e3";
}
.fa-dashboard:before,
.fa-tachometer:before {
  content: "\f0e4";
}
.fa-comment-o:before {
  content: "\f0e5";
}
.fa-comments-o:before {
  content: "\f0e6";
}
.fa-flash:before,
.fa-bolt:before {
  content: "\f0e7";
}
.fa-sitemap:before {
  content: "\f0e8";
}
.fa-umbrella:before {
  content: "\f0e9";
}
.fa-paste:before,
.fa-clipboard:before {
  content: "\f0ea";
}
.fa-lightbulb-o:before {
  content: "\f0eb";
}
.fa-exchange:before {
  content: "\f0ec";
}
.fa-cloud-download:before {
  content: "\f0ed";
}
.fa-cloud-upload:before {
  content: "\f0ee";
}
.fa-user-md:before {
  content: "\f0f0";
}
.fa-stethoscope:before {
  content: "\f0f1";
}
.fa-suitcase:before {
  content: "\f0f2";
}
.fa-bell-o:before {
  content: "\f0a2";
}
.fa-coffee:before {
  content: "\f0f4";
}
.fa-cutlery:before {
  content: "\f0f5";
}
.fa-file-text-o:before {
  content: "\f0f6";
}
.fa-building-o:before {
  content: "\f0f7";
}
.fa-hospital-o:before {
  content: "\f0f8";
}
.fa-ambulance:before {
  content: "\f0f9";
}
.fa-medkit:before {
  content: "\f0fa";
}
.fa-fighter-jet:before {
  content: "\f0fb";
}
.fa-beer:before {
  content: "\f0fc";
}
.fa-h-square:before {
  content: "\f0fd";
}
.fa-plus-square:before {
  content: "\f0fe";
}
.fa-angle-double-left:before {
  content: "\f100";
}
.fa-angle-double-right:before {
  content: "\f101";
}
.fa-angle-double-up:before {
  content: "\f102";
}
.fa-angle-double-down:before {
  content: "\f103";
}
.fa-angle-left:before {
  content: "\f104";
}
.fa-angle-right:before {
  content: "\f105";
}
.fa-angle-up:before {
  content: "\f106";
}
.fa-angle-down:before {
  content: "\f107";
}
.fa-desktop:before {
  content: "\f108";
}
.fa-laptop:before {
  content: "\f109";
}
.fa-tablet:before {
  content: "\f10a";
}
.fa-mobile-phone:before,
.fa-mobile:before {
  content: "\f10b";
}
.fa-circle-o:before {
  content: "\f10c";
}
.fa-quote-left:before {
  content: "\f10d";
}
.fa-quote-right:before {
  content: "\f10e";
}
.fa-spinner:before {
  content: "\f110";
}
.fa-circle:before {
  content: "\f111";
}
.fa-mail-reply:before,
.fa-reply:before {
  content: "\f112";
}
.fa-github-alt:before {
  content: "\f113";
}
.fa-folder-o:before {
  content: "\f114";
}
.fa-folder-open-o:before {
  content: "\f115";
}
.fa-smile-o:before {
  content: "\f118";
}
.fa-frown-o:before {
  content: "\f119";
}
.fa-meh-o:before {
  content: "\f11a";
}
.fa-gamepad:before {
  content: "\f11b";
}
.fa-keyboard-o:before {
  content: "\f11c";
}
.fa-flag-o:before {
  content: "\f11d";
}
.fa-flag-checkered:before {
  content: "\f11e";
}
.fa-terminal:before {
  content: "\f120";
}
.fa-code:before {
  content: "\f121";
}
.fa-mail-reply-all:before,
.fa-reply-all:before {
  content: "\f122";
}
.fa-star-half-empty:before,
.fa-star-half-full:before,
.fa-star-half-o:before {
  content: "\f123";
}
.fa-location-arrow:before {
  content: "\f124";
}
.fa-crop:before {
  content: "\f125";
}
.fa-code-fork:before {
  content: "\f126";
}
.fa-unlink:before,
.fa-chain-broken:before {
  content: "\f127";
}
.fa-question:before {
  content: "\f128";
}
.fa-info:before {
  content: "\f129";
}
.fa-exclamation:before {
  content: "\f12a";
}
.fa-superscript:before {
  content: "\f12b";
}
.fa-subscript:before {
  content: "\f12c";
}
.fa-eraser:before {
  content: "\f12d";
}
.fa-puzzle-piece:before {
  content: "\f12e";
}
.fa-microphone:before {
  content: "\f130";
}
.fa-microphone-slash:before {
  content: "\f131";
}
.fa-shield:before {
  content: "\f132";
}
.fa-calendar-o:before {
  content: "\f133";
}
.fa-fire-extinguisher:before {
  content: "\f134";
}
.fa-rocket:before {
  content: "\f135";
}
.fa-maxcdn:before {
  content: "\f136";
}
.fa-chevron-circle-left:before {
  content: "\f137";
}
.fa-chevron-circle-right:before {
  content: "\f138";
}
.fa-chevron-circle-up:before {
  content: "\f139";
}
.fa-chevron-circle-down:before {
  content: "\f13a";
}
.fa-html5:before {
  content: "\f13b";
}
.fa-css3:before {
  content: "\f13c";
}
.fa-anchor:before {
  content: "\f13d";
}
.fa-unlock-alt:before {
  content: "\f13e";
}
.fa-bullseye:before {
  content: "\f140";
}
.fa-ellipsis-h:before {
  content: "\f141";
}
.fa-ellipsis-v:before {
  content: "\f142";
}
.fa-rss-square:before {
  content: "\f143";
}
.fa-play-circle:before {
  content: "\f144";
}
.fa-ticket:before {
  content: "\f145";
}
.fa-minus-square:before {
  content: "\f146";
}
.fa-minus-square-o:before {
  content: "\f147";
}
.fa-level-up:before {
  content: "\f148";
}
.fa-level-down:before {
  content: "\f149";
}
.fa-check-square:before {
  content: "\f14a";
}
.fa-pencil-square:before {
  content: "\f14b";
}
.fa-external-link-square:before {
  content: "\f14c";
}
.fa-share-square:before {
  content: "\f14d";
}
.fa-compass:before {
  content: "\f14e";
}
.fa-toggle-down:before,
.fa-caret-square-o-down:before {
  content: "\f150";
}
.fa-toggle-up:before,
.fa-caret-square-o-up:before {
  content: "\f151";
}
.fa-toggle-right:before,
.fa-caret-square-o-right:before {
  content: "\f152";
}
.fa-euro:before,
.fa-eur:before {
  content: "\f153";
}
.fa-gbp:before {
  content: "\f154";
}
.fa-dollar:before,
.fa-usd:before {
  content: "\f155";
}
.fa-rupee:before,
.fa-inr:before {
  content: "\f156";
}
.fa-cny:before,
.fa-rmb:before,
.fa-yen:before,
.fa-jpy:before {
  content: "\f157";
}
.fa-ruble:before,
.fa-rouble:before,
.fa-rub:before {
  content: "\f158";
}
.fa-won:before,
.fa-krw:before {
  content: "\f159";
}
.fa-bitcoin:before,
.fa-btc:before {
  content: "\f15a";
}
.fa-file:before {
  content: "\f15b";
}
.fa-file-text:before {
  content: "\f15c";
}
.fa-sort-alpha-asc:before {
  content: "\f15d";
}
.fa-sort-alpha-desc:before {
  content: "\f15e";
}
.fa-sort-amount-asc:before {
  content: "\f160";
}
.fa-sort-amount-desc:before {
  content: "\f161";
}
.fa-sort-numeric-asc:before {
  content: "\f162";
}
.fa-sort-numeric-desc:before {
  content: "\f163";
}
.fa-thumbs-up:before {
  content: "\f164";
}
.fa-thumbs-down:before {
  content: "\f165";
}
.fa-youtube-square:before {
  content: "\f166";
}
.fa-youtube:before {
  content: "\f167";
}
.fa-xing:before {
  content: "\f168";
}
.fa-xing-square:before {
  content: "\f169";
}
.fa-youtube-play:before {
  content: "\f16a";
}
.fa-dropbox:before {
  content: "\f16b";
}
.fa-stack-overflow:before {
  content: "\f16c";
}
.fa-instagram:before {
  content: "\f16d";
}
.fa-flickr:before {
  content: "\f16e";
}
.fa-adn:before {
  content: "\f170";
}
.fa-bitbucket:before {
  content: "\f171";
}
.fa-bitbucket-square:before {
  content: "\f172";
}
.fa-tumblr:before {
  content: "\f173";
}
.fa-tumblr-square:before {
  content: "\f174";
}
.fa-long-arrow-down:before {
  content: "\f175";
}
.fa-long-arrow-up:before {
  content: "\f176";
}
.fa-long-arrow-left:before {
  content: "\f177";
}
.fa-long-arrow-right:before {
  content: "\f178";
}
.fa-apple:before {
  content: "\f179";
}
.fa-windows:before {
  content: "\f17a";
}
.fa-android:before {
  content: "\f17b";
}
.fa-linux:before {
  content: "\f17c";
}
.fa-dribbble:before {
  content: "\f17d";
}
.fa-skype:before {
  content: "\f17e";
}
.fa-foursquare:before {
  content: "\f180";
}
.fa-trello:before {
  content: "\f181";
}
.fa-female:before {
  content: "\f182";
}
.fa-male:before {
  content: "\f183";
}
.fa-gittip:before {
  content: "\f184";
}
.fa-sun-o:before {
  content: "\f185";
}
.fa-moon-o:before {
  content: "\f186";
}
.fa-archive:before {
  content: "\f187";
}
.fa-bug:before {
  content: "\f188";
}
.fa-vk:before {
  content: "\f189";
}
.fa-weibo:before {
  content: "\f18a";
}
.fa-renren:before {
  content: "\f18b";
}
.fa-pagelines:before {
  content: "\f18c";
}
.fa-stack-exchange:before {
  content: "\f18d";
}
.fa-arrow-circle-o-right:before {
  content: "\f18e";
}
.fa-arrow-circle-o-left:before {
  content: "\f190";
}
.fa-toggle-left:before,
.fa-caret-square-o-left:before {
  content: "\f191";
}
.fa-dot-circle-o:before {
  content: "\f192";
}
.fa-wheelchair:before {
  content: "\f193";
}
.fa-vimeo-square:before {
  content: "\f194";
}
.fa-turkish-lira:before,
.fa-try:before {
  content: "\f195";
}
.fa-plus-square-o:before {
  content: "\f196";
}
.fa-space-shuttle:before {
  content: "\f197";
}
.fa-slack:before {
  content: "\f198";
}
.fa-envelope-square:before {
  content: "\f199";
}
.fa-wordpress:before {
  content: "\f19a";
}
.fa-openid:before {
  content: "\f19b";
}
.fa-institution:before,
.fa-bank:before,
.fa-university:before {
  content: "\f19c";
}
.fa-mortar-board:before,
.fa-graduation-cap:before {
  content: "\f19d";
}
.fa-yahoo:before {
  content: "\f19e";
}
.fa-google:before {
  content: "\f1a0";
}
.fa-reddit:before {
  content: "\f1a1";
}
.fa-reddit-square:before {
  content: "\f1a2";
}
.fa-stumbleupon-circle:before {
  content: "\f1a3";
}
.fa-stumbleupon:before {
  content: "\f1a4";
}
.fa-delicious:before {
  content: "\f1a5";
}
.fa-digg:before {
  content: "\f1a6";
}
.fa-pied-piper:before {
  content: "\f1a7";
}
.fa-pied-piper-alt:before {
  content: "\f1a8";
}
.fa-drupal:before {
  content: "\f1a9";
}
.fa-joomla:before {
  content: "\f1aa";
}
.fa-language:before {
  content: "\f1ab";
}
.fa-fax:before {
  content: "\f1ac";
}
.fa-building:before {
  content: "\f1ad";
}
.fa-child:before {
  content: "\f1ae";
}
.fa-paw:before {
  content: "\f1b0";
}
.fa-spoon:before {
  content: "\f1b1";
}
.fa-cube:before {
  content: "\f1b2";
}
.fa-cubes:before {
  content: "\f1b3";
}
.fa-behance:before {
  content: "\f1b4";
}
.fa-behance-square:before {
  content: "\f1b5";
}
.fa-steam:before {
  content: "\f1b6";
}
.fa-steam-square:before {
  content: "\f1b7";
}
.fa-recycle:before {
  content: "\f1b8";
}
.fa-automobile:before,
.fa-car:before {
  content: "\f1b9";
}
.fa-cab:before,
.fa-taxi:before {
  content: "\f1ba";
}
.fa-tree:before {
  content: "\f1bb";
}
.fa-spotify:before {
  content: "\f1bc";
}
.fa-deviantart:before {
  content: "\f1bd";
}
.fa-soundcloud:before {
  content: "\f1be";
}
.fa-database:before {
  content: "\f1c0";
}
.fa-file-pdf-o:before {
  content: "\f1c1";
}
.fa-file-word-o:before {
  content: "\f1c2";
}
.fa-file-excel-o:before {
  content: "\f1c3";
}
.fa-file-powerpoint-o:before {
  content: "\f1c4";
}
.fa-file-photo-o:before,
.fa-file-picture-o:before,
.fa-file-image-o:before {
  content: "\f1c5";
}
.fa-file-zip-o:before,
.fa-file-archive-o:before {
  content: "\f1c6";
}
.fa-file-sound-o:before,
.fa-file-audio-o:before {
  content: "\f1c7";
}
.fa-file-movie-o:before,
.fa-file-video-o:before {
  content: "\f1c8";
}
.fa-file-code-o:before {
  content: "\f1c9";
}
.fa-vine:before {
  content: "\f1ca";
}
.fa-codepen:before {
  content: "\f1cb";
}
.fa-jsfiddle:before {
  content: "\f1cc";
}
.fa-life-bouy:before,
.fa-life-buoy:before,
.fa-life-saver:before,
.fa-support:before,
.fa-life-ring:before {
  content: "\f1cd";
}
.fa-circle-o-notch:before {
  content: "\f1ce";
}
.fa-ra:before,
.fa-rebel:before {
  content: "\f1d0";
}
.fa-ge:before,
.fa-empire:before {
  content: "\f1d1";
}
.fa-git-square:before {
  content: "\f1d2";
}
.fa-git:before {
  content: "\f1d3";
}
.fa-hacker-news:before {
  content: "\f1d4";
}
.fa-tencent-weibo:before {
  content: "\f1d5";
}
.fa-qq:before {
  content: "\f1d6";
}
.fa-wechat:before,
.fa-weixin:before {
  content: "\f1d7";
}
.fa-send:before,
.fa-paper-plane:before {
  content: "\f1d8";
}
.fa-send-o:before,
.fa-paper-plane-o:before {
  content: "\f1d9";
}
.fa-history:before {
  content: "\f1da";
}
.fa-circle-thin:before {
  content: "\f1db";
}
.fa-header:before {
  content: "\f1dc";
}
.fa-paragraph:before {
  content: "\f1dd";
}
.fa-sliders:before {
  content: "\f1de";
}
.fa-share-alt:before {
  content: "\f1e0";
}
.fa-share-alt-square:before {
  content: "\f1e1";
}
.fa-bomb:before {
  content: "\f1e2";
}
.fa-soccer-ball-o:before,
.fa-futbol-o:before {
  content: "\f1e3";
}
.fa-tty:before {
  content: "\f1e4";
}
.fa-binoculars:before {
  content: "\f1e5";
}
.fa-plug:before {
  content: "\f1e6";
}
.fa-slideshare:before {
  content: "\f1e7";
}
.fa-twitch:before {
  content: "\f1e8";
}
.fa-yelp:before {
  content: "\f1e9";
}
.fa-newspaper-o:before {
  content: "\f1ea";
}
.fa-wifi:before {
  content: "\f1eb";
}
.fa-calculator:before {
  content: "\f1ec";
}
.fa-paypal:before {
  content: "\f1ed";
}
.fa-google-wallet:before {
  content: "\f1ee";
}
.fa-cc-visa:before {
  content: "\f1f0";
}
.fa-cc-mastercard:before {
  content: "\f1f1";
}
.fa-cc-discover:before {
  content: "\f1f2";
}
.fa-cc-amex:before {
  content: "\f1f3";
}
.fa-cc-paypal:before {
  content: "\f1f4";
}
.fa-cc-stripe:before {
  content: "\f1f5";
}
.fa-bell-slash:before {
  content: "\f1f6";
}
.fa-bell-slash-o:before {
  content: "\f1f7";
}
.fa-trash:before {
  content: "\f1f8";
}
.fa-copyright:before {
  content: "\f1f9";
}
.fa-at:before {
  content: "\f1fa";
}
.fa-eyedropper:before {
  content: "\f1fb";
}
.fa-paint-brush:before {
  content: "\f1fc";
}
.fa-birthday-cake:before {
  content: "\f1fd";
}
.fa-area-chart:before {
  content: "\f1fe";
}
.fa-pie-chart:before {
  content: "\f200";
}
.fa-line-chart:before {
  content: "\f201";
}
.fa-lastfm:before {
  content: "\f202";
}
.fa-lastfm-square:before {
  content: "\f203";
}
.fa-toggle-off:before {
  content: "\f204";
}
.fa-toggle-on:before {
  content: "\f205";
}
.fa-bicycle:before {
  content: "\f206";
}
.fa-bus:before {
  content: "\f207";
}
.fa-ioxhost:before {
  content: "\f208";
}
.fa-angellist:before {
  content: "\f209";
}
.fa-cc:before {
  content: "\f20a";
}
.fa-shekel:before,
.fa-sheqel:before,
.fa-ils:before {
  content: "\f20b";
}
.fa-meanpath:before {
  content: "\f20c";
}
/*!
*
* IPython base
*
*/
.modal.fade .modal-dialog {
  -webkit-transform: translate(0, 0);
  -ms-transform: translate(0, 0);
  -o-transform: translate(0, 0);
  transform: translate(0, 0);
}
code {
  color: #000;
}
pre {
  font-size: inherit;
  line-height: inherit;
}
label {
  font-weight: normal;
}
/* Make the page background atleast 100% the height of the view port */
/* Make the page itself atleast 70% the height of the view port */
.border-box-sizing {
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
.corner-all {
  border-radius: 2px;
}
.no-padding {
  padding: 0px;
}
/* Flexible box model classes */
/* Taken from Alex Russell http://infrequently.org/2009/08/css-3-progress/ */
/* This file is a compatability layer.  It allows the usage of flexible box 
model layouts accross multiple browsers, including older browsers.  The newest,
universal implementation of the flexible box model is used when available (see
`Modern browsers` comments below).  Browsers that are known to implement this 
new spec completely include:

    Firefox 28.0+
    Chrome 29.0+
    Internet Explorer 11+ 
    Opera 17.0+

Browsers not listed, including Safari, are supported via the styling under the
`Old browsers` comments below.
*/
.hbox {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
.hbox > * {
  /* Old browsers */
  -webkit-box-flex: 0;
  -moz-box-flex: 0;
  box-flex: 0;
  /* Modern browsers */
  flex: none;
}
.vbox {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
}
.vbox > * {
  /* Old browsers */
  -webkit-box-flex: 0;
  -moz-box-flex: 0;
  box-flex: 0;
  /* Modern browsers */
  flex: none;
}
.hbox.reverse,
.vbox.reverse,
.reverse {
  /* Old browsers */
  -webkit-box-direction: reverse;
  -moz-box-direction: reverse;
  box-direction: reverse;
  /* Modern browsers */
  flex-direction: row-reverse;
}
.hbox.box-flex0,
.vbox.box-flex0,
.box-flex0 {
  /* Old browsers */
  -webkit-box-flex: 0;
  -moz-box-flex: 0;
  box-flex: 0;
  /* Modern browsers */
  flex: none;
  width: auto;
}
.hbox.box-flex1,
.vbox.box-flex1,
.box-flex1 {
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
}
.hbox.box-flex,
.vbox.box-flex,
.box-flex {
  /* Old browsers */
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
}
.hbox.box-flex2,
.vbox.box-flex2,
.box-flex2 {
  /* Old browsers */
  -webkit-box-flex: 2;
  -moz-box-flex: 2;
  box-flex: 2;
  /* Modern browsers */
  flex: 2;
}
.box-group1 {
  /*  Deprecated */
  -webkit-box-flex-group: 1;
  -moz-box-flex-group: 1;
  box-flex-group: 1;
}
.box-group2 {
  /* Deprecated */
  -webkit-box-flex-group: 2;
  -moz-box-flex-group: 2;
  box-flex-group: 2;
}
.hbox.start,
.vbox.start,
.start {
  /* Old browsers */
  -webkit-box-pack: start;
  -moz-box-pack: start;
  box-pack: start;
  /* Modern browsers */
  justify-content: flex-start;
}
.hbox.end,
.vbox.end,
.end {
  /* Old browsers */
  -webkit-box-pack: end;
  -moz-box-pack: end;
  box-pack: end;
  /* Modern browsers */
  justify-content: flex-end;
}
.hbox.center,
.vbox.center,
.center {
  /* Old browsers */
  -webkit-box-pack: center;
  -moz-box-pack: center;
  box-pack: center;
  /* Modern browsers */
  justify-content: center;
}
.hbox.baseline,
.vbox.baseline,
.baseline {
  /* Old browsers */
  -webkit-box-pack: baseline;
  -moz-box-pack: baseline;
  box-pack: baseline;
  /* Modern browsers */
  justify-content: baseline;
}
.hbox.stretch,
.vbox.stretch,
.stretch {
  /* Old browsers */
  -webkit-box-pack: stretch;
  -moz-box-pack: stretch;
  box-pack: stretch;
  /* Modern browsers */
  justify-content: stretch;
}
.hbox.align-start,
.vbox.align-start,
.align-start {
  /* Old browsers */
  -webkit-box-align: start;
  -moz-box-align: start;
  box-align: start;
  /* Modern browsers */
  align-items: flex-start;
}
.hbox.align-end,
.vbox.align-end,
.align-end {
  /* Old browsers */
  -webkit-box-align: end;
  -moz-box-align: end;
  box-align: end;
  /* Modern browsers */
  align-items: flex-end;
}
.hbox.align-center,
.vbox.align-center,
.align-center {
  /* Old browsers */
  -webkit-box-align: center;
  -moz-box-align: center;
  box-align: center;
  /* Modern browsers */
  align-items: center;
}
.hbox.align-baseline,
.vbox.align-baseline,
.align-baseline {
  /* Old browsers */
  -webkit-box-align: baseline;
  -moz-box-align: baseline;
  box-align: baseline;
  /* Modern browsers */
  align-items: baseline;
}
.hbox.align-stretch,
.vbox.align-stretch,
.align-stretch {
  /* Old browsers */
  -webkit-box-align: stretch;
  -moz-box-align: stretch;
  box-align: stretch;
  /* Modern browsers */
  align-items: stretch;
}
div.error {
  margin: 2em;
  text-align: center;
}
div.error > h1 {
  font-size: 500%;
  line-height: normal;
}
div.error > p {
  font-size: 200%;
  line-height: normal;
}
div.traceback-wrapper {
  text-align: left;
  max-width: 800px;
  margin: auto;
}
/**
 * Primary styles
 *
 * Author: Jupyter Development Team
 */
body {
  background-color: #fff;
  /* This makes sure that the body covers the entire window and needs to
       be in a different element than the display: box in wrapper below */
  position: absolute;
  left: 0px;
  right: 0px;
  top: 0px;
  bottom: 0px;
  overflow: visible;
}
body > #header {
  /* Initially hidden to prevent FLOUC */
  display: none;
  background-color: #fff;
  /* Display over codemirror */
  position: relative;
  z-index: 100;
}
body > #header #header-container {
  padding-bottom: 5px;
  padding-top: 5px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
body > #header .header-bar {
  width: 100%;
  height: 1px;
  background: #e7e7e7;
  margin-bottom: -1px;
}
@media print {
  body > #header {
    display: none !important;
  }
}
#header-spacer {
  width: 100%;
  visibility: hidden;
}
@media print {
  #header-spacer {
    display: none;
  }
}
#ipython_notebook {
  padding-left: 0px;
  padding-top: 1px;
  padding-bottom: 1px;
}
@media (max-width: 991px) {
  #ipython_notebook {
    margin-left: 10px;
  }
}
#noscript {
  width: auto;
  padding-top: 16px;
  padding-bottom: 16px;
  text-align: center;
  font-size: 22px;
  color: red;
  font-weight: bold;
}
#ipython_notebook img {
  height: 28px;
}
#site {
  width: 100%;
  display: none;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  overflow: auto;
}
@media print {
  #site {
    height: auto !important;
  }
}
/* Smaller buttons */
.ui-button .ui-button-text {
  padding: 0.2em 0.8em;
  font-size: 77%;
}
input.ui-button {
  padding: 0.3em 0.9em;
}
span#login_widget {
  float: right;
}
span#login_widget > .button,
#logout {
  color: #333;
  background-color: #fff;
  border-color: #ccc;
}
span#login_widget > .button:focus,
#logout:focus,
span#login_widget > .button.focus,
#logout.focus {
  color: #333;
  background-color: #e6e6e6;
  border-color: #8c8c8c;
}
span#login_widget > .button:hover,
#logout:hover {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
span#login_widget > .button:active,
#logout:active,
span#login_widget > .button.active,
#logout.active,
.open > .dropdown-togglespan#login_widget > .button,
.open > .dropdown-toggle#logout {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
span#login_widget > .button:active:hover,
#logout:active:hover,
span#login_widget > .button.active:hover,
#logout.active:hover,
.open > .dropdown-togglespan#login_widget > .button:hover,
.open > .dropdown-toggle#logout:hover,
span#login_widget > .button:active:focus,
#logout:active:focus,
span#login_widget > .button.active:focus,
#logout.active:focus,
.open > .dropdown-togglespan#login_widget > .button:focus,
.open > .dropdown-toggle#logout:focus,
span#login_widget > .button:active.focus,
#logout:active.focus,
span#login_widget > .button.active.focus,
#logout.active.focus,
.open > .dropdown-togglespan#login_widget > .button.focus,
.open > .dropdown-toggle#logout.focus {
  color: #333;
  background-color: #d4d4d4;
  border-color: #8c8c8c;
}
span#login_widget > .button:active,
#logout:active,
span#login_widget > .button.active,
#logout.active,
.open > .dropdown-togglespan#login_widget > .button,
.open > .dropdown-toggle#logout {
  background-image: none;
}
span#login_widget > .button.disabled:hover,
#logout.disabled:hover,
span#login_widget > .button[disabled]:hover,
#logout[disabled]:hover,
fieldset[disabled] span#login_widget > .button:hover,
fieldset[disabled] #logout:hover,
span#login_widget > .button.disabled:focus,
#logout.disabled:focus,
span#login_widget > .button[disabled]:focus,
#logout[disabled]:focus,
fieldset[disabled] span#login_widget > .button:focus,
fieldset[disabled] #logout:focus,
span#login_widget > .button.disabled.focus,
#logout.disabled.focus,
span#login_widget > .button[disabled].focus,
#logout[disabled].focus,
fieldset[disabled] span#login_widget > .button.focus,
fieldset[disabled] #logout.focus {
  background-color: #fff;
  border-color: #ccc;
}
span#login_widget > .button .badge,
#logout .badge {
  color: #fff;
  background-color: #333;
}
.nav-header {
  text-transform: none;
}
#header > span {
  margin-top: 10px;
}
.modal_stretch .modal-dialog {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
  min-height: 80vh;
}
.modal_stretch .modal-dialog .modal-body {
  max-height: calc(100vh - 200px);
  overflow: auto;
  flex: 1;
}
@media (min-width: 768px) {
  .modal .modal-dialog {
    width: 700px;
  }
}
@media (min-width: 768px) {
  select.form-control {
    margin-left: 12px;
    margin-right: 12px;
  }
}
/*!
*
* IPython auth
*
*/
.center-nav {
  display: inline-block;
  margin-bottom: -4px;
}
/*!
*
* IPython tree view
*
*/
/* We need an invisible input field on top of the sentense*/
/* "Drag file onto the list ..." */
.alternate_upload {
  background-color: none;
  display: inline;
}
.alternate_upload.form {
  padding: 0;
  margin: 0;
}
.alternate_upload input.fileinput {
  text-align: center;
  vertical-align: middle;
  display: inline;
  opacity: 0;
  z-index: 2;
  width: 12ex;
  margin-right: -12ex;
}
.alternate_upload .btn-upload {
  height: 22px;
}
/**
 * Primary styles
 *
 * Author: Jupyter Development Team
 */
ul#tabs {
  margin-bottom: 4px;
}
ul#tabs a {
  padding-top: 6px;
  padding-bottom: 4px;
}
ul.breadcrumb a:focus,
ul.breadcrumb a:hover {
  text-decoration: none;
}
ul.breadcrumb i.icon-home {
  font-size: 16px;
  margin-right: 4px;
}
ul.breadcrumb span {
  color: #5e5e5e;
}
.list_toolbar {
  padding: 4px 0 4px 0;
  vertical-align: middle;
}
.list_toolbar .tree-buttons {
  padding-top: 1px;
}
.dynamic-buttons {
  padding-top: 3px;
  display: inline-block;
}
.list_toolbar [class*="span"] {
  min-height: 24px;
}
.list_header {
  font-weight: bold;
  background-color: #EEE;
}
.list_placeholder {
  font-weight: bold;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 7px;
  padding-right: 7px;
}
.list_container {
  margin-top: 4px;
  margin-bottom: 20px;
  border: 1px solid #ddd;
  border-radius: 2px;
}
.list_container > div {
  border-bottom: 1px solid #ddd;
}
.list_container > div:hover .list-item {
  background-color: red;
}
.list_container > div:last-child {
  border: none;
}
.list_item:hover .list_item {
  background-color: #ddd;
}
.list_item a {
  text-decoration: none;
}
.list_item:hover {
  background-color: #fafafa;
}
.list_header > div,
.list_item > div {
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 7px;
  padding-right: 7px;
  line-height: 22px;
}
.list_header > div input,
.list_item > div input {
  margin-right: 7px;
  margin-left: 14px;
  vertical-align: baseline;
  line-height: 22px;
  position: relative;
  top: -1px;
}
.list_header > div .item_link,
.list_item > div .item_link {
  margin-left: -1px;
  vertical-align: baseline;
  line-height: 22px;
}
.new-file input[type=checkbox] {
  visibility: hidden;
}
.item_name {
  line-height: 22px;
  height: 24px;
}
.item_icon {
  font-size: 14px;
  color: #5e5e5e;
  margin-right: 7px;
  margin-left: 7px;
  line-height: 22px;
  vertical-align: baseline;
}
.item_buttons {
  line-height: 1em;
  margin-left: -5px;
}
.item_buttons .btn,
.item_buttons .btn-group,
.item_buttons .input-group {
  float: left;
}
.item_buttons > .btn,
.item_buttons > .btn-group,
.item_buttons > .input-group {
  margin-left: 5px;
}
.item_buttons .btn {
  min-width: 13ex;
}
.item_buttons .running-indicator {
  padding-top: 4px;
  color: #5cb85c;
}
.item_buttons .kernel-name {
  padding-top: 4px;
  color: #5bc0de;
  margin-right: 7px;
  float: left;
}
.toolbar_info {
  height: 24px;
  line-height: 24px;
}
.list_item input:not([type=checkbox]) {
  padding-top: 3px;
  padding-bottom: 3px;
  height: 22px;
  line-height: 14px;
  margin: 0px;
}
.highlight_text {
  color: blue;
}
#project_name {
  display: inline-block;
  padding-left: 7px;
  margin-left: -2px;
}
#project_name > .breadcrumb {
  padding: 0px;
  margin-bottom: 0px;
  background-color: transparent;
  font-weight: bold;
}
#tree-selector {
  padding-right: 0px;
}
#button-select-all {
  min-width: 50px;
}
#select-all {
  margin-left: 7px;
  margin-right: 2px;
}
.menu_icon {
  margin-right: 2px;
}
.tab-content .row {
  margin-left: 0px;
  margin-right: 0px;
}
.folder_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f114";
}
.folder_icon:before.pull-left {
  margin-right: .3em;
}
.folder_icon:before.pull-right {
  margin-left: .3em;
}
.notebook_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f02d";
  position: relative;
  top: -1px;
}
.notebook_icon:before.pull-left {
  margin-right: .3em;
}
.notebook_icon:before.pull-right {
  margin-left: .3em;
}
.running_notebook_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f02d";
  position: relative;
  top: -1px;
  color: #5cb85c;
}
.running_notebook_icon:before.pull-left {
  margin-right: .3em;
}
.running_notebook_icon:before.pull-right {
  margin-left: .3em;
}
.file_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f016";
  position: relative;
  top: -2px;
}
.file_icon:before.pull-left {
  margin-right: .3em;
}
.file_icon:before.pull-right {
  margin-left: .3em;
}
#notebook_toolbar .pull-right {
  padding-top: 0px;
  margin-right: -1px;
}
ul#new-menu {
  left: auto;
  right: 0;
}
.kernel-menu-icon {
  padding-right: 12px;
  width: 24px;
  content: "\f096";
}
.kernel-menu-icon:before {
  content: "\f096";
}
.kernel-menu-icon-current:before {
  content: "\f00c";
}
#tab_content {
  padding-top: 20px;
}
#running .panel-group .panel {
  margin-top: 3px;
  margin-bottom: 1em;
}
#running .panel-group .panel .panel-heading {
  background-color: #EEE;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 7px;
  padding-right: 7px;
  line-height: 22px;
}
#running .panel-group .panel .panel-heading a:focus,
#running .panel-group .panel .panel-heading a:hover {
  text-decoration: none;
}
#running .panel-group .panel .panel-body {
  padding: 0px;
}
#running .panel-group .panel .panel-body .list_container {
  margin-top: 0px;
  margin-bottom: 0px;
  border: 0px;
  border-radius: 0px;
}
#running .panel-group .panel .panel-body .list_container .list_item {
  border-bottom: 1px solid #ddd;
}
#running .panel-group .panel .panel-body .list_container .list_item:last-child {
  border-bottom: 0px;
}
.delete-button {
  display: none;
}
.duplicate-button {
  display: none;
}
.rename-button {
  display: none;
}
.shutdown-button {
  display: none;
}
.dynamic-instructions {
  display: inline-block;
  padding-top: 4px;
}
/*!
*
* IPython text editor webapp
*
*/
.selected-keymap i.fa {
  padding: 0px 5px;
}
.selected-keymap i.fa:before {
  content: "\f00c";
}
#mode-menu {
  overflow: auto;
  max-height: 20em;
}
.edit_app #header {
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
}
.edit_app #menubar .navbar {
  /* Use a negative 1 bottom margin, so the border overlaps the border of the
    header */
  margin-bottom: -1px;
}
.dirty-indicator {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 20px;
}
.dirty-indicator.pull-left {
  margin-right: .3em;
}
.dirty-indicator.pull-right {
  margin-left: .3em;
}
.dirty-indicator-dirty {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 20px;
}
.dirty-indicator-dirty.pull-left {
  margin-right: .3em;
}
.dirty-indicator-dirty.pull-right {
  margin-left: .3em;
}
.dirty-indicator-clean {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 20px;
}
.dirty-indicator-clean.pull-left {
  margin-right: .3em;
}
.dirty-indicator-clean.pull-right {
  margin-left: .3em;
}
.dirty-indicator-clean:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f00c";
}
.dirty-indicator-clean:before.pull-left {
  margin-right: .3em;
}
.dirty-indicator-clean:before.pull-right {
  margin-left: .3em;
}
#filename {
  font-size: 16pt;
  display: table;
  padding: 0px 5px;
}
#current-mode {
  padding-left: 5px;
  padding-right: 5px;
}
#texteditor-backdrop {
  padding-top: 20px;
  padding-bottom: 20px;
}
@media not print {
  #texteditor-backdrop {
    background-color: #EEE;
  }
}
@media print {
  #texteditor-backdrop #texteditor-container .CodeMirror-gutter,
  #texteditor-backdrop #texteditor-container .CodeMirror-gutters {
    background-color: #fff;
  }
}
@media not print {
  #texteditor-backdrop #texteditor-container .CodeMirror-gutter,
  #texteditor-backdrop #texteditor-container .CodeMirror-gutters {
    background-color: #fff;
  }
}
@media not print {
  #texteditor-backdrop #texteditor-container {
    padding: 0px;
    background-color: #fff;
    -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
    box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  }
}
/*!
*
* IPython notebook
*
*/
/* CSS font colors for translated ANSI colors. */
.ansibold {
  font-weight: bold;
}
/* use dark versions for foreground, to improve visibility */
.ansiblack {
  color: black;
}
.ansired {
  color: darkred;
}
.ansigreen {
  color: darkgreen;
}
.ansiyellow {
  color: #c4a000;
}
.ansiblue {
  color: darkblue;
}
.ansipurple {
  color: darkviolet;
}
.ansicyan {
  color: steelblue;
}
.ansigray {
  color: gray;
}
/* and light for background, for the same reason */
.ansibgblack {
  background-color: black;
}
.ansibgred {
  background-color: red;
}
.ansibggreen {
  background-color: green;
}
.ansibgyellow {
  background-color: yellow;
}
.ansibgblue {
  background-color: blue;
}
.ansibgpurple {
  background-color: magenta;
}
.ansibgcyan {
  background-color: cyan;
}
.ansibggray {
  background-color: gray;
}
div.cell {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
  border-radius: 2px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  border-width: 1px;
  border-style: solid;
  border-color: transparent;
  width: 100%;
  padding: 5px;
  /* This acts as a spacer between cells, that is outside the border */
  margin: 0px;
  outline: none;
  border-left-width: 1px;
  padding-left: 5px;
  background: linear-gradient(to right, transparent -40px, transparent 1px, transparent 1px, transparent 100%);
}
div.cell.jupyter-soft-selected {
  border-left-color: #90CAF9;
  border-left-color: #E3F2FD;
  border-left-width: 1px;
  padding-left: 5px;
  border-right-color: #E3F2FD;
  border-right-width: 1px;
  background: #E3F2FD;
}
@media print {
  div.cell.jupyter-soft-selected {
    border-color: transparent;
  }
}
div.cell.selected {
  border-color: #ababab;
  border-left-width: 0px;
  padding-left: 6px;
  background: linear-gradient(to right, #42A5F5 -40px, #42A5F5 5px, transparent 5px, transparent 100%);
}
@media print {
  div.cell.selected {
    border-color: transparent;
  }
}
div.cell.selected.jupyter-soft-selected {
  border-left-width: 0;
  padding-left: 6px;
  background: linear-gradient(to right, #42A5F5 -40px, #42A5F5 7px, #E3F2FD 7px, #E3F2FD 100%);
}
.edit_mode div.cell.selected {
  border-color: #66BB6A;
  border-left-width: 0px;
  padding-left: 6px;
  background: linear-gradient(to right, #66BB6A -40px, #66BB6A 5px, transparent 5px, transparent 100%);
}
@media print {
  .edit_mode div.cell.selected {
    border-color: transparent;
  }
}
.prompt {
  /* This needs to be wide enough for 3 digit prompt numbers: In[100]: */
  min-width: 14ex;
  /* This padding is tuned to match the padding on the CodeMirror editor. */
  padding: 0.4em;
  margin: 0px;
  font-family: monospace;
  text-align: right;
  /* This has to match that of the the CodeMirror class line-height below */
  line-height: 1.21429em;
  /* Don't highlight prompt number selection */
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  /* Use default cursor */
  cursor: default;
}
@media (max-width: 540px) {
  .prompt {
    text-align: left;
  }
}
div.inner_cell {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
}
@-moz-document url-prefix() {
  div.inner_cell {
    overflow-x: hidden;
  }
}
/* input_area and input_prompt must match in top border and margin for alignment */
div.input_area {
  border: 1px solid #cfcfcf;
  border-radius: 2px;
  background: #f7f7f7;
  line-height: 1.21429em;
}
/* This is needed so that empty prompt areas can collapse to zero height when there
   is no content in the output_subarea and the prompt. The main purpose of this is
   to make sure that empty JavaScript output_subareas have no height. */
div.prompt:empty {
  padding-top: 0;
  padding-bottom: 0;
}
div.unrecognized_cell {
  padding: 5px 5px 5px 0px;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
div.unrecognized_cell .inner_cell {
  border-radius: 2px;
  padding: 5px;
  font-weight: bold;
  color: red;
  border: 1px solid #cfcfcf;
  background: #eaeaea;
}
div.unrecognized_cell .inner_cell a {
  color: inherit;
  text-decoration: none;
}
div.unrecognized_cell .inner_cell a:hover {
  color: inherit;
  text-decoration: none;
}
@media (max-width: 540px) {
  div.unrecognized_cell > div.prompt {
    display: none;
  }
}
div.code_cell {
  /* avoid page breaking on code cells when printing */
}
@media print {
  div.code_cell {
    page-break-inside: avoid;
  }
}
/* any special styling for code cells that are currently running goes here */
div.input {
  page-break-inside: avoid;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
@media (max-width: 540px) {
  div.input {
    /* Old browsers */
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-box-align: stretch;
    display: -moz-box;
    -moz-box-orient: vertical;
    -moz-box-align: stretch;
    display: box;
    box-orient: vertical;
    box-align: stretch;
    /* Modern browsers */
    display: flex;
    flex-direction: column;
    align-items: stretch;
  }
}
/* input_area and input_prompt must match in top border and margin for alignment */
div.input_prompt {
  color: #303F9F;
  border-top: 1px solid transparent;
}
div.input_area > div.highlight {
  margin: 0.4em;
  border: none;
  padding: 0px;
  background-color: transparent;
}
div.input_area > div.highlight > pre {
  margin: 0px;
  border: none;
  padding: 0px;
  background-color: transparent;
}
/* The following gets added to the <head> if it is detected that the user has a
 * monospace font with inconsistent normal/bold/italic height.  See
 * notebookmain.js.  Such fonts will have keywords vertically offset with
 * respect to the rest of the text.  The user should select a better font.
 * See: https://github.com/ipython/ipython/issues/1503
 *
 * .CodeMirror span {
 *      vertical-align: bottom;
 * }
 */
.CodeMirror {
  line-height: 1.21429em;
  /* Changed from 1em to our global default */
  font-size: 14px;
  height: auto;
  /* Changed to auto to autogrow */
  background: none;
  /* Changed from white to allow our bg to show through */
}
.CodeMirror-scroll {
  /*  The CodeMirror docs are a bit fuzzy on if overflow-y should be hidden or visible.*/
  /*  We have found that if it is visible, vertical scrollbars appear with font size changes.*/
  overflow-y: hidden;
  overflow-x: auto;
}
.CodeMirror-lines {
  /* In CM2, this used to be 0.4em, but in CM3 it went to 4px. We need the em value because */
  /* we have set a different line-height and want this to scale with that. */
  padding: 0.4em;
}
.CodeMirror-linenumber {
  padding: 0 8px 0 4px;
}
.CodeMirror-gutters {
  border-bottom-left-radius: 2px;
  border-top-left-radius: 2px;
}
.CodeMirror pre {
  /* In CM3 this went to 4px from 0 in CM2. We need the 0 value because of how we size */
  /* .CodeMirror-lines */
  padding: 0;
  border: 0;
  border-radius: 0;
}
/*

Original style from softwaremaniacs.org (c) Ivan Sagalaev <Maniac@SoftwareManiacs.Org>
Adapted from GitHub theme

*/
.highlight-base {
  color: #000;
}
.highlight-variable {
  color: #000;
}
.highlight-variable-2 {
  color: #1a1a1a;
}
.highlight-variable-3 {
  color: #333333;
}
.highlight-string {
  color: #BA2121;
}
.highlight-comment {
  color: #408080;
  font-style: italic;
}
.highlight-number {
  color: #080;
}
.highlight-atom {
  color: #88F;
}
.highlight-keyword {
  color: #008000;
  font-weight: bold;
}
.highlight-builtin {
  color: #008000;
}
.highlight-error {
  color: #f00;
}
.highlight-operator {
  color: #AA22FF;
  font-weight: bold;
}
.highlight-meta {
  color: #AA22FF;
}
/* previously not defined, copying from default codemirror */
.highlight-def {
  color: #00f;
}
.highlight-string-2 {
  color: #f50;
}
.highlight-qualifier {
  color: #555;
}
.highlight-bracket {
  color: #997;
}
.highlight-tag {
  color: #170;
}
.highlight-attribute {
  color: #00c;
}
.highlight-header {
  color: blue;
}
.highlight-quote {
  color: #090;
}
.highlight-link {
  color: #00c;
}
/* apply the same style to codemirror */
.cm-s-ipython span.cm-keyword {
  color: #008000;
  font-weight: bold;
}
.cm-s-ipython span.cm-atom {
  color: #88F;
}
.cm-s-ipython span.cm-number {
  color: #080;
}
.cm-s-ipython span.cm-def {
  color: #00f;
}
.cm-s-ipython span.cm-variable {
  color: #000;
}
.cm-s-ipython span.cm-operator {
  color: #AA22FF;
  font-weight: bold;
}
.cm-s-ipython span.cm-variable-2 {
  color: #1a1a1a;
}
.cm-s-ipython span.cm-variable-3 {
  color: #333333;
}
.cm-s-ipython span.cm-comment {
  color: #408080;
  font-style: italic;
}
.cm-s-ipython span.cm-string {
  color: #BA2121;
}
.cm-s-ipython span.cm-string-2 {
  color: #f50;
}
.cm-s-ipython span.cm-meta {
  color: #AA22FF;
}
.cm-s-ipython span.cm-qualifier {
  color: #555;
}
.cm-s-ipython span.cm-builtin {
  color: #008000;
}
.cm-s-ipython span.cm-bracket {
  color: #997;
}
.cm-s-ipython span.cm-tag {
  color: #170;
}
.cm-s-ipython span.cm-attribute {
  color: #00c;
}
.cm-s-ipython span.cm-header {
  color: blue;
}
.cm-s-ipython span.cm-quote {
  color: #090;
}
.cm-s-ipython span.cm-link {
  color: #00c;
}
.cm-s-ipython span.cm-error {
  color: #f00;
}
.cm-s-ipython span.cm-tab {
  background: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADAAAAAMCAYAAAAkuj5RAAAAAXNSR0IArs4c6QAAAGFJREFUSMft1LsRQFAQheHPowAKoACx3IgEKtaEHujDjORSgWTH/ZOdnZOcM/sgk/kFFWY0qV8foQwS4MKBCS3qR6ixBJvElOobYAtivseIE120FaowJPN75GMu8j/LfMwNjh4HUpwg4LUAAAAASUVORK5CYII=);
  background-position: right;
  background-repeat: no-repeat;
}
div.output_wrapper {
  /* this position must be relative to enable descendents to be absolute within it */
  position: relative;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
  z-index: 1;
}
/* class for the output area when it should be height-limited */
div.output_scroll {
  /* ideally, this would be max-height, but FF barfs all over that */
  height: 24em;
  /* FF needs this *and the wrapper* to specify full width, or it will shrinkwrap */
  width: 100%;
  overflow: auto;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 2px 8px rgba(0, 0, 0, 0.8);
  box-shadow: inset 0 2px 8px rgba(0, 0, 0, 0.8);
  display: block;
}
/* output div while it is collapsed */
div.output_collapsed {
  margin: 0px;
  padding: 0px;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
}
div.out_prompt_overlay {
  height: 100%;
  padding: 0px 0.4em;
  position: absolute;
  border-radius: 2px;
}
div.out_prompt_overlay:hover {
  /* use inner shadow to get border that is computed the same on WebKit/FF */
  -webkit-box-shadow: inset 0 0 1px #000;
  box-shadow: inset 0 0 1px #000;
  background: rgba(240, 240, 240, 0.5);
}
div.output_prompt {
  color: #D84315;
}
/* This class is the outer container of all output sections. */
div.output_area {
  padding: 0px;
  page-break-inside: avoid;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
div.output_area .MathJax_Display {
  text-align: left !important;
}
div.output_area .rendered_html table {
  margin-left: 0;
  margin-right: 0;
}
div.output_area .rendered_html img {
  margin-left: 0;
  margin-right: 0;
}
div.output_area img,
div.output_area svg {
  max-width: 100%;
  height: auto;
}
div.output_area img.unconfined,
div.output_area svg.unconfined {
  max-width: none;
}
/* This is needed to protect the pre formating from global settings such
   as that of bootstrap */
.output {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
}
@media (max-width: 540px) {
  div.output_area {
    /* Old browsers */
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-box-align: stretch;
    display: -moz-box;
    -moz-box-orient: vertical;
    -moz-box-align: stretch;
    display: box;
    box-orient: vertical;
    box-align: stretch;
    /* Modern browsers */
    display: flex;
    flex-direction: column;
    align-items: stretch;
  }
}
div.output_area pre {
  margin: 0;
  padding: 0;
  border: 0;
  vertical-align: baseline;
  color: black;
  background-color: transparent;
  border-radius: 0;
}
/* This class is for the output subarea inside the output_area and after
   the prompt div. */
div.output_subarea {
  overflow-x: auto;
  padding: 0.4em;
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
  max-width: calc(100% - 14ex);
}
div.output_scroll div.output_subarea {
  overflow-x: visible;
}
/* The rest of the output_* classes are for special styling of the different
   output types */
/* all text output has this class: */
div.output_text {
  text-align: left;
  color: #000;
  /* This has to match that of the the CodeMirror class line-height below */
  line-height: 1.21429em;
}
/* stdout/stderr are 'text' as well as 'stream', but execute_result/error are *not* streams */
div.output_stderr {
  background: #fdd;
  /* very light red background for stderr */
}
div.output_latex {
  text-align: left;
}
/* Empty output_javascript divs should have no height */
div.output_javascript:empty {
  padding: 0;
}
.js-error {
  color: darkred;
}
/* raw_input styles */
div.raw_input_container {
  line-height: 1.21429em;
  padding-top: 5px;
}
pre.raw_input_prompt {
  /* nothing needed here. */
}
input.raw_input {
  font-family: monospace;
  font-size: inherit;
  color: inherit;
  width: auto;
  /* make sure input baseline aligns with prompt */
  vertical-align: baseline;
  /* padding + margin = 0.5em between prompt and cursor */
  padding: 0em 0.25em;
  margin: 0em 0.25em;
}
input.raw_input:focus {
  box-shadow: none;
}
p.p-space {
  margin-bottom: 10px;
}
div.output_unrecognized {
  padding: 5px;
  font-weight: bold;
  color: red;
}
div.output_unrecognized a {
  color: inherit;
  text-decoration: none;
}
div.output_unrecognized a:hover {
  color: inherit;
  text-decoration: none;
}
.rendered_html {
  color: #000;
  /* any extras will just be numbers: */
}
.rendered_html em {
  font-style: italic;
}
.rendered_html strong {
  font-weight: bold;
}
.rendered_html u {
  text-decoration: underline;
}
.rendered_html :link {
  text-decoration: underline;
}
.rendered_html :visited {
  text-decoration: underline;
}
.rendered_html h1 {
  font-size: 185.7%;
  margin: 1.08em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
}
.rendered_html h2 {
  font-size: 157.1%;
  margin: 1.27em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
}
.rendered_html h3 {
  font-size: 128.6%;
  margin: 1.55em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
}
.rendered_html h4 {
  font-size: 100%;
  margin: 2em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
}
.rendered_html h5 {
  font-size: 100%;
  margin: 2em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
  font-style: italic;
}
.rendered_html h6 {
  font-size: 100%;
  margin: 2em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
  font-style: italic;
}
.rendered_html h1:first-child {
  margin-top: 0.538em;
}
.rendered_html h2:first-child {
  margin-top: 0.636em;
}
.rendered_html h3:first-child {
  margin-top: 0.777em;
}
.rendered_html h4:first-child {
  margin-top: 1em;
}
.rendered_html h5:first-child {
  margin-top: 1em;
}
.rendered_html h6:first-child {
  margin-top: 1em;
}
.rendered_html ul {
  list-style: disc;
  margin: 0em 2em;
  padding-left: 0px;
}
.rendered_html ul ul {
  list-style: square;
  margin: 0em 2em;
}
.rendered_html ul ul ul {
  list-style: circle;
  margin: 0em 2em;
}
.rendered_html ol {
  list-style: decimal;
  margin: 0em 2em;
  padding-left: 0px;
}
.rendered_html ol ol {
  list-style: upper-alpha;
  margin: 0em 2em;
}
.rendered_html ol ol ol {
  list-style: lower-alpha;
  margin: 0em 2em;
}
.rendered_html ol ol ol ol {
  list-style: lower-roman;
  margin: 0em 2em;
}
.rendered_html ol ol ol ol ol {
  list-style: decimal;
  margin: 0em 2em;
}
.rendered_html * + ul {
  margin-top: 1em;
}
.rendered_html * + ol {
  margin-top: 1em;
}
.rendered_html hr {
  color: black;
  background-color: black;
}
.rendered_html pre {
  margin: 1em 2em;
}
.rendered_html pre,
.rendered_html code {
  border: 0;
  background-color: #fff;
  color: #000;
  font-size: 100%;
  padding: 0px;
}
.rendered_html blockquote {
  margin: 1em 2em;
}
.rendered_html table {
  margin-left: auto;
  margin-right: auto;
  border: 1px solid black;
  border-collapse: collapse;
}
.rendered_html tr,
.rendered_html th,
.rendered_html td {
  border: 1px solid black;
  border-collapse: collapse;
  margin: 1em 2em;
}
.rendered_html td,
.rendered_html th {
  text-align: left;
  vertical-align: middle;
  padding: 4px;
}
.rendered_html th {
  font-weight: bold;
}
.rendered_html * + table {
  margin-top: 1em;
}
.rendered_html p {
  text-align: left;
}
.rendered_html * + p {
  margin-top: 1em;
}
.rendered_html img {
  display: block;
  margin-left: auto;
  margin-right: auto;
}
.rendered_html * + img {
  margin-top: 1em;
}
.rendered_html img,
.rendered_html svg {
  max-width: 100%;
  height: auto;
}
.rendered_html img.unconfined,
.rendered_html svg.unconfined {
  max-width: none;
}
div.text_cell {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
@media (max-width: 540px) {
  div.text_cell > div.prompt {
    display: none;
  }
}
div.text_cell_render {
  /*font-family: "Helvetica Neue", Arial, Helvetica, Geneva, sans-serif;*/
  outline: none;
  resize: none;
  width: inherit;
  border-style: none;
  padding: 0.5em 0.5em 0.5em 0.4em;
  color: #000;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
a.anchor-link:link {
  text-decoration: none;
  padding: 0px 20px;
  visibility: hidden;
}
h1:hover .anchor-link,
h2:hover .anchor-link,
h3:hover .anchor-link,
h4:hover .anchor-link,
h5:hover .anchor-link,
h6:hover .anchor-link {
  visibility: visible;
}
.text_cell.rendered .input_area {
  display: none;
}
.text_cell.rendered .rendered_html {
  overflow-x: auto;
  overflow-y: hidden;
}
.text_cell.unrendered .text_cell_render {
  display: none;
}
.cm-header-1,
.cm-header-2,
.cm-header-3,
.cm-header-4,
.cm-header-5,
.cm-header-6 {
  font-weight: bold;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
}
.cm-header-1 {
  font-size: 185.7%;
}
.cm-header-2 {
  font-size: 157.1%;
}
.cm-header-3 {
  font-size: 128.6%;
}
.cm-header-4 {
  font-size: 110%;
}
.cm-header-5 {
  font-size: 100%;
  font-style: italic;
}
.cm-header-6 {
  font-size: 100%;
  font-style: italic;
}
/*!
*
* IPython notebook webapp
*
*/
@media (max-width: 767px) {
  .notebook_app {
    padding-left: 0px;
    padding-right: 0px;
  }
}
#ipython-main-app {
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  height: 100%;
}
div#notebook_panel {
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  height: 100%;
}
div#notebook {
  font-size: 14px;
  line-height: 20px;
  overflow-y: hidden;
  overflow-x: auto;
  width: 100%;
  /* This spaces the page away from the edge of the notebook area */
  padding-top: 20px;
  margin: 0px;
  outline: none;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  min-height: 100%;
}
@media not print {
  #notebook-container {
    padding: 15px;
    background-color: #fff;
    min-height: 0;
    -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
    box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  }
}
@media print {
  #notebook-container {
    width: 100%;
  }
}
div.ui-widget-content {
  border: 1px solid #ababab;
  outline: none;
}
pre.dialog {
  background-color: #f7f7f7;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding: 0.4em;
  padding-left: 2em;
}
p.dialog {
  padding: 0.2em;
}
/* Word-wrap output correctly.  This is the CSS3 spelling, though Firefox seems
   to not honor it correctly.  Webkit browsers (Chrome, rekonq, Safari) do.
 */
pre,
code,
kbd,
samp {
  white-space: pre-wrap;
}
#fonttest {
  font-family: monospace;
}
p {
  margin-bottom: 0;
}
.end_space {
  min-height: 100px;
  transition: height .2s ease;
}
.notebook_app > #header {
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
}
@media not print {
  .notebook_app {
    background-color: #EEE;
  }
}
kbd {
  border-style: solid;
  border-width: 1px;
  box-shadow: none;
  margin: 2px;
  padding-left: 2px;
  padding-right: 2px;
  padding-top: 1px;
  padding-bottom: 1px;
}
/* CSS for the cell toolbar */
.celltoolbar {
  border: thin solid #CFCFCF;
  border-bottom: none;
  background: #EEE;
  border-radius: 2px 2px 0px 0px;
  width: 100%;
  height: 29px;
  padding-right: 4px;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
  /* Old browsers */
  -webkit-box-pack: end;
  -moz-box-pack: end;
  box-pack: end;
  /* Modern browsers */
  justify-content: flex-end;
  display: -webkit-flex;
}
@media print {
  .celltoolbar {
    display: none;
  }
}
.ctb_hideshow {
  display: none;
  vertical-align: bottom;
}
/* ctb_show is added to the ctb_hideshow div to show the cell toolbar.
   Cell toolbars are only shown when the ctb_global_show class is also set.
*/
.ctb_global_show .ctb_show.ctb_hideshow {
  display: block;
}
.ctb_global_show .ctb_show + .input_area,
.ctb_global_show .ctb_show + div.text_cell_input,
.ctb_global_show .ctb_show ~ div.text_cell_render {
  border-top-right-radius: 0px;
  border-top-left-radius: 0px;
}
.ctb_global_show .ctb_show ~ div.text_cell_render {
  border: 1px solid #cfcfcf;
}
.celltoolbar {
  font-size: 87%;
  padding-top: 3px;
}
.celltoolbar select {
  display: block;
  width: 100%;
  height: 32px;
  padding: 6px 12px;
  font-size: 13px;
  line-height: 1.42857143;
  color: #555555;
  background-color: #fff;
  background-image: none;
  border: 1px solid #ccc;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  -webkit-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  -o-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  height: 30px;
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
  width: inherit;
  font-size: inherit;
  height: 22px;
  padding: 0px;
  display: inline-block;
}
.celltoolbar select:focus {
  border-color: #66afe9;
  outline: 0;
  -webkit-box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
  box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
}
.celltoolbar select::-moz-placeholder {
  color: #999;
  opacity: 1;
}
.celltoolbar select:-ms-input-placeholder {
  color: #999;
}
.celltoolbar select::-webkit-input-placeholder {
  color: #999;
}
.celltoolbar select::-ms-expand {
  border: 0;
  background-color: transparent;
}
.celltoolbar select[disabled],
.celltoolbar select[readonly],
fieldset[disabled] .celltoolbar select {
  background-color: #eeeeee;
  opacity: 1;
}
.celltoolbar select[disabled],
fieldset[disabled] .celltoolbar select {
  cursor: not-allowed;
}
textarea.celltoolbar select {
  height: auto;
}
select.celltoolbar select {
  height: 30px;
  line-height: 30px;
}
textarea.celltoolbar select,
select[multiple].celltoolbar select {
  height: auto;
}
.celltoolbar label {
  margin-left: 5px;
  margin-right: 5px;
}
.completions {
  position: absolute;
  z-index: 110;
  overflow: hidden;
  border: 1px solid #ababab;
  border-radius: 2px;
  -webkit-box-shadow: 0px 6px 10px -1px #adadad;
  box-shadow: 0px 6px 10px -1px #adadad;
  line-height: 1;
}
.completions select {
  background: white;
  outline: none;
  border: none;
  padding: 0px;
  margin: 0px;
  overflow: auto;
  font-family: monospace;
  font-size: 110%;
  color: #000;
  width: auto;
}
.completions select option.context {
  color: #286090;
}
#kernel_logo_widget {
  float: right !important;
  float: right;
}
#kernel_logo_widget .current_kernel_logo {
  display: none;
  margin-top: -1px;
  margin-bottom: -1px;
  width: 32px;
  height: 32px;
}
#menubar {
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  margin-top: 1px;
}
#menubar .navbar {
  border-top: 1px;
  border-radius: 0px 0px 2px 2px;
  margin-bottom: 0px;
}
#menubar .navbar-toggle {
  float: left;
  padding-top: 7px;
  padding-bottom: 7px;
  border: none;
}
#menubar .navbar-collapse {
  clear: left;
}
.nav-wrapper {
  border-bottom: 1px solid #e7e7e7;
}
i.menu-icon {
  padding-top: 4px;
}
ul#help_menu li a {
  overflow: hidden;
  padding-right: 2.2em;
}
ul#help_menu li a i {
  margin-right: -1.2em;
}
.dropdown-submenu {
  position: relative;
}
.dropdown-submenu > .dropdown-menu {
  top: 0;
  left: 100%;
  margin-top: -6px;
  margin-left: -1px;
}
.dropdown-submenu:hover > .dropdown-menu {
  display: block;
}
.dropdown-submenu > a:after {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: block;
  content: "\f0da";
  float: right;
  color: #333333;
  margin-top: 2px;
  margin-right: -10px;
}
.dropdown-submenu > a:after.pull-left {
  margin-right: .3em;
}
.dropdown-submenu > a:after.pull-right {
  margin-left: .3em;
}
.dropdown-submenu:hover > a:after {
  color: #262626;
}
.dropdown-submenu.pull-left {
  float: none;
}
.dropdown-submenu.pull-left > .dropdown-menu {
  left: -100%;
  margin-left: 10px;
}
#notification_area {
  float: right !important;
  float: right;
  z-index: 10;
}
.indicator_area {
  float: right !important;
  float: right;
  color: #777;
  margin-left: 5px;
  margin-right: 5px;
  width: 11px;
  z-index: 10;
  text-align: center;
  width: auto;
}
#kernel_indicator {
  float: right !important;
  float: right;
  color: #777;
  margin-left: 5px;
  margin-right: 5px;
  width: 11px;
  z-index: 10;
  text-align: center;
  width: auto;
  border-left: 1px solid;
}
#kernel_indicator .kernel_indicator_name {
  padding-left: 5px;
  padding-right: 5px;
}
#modal_indicator {
  float: right !important;
  float: right;
  color: #777;
  margin-left: 5px;
  margin-right: 5px;
  width: 11px;
  z-index: 10;
  text-align: center;
  width: auto;
}
#readonly-indicator {
  float: right !important;
  float: right;
  color: #777;
  margin-left: 5px;
  margin-right: 5px;
  width: 11px;
  z-index: 10;
  text-align: center;
  width: auto;
  margin-top: 2px;
  margin-bottom: 0px;
  margin-left: 0px;
  margin-right: 0px;
  display: none;
}
.modal_indicator:before {
  width: 1.28571429em;
  text-align: center;
}
.edit_mode .modal_indicator:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f040";
}
.edit_mode .modal_indicator:before.pull-left {
  margin-right: .3em;
}
.edit_mode .modal_indicator:before.pull-right {
  margin-left: .3em;
}
.command_mode .modal_indicator:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: ' ';
}
.command_mode .modal_indicator:before.pull-left {
  margin-right: .3em;
}
.command_mode .modal_indicator:before.pull-right {
  margin-left: .3em;
}
.kernel_idle_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f10c";
}
.kernel_idle_icon:before.pull-left {
  margin-right: .3em;
}
.kernel_idle_icon:before.pull-right {
  margin-left: .3em;
}
.kernel_busy_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f111";
}
.kernel_busy_icon:before.pull-left {
  margin-right: .3em;
}
.kernel_busy_icon:before.pull-right {
  margin-left: .3em;
}
.kernel_dead_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f1e2";
}
.kernel_dead_icon:before.pull-left {
  margin-right: .3em;
}
.kernel_dead_icon:before.pull-right {
  margin-left: .3em;
}
.kernel_disconnected_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f127";
}
.kernel_disconnected_icon:before.pull-left {
  margin-right: .3em;
}
.kernel_disconnected_icon:before.pull-right {
  margin-left: .3em;
}
.notification_widget {
  color: #777;
  z-index: 10;
  background: rgba(240, 240, 240, 0.5);
  margin-right: 4px;
  color: #333;
  background-color: #fff;
  border-color: #ccc;
}
.notification_widget:focus,
.notification_widget.focus {
  color: #333;
  background-color: #e6e6e6;
  border-color: #8c8c8c;
}
.notification_widget:hover {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
.notification_widget:active,
.notification_widget.active,
.open > .dropdown-toggle.notification_widget {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
.notification_widget:active:hover,
.notification_widget.active:hover,
.open > .dropdown-toggle.notification_widget:hover,
.notification_widget:active:focus,
.notification_widget.active:focus,
.open > .dropdown-toggle.notification_widget:focus,
.notification_widget:active.focus,
.notification_widget.active.focus,
.open > .dropdown-toggle.notification_widget.focus {
  color: #333;
  background-color: #d4d4d4;
  border-color: #8c8c8c;
}
.notification_widget:active,
.notification_widget.active,
.open > .dropdown-toggle.notification_widget {
  background-image: none;
}
.notification_widget.disabled:hover,
.notification_widget[disabled]:hover,
fieldset[disabled] .notification_widget:hover,
.notification_widget.disabled:focus,
.notification_widget[disabled]:focus,
fieldset[disabled] .notification_widget:focus,
.notification_widget.disabled.focus,
.notification_widget[disabled].focus,
fieldset[disabled] .notification_widget.focus {
  background-color: #fff;
  border-color: #ccc;
}
.notification_widget .badge {
  color: #fff;
  background-color: #333;
}
.notification_widget.warning {
  color: #fff;
  background-color: #f0ad4e;
  border-color: #eea236;
}
.notification_widget.warning:focus,
.notification_widget.warning.focus {
  color: #fff;
  background-color: #ec971f;
  border-color: #985f0d;
}
.notification_widget.warning:hover {
  color: #fff;
  background-color: #ec971f;
  border-color: #d58512;
}
.notification_widget.warning:active,
.notification_widget.warning.active,
.open > .dropdown-toggle.notification_widget.warning {
  color: #fff;
  background-color: #ec971f;
  border-color: #d58512;
}
.notification_widget.warning:active:hover,
.notification_widget.warning.active:hover,
.open > .dropdown-toggle.notification_widget.warning:hover,
.notification_widget.warning:active:focus,
.notification_widget.warning.active:focus,
.open > .dropdown-toggle.notification_widget.warning:focus,
.notification_widget.warning:active.focus,
.notification_widget.warning.active.focus,
.open > .dropdown-toggle.notification_widget.warning.focus {
  color: #fff;
  background-color: #d58512;
  border-color: #985f0d;
}
.notification_widget.warning:active,
.notification_widget.warning.active,
.open > .dropdown-toggle.notification_widget.warning {
  background-image: none;
}
.notification_widget.warning.disabled:hover,
.notification_widget.warning[disabled]:hover,
fieldset[disabled] .notification_widget.warning:hover,
.notification_widget.warning.disabled:focus,
.notification_widget.warning[disabled]:focus,
fieldset[disabled] .notification_widget.warning:focus,
.notification_widget.warning.disabled.focus,
.notification_widget.warning[disabled].focus,
fieldset[disabled] .notification_widget.warning.focus {
  background-color: #f0ad4e;
  border-color: #eea236;
}
.notification_widget.warning .badge {
  color: #f0ad4e;
  background-color: #fff;
}
.notification_widget.success {
  color: #fff;
  background-color: #5cb85c;
  border-color: #4cae4c;
}
.notification_widget.success:focus,
.notification_widget.success.focus {
  color: #fff;
  background-color: #449d44;
  border-color: #255625;
}
.notification_widget.success:hover {
  color: #fff;
  background-color: #449d44;
  border-color: #398439;
}
.notification_widget.success:active,
.notification_widget.success.active,
.open > .dropdown-toggle.notification_widget.success {
  color: #fff;
  background-color: #449d44;
  border-color: #398439;
}
.notification_widget.success:active:hover,
.notification_widget.success.active:hover,
.open > .dropdown-toggle.notification_widget.success:hover,
.notification_widget.success:active:focus,
.notification_widget.success.active:focus,
.open > .dropdown-toggle.notification_widget.success:focus,
.notification_widget.success:active.focus,
.notification_widget.success.active.focus,
.open > .dropdown-toggle.notification_widget.success.focus {
  color: #fff;
  background-color: #398439;
  border-color: #255625;
}
.notification_widget.success:active,
.notification_widget.success.active,
.open > .dropdown-toggle.notification_widget.success {
  background-image: none;
}
.notification_widget.success.disabled:hover,
.notification_widget.success[disabled]:hover,
fieldset[disabled] .notification_widget.success:hover,
.notification_widget.success.disabled:focus,
.notification_widget.success[disabled]:focus,
fieldset[disabled] .notification_widget.success:focus,
.notification_widget.success.disabled.focus,
.notification_widget.success[disabled].focus,
fieldset[disabled] .notification_widget.success.focus {
  background-color: #5cb85c;
  border-color: #4cae4c;
}
.notification_widget.success .badge {
  color: #5cb85c;
  background-color: #fff;
}
.notification_widget.info {
  color: #fff;
  background-color: #5bc0de;
  border-color: #46b8da;
}
.notification_widget.info:focus,
.notification_widget.info.focus {
  color: #fff;
  background-color: #31b0d5;
  border-color: #1b6d85;
}
.notification_widget.info:hover {
  color: #fff;
  background-color: #31b0d5;
  border-color: #269abc;
}
.notification_widget.info:active,
.notification_widget.info.active,
.open > .dropdown-toggle.notification_widget.info {
  color: #fff;
  background-color: #31b0d5;
  border-color: #269abc;
}
.notification_widget.info:active:hover,
.notification_widget.info.active:hover,
.open > .dropdown-toggle.notification_widget.info:hover,
.notification_widget.info:active:focus,
.notification_widget.info.active:focus,
.open > .dropdown-toggle.notification_widget.info:focus,
.notification_widget.info:active.focus,
.notification_widget.info.active.focus,
.open > .dropdown-toggle.notification_widget.info.focus {
  color: #fff;
  background-color: #269abc;
  border-color: #1b6d85;
}
.notification_widget.info:active,
.notification_widget.info.active,
.open > .dropdown-toggle.notification_widget.info {
  background-image: none;
}
.notification_widget.info.disabled:hover,
.notification_widget.info[disabled]:hover,
fieldset[disabled] .notification_widget.info:hover,
.notification_widget.info.disabled:focus,
.notification_widget.info[disabled]:focus,
fieldset[disabled] .notification_widget.info:focus,
.notification_widget.info.disabled.focus,
.notification_widget.info[disabled].focus,
fieldset[disabled] .notification_widget.info.focus {
  background-color: #5bc0de;
  border-color: #46b8da;
}
.notification_widget.info .badge {
  color: #5bc0de;
  background-color: #fff;
}
.notification_widget.danger {
  color: #fff;
  background-color: #d9534f;
  border-color: #d43f3a;
}
.notification_widget.danger:focus,
.notification_widget.danger.focus {
  color: #fff;
  background-color: #c9302c;
  border-color: #761c19;
}
.notification_widget.danger:hover {
  color: #fff;
  background-color: #c9302c;
  border-color: #ac2925;
}
.notification_widget.danger:active,
.notification_widget.danger.active,
.open > .dropdown-toggle.notification_widget.danger {
  color: #fff;
  background-color: #c9302c;
  border-color: #ac2925;
}
.notification_widget.danger:active:hover,
.notification_widget.danger.active:hover,
.open > .dropdown-toggle.notification_widget.danger:hover,
.notification_widget.danger:active:focus,
.notification_widget.danger.active:focus,
.open > .dropdown-toggle.notification_widget.danger:focus,
.notification_widget.danger:active.focus,
.notification_widget.danger.active.focus,
.open > .dropdown-toggle.notification_widget.danger.focus {
  color: #fff;
  background-color: #ac2925;
  border-color: #761c19;
}
.notification_widget.danger:active,
.notification_widget.danger.active,
.open > .dropdown-toggle.notification_widget.danger {
  background-image: none;
}
.notification_widget.danger.disabled:hover,
.notification_widget.danger[disabled]:hover,
fieldset[disabled] .notification_widget.danger:hover,
.notification_widget.danger.disabled:focus,
.notification_widget.danger[disabled]:focus,
fieldset[disabled] .notification_widget.danger:focus,
.notification_widget.danger.disabled.focus,
.notification_widget.danger[disabled].focus,
fieldset[disabled] .notification_widget.danger.focus {
  background-color: #d9534f;
  border-color: #d43f3a;
}
.notification_widget.danger .badge {
  color: #d9534f;
  background-color: #fff;
}
div#pager {
  background-color: #fff;
  font-size: 14px;
  line-height: 20px;
  overflow: hidden;
  display: none;
  position: fixed;
  bottom: 0px;
  width: 100%;
  max-height: 50%;
  padding-top: 8px;
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  /* Display over codemirror */
  z-index: 100;
  /* Hack which prevents jquery ui resizable from changing top. */
  top: auto !important;
}
div#pager pre {
  line-height: 1.21429em;
  color: #000;
  background-color: #f7f7f7;
  padding: 0.4em;
}
div#pager #pager-button-area {
  position: absolute;
  top: 8px;
  right: 20px;
}
div#pager #pager-contents {
  position: relative;
  overflow: auto;
  width: 100%;
  height: 100%;
}
div#pager #pager-contents #pager-container {
  position: relative;
  padding: 15px 0px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
div#pager .ui-resizable-handle {
  top: 0px;
  height: 8px;
  background: #f7f7f7;
  border-top: 1px solid #cfcfcf;
  border-bottom: 1px solid #cfcfcf;
  /* This injects handle bars (a short, wide = symbol) for 
        the resize handle. */
}
div#pager .ui-resizable-handle::after {
  content: '';
  top: 2px;
  left: 50%;
  height: 3px;
  width: 30px;
  margin-left: -15px;
  position: absolute;
  border-top: 1px solid #cfcfcf;
}
.quickhelp {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
  line-height: 1.8em;
}
.shortcut_key {
  display: inline-block;
  width: 20ex;
  text-align: right;
  font-family: monospace;
}
.shortcut_descr {
  display: inline-block;
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
}
span.save_widget {
  margin-top: 6px;
}
span.save_widget span.filename {
  height: 1em;
  line-height: 1em;
  padding: 3px;
  margin-left: 16px;
  border: none;
  font-size: 146.5%;
  border-radius: 2px;
}
span.save_widget span.filename:hover {
  background-color: #e6e6e6;
}
span.checkpoint_status,
span.autosave_status {
  font-size: small;
}
@media (max-width: 767px) {
  span.save_widget {
    font-size: small;
  }
  span.checkpoint_status,
  span.autosave_status {
    display: none;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  span.checkpoint_status {
    display: none;
  }
  span.autosave_status {
    font-size: x-small;
  }
}
.toolbar {
  padding: 0px;
  margin-left: -5px;
  margin-top: 2px;
  margin-bottom: 5px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
.toolbar select,
.toolbar label {
  width: auto;
  vertical-align: middle;
  margin-right: 2px;
  margin-bottom: 0px;
  display: inline;
  font-size: 92%;
  margin-left: 0.3em;
  margin-right: 0.3em;
  padding: 0px;
  padding-top: 3px;
}
.toolbar .btn {
  padding: 2px 8px;
}
.toolbar .btn-group {
  margin-top: 0px;
  margin-left: 5px;
}
#maintoolbar {
  margin-bottom: -3px;
  margin-top: -8px;
  border: 0px;
  min-height: 27px;
  margin-left: 0px;
  padding-top: 11px;
  padding-bottom: 3px;
}
#maintoolbar .navbar-text {
  float: none;
  vertical-align: middle;
  text-align: right;
  margin-left: 5px;
  margin-right: 0px;
  margin-top: 0px;
}
.select-xs {
  height: 24px;
}
.pulse,
.dropdown-menu > li > a.pulse,
li.pulse > a.dropdown-toggle,
li.pulse.open > a.dropdown-toggle {
  background-color: #F37626;
  color: white;
}
/**
 * Primary styles
 *
 * Author: Jupyter Development Team
 */
/** WARNING IF YOU ARE EDITTING THIS FILE, if this is a .css file, It has a lot
 * of chance of beeing generated from the ../less/[samename].less file, you can
 * try to get back the less file by reverting somme commit in history
 **/
/*
 * We'll try to get something pretty, so we
 * have some strange css to have the scroll bar on
 * the left with fix button on the top right of the tooltip
 */
@-moz-keyframes fadeOut {
  from {
    opacity: 1;
  }
  to {
    opacity: 0;
  }
}
@-webkit-keyframes fadeOut {
  from {
    opacity: 1;
  }
  to {
    opacity: 0;
  }
}
@-moz-keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
@-webkit-keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
/*properties of tooltip after "expand"*/
.bigtooltip {
  overflow: auto;
  height: 200px;
  -webkit-transition-property: height;
  -webkit-transition-duration: 500ms;
  -moz-transition-property: height;
  -moz-transition-duration: 500ms;
  transition-property: height;
  transition-duration: 500ms;
}
/*properties of tooltip before "expand"*/
.smalltooltip {
  -webkit-transition-property: height;
  -webkit-transition-duration: 500ms;
  -moz-transition-property: height;
  -moz-transition-duration: 500ms;
  transition-property: height;
  transition-duration: 500ms;
  text-overflow: ellipsis;
  overflow: hidden;
  height: 80px;
}
.tooltipbuttons {
  position: absolute;
  padding-right: 15px;
  top: 0px;
  right: 0px;
}
.tooltiptext {
  /*avoid the button to overlap on some docstring*/
  padding-right: 30px;
}
.ipython_tooltip {
  max-width: 700px;
  /*fade-in animation when inserted*/
  -webkit-animation: fadeOut 400ms;
  -moz-animation: fadeOut 400ms;
  animation: fadeOut 400ms;
  -webkit-animation: fadeIn 400ms;
  -moz-animation: fadeIn 400ms;
  animation: fadeIn 400ms;
  vertical-align: middle;
  background-color: #f7f7f7;
  overflow: visible;
  border: #ababab 1px solid;
  outline: none;
  padding: 3px;
  margin: 0px;
  padding-left: 7px;
  font-family: monospace;
  min-height: 50px;
  -moz-box-shadow: 0px 6px 10px -1px #adadad;
  -webkit-box-shadow: 0px 6px 10px -1px #adadad;
  box-shadow: 0px 6px 10px -1px #adadad;
  border-radius: 2px;
  position: absolute;
  z-index: 1000;
}
.ipython_tooltip a {
  float: right;
}
.ipython_tooltip .tooltiptext pre {
  border: 0;
  border-radius: 0;
  font-size: 100%;
  background-color: #f7f7f7;
}
.pretooltiparrow {
  left: 0px;
  margin: 0px;
  top: -16px;
  width: 40px;
  height: 16px;
  overflow: hidden;
  position: absolute;
}
.pretooltiparrow:before {
  background-color: #f7f7f7;
  border: 1px #ababab solid;
  z-index: 11;
  content: "";
  position: absolute;
  left: 15px;
  top: 10px;
  width: 25px;
  height: 25px;
  -webkit-transform: rotate(45deg);
  -moz-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  -o-transform: rotate(45deg);
}
ul.typeahead-list i {
  margin-left: -10px;
  width: 18px;
}
ul.typeahead-list {
  max-height: 80vh;
  overflow: auto;
}
ul.typeahead-list > li > a {
  /** Firefox bug **/
  /* see https://github.com/jupyter/notebook/issues/559 */
  white-space: normal;
}
.cmd-palette .modal-body {
  padding: 7px;
}
.cmd-palette form {
  background: white;
}
.cmd-palette input {
  outline: none;
}
.no-shortcut {
  display: none;
}
.command-shortcut:before {
  content: "(command)";
  padding-right: 3px;
  color: #777777;
}
.edit-shortcut:before {
  content: "(edit)";
  padding-right: 3px;
  color: #777777;
}
#find-and-replace #replace-preview .match,
#find-and-replace #replace-preview .insert {
  background-color: #BBDEFB;
  border-color: #90CAF9;
  border-style: solid;
  border-width: 1px;
  border-radius: 0px;
}
#find-and-replace #replace-preview .replace .match {
  background-color: #FFCDD2;
  border-color: #EF9A9A;
  border-radius: 0px;
}
#find-and-replace #replace-preview .replace .insert {
  background-color: #C8E6C9;
  border-color: #A5D6A7;
  border-radius: 0px;
}
#find-and-replace #replace-preview {
  max-height: 60vh;
  overflow: auto;
}
#find-and-replace #replace-preview pre {
  padding: 5px 10px;
}
.terminal-app {
  background: #EEE;
}
.terminal-app #header {
  background: #fff;
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
}
.terminal-app .terminal {
  float: left;
  font-family: monospace;
  color: white;
  background: black;
  padding: 0.4em;
  border-radius: 2px;
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.4);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.4);
}
.terminal-app .terminal,
.terminal-app .terminal dummy-screen {
  line-height: 1em;
  font-size: 14px;
}
.terminal-app .terminal-cursor {
  color: black;
  background: white;
}
.terminal-app #terminado-container {
  margin-top: 20px;
}
/*# sourceMappingURL=style.min.css.map */
    </style>
<style type="text/css">
    .highlight .hll { background-color: #ffffcc }
.highlight  { background: #f8f8f8; }
.highlight .c { color: #408080; font-style: italic } /* Comment */
.highlight .err { border: 1px solid #FF0000 } /* Error */
.highlight .k { color: #008000; font-weight: bold } /* Keyword */
.highlight .o { color: #666666 } /* Operator */
.highlight .n { color: #040404}
.highlight .ch { color: #408080; font-style: italic } /* Comment.Hashbang */
.highlight .cm { color: #408080; font-style: italic } /* Comment.Multiline */
.highlight .cp { color: #BC7A00 } /* Comment.Preproc */
.highlight .cpf { color: #408080; font-style: italic } /* Comment.PreprocFile */
.highlight .c1 { color: #408080; font-style: italic } /* Comment.Single */
.highlight .cs { color: #408080; font-style: italic } /* Comment.Special */
.highlight .gd { color: #A00000 } /* Generic.Deleted */
.highlight .ge { font-style: italic } /* Generic.Emph */
.highlight .gr { color: #FF0000 } /* Generic.Error */
.highlight .gh { color: #000080; font-weight: bold } /* Generic.Heading */
.highlight .gi { color: #00A000 } /* Generic.Inserted */
.highlight .go { color: #888888 } /* Generic.Output */
.highlight .gp { color: #000080; font-weight: bold } /* Generic.Prompt */
.highlight .gs { font-weight: bold } /* Generic.Strong */
.highlight .gu { color: #800080; font-weight: bold } /* Generic.Subheading */
.highlight .gt { color: #0044DD } /* Generic.Traceback */
.highlight .kc { color: #008000; font-weight: bold } /* Keyword.Constant */
.highlight .kd { color: #008000; font-weight: bold } /* Keyword.Declaration */
.highlight .kn { color: #008000; font-weight: bold } /* Keyword.Namespace */
.highlight .kp { color: #008000 } /* Keyword.Pseudo */
.highlight .kr { color: #008000; font-weight: bold } /* Keyword.Reserved */
.highlight .kt { color: #B00040 } /* Keyword.Type */
.highlight .m { color: #666666 } /* Literal.Number */
.highlight .s { color: #BA2121 } /* Literal.String */
.highlight .na { color: #7D9029 } /* Name.Attribute */
.highlight .nb { color: #008000 } /* Name.Builtin */
.highlight .nc { color: #0000FF; font-weight: bold } /* Name.Class */
.highlight .no { color: #880000 } /* Name.Constant */
.highlight .nd { color: #AA22FF } /* Name.Decorator */
.highlight .ni { color: #999999; font-weight: bold } /* Name.Entity */
.highlight .ne { color: #D2413A; font-weight: bold } /* Name.Exception */
.highlight .nf { color: #0000FF } /* Name.Function */
.highlight .nl { color: #A0A000 } /* Name.Label */
.highlight .nn { color: #0000FF; font-weight: bold } /* Name.Namespace */
.highlight .nt { color: #008000; font-weight: bold } /* Name.Tag */
.highlight .nv { color: #19177C } /* Name.Variable */
.highlight .ow { color: #AA22FF; font-weight: bold } /* Operator.Word */
.highlight .w { color: #bbbbbb } /* Text.Whitespace */
.highlight .mb { color: #666666 } /* Literal.Number.Bin */
.highlight .mf { color: #666666 } /* Literal.Number.Float */
.highlight .mh { color: #666666 } /* Literal.Number.Hex */
.highlight .mi { color: #666666 } /* Literal.Number.Integer */
.highlight .mo { color: #666666 } /* Literal.Number.Oct */
.highlight .sb { color: #BA2121 } /* Literal.String.Backtick */
.highlight .sc { color: #BA2121 } /* Literal.String.Char */
.highlight .sd { color: #BA2121; font-style: italic } /* Literal.String.Doc */
.highlight .s2 { color: #BA2121 } /* Literal.String.Double */
.highlight .se { color: #BB6622; font-weight: bold } /* Literal.String.Escape */
.highlight .sh { color: #BA2121 } /* Literal.String.Heredoc */
.highlight .si { color: #BB6688; font-weight: bold } /* Literal.String.Interpol */
.highlight .sx { color: #008000 } /* Literal.String.Other */
.highlight .sr { color: #BB6688 } /* Literal.String.Regex */
.highlight .s1 { color: #BA2121 } /* Literal.String.Single */
.highlight .ss { color: #19177C } /* Literal.String.Symbol */
.highlight .bp { color: #008000 } /* Name.Builtin.Pseudo */
.highlight .vc { color: #19177C } /* Name.Variable.Class */
.highlight .vg { color: #19177C } /* Name.Variable.Global */
.highlight .vi { color: #19177C } /* Name.Variable.Instance */
.highlight .il { color: #666666 } /* Literal.Number.Integer.Long */
    </style>
<style type="text/css">
    
/* Temporary definitions which will become obsolete with Notebook release 5.0 */
.ansi-black-fg { color: #3E424D; }
.ansi-black-bg { background-color: #3E424D; }
.ansi-black-intense-fg { color: #282C36; }
.ansi-black-intense-bg { background-color: #282C36; }
.ansi-red-fg { color: #E75C58; }
.ansi-red-bg { background-color: #E75C58; }
.ansi-red-intense-fg { color: #B22B31; }
.ansi-red-intense-bg { background-color: #B22B31; }
.ansi-green-fg { color: #00A250; }
.ansi-green-bg { background-color: #00A250; }
.ansi-green-intense-fg { color: #007427; }
.ansi-green-intense-bg { background-color: #007427; }
.ansi-yellow-fg { color: #DDB62B; }
.ansi-yellow-bg { background-color: #DDB62B; }
.ansi-yellow-intense-fg { color: #B27D12; }
.ansi-yellow-intense-bg { background-color: #B27D12; }
.ansi-blue-fg { color: #208FFB; }
.ansi-blue-bg { background-color: #208FFB; }
.ansi-blue-intense-fg { color: #0065CA; }
.ansi-blue-intense-bg { background-color: #0065CA; }
.ansi-magenta-fg { color: #D160C4; }
.ansi-magenta-bg { background-color: #D160C4; }
.ansi-magenta-intense-fg { color: #A03196; }
.ansi-magenta-intense-bg { background-color: #A03196; }
.ansi-cyan-fg { color: #60C6C8; }
.ansi-cyan-bg { background-color: #60C6C8; }
.ansi-cyan-intense-fg { color: #258F8F; }
.ansi-cyan-intense-bg { background-color: #258F8F; }
.ansi-white-fg { color: #C5C1B4; }
.ansi-white-bg { background-color: #C5C1B4; }
.ansi-white-intense-fg { color: #A1A6B2; }
.ansi-white-intense-bg { background-color: #A1A6B2; }

.ansi-bold { font-weight: bold; }

    </style>


<style type="text/css">
/* Overrides of notebook CSS for static HTML export */
body {
  overflow: visible;
  padding: 8px;
}

div#notebook {
  overflow: visible;
  border-top: none;
}

@media print {
  div.cell {
    display: block;
    page-break-inside: avoid;
  } 
  div.output_wrapper { 
    display: block;
    page-break-inside: avoid; 
  }
  div.output { 
    display: block;
    page-break-inside: avoid; 
  }
}
</style>

<!-- Custom stylesheet, it must be in the same directory as the html file -->
<link rel="stylesheet" href="custom.css">

<!-- Loading mathjax macro -->
<!-- Load mathjax -->
    <script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS_HTML"></script>
    <!-- MathJax configuration -->
    <script type="text/x-mathjax-config">
    MathJax.Hub.Config({
        tex2jax: {
            inlineMath: [ ['$','$'], ["\\(","\\)"] ],
            displayMath: [ ['$$','$$'], ["\\[","\\]"] ],
            processEscapes: true,
            processEnvironments: true
        },
        // Center justify equations in code and markdown cells. Elsewhere
        // we use CSS to left justify single line equations in code cells.
        displayAlign: 'center',
        "HTML-CSS": {
            styles: {'.MathJax_Display': {"margin": 0}},
            linebreaks: { automatic: true }
        }
    });
    </script>
    <!-- End of mathjax configuration --></head>
<body>
  <div tabindex="-1" id="notebook" class="border-box-sizing">
    <div class="container" id="notebook-container">

<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Caffe-LSTM-Example-on-Sin(t)-Waveform-Prediction">Caffe LSTM Example on Sin(t) Waveform Prediction<a class="anchor-link" href="#Caffe-LSTM-Example-on-Sin(t)-Waveform-Prediction">&#182;</a></h1><h3 id="with-Mini-Batch-Training">with Mini-Batch Training<a class="anchor-link" href="#with-Mini-Batch-Training">&#182;</a></h3><p>I used to create LSTM networks using plain Python/Numpy or using Tensorflow. Recently I started to use <a href="http://caffe.berkeleyvision.org/">Caffe</a>, which is a wonderful framework, but has terrible documents for beginners to pick it up. I tried to create LSTM networks in Caffe and got lots of issues. There are many LSTM examples in Tensorflow, but it is nearly a desert for Caffe LSTM examples. I searched on google, found several Caffe LSTM examples online, but I could not get any of those working. So I spent sometime studying Caffe code and then adapted <a href="https://github.com/sunsided/tensorflow-lstm-sin">Tensorflow Sin(t)</a> example to Caffe.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[1]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span></span><span class="kn">import</span> <span class="nn">numpy</span> <span class="kn">as</span> <span class="nn">np</span>
<span class="kn">import</span> <span class="nn">math</span>
<span class="kn">import</span> <span class="nn">os</span>
<span class="kn">import</span> <span class="nn">caffe</span>
<span class="kn">import</span> <span class="nn">matplotlib</span>
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="kn">as</span> <span class="nn">plt</span>
<span class="o">%</span><span class="k">matplotlib</span> inline

<span class="n">GPU_ID</span> <span class="o">=</span> <span class="mi">0</span>
<span class="n">caffe</span><span class="o">.</span><span class="n">set_mode_gpu</span><span class="p">()</span>
<span class="n">caffe</span><span class="o">.</span><span class="n">set_device</span><span class="p">(</span><span class="n">GPU_ID</span><span class="p">)</span>

<span class="o">%</span><span class="k">load_ext</span> autoreload
<span class="o">%</span><span class="k">autoreload</span> 2
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[2]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Use the sample generator from Tensorflow Sin(t) online</span>
<span class="k">def</span> <span class="nf">generate_sample</span><span class="p">(</span><span class="n">f</span> <span class="o">=</span> <span class="mf">1.0</span><span class="p">,</span> <span class="n">t0</span> <span class="o">=</span> <span class="bp">None</span><span class="p">,</span> <span class="n">batch_size</span> <span class="o">=</span> <span class="mi">1</span><span class="p">,</span> <span class="n">predict</span> <span class="o">=</span> <span class="mi">50</span><span class="p">,</span> <span class="n">samples</span> <span class="o">=</span> <span class="mi">100</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;</span>
<span class="sd">    Generates data samples.</span>

<span class="sd">    :param f: The frequency to use for all time series or None to randomize.</span>
<span class="sd">    :param t0: The time offset to use for all time series or None to randomize.</span>
<span class="sd">    :param batch_size: The number of time series to generate.</span>
<span class="sd">    :param predict: The number of future samples to generate.</span>
<span class="sd">    :param samples: The number of past (and current) samples to generate.</span>
<span class="sd">    :return: Tuple that contains the past times and values as well as the future times and values. In all outputs,</span>
<span class="sd">             each row represents one time series of the batch.</span>
<span class="sd">    &quot;&quot;&quot;</span>
    <span class="n">Fs</span> <span class="o">=</span> <span class="mf">100.0</span>

    <span class="n">T</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">empty</span><span class="p">((</span><span class="n">batch_size</span><span class="p">,</span> <span class="n">samples</span><span class="p">))</span>
    <span class="n">Y</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">empty</span><span class="p">((</span><span class="n">batch_size</span><span class="p">,</span> <span class="n">samples</span><span class="p">))</span>
    <span class="n">FT</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">empty</span><span class="p">((</span><span class="n">batch_size</span><span class="p">,</span> <span class="n">predict</span><span class="p">))</span>
    <span class="n">FY</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">empty</span><span class="p">((</span><span class="n">batch_size</span><span class="p">,</span> <span class="n">predict</span><span class="p">))</span>

    <span class="n">_t0</span> <span class="o">=</span> <span class="n">t0</span>
    <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">batch_size</span><span class="p">):</span>
        <span class="n">t</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">arange</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span> <span class="n">samples</span> <span class="o">+</span> <span class="n">predict</span><span class="p">)</span> <span class="o">/</span> <span class="n">Fs</span>
        <span class="k">if</span> <span class="n">_t0</span> <span class="ow">is</span> <span class="bp">None</span><span class="p">:</span>
            <span class="n">t0</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">rand</span><span class="p">()</span> <span class="o">*</span> <span class="mi">2</span> <span class="o">*</span> <span class="n">np</span><span class="o">.</span><span class="n">pi</span>
        <span class="k">else</span><span class="p">:</span>
            <span class="n">t0</span> <span class="o">=</span> <span class="n">_t0</span> <span class="o">+</span> <span class="n">i</span><span class="o">/</span><span class="nb">float</span><span class="p">(</span><span class="n">batch_size</span><span class="p">)</span>

        <span class="n">freq</span> <span class="o">=</span> <span class="n">f</span>
        <span class="k">if</span> <span class="n">freq</span> <span class="ow">is</span> <span class="bp">None</span><span class="p">:</span>
            <span class="n">freq</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">rand</span><span class="p">()</span> <span class="o">*</span> <span class="mf">3.5</span> <span class="o">+</span> <span class="mf">0.5</span>

        <span class="n">y</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sin</span><span class="p">(</span><span class="mi">2</span> <span class="o">*</span> <span class="n">np</span><span class="o">.</span><span class="n">pi</span> <span class="o">*</span> <span class="n">freq</span> <span class="o">*</span> <span class="p">(</span><span class="n">t</span> <span class="o">+</span> <span class="n">t0</span><span class="p">))</span>

        <span class="n">T</span><span class="p">[</span><span class="n">i</span><span class="p">,</span> <span class="p">:]</span> <span class="o">=</span> <span class="n">t</span><span class="p">[</span><span class="mi">0</span><span class="p">:</span><span class="n">samples</span><span class="p">]</span>
        <span class="n">Y</span><span class="p">[</span><span class="n">i</span><span class="p">,</span> <span class="p">:]</span> <span class="o">=</span> <span class="n">y</span><span class="p">[</span><span class="mi">0</span><span class="p">:</span><span class="n">samples</span><span class="p">]</span>

        <span class="n">FT</span><span class="p">[</span><span class="n">i</span><span class="p">,</span> <span class="p">:]</span> <span class="o">=</span> <span class="n">t</span><span class="p">[</span><span class="n">samples</span><span class="p">:</span><span class="n">samples</span> <span class="o">+</span> <span class="n">predict</span><span class="p">]</span>
        <span class="n">FY</span><span class="p">[</span><span class="n">i</span><span class="p">,</span> <span class="p">:]</span> <span class="o">=</span> <span class="n">y</span><span class="p">[</span><span class="n">samples</span><span class="p">:</span><span class="n">samples</span> <span class="o">+</span> <span class="n">predict</span><span class="p">]</span>

    <span class="k">return</span> <span class="n">T</span><span class="p">,</span> <span class="n">Y</span><span class="p">,</span> <span class="n">FT</span><span class="p">,</span> <span class="n">FY</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[3]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span></span><span class="n">solver</span> <span class="o">=</span> <span class="n">caffe</span><span class="o">.</span><span class="n">AdamSolver</span><span class="p">(</span><span class="s1">&#39;Caffe_TOY_LSTM_batch_solver.prototxt&#39;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[4]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Network Parameters</span>
<span class="n">n_input</span> <span class="o">=</span> <span class="mi">1</span> <span class="c1"># single input stream</span>
<span class="n">n_steps</span> <span class="o">=</span> <span class="mi">100</span> <span class="c1"># timesteps</span>
<span class="n">n_hidden</span> <span class="o">=</span> <span class="mi">150</span> <span class="c1"># hidden units in LSTM</span>
<span class="n">n_outputs</span> <span class="o">=</span> <span class="mi">50</span> <span class="c1"># predictions in future time</span>
<span class="n">batch_size</span> <span class="o">=</span> <span class="mi">20</span> <span class="c1"># batch of data</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[5]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Train network</span>
<span class="n">niter</span> <span class="o">=</span> <span class="mi">2000</span>
<span class="n">disp_step</span> <span class="o">=</span> <span class="mi">200</span>
<span class="n">train_loss</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">zeros</span><span class="p">(</span><span class="n">niter</span><span class="p">)</span>
<span class="n">solver</span><span class="o">.</span><span class="n">net</span><span class="o">.</span><span class="n">params</span><span class="p">[</span><span class="s1">&#39;lstm1&#39;</span><span class="p">][</span><span class="mi">1</span><span class="p">]</span><span class="o">.</span><span class="n">data</span><span class="p">[</span><span class="n">n_hidden</span> <span class="p">:</span> <span class="mi">2</span> <span class="o">*</span> <span class="n">n_hidden</span><span class="p">]</span> <span class="o">=</span> <span class="mi">1</span>
<span class="n">solver</span><span class="o">.</span><span class="n">net</span><span class="o">.</span><span class="n">blobs</span><span class="p">[</span><span class="s1">&#39;clip&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">data</span><span class="p">[</span><span class="o">...</span><span class="p">]</span> <span class="o">=</span> <span class="mi">1</span>
<span class="c1">#solver.net.blobs[&#39;clip&#39;].data[0] = 0</span>
<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">niter</span><span class="p">):</span>
    <span class="n">_</span><span class="p">,</span> <span class="n">batch_x</span><span class="p">,</span> <span class="n">_</span><span class="p">,</span> <span class="n">batch_y</span> <span class="o">=</span> <span class="n">generate_sample</span><span class="p">(</span><span class="n">f</span><span class="o">=</span><span class="bp">None</span><span class="p">,</span>
                                         <span class="n">t0</span><span class="o">=</span><span class="bp">None</span><span class="p">,</span>
                                         <span class="n">batch_size</span><span class="o">=</span><span class="n">batch_size</span><span class="p">,</span>
                                         <span class="n">samples</span><span class="o">=</span><span class="n">n_steps</span><span class="p">,</span>
                                         <span class="n">predict</span><span class="o">=</span><span class="n">n_outputs</span><span class="p">)</span>
    <span class="n">batch_x</span> <span class="o">=</span> <span class="n">batch_x</span><span class="o">.</span><span class="n">transpose</span><span class="p">()</span>
    <span class="c1">#batch_y = batch_y.transpose()</span>
    <span class="n">solver</span><span class="o">.</span><span class="n">net</span><span class="o">.</span><span class="n">blobs</span><span class="p">[</span><span class="s1">&#39;label&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">data</span><span class="p">[:,:]</span> <span class="o">=</span> <span class="n">batch_y</span>
    <span class="n">solver</span><span class="o">.</span><span class="n">net</span><span class="o">.</span><span class="n">blobs</span><span class="p">[</span><span class="s1">&#39;data&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">data</span><span class="p">[:,:,</span><span class="mi">0</span><span class="p">]</span>  <span class="o">=</span> <span class="n">batch_x</span>
    <span class="n">solver</span><span class="o">.</span><span class="n">step</span><span class="p">(</span><span class="mi">1</span><span class="p">)</span>
    <span class="n">train_loss</span><span class="p">[</span><span class="n">i</span><span class="p">]</span> <span class="o">=</span> <span class="n">solver</span><span class="o">.</span><span class="n">net</span><span class="o">.</span><span class="n">blobs</span><span class="p">[</span><span class="s1">&#39;loss&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">data</span>
    <span class="k">if</span> <span class="n">i</span> <span class="o">%</span> <span class="n">disp_step</span> <span class="o">==</span> <span class="mi">0</span><span class="p">:</span>
        <span class="k">print</span> <span class="s2">&quot;step &quot;</span><span class="p">,</span> <span class="n">i</span><span class="p">,</span> <span class="s2">&quot;, loss = &quot;</span><span class="p">,</span> <span class="n">train_loss</span><span class="p">[</span><span class="n">i</span><span class="p">]</span>
<span class="k">print</span> <span class="s2">&quot;Finished training, iteration reached&quot;</span><span class="p">,</span> <span class="n">niter</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>step  0 , loss =  41.7146110535
step  200 , loss =  9.77667808533
step  400 , loss =  7.38890314102
step  600 , loss =  4.39145421982
step  800 , loss =  1.36509764194
step  1000 , loss =  0.663882374763
step  1200 , loss =  0.351818472147
step  1400 , loss =  0.291823685169
step  1600 , loss =  0.251198112965
step  1800 , loss =  0.189343497157
Finished training, iteration reached 2000
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[6]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># plot loss value during training</span>
<span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">arange</span><span class="p">(</span><span class="n">niter</span><span class="p">),</span> <span class="n">train_loss</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[6]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>[&lt;matplotlib.lines.Line2D at 0x7f85acce8590&gt;]</pre>
</div>

</div>

<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
hLWGshYRkbbUlIaQ3yA8aqgmtFO4AagBfgHg7tcBNwO3EXpNbAwc5u51LVHgJIhqADLHYvj618P6
a19rXt4TJmS/Hj8+zJ0BYQwISE+otWpV884lIiJSiqaM0/Csu3dw9445y48y0lzl7tu4+ybufqi7
lzhc0vrhiCPSjwoOPzysP/kktFm4997C7yulcWXkn/8M81ZAGDYaQkNOERGRttLu555oLUuXwg03
hDktttsOdt897B88GPbbLwzwVMivf136+fbZJ70dBQ3XXQczZpSel4iISFO0VZfLdidqgDhsWBjV
EcI02lHbiI4dw7DRXfIMnt2rV/POHU2idf/9oYtmHG+8AdOmheGqq6vhsMOaVwYREdnwqKahBW29
dXZvhszeD3UZLTqGDk1vjx8fZt9sqjVr4qUbOBBOPBFGjAjdNdetg8svTzeqFBERaYyChlb261/D
tddmBxA77BBmpgQ4/nj4zW/i59etW/brebljbzZi1qywfukluPrq8IijkBtugHHjSstfRETaLz2e
aGWXXZbe7tw51AyYhV/6ELZLGWuhTx947738x37xC7jySvjiC+jZM3+a6LzLlzd+rosuCuuePcNj
jY4d45dTRETaH9U0tKGodgFCDUTv1Gwc0bgPcXzlK4WPXXVVmDGzV68wWFUUXDz7bDpNFDQsXRrW
cXpyHHYYjB0bv4wiItI+KWhoQ1OmhCGoIbQviKbKjoaLzpwc67TT8ufRWIAxYkRYT58OF14Id98d
AolINNZDFDTErT347LN46UREpP1S0NCG+vQJYzvk8+mn8Mc/pl9fe23+dNFYDYV88UV6+9FHw9DT
mVN8R48lfvzjsH7ggdDrQ0REpDEKGhKiT5/s7plbbRWGib755vD61lvDCJDLlrXsed9+O97kWxqy
WkREFDQk3Nlnw0MPwVlnhYmzTjgh7D/22ND74Zlnmn+O6FFFMcWCBo1MKSKyYVDviQQaODC93aFD
dk3ALbeEabqjtg1RG4XmmD491GJstFHp733mGTjggJBHS03aJSIiyaSahoSZObN47UHHjtmNIZsy
j0U+u+8Os2cXT/POO2FgqswBpSZODOvMrqXFfPgh/PSnetwhIrI+UtCQMDvsAJtv3vbnnTULbr+9
8PH6evjVr8JkXJnBRdTwMnd2zkLOOCPUlrR02wwREWl9Chrk36JxIwDeeiv72LvvprtnrlsXltWr
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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[7]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Test the prediction with trained net</span>
<span class="n">n_tests</span> <span class="o">=</span> <span class="mi">3</span>
<span class="n">solver</span><span class="o">.</span><span class="n">test_nets</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span><span class="o">.</span><span class="n">blobs</span><span class="p">[</span><span class="s1">&#39;data&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">reshape</span><span class="p">(</span><span class="n">n_steps</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">1</span><span class="p">)</span>
<span class="n">solver</span><span class="o">.</span><span class="n">test_nets</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span><span class="o">.</span><span class="n">blobs</span><span class="p">[</span><span class="s1">&#39;clip&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">reshape</span><span class="p">(</span><span class="n">n_steps</span><span class="p">,</span> <span class="mi">1</span><span class="p">)</span>
<span class="n">solver</span><span class="o">.</span><span class="n">test_nets</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span><span class="o">.</span><span class="n">reshape</span><span class="p">()</span>

<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span> <span class="n">n_tests</span> <span class="o">+</span> <span class="mi">1</span><span class="p">):</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">subplot</span><span class="p">(</span><span class="n">n_tests</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="n">i</span><span class="p">)</span>
    <span class="n">t</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="n">next_t</span><span class="p">,</span> <span class="n">expected_y</span> <span class="o">=</span> <span class="n">generate_sample</span><span class="p">(</span><span class="n">f</span><span class="o">=</span><span class="n">i</span><span class="p">,</span> <span class="n">t0</span><span class="o">=</span><span class="bp">None</span><span class="p">,</span> <span class="n">samples</span><span class="o">=</span><span class="n">n_steps</span><span class="p">,</span> <span class="n">predict</span><span class="o">=</span><span class="n">n_outputs</span><span class="p">)</span>
    <span class="n">test_input</span> <span class="o">=</span> <span class="n">y</span><span class="o">.</span><span class="n">transpose</span><span class="p">()</span>
    <span class="n">expected_y</span> <span class="o">=</span> <span class="n">expected_y</span><span class="o">.</span><span class="n">reshape</span><span class="p">(</span><span class="n">n_outputs</span><span class="p">)</span>
    <span class="n">solver</span><span class="o">.</span><span class="n">test_nets</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span><span class="o">.</span><span class="n">blobs</span><span class="p">[</span><span class="s1">&#39;clip&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">data</span><span class="p">[</span><span class="o">...</span><span class="p">]</span> <span class="o">=</span> <span class="mi">1</span>
    <span class="n">solver</span><span class="o">.</span><span class="n">test_nets</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span><span class="o">.</span><span class="n">blobs</span><span class="p">[</span><span class="s1">&#39;data&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">data</span><span class="p">[:,:,</span><span class="mi">0</span><span class="p">]</span>  <span class="o">=</span> <span class="n">test_input</span>
    <span class="n">solver</span><span class="o">.</span><span class="n">test_nets</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span><span class="o">.</span><span class="n">forward</span><span class="p">()</span>
    <span class="n">prediction</span> <span class="o">=</span> <span class="n">solver</span><span class="o">.</span><span class="n">test_nets</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span><span class="o">.</span><span class="n">blobs</span><span class="p">[</span><span class="s1">&#39;ip1&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">data</span>

    <span class="c1"># remove the batch size dimensions</span>
    <span class="n">t</span> <span class="o">=</span> <span class="n">t</span><span class="o">.</span><span class="n">squeeze</span><span class="p">()</span>
    <span class="n">y</span> <span class="o">=</span> <span class="n">y</span><span class="o">.</span><span class="n">squeeze</span><span class="p">()</span>
    <span class="n">next_t</span> <span class="o">=</span> <span class="n">next_t</span><span class="o">.</span><span class="n">squeeze</span><span class="p">()</span>
    <span class="n">prediction</span> <span class="o">=</span> <span class="n">prediction</span><span class="o">.</span><span class="n">squeeze</span><span class="p">()</span>
        
    <span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">t</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="n">color</span><span class="o">=</span><span class="s1">&#39;black&#39;</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">t</span><span class="p">[</span><span class="o">-</span><span class="mi">1</span><span class="p">],</span> <span class="n">next_t</span><span class="p">),</span> <span class="n">np</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">y</span><span class="p">[</span><span class="o">-</span><span class="mi">1</span><span class="p">],</span> <span class="n">expected_y</span><span class="p">),</span> <span class="n">color</span><span class="o">=</span><span class="s1">&#39;green&#39;</span><span class="p">,</span> <span class="n">linestyle</span><span class="o">=</span><span class="s2">&quot;:&quot;</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">t</span><span class="p">[</span><span class="o">-</span><span class="mi">1</span><span class="p">],</span> <span class="n">next_t</span><span class="p">),</span> <span class="n">np</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">y</span><span class="p">[</span><span class="o">-</span><span class="mi">1</span><span class="p">],</span> <span class="n">prediction</span><span class="p">),</span> <span class="n">color</span><span class="o">=</span><span class="s1">&#39;red&#39;</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">ylim</span><span class="p">([</span><span class="o">-</span><span class="mi">1</span><span class="p">,</span> <span class="mi">1</span><span class="p">])</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;time [t]&#39;</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;signal&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
2c+muAgQaQAAAABJRU5ErkJggg==
"
>
</div>

</div>

</div>
</div>

</div>
    </div>
  </div>
</body>
</html>
