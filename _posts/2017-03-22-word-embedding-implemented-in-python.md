---
layout: post
title: "Word Embedding Implemented in Python"
description: ""
category: 
tags: 
 - Deep Learning
 - Word Embedding
 - Word Vector
 - NLP
 - Continuous Bag of Words
 - Skipgram
 - Negative Sampling
---
{% include JB/setup %}
<html>
<head><meta charset="utf-8" />
<title>WordEmbedding_Python</title>

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
.highlight .n { color: #040404} 
.highlight .o { color: #666666 } /* Operator */
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
<h1 id="Word-Embedding-Training-in-Python">Word Embedding Training in Python<a class="anchor-link" href="#Word-Embedding-Training-in-Python">&#182;</a></h1><p>Backpropagation gradient calculation should be straightforward once you did any Affine (fully connected) neural network, or Convolution Neural Network (CNN) and Softmax classifier. One example showing the gradient calculation and backpropagation can be found <a href="http://www.xiaoliangbai.com/2016/11/28/softmax-classifier-in-neural-network">here</a>.</p>
<h4 id="&quot;You-shall-know-a-word-by-the-company-it-keeps&quot;---John-Rupert-Firth">"You shall know a word by the company it keeps" - <a href="https://en.wikipedia.org/wiki/John_Rupert_Firth">John Rupert Firth</a><a class="anchor-link" href="#&quot;You-shall-know-a-word-by-the-company-it-keeps&quot;---John-Rupert-Firth">&#182;</a></h4><p>Word Embedding has become very popular since Thomas Mikolov's Word2vec <a href="https://arxiv.org/pdf/1301.3781.pdf">paper</a> was published. We are going to compress words from high-dimension, sparse space (vocabulary) to lower-dimension, continous vector space. It is pretty amazing to see certain linguistic, semantic relations can be encoded and linear transformation can be applied. For example, vector('Rome') is close to vec('Paris') - vec('France') + vec('Italy').</p>
<p>Continuous Bag of Words (CBOW) and Skipgram are two models commonly used to extract this relation into vectors. Comparing with other optimization problems, Word Embedding training has one difficulity - the size of vocabulary is too big to process efficiently, and evaluation is needed for each step. To get around the expensive evaluation of classifier cost (such as applying Softmax prediction + Cross-Entropy loss) scores on the complete vocabulary, negative sampling method can be used to approximate probabilities from Softmax classifier.</p>
<p>This project documents some naive implementations on Word Embedding training. Many functions should be fine-tuned in order to build an efficient deep learning framework</p>
<p>Part of the dataset processing code is adapted based on TensorFlow <a href="https://www.tensorflow.org/code/tensorflow/examples/tutorials/word2vec/word2vec_basic.py">tutorial</a> on word2vec</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[1]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span></span><span class="kn">import</span> <span class="nn">numpy</span> <span class="kn">as</span> <span class="nn">np</span>
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="kn">as</span> <span class="nn">plt</span>
<span class="kn">import</span> <span class="nn">tensorflow</span> <span class="kn">as</span> <span class="nn">tf</span>
<span class="kn">import</span> <span class="nn">scipy.io</span>
<span class="kn">import</span> <span class="nn">scipy.misc</span>
<span class="kn">import</span> <span class="nn">time</span>
<span class="kn">import</span> <span class="nn">sys</span>
<span class="kn">import</span> <span class="nn">os</span>
<span class="kn">import</span> <span class="nn">glob</span>
<span class="kn">import</span> <span class="nn">random</span>
<span class="kn">from</span> <span class="nn">random</span> <span class="kn">import</span> <span class="n">randrange</span>
<span class="kn">import</span> <span class="nn">zipfile</span>
<span class="kn">import</span> <span class="nn">collections</span>
<span class="kn">import</span> <span class="nn">cPickle</span> <span class="kn">as</span> <span class="nn">pickle</span>

<span class="kn">from</span> <span class="nn">sklearn.manifold</span> <span class="kn">import</span> <span class="n">TSNE</span>
<span class="kn">from</span> <span class="nn">six.moves</span> <span class="kn">import</span> <span class="n">urllib</span>
<span class="kn">from</span> <span class="nn">six.moves</span> <span class="kn">import</span> <span class="nb">xrange</span> <span class="c1"># pylint: diable=redefined-builtin</span>


<span class="c1"># Setup Matplotlib and autoreload</span>
<span class="o">%</span><span class="k">matplotlib</span> inline
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
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Because we are not using any existing flow/package, we need to define all building blocks in Python</span>
<span class="c1"># </span>
<span class="k">def</span> <span class="nf">normalize_vecs</span><span class="p">(</span><span class="n">x</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot; Row normalization function </span>
<span class="sd">    </span>
<span class="sd">    Normalize each row of input matrix</span>
<span class="sd">    </span>
<span class="sd">    - Inputs:</span>
<span class="sd">        x: vectors (matrix)</span>
<span class="sd">    - Outputs:</span>
<span class="sd">        x: normalized vectors (matrix)</span>
<span class="sd">    &quot;&quot;&quot;</span>
    <span class="n">xl_vec</span> <span class="o">=</span>  <span class="n">np</span><span class="o">.</span><span class="n">sqrt</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">(</span><span class="n">x</span><span class="o">**</span><span class="mi">2</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">,</span> <span class="n">keepdims</span><span class="o">=</span><span class="bp">True</span><span class="p">))</span>
    <span class="n">x</span> <span class="o">=</span> <span class="n">x</span><span class="o">/</span><span class="n">xl_vec</span>
    
    <span class="k">return</span> <span class="n">x</span>

<span class="c1"># Sigmoid logistic function</span>
<span class="k">def</span> <span class="nf">logistic</span><span class="p">(</span><span class="n">x</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;</span>
<span class="sd">    Apply logistic function to input vector</span>
<span class="sd">    </span>
<span class="sd">    Inputs:</span>
<span class="sd">         - vector x with shape (N, D)</span>
<span class="sd">    Outputs:</span>
<span class="sd">         - out    # Output vector of shape (N, D)</span>
<span class="sd">         - dx     # gradient with regarding to x, shape (N, D)</span>
<span class="sd">    &quot;&quot;&quot;</span>
    <span class="n">out</span> <span class="o">=</span> <span class="mi">1</span><span class="o">/</span> <span class="p">(</span><span class="mi">1</span> <span class="o">+</span> <span class="n">np</span><span class="o">.</span><span class="n">exp</span><span class="p">(</span><span class="o">-</span><span class="n">x</span><span class="p">))</span>
    <span class="n">dx</span> <span class="o">=</span> <span class="n">out</span> <span class="o">*</span> <span class="p">(</span><span class="mi">1</span> <span class="o">-</span> <span class="n">out</span><span class="p">)</span>
    
    <span class="k">return</span> <span class="n">out</span><span class="p">,</span> <span class="n">dx</span>

<span class="c1"># Softmax function</span>
<span class="k">def</span> <span class="nf">softmax</span><span class="p">(</span><span class="n">x</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;</span>
<span class="sd">    Calculate softmax based probability for given input vector</span>
<span class="sd">    &quot;&quot;&quot;</span>
    <span class="n">x</span> <span class="o">-=</span> <span class="n">np</span><span class="o">.</span><span class="n">max</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="n">x</span><span class="o">.</span><span class="n">ndim</span><span class="o">-</span><span class="mi">1</span><span class="p">,</span> <span class="n">keepdims</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span>   <span class="c1"># Numerically safe operation</span>
    <span class="n">exp_x</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">exp</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>
    <span class="n">p</span> <span class="o">=</span> <span class="n">exp_x</span> <span class="o">/</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">(</span><span class="n">exp_x</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="n">x</span><span class="o">.</span><span class="n">ndim</span><span class="o">-</span><span class="mi">1</span><span class="p">,</span> <span class="n">keepdims</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span>
    
    <span class="k">return</span> <span class="n">p</span>

<span class="c1"># Softmax cost layer</span>
<span class="k">def</span> <span class="nf">softmax_cost</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">w</span><span class="p">,</span> <span class="n">target_idx</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;</span>
<span class="sd">    Calculate softmax cost and gradient</span>
<span class="sd">    No bias in this implmentation</span>
<span class="sd">    </span>
<span class="sd">    Inputs</span>
<span class="sd">        - x            # vector from previous layer, such as hidden layer</span>
<span class="sd">        - w            # weight for last layer, so called &quot;output vectors&quot;</span>
<span class="sd">        - target_idx   # Target word index, ground truth</span>
<span class="sd">    </span>
<span class="sd">    Outputs</span>
<span class="sd">        - cost         # Softmax + cross-entropy cost for current predications</span>
<span class="sd">        - dw           # Gradient with regarding to weights</span>
<span class="sd">        - dx           # Gradient with regarding to input vector</span>
<span class="sd">    &quot;&quot;&quot;</span>
    <span class="n">V</span><span class="p">,</span> <span class="n">D</span> <span class="o">=</span> <span class="n">w</span><span class="o">.</span><span class="n">shape</span>   <span class="c1"># V: vocabulary size, D: Vector dimension</span>
    <span class="n">x</span> <span class="o">=</span> <span class="n">x</span><span class="o">.</span><span class="n">reshape</span><span class="p">((</span><span class="mi">1</span><span class="p">,</span> <span class="n">D</span><span class="p">))</span>
    <span class="c1"># x.shape is (1, D)</span>
    <span class="n">prob</span> <span class="o">=</span> <span class="n">softmax</span><span class="p">(</span><span class="n">x</span><span class="o">.</span><span class="n">dot</span><span class="p">(</span><span class="n">w</span><span class="o">.</span><span class="n">T</span><span class="p">))</span>    <span class="c1"># (1, V)</span>
    <span class="n">cost</span> <span class="o">=</span> <span class="o">-</span><span class="n">np</span><span class="o">.</span><span class="n">log</span><span class="p">(</span><span class="n">prob</span><span class="p">[</span><span class="mi">0</span><span class="p">,</span> <span class="n">target_idx</span><span class="p">])</span>  <span class="c1"># Cross-entropy loss, Grand truth distribution is one hot</span>
    <span class="n">dcost</span> <span class="o">=</span> <span class="n">prob</span>                  <span class="c1"># (1, V)</span>
    <span class="n">dcost</span><span class="p">[</span><span class="mi">0</span><span class="p">,</span> <span class="n">target_idx</span><span class="p">]</span> <span class="o">-=</span> <span class="mi">1</span>
    <span class="n">dw</span> <span class="o">=</span> <span class="n">dcost</span><span class="o">.</span><span class="n">T</span><span class="o">.</span><span class="n">dot</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>           <span class="c1"># (V,1) * (1, D) ==&gt; (V, D)</span>
    <span class="n">dx</span> <span class="o">=</span> <span class="n">dcost</span><span class="o">.</span><span class="n">dot</span><span class="p">(</span><span class="n">w</span><span class="p">)</span>             <span class="c1"># (1,V) * (V, D) ==&gt; (1, D)</span>
    
    <span class="k">return</span> <span class="n">cost</span><span class="p">,</span> <span class="n">dw</span><span class="p">,</span> <span class="n">dx</span><span class="o">.</span><span class="n">flatten</span><span class="p">()</span>

<span class="c1"># Naive negative sample generator to randomly pick negative samples</span>
<span class="c1"># Paper recommend to use probability^(3/4), here we just use uniform distribution</span>
<span class="k">def</span> <span class="nf">get_random_samples</span><span class="p">(</span><span class="n">target_idx</span><span class="p">,</span> <span class="n">data_size</span><span class="p">,</span> <span class="n">sample_size</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;</span>
<span class="sd">    Randomly pick sample_size of samples for negative sampling</span>
<span class="sd">    &quot;&quot;&quot;</span>
    <span class="n">indices</span> <span class="o">=</span> <span class="p">[</span><span class="bp">None</span><span class="p">]</span> <span class="o">*</span> <span class="n">sample_size</span>
    <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">xrange</span><span class="p">(</span><span class="n">sample_size</span><span class="p">):</span>
        <span class="n">new_idx</span> <span class="o">=</span> <span class="n">random</span><span class="o">.</span><span class="n">randint</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span> <span class="n">data_size</span> <span class="o">-</span> <span class="mi">1</span><span class="p">)</span>
        <span class="k">while</span> <span class="n">new_idx</span> <span class="o">==</span> <span class="n">target_idx</span><span class="p">:</span>
            <span class="n">new_idx</span> <span class="o">=</span> <span class="n">random</span><span class="o">.</span><span class="n">randint</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span> <span class="n">data_size</span> <span class="o">-</span> <span class="mi">1</span><span class="p">)</span>
        <span class="n">indices</span><span class="p">[</span><span class="n">i</span><span class="p">]</span> <span class="o">=</span> <span class="n">new_idx</span>
    <span class="k">return</span> <span class="n">indices</span>
        

<span class="c1"># Negative sampling cost layer</span>
<span class="k">def</span> <span class="nf">negative_sampling_cost</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">w</span><span class="p">,</span> <span class="n">target_idx</span><span class="p">,</span> <span class="n">sample_size</span><span class="o">=</span><span class="mi">10</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;</span>
<span class="sd">    Purpose is to replace softmax cost layer to handle large vocabulary size</span>
<span class="sd">    Using randomly picked samples to adjust prediction and provide feedback</span>
<span class="sd">    </span>
<span class="sd">    Inputs</span>
<span class="sd">        - x            # vector from previous layer, such as hidden layer</span>
<span class="sd">        - w            # weight for last layer, so called &quot;output vectors&quot;</span>
<span class="sd">        - target_idx   # Target word index, ground truth</span>
<span class="sd">        - sample_size  # Size for negative sampling</span>
<span class="sd">    </span>
<span class="sd">    Outputs</span>
<span class="sd">        - cost         # Softmax + cross-entropy cost for current predication</span>
<span class="sd">        - dw           # Gradient with regarding to weights</span>
<span class="sd">        - dx           # Gradient with regarding to input vector</span>
<span class="sd">    </span>
<span class="sd">    &quot;&quot;&quot;</span>
    <span class="n">V</span><span class="p">,</span> <span class="n">D</span> <span class="o">=</span> <span class="n">w</span><span class="o">.</span><span class="n">shape</span>
    <span class="n">dw</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">zeros_like</span><span class="p">(</span><span class="n">w</span><span class="p">)</span>
    <span class="n">dx</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">zeros_like</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>
    <span class="n">indices</span> <span class="o">=</span> <span class="p">[</span><span class="n">target_idx</span><span class="p">]</span>
    <span class="n">indices</span><span class="o">.</span><span class="n">extend</span><span class="p">(</span><span class="n">get_random_samples</span><span class="p">(</span><span class="n">target_idx</span><span class="p">,</span> <span class="n">V</span><span class="p">,</span> <span class="n">sample_size</span><span class="p">))</span>
    <span class="c1">#print &quot;indices = {}&quot;.format(indices)</span>
    <span class="n">labels</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">array</span><span class="p">([</span><span class="mi">1</span><span class="p">]</span> <span class="o">+</span> <span class="p">[</span><span class="o">-</span><span class="mi">1</span> <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">sample_size</span><span class="p">)])</span>   <span class="c1"># (sample_size + 1,)</span>
    <span class="n">wvecs</span> <span class="o">=</span> <span class="n">w</span><span class="p">[</span><span class="n">indices</span><span class="p">]</span>                                           <span class="c1"># (sample_size+1, D)</span>
    <span class="n">z</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">dot</span><span class="p">(</span><span class="n">wvecs</span><span class="p">,</span> <span class="n">x</span><span class="o">.</span><span class="n">T</span><span class="p">)</span>    <span class="c1"># (sample_size + 1, D) dot (D) ==&gt; (sample_size + 1)</span>
    <span class="n">z</span> <span class="o">=</span> <span class="n">z</span> <span class="o">*</span> <span class="n">labels</span>
    <span class="n">scores</span><span class="p">,</span> <span class="n">_</span> <span class="o">=</span> <span class="n">logistic</span><span class="p">(</span><span class="n">z</span><span class="p">)</span> <span class="c1"># (sample_size + 1)</span>
    <span class="n">cost</span> <span class="o">=</span> <span class="o">-</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">log</span><span class="p">(</span><span class="n">scores</span><span class="p">))</span>   <span class="c1"># A scaler </span>
    <span class="c1"># Calculate gradients</span>
    <span class="n">dz</span> <span class="o">=</span> <span class="n">labels</span> <span class="o">*</span> <span class="p">(</span><span class="n">scores</span> <span class="o">-</span><span class="mi">1</span><span class="p">)</span>   <span class="c1"># (sample_size + 1)</span>
    <span class="n">dz</span> <span class="o">=</span> <span class="n">dz</span><span class="o">.</span><span class="n">reshape</span><span class="p">((</span><span class="mi">1</span><span class="p">,</span> <span class="n">sample_size</span> <span class="o">+</span> <span class="mi">1</span><span class="p">))</span>
    <span class="n">dx</span> <span class="o">=</span> <span class="n">dz</span><span class="o">.</span><span class="n">dot</span><span class="p">(</span><span class="n">wvecs</span><span class="p">)</span>    <span class="c1"># (sample_size + 1) dot (sample_size + 1, D) ==&gt; (1, D)</span>
    <span class="n">dwvecs</span> <span class="o">=</span> <span class="n">dz</span><span class="o">.</span><span class="n">T</span><span class="o">.</span><span class="n">dot</span><span class="p">(</span><span class="n">x</span><span class="o">.</span><span class="n">reshape</span><span class="p">((</span><span class="mi">1</span><span class="p">,</span> <span class="n">D</span><span class="p">)))</span>  <span class="c1"># (sample_size + 1, 1) dot (1, D) ==&gt; (sample_size + 1, D)</span>
    
    <span class="c1"># Copy gradient for sample vectors to complete dW array</span>
    <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">sample_size</span> <span class="o">+</span> <span class="mi">1</span><span class="p">):</span>
        <span class="n">dw</span><span class="p">[</span><span class="n">indices</span><span class="p">[</span><span class="n">i</span><span class="p">]]</span> <span class="o">+=</span> <span class="n">dwvecs</span><span class="p">[</span><span class="n">i</span><span class="p">,:]</span>
    
    <span class="k">return</span> <span class="n">cost</span><span class="p">,</span> <span class="n">dw</span><span class="p">,</span> <span class="n">dx</span><span class="o">.</span><span class="n">flatten</span><span class="p">()</span>


<span class="c1"># skipgram function</span>
<span class="k">def</span> <span class="nf">skipgram</span><span class="p">(</span><span class="n">center_word</span><span class="p">,</span> <span class="n">context_size</span><span class="p">,</span> 
             <span class="n">context_words</span><span class="p">,</span> <span class="n">input_vectors</span><span class="p">,</span> <span class="n">output_vectors</span><span class="p">,</span> 
             <span class="n">cost_func</span><span class="o">=</span><span class="n">negative_sampling_cost</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;</span>
<span class="sd">    Skip-Gram model</span>
<span class="sd">     - Inputs:</span>
<span class="sd">        center_word: index of current center word</span>
<span class="sd">        context_size: size of context window</span>
<span class="sd">        context_words: list of word indexs of context words</span>
<span class="sd">        input_vectors: word vectors from input to hidden layer, for lookup</span>
<span class="sd">        output_vectors: word vectors from hidden layer to final cost function</span>
<span class="sd">        cost_func: cost function, such as softmax_cost or negative_sampling_cost</span>
<span class="sd">     - Outputs:</span>
<span class="sd">        cost: evaluated cost value</span>
<span class="sd">        grad_in: gradient with regard to input_vectors</span>
<span class="sd">        grad_out: gradient with regard to output_vectors</span>
<span class="sd">    &quot;&quot;&quot;</span>
    <span class="n">cost</span> <span class="o">=</span> <span class="mi">0</span>
    <span class="n">grad_in</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">zeros_like</span><span class="p">(</span><span class="n">input_vectors</span><span class="p">)</span>
    <span class="n">grad_out</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">zeros_like</span><span class="p">(</span><span class="n">output_vectors</span><span class="p">)</span>
    
    <span class="n">center_word_vec</span> <span class="o">=</span> <span class="n">input_vectors</span><span class="p">[</span><span class="n">center_word</span><span class="p">,</span> <span class="p">:]</span>
    
    <span class="k">for</span> <span class="n">target_word_idx</span> <span class="ow">in</span> <span class="n">context_words</span><span class="p">:</span>
        <span class="n">c_cost</span><span class="p">,</span> <span class="n">c_dw</span><span class="p">,</span> <span class="n">c_dx</span> <span class="o">=</span> <span class="n">cost_func</span><span class="p">(</span><span class="n">center_word_vec</span><span class="p">,</span> <span class="n">output_vectors</span><span class="p">,</span> <span class="n">target_word_idx</span><span class="p">)</span>
        <span class="n">cost</span> <span class="o">+=</span> <span class="n">c_cost</span>
        <span class="n">grad_in</span><span class="p">[</span><span class="n">center_word</span><span class="p">,</span> <span class="p">:]</span> <span class="o">+=</span> <span class="n">c_dx</span>
        <span class="n">grad_out</span> <span class="o">+=</span> <span class="n">c_dw</span>
        
    <span class="k">return</span> <span class="n">cost</span><span class="p">,</span> <span class="n">grad_in</span><span class="p">,</span> <span class="n">grad_out</span>
        
<span class="c1"># continuous bag of words</span>
<span class="k">def</span> <span class="nf">cbow</span><span class="p">(</span><span class="n">center_word</span><span class="p">,</span> <span class="n">context_size</span><span class="p">,</span> 
             <span class="n">context_words</span><span class="p">,</span> <span class="n">input_vectors</span><span class="p">,</span> <span class="n">output_vectors</span><span class="p">,</span> 
             <span class="n">cost_func</span><span class="o">=</span><span class="n">negative_sampling_cost</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;</span>
<span class="sd">    CBOW model</span>
<span class="sd">     - Inputs:</span>
<span class="sd">        center_word: index of current center word</span>
<span class="sd">        context_size: size of context window</span>
<span class="sd">        context_words: list of word indexs of context words</span>
<span class="sd">        input_vectors: word vectors from input to hidden layer, for lookup</span>
<span class="sd">        output_vectors: word vectors from hidden layer to final cost function</span>
<span class="sd">        cost_func: cost function, such as softmax_cost or negative_sampling_cost</span>
<span class="sd">     - Outputs:</span>
<span class="sd">        cost: evaluated cost value</span>
<span class="sd">        grad_in: gradient with regard to input_vectors</span>
<span class="sd">        grad_out: gradient with regard to output_vectors</span>
<span class="sd">        </span>
<span class="sd">    &quot;&quot;&quot;</span>
    <span class="n">cost</span> <span class="o">=</span> <span class="mi">0</span>
    <span class="n">grad_in</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">zeros_like</span><span class="p">(</span><span class="n">input_vectors</span><span class="p">)</span>
    <span class="n">grad_out</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">zeros_like</span><span class="p">(</span><span class="n">output_vectors</span><span class="p">)</span>
    <span class="n">V</span><span class="p">,</span> <span class="n">D</span> <span class="o">=</span> <span class="n">input_vectors</span><span class="o">.</span><span class="n">shape</span>
    
    <span class="n">onehot</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">zeros</span><span class="p">((</span><span class="mi">2</span><span class="o">*</span><span class="n">context_size</span><span class="p">,</span> <span class="n">V</span><span class="p">))</span>
    <span class="n">target_word_idx</span> <span class="o">=</span> <span class="n">center_word</span>
    <span class="c1">#print context_size, context_words</span>
    <span class="k">for</span> <span class="n">i</span><span class="p">,</span> <span class="n">w_idx</span> <span class="ow">in</span> <span class="nb">enumerate</span><span class="p">(</span><span class="n">context_words</span><span class="p">):</span>
        <span class="n">onehot</span><span class="p">[</span><span class="n">i</span><span class="p">,</span> <span class="n">w_idx</span><span class="p">]</span> <span class="o">+=</span> <span class="mi">1</span>
    
    <span class="n">d</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">dot</span><span class="p">(</span><span class="n">onehot</span><span class="p">,</span> <span class="n">input_vectors</span><span class="p">)</span> <span class="c1"># (2C, V) dot (V, D) ==&gt; (2C, D)</span>
    <span class="n">cbow_vec</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">(</span><span class="n">d</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="mi">0</span><span class="p">)</span><span class="o">/</span><span class="p">(</span><span class="mi">2</span> <span class="o">*</span> <span class="n">context_size</span><span class="p">)</span>  <span class="c1"># Average vectors&#39; weight, shape (1, D)</span>
    <span class="n">cost</span><span class="p">,</span> <span class="n">grad_out</span><span class="p">,</span> <span class="n">grad_cbow_vec</span> <span class="o">=</span> <span class="n">cost_func</span><span class="p">(</span><span class="n">cbow_vec</span><span class="p">,</span> <span class="n">output_vectors</span><span class="p">,</span> <span class="n">target_word_idx</span><span class="p">)</span>

    <span class="k">for</span> <span class="n">word</span> <span class="ow">in</span> <span class="n">context_words</span><span class="p">:</span>
        <span class="n">grad_in</span><span class="p">[</span><span class="n">word</span><span class="p">]</span> <span class="o">+=</span> <span class="n">grad_cbow_vec</span><span class="o">/</span><span class="p">(</span><span class="mi">2</span> <span class="o">*</span> <span class="n">context_size</span><span class="p">)</span>
    
        
    <span class="k">return</span> <span class="n">cost</span><span class="p">,</span> <span class="n">grad_in</span><span class="p">,</span> <span class="n">grad_out</span>
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
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Check gradient   </span>
<span class="k">def</span> <span class="nf">gradcheck_naive</span><span class="p">(</span><span class="n">f</span><span class="p">,</span> <span class="n">x</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot; </span>
<span class="sd">    Gradient check for a function f </span>
<span class="sd">    - f should be a function that takes a single argument and outputs the cost and its gradients</span>
<span class="sd">    - x is the point (numpy array) to check the gradient at</span>
<span class="sd">    &quot;&quot;&quot;</span> 

    <span class="n">rndstate</span> <span class="o">=</span> <span class="n">random</span><span class="o">.</span><span class="n">getstate</span><span class="p">()</span>
    <span class="n">random</span><span class="o">.</span><span class="n">setstate</span><span class="p">(</span><span class="n">rndstate</span><span class="p">)</span>  
    <span class="n">fx</span><span class="p">,</span> <span class="n">grad</span> <span class="o">=</span> <span class="n">f</span><span class="p">(</span><span class="n">x</span><span class="p">)</span> <span class="c1"># Evaluate function value at original point</span>
    <span class="n">h</span> <span class="o">=</span> <span class="mf">1e-8</span>

    <span class="c1"># Iterate over all indexes in x</span>
    <span class="n">it</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">nditer</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">flags</span><span class="o">=</span><span class="p">[</span><span class="s1">&#39;multi_index&#39;</span><span class="p">],</span> <span class="n">op_flags</span><span class="o">=</span><span class="p">[</span><span class="s1">&#39;readwrite&#39;</span><span class="p">])</span>
    <span class="k">while</span> <span class="ow">not</span> <span class="n">it</span><span class="o">.</span><span class="n">finished</span><span class="p">:</span>
        <span class="n">ix</span> <span class="o">=</span> <span class="n">it</span><span class="o">.</span><span class="n">multi_index</span>
        <span class="n">org_fx</span> <span class="o">=</span> <span class="n">fx</span>
        <span class="n">org_x</span> <span class="o">=</span> <span class="n">x</span><span class="p">[</span><span class="n">ix</span><span class="p">]</span>
        <span class="n">x</span><span class="p">[</span><span class="n">ix</span><span class="p">]</span> <span class="o">=</span> <span class="n">org_x</span> <span class="o">+</span> <span class="mf">0.5</span><span class="o">*</span><span class="n">h</span>
        <span class="n">random</span><span class="o">.</span><span class="n">setstate</span><span class="p">(</span><span class="n">rndstate</span><span class="p">)</span>
        <span class="n">fx_a</span><span class="p">,</span> <span class="n">_</span> <span class="o">=</span> <span class="n">f</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>
        <span class="n">x</span><span class="p">[</span><span class="n">ix</span><span class="p">]</span> <span class="o">=</span> <span class="n">org_x</span> <span class="o">-</span> <span class="mf">0.5</span><span class="o">*</span><span class="n">h</span>
        <span class="n">random</span><span class="o">.</span><span class="n">setstate</span><span class="p">(</span><span class="n">rndstate</span><span class="p">)</span>
        <span class="n">fx_b</span><span class="p">,</span> <span class="n">_</span> <span class="o">=</span> <span class="n">f</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>
        <span class="n">fx</span> <span class="o">=</span> <span class="n">org_fx</span>
        <span class="n">x</span><span class="p">[</span><span class="n">ix</span><span class="p">]</span> <span class="o">=</span> <span class="n">org_x</span>
        <span class="n">numgrad</span> <span class="o">=</span> <span class="p">(</span><span class="n">fx_a</span> <span class="o">-</span> <span class="n">fx_b</span><span class="p">)</span> <span class="o">/</span> <span class="n">h</span>

        <span class="c1"># Compare gradients</span>
        <span class="n">reldiff</span> <span class="o">=</span> <span class="nb">abs</span><span class="p">(</span><span class="n">numgrad</span> <span class="o">-</span> <span class="n">grad</span><span class="p">[</span><span class="n">ix</span><span class="p">])</span> <span class="o">/</span> <span class="nb">max</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span> <span class="nb">abs</span><span class="p">(</span><span class="n">numgrad</span><span class="p">),</span> <span class="nb">abs</span><span class="p">(</span><span class="n">grad</span><span class="p">[</span><span class="n">ix</span><span class="p">]))</span>
        <span class="k">if</span> <span class="n">reldiff</span> <span class="o">&gt;</span> <span class="mf">1e-5</span><span class="p">:</span>
            <span class="k">print</span> <span class="s2">&quot;Gradient check failed.&quot;</span>
            <span class="k">print</span> <span class="s2">&quot;First gradient error found at index </span><span class="si">%s</span><span class="s2">&quot;</span> <span class="o">%</span> <span class="nb">str</span><span class="p">(</span><span class="n">ix</span><span class="p">)</span>
            <span class="k">print</span> <span class="s2">&quot;Your gradient: </span><span class="si">%f</span><span class="s2"> </span><span class="se">\t</span><span class="s2"> Numerical gradient: </span><span class="si">%f</span><span class="s2">&quot;</span> <span class="o">%</span> <span class="p">(</span><span class="n">grad</span><span class="p">[</span><span class="n">ix</span><span class="p">],</span> <span class="n">numgrad</span><span class="p">)</span>
            <span class="k">return</span>
    
        <span class="n">it</span><span class="o">.</span><span class="n">iternext</span><span class="p">()</span> <span class="c1"># Step </span>
    <span class="k">print</span> <span class="s2">&quot;Gradient check passed!&quot;</span>


    
<span class="k">def</span> <span class="nf">getRandomContext</span><span class="p">(</span><span class="n">context_size</span><span class="p">,</span>
                     <span class="n">dataset</span><span class="p">):</span>
    <span class="n">span</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="n">dataset</span><span class="p">)</span>
    <span class="n">centerword_idx</span> <span class="o">=</span> <span class="n">random</span><span class="o">.</span><span class="n">randint</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span> <span class="n">span</span><span class="o">-</span><span class="mi">1</span><span class="p">)</span>
    <span class="n">context</span> <span class="o">=</span> <span class="n">dataset</span><span class="p">[</span><span class="nb">max</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span> <span class="n">centerword_idx</span> <span class="o">-</span> <span class="n">context_size</span><span class="p">):</span> <span class="n">centerword_idx</span><span class="p">]</span>
    <span class="k">if</span> <span class="n">centerword_idx</span> <span class="o">+</span> <span class="mi">1</span> <span class="o">&lt;</span> <span class="n">span</span><span class="p">:</span>
        <span class="n">context</span> <span class="o">+=</span> <span class="n">dataset</span><span class="p">[</span><span class="n">centerword_idx</span> <span class="o">+</span> <span class="mi">1</span><span class="p">:</span> <span class="nb">min</span><span class="p">(</span><span class="n">span</span><span class="p">,</span> <span class="n">centerword_idx</span> <span class="o">+</span> <span class="n">context_size</span> <span class="o">+</span> <span class="mi">1</span><span class="p">)]</span>
    <span class="c1">#print &quot;centerword = {}, context = {}&quot;.format(dataset[centerword_idx], context)</span>
    <span class="k">return</span> <span class="n">dataset</span><span class="p">[</span><span class="n">centerword_idx</span><span class="p">],</span> <span class="p">[</span><span class="n">dataset</span><span class="p">[</span><span class="n">w</span><span class="p">]</span> <span class="k">for</span> <span class="n">w</span> <span class="ow">in</span> <span class="n">context</span><span class="p">]</span>

<span class="k">def</span> <span class="nf">word2vec_sgd_batch</span><span class="p">(</span><span class="n">model</span><span class="p">,</span> <span class="n">word_vectors</span><span class="p">,</span> <span class="n">dataset</span><span class="p">,</span> <span class="n">context_size</span><span class="p">,</span> <span class="n">word2vec_cost_func</span><span class="o">=</span><span class="n">negative_sampling_cost</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot; Run word2vec stochastic gradient descent for a set (batchsize) of randomly picked data&quot;&quot;&quot;</span>
    <span class="n">batchsize</span> <span class="o">=</span> <span class="mi">50</span>
    <span class="n">cost</span> <span class="o">=</span> <span class="mf">0.0</span>
    <span class="n">grad</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">zeros</span><span class="p">(</span><span class="n">word_vectors</span><span class="o">.</span><span class="n">shape</span><span class="p">)</span>
    <span class="n">N</span> <span class="o">=</span> <span class="n">word_vectors</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span>
    <span class="n">input_vectors</span> <span class="o">=</span> <span class="n">word_vectors</span><span class="p">[:</span><span class="n">N</span><span class="o">/</span><span class="mi">2</span><span class="p">,</span> <span class="p">:]</span>
    <span class="n">output_vectors</span> <span class="o">=</span> <span class="n">word_vectors</span><span class="p">[</span><span class="n">N</span><span class="o">/</span><span class="mi">2</span><span class="p">:,:]</span>
    <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">xrange</span><span class="p">(</span><span class="n">batchsize</span><span class="p">):</span>
        <span class="n">c_size</span> <span class="o">=</span> <span class="n">random</span><span class="o">.</span><span class="n">randint</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span> <span class="n">context_size</span><span class="p">)</span>
        <span class="n">centerword</span><span class="p">,</span> <span class="n">context</span> <span class="o">=</span> <span class="n">getRandomContext</span><span class="p">(</span><span class="n">c_size</span><span class="p">,</span> <span class="n">dataset</span><span class="p">)</span>
        <span class="n">c</span><span class="p">,</span> <span class="n">gin</span><span class="p">,</span> <span class="n">gout</span> <span class="o">=</span> <span class="n">model</span><span class="p">(</span><span class="n">centerword</span><span class="p">,</span> <span class="n">c_size</span><span class="p">,</span> <span class="n">context</span><span class="p">,</span> <span class="n">input_vectors</span><span class="p">,</span> <span class="n">output_vectors</span><span class="p">,</span> <span class="n">word2vec_cost_func</span><span class="p">)</span>
        <span class="n">cost</span> <span class="o">+=</span> <span class="n">c</span><span class="o">/</span> <span class="n">batchsize</span>
        <span class="n">grad</span><span class="p">[:</span><span class="n">N</span><span class="o">/</span><span class="mi">2</span><span class="p">,</span> <span class="p">:]</span> <span class="o">+=</span> <span class="n">gin</span> <span class="o">/</span> <span class="n">batchsize</span>
        <span class="n">grad</span><span class="p">[</span><span class="n">N</span><span class="o">/</span><span class="mi">2</span><span class="p">:,</span> <span class="p">:]</span> <span class="o">+=</span> <span class="n">gout</span> <span class="o">/</span><span class="n">batchsize</span>
        
    <span class="k">return</span> <span class="n">cost</span><span class="p">,</span> <span class="n">grad</span>


<span class="c1">### Check gradient with summy dataset</span>
<span class="c1">#dummy_dataset = [&#39;abacus&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;, &#39;e&#39;]</span>
<span class="n">dummy_dataset</span> <span class="o">=</span> <span class="p">[</span><span class="mi">0</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">3</span><span class="p">,</span> <span class="mi">4</span><span class="p">]</span>
<span class="n">dummy_dict</span> <span class="o">=</span> <span class="nb">dict</span><span class="p">([(</span><span class="s2">&quot;abacus&quot;</span><span class="p">,</span> <span class="mi">0</span><span class="p">),</span> <span class="p">(</span><span class="s2">&quot;b&quot;</span><span class="p">,</span> <span class="mi">1</span><span class="p">),</span> <span class="p">(</span><span class="s2">&quot;c&quot;</span><span class="p">,</span> <span class="mi">2</span><span class="p">),</span> <span class="p">(</span><span class="s2">&quot;d&quot;</span><span class="p">,</span> <span class="mi">3</span><span class="p">),</span> <span class="p">(</span><span class="s2">&quot;e&quot;</span><span class="p">,</span> <span class="mi">4</span><span class="p">)])</span>

<span class="c1"># Fix random seeds for numerical gradient check</span>
<span class="n">random</span><span class="o">.</span><span class="n">seed</span><span class="p">(</span><span class="mi">123456</span><span class="p">)</span>
<span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">seed</span><span class="p">(</span><span class="mi">654321</span><span class="p">)</span>
<span class="n">dummy_vectors</span> <span class="o">=</span> <span class="n">normalize_vecs</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">randn</span><span class="p">(</span><span class="mi">10</span><span class="p">,</span> <span class="mi">3</span><span class="p">))</span>

<span class="c1"># Run Gradient check</span>
<span class="n">gradcheck_naive</span><span class="p">(</span><span class="k">lambda</span> <span class="n">vec</span><span class="p">:</span> <span class="n">word2vec_sgd_batch</span><span class="p">(</span><span class="n">skipgram</span><span class="p">,</span> <span class="n">vec</span><span class="p">,</span> <span class="n">dummy_dataset</span><span class="p">,</span> <span class="mi">5</span><span class="p">),</span> <span class="n">dummy_vectors</span><span class="p">)</span>
<span class="n">gradcheck_naive</span><span class="p">(</span><span class="k">lambda</span> <span class="n">vec</span><span class="p">:</span> <span class="n">word2vec_sgd_batch</span><span class="p">(</span><span class="n">skipgram</span><span class="p">,</span> <span class="n">vec</span><span class="p">,</span> <span class="n">dummy_dataset</span><span class="p">,</span> <span class="mi">5</span><span class="p">,</span> <span class="n">softmax_cost</span><span class="p">),</span> <span class="n">dummy_vectors</span><span class="p">)</span>
<span class="n">gradcheck_naive</span><span class="p">(</span><span class="k">lambda</span> <span class="n">vec</span><span class="p">:</span> <span class="n">word2vec_sgd_batch</span><span class="p">(</span><span class="n">cbow</span><span class="p">,</span> <span class="n">vec</span><span class="p">,</span> <span class="n">dummy_dataset</span><span class="p">,</span> <span class="mi">5</span><span class="p">),</span> <span class="n">dummy_vectors</span><span class="p">)</span>
<span class="n">gradcheck_naive</span><span class="p">(</span><span class="k">lambda</span> <span class="n">vec</span><span class="p">:</span> <span class="n">word2vec_sgd_batch</span><span class="p">(</span><span class="n">cbow</span><span class="p">,</span> <span class="n">vec</span><span class="p">,</span> <span class="n">dummy_dataset</span><span class="p">,</span> <span class="mi">5</span><span class="p">,</span> <span class="n">softmax_cost</span><span class="p">),</span> <span class="n">dummy_vectors</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>Gradient check passed!
Gradient check passed!
Gradient check passed!
Gradient check passed!
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[4]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Time to get some read dataset to play with!</span>
<span class="c1"># We will use &#39;text8&#39; dataset, a text-only version of Wikipedia dataset, trimmed to the first 10^8 bytes</span>

<span class="n">dataset_url</span> <span class="o">=</span> <span class="s1">&#39;http://mattmahoney.net/dc/text8.zip&#39;</span>
<span class="n">expected_bytes</span> <span class="o">=</span> <span class="mi">31344016</span>

<span class="c1"># To Do: add auto retry with delay if network connection error found</span>
<span class="k">def</span> <span class="nf">may_need_download</span><span class="p">(</span><span class="n">url_link</span><span class="p">,</span> <span class="n">dest_directory</span><span class="p">,</span> <span class="n">expected_bytes</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;</span>
<span class="sd">    Download files if not available locally</span>
<span class="sd">    Args:</span>
<span class="sd">         url_link: the target file for downloading</span>
<span class="sd">         dest_directory: local directory to save downloaded file</span>
<span class="sd">         expected_bytes: expected file size, used to make sure downloading is correct</span>
<span class="sd">    Return:</span>
<span class="sd">         filenpath</span>
<span class="sd">         &quot;&quot;&quot;</span>
    <span class="k">if</span> <span class="ow">not</span> <span class="n">os</span><span class="o">.</span><span class="n">path</span><span class="o">.</span><span class="n">exists</span><span class="p">(</span><span class="n">dest_directory</span><span class="p">):</span>
        <span class="n">os</span><span class="o">.</span><span class="n">makedirs</span><span class="p">(</span><span class="n">dest_directory</span><span class="p">)</span>
    <span class="n">filename</span> <span class="o">=</span> <span class="n">url_link</span><span class="o">.</span><span class="n">split</span><span class="p">(</span><span class="s1">&#39;/&#39;</span><span class="p">)[</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span>
    <span class="n">filepath</span> <span class="o">=</span> <span class="n">os</span><span class="o">.</span><span class="n">path</span><span class="o">.</span><span class="n">join</span><span class="p">(</span><span class="n">dest_directory</span><span class="p">,</span> <span class="n">filename</span><span class="p">)</span>
    
    <span class="k">if</span> <span class="ow">not</span> <span class="n">os</span><span class="o">.</span><span class="n">path</span><span class="o">.</span><span class="n">exists</span><span class="p">(</span><span class="n">filepath</span><span class="p">):</span>
        <span class="k">def</span> <span class="nf">_progress</span><span class="p">(</span><span class="n">count</span><span class="p">,</span> <span class="n">block_size</span><span class="p">,</span> <span class="n">total_size</span><span class="p">):</span>
            <span class="n">sys</span><span class="o">.</span><span class="n">stdout</span><span class="o">.</span><span class="n">write</span><span class="p">(</span><span class="s1">&#39;</span><span class="se">\r</span><span class="s1">&gt;&gt;&gt; Downloading </span><span class="si">%s</span><span class="s1"> </span><span class="si">%.1f%%</span><span class="s1">&#39;</span> 
                             <span class="o">%</span><span class="p">(</span><span class="n">filename</span><span class="p">,</span> <span class="nb">float</span><span class="p">(</span><span class="n">count</span> <span class="o">*</span> <span class="n">block_size</span><span class="p">)</span> <span class="o">/</span> <span class="nb">float</span><span class="p">(</span><span class="n">total_size</span><span class="p">)</span> <span class="o">*</span> <span class="mf">100.0</span><span class="p">))</span>
            <span class="n">sys</span><span class="o">.</span><span class="n">stdout</span><span class="o">.</span><span class="n">flush</span><span class="p">()</span>
        <span class="n">filepath</span><span class="p">,</span> <span class="n">_</span> <span class="o">=</span> <span class="n">urllib</span><span class="o">.</span><span class="n">request</span><span class="o">.</span><span class="n">urlretrieve</span><span class="p">(</span><span class="n">url_link</span><span class="p">,</span> <span class="n">filepath</span><span class="p">,</span> <span class="n">_progress</span><span class="p">)</span>
        <span class="k">print</span> <span class="s1">&#39;</span><span class="se">\n</span><span class="s1">&#39;</span>
        
    <span class="n">statinfo</span> <span class="o">=</span> <span class="n">os</span><span class="o">.</span><span class="n">stat</span><span class="p">(</span><span class="n">filepath</span><span class="p">)</span>
    <span class="k">if</span> <span class="n">statinfo</span><span class="o">.</span><span class="n">st_size</span> <span class="o">==</span> <span class="n">expected_bytes</span><span class="p">:</span>
        <span class="k">print</span> <span class="s1">&#39;Successfully downloaded&#39;</span><span class="p">,</span> <span class="n">filename</span><span class="p">,</span> <span class="n">statinfo</span><span class="o">.</span><span class="n">st_size</span><span class="p">,</span> <span class="s1">&#39;bytes.&#39;</span>
    <span class="k">else</span><span class="p">:</span>
        <span class="k">raise</span> <span class="ne">Exception</span><span class="p">(</span><span class="s1">&#39;File &#39;</span> <span class="o">+</span> <span class="n">filepath</span> <span class="o">+</span> <span class="s1">&#39; is damaged. Please try to download it again&#39;</span><span class="p">)</span>
    <span class="k">return</span> <span class="n">filepath</span>

<span class="n">dataset_file</span> <span class="o">=</span> <span class="n">may_need_download</span><span class="p">(</span><span class="n">dataset_url</span><span class="p">,</span> <span class="s1">&#39;dataset&#39;</span><span class="p">,</span> <span class="n">expected_bytes</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>Successfully downloaded text8.zip 31344016 bytes.
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[5]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Read data into a list of strings</span>
<span class="k">def</span> <span class="nf">read_data</span><span class="p">(</span><span class="n">filename</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;</span>
<span class="sd">    Extract the file, it is a huge list of strings</span>
<span class="sd">    &quot;&quot;&quot;</span>
    <span class="k">with</span> <span class="n">zipfile</span><span class="o">.</span><span class="n">ZipFile</span><span class="p">(</span><span class="n">filename</span><span class="p">)</span> <span class="k">as</span> <span class="n">f</span><span class="p">:</span>
        <span class="n">data</span> <span class="o">=</span> <span class="n">f</span><span class="o">.</span><span class="n">read</span><span class="p">(</span><span class="n">f</span><span class="o">.</span><span class="n">namelist</span><span class="p">()[</span><span class="mi">0</span><span class="p">])</span><span class="o">.</span><span class="n">split</span><span class="p">()</span>
    <span class="k">return</span> <span class="n">data</span>

<span class="n">words_list</span> <span class="o">=</span> <span class="n">read_data</span><span class="p">(</span><span class="n">dataset_file</span><span class="p">)</span>
<span class="k">print</span> <span class="s2">&quot;Dataset type </span><span class="si">%s</span><span class="s2">, with </span><span class="si">%d</span><span class="s2"> words&quot;</span> <span class="o">%</span> <span class="p">(</span><span class="nb">type</span><span class="p">(</span><span class="n">words_list</span><span class="p">),</span> <span class="nb">len</span><span class="p">(</span><span class="n">words_list</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>Dataset type &lt;type &#39;list&#39;&gt;, with 17005207 words
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
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Process data</span>
<span class="k">def</span> <span class="nf">build_dataset</span><span class="p">(</span><span class="n">words_list</span><span class="p">,</span> <span class="n">vocabulary_size</span><span class="p">):</span>
    <span class="n">count</span> <span class="o">=</span> <span class="p">[[</span><span class="s1">&#39;UNK&#39;</span><span class="p">,</span> <span class="o">-</span><span class="mi">1</span><span class="p">]]</span>
    <span class="n">count</span><span class="o">.</span><span class="n">extend</span><span class="p">(</span><span class="n">collections</span><span class="o">.</span><span class="n">Counter</span><span class="p">(</span><span class="n">words_list</span><span class="p">)</span><span class="o">.</span><span class="n">most_common</span><span class="p">(</span><span class="n">vocabulary_size</span> <span class="o">-</span> <span class="mi">1</span><span class="p">))</span>
    <span class="n">dictionary</span> <span class="o">=</span> <span class="nb">dict</span><span class="p">()</span>
    <span class="k">for</span> <span class="n">word</span><span class="p">,</span> <span class="n">_</span> <span class="ow">in</span> <span class="n">count</span><span class="p">:</span>
        <span class="n">dictionary</span><span class="p">[</span><span class="n">word</span><span class="p">]</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="n">dictionary</span><span class="p">)</span>
    <span class="n">data</span> <span class="o">=</span> <span class="nb">list</span><span class="p">()</span>
    <span class="n">unk_count</span> <span class="o">=</span> <span class="mi">0</span>
    <span class="k">for</span> <span class="n">word</span> <span class="ow">in</span> <span class="n">words_list</span><span class="p">:</span>
        <span class="k">if</span> <span class="n">word</span> <span class="ow">in</span> <span class="n">dictionary</span><span class="p">:</span>
            <span class="n">index</span> <span class="o">=</span> <span class="n">dictionary</span><span class="p">[</span><span class="n">word</span><span class="p">]</span>
        <span class="k">else</span><span class="p">:</span>
            <span class="n">index</span> <span class="o">=</span> <span class="mi">0</span> <span class="c1"># map to unknown &#39;unk&#39;</span>
            <span class="n">unk_count</span> <span class="o">+=</span> <span class="mi">1</span>
        <span class="n">data</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">index</span><span class="p">)</span>
    <span class="n">count</span><span class="p">[</span><span class="mi">0</span><span class="p">][</span><span class="mi">1</span><span class="p">]</span> <span class="o">=</span> <span class="n">unk_count</span>
    <span class="n">reverse_dictionary</span> <span class="o">=</span> <span class="nb">dict</span><span class="p">(</span><span class="nb">zip</span><span class="p">(</span><span class="n">dictionary</span><span class="o">.</span><span class="n">values</span><span class="p">(),</span> <span class="n">dictionary</span><span class="o">.</span><span class="n">keys</span><span class="p">()))</span>
    <span class="k">return</span> <span class="n">data</span><span class="p">,</span> <span class="n">count</span><span class="p">,</span> <span class="n">dictionary</span><span class="p">,</span> <span class="n">reverse_dictionary</span>

<span class="c1">### Get Vocabulary ready</span>
<span class="n">vocabulary_size</span> <span class="o">=</span> <span class="mi">20000</span>
<span class="n">dataset</span><span class="p">,</span> <span class="n">count</span><span class="p">,</span> <span class="n">dictionary</span><span class="p">,</span> <span class="n">r_dictionary</span> <span class="o">=</span> <span class="n">build_dataset</span><span class="p">(</span><span class="n">words_list</span><span class="p">,</span> <span class="n">vocabulary_size</span><span class="p">)</span>
<span class="k">del</span> <span class="n">words_list</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[7]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Check some samples of the dataset </span>
<span class="k">print</span> <span class="s1">&#39;Most common words:&#39;</span><span class="p">,</span> <span class="n">count</span><span class="p">[:</span><span class="mi">5</span><span class="p">]</span>
<span class="k">print</span> <span class="s1">&#39;Sample data:&#39;</span><span class="p">,</span> <span class="n">dataset</span><span class="p">[:</span><span class="mi">10</span><span class="p">],</span> <span class="p">[</span><span class="n">r_dictionary</span><span class="p">[</span><span class="n">i</span><span class="p">]</span> <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="n">dataset</span><span class="p">[:</span><span class="mi">10</span><span class="p">]]</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>Most common words: [[&#39;UNK&#39;, 996665], (&#39;the&#39;, 1061396), (&#39;of&#39;, 593677), (&#39;and&#39;, 416629), (&#39;one&#39;, 411764)]
Sample data: [5239, 3084, 12, 6, 195, 2, 3137, 46, 59, 156] [&#39;anarchism&#39;, &#39;originated&#39;, &#39;as&#39;, &#39;a&#39;, &#39;term&#39;, &#39;of&#39;, &#39;abuse&#39;, &#39;first&#39;, &#39;used&#39;, &#39;against&#39;]
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[8]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Add parameter saving and restoring capability</span>

<span class="k">def</span> <span class="nf">save_params</span><span class="p">(</span><span class="nb">iter</span><span class="p">,</span> <span class="n">params</span><span class="p">,</span> <span class="n">cost_history</span><span class="p">,</span> <span class="n">target_dir</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot; Function to save paramerters for later to restore. &quot;&quot;&quot;</span>
    <span class="k">if</span> <span class="ow">not</span> <span class="n">os</span><span class="o">.</span><span class="n">path</span><span class="o">.</span><span class="n">exists</span><span class="p">(</span><span class="n">target_dir</span><span class="p">):</span>
        <span class="n">os</span><span class="o">.</span><span class="n">makedirs</span><span class="p">(</span><span class="n">target_dir</span><span class="p">)</span>
        
    <span class="n">filepath</span> <span class="o">=</span> <span class="n">os</span><span class="o">.</span><span class="n">path</span><span class="o">.</span><span class="n">join</span><span class="p">(</span><span class="n">target_dir</span><span class="p">,</span> <span class="s2">&quot;saved_params_</span><span class="si">%d</span><span class="s2">.npy&quot;</span> <span class="o">%</span> <span class="nb">iter</span><span class="p">)</span>    
    <span class="k">with</span> <span class="nb">open</span><span class="p">(</span><span class="n">filepath</span><span class="p">,</span> <span class="s2">&quot;w&quot;</span><span class="p">)</span> <span class="k">as</span> <span class="n">f</span><span class="p">:</span> 
        <span class="n">pickle</span><span class="o">.</span><span class="n">dump</span><span class="p">(</span><span class="n">params</span><span class="p">,</span> <span class="n">f</span><span class="p">)</span>
        <span class="n">pickle</span><span class="o">.</span><span class="n">dump</span><span class="p">(</span><span class="n">cost_history</span><span class="p">,</span> <span class="n">f</span><span class="p">)</span>
        <span class="n">pickle</span><span class="o">.</span><span class="n">dump</span><span class="p">(</span><span class="n">random</span><span class="o">.</span><span class="n">getstate</span><span class="p">(),</span> <span class="n">f</span><span class="p">)</span>
        
<span class="k">def</span> <span class="nf">load_saved_params</span><span class="p">(</span><span class="n">target_dir</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot; Restore saved parameters and set iteration number. &quot;&quot;&quot;</span>
    <span class="n">start_point</span> <span class="o">=</span> <span class="mi">0</span>
    <span class="k">for</span> <span class="n">f</span> <span class="ow">in</span> <span class="n">glob</span><span class="o">.</span><span class="n">glob</span><span class="p">(</span><span class="s2">&quot;{}/saved_params_*.npy&quot;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">target_dir</span><span class="p">)):</span>
        <span class="nb">iter</span> <span class="o">=</span> <span class="nb">int</span><span class="p">(</span><span class="n">os</span><span class="o">.</span><span class="n">path</span><span class="o">.</span><span class="n">splitext</span><span class="p">(</span><span class="n">os</span><span class="o">.</span><span class="n">path</span><span class="o">.</span><span class="n">basename</span><span class="p">(</span><span class="n">f</span><span class="p">))[</span><span class="mi">0</span><span class="p">]</span><span class="o">.</span><span class="n">split</span><span class="p">(</span><span class="s2">&quot;_&quot;</span><span class="p">)[</span><span class="o">-</span><span class="mi">1</span><span class="p">])</span>
        <span class="k">if</span> <span class="nb">iter</span> <span class="o">&gt;</span> <span class="n">start_point</span> <span class="p">:</span>
            <span class="n">start_point</span> <span class="o">=</span> <span class="nb">iter</span>
    <span class="k">if</span> <span class="n">start_point</span> <span class="o">&gt;</span> <span class="mi">0</span><span class="p">:</span>
        <span class="k">with</span> <span class="nb">open</span><span class="p">(</span><span class="s2">&quot;{}/saved_params_{}.npy&quot;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">target_dir</span><span class="p">,</span> <span class="n">start_point</span><span class="p">),</span> <span class="s2">&quot;r&quot;</span><span class="p">)</span> <span class="k">as</span> <span class="n">f</span><span class="p">:</span>
            <span class="n">params</span> <span class="o">=</span> <span class="n">pickle</span><span class="o">.</span><span class="n">load</span><span class="p">(</span><span class="n">f</span><span class="p">)</span>
            <span class="n">cost_history</span> <span class="o">=</span> <span class="n">pickle</span><span class="o">.</span><span class="n">load</span><span class="p">(</span><span class="n">f</span><span class="p">)</span>
            <span class="n">state</span> <span class="o">=</span> <span class="n">pickle</span><span class="o">.</span><span class="n">load</span><span class="p">(</span><span class="n">f</span><span class="p">)</span>
        <span class="k">return</span> <span class="n">start_point</span><span class="p">,</span> <span class="n">params</span><span class="p">,</span> <span class="n">cost_history</span><span class="p">,</span> <span class="n">state</span>
    <span class="k">else</span><span class="p">:</span>
        <span class="k">return</span> <span class="n">start_point</span><span class="p">,</span> <span class="bp">None</span><span class="p">,</span> <span class="p">[],</span> <span class="bp">None</span>
    
    

<span class="k">def</span> <span class="nf">sgd_optimizer</span><span class="p">(</span><span class="n">func</span><span class="p">,</span> <span class="n">x0</span><span class="p">,</span> <span class="n">step</span><span class="p">,</span> <span class="n">iterations</span><span class="p">,</span> 
                  <span class="n">PRINT_EVERY</span><span class="o">=</span><span class="mi">100</span><span class="p">,</span>
                  <span class="n">SAVE_PARAMS_EVERY</span><span class="o">=</span><span class="mi">2000</span><span class="p">,</span>
                  <span class="n">use_saved</span><span class="o">=</span><span class="bp">False</span><span class="p">,</span> 
                  <span class="n">save_dir</span><span class="o">=</span><span class="s1">&#39;saved_params_dir&#39;</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot; </span>
<span class="sd">    Stochastic Gradient Descent Optimizer             </span>
<span class="sd">    </span>
<span class="sd">     Inputs:                                                         </span>
<span class="sd">     - func: the function to optimize, it should take a single        </span>
<span class="sd">         argument and yield two outputs, a cost and the gradient  </span>
<span class="sd">         with respect to the arguments                            </span>
<span class="sd">     - x0: the initial point to start SGD from                     </span>
<span class="sd">     - step: the step size for SGD                                 </span>
<span class="sd">     - iterations: total iterations to run SGD with</span>
<span class="sd">     - save_dir: directory for saving parameters</span>
<span class="sd"> </span>

<span class="sd">     Output:                                                         </span>
<span class="sd">     - x: the parameter value after SGD finishes  </span>
<span class="sd">     - cost_history: the history of cost function value</span>
<span class="sd">    &quot;&quot;&quot;</span>
    
    <span class="c1"># Anneal learning rate every several iterations</span>
    <span class="n">ANNEAL_EVERY</span> <span class="o">=</span> <span class="mi">5000</span>
    <span class="n">x</span> <span class="o">=</span> <span class="n">x0</span>
    <span class="n">start_iter</span> <span class="o">=</span> <span class="mi">0</span>
    <span class="n">cost_history</span> <span class="o">=</span> <span class="p">[]</span>
    <span class="k">if</span> <span class="n">use_saved</span><span class="p">:</span>
        <span class="n">start_iter</span> <span class="p">,</span> <span class="n">old_x</span><span class="p">,</span> <span class="n">cost_history</span><span class="p">,</span> <span class="n">state</span> <span class="o">=</span> <span class="n">load_saved_params</span><span class="p">(</span><span class="n">save_dir</span><span class="p">)</span>
        <span class="k">if</span> <span class="n">start_iter</span> <span class="o">&gt;</span> <span class="mi">0</span><span class="p">:</span>
            <span class="n">x</span> <span class="o">=</span> <span class="n">old_x</span><span class="p">;</span>
            <span class="n">step</span> <span class="o">*=</span> <span class="mf">0.5</span> <span class="o">**</span> <span class="p">(</span><span class="n">start_iter</span> <span class="o">/</span> <span class="n">ANNEAL_EVERY</span><span class="p">)</span>
        <span class="k">if</span> <span class="n">state</span><span class="p">:</span>
            <span class="n">random</span><span class="o">.</span><span class="n">setstate</span><span class="p">(</span><span class="n">state</span><span class="p">)</span>
    <span class="k">else</span><span class="p">:</span>
        <span class="k">pass</span>
    
    
    <span class="n">expcost</span> <span class="o">=</span> <span class="bp">None</span>
    
    
    <span class="k">for</span> <span class="nb">iter</span> <span class="ow">in</span> <span class="nb">xrange</span><span class="p">(</span><span class="n">start_iter</span> <span class="o">+</span> <span class="mi">1</span><span class="p">,</span> <span class="n">iterations</span> <span class="o">+</span> <span class="mi">1</span><span class="p">):</span>
        <span class="n">cost</span> <span class="o">=</span> <span class="bp">None</span>
        <span class="n">cost</span><span class="p">,</span> <span class="n">grad</span> <span class="o">=</span> <span class="n">func</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>
        <span class="n">x</span> <span class="o">-=</span> <span class="n">step</span> <span class="o">*</span> <span class="n">grad</span>
        <span class="n">cost_history</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">cost</span><span class="p">)</span>
        
        <span class="k">if</span> <span class="nb">iter</span> <span class="o">%</span> <span class="n">PRINT_EVERY</span> <span class="o">==</span> <span class="mi">0</span><span class="p">:</span>
            <span class="k">if</span> <span class="ow">not</span> <span class="n">expcost</span><span class="p">:</span>
                <span class="n">expcost</span> <span class="o">=</span> <span class="n">cost</span>
            <span class="k">else</span><span class="p">:</span>
                <span class="n">expcost</span> <span class="o">=</span> <span class="o">.</span><span class="mi">95</span> <span class="o">*</span> <span class="n">expcost</span> <span class="o">+</span> <span class="o">.</span><span class="mo">05</span> <span class="o">*</span> <span class="n">cost</span>
            <span class="k">print</span> <span class="s2">&quot;</span><span class="se">\r</span><span class="s2">&gt;&gt;&gt; iter </span><span class="si">%d</span><span class="s2">: </span><span class="si">%f</span><span class="s2">&quot;</span> <span class="o">%</span> <span class="p">(</span><span class="nb">iter</span><span class="p">,</span> <span class="n">expcost</span><span class="p">)</span>
        
        <span class="k">if</span> <span class="nb">iter</span> <span class="o">%</span> <span class="n">SAVE_PARAMS_EVERY</span> <span class="o">==</span> <span class="mi">0</span> <span class="ow">and</span> <span class="n">use_saved</span><span class="p">:</span>
            <span class="n">save_params</span><span class="p">(</span><span class="nb">iter</span><span class="p">,</span> <span class="n">x</span><span class="p">,</span> <span class="n">cost_history</span><span class="p">,</span> <span class="n">save_dir</span><span class="p">)</span>
            
        <span class="k">if</span> <span class="nb">iter</span> <span class="o">%</span> <span class="n">ANNEAL_EVERY</span> <span class="o">==</span> <span class="mi">0</span><span class="p">:</span>
            <span class="n">step</span> <span class="o">*=</span> <span class="mf">0.5</span>
    <span class="k">print</span> <span class="s2">&quot;</span><span class="se">\n</span><span class="s2">&quot;</span>
    <span class="k">return</span> <span class="n">x</span><span class="p">,</span> <span class="n">cost_history</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[9]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span></span><span class="n">embedding_size</span> <span class="o">=</span> <span class="mi">64</span>
<span class="n">word_vectors</span> <span class="o">=</span> <span class="n">normalize_vecs</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">randn</span><span class="p">(</span><span class="mi">2</span><span class="o">*</span><span class="n">vocabulary_size</span><span class="p">,</span> <span class="n">embedding_size</span><span class="p">))</span>
<span class="n">context_window_size</span> <span class="o">=</span> <span class="mi">1</span>

<span class="n">trained_word_vector</span><span class="p">,</span> <span class="n">cost_history</span> <span class="o">=</span> <span class="n">sgd_optimizer</span><span class="p">(</span><span class="k">lambda</span> <span class="n">vec</span><span class="p">:</span> 
                                        <span class="n">word2vec_sgd_batch</span><span class="p">(</span><span class="n">skipgram</span><span class="p">,</span> 
                                                             <span class="n">vec</span><span class="p">,</span> <span class="n">dataset</span><span class="p">,</span> 
                                                             <span class="n">context_window_size</span><span class="p">),</span>
                                        <span class="n">word_vectors</span><span class="p">,</span> 
                                        <span class="mi">1</span><span class="p">,</span> <span class="mi">30000</span><span class="p">,</span> <span class="n">use_saved</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span>

<span class="c1">#print len(dataset)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>&gt;&gt;&gt; iter 100: 15.142714
&gt;&gt;&gt; iter 200: 15.127362
&gt;&gt;&gt; iter 300: 15.097164
&gt;&gt;&gt; iter 400: 15.010163
&gt;&gt;&gt; iter 500: 14.846600
&gt;&gt;&gt; iter 600: 14.618834
&gt;&gt;&gt; iter 700: 14.298757
&gt;&gt;&gt; iter 800: 14.051741
&gt;&gt;&gt; iter 900: 13.763645
&gt;&gt;&gt; iter 1000: 13.466327
&gt;&gt;&gt; iter 1100: 13.084013
&gt;&gt;&gt; iter 1200: 12.830128
&gt;&gt;&gt; iter 1300: 12.493584
&gt;&gt;&gt; iter 1400: 12.276524
&gt;&gt;&gt; iter 1500: 12.077296
&gt;&gt;&gt; iter 1600: 11.762810
&gt;&gt;&gt; iter 1700: 11.465948
&gt;&gt;&gt; iter 1800: 11.179325
&gt;&gt;&gt; iter 1900: 10.937557
&gt;&gt;&gt; iter 2000: 10.731226
&gt;&gt;&gt; iter 2100: 10.509891
&gt;&gt;&gt; iter 2200: 10.285919
&gt;&gt;&gt; iter 2300: 10.084203
&gt;&gt;&gt; iter 2400: 9.869337
&gt;&gt;&gt; iter 2500: 9.586403
&gt;&gt;&gt; iter 2600: 9.439124
&gt;&gt;&gt; iter 2700: 9.284449
&gt;&gt;&gt; iter 2800: 9.117748
&gt;&gt;&gt; iter 2900: 8.927890
&gt;&gt;&gt; iter 3000: 8.750479
&gt;&gt;&gt; iter 3100: 8.567016
&gt;&gt;&gt; iter 3200: 8.372594
&gt;&gt;&gt; iter 3300: 8.173714
&gt;&gt;&gt; iter 3400: 8.059736
&gt;&gt;&gt; iter 3500: 7.852919
&gt;&gt;&gt; iter 3600: 7.679299
&gt;&gt;&gt; iter 3700: 7.461978
&gt;&gt;&gt; iter 3800: 7.326921
&gt;&gt;&gt; iter 3900: 7.174543
&gt;&gt;&gt; iter 4000: 6.989613
&gt;&gt;&gt; iter 4100: 6.842037
&gt;&gt;&gt; iter 4200: 6.695531
&gt;&gt;&gt; iter 4300: 6.558940
&gt;&gt;&gt; iter 4400: 6.450024
&gt;&gt;&gt; iter 4500: 6.361125
&gt;&gt;&gt; iter 4600: 6.226748
&gt;&gt;&gt; iter 4700: 6.113042
&gt;&gt;&gt; iter 4800: 6.014114
&gt;&gt;&gt; iter 4900: 5.919818
&gt;&gt;&gt; iter 5000: 5.809129
&gt;&gt;&gt; iter 5100: 5.711771
&gt;&gt;&gt; iter 5200: 5.631438
&gt;&gt;&gt; iter 5300: 5.514884
&gt;&gt;&gt; iter 5400: 5.434048
&gt;&gt;&gt; iter 5500: 5.324360
&gt;&gt;&gt; iter 5600: 5.249820
&gt;&gt;&gt; iter 5700: 5.220132
&gt;&gt;&gt; iter 5800: 5.150067
&gt;&gt;&gt; iter 5900: 5.041397
&gt;&gt;&gt; iter 6000: 4.958067
&gt;&gt;&gt; iter 6100: 4.882629
&gt;&gt;&gt; iter 6200: 4.823477
&gt;&gt;&gt; iter 6300: 4.719328
&gt;&gt;&gt; iter 6400: 4.703851
&gt;&gt;&gt; iter 6500: 4.668334
&gt;&gt;&gt; iter 6600: 4.565740
&gt;&gt;&gt; iter 6700: 4.531533
&gt;&gt;&gt; iter 6800: 4.527520
&gt;&gt;&gt; iter 6900: 4.477774
&gt;&gt;&gt; iter 7000: 4.393866
&gt;&gt;&gt; iter 7100: 4.349869
&gt;&gt;&gt; iter 7200: 4.287739
&gt;&gt;&gt; iter 7300: 4.188506
&gt;&gt;&gt; iter 7400: 4.124938
&gt;&gt;&gt; iter 7500: 4.062781
&gt;&gt;&gt; iter 7600: 4.038402
&gt;&gt;&gt; iter 7700: 3.969521
&gt;&gt;&gt; iter 7800: 3.971548
&gt;&gt;&gt; iter 7900: 3.921790
&gt;&gt;&gt; iter 8000: 3.929343
&gt;&gt;&gt; iter 8100: 3.884722
&gt;&gt;&gt; iter 8200: 3.806265
&gt;&gt;&gt; iter 8300: 3.757294
&gt;&gt;&gt; iter 8400: 3.756317
&gt;&gt;&gt; iter 8500: 3.716506
&gt;&gt;&gt; iter 8600: 3.676878
&gt;&gt;&gt; iter 8700: 3.657006
&gt;&gt;&gt; iter 8800: 3.658382
&gt;&gt;&gt; iter 8900: 3.606045
&gt;&gt;&gt; iter 9000: 3.595908
&gt;&gt;&gt; iter 9100: 3.548167
&gt;&gt;&gt; iter 9200: 3.557864
&gt;&gt;&gt; iter 9300: 3.488735
&gt;&gt;&gt; iter 9400: 3.460848
&gt;&gt;&gt; iter 9500: 3.429942
&gt;&gt;&gt; iter 9600: 3.412726
&gt;&gt;&gt; iter 9700: 3.378585
&gt;&gt;&gt; iter 9800: 3.358519
&gt;&gt;&gt; iter 9900: 3.343109
&gt;&gt;&gt; iter 10000: 3.363491
&gt;&gt;&gt; iter 10100: 3.363901
&gt;&gt;&gt; iter 10200: 3.320365
&gt;&gt;&gt; iter 10300: 3.284050
&gt;&gt;&gt; iter 10400: 3.258947
&gt;&gt;&gt; iter 10500: 3.226283
&gt;&gt;&gt; iter 10600: 3.205318
&gt;&gt;&gt; iter 10700: 3.199333
&gt;&gt;&gt; iter 10800: 3.175485
&gt;&gt;&gt; iter 10900: 3.174435
&gt;&gt;&gt; iter 11000: 3.121339
&gt;&gt;&gt; iter 11100: 3.102123
&gt;&gt;&gt; iter 11200: 3.087775
&gt;&gt;&gt; iter 11300: 3.073892
&gt;&gt;&gt; iter 11400: 3.034521
&gt;&gt;&gt; iter 11500: 3.016586
&gt;&gt;&gt; iter 11600: 3.014720
&gt;&gt;&gt; iter 11700: 2.994715
&gt;&gt;&gt; iter 11800: 2.958088
&gt;&gt;&gt; iter 11900: 2.979039
&gt;&gt;&gt; iter 12000: 2.962898
&gt;&gt;&gt; iter 12100: 2.922493
&gt;&gt;&gt; iter 12200: 2.932794
&gt;&gt;&gt; iter 12300: 2.892336
&gt;&gt;&gt; iter 12400: 2.894966
&gt;&gt;&gt; iter 12500: 2.881443
&gt;&gt;&gt; iter 12600: 2.832328
&gt;&gt;&gt; iter 12700: 2.856374
&gt;&gt;&gt; iter 12800: 2.831711
&gt;&gt;&gt; iter 12900: 2.863712
&gt;&gt;&gt; iter 13000: 2.843840
&gt;&gt;&gt; iter 13100: 2.847455
&gt;&gt;&gt; iter 13200: 2.813263
&gt;&gt;&gt; iter 13300: 2.817830
&gt;&gt;&gt; iter 13400: 2.809909
&gt;&gt;&gt; iter 13500: 2.809166
&gt;&gt;&gt; iter 13600: 2.802369
&gt;&gt;&gt; iter 13700: 2.792205
&gt;&gt;&gt; iter 13800: 2.813283
&gt;&gt;&gt; iter 13900: 2.813931
&gt;&gt;&gt; iter 14000: 2.806737
&gt;&gt;&gt; iter 14100: 2.804330
&gt;&gt;&gt; iter 14200: 2.788540
&gt;&gt;&gt; iter 14300: 2.807760
&gt;&gt;&gt; iter 14400: 2.775908
&gt;&gt;&gt; iter 14500: 2.740234
&gt;&gt;&gt; iter 14600: 2.747506
&gt;&gt;&gt; iter 14700: 2.740294
&gt;&gt;&gt; iter 14800: 2.684119
&gt;&gt;&gt; iter 14900: 2.649346
&gt;&gt;&gt; iter 15000: 2.648224
&gt;&gt;&gt; iter 15100: 2.654741
&gt;&gt;&gt; iter 15200: 2.644998
&gt;&gt;&gt; iter 15300: 2.633809
&gt;&gt;&gt; iter 15400: 2.641030
&gt;&gt;&gt; iter 15500: 2.660329
&gt;&gt;&gt; iter 15600: 2.662161
&gt;&gt;&gt; iter 15700: 2.633361
&gt;&gt;&gt; iter 15800: 2.659201
&gt;&gt;&gt; iter 15900: 2.651981
&gt;&gt;&gt; iter 16000: 2.610024
&gt;&gt;&gt; iter 16100: 2.602103
&gt;&gt;&gt; iter 16200: 2.581829
&gt;&gt;&gt; iter 16300: 2.550988
&gt;&gt;&gt; iter 16400: 2.517804
&gt;&gt;&gt; iter 16500: 2.512838
&gt;&gt;&gt; iter 16600: 2.508392
&gt;&gt;&gt; iter 16700: 2.520389
&gt;&gt;&gt; iter 16800: 2.507302
&gt;&gt;&gt; iter 16900: 2.523870
&gt;&gt;&gt; iter 17000: 2.499940
&gt;&gt;&gt; iter 17100: 2.513977
&gt;&gt;&gt; iter 17200: 2.504930
&gt;&gt;&gt; iter 17300: 2.518843
&gt;&gt;&gt; iter 17400: 2.514356
&gt;&gt;&gt; iter 17500: 2.516082
&gt;&gt;&gt; iter 17600: 2.522284
&gt;&gt;&gt; iter 17700: 2.556433
&gt;&gt;&gt; iter 17800: 2.544539
&gt;&gt;&gt; iter 17900: 2.575273
&gt;&gt;&gt; iter 18000: 2.555194
&gt;&gt;&gt; iter 18100: 2.609805
&gt;&gt;&gt; iter 18200: 2.623953
&gt;&gt;&gt; iter 18300: 2.615340
&gt;&gt;&gt; iter 18400: 2.591577
&gt;&gt;&gt; iter 18500: 2.610378
&gt;&gt;&gt; iter 18600: 2.595383
&gt;&gt;&gt; iter 18700: 2.581249
&gt;&gt;&gt; iter 18800: 2.559557
&gt;&gt;&gt; iter 18900: 2.552271
&gt;&gt;&gt; iter 19000: 2.544696
&gt;&gt;&gt; iter 19100: 2.586441
&gt;&gt;&gt; iter 19200: 2.599598
&gt;&gt;&gt; iter 19300: 2.603714
&gt;&gt;&gt; iter 19400: 2.603543
&gt;&gt;&gt; iter 19500: 2.578862
&gt;&gt;&gt; iter 19600: 2.589547
&gt;&gt;&gt; iter 19700: 2.556354
&gt;&gt;&gt; iter 19800: 2.555944
&gt;&gt;&gt; iter 19900: 2.527344
&gt;&gt;&gt; iter 20000: 2.515879
&gt;&gt;&gt; iter 20100: 2.503299
&gt;&gt;&gt; iter 20200: 2.490162
&gt;&gt;&gt; iter 20300: 2.501330
&gt;&gt;&gt; iter 20400: 2.488866
&gt;&gt;&gt; iter 20500: 2.463605
&gt;&gt;&gt; iter 20600: 2.458159
&gt;&gt;&gt; iter 20700: 2.433686
&gt;&gt;&gt; iter 20800: 2.423189
&gt;&gt;&gt; iter 20900: 2.432274
&gt;&gt;&gt; iter 21000: 2.434593
&gt;&gt;&gt; iter 21100: 2.425869
&gt;&gt;&gt; iter 21200: 2.427357
&gt;&gt;&gt; iter 21300: 2.441660
&gt;&gt;&gt; iter 21400: 2.409635
&gt;&gt;&gt; iter 21500: 2.403614
&gt;&gt;&gt; iter 21600: 2.433992
&gt;&gt;&gt; iter 21700: 2.444090
&gt;&gt;&gt; iter 21800: 2.462798
&gt;&gt;&gt; iter 21900: 2.462520
&gt;&gt;&gt; iter 22000: 2.462924
&gt;&gt;&gt; iter 22100: 2.454772
&gt;&gt;&gt; iter 22200: 2.487916
&gt;&gt;&gt; iter 22300: 2.488028
&gt;&gt;&gt; iter 22400: 2.495287
&gt;&gt;&gt; iter 22500: 2.468934
&gt;&gt;&gt; iter 22600: 2.457199
&gt;&gt;&gt; iter 22700: 2.455810
&gt;&gt;&gt; iter 22800: 2.437125
&gt;&gt;&gt; iter 22900: 2.458581
&gt;&gt;&gt; iter 23000: 2.493252
&gt;&gt;&gt; iter 23100: 2.471698
&gt;&gt;&gt; iter 23200: 2.490359
&gt;&gt;&gt; iter 23300: 2.496645
&gt;&gt;&gt; iter 23400: 2.507487
&gt;&gt;&gt; iter 23500: 2.534732
&gt;&gt;&gt; iter 23600: 2.490386
&gt;&gt;&gt; iter 23700: 2.501691
&gt;&gt;&gt; iter 23800: 2.471074
&gt;&gt;&gt; iter 23900: 2.465607
&gt;&gt;&gt; iter 24000: 2.460707
&gt;&gt;&gt; iter 24100: 2.481947
&gt;&gt;&gt; iter 24200: 2.488133
&gt;&gt;&gt; iter 24300: 2.451984
&gt;&gt;&gt; iter 24400: 2.475954
&gt;&gt;&gt; iter 24500: 2.493711
&gt;&gt;&gt; iter 24600: 2.462351
&gt;&gt;&gt; iter 24700: 2.482828
&gt;&gt;&gt; iter 24800: 2.492132
&gt;&gt;&gt; iter 24900: 2.497655
&gt;&gt;&gt; iter 25000: 2.476303
&gt;&gt;&gt; iter 25100: 2.492079
&gt;&gt;&gt; iter 25200: 2.475966
&gt;&gt;&gt; iter 25300: 2.467218
&gt;&gt;&gt; iter 25400: 2.450641
&gt;&gt;&gt; iter 25500: 2.433377
&gt;&gt;&gt; iter 25600: 2.422653
&gt;&gt;&gt; iter 25700: 2.403179
&gt;&gt;&gt; iter 25800: 2.392250
&gt;&gt;&gt; iter 25900: 2.405882
&gt;&gt;&gt; iter 26000: 2.377624
&gt;&gt;&gt; iter 26100: 2.364691
&gt;&gt;&gt; iter 26200: 2.355837
&gt;&gt;&gt; iter 26300: 2.345257
&gt;&gt;&gt; iter 26400: 2.345679
&gt;&gt;&gt; iter 26500: 2.342889
&gt;&gt;&gt; iter 26600: 2.367379
&gt;&gt;&gt; iter 26700: 2.393426
&gt;&gt;&gt; iter 26800: 2.444213
&gt;&gt;&gt; iter 26900: 2.417209
&gt;&gt;&gt; iter 27000: 2.438486
&gt;&gt;&gt; iter 27100: 2.438410
&gt;&gt;&gt; iter 27200: 2.462644
&gt;&gt;&gt; iter 27300: 2.432779
&gt;&gt;&gt; iter 27400: 2.425466
&gt;&gt;&gt; iter 27500: 2.421917
&gt;&gt;&gt; iter 27600: 2.432899
&gt;&gt;&gt; iter 27700: 2.424900
&gt;&gt;&gt; iter 27800: 2.421964
&gt;&gt;&gt; iter 27900: 2.441862
&gt;&gt;&gt; iter 28000: 2.484662
&gt;&gt;&gt; iter 28100: 2.496116
&gt;&gt;&gt; iter 28200: 2.499512
&gt;&gt;&gt; iter 28300: 2.496692
&gt;&gt;&gt; iter 28400: 2.514777
&gt;&gt;&gt; iter 28500: 2.488605
&gt;&gt;&gt; iter 28600: 2.468500
&gt;&gt;&gt; iter 28700: 2.435790
&gt;&gt;&gt; iter 28800: 2.419856
&gt;&gt;&gt; iter 28900: 2.380359
&gt;&gt;&gt; iter 29000: 2.353039
&gt;&gt;&gt; iter 29100: 2.344961
&gt;&gt;&gt; iter 29200: 2.328637
&gt;&gt;&gt; iter 29300: 2.313071
&gt;&gt;&gt; iter 29400: 2.315946
&gt;&gt;&gt; iter 29500: 2.296986
&gt;&gt;&gt; iter 29600: 2.291862
&gt;&gt;&gt; iter 29700: 2.323659
&gt;&gt;&gt; iter 29800: 2.309146
&gt;&gt;&gt; iter 29900: 2.293766
&gt;&gt;&gt; iter 30000: 2.292499


</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[10]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Plot training cost curve</span>
<span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">cost_history</span><span class="p">,</span> <span class="s1">&#39;o&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;Iteration&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;Cost&#39;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[10]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>&lt;matplotlib.text.Text at 0x7f0764bfd4d0&gt;</pre>
</div>

</div>

<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAicAAAF5CAYAAABEPIrHAAAABHNCSVQICAgIfAhkiAAAAAlwSFlz
AAAPYQAAD2EBqD+naQAAIABJREFUeJzsnXmYVOWZvu+vem+6aDZxwT3OZJhk1ICJsmgmjsomqMHM
hCyTzPxmJiYxKopJFAYwEZMoLkTJxJlrsswkYTKJJuACSmJiFIgmEHciSUYEQVGW7q7uht7q+/3x
fp+nGrqBbhq6uuu5r6uuqjp1zqmvjgnn6Xd5Xue9RwghhBAiX0j19gKEEEIIIXKROBFCCCFEXiFx
IoQQQoi8QuJECCGEEHmFxIkQQggh8gqJEyGEEELkFRInQgghhMgrJE6EEEIIkVdInAghhBAir5A4
EUIIIURekRfixDl3rnNumXNui3Mu65yb1sE+I51zS51zNc65eufcU86543tjvUIIIYQ4fOSFOAEG
AM8AnwX2GfbjnHsH8ATwEnAe8FfAl4E9R3CNQgghhDgCuHwb/OecywKXeu+X5WxbAjR77z/ReysT
QgghxJEgXyInneKcc8AU4A/OuRXOuW3OuV875y7p7bUJIYQQoufJe3ECDAeqgC8ADwMXAj8B7nfO
ndubCxNCCCFEz1Pc2ws4CKKA+qn3/uvh9XPOubHAFVgtSjucc0OBCcBGVJcihBBCdIVy4GTgEe/9
jt5YQF8QJ9uBVmD9XtvXA+M6OWYC8P3DuSghhBCin/NR4Ae98cV5L0689y3Oud8A79zroz8HXu3k
sI0A3/ve9xg5cuRhXF3/Y+bMmdx55529vYw+ha5Z99B16zq6Zt1D161rrF+/no997GMQ7qW9QV6I
E+fcAOA0wIVNpzrnzgB2eu83A7cB/+OcewL4BTAJuBh4fyen3AMwcuRIRo0adVjX3t+orq7WNesi
umbdQ9et6+iadQ9dt27Ta2UReSFOgLMw0eHD4/aw/bvAP3rvf+qcuwK4EVgEvAx80Hu/pjcWK4QQ
QojDR16IE+/94xygc8h7/x3gO0diPUIIIYToPfpCK7EQQgghCgiJE9GOGTNm9PYS+hy6Zt1D163r
6Jp1D123vkfe2df3BM65UcDaY455Lx/60CQWLJhFOp3u7WUJIYQQec+6desYPXo0wGjv/breWEO/
jpy88UYpd9/9KCedNI6tW7f29nKEEEIIcRD0a3ECrwGeXbuaGTHibDZs2NDbCxJCCCHEAejn4mQ4
cDQwAvgA73znBYqgCCGEEHlOPxcnZwANQAXwJ6CS8877YO8uSQghhBD7pZ+Lk5XAFmBneMCf/vQq
mUymNxclhBBCiP3Qz8XJtcBLwOrwfAdQxj//83W9uiohhBBCdE4/FyfjScb1AEwG7uGHP1zRS+sR
QgghxIHIC/v6w0cDMA9YBZRjM4zGAuV473HO7e9gIYQQQvQC/VycfBAYikVPBgO7gP8FdlNTU8Pg
wYN7c3FCCCGE6IB+ntYpxgYcv4RFT14K74v49Ke/0JsLE0IIIUQn9HNxcg3wNHAhcEl4fhq4lR/+
cHlvLkwIIYQQndDPxckPgfdhLcVLgUeA9wKLgQr641whIYQQoq/Tz2tO/g74GXA1UILVndQAVUAL
bW1tFBf380sghBBC9DH6+Z35O1iHzmJgUs725cBneOONNzj++ON7Y2FCCCGE6IR+ntapA24DnqJ9
3clTwG1MmfKPvbg2IYQQQnREP4+clADfAE4M76OvyavAE7zwwuu9siohhBBCdE4/FydZYDfwYWAC
Jk48Vhh7E9lsG9lsllSqnweQhBBCiD5EPxcnrcBcYGLONhfeZ4ErJUyEEEKIPKOf35nLaC9McpkE
lNPW1nYE1yOEEEKIA9HPxckA2g/+y8UBabLZ7BFcjxBCCCEORD8XJ/VYjUkuPue5VsP/hBBCiDyj
n9eceOBh4DxgITZfZwA2rfg4oE1GbEIIIUSe0c/vyk3AZ4FKzO9kfs5nDwGPs2fPHsrKynphbUII
IYToiH6e1nFAOfAlkgGA08Lzb4BbmTNnYe8tTwghhBD70M/FSREwCPg68CjwBrArPD8KLGbZsid6
b3lCCCGE2Ie8ECfOuXOdc8ucc1ucc1nn3LT97Htv2OeqA5+5BCuK3QLMAZ4HngzPc4AtvPnmdk0n
FkIIIfKIvBAnWJXqM1iBSKdKwTl3KfA+TG0c5GnrsMjJFBKHWBfe38WePXXq2BFCCCHyiLwoiPXe
rwBWALhOlIJzbgSmMiZgLTgHQR1QAZwLzMO6dSqxbp3xwHVAJd57CRQhhBAiT8iXyMl+CYLlv4Bb
vffrD/7IFmAgcCnwR+BNYCOwB1gKjAMqlNYRQggh8oi8iJwcBF8Emr3393TtsDQmSBzwf8DXaG9n
/zDwGTKZDNXV1T2zUiGEEEIcEnkvTpxzo4GrgPd0/ehNWHAoCxwDXIMVyb4DS+2MA25l7tw7WLTo
ph5asRBCCNE3WLJkCUuWLGm3rba2tpdWk+DyLaXhnMsCl3rvl4X3VwO3075QtghTHJu896d2cI5R
wFo4HkvrHIXpsJnAZJLC2IeBOznxxFZeffWXh+03CSGEEH2FdevWMXr0aIDR3vt1vbGGvI+cYLUm
K/fa9mjY/u39HzoAqAJqgAVYh04kdux43nprjopihRBCiDwhL8SJc24AcBrJCOFTnXNnADu995sx
57Tc/VuAN7z3f9j/mRtIWocnd7LPFHbvvl7CRAghhMgT8kKcAGcBv8CUhMfSOADfBf6xg/0PMheV
AnZjQ/46Ex8OqFbkRAghhMgT8kKceO8fpwttzR3VmXRMG1AGZEgiKG+fhaT2JCNxIoQQQuQJeSFO
Dh/FQCvQiHm8jQcWYmZsA7C0zwigkVSqT1i+CCGEEP2efn5HbsN+YglwI3ARcA5WX7s0PP8tqRRk
MpleW6UQQgghEvq1OCkpKcfs6quA7diwv0kk6R3r2Mlm72bOnNs7PokQQgghjij9WpxAE1CKCZMT
2V/HzrJlq47YqoQQQgjROf1anBQXDwB2YMP/hrG/jp2WlkrN2BFCCCHygH4tTioqhmLdOkNIOnY6
wlNc3KBuHSGEECIP6NfiJJVqxCImO7DUzvJO9nyQSy4Zf8TWJYQQQojO6dfi5PzzR2FTiRuBWVjH
zoMkERQPPAR8lptuuqZX1iiEEEKI9vRrcfKZz3wcaMZqTr4HzAV+g7UUTwPOxQRLKdXV1b21TCGE
EELk0K/FyYABAzCztSLgWuDC8El0hy0HzgRSKoYVQggh8oR+LU6y2SxQjQmRscB0YAztTdg+DLRQ
X1/fW8sUQgghRA79WpwUFRVhxbADsVmC1wITaW/CNgm4m9mzF/bKGoUQQgjRnn4tTixy4oBa4Alg
Qid7TuHBB9ccsXUJIYQQonP6tTixyIlNHYbd7DuVOCITNiGEECJf6OdTiaG01NPcXILpsDosvZM7
lXgccB0lJTJhE0IIIfKBfh05ARg8+Ghs+N94LK2zd0HsGGACEyaM7rU1CiGEECKhX0dOvPekUkOB
LKbD5mAFsZC0E08EWoDVvbJGIYQQQrSnX4sT5xylpY1ADfAUcAMwj47SOsuX39Vr6xRCCCFEQr9P
60yefA6wByuIvZyO0zqX89ZbTSqIFUIIIfKAfi9OvvKVz2MBojeAmezrczIRuIbdu7eqIFYIIYTI
A/q9OEmn09jPLCWpN9mbSUCpIidCCCFEHtDvxUkqFX/iYNr7nOTigEESJ0IIIUQe0O/FSWtrK9ZK
nKG98Vou0ahNCCGEEL1NvxcnyXydRmBFJ3stBxpVcyKEEELkAf1enFiqphJoBq4EHiKJoPjw/nNA
s8SJEEIIkQf0e3FiDAaKMI+TrwOnY46x7w7v/zV8LoQQQojept+LE5tMXAeUA98BqjHPkx3AQGAz
cDNQrIJYIYQQIg/o9+LEunUaw7sa4LeYK+wIYDhwbHjfypYtW3pljUIIIYRIyAtx4pw71zm3zDm3
xTmXdc5Ny/ms2Dn3Nefcc865+rDPd51zxx7MuU2ctGHzc4qAo4FLgLGYfX0V8EdgABde+NGe/mlC
CCGE6CJ5IU6wQTfPAJ9l337fSuBM4CbgPcBlwDsx//kDYmkdB5QBO4FZwDcxcRJt7J8Ebuf3v3+V
TEYtxUIIIURvkhfixHu/wns/13v/U/ZySvPe13nvJ3jv7/Pe/8F7/zTWdjPaOXf8gc5tHTgtWH1J
OfAscC372thPBu5m9uyFPfa7hBBCCNF18kKcdINBWISl5kA7mjgZCNQDaWA1MKGTvS/mgQdW99Qa
hRBCCNEN+pw4cc6VAV8FfuC9rz/Q/uYQOxibTLwLyyB1bmPf0lKprh0hhBCiFynu7QV0BedcMfAj
LGrymQPtP3PmTKqrq4EXgVZMlPjw6EigeEpKGmTGJoQQoiBYsmQJS5Ysabettra2l1aT0GfESY4w
OQE4/2CiJnfeeSfvec97SKVOxjp2jsGcYpdjNSZ78xDTpo3ruUULIYQQecyMGTOYMWNGu23r1q1j
9OjRvbQio0+IkxxhcirwAe/9ri4ci0VKSrDC2B8BUzGxcnHOnstx7mpuvvmZHlu3EEIIIbpOXogT
59wA4DSSXMupzrkzsN7frcB9WDvxxUCJc+7osN9O733L/s5t9SNFQAXma/Jx4F3YPJ3PY7W1NeEz
Rzqd7sFfJoQQQoiuki8FsWcBvwPWYmGO24F1mLfJ8Vio43jMC2Ur8Hp4HnOgE1vkpBQzW4uGbM8D
3wBeAtaE52/ivZNLrBBCCNHL5EXkxHv/OPsXSt0WUd57ysuPZs+ebVhRbDE27C+35iT6nCxm4sRP
8vzzK7v7dUIIIYQ4RPIlcnLYcM4xbFgKG/ZXAWSASTl75LYNT+bFF7ceyeUJIYQQYi/6vTgBuPTS
87CC2AHYVOJ6YB5wAXBpeJ4H1OP9wGB5L4QQQojeoCDEyZe/fC1Wd1ID7ACmY+UqcbbOyvB+OrBD
PidCCCFEL5IXNSeHm0GDBpFMJm4DrsFm60RceN8GfEbiRAghhOhFCiJyYu3EHhiCde1M6mTPyUCV
7OuFEEKIXqQgxImRwmpNBtL5bB2AtMSJEEII0YsUhDhpaWnBCmHB6k5yxUeG9sWxNVxzzXwymcyR
XaQQQgghgAIRJ8XFxUAtkMWEycPhkwz7FseuZ/HiMYwZM10CRQghhOgFCkKcWGtwI1YQ64A7gQeB
24BrsWLYmOpxZLOTWL9+JnPm3N4byxVCCCEKmoIQJ6lUCjNgq8dEyieAu7EhgBM6PCabnciyZauO
1BKFEEIIESgIcWIFrkOAcqASG9lzNDCYfYtjYz2Ko6WlUsWxQgghxBGmIHxOLHKyA4ueZIGjsOLX
uZgYqQcWAqswF9kGYCxFRbXyPBFCCCGOMAUROTGBsQcowupO5gK/AUYBP6Fjx9hzqK+vUVGsEEII
cYQpCHFiqZmjsChJBTAOeAC4B0vxRMfYpCgWJlNTc4uKYoUQQogjTEGIE4uc7ALSmAnbQmBEeD2U
zhxjs9lJKooVQgghjjAFUXNikZNSoA6LijyJRVGymGDprK4kKYpV7YkQQghxZCiIyImJkzSwG2jC
CmD/DzNjy9DeMbbdkZSUNEiYCCGEEEeQghAnJi7exFqJjwK2AmXAl8Lr5R0el0otZ9q08UdolUII
IYSAAknrGGVYfckOoAQTKeeEx11YaicWxZrFfXX1jdx885O9s1whhBCiQCmIyIkxCJuvU4917AwD
fglcDtwHPAVcBFwSnp+mpcWRTqd7ZbVCCCFEoVJAkZMMVm+Swrp06rEIisPqUeaH/TyxQLah4REV
wwohhBBHmIKInDjnSKVaMSO2NNZWPBqLpOxdDOvffva+9sgtUgghhBBAAUVOKipKaWhoBqqAt4DN
4ZMVwBnAPwBbsPRPDSZiWnthpUIIIURhUxCRE+89VVUnYXNzdmDFsc9j2uyzwHnA1WHbk8AzwL8C
Lbz++uu9smYhhBCiUCmIyIlzjqKiDCZOslh0ZAjwMta1Mw84DTgTaMamFe8CyvnAB/6Wl19Wx44Q
QghxpCiIyAnAkCEVmENsLIbdhKVuGoB3ABOArwAvAavD8x1s2PAaGzZs6JU1CyGEEIVIwYiT2tpW
LCqSwQRJC1CJRVH+FlgMTCbxOSG8X8zYsR864usVQgghCpW8ECfOuXOdc8ucc1ucc1nn3LQO9vmS
c26rc67RObfSOXfawZ7fe082OzC824MJk8GYSKnBRMt44IvA6ViB7HjgLOAJduzYc0i/TwghhBAH
T16IE6wY5BmsOnWfQTfOuS8AVwKfAt6HqYpHnHOlB3Ny5xwlJQ0k5mtFWGqnlSTVcynwOPA14Flg
FfA0cC7QSk1NzSH8PCGEEEIcLHkhTrz3K7z3c733P6XjEcFXA1/23j/gvX8B+HvgOExRHBQXXzwW
qzGpw0RKIyZOhmJzd07ACmPHY4ZsFwCXAXcCY7nhhq9178cJIYQQokvkhTjZH865U4BjgJ/Hbd77
OsxvfszBnmfBglmYMGnAUjotmA7aA5RiHidjgenhtCuBpeH5I/znf95HJpPpgV8khBBCiP2R9+IE
EyYe2LbX9m3hs4OiqqoqnMYT24ShGkvpVGPRlNuBa0kGABKeJ9HScgdz5izs/q8QQgghxEHRF8RJ
Z+S21RwkezAR0oDVndSSRFO2YnUmEzo4zgNTWLZsdfdXK4QQQoiDoi+YsL2BCZGjaR89GQ78bn8H
zpw5k+rq6pwt27FISZw03IKJlNbwGEYSMckACzHBMgBo4K23dlJXV8fAgQMRQggh+jpLlixhyZIl
7bbV1vb+XDnnfReDD4cZ51wWuNR7vyxn21bgNu/9neH9QEyo/L33/kcdnGMUsHbt2rWMGjUKgGw2
S1HRGJK5OUVAGxY52YOleUqAF7BOnulYimcCSZDmYd71rkWsWXMf6XQaIYQQor+xbt06Ro8eDTDa
e7+uN9aQF2kd59wA59wZzrkzw6ZTw/sTwvu7gDnOuanOub8C/gt4DatYPShSqRSJMKnDUjr1wMWY
MElhtSYPYRGTjmpPprB+/UzmzLm9+z9WCCGEEPslL8QJ5nb2O2AtFqK4HVgH3ATgvb8VuBu4F+vS
qQAmee+bD/YLLELksNROC9ZKTDhdGZbS8cAC4Gd0XHsC2exEli1b1aUfJ4QQQoiDJy9qTrz3j3MA
oeS9n48ZkHQL5xypFGSzJSSFsS1Yrcl5wKPhsQqzT+nIbgXA0dJSifce5zrbRwghhBDdJV8iJ4cd
7z2lpSXYNOJK7Kc3A7uxOpNWYATWVtxRI5B/+7mkpEHCRAghhDhM5EXk5EjgnKOoKIvVm0QBApbe
aQKqsALZLcBmYDlmXd++YwdGMHHie4/s4oUQQogComAiJ0YZFinZiRmxVWGXIJqxnQ78DXALJkou
xEb5RLfYR4EP8dhjv6auru6Ir14IIYQoBAomcuK9Z+DAETQ0bMNSOEWYSBmGeZpUYjW4ZcDlwK+B
87F6lPlY9KQM2MyGDY5jj53G8OHFTJ06jgULZqm1WAghhOghCiZy4pyjrGw3Vghbhc3TKcVaij3w
F8DrWPrGAb/E0jpx1s79WAHt14BnaGz8JRs3rmTx4jGMGTNdc3eEEEKIHqJgxAnAlCljsCnEldjw
v4GY4MgCrwKDMLFSixmy5c7aia8nket9ks1OlPeJEEII0YMUlDj5ylc+j9Wa7MIM2XZhl6AFOBEz
ZdsNfC68zp2109ncHXmfCCGEED1JQYkTqwvZg9WOtJIMADwZeBYTJMXAb7EuniKStuKY7umIxPtE
CCGEEIdGQYkTEw+xO2cAlrrxWK3JUSRiJB22vxaeHSZkOhMf8j4RQggheoqCEieGx1I6GawgNoX5
m2zDREs5lu4ZhgmSh8O+ReH1vqRSK5g2bfzhXrgQQghREBRMK3FCESY2oltsDSZKMlgXj8ecY3cC
NwNfDNtnAYtIBgQ6IEsqtYKRI+/i5pvvO8K/QwghhOifFKA4qcDqTiBxi92ORVHeBE4LzyXAR4EX
sZbiycBFmEHbF8LxVRQV1TF+/NQjtnohhBCiv1NQaR2rOanCWonLMdv6WqyVuBm7HH/ExMvxWHTk
Kax9OLIWuBUroF1NS8vz/Md/vF9eJ0IIIUQPUVDiJJVKkbQPD8FqTfZgIqSVpIOnFCuGrcUETCx0
XUjieyKvEyGEEOJwUFDiBCCVasHqSnZiImQwlt3KYu3DJZhd/R7g0+Go2KWzt9dJ0r0jrxMhhBCi
ZygoceK9Z9iwP8OcYRvD1p2YOIm29pXABswR9nfYIMBHMCFSgXmhzAMuAC4Nz/OAenmdCCGEED1A
QYkT5xylpc0kniWV4dGGCZNBmMfJauAyLPVzBXA98BHgZZJZO7mTis8BplNUVCuvEyGEEOIQKahu
nUwmQ339W5hF/YDwPAirH3kDi4x44OiwbRfwsbC9BJvLcw0wDriBxPckDdRTX+/JZDKaUCyEEEIc
AgUVOZk9eyE1NWdgmmwwVuxaEx4VmFjZgxmyZbAIyzFY2ua1sM944BLgcWxC8bNYLcoz7Nx5C2ef
fZm6doQQQohDoKDEyQMPrMI8THK7dlKYEKnGLOyrgK3AP2PRlZexVuIsFiG5HRsSOI+9JxTDxfz+
99eoa0cIIYQ4BLolTpxzc51zlR1sr3DOzT30ZfU83nuam2ONSQqLkFRg9SYOaxvejQmVBZifSRrz
Q0lhoqYBeALYxL4Tin34ninq2hFCCCEOge5GTuZhIYa9qQyf5R1WDNuICYw2LLWTxlxiS7HunQqS
bp0irDMng0VNAIaH99H7JMO+nTvzaWoqJZu1Y9S9I4QQQnSN7ooTR8cjes/AenPzkqlTx2HOr0Vh
Sy1W6FqMpXQ2YwWyT2I/sQgzZluB/dxnMXGTxUTN3p079wMbef31P5BOn0Vx8btJp8/npJPO56qr
5qkWRQghhDgIuiROnHO7nHM7sTv1BufczpxHLXaX/t/DsdCeYMGCWbzznZswcZHFIiOVWBdOHRY5
2YVFVgZh83RagS9jkZViLMpSD1xJe7fYDHA5Vix7Mo2Nt9DW9jwNDb9g06afs3jxObK4F0IIIQ6C
rrYSX4Pdib+F5TNqcz5rBjZ679f00Np6nHQ6zdNPL6W6+izMw+R1rGsn1pvETNUOTKB8DvgfrHun
FKs/ibUqa4Hv5pw9WtuvIREtEUc2O4n162HOnNtZtGj+4fmBQgghRD+gS+LEe/9dAOfcK8Aq733r
YVnVYaSqqgoLGNVjTrG1WFSkKjzqwp67MfO14cBngG9iKZ1G4CvAv5F06oAVys7HRMr8Dr/bLO7v
YNGiHvxBQgghRD+juzUnGWBkfOOcu8Q591Pn3C3OudKeWdrhwYb/NWGZqWpMpDRjaZx6TJTEtM4q
LED0POaFksWiJ5PCfrHspi6cE6z9eG+X2Lifk8W9EEIIcQC6K07uBf4cwDl3KvBDLKTwIeDWnlna
4cG6aFrCu11Y9KQK2E5Si9IWPqsAzgQexMRHOdbh4zCX2EfCeXJ9TaI1fkedPHNlcS+EEEIcgO6K
kz8HngmvPwQ87r3/CPBJrIWlR3HOpZxzX3bO/Z9zrtE590fn3JzunMsiJxVYzUkrJkYGk7jDDsCi
Jqnw/Pdh3zJMf8WpxrMwHfYJ4D6SAYHjgJ+wbyfPSuAc6utrVBQrhBBC7IdDaSWOx15AMmRmMzDs
UBfVAV8EPoUVf/wF8Hng8865K7t6IkupDMVSOEMxofFW+LQUEyJvhtd1mFvsLszGfjBwEfZzM8AW
4PdY5OV64A7gdOAmrHY4dvIQnidTU3OLHGSFEEKI/dBdcfJbYI5z7uPA+4GHwvZTsNaWnmYMsNR7
v8J7v8l7fz82Dvh93TlZKtWARULqMXESO3GGYJ06cfZOA5bGARMqtVgL8fXAuVjkZS5JMe19WH1K
G1aXEklqTLLZSXKQFUIIIfZDd8XJNcAo4B5ggff+j2H75cDqnljYXqwG/sY592cAzrkzsPzJw/s9
qgOcc1RWggmRNkygDMJSNhkstVNG0rWzE0v5bMdSOpdhoqQV+DowhaT+JI3VmbwjnHfvmpN5QL2K
YoUQQoj90FWfEwC8988Bf9XBR9djd/ye5qtY5ervnXNtmKia7b3/n+6c7KMfncK99y4lKXKtwy5F
NFobjAWAyjBhUom5xaaA0zCn2BRm0gZWfzIdi5BMxCIs0zG/k/kkhrqPANMpKmpWUawQQgjRCYc0
ldg5N9o59zHn3Eedc6O893u89y0HPrLL/B3wEeDDwHuwKtTrQ1qpy9x222xKS1sw8VGN6amK8Gmc
WBzbiQdguigdtv2epPU4Cow0ltL5FfBu4P/ouOZkAnA1gweXd2fZQgghREHQrciJc2441j78fswA
xAHVzrlfAB/23r+1v+O7wa3ALd77H4X3LzrnTgZuAP67s4NmzpxJdXV1u20zZsxgxowZDBkyjDfe
yGLFsClsts6b4fVu4GgspTMU+4lNwHHhLHEgoCexrp+Ldekci4mVWHOSwYzZVmFCp4E//WkbmUyG
dDrWswghhBBHniVLlrBkyZJ222prazvZ+8jhulP74Jz7IVZY8XHv/fqw7S8xP/c/eu9n9OginduO
pXHuzdl2A/AJ7/1fdLD/KGDt2rVrGTVq1D7n896TTo+moaERayWOE4lTWHSkDSuSbcYGA6ZIhEgx
Vvy6DfgGMB6bp/M6FtS5FFiEiZEMSXpnAkl652He9a5FrFlznwSKEEKIvGLdunWMHj0aYLT3fl1v
rKG7aZ2JwKejMAHw3r8EfJb2bSo9xQPAbOfcZOfcSc65y4CZ2BjgLuOcY/fuJkyYDCWJlmRJJhY3
YNGUPZhYGYwVxDZgNSpZ4EvAFdik42rgOeCFcLwnmbezd3pnCuvXz1RLsRBCCNEB3RUnKRKb1Vxa
DuGc++NK4MfAYuAlLM3zb1gupct47ykvPwpb6k4sauIwYeKwqEkJVnsyPBxVh3X4pDCBMjzssw7z
O2nE0jmrsTbjh7HoyYQO12BzdtRSLIQQQuxNd4XEY8Ai51wswsA5NwK4E/h5TywsF+99g/f+Wu/9
Kd77Ad6mZh9BAAAgAElEQVT7P/Pez+vu4EHnHEOHOixtEwcAlmDaKk3iHtuKpWZaMfGxA+vuIbw/
C4uaVGGCxWFFtk8DXyYROx2uQi3FQgghRAd0V5xcid3FNzrn/uSc+yPwStj2uZ5a3OHk0kvPw1Iv
xVhRbBmWqslg0ZRKLOVD+AxMaLRiKZ49mA/cVkzgVGBecX/COqpXYmKmM/HhKSlpSN5JpAghhBBA
N8WJ936z934U5kB2F+ZGNtl7P9p7/1pPLvBwsWDBLCxaUoGlcQaS2NrvCe8zmGBJY2mcNqy2pByL
mLSGbSMwAXMfiddJGrs8cThgLhngk2zfvoN0ejTFxe8mnT6fk046n6uumqfZO0IIIQqaLokT59z5
zrmXnHMDAbz3K733d3vvvw78xjn3onPu3MOy0h6mqqqK4cNPw8REbBeux9p9W7DumwZMqGSwmpPo
HFsD/CVJ981rWPTlGOAkklTOp7CxQA+SRFDqsPk8F1NffxQNDbfQ1vY8DQ2/YNOmn7N48TmMGTNd
AkUIIUTB0tXIyTXAf3jv6/b+wHtfC9yLtafkPWZj34yJhl2YIMlgkZGBWLqnEousNIXPBoXnZuAX
JNONl4Z967FIiwc2AH8NzAZ+A5yPOf6/B5iDdfXs28mTzU5SJ48QQoiCpqvi5AxgxX4+fxQY3f3l
HFkuvnhseOWwOpJiTKgMxMRGdXhEv5NakiJXF/bdFfYdFB7jgB9gXTp3AR/C7O2LsCLZUzDbe3Xy
CCGEEB3RVXFyNB23EEdaMXOQPsHNN18XXrViRbBlmIiI7cX1JNGQ2N1ThomYWHuyG7NbqcUKYK/D
5ukch1m+ZLBhgTMxUTIgfOcA1MkjhBBC7EtXxckWOh74FzkdK9boE5g7awoYhkVGqrCUTCvmABuN
2tKYKBkaHg4TMIMxvXYd1lrcinXpFIdz1mMOsdsx75P5WDcPWD3L/jt5cocDSqgIIYQoFLoqTh4G
vuSc22dynXOuArgJq/7sE6RS8ed/G4uENGLRkXIsctKKBYri4L96LI2TDp/VYCJjBCZiqjChEmtT
bsOKYkuBy7FW4w9iHTzj6LiTB1KpFUybNp66ujquumoep5xyASeccCmnnHKBunmEEEL0e7o6+O9m
7O66wTl3D/Ay9uf/SMy6vghY0KMrPIxks1lMSPwAS8mUYWmaIVh05HXs59VjUZQhWETFY2KmBhMe
g7GhgbuxluMoYB4Fngjnvgkrfj0dS+/cCNxB0nocO39+zKBBN3P//dV84xtLaG29A4u42OeLFz/C
Y49N11weIYQQ/ZYuiRPv/Tbn3FjMOv4rJEUTHgsDfMZ7v61nl3j4aGhowARGLD5twSIgMeUShwFm
sbRPHRZVacTEShQmr4btDkvhFGE1KBlsPuIbmADZigmT2Vi3Tkt4fS3gSaUc3reyc+dd7Nz5FDA2
HBdxZLMTWb/eM2fO7SxaNL+nL4kQQgjR63TZhM17/6r3fjJWVHE2cA4wzHs/2Xu/sYfXd1i58cbb
sPSMw37ObqzzhvB6EJbSyYZtsUsnduwMwkRIM5bSqcQEC+GYVuB3WF1KPVYgewvWwXMTNgXgl8AJ
wB1ksx/C+7sx87bVqJtHCCFEIdLVtM7beO93YQYefZYHH1yNpWFeI4mUlGBiI4VFSmJRbDkmShrD
fsVYZGRP2Lcec4sFqydZhQmYOPX4NkzAjAfmAY+H89cSDHaxNM9NYS0H182TWzQrhBBC9AcOxwTh
PoH3nqamMtp3zRRhAqIEi6Q0hNexBiVN4mlSgUVXSkjs733Y7+uYUElh9SfjgZ+F4y7H7GJKsSjK
SZgwqQvHxOhM17p5hBBCiP5CwYoT5xz19ZuBuSQW9g6LZLSR1JcMxYRCCmsfriKpJ0lhEZTcgthq
EhFTHfZ5Vzj3Zszv5NnwPBaLzNRjoiU61sLBdPMIIYQQ/ZGCFSdGKXApltr5Nhb9aMXEyG4SsRJr
SlrD+6bwHMXLznCuSkysbME6f3aFz+7CBE8JVuD6RHi+HUsZ3YYVxV5AIkhmYWme5SSCxZNKLWfk
yDtzDOSEEEKI/kW3a076Ot57qqqOJZMpwjp2rsQiGEOw1t/oArsNOJZEjOzBxEIZJlg2YSLmGExo
bMJERjPWjVMF/Bh4P3AqFnFpCsc8htWw/ByrNRmHmbbF9uLvAP8AXA+kKSrK8K53jWD58u+ojVgI
IUS/pWAjJ845ysp2Y0JgBNbmG4tcS7GISB0WDYmmZwNJalAqsbbhUpKZPDuxupVog1+B1Zncg3Ve
b8bSNzUkk4znxhVh6aD7gF8B78ZqVa4CngdW09b2PC+8MJOLLvqkjNiEEEL0WwpWnABMnTqOVOoR
4D8xYTCOpDtnOxYlSWNpnmGYAInur1GoDMMiJE0kgqQSExtDwr6PYqJkBPDPWIrn8rD/BzExk1v8
uhZ4L7AYayt2bz/M50RTi4UQQvRfClqcLFgwi5Ej7yCVeh5L2/wBEw5DMLFRjqV4ssBGkkGAbVj0
I9abpDCBMRgTMzUk9SrRrM1hIub5cL5dWK2Lw+buxFqThVj9yWu0N2BLkM+JEEKI/kxBi5N0Os2a
Nffx2c/+OmzZiEU9arFakWosOlJG0jIca04cJlxyxUcGEx0ZLMJSH/avxcRGE5aycZiQiZb1szBR
8iDmj3IRhzq1WIMChRBC9FUKWpyACZSvf/0mjjtuKFbEekJ4jrNzBmKiogxL2YAJhzasowcs0pIO
7/eQ1KkUhdd1WJFsNF0bEc49HlgRzpEFfhTOkaJjn5Oka6cjn5NMJqNBgUIIIfo8BS9OItOn/w2J
db3H0jUOi35UYCJlECZKBmIixGGpn10kUZQykrqU8rB/ERZdKcKEz5vh2DOxduLPYh053w3f5Ul8
TjKYo+wFWNvzBcAnmTjxve3Wn8lkGDNmOosXj2HjxpVs2bKUjRtXsnjxGMaMmS6BIoQQos8gcRK4
/vp/wlItYzGB0Ihdnj1YFGUXFvUYgAmXaHdfjUU7SsNjSNi3KHwWt1eSTCsuxkTLPeGcz5LUl0RR
Mgu4FbgQeB+wElgani/nscd+TSaTeTt9M3v2Qtavv5ZsNk44BhXQCiGE6ItInAQWLPgGlmq5Dqs3
qcIEyFEk3iSxlqQpfDYQS9VE+/oKknk7hNdpktk7VVg0pQkrjh2GRUyqSGpWmrD24ceB9wD/inXs
1GMRlAuBb7JhwxsMHTqGESOmccopF/Cd7zxENrv3oEATLiqgFUII0ZcoWBO2XDKZDN/61gNY0esq
LJoxCBMM20mKXsGiJsMwc7a6sG0oFhWpCNsqaD8M0GHRlaOA0cBPMOHxHHAKJoq2YCLkWuBp4Oqw
noWYaJkePrsOa0O+g5aWibz+usPqVSaRCJyF4XcMwGpXxtHUVKpBgUIIIfoEBR85yWQyvPe902hp
qcAiGP+CXZbdmEhpDe+bMHGxm6RoNbrAxmjJrrD/IJK5Om3htceEy1pMvGwM+y3HZu9cgAmPm4HP
AB8hEUixvTha3l9LIkbI+Z46TMSMoX0a6By2b/8D9fX1PXTVhBBCiMNHwYuT669fwMsv78YKWv8V
M0Vrw6IRe0g6bmLr8FAsIpLbsdOIpWvKsGBUbdinPBy3M2yvxyIuMbKyK5xjPSZE/hubVPzvwDsx
0bMFc42NKZtVOa8jsYD2cyQiJqk7gUm0tt6huhMhhBB9goIXJz/4wcNYLUcpdlN/iaTuoxkTJwMx
gRKjKSdi0ZBWTJA0YyIjusXuwdIpaUy4NIZvKwnn2o4JlhZMBKUxIbMVS/V8Apu10wScBxxH4okS
/U/27uL5OfAU+woXw/spqjsRQgjRJ+gz4sQ5d5xz7r+dc9udc43OuWedc6MO5ZzeexobwUzPhoSt
5eH1AkyQFGERjmpMGAC8gomLaFVfQeIWWxKOiQ6x0cwNLC1UE74jzu/Jhu3bsOjJk8C3sAhKC/A1
TLRE47cM+6ZvvhfWcCKHYtwmhBBC5AN9Qpw45wZh+YwmLDQwEivQ2HXoZ09jYiIWtzZiouL9wMnh
85awLY1FSCqwaInDxMcwLOWzm8SnxGOXNxP2GUTinVIdHnXYNOPa8N3bwk/cCvwWEz7PAWcB9wNf
xITR3umbheFyZOmqcZsQQgiRb/SVbp0vApu89/+Us+3VQz2pc47KyiYymTiZeDmJTf3WsFcGi6TE
QYDlmAgYiomPGiy9swdL8VRhEZZdJGmYGuxSN+91TEnOeVsx4bMTEy4Phe9djQ0AnIB5sNyKpXy+
k/NLngDmA2swj5Rx7NuxM6KdcZs6d4QQQuQrfSJyAkwFfuuc+1/n3Dbn3Drn3D8d8KiD4CMfuRB4
GPg2cA0mHAZhN/VxmMDYg12qLCYYirAISx3JRGLC5zUkQwH3hOeG8IjbmjBhMh6LmjhMvJRirrF1
JCKmAnOQvQ2LokzH2o9jiucLYS2OxLjtIuAc2nfs/C2PPbaGK664Qfb2Qggh8pq+Ik5OBT4NvIzd
eb8JfN0597FDPfFtt93IyJF34tw64DGSm34GS52kMQFRHl7H+pMGkpbikvC5x4RHbCtuCs/lWGSk
lmSIYMxUFYdtWUyIHIdFWKqAY4FNWMfOc1h0J7Y5x7qTbZhY8mHN24A5tG81dsB5bNjQxL33nnvQ
9vaqTxFCCNEbuL5wA3LONQFPe+/Pzdm2CDjLez+ug/1HAWvPO+88qqur2302Y8YMZsyY0W5bJpNh
zpzbWbZsFRs3voIVqILVcXwBEwRxivBWksF+lVjUogoTHDuwwYE7SWbw7Ar7tZCIjupwfDRoy5JM
Km7B0jcrsZqSH2OiJB3WtBJL4bwKfBhL34zFWo/nYULnBfYtjJ2HRVMm7X25SKWWc+WVT7Fo0Xwy
mQyzZy/kgQdW0dIygJKSBqZOHceCBbNIp9P7HCuEEKLvsmTJEpYsWdJuW21tLb/61a8ARnvv1/XG
uvqKONkIPOq9/5ecbVcAs733J3Sw/yhg7dq1axk16uAbejKZDIMGvY9s9mgsAlGKRT+iyVkrJjhi
1KQKExzFYXsm7OOx9M9Oks6dNBbtGIwJlgYsShLTN4OxyEo11oXzo/B5LJb9CyzlMwY4HWshfgG4
DOvWGRU+24bVnezNBZiw6ajOxHPyyRfx3HP3M2bM9DCjZwKxfTmVeoSRI+9gzZr7JFCEEKKfs27d
OkaPHg29KE76SlpnFRYayOWd9EBRbC433ngb2ezxmNB4ByYYBoZHCotq7MbSNrGLJ3fGzgAST5Na
TLgMwtI1b4TXNeE4MIGyK5y7Doug1AKPkljhDyGx0b8O+CpwCUlBbuwGKsOiOm103LET/VE6wtqM
Z8++TcMDhRBC9Dp9RZzcCZzjnLvBOfcO59xHgH/Cxvr2GA8+uBq7kTeSeIs0kHTXlGMurynsZj8k
7FMbnneG7UPDOSow8bENS+3UhOOLMEERIzC50ZjoTFuJRWSaSAptVwBvhu3R72QH1tkTfVjiVONc
XDh/Z1EyazN+4IHVHQwPNDQ8UAghxJGiT4gT7/1vsfzFDOB5YDZwtff+f3rwO2hpiTf34zGh8BZ2
U48RkCFYhKISEwaxRTg6vcYoShQgaUxcDMTEgyO55LG+pIykyDa2KZdiQuMorP6XsJ5Z4Ttmhfef
w6YaXxvW0oDNBvoi8CCJ30pslX6ow9/u3HKmTh0Xfr9M3IQQQvQufcXnBO/9w1jP72HBOUdRUQZL
nUwhsauPEZPtWCSkGBMOteFzR1KL0oQJhBj5eDPsGzt+olBwJE6xxeE8TcDRWGfO8VhkpAy4Efgf
TNQcHbZ/M+yzFjgJ+DzmfXIGNrH4euBuTKRUYSKrCOdWY9piCiagbgN+TlERLF1aRl1dXc769qZ3
TdzkyyKEEIVDn4icHAkymQz19Tsw+/jxmHAYFp6bsZt/9CqJN/EykoF/bTnPLZhYidGTbSS1KhVh
+x4sGpMFhofzNGBiZSfJTJ5HSIzhWjDhcF1Y9TDgV5gQOQYzbLsW+C4wM7wfiGW/Xsbqmn6DFc6+
BzgbeJLW1lVs2vRzMpl307H+86RSK5g2bXyXr+uhkMlkuOqqefJlEUKIAqPPRE4ON7NnL2TXrnnA
XZhI+BtgIyZMzgC+hGm5HSReI9GqvgQTFH+GRUsqw/tyTMiUkaR+4iDBcky0HEdSTPsWJmYywLmY
UPp8OH90enWYW+xDWPdNnO1zNBYleR4TJhOx9uFoc084903hN43HIii53A1chHMe788DbsdqkYso
KtpCU9NUMpkM6XT6sEcyMplMTufQfGLn0OLFj/DYY9PVOSSEEP0YRU4CS5c+gfeXYb4ipVhq5DUs
/fInrIajBItmxPRMmqSLpwwTLvGGHWtNPBYhKcFM1cBqTKIgiYWwu0iM2AYAczHteDomaN7EIiUD
gdeBZeE7o6V+PSZOniQRI6vYd0pxBngAmEz7ycYXY/U2u/H+Wqxt+X2YAHqElpbn+fd/fy8nnzye
k046/7BHMmbPXqjOISGEKFAkToC6ujq2bm3CboIxHVMF/IREiFyFFcQejQmCYzHBEAtZU1hEoiUc
DyY4HBZFGUYSGQETHjFFFFuBB2C1LYOBz2BC5RmSTpw4lPCTWM0JWORkGzYc8E8khm6dtQ/fhkVr
6kkmG99PMgH5d1jd8WIsshKPr8f7b7Jz51fYtOnnB+Uweyg88MAqdQ4JIUSBInECzJlzO62tkLTa
xnbc2GGzEUuVTMD8T8AiKkUk6ZtSTBgUh+Pi+yZMtGwP2+qwaEklFmmpwARHdI6tCOf8Y9hWhIma
wSQzdDaTtDHvCOd9DUs/bSMpat27fTiD1ZTswERKTPncHl5Hy/tVJNGXyMKwz2QOdyQj6ZxS55AQ
QhQiEifYX+lWYxL9QWYBd2BTik/ERMJE4FNYJGMAJjgqSCIjZeF9rD8ZQjIssAITKRksQlGFRVUa
MdERTdjqsBRQLIzdgRXYnk0igmKx7VasCLYsrPlZLDpTmvM7cj1PMsAHw7E1wM9JUj4x/ZPB0kmx
CymXvVNEiTDo6UiGc46SkgP7sqh7Rwgh+icFL06Sv9KvJxEkVcB9wK9JRIHDWnhPwgREdJItDp9X
he0eay2uwYRJCSZAYnQlUh4eO0nqkmMkZAAmaNrC8zdJun2asUhLCzYHcRAmKo4DfhY+j7/jOizi
8SCwAPNA2Yh1B0H79E9M84wlKfR9+yrl7BNrVC4Nz3OB+h6PZEydOo5UqiMbfnqlc0gIIcSRo+DF
SfJXehQkT2HGZx/DWnGnkErVYzfo1ZjgiFOBd2HRiiGYGNmBiYVYc9IWHm9hQqAsfN6EpXCGYCIj
ioE40TjWmAzChE3sCEpjQsaHfbKYuBmK+aPE4tt/Cb/jEszh/wfAT7FOnjgDqCz8hvlYrUpummcc
5kYbC2YvxNJMuTUqZ4bf+BQwhtraP1FfX9+VS79fMbNgwSxGjryDVGo5iVDypFLLGTnyTm6++bpO
jxVCCNG3KXhxArl/paexm/VK7Ga+EudOZ/DgYqx1NzrIjsRERBQTMa3TikU1BofP4uDAepJ6kloS
K/taTHSUh2OjT0pNeDSHcy8gSf2UhvNtDuuJ578g/JoizHztBeD/sNboo8OansAiPqVYQe9FWEfO
B2mf5vkU5j57ETbJeGXY/5rw+z9IbicPPE99/Vc5++zLDlgYe7DeJel0mjVr7uPKK5/i5JMvYsSI
Szj55Iu48sqn1EYshBD9nD4xlbirdHUqceKpMTOnddXj3P2Ult5AU9NczOfkKCxdcgkWqWjGxITD
RAYk3T0xnfNGeF+J1ZK0YHUsr+dsj4MAh2NRlj2YgGjDIiUxHVSH1ZnswETI8PDd27CW49cxsVKE
iZsKYA1muDYknKcCE0JvAbdiHTlbMGfZNVi05HIsGvNBLNryePgd6zHH2o48UgAe5IorVvNv/3bL
Aa5z16ceyyFWCCGODJpKnCd09lf66af/Oy0ti4A/YNOAq7Dow/ewS3cUdoM9ChMjUzChUYJFSmow
8VGGCZMBWFplF4mzbOzwKcFak2NbcnSaHRa+w4XPXicpvK3FhMpQTDg0YFGUMqyI9jjgFkyU7Ay/
dixWN1NE4nXyifBZHSa8tmEFt/+OpXHODcc4LFoyuZMrOYXvf//RTq/zoXiXSJgIIUThIHESSKfT
LFo0n1deWcnmzT/llVdWUlvbFm6kq7C0yV8CV2Jpk2rsZh4dXYcCN2NCYBAmHMAESYx+VJP4nFRj
oqaZpLMnmrkNCI/4HSWYqCkNjzg0sD48N4ZzNGECpgabu/MqZtYGJqzOBU7DBFbsNLoFa5O+CPh0
ONfw8L2xBmUNJpayYX2dt/g2NpaRzWY7/HRf75LD1/EjhBCi7yJx0gHOuZwuHrAb8uVYxGMhFqVo
wYRFFXaTrQn7ZsPrGP2oDc9Dw/HRRTYW0FaQmLNFE7ZB4X01luKpCce2kbQhF2NRmdhenAnriWuO
DrYDw5qqwvabMSETBxHGSMgsrDtpXjjPbqwGJXbqxLbkDB23+FobclvbTk488bK3a0m2bt3KVVfN
48QT38/GjTGys3fHzzwgI+8SIYQQgMRJpyRdPGDFpzMxo7PLgBHYDb4MEw5xWvAVmCDYQzJLJ3bm
1GFRiRJMnDRjaZiBWA3ITkyU5BbL1mKRklivksJERlzXoLCOODQwFtxCIoBqSdqNfxu+f374/h/n
rMeH80zEUj4xZeXCsdcBd4a1rtjramWwTp5zgJfedo+9++7TOfXUv+aee05n8+ay8B2x42cllh4b
i7VAT+KNN/6owX5CCCEkTvbH1KnjcO4nmMiYgEUQUiSFrYOwm/wJmGj4LVbsWo4JkTRJbUgWu+HH
1uAoNLaH80ZvlIEkrrLRuG0IJjwGkdSrxLROnMnTFr5vdzhvKuxXQeK5kgrffV54fQPJhOVbwvH1
WPFrbFnOYBGeJ7FW6+FYcfDycOw8LKpyNRaBqcfSXmcAX6Cp6U68fw5LEVVjHT8Tae+rshy4gLa2
Y7nnnqcYOnQMV1xxg0SKEEIUKBIn++GLX/wUJSVfwApLoyjx2A21DLtxH4V1tKSBUzBRMpTEhr4K
ExJt4bPYIjwUExutmCCpDuevC98+NJw7TkIeHI5twcRKJSZEMuG7hmGFrDGKEjuB6kjM217BhNB0
THwsCp/dj7VO12JiYwhWn7ICS2PFac2PkqSrvk0yHHA4SXHtJVh3z7zwmyaTuMu2YBb5kNjhj8NS
ZjGaEocMju/SzJ7eTAcpFSWEED2LxMl++OpX76W19etY1MGT1F1cj3WzRMEyPDy3YTfrnSTThaOY
iO3Ccb8dmNgYQjKlOKZXYlQkQzLwryYcOzRsr8KEjSeJoLTlrGkQ1v3TFNZyRjjPTkwUgAmFKmA2
lsrxmCDZRZLGeRRLZX0Hi5jsBv4b+A1wDyY+4hychVgU6XrM1XZY+J5YB5MmKaaNgiWKlPYdPN5P
4aWXrtlvB8/BeqYcDnrzu4UQor8jcbIfrLskOqY+QjJz50ngYuDdmBAowsTAWcBjmAiIDq+xqDUK
j2JMVBRjIiRa0ee6ysa6kliHEgVHOSZiMiRmbnHAX+yiGRjOs4skdZTFinjLsDTTGJIZPtEXJaau
0lidy2osOkI471cxEZPFIh3HkQwKjJGaJzDPlGcwcdMWjo837Lhf7sTkvWf2xPk+F+D9vSxe/OO3
b/q5EYq6ujrGjJnO4sVj2Lhx5WGfkpxL9Gvpje8WRw5FxIToPSROOqH9ZNxcUfJjzLL9KSx6UIxF
UWK3zlzgnZg4qMEERvQ4cZhYiO3FJeF5MBYRqcTEwmCSmT11JFGYUixyUYYJoGiV7zARVEUypbiR
ZOaPw6IY5ZiJ202YCPjXsLY4FyiFRWEGYhGN6zEhsQUTZ6uxaEw8XyyWBZvfkw3rXI0JjijqPDYN
Ob6PgiYORYzn+SIwGvNoWQkspa1tNXffvZGhQ8dw7LGTGTjwdAYOPItjj/1rXnzx6m55pnSH3BvV
ofi1iPxGETEh8gOJk05oPxk3TTJ3ZzrwO6CYAQNK+fjHJ5GkWR4ncU712A24FbsJp7EISYyoxPk4
w8Lxb4btAzCBEdt/o5fKEJIWXofZye8I509hhbXRNj+FiZBqrE3ZY54nA8NnD2HiZRlWW+IwMfVL
LMpzXHj/NFbHMj2s7cGwljRJfczEsO814bvqSYRYFHWbsBbm00mGEp4Vrukr4TzTsULcReEaRsFy
OTCDlpbVbNvWRibzNTKZ39DYOITOzOCy2QkdeqZ09S/hzm5US5c+sZdfS+53y6+lr6KImBD5g8TJ
fmg/Gbf93J1U6lr+3//7W/7rv+7m5Zd/RnHxNkxQOOzGuxuLhsSoyE5MSOzChES8wddgQiF6osSO
m2JMnMT24G3hdTkWLanDilwrSCIuMdVTRSJ4SrH/zOnwXWeG49vCZ69hIqcuZ991WLt0GzYQcEc4
t8s591jgH4B3hMeQcJ1OCL8virofhzU/gnUzbcHM3n6ARZlGh/dXYwJqIsnAwdgFNBG4HatNiQW1
UQBF4jEXAJexefM2rrpq7ts+K7kC43Ofm0tdXd1+xUpnN6p77jmHrVub9vruXFy3/VqURuhdFBET
In+QONkPnU/GXfH2ZNxMJsMll1xBa+tRJG25zViUohGLJMRi1jhHJw7v202S8qnMeV+KRVRqsNRP
TOXEOpKB4buKSepKolNtOuy3BxNDsXX5+HDMj8Pxg7HISizedZgAmRjO+SwmKi4Ln0Wb/fj6DGy4
4FasxiTOHtqA+cLch4mFS0kKYdcCXw7f+00s+nNj2D4pXLd6YBpWWDyUpAvoQUwQxSnJr+T8N4k+
K7HjZyltbc9yzz1ncuqpf83ixeewceP9bNkyko0bX+eee75PdfUYiorGkk6P7rBtefbs2zq4UdXj
/a9pba3J+e5I8r+PoqLMQdvtK42QP+zrYJygiJgQRxaJk/1wMJNxZ89eyO9/fyJWx1GBRQh+iUUS
Yo0AkyYAACAASURBVEGow27Qg0gGAsb23ugnMgQTEw3YzTsWyoJFOgaSDBeM7cPx2F3h3HGGTknY
Piznsz+E84zCRE8mfNYS3leF9f4qnLssrLOR5ObsgfeSdPxE07gSTNScg0V4BmH1KmdjLco1WATm
Wkz0VIb9y4APYd4wsWV6PpYOOhMTZVGsFJG0HN+PdUg9FNbVWcfPszQ13UU2Ox4TSY+F63gP8ALe
r6G+/rfce+94zj77snZRlm9846d73ahyBdAILDWVG62JbrefYODAg/u/ldII+RMtal9j1hHdj4gJ
IbqOphJ3gY4m455yygVs3Aj2F/sHsBt1Bkuz7I5HYuJjJ5b2eI1kmjE5z1kS4dGERRZyTd8Gh33q
wuvWcGyM2MSum5h6IRwfC1CrSNxrB2A3/uOxNMxRWBTkmLDOozDxcjFWCPwG5oQ7IJzrk9hN/mhM
wPwa+BwW4TgX8zt5EvhR+P4Tw/u/JnGZPRMTGc2YW+xl4TesCedoxQTBJqz+5XZsIvIlYe0pYA7m
wbIy5zpuxVJOm4CXMMHzavjsw5iI2Zv/ZciQW6ip+SrZ7EVhLUtzPp+HCZOJ4TeksP++c0lEkRX+
FhVdza5dv+t0wnLkqqvmsXjxmBCdaU8qtZwrr3yKRYvm7/ccfZFMJsPs2Qt54IFVtLQMoKSkgalT
x7FgwawDXrPDif1/Ofd/R7l4Tj75Ql555WcHfT5N0hZ9FU0l7mPs/Q+N957m5kqS+of3Yxb2tdhf
6NHZdTB2w4+D/TIkHTbZsO8e7D9HGXaDLidJCcWOm/g++qRkMGHSgomZaJW/neQf2GaSgX3V4bki
fGcaq0s5Kpy3Imdtu8KxD5KIlVpMpOzChELsGKoJ63gwnH8jVtj6ACbWFoQ1Z7CiWbBISpzAvAO7
wUeX2xiFKsVEx2vh/UQsSnIsFpmpxGpXGmgvTN6PCaU/J2lX3hTO03HYHl5g584FQSjkGu5FYstz
LGQ+G+t2iu3UGUwE3Ulb2zsYMeIDnaZn4h8EhZhGyOdoUfsas/akUiuYNm38Ac+hNJ04EvTHoMLe
SJwcAs45SksbSYbhzcJqKSC5Ycf5O01YDcULmGdIczguRTIcsJKkrmMI9pd5ESYGYvSjLTx2k0RB
fPie0vBdsRalhcSddhAmAmKH0BthW1NY525MsMTpx3HScSqsIdbIpMPabwnPT4VzfAoTIrGOpQWL
KpRjKY8GrAsni0VFfkZyU/eY4NgTjl2Ws65suC7Hhf0fx1JDa7HozYthjXXY/KOzsUjKxSTtysXh
3LG2JpeYmrk/rCumaXZi7c/Rd2U3yayhBqyNfFLOOXJrXh4hk/nN2zfcurq6fW5aJ5/8N7z5Zox8
dYSjqan8oP4Ryt2ns4nQne1/pMnnotPOa8yWv11jtj/yWXiJvk+hCV+Jk0NkwoSzgNexGoQ0dpPz
2I1wBMlcm2EkRbFPk3iK5IqQWMTqsJtjChMAzWF7G0mEpAoTA0NIvFKymChoxURCcXiOUYvmsJ4a
TDREe/1GTJBEg7fy8Iiv68N3ggmpMkyUpML5Y1Hr4LBvG0mdSRoTCjvD9YiCKBYO14dr1RyO3x2u
0Q4s5VMc1rc7/L5aLJW0NJx/TljHB7BITRVJi/F7scLcDeHY3CJasCjLuWG/E2hvo/84Fh26KGwr
yzl2LIm/DJhQi11FSfFsNruGF19s4NhjpzB06Gjuvvt9oTD3TF591dHYuI19C2sjnvr61ztNC+T+
Q3XssRMpLT2NVOovKSk5j6Kid3HGGRPYunVrh/v35j9s+RwtOpgas/2Rz8JL9G0KUfhKnHST+I/9
97//IDZA70YsrVGFRQrqgW+FveNN2GORiUcxAVFG0v47MGefWDgbpxfHWpI9Yb+ysM9Qklk8O8K2
ozChsQO7sdeF/bLhuZ6kZiUW3xaRRAYaSaz0s1iKaASJGdzu8D2PhHUXYZGMOPk4dgy5sP9bmGBK
Y1GjDFZ0W0oSIYr+LEOwFFmMIlVg4mE4Fjn5SbgGb5L8T/ffsHRNCRYxqaZ9Ae9ckjTW6Vg0BJL0
zy1YkfDLWOQlDiVcGL5nDhYhKSEpgm3Galh8OM9S2nuuRNHzPuBJGhvPp6VlETZwMVcAlbDvhOfI
8vA9+7J161ZOPvncIHa+y7Ztr9DS8lW8v5xstpxs9jSeey7DCSeMY8OGDXnzD1t3ik6PRJQn9zvS
6TSLFs3nlVdWsnnzT3nllZUsWjT/oGph8ll4ib5NIQrfPilOnHM3OOeyzrk7euP7c/+xr68fhhVz
zsVC/RdhgwAbsBbb6MwaUyKxm6UcEwu7SbpzSrGbfaxZaQv7xU6e0rDv0ZhoiJGOKCyiH8lQ7CYO
JlByow6x42cHiQNtFErZ8IhrinN5XNg3CplYnzI4bH+IJDUEyRTmorDmXeHY1rDeEpKC4Oj1MgTz
QKkOj0HhejVhxbYvAleRdC3F9NaJmJDJYIIg1uHMwyIpx4RztWDRkS8D/5+9N4/zrKzu/N/fquq9
a+nqBZqGBk1EEAWjKLIpimwG0YRMEiaT1V9GYtCI4owraBQwijtZ1Jk4GTP5TRLRAQQEJMYFURGj
ouIYFQR6pbu6tt6quurOH+e8Obe6C3CDhqTv61Wvqvou9z73uc/znM/5nM85zz8QgGMFkRL9nLyW
NVbOztfnUaBjJwFYTs3Pv5hIyz6dEBW7YIzluS+hisndTOllBEBke95DABEN5HT+/14WLz5ojzDN
2NgYT3nKGQwNef4/yGt9iBAYH5d9upzp6QM4/PDTeOUr38wdd5z/My1su4ME//9JwMPMwoazXoU5
c7bOyvK8/OUX/lxB1I/DJHU6nR/7/vZl++w7Hs7j3yPwfcyBk06n8wzgDwl3fa8chWJPIwzhq4Bf
JYScNxIMyplEVdRNhEFdQNUt0RiPEwZ7mKptIjtxH/F4llIi0j7C0I8TxnYbBR4MAW3La8rGtHcm
3kGACUMlKwgg0QZKywhDPZLXXJzXX0yEZibyPKPZ7vvyntyEcEGeu58AQIIsM5gmCUZiHbUP0HZC
A7Mrr7uDqg1zE/DnBCiYl+eyQF1DCF2t8/L27JvTgCe0Xvdevpj98R6qUu8LCLZpdfbjJcTw+kuq
RH9bBPtqAix9Cfgvef7NlMG9LK+rHsV9hMaJcSEw6WR/fIxgko4imJ0TCRZuio0b72L16l/hcY97
Puee+1rOPfd1rFp1PEND7fOvAb5JCLH/igAnUesFrmN6+tn89V9fO2tGEDz4wra7AT/44JM46qhT
OeigZ9Pb+3R6ep5Mb+/zOPjg5/3YIaIHFp2OAr/Hpk2bWbr0GTNCYHfdBZdf/mWWLj121po0D3U0
TTMDFDwUkzRb4b6Hur8fF3j9tNk7+0DNY+f4eT+rf6/A9zEFTjqdzmKCpvj/qM1sHvGjUKxhl90R
7Tjh6VvnZCMFIg6hxJ7zCeO2gwIt1huZSxhSGZV5+b9hmQXE45tLARo3AtxBGNOxfM09dhbm9RZT
wtU5FKMzlwAEC6h9bzbmPQ7kb8MuCnqtKmvIaQ7BmAwRC/UYFTYyC2mCKpEvA7KL2vzQYnSD2Y7T
ifTinjzveLarlwqNDRPhsmkCLL49r70pz7WBABH/JfthOQFsFuTf27NfryaYrz+iKt3K8NxCMBTH
Ap/JZ7mMAFyfoorFCWqgitv9KgVS2qLb6wm9zjuIVOsT81qvYmrqW2k4P84HP/hZPvjBExgbW5rn
HyeyhfoI0PV1ZtZ6sfT/b1JZS7Mdsy9sMw14FLC7++61fPObf8i9985n69aLmZq6na1bP8Pdd3+a
P//zZ80IEc22UI6NjTExsZPu7ldkP8lwnURUVf51xsdfyK5ds4XArmdy8nY+9KETfqxQ1NjYGOee
+1r6+o5kzpyjmDPnBPr6jubcc1/Ha15zyQNS5N/5zkt5ylNe8FOFwH6WbJ8H6q9Hg05o3/HQx8P5
rH4ewPexCFweU+CEcKGvbprmn/ZWA2ai2IYwbLsPissII3gTEVaYRwlcp/O17VRBthVUmGOEErJa
4n6AMNSbKWFmX37Gv1fk70Wt84zmz2C+py5kYX53O2GcN+d3pvJ6Wwj2w7DNEio9uTe/vzS/25/3
vJja7NA6LWbL9FG7H1tefyNVC6Y3r7OMCmU1hLFeRGg43P3Z+7eE/7+2nsXc/Pzt1O7O9xLF4QxZ
nUqFgabzWlsJ4/hSQl/zGeAvmKkzsdidAABKJ3QQIc49Jftl94VkHhHOuY+ZWT2fJdi1VxKl+n+N
PfcXghDmXkQAlwni2Z6d3xlh5maLZh8dS4h0z5ilPbT+b3Lhm3kUO9hu16XAf8vznkCkTsd2AdPT
7+Lb317Gccf9yqwLtLtIf/jDJzE5+VUi1HU0oct5NvD+vGfv44EK6/3yQ4ai1q5dy8EHH8cHP/hZ
xsb+jKmpbzA1dTNjY7fywQ+ewH//71c9AEXe0DTfaKWU/2QhsJ802+fBDFqBw2c9IjqhR1rn81g9
ZsuGm6kBaz+rZ/3cntWPC3x3ZwgfCjA9mp/1Y6YIW6fT+U1CeXp00zSTnU7nM8C/NE3zqlk++7AU
YfOYWazpeQQIaQOU51NFwU4mjOYPCZBwKuFlb6I0JEMEcLC2yEKKdYEANQ21geAYAWDGCP3JaH6m
iwAGhnEWEMbTOimGEnqo1OOevO5cyoBr7N2T5z5KpCpAGSYM8XoCVMzJ8zRUXZcughHpIcDErvxu
FwFOvE9FrGPZXo8FFOiYoIrZraeKwanJGaKyohbmZwRcXwaeRGhDbiSyc+ZSTNFZRGrz1rynTQRo
eBtVJbfJtn2n1dbnEmGhmwjgcDRhsH+VAAeGXp5HiHl/iShc1xbPOn7eTIR2LiG0S51ZPvN6IgS0
iAA0L6AAyXKCVDybCPFcSIC0DjFtTiBAwGUEMFhEPMMJFi+eoL//wPuLob32tS/lsMPOYmzs1mzX
sQQTZUbXDQRgeVVe30KApxEC4he0Xns5c+bcxpw5c9m27a3Uxpi26Zep+UI+i6uZOYd2P6Y55JDT
uPPOG+9/xYJnY2NjHHLICQwNPRU4hz0L7tnOW/L/sd365Aetftv9aDj44FO4664HLsQ2NjbGG9/4
Lq666mYmJxcyZ842zjrreN72tlffL6ptmobx8XGOPfbsVng45lxX1/Uceug76Onp4lvfOr/VX3X8
vAr0tYvh7dw5j/Hxe4C5LF68knnztt9fGG/x4sX/rovJrV27ljPO+H2+/e01NM0Anc4wRxyxiuuu
+wi9vb053i5lto1Iu7qu5bzzvvJzeVYxXtrasdhK5dBD38lznnMM119/6/1FDU877Wg+97mv8n//
7wWzjq/dP797EcRHQxG2xwQ46XQ6BxK7xp3SNM3t+dpDgpNnP/vZ9Pf3z3jvnHPO4ZxzzvmZ2jOz
sudFhGfe1hi8mIj5+7cZHluIhf0EwqBuye9MUim9ywnjPUyFaqxVMp8AHftRYRgZiQlqH55DKD2K
LIiiVou5zSfAgoBjcbbFTQG7CQNP6zqGE+YQHrshKDUniwnQs5kAIRp0662syu9to8rjQ9V5cYfl
uRSrM0XpaeZQlVktHLcsP/+j/Owi4HF531uzHbcQGpTufB5/Txj392abf5HQwJit5Plldo4Afodg
Rz5LiWYPAF5I7Cu0kDD+VxEg4q2EtsWKtscSpfwFNzBzrJzUuj89pDECIP0zAZ6OJYDPjQTD0CFY
peOyb0/Oz9xCALLr8xztirqvJozvP+U9v5+Zi+oVzJ37OiYmHp/ffz4xZo8mium9LV+zWq5Hex6M
5Wc/nn3wAoJVEmyM5fdvz+/aB77+Tfas0DsTRHR338lLXnI6nU73jEW2r6+bb37T9PTZwM1rgc8T
rNw48RzbImXb0j7q2l1dO1i9ev6MxfyBKsG2X9+9Ku7o6J2MjV3KnuBjjHBgurKNPx1IeqijjN2r
mJ4+jgCb9sNMYLls2eNmgJW9WcX3kT7Wrl3L4x9/Ejt3vpcquNgA1zFv3iv5rd96IX/911/iwZ7V
IYecOgNI/7THbMD39NOP5rOfvXUPEBIVsv8DDzy+2gUk/w54P729P+CEE55BT08PIyMjfO5zn4O9
CE7uF4s9mn+I1VWhg5ZuuvVaZ7fPPw1obrvttubhOEZHR5sjjjil6eq6toGRBk5p4JoGphtoGjh5
t7/f1MCT8nO/08DfNnBwA/+zgWc38MQGDmrg6Q0c1sChDfxiA49v4JgGDsj3npDvPT5fe1b+flqe
7xcaWJWfe2IDBzbwzNb3npDfXZmfW5mvH9rAIfneoa2fg7Idz8jzeY3H5c/KfG91A/vn+97LIfn7
cfn+L+b1D2x97tA83+p8/Sn5nWfm+09s4PD87T3YN6vzc0/Kdh+S763Kax7awLH53eH83CH5/+Py
ep73kAb+MT/zpHz9mDzHE/OZ3Jv/TzdwYQMfa+BleS/vyrY8JV8/Ms/32mzbkxr4pTxn08CaBp7X
as9Uvn9dA8/Na6xp4KgGfjO//8YGTm1ivB2X52kaGG3g+LynZ+V3T25qDF6Y5315A//QxBi8Itv6
j/n+c/L6R+S1Ppnfn2rgrLzOEXntw5qZ43s0z3FEvjaa1/jdBq7Nz0y3zuP7p7buod3W3832PX23
a5yS9zHSavMTsq3Tresc28ALW9drt/E52d9vymucmt9vmj3b0sxy7bpOp3NFMzh4ZLN69XObVavO
ag455OTm5S+/sBkdHX2Q9aJ9jt2v48+FTawlZ83ynvdxctPVdfyDXnN6evpB17CXv/zCXL+85nWt
a/zXWfu2q+u65ogjTpn1eo+W46Hu+yc9jjzy1Hweuz+LpoFPNj09T3qAZ1U/q1ad9XNvl+eL53jd
LNd9sPF17azt7Oq6tnnFKy5qmqZpbrvttoZAOU9r9pLdf6xoTj4NPIXIlTwqf75K8NhHNU0gkkfq
mFms6WxWrpxDb+9r6e19BitXvpDe3o10OtbTOD6bPQH8NuHRvpAI43yU0KYsoRgBWZQJikGxXokV
XCcp0ekiKiwjAyJTIw2/JF/fXePRS2kzDLuYBSTbMkBpRwyDyGKY9my2kPqN+VSZ/EmCJerO93oI
lmGaCvksorKZzApSuLs477nJ++gQoZe5eW2ZnE5+rkNVhB3Kez6PytzpyXs+gRL5LiCSv7ZRDNJ4
6557CW9jO6FB+QzBCFxPMCSX5/01BEPQQ3jkEM//6DzPGJFdcwKhhVlBZOhY0+S0vJcr8u+LCWH1
0QTTYXn/dkG4S4gQyeezvWR/Hp/tu5mYOjcQTMWriLDRQkJX832CfXkrxca8gAh9XUc9+yUEa2OK
uKyNRex+IV9TK3IvMzOTthJj8Wyq0rH38Ayi/szNeS8XEGyVNWBMwVb/ciwzdSp6iw0xNrZROpu1
2d/PzLYeTIS9Xks8Y3e9voiZlYE9ZtO+jNI0f8XQ0KXcffdND6gHcVnas0ZFwwNXK76G2XVCM6sQ
T09/gbvuumHGNWerQvyKV1zE6Ojo/W1RKHz55f/QyuByawavcQ8xvtu6p4enpsbPY+n+WcWoD9aG
b397DcWK736cwa5d6gIf6BzTP1OW1gMdnm/2FOOG0h7ufljWYM/DzL1H2Jw+4PGYCOvMduxNzcnu
R9MUfds07Xjy+S1B4a8RxmY/QmPRRaSRXkQthjsJ3HUrMcAWEgYcSiRqtVj1JKsJQ3AAsRCvJDQi
SwhDt54KF6g3cbM9wcX2fG1T/r0foQkxDdhFvyfPJ6Y1nDQ3/++njL36lfbEtX7LAJXpNIfS3zSE
8V1HCXZ78mc831tCpVlbV2UlVYhNwfFw67o9rb8tLted/bErPz+fqiC7X37Hei32VUOBn35C13Ed
ET44nZj43tv/IMIsqwiwcWyeZ5AwAkcSi/+bs4/3J4DrCYRxWEQUrTuKoIxfQIVTbsnfR+Y1vpP9
8wzgDgIgfZwgHHdQmz4uzLY+ndIQPRH4DWIBvjDb8DHCWG3M67yYANGXAy8jnu+XCGN/af5+DpF1
dAoBhF5EaEc8LiJCb79B6Nqfnuc+Pj+7jaoM7DlfRIiNbyOA1espncrziDDZJdT8WUg891/Pa70o
r/t2StsCEQZ7FvBBasPJ87OPDfX8CTPDUeuozSR3Ah9gNj1Ip3MFRx75IUZGpu4PNW3atIXx8a8y
sxaOYa32a79KhfUuYma4+KJWf7U1MluBVfzBHyzly1/+Ft/5zrk0zdcJbZJlB+bT1dXPwoXb6e7e
yciIYvrrmRlavIgYb2290u7Hzx6mmG3jxzPPPI5LLnnNTxwymhmemqmtOPzwdz9gZd8H23wS4A1v
eCdXXvkF7r57BwHadz9cC44gnM0TqfHQDkF2s3jxJn7/98/8qUJibdsy23sHHfRi1qzZPQwJs2u2
GkrTtfsRbe7u/gT77/84pqfXsW7drbBv47+f6njUoKr24Ol0Og/ArFxOT88cYrF4FWX0byIMx3LC
UH6XABp9xOPpIQyne+jMzc8P5Ptb8v9hqqaJKceb8pw7CSMlyFCPYRbKAsJjXECJXRXRNvn9sfye
gGlunnMZBTjUyZglpBh3R/5WQ7Kl9TPUuk5vthkqm2knYbjsOwGU2U1Ww+3Oz1h2v6G2AviFPI+M
kWzQZOveraRL6zpTlAbIZ/FnlJbmKGJR7yeAxHA+23XEYmV9G7OVdhHAqp/QVfwtVQFX0ORWAmYC
LaL2X3o1seg9ntj48LmUDuhMAvx8ijBgN2Y7N1Bsmhs7zs3vXEgYW4vPXZP3/CYCmFyU75+f5zg9
23MAsbHiYgosyDhoMAV6Hq8myM4jCbbm1UT69Kn5940EoGjXcOkigMbjsr1XZ3+9Mp/Xiwk9zqUE
SNye5/8FwjC8Ic/xgvz8VPbNTRQ7cXHe3y9TlYEnsg+enM9jHaEJ+kMCLK1kNvFjMCof5BvfeEUr
a+MKxsdlNcl+/hUi8tzOvrgs+8F14aUEQLLA4TUEqGpne12Zv3+Tj3zkE3znOy+laf6KAJybibl6
OfAtpqe/yPj4aYyMKNp2PZHVarLP/oUA1A/s6U9OLrw/a0UKfve/H+jYM0X9p69j0zTNT1w5tWma
+zPHdk8Xv/zyo1i9+pn09x/FBz5wDHfffRO14zvMZNjOJBjJbcS4fRsxBmUHn4Up8OPjX53BcP04
fSQTdOCBL9qDCfL9xz/+FNav/yGzm8Lj2bP69Dh7zktmtHlq6husWXMl69b9xYO28ZE4HrPMyYMd
jzRz8lCH6DeyfLYQi/SbiUH9XWIBlQ2AMKBmsqwjskzWEXS+oGWYmBjTxIK5lvD47yGo63uIyTqH
mbVIDM30UHVLllCgBmISWuzMzBtZF3cndkO9NmgSNCjMNdsGAjy4fxCUeHVHnmslAQgM0YxRZfPH
qBBMLzHJllAbIsqqLMrvr80+3JnnXZD911CgZjLbPJB9b6hkZ57DrClB2EC25VuEcXCDxnupMv4N
wWo8mTBmX8vzXkUsVgLN+VRW1TICQBxEGN3X5HOdT3j+HycEzncThvRd+fmjiMySXQSL8OXsx0FC
vPtGIpz4HeBwIlusi/CcPp5t/xQhmrshX9+R7f57Ajj8RbbFCsLXEQDF8Xpo3us/Zbs/lM/qlGzv
WcQ+Utdm3xiiW0oY6A/ms7sl23MYYVj14mUOjs7fX6RCNR3CwP9HIgvqJGJszstn/VaCVVmQ93l2
tu0f855vIUJI1xI1YtYRgONiKtuoIQBBL/CfgQ8ToOzDlGi27SUP5XXbjMpFBBP1rbzXF+Xzu4US
oR6fz7CdHXULxaL+IwFIj2VPIbLHcYTRfCpRDHK2bKWnE/PGTS7NMHldtuHD1Gakba/be/wsOh3d
3d1MTcmaxp5enc7CZGh28h//4ym84x2vo6+v7/6rN03DH/3R6/ngB80cO5uZGV8NcA1HHPH++xmP
3ZmDNuMxMbGQDRt+yNTUbCxPrDsHH3wKt9/+CV7zmov5u7+7lm3bYGpqFyFubz8nhePriDl2IjEW
/o4obvjU7Ks3EOv3FUTK/1Oz378MvDv79oGEzufR2/tt+vpWzZohAzA6Osoxx7yY7373ICIELNg/
kMMOu5ubbvpbTj75P/Hd764mdn9fm9c9s3Xfrp+n0um8gab55byvMwim57eYmbm3mQBXz857vpZY
v78P+7J1fr7How2cQEzMAw98EWvXNoQHOEYsvvMIb+9zhFf+HqqkPFTF1QMJYzSPMJ7W6XBDwXYl
VA93FF7ITEBjVgyUZ96f15VeN6VYg2fFVrUqZtXcm+eZRxg3i8p5uMNxNwEUtlDe+3Jiwfaa7tzc
TXnR/cTEOoCYeOvzb6vsbmm1cQO1UaHaESimY3Heg+1aTqVxq+kZJYDJ/Px/Q95bd/5/C2HsyXP2
5LnMPHouYbgsx7973yyiDEB/tkdQZTu3UDHjMcLYvJdYRBYQ4Y2Ls682EoDr7YQh/AqxyG7Nvjos
72dT9vN+1GaLbiB5cvb39wkgcANhwH+Q53pztvUUQv61Pe93bd7/NBHmuYhYnA8gDPJzso8vIDQ9
/5j9+HwitfpPiUq8XyLG7hnZ7zcRYOOfsw+eTBUVfDIB+jrEmPkqYYBfQRiROwkm6hPZ9iGCYXkq
wYZYCO/bhO7ks9nm5xDGZndG5LTsm9V5/euJZ/xVKgR0LgFwPs6eoZqTiLF6ed7nXcR4viHfvyT7
yuwomZVtBKj6VYJFeQsR+pstA6khQgs7qArBi/L3ODFWrsn+WkGAuqOyv87PtnyJcjja2Vga7ZUE
ULqYeGbbief65/n3hdS+VO8EPk1PT4f99+9mcHA+w8O7mJxcwLp1PyBCj2/e7RrtUNUGli7dzqJF
S5ma6p2R4l6GWadgc34P9gRR4WB0d29mampFtrENBNv9aNjxXwkQ/mvEOD4+73kBATw/RIz93yGM
uaD+FmI+uH1J+9xqedrZUFPA9RxxxHu5/vqP8Gd/9iGuvPKzrFlzL1NTy7M9bdB2PfAWDj98sH6o
pwAAIABJREFUHnfcsY3IPryVcELeSQD0tbRDfU94wp2cfPLxfPKTX+Deew39n0Bo5rpb/XFcnv90
Yj24MMfJ0bAvrPNv/+h0Osyda5qqXuTjiQmkxuDXCEO2LH8b0pikYt1qR3ZQqa8NMSB3UUYSSgi7
mVggu6kwgwXLJrJNw1R5+2mqCNx2CggpJl1HhT6sQDvR+o41Saw+200M9rXZJg36SL6vGHYqX/P1
ybyG+/lsyPvalP0wlNdcQu0VZAhJL30rJQJuV961Iu9kXq/J/5fkZ1ZQqd4DeV6BlSErtTyGT0ao
3ak3U2GlJZQ4eJjSHA1T2xfMp6rYKp5dkH//DQXg/P/g/MwkMVa+lW39dD6fSeL5Kur9Q2psPIfa
kkD6+S4CpFyX9/tFgnURCPTm555PPN91FDPVS4zdjQTgaIhF/HiCUflLovR/d967xvOjVDG9/0AV
IPwoNb4VuhpKvD0/cyAlAl9DeLo/yPMvyPOpSbqJAG1HEWDtlwjv8Ct5bfdZmk34uDWv8dJsx6/l
da8jDOHvEobkTmZuOqmGxArE7yFAwBpqu4PePNf7KQZyjErh/9V8TrcTgKK9E3b7WEcY1QWEoZ5H
gbAXEcb6ouzfO/Mzv0J4/5/Le7me2oPL8OEnCY/aEOv7iHG2mjBg38y/L8q+M5x5DPApdu06kXvv
Xc83v/kn3H33Taxb92Ri3HbYU4RrqOpvgV42b95TbHzEEafw3e9uJ6oeG9aSnfU8R2WfXpL9djJT
U8dnG0/IzyydpR9vJtbhZQRz8iqCbfx7Qkw9mPf7KgLYviD76GBiLq8hxvvi3c49SoyZP8m2nZTf
ORx4Nd/+9g858MAT+MAHnszdd89lamouBfQqTBXnPpQ77riTCmFfSmjbFhFaLvvk40DDnXcOceWV
32LDhnUEOF5G6LeeR6USX0Y4LC8gxpjPcu/XtdkHTh7B44UvPJ5YVK+ngMUyYnCZaXIMscj/PVUa
3SJmZ1L1QFyYzerZSTEADcUquNmfYZbFlLEczO9bS0Q9Sz+xsI0RBtGNAGVt+vJ7XtPzLMxrzqFA
kLsuj1JgY17r/tVgmIWyg9rvZzDvfQEFnBbl/blB4Wh+fle2RSHxMDPrtAxQ4ZKBfN3wlqXyBQoy
RROt18xkegm1SeKC/HsXtRnhAqrsvRlL7jVk+7bkcxaEbSW8SQEdVHG+JcSiKZO1kDACO/L5mFH1
hfzMf83/3T36+Gz/B/LehwnPqTff/1R+byfhCQsEp7P9N+bndma7XkoB0P0pHc1LCfbgB3mOz2e7
byY8xhPzPJuzbSspUHEesejvl9d+K7VD979k/0EACLKfpykdyQDBLBydfXZPtmcDQWNP531sJED+
OmJx3k6FNgeZCSzOJ7Quk/naN/J5vTR//xFh3C8l5sxvMTOL6s1EmG6Y2qF8mnIIPk4YgivyGd1H
MChnECG1USKUtIB4tpdnf+3OdJsx9fTs+4XUlg3vpMDDbXndNsjpJcabgEFnyG0gPpY/FxKsgqLv
u7PN1+Trggw3vHTrAasKf4ViFH12MoNmQx1PsSkWGJQ5vIjp6csYHt5BjNF/ppI212Y7LiEAwK35
+3TiOV9J1QL6lTy3QNDDNUNm9eZsx0ZiHGwmxscX83UByM0Eg3Miwc7Np8D2RQQQeUb+/1QCHK0h
wM+BhGZlAnVB0bZu9gzbCbx+I5+XWrFvUM/XzCpB8W+wa9ftrFt3NZOTbmBqfauvUkD8i5SjsoY9
t2LZe8c+cPIIHhdffAGHHXY3sZBeS0zIHcSCoGC1Qyyy3ycmyqFUlse7iQX1ccTkXkwAmAnCG1Bn
oeh0PM+hmHMztameIYwuyuBDaTx25LUECBpYmRDR+zBhEDRqak48/yRlgOdROyjLKrQZkIG8D1kM
C7315znVx3S1vj+ebR0kFuWlxGQTtNkeWRDDKjJBu/L8Vrzdkf20hRKqtivRfpUwGO6avCi/vzTv
dZRKa7Z0f1sg7HO+Md9bRx0yGw2xeJkOLfvSUBlPgqgFFPMzQdC8o5RA+Q+pDSefR+1htJow4r3U
Jo72dRfwPWr/p81UBePfp4DXALGAzyVi7r3EYncClY5+LbEwPyOfz6r8/IZsP4ThPI5YHBU5zwP+
O+H5z8tn8INWf/9i9s8NxPO+ljCEMi63UmyUe0gJkv84n8UQpaNSkzRGsENXEOCL7O/PEWPpvdmW
/antKKTBf0CwEBrMEyhDfH5eU5HzawngtIwwrHMIlmkhZThup8TdfUTopp3mvJYwgHMJsHc0ARbm
EuPxRsJ4HkeEkpewJ8j5IjFu35H9dhEBDi8APpJtPY0YW1BFIc/O52LJgctabTf1+y6CNWuncbdT
1BsCxB5HPOfv57lN7z6fACBPIUDVHCKM9Fkie2z/PMcrCF3XiXmfft8dw+cQ4EEgtznb4KFR30qA
j25ire3k/SzO786htEvTeb/zCPAlgHlm9texBCv5LmIc/gEBvt9PrCEj+b3ebO/nCXswWwqwwOuo
vN5xxDj/IiVob3+2LfB+U16jQ8gH/rV1DcG926g82OaCj/yxD5w8QkfTNPT29vKVr1zJueeeRG/v
a+l0/oEY9KsIuvlaYlG9nKBQtxKD73CqNPx0vqZx3EoIJseJhWqSqm4KJXJdRG2SB7EwQ2kdxogB
qrATYjJpHAU11v8wxbe9od9ktmsJFSZanm23tL4MwCCVdbSLYnkUvRoG2ZDvCcI25Xem85ym9qo9
MetoIbXRod6vQMEQiWGZvjyH97eNWNzdc8hNFkcoNqQv39f4jVHgS+9JUGTac1tbM4/S7lgXxmq6
A4RRUTA8STEJO6lwlBs87sh2zCEMwzjFJp2X31lC1NmBKu/vhoxulfB32V5FwYb7dhHjdBvh3Z2a
bfsetU/TddS+Sp08/0biGT8vz3kM4f0NUGPxVgIovYUaN/15r24f0CEW5mkKDGtc3pLt6gX+E6Xf
uYoYY3+V1x6hnv1X8rVBYu5Zu+dThFG+N18n27KNYgQNM76cEok/njB+7yKM/HPznt6e7bmPMEhH
EwZ1A2FE3p9/X01oaZZRS/JigjHpzn5s8ppvyHs6ijCAb8h7v54AZ+q5vkwZnrPzfGYBnkaJlK3o
7HZlv0KMfSv9qklzvdhGjAXTtQVP/0zNx8/nNYYJQ/lsSmT55XxmW4H/mee7JH8LgscJ43pl9ueH
s5862a/nEeHDVxKhx1/P53UxZYgvo8KaPyDWsj5qn6r3Utk1r8zPrCC0HD/Kvjcjcisxx75HMGbb
s7+3EQD/1dTeYLcTDsLpRIj12QTwXUOxS1dTFbwdZ00+v3YJBPKanyAAzO/nPbydys50PfW4MT8r
EDuScl6+RjHzZrttJoDtOh68Xssjf+wDJw/jMVtxoDe84TLe8Y7XMzr6Tc4779fpdN5DCbH+lBJe
fpxYXI6maNqXEwvHQRSzsJPwUOYRk8F0UQ30EmKSSV0LRnZQ4SF/b6Fqm1iivoswhBPEoqGI0poj
7RL205Q2o0OxDm6wJ+sie7GIMhjdVChJ4CVNqu5F/Ygp0mT7Bij07/+LqU0LrS3SR6Ulb873prO9
plwbrx/Je1nYas8OahPHLdknPdQCNkDVfnGim/W0K1+THVlMGC1rpgxSRfVGW8/CEJIe9648pwX5
hvJ/+xCKOt9FCPUWZZ+9MNs6Rol5d+ZPQyzahvAWUMJrGZIFxOJ6Qp5vcV5XxmwHscjfmtfxHncQ
i/DrCcAxQu2kPUl4zNe0+n9z9uE8Sth8b7bLMWZIYh3F7qzIvovshuibP6ZqBO3I/lccOpcwGscS
hsWU5HmEx+kWD9tbPwLnv8nr9RLG8aA8zz15rXsotuIDeb0PUBlcX8w2PyXvaU22b5xgkmQ5T8w2
fJQyUG/P+1pAsEsbCeP7a8T6IDs5Shi3l1LzZ5QYE+flOb9LADJDtBDjRf3ICLUB/PWE1z6XcKDm
5jO5Ns9P3osauB0Ea/ZMYjysI+rkLCJ0I2/K732SMPDfIcbk2wgwspLSeSguvzf7/r1UqOLG7K9r
8jqjBLDpItiIbkInMkaEYp5PsFZ/nP1/HQEobs5rN9R6ZMYWxFi8Nfv4Iiqsegbl+Jj1pXNyGcUe
2787KTZ4c55nHTUur8nX/pjSqHQIwDFBsIU7iee+npmstyUXTiWA6+WUoHZDvraWEHHrDN1NPOcV
VO2tc9nbxz5w8jAdM/P5Z99V9Oqrv0jTnEI8hicQg+VHlFhuOTG47iO8gi9R1JuAYZoYkNuo1NSt
xODvo+qJKDR1R955VPXWBZSGRMqyK9ujKBFKc+I5x1qf1wszDdl2uVC29Seb8nND+T2Nh8bXMIMg
Q93LBFV3xD2AGqronPoVQyhS93r0Q9lG8pqjFGNh0TjDBt3U4jtC6W82U0Xh7I+F2TazrAQ4AhK1
IhpRdSlS5falWh2Fu4qY5+azUvQrE6Agdi5VaM49jiZar7eBgM91mmKhfP7k/W6mPNApatHrJzzK
l+T/++XntrU+b4hwPuUVGgb7dcJ730EsxocSokOzfywYZ0jIdHHHTpuls90nUiHGb1KM2frsJxd0
Ad4oJfh2cX5ifg4q1fuEbKP6gg7FDloo0PR86/38NmHITBnvzedxfP5tGYABwqAPEvO9jwJCIwR7
IZv4meyTNxIMw4cpkDdIgKD5hPFem5/933kdnQf3EVoH/F6e93WExmMBEXpxzo0RYPG0vOZ2AlA0
RKjjSIqtE8C+L/v6ZMIIbszv9hIZXo7dpQSD9Pt5roPyOU/l64vyHFcSc0idx6n5TPuoXcplds6i
HKspAgg9n3re51Og1kKPZ2Y7j8rn1iGM8rvyHBfkcwH4XwR42UWwNp8mRLvrqb3JFLffTdUnMvzz
OSrkLSsylxofEwRQdIxuJpzUkwlwK/M73OpPw7xr8r1PZZ8ck8/xwjzXbQSw6SPGi0D6XQSDdXi+
Liv4L8S4OIYYE3v32AdOHqbjoYoDveENlzE5uYgYKP+FmATfJgbPpyjdQR+xwJxFiVwX5f+7KA3B
IFXSfn5+bjMxUQQeLqyDhJGfpBgF02FlVJzQZgbJRAiOpiiDbR0Qs4FMkdVg7qTCLhqVuZQAT2Oq
gbMy7CYqG2dnXkvmY39qYVB3MUWxL5PUAgWxCEnDa+RsjwtFQ4UWuvI7AigNqNkBhsvcaXkx5WVr
iBZQbIbGrV0MTlGzYMqCcjtb5+qj2CaN41xKxyJzQ97LJJURJWNmqMv0aDeA9DwyWgqHoVg5Q0vd
+Qx/M+99kGBJtuR7myjx7115nR9Q7JUZaYMUcP0epSUapergyD4NZxu2tn43hJEzBHgvJQBXFL2S
SplfQNX02Z/ajsCw4zKCidhBGBx1VRdnP2ygWDr7V03PRmKOLsn2rCUMu203xf89FNMpABFkrSee
/feobRo0+gLmbsKQn5Df/wBh3DdRAHon4flOEWmugqzVBDOxP+EN/0v21cfyPGaaWM353DxXh2Ld
vpbn+e38ziZqLuwitCmG1f4o7/+q/JwA0LnwaSLDRA1XNzF3Pp59albUAgK4Lso+uoNyhgayfRdT
uiwzwb5GGfuGyNTaQgnuv5/newshKO0hxtPa/H8BAe6elP1xQX5+CeWQ/B0Bil+b11lDieq3EELk
38u2bszzr8o2XJHPeRPlgN1KbU2xkAiDWq5gaT6jl+W5z6OY2wOIdfydRPjI7UmuJsa1miPDqjpG
p2T/30MAOdfsnny+ipH37rEPnDxMx+x7HsQxPX06V1/9RebMURne/txrCMByDbUHyQAl0OoiBtW5
lJfeEAtAPzHoyPc0gBqedmhkmBK6SrMPEQucab6CjC5i4uhVLyUmhenD7v2jANQYpz/qRaapDBUp
cZkHBa0yGwKvNvPhdfrzswKA/rwnBYqGNNo1W1xYFlEaCz2VboJ1MZvFhW0oz6F+x88qxjW7RkGv
GVFjVNhDgy/wsYidGU+Goiaocv7zWz+GxQYoseoOSvMz3eov6XfFeRoRQ0eLiUVN8bHxfYGdAt22
LkZvFQrcmRUmgGrXcRFIbWk9KwFMP2FwFEx3Ux6y2hrHw2IKEFpkb4ryIhfkdVzgNVBDRLrsfCqs
1CFYnjXUlg1jFMiB8mbH8rWr8v7WUJWTNxNjeTnlOX8z22DWlK/bZxsI5gLC8Jql1kel/yqUVoDs
uPD5asjfmq9PErqZidb5zDqbJDRoi6nw5Jy8P8NLSwhj/FRKE6Wo/Jbsl4VE+EAN1OVESGBDXmuI
MLwjRDE9CMP51lZ/mlk4n9KFzSPA62De9xSVPr+F0OH05rmPzs+eRDkI+1P6u08SoSHH7li272+I
sbaSYAIm8zs6PV353BZknzknvpDnWUuFfRcQoNAw6DCxZn+bYLEOI7JjdE66CUD0YSoEO0oIee8k
wldWgVZnY1HGkezrrxJrfLvStxqiN+Tz1EGbJPRK04QAdyr72HILhm1lZrsJ+2L4/rJ8FgLS2Qr8
7Z1jHzh5GI6maZIVeSD02WFyciFnnqkyfPfPTQP/PzGYr6cmxPOpxfXFhDdzEDG4NGSm9bYN0jQ1
aGUeRilDrSe4gAIZu/JcetoWBzNN1xCNXomq/bG8di+lSxmm0ofVO6ivmEexAKbjymwYrtpOiTpl
GgRVLsBQ2SzqCbqIhVavcAmxGFgDZZqqsiuQMyQ2QHkzhnvM/tFoL81zdVFCSSvKmjJMXtMMmzGK
SfLee4iFlPycxtsF3O+6KMvCqGfxOY9RGh0FoKOt7+u5D+Xfm3brg03MZHbIz6pvsY88r+JTqArB
6lAEgwKBHkLfoG5HXdIAVb9Gj3lBPiv1J0+h2J/JfEZrqUJbgkjDDQfndxdSAt1dlHBYI7WRAkUa
XEOUZr2pexnKz2qQtzFTw+Xr8ygQvJIwMl35c2vep8LeBfm/4TDDTYYBevP9QQI0XksZzU9R2U5n
ZPvJa38n+/d7VP2VIarGz3fz3L9D7bFktedFee8+XzVKf03Q/TJuMlxPpbbgWEOkxA5SYlKrTI9T
YEhm924q40XR95XU3HhJtvu9+b5hoTGijs40EZrptJ7PADU27iWcuqUUc0x+xoJvA8Qaavq/guyN
1Fp5O5U0YJh2gnAQ72w9E0HlLqqI5EC+/hYC1C4gmAmZMcea680QNW5ljOdln/0CMYZcn7Zkez5N
1TpaltedpETMN1CJCkMECNtOzIWb8rXJ/N44+zQn/4aPTqeTrMgDKZ9HGR29k6uu+jylMfG4jAjz
/CKBcC8jBmA3wao0VK2S5YTR0BipZp9L1eroJTwpWRZj0S6EhkbWE5N4nFrITVedR9VDEfy4wCuQ
VVTp+ZcQk1nPVY2IQGFbvm/sX/raiWiNEb0uU16d7FOUwM+Fx/sxfNVLFfaSajcsMEyxFoqG9eY3
tb7neQRyhkqGKfGldU7M6plLeUZ6kJuo9GyozIax1u/5FGVrqMd6HjspT1m2yMPQjO1rZw1tp2qL
KKrVm9pOsRTzqZDUcPaF2USbKa/OzC3HoaG7hYTeQiOhIHZH9s3GvJcVFFgm73WS0ibpQcq+CWR2
UmNEIwsF0uZT9XG+nm1WO9NPpLDKjvisJqiwWx/FsinG1dNUGC6QF0xsIeaDGU8bKVA5QhjrHmKO
K1iW7bNgoloIgYbMxAQxJ9uGty04N724n8g2MbVVoOr8WkBldw0Q41ANiEySBRkNsWqE22vBJwnD
aGhLb19tlXqvT1OOjOFbGaGD8tyyYnPy76XZjqcTa1p39s3vUfuOLczrLM1z/im1D5P3IMBUpD9F
AAFBhgJz2Vt1Npdke9bnbwG5jscqao3uIUBVQ4wzx7drbU+ep4fS/HWIcNowMf5/nWCE1LcJ1pa0
2vEjatzbZ/cRZSScH5uorB8z3HTQdO6Oz3aPUCFqgd5OSrD+5jzf2YSwe5/m5N/s8cIXHk9X1/Wz
vDMGnMbY2Nu5++7PEOK3du0CwzxWcTyGmIgi8RsoYah1TGQbnkygZ/+XznwnNXkNccyhFpQ+YgJt
puqeWG1VpsG4+yZKRAuVKuzk9zuGR1yQ9WplNeZk22U6ZGxc+A1d9FPegIXYBvM7Fo7S4zN1WJGr
tOj2PMd2aiFQcCid3BboKniVudAQTbQ+p15GQaSF9BoqBDNNGSCLtRkWggp1wUzdjgJga8PIPKiD
GaDKdxseMg1zmBL5KTQ2XXkFVdtjgqproqEUqMj6mBVlWMvwxbLsZ5kh06I/S4hc1RGo45E1U1ui
QZJx0wjoDdqneqKbKL2RYNXwhmFH9VKTFBNgGHAs2zaVbRNQWfG4Q+1tNZHnEZx5DZ9LFwFCBvN7
GmGLEJrqDCVOVv9kHw5Sm3YqbtxMVfs1WwQqlVlDtoiqu7Mm7+99eQ5TRA0VGEqTPVOjIssqmJaV
kh2QNdPITWfbuvN7ZrAtJMCIjJd9uIsaX4rie4lQlNk081rX2EyxFmspgCxI+Y28DzVZPVQGmiJX
Qblz1PnkGqlD4ji6h5rbf0Q5ExZ3VN9C6/nNocZyHyF2NZS6Iv9eQ61RssSuV6aV/w4FCDdQOrMR
Ii19HaE5cWzrfG4jWC8o8bjCeR0KWXOdLeeb69V0tmEnlbq+kAAl+xFAt62T3HvHPnDyMB0XX3wB
hx/+brq6rqNQd0PEZd9IiY5eTywu11HhAyjh6a2E0OyXCRCzkhBCOakPIAZZA/xfShA7RRnkc6kd
dw3R6GkP5d+yJqLwbiojSAraKql+Z4DysPoo4aIiXI2U8fRuAsy0PUbDNWZ0KMad1zq/2UbteigW
6pokYq8yRS4MshVmugiC1G3I+syjwJyiVOuxjFAM0gSxAMlILKN0MQI+BbxD1KKg0TEl1meszkdm
ahmxaCzM88tuyFa46I9SAGOA8uq3UiG8EcqTnkMV0lOk3J33okEj27mcqvWiAZxPgaUxZjIrpr6a
vaXXpkZDZkFDZh9spPZ5Erwq3NXA6A17LRdSsyE2UOyP4uk5VHjDDBvBhbodGcM2C9NPsXpmUygo
l6VRdGuKvmBaj9dKs6PZL7I5gngzutQGyYJ1Wn1BtqU/ryVDN5caUy7ZMpLjhD5NkLSd0kRp/ARU
1sUxi2cDe2aRCSqXU+uWwEpGTqGr8+s+KjSnw+N4sTbTfVTIwurFFg4UvKjvkq0yDKFeZZR4nmad
mTmo3sTzqj8bI0IUhv7UmM2h9uEyjdaxIHtnxpgMZT8BPGTKHPPzKQDZBgYCz14qVVjwoONkKNjx
PZHt6idYGbPeTNN3/Bh2NzHB7UBG87n5TIaIbC+divmtdgqGZBbH8zsWANz7xz5w8jAdvb293HLL
FZx33pc55JBTWbXqRRxyyKn09rovw/2fJBTcXyYYk+/n6y6ogpQ3E6r/a6i47wVE/HAtgXoVjJn1
MkLRtE7iJRQlr5c4RBkuKG/AuL1eyACVJqmGYSdl0KFCBIYY+qn9aPqJCaB3tpQSM6pfsfjZUmKi
KoRzUgk29Mo1PgreNN4Cj0FqDxNj/ZOUhkJdjPeuAVLY2snvKWS1eJdMCpQwTcrd8M0SyuvV+5fu
hWIFBvJzW1t9bwq1i70Azvd9z/odPidDJApC9YYbalEUTLWFxltb/WZIxoVrCQVShpmpmbEtiqPX
U8/U8IDF2BTeykzpmcr6+FzUYdl/o3kOgZEgZxEx7g3FTFExf6jsHRm4jVR6st9f2vq/ab2uONc5
4z0ZthnLthl2MitpDgXiN+VPhxJH+zz8XC+131ZDaamGqf1xrGMjOJzf6nvDbM5RwRVUUUUZElm4
LVRtoL7W3wOEER2hgLqMheEo540hyzZwgTKM1siRMZXd83y2YQlhmEcpEbkA6z7KqRGYKMpWYG6o
zRIGhhwtmXAV5YgYEpId1qi7JnZT4VbBqsBCALM+73OSSqGX8VGbNZT3a+acdaQUzsv8KVR2PC1t
XddMOcONMoFz89yG1HRgFlMg13nse4I+Ga6l2beG90YIxqSfRwNj4rEPnDyMR29vL+9735u5884b
ueee/8MPf3gDfX2r2HMA9BLg40YWLpxHV9eniFjhDcys2jdNpABaJ+Rb1C6jevQXUl7EUyl9Slsk
6WIgTangVL1G22MYIIxvW1DpBFFkarxfmlRGYCNlxMwAMCVUylUNhupxxa6bqZoZLshdVBhCr02j
p6flAtZFZayoE1Fg5nUEGQIDNSr3URkX0qq2S4ZGWlaPf5CiT/3eOspganAHKVq77RUqvvS8Mg4q
813oPWSV/N5SirlyuwNDDNLeMlkyRdOUONg6LVLm/fkMNlFp4IIYQ36GOvSUXXxHWs9VwDREZW+0
tUWOP0XTGiPZLrUpCnVlUmT4xinxJVSoTnbMzKV1+X473Hhf3h9UKAJKO2BIRC9ZkLyJAlkaTpkv
U2aly+fl58YocL2w9QxGKTCs0d+a7dhIGTDDUD5Pw7GKhM1iMpzSHqeyDLKYjouF2ccCBdkXw63q
XbzHzXkfMpMyRoqGBZTtcaaIfhElLHaeer5Rav0yNGmoWUG7zK1aoz4qfKWxnkOtY71UtgzUeiTz
odh4AQWOyWvp+EClQpvNZIhvkBIuy1oKKmU3nFNQxRS3tfra0MtGqqryIJV6DRVWN3SpYyrQUEOj
hsewkmHu+yhGaJIYp67JbvWwk0i8UOf16Dj2gZNH6Oh0OnQ6Hbq79WJnOxoGBxdz+OHvodM5klCa
ryKU+Qpl/wfBlnQRoaCL8j3FnmdQFN5/oxYfQyiGYbYRA9XUzTab0EXthiydqlHSa9Yz35rfs6bE
ELXAaMz0rPUG51OCT0uHj1Abci2iFipFm1DeQU+r3Yp826JcVfHrqUqPmynjKw27lgpNmBrcrumi
bqeXiu9aB0bDasbGGLF46IlqfBW5Dub5zXTRQ/SaWylQIKuh0dtIGTLDZ96L4EVDrjHUmC5qXdfn
oyemqFiPVo/O0JTpzVLtHWYWsdOzu48SRhreUUhsP+jVClqs6CtoMpynNzpJbU3gmGglRSf2AAAg
AElEQVQbUcNGMg2m1E5Q2h9riUifq+eACme0Qdq81nWWULVUdBDMSFIE7vPV6G6n9CTqeDSyZi8J
LHZR88P5oyfssjyP0l3oOe/I98zUMEy5iDK6Y1R4TkOrsLmdIWKIbAelj5ChU+w8TjFVAgEBn4BS
RtRn433LmupEOJ+HqH2sDEEuz3OupUoXGPKy9AAUANJZcK1QByM4M6yixsjUWsNXsnm91NpkOFvt
nWEnGTiBggxUmzVyHJsxqRjYMen8smhkm1lzfPVQmYeGc12DbXs3Bd7XE/PIsa9IehEVdt+RfS1D
KqsiQ2lWpqHLtv5x7x77wMkjfAwMzGHmplPt41qWLl3ILbdcwctffjurV0+ycOHXiTLGN1L1UPoo
6vZ0os7Auyjv5VSqMJhpbx1iIC+nBqyppDILGr+2YE5kbfqsoR6oWP0mYsGQNjX+b8xdI7Kj9Tmz
YVzgoTxKqV4XMb3pfsr7XEqxCVK07VizuhU1MAuostEaq4YIC/i6GSGyAXrn7VCVorIhKlzjoqsX
ZThNI2RqraE0F5C2aNDPb6aqZlprpY/yxNrGTo2JAEfKu12sTk/esvQ7W31uBVvTwNUe6MnqlctO
2M9qIoYogaLZIC7oi6nF3/CdhqItujXDxoKA7fOb4i1gVHismLRtQGQxbG9f68d+ECCa+qsI2Ocv
SLHWid6y43OSynpbQs0xw1d6sbIJVqQ1/dv+GKNAteHXKYLd0diaoWGJc9sgUJBZMkQkYyEDYCG/
YUrjBaWJMMwgYyOQNYzoeawo3C7gqDGXBWgzgYaf1lGZKGbGeB+Cax0hQbLs2kJKJKqo/R5KMC8A
lhnztyFP39dwC1IUhRoqMQRieErQYPKAqfIC3HEqI1ADr3EX/Mj+LaGynQxjqdOyD9T0WXJe1srx
bX87Pg3fuq4o0G7r9HZSIVVDUVuocvkTVD0fx5Lt3U5sMHgNjwYGZR84eYSP4eGd1KZTbaHsdcD7
2LJl5/3hoB/96DOMj3+dkZGvs2iRKnGPEynwcTOhtrZ65TeYuUnfHMJAdCgGRNpTD3GA8vIFNMZ0
5xJgwYkrqtfTMqbrQriLSsWTcncSD1ETWeO/pHU+F91hSngGldHQTSnvDe/oHZpa3d7vRXGr+hdZ
EsVqLqyLKQ2DuhUX4s15/3qvsjb3UUIyKXkZCcNgLm5jVGqr2g1j+YOU+E8P26wDwxm7qEwH0yrV
Kwh6NIIuxjIxO1vXN5VbTYVgTObMbAXBqGBVb1yx4nDrHMta92/Gic95a+t3O2NBwGSZenUweq6m
T/dSWqFlrXvYRYEyGQOrvyrAVjRu+GOIEka3F20z1SZbbRtufcf0VrUkFuPSCHh+Q2ttsbKhT5/5
aOtZmlGzJfvF8SBIV8RpKMUaP2afWcBNFkMgY3aVAnMNo0DPOanTIsOhAdSjh9JHtfVDCosHqKwW
wzgaXoGaWYUyf4LWNoMmo6DBNeTinGyHL32+ZmXZZ/OpbSIE9gqEZc0EN2YcjlMgQ4bDcwj01LbM
oYrDDVFg2powbebC9P0uYj1xnPpsllCCflPbZSKdd4JWgWyb8XENMLzmM9NZFLTLzhnK8xBQLqZC
kEP5+1IiCeNl7O1jHzh5BI+maZia6qcEsKcSW4Wfmv9fwdRUH01TqLXT6dDX18fy5Xr6Hq+htACK
Zk8lsoFeQwz2lxID9I2U2FStwCsp3YcelkJC2QI9ui5qUZf1EGlrTP1bilKvcQOVc68uZYpaeMzc
kBFZRoWfllNUuOEcQxYj2RYXCcWTW1p/S8fOp8R1loTXgKiTUYy3hRKVakykt23PAEWV2u4llDcN
lcljAS7TiTVo26jUXgV9OynAYMEzaV0XZe9boCIDoUfVjpkLEKxLod5jGwUYzeiRqoYSCW+g9D6G
3Yxf68W12SMozYuZOFNURoZiXA2iwHEzFfpTwGcGkqEDqLFmqMCCbobFfKYuyGNUuXhLtMtSOWaN
vwva2+JVPVSpcENk7ewJs2wMNagXMKzg3DEkIrsjE+FnHJObKIPVRWV6Gd6QCRuiMsY2U+Ge7dRm
nn3UDuXOS/vPsJei7Ha/zmFmerzP3VRuDaXz2awZ78Ox5pYA24gxa70b9WeyNRpVxeZmfCkuNaS2
hBKpu4bINg5Szpb1aWSeFJkKOgTAMmUbKS2QKdHqbRblPejQWXFbPZKhGEOiWyjtS7v+yRxKIGtW
3jIKmLfX1S2UBkr9mCyV6596OUPIAhQFtjKq6lIUxwrc51GAVodkPrF55JvZV+fk39lRxdkWowAW
/k/+fjOwmDlzttLp7KmY3rNuSi+R9XMttfC8nthb4nRiIH6FqJHyVqqI0yFUASEzJNSYOPENpyi0
1Pv+EVWV0wVXYyRtrFEyZU6PwKEmWjeG20OpyVXYS53rMaqn0VuzYJdtgDLynmNZ/vi3Asb9mAmy
FIvqoRramUvty6P4VO9EtsSFQZHrMLWvj7VE9GI0yIYwBFBqXkYp1f0URR/Pp+qlGLLRq3fRtUaI
2Q/DlO5Gr8yiYoYDpaBluqTvTaOU2bkv+6qHWhCtfSKQEABo/PVy1V+oBRJMqeswVdLn3EcJta1j
Y3qoC7XCSrUW6o7Ue2zO61u4y/PLCmnYvbbsjOBOD1kW0Xo8sjWKIe1TU5y3UqEwQ03G+a2ILGgg
X5dxU+PjHBlqfdest+1UkTf1VTIuapdkNNuZXu1wggUC1VfIRpqZI+PRDs/KkHlNGU+vJTPRQ5Uj
aJfDtxjaFooh2UxVAO6jKhPPz3uUxdPQmxZtyExgPNJ6zXCoBlu2QEEwVEq9AuV2JpPzc6r1HcGy
wNrwNRRIkZ11XloXxvmnxsQ+1akboJwHtToC4XbVYsGPuibnvSFkHbu25miUCvMazjQ87vwX/CrA
1enal63z7/bYE2TUYOjq+hRnnXXCrN+bvW7KRcSukisJ0exiooJgh9gIagHwW8A/5+c3AL9LTMKb
iYG5gmICBBKq82UW2ml4W6my8np7GvP5rb+dpHpS6k/Uk+htzGtdty+vtR/FDmyilOuyGRoeDaR6
DBdo22dc3BoehrCk+/XEzTJRODhNZae0aWXrJRiOUKNjrN1S7tN5j9LQesiCHRdxFyn7Rm1HW1gs
rbyRomC3U1kMPa3+FOS0RYtqRZbm/4r1+ijjZMjLgmg7KB2KIjq1PF7/AIrqN917lMpIUvSsmFaW
qbf1t97+ADNTqpdRpcWtnWKoywwnQ4jqoGg9mwkqZCOIGaTi/aaNOxal+YcpIyBTtbv2pc0ULafS
ew1JLaNYMsGO4HRZnkMDofe/mNIZCXYMdaoFsw1qNSzFLrg0pVlWwPCC+g51CX5WY66HP58qrreJ
CjGoVRvM6xm6UD+ikFJGQJHufAo8yRzMoSrRCvzMfPJ61u8YYeYWATI4yykACSWKdS4bXjY0bd/3
MlOYLosiIO/K7wlgnRPOD0Gz4msLzinENRQzSDlWOmWCruVU9pM6vJ3UWtQO385vnb/NerSFyuqn
TGMXeJuFM0Zl28nOmvXkfDBUrvh472tNPDrtEMK/laPT6TwNuO22227jaU972t5uzoxjbGyMY489
mzvuOL+1Y3FDV9enOPzw93DLLVfQ29v7gN994xvfxVVX3czk5ELmzNnG6acfzcTEBB/96NVMTr6b
0LPcSAzEU4Ev5bcPpzyGFQQAWEfVFIBKC95ATOzjqQ3GXFDVVbyWyAaSaYECFqNUiGGs9TqUyn2U
AFXqIzyP3rkTT49KHYRt0YPb0fqcnkY/tZts21OQOpZFMcvBtGVFc+0qtb5mrB5meqMHEiGDXQQr
tYYyltZqMf3PkIahAb1OPdENlBempy3okdp2sYUS6FnWXOaiLWLWizVksYPIAFPPYHYMVDqi3to8
YqxsINLJpf8V7VmZV62JNPoO4nnfRTE2ahdMd/a5+94ayvsTvChy3UqMlTUUa3I3JdBVi6FA2CyH
ea2/rbiqEbWejsJJAZbGwH40fCQAXEyFJrtan1X748IvSFDnpaEaoYS01ugxC8hrLGl9Tj3A9nxu
6hsEDTJnXkeQqdfueNEID7TOoVBY1kkmx3pJik/NyrMy9aZWv/VQmyIKvOw7t7to61usFSKLA5Wd
Yzi13eZuAgiroZMNbG+noWGFet6CaEOPZlmZYmt4zZDwCBWWEoD42oHEeDs4fx9IrJ2dbJvrlU7S
CiqTRn3JZirMo0MHJdQXqLouHEiFlWWgTHU3RCRD7TyRyZF1ko2W4ZIVu5vSq1l0zppRf0FkfH6N
2E6ApzdN8zX2wrEPnOyFYzaQcdZZx/O2t736AYHJ7kfTNDPCP3HOy/jIRz7B2NilREXZpxMbZXWA
k4nF/a0EqFhPxSX3JxbGbxIxxx8AzyRSmdUYmIGwitjsan9K7yCtPYcwSu2aGZahN8bd3XpPhkVv
yUOxnEZ+kJhQh1CLgrVWoEDXIUQqouI38vrLKQ9BQ9BL6T42te7RAlwDzFysdxEL0RwqRVlPRirZ
hbG9OOlZL822LSeMvbSq7XdhU+iqZ6ouA4rdUSyst7uREkGuzPMJigR0lmm332VBBIMujoacRild
insHeY9bKZChUbFSbzeRWWGaqosfFAAwZdaFW2raUIgGSlahrZFoFyZzIT+YYg1kCDQs27JP1lMe
ugyIacQHZJsFt2obBoltAtqgQyZRcewBxHNdQO1WLNiBAjD757k03tZ8cTxq5GTDLPCmRshsMdkz
+1Pho6yD4GsHsZeNbVhPMVdS/4Jj2Q+zO3opUSkUqDV847NRv2XauQDYPhfcdFr9pT5uZ/aXjILZ
USuIsQ9V7FFmqotiNWy/jIzZexpZHSPHZ5sRtQ2CPEOQw5TDspYK3TkH1ICZVaPDMNG6ho5WuyYL
VBh7iplZM2ZveQ4ZScXFhsfVO01QhQcbai42BKBRSO1zci7IePl51zhDV47JpcD5+RyOhn3g5Od7
PNrBSfvYHWT8rMdMZuazRFbPLwPPy0/cRAz2owhjvo2YRP8nX7uMKKe/lggbXUot4GuJCfDnwClU
Oq6Gtgc4E/gHKj6v+t5qpk8nNsFaTgANF1oLLW3L95xALjoDxEJmtowFlgwJuHDKEuhR6uWrGdAj
UYhmXQGrJhrKcl4YDzZ+63mlbV04+rN9q6jqsdZtWUmJYPVk9PrsJxfDuVTK8nYiTGe4SQ/NLAlB
neDDei/2jYugITcXzLXU/jumRk9TC7Tt09jqyWp020LkgXyOsjR+ViMrE6DY1jCU14EqgGf/aJgF
iI6VlZTAer+8D0W2xvDVB7l4j+a59TJp9fl+VMjKdttfAoHdWSdTXfVYO7t9r5cq5b40fyvw1ZgK
0M1EkgEz60UdF5Txe1ze73T2w1Q+m/2o1GnHyC4KODheTdn1XgWK08ScuJfSJMmqOIZsr4zWinwu
B1Dzx9fXUsUCx1rvuRa0AYjshYDUe51Hhbg2ZT8LDkaoVF9fMyRiWMSwhgXYvPfFVKhxUevZ9FAi
ZuuTKLBeTjh1/RTLZRvtZ5krQ4ZqzWQpDM/Yh85L9SMCCNu3lBjvEwTwNoPSNUkWUIBvKNM5CrV2
mh69ktory/Rx9XqGYxvgn4A/ICqV/xD2IjjZpznZy8fPE5jAzLL5q1d/mZ6eVxElnK2xoGDuiYQx
1ZvqIxapywiP633AbxNZROT39iNCPd8mtu9+OxViMe4qNTqXEgBuoViHbxCL0xiVwrqIMsj7U0XB
9Lz0CkT7Vns1XdMYvaX0pTYVD1pcS9HaUmbu/Gsa7zLKQ9PwOnGdyOpCzOZQR6P6fwtV9G4hJdDV
+1UQ3W5DO11aD9NY9hYqbdUCcPbdVLZnBZX9ZE0Va4uo+9lO1T5Q0KruxUyjzVQYzrRda44Y8xZw
GEJQ5NpLlcyWaje2b70c0yc1aN6rzAqU8RdYqo+YS4W9llKiVutJ6G2OUhWI1SzIlElrS2OrRbIG
jGEp60+0M1oEggtafwt4/J5ZMd6rGik93N21JArNZQ4U6K6gNAwW8BI4LyfGxEZqPLcF2YZ0ZDY0
1s6ZNos2RWkxZBXVMjnGNbzkPfrMBebu1yMDp37GLB6zixZSIth1lBhfMNQuaKg2ZmP2haCqr3U+
xeh9FPugxsLMnD6qkq6hDjVXZvIpcJZF6qfWJNPmLRXfZmsNH1pgznGizshQUXtM9VFzVkfHsTtI
MSDDVHE/U5Kdb4Y5TTxQpK8OxXIMlv+HAkauja6bI8SzN4NwB7HZ7EoKWO+9Yx84+Td4tOukbN58
K694xdfo7v4hNfgNP5wJHEbFkP+eWBC+Re3/s5gADCcQE/M/E3qTCSI2qVemUfsKASQ0zHqw0pSK
xRx6i4AvUpNV72SEYCEU1t6Rnx+mqt6qStdgm+JpbN9FtJeawO4lZHqr4jSBhYZWI2o5cQsWmWKt
PmA5tbgqmmwvAkupkIvitVGq9ocGzdRM01P7qY0brQliBpLUrHUyVPGbQqxGYDO1WeB46/4PaJ3D
OPh6yoNUuEerr7dQbIuUunR0L1WRdj9qodObVmi6gjL0DTONvoZngAI33rOGUwPr9c36cWHWI7X9
9ol9voiql2IWjhkYY8RiviTbtizv37o7psPKthmCM3tLZmWUSvFtMyXWgxlmZraYITay3c4lDarg
dyclbjQrZAlVBl7RtuJyQ4D9VNE0AZ0UvzVCxinwoDhYMOV4VA+hw2GIa5oYO+PUuBXcKSqdTzFb
SyiGQKBgwTr1Hz5L0+hlBZyfgjnP08+eO5mPUdWYnWtzKaG/QlSzgNoF3vqZGcJcTgnNF+b/UMJv
M+s09oa6oFgbw2QyPNYpcZyvozZM3UqVLpB9tb8FVPOpJIZ25qDhYdlsBdoyrguoLCYZMu/Vsfqb
7Esl3nc87EdfXx/ve9+bednLziaMvZlCzyBCLOuJSXodYbQ+RxV3g6rD8GpiML+eEN0uAy4hJqaF
hlxk7yIm6BnEwP9FYnIfkddYBRxKVUAkz/d4ArXrUaoB2Jrfe3zrGooq51HCWI21cXgLJFm1VY/V
0JEepoufFO3m1uf8zCbKWFpkaZwS6unVSKsuzfc02rapHXZwkTE27eKuAHCYqiRre0bzswp09d5d
0MysMMVX4aphG/U5emayHXqA81rXMDRjWMgKm4ta5xmkUnbNLDG8YsbGLioLxsVb9kMRqwyAYMi2
3UexCIIgmQAzi+xDs5gsqLWUCgtsozxJn6+hAQW9tlfAYJjJAnL3Uamjgg0N/mJKc+B9SdmrI5NF
8Tma5q54V0ZpW+scXgPqWZvZIgCTcVRDZOaWWV+GzAyvWFHVDB/BzBBl9AWUpqsP5PkNs6lTUtSq
Zz5EhTc2UnWHZCBl4wQ96ksE1LI/ZuSN5d+Of+v3CATNElM34TNsMxzuF2ZasGEStyFwrVvU+qzp
ztY9UUSvE6GGxGq23pNrwgQVdlE7BuUobaBEstZyklmcR4loXTMcj8MUe2TfWutm/9b9dPI915pp
Zs4FHTCzLmV1LiRKUez9lOLHBDjpdDqv63Q6X+l0OqOdTmdDp9P5RKfTOXRvt+uxdFx88QUcdtg9
wFuIzQO/TAheX0aAiD8GriYMo7S3x4lE6vF1RPXAM4hBfyPl8egV30UIqcaJtGXjyssJoe0a4K/z
PKPERL+M8qT/hphEK/Ncb6EEak+lRJvSjtKlKyhWaCvlvRq+kBY1y0fDam0DMxR2UrSu1LBeSbs0
v2JFKAGwjJQeneyEGTiW4pYNko1pZ9fIclh3Rq95CeV92U4NjFk3o9SiNUF5/4IgY9OGPbwvQVWb
ltd4LG09G0GWRsnFTQO4P1WUTHGmWyVodGQU9P4NH7QraG6jdnGWoTEubzq24YU+KkXaWi2CTMGA
dTGsrCu41GgLUAby3tpZNIIOGRiB2jxmprkr3JTiN4wq09EuwDZCZZcImGTkZGfaVYYVAC+i2CPB
bj/FwphqbTaO7MkSwiitoJZ8Q1lmeRk+0LibleV2FQKnPooZM/S4lJmhQ0sEWH9mhMrSM1SikbT/
NLKOn01Umrgp0TKxXVS5ADUnOgg6NuqezKKRNTHkYXVZx4ghLksHWMTP83SoWiFjlDBaAKHOaBEz
04gN2brW+Dy9//kUgyQrJPhQz9YWgHuffVTJgN2BfFtLspUSUZu6L9uivsaxu5AAJo+O4zEBTgjr
+AHgGOD5xMi8odPpLHjQb+077j96e3v5yleu5NxzT2LOnNcSTMgNRAjn68Rk+RiRfjzEzA2gLgDe
QwhZf4GYqMdRBsoCUW8hFqsPEJPo9/L3ccRk+DQBOv6FKuzVS4h0T81zHECFSAaAFxOL6guJkNET
qOwQjaQpdxoQvUdjwtKbw1R9Dz0w6yPohQsS9ErGqJohZq9Iz7r4K+JcQqXGKki0bsUApRNRjNdL
UaqGNMyu2UWFmvqoYliGVUzZHaRKnuvtCLRcXLsIdktj4F4eWyjQYolvayHYHjM4TIE0nXkRZSB8
fxOV/qr32dZdLKcyBASYfsc+NDW6XTPEZ2VaueJFy/Jr7H2uKyjgpDfd1gOYkWG9F8XcGi8NlVlP
VuV0fC2lGK1BSsexkBhH6nfU6aghMqtGcCuQkQVSG+DrhjkViDrmNEK2S/CtJmIRtfO4QFxQoQj6
IGZmddhOi9YpfrVmz1bKwKpl0VjLWC2mUuwFv4ZaZd4MOziOrD+krsg5vS37fhnFGhhGMdShRsRz
G1aZS4mKrcQrY9VHFfmz1ofMoeydNYoMPUGxr4IydUxmKEIVS2zfuwzOFiosp4BX0O1as4CqMdNQ
GinZSsfsZkqXIvvjs1ccrYDXEvaGQfuouT7MTH2PmsRHx/GYACdN07ygaZqPNk1zR9M0txNWbzWZ
iL3v+PGO3t5e/vIvL2XVqkMITUkvUZn22cD7CdbiRqJo2/sIpmSUYDYmiJDO94mJcwEFCDRIpxHg
oo8I3QwTk+BICu1/ggA6gggN/muICfJJYqKeQExMDd8fU/U8FhPsjYZlFRXf7yOykBSlSZnLiCjm
NC5rnFcgsoJKSbVOhQuf3u8ERX9vpUpzG7JQC9NW+Os9GgKwoNNIq28snqX3ZEqn52mn2Vo3Ra/H
MIpMhAt6O2ximxTmusAa4jHEtYQyhFLmFk0z1HMfxbhY16Kn9exdmPVy1bsI9GRT7Ms+Kv6/girt
b0aMOof9qJRI03I1GrJX6hCWURoH+3qg1U6Ng6Ep62Ko1VDLsJ3anE5Wpx0WUbC5hRIXNlQpeg1W
ezsFq8taY2SYmfVSFCFbALE/r6lwVqABJZqdIECpfbuDSsMVSJrRIpMlE2Q2F5SRXU5pSjSKFk8z
+0MGYEOrneqxZLaW54/XsLihoFuDbWhQllCWZRdVNr8tGpfdsSaK+jcFsUspPZMA3LVqS6sPl1NG
W4fFUKtsXk/rWopovVezrCxY2E+tfQI2U4cNHbluqndTWK6GyMwpn9MSytExXAtVFNC05K2U3mYZ
xQCrLxLUL6PGkeNQJ+LRcTwmwMksxwDlTu07foKjaRomJ83z97iZmXReH7H/z+eIEM0zgc8QmTb/
gQAtAoND8lzGpE1PdOL2AR+icu2hJuNJhI7EDKJ5hI5llKhsezcRBhoF3kAxNv35v+GJ/0VMaqlV
0xJXU7S3IQrDBnrATnRj76OEYdyfYjAWUXFbvXoXMmlXwwVqTPandlk1W8NFbpTaOwPKK5tDZe/I
+AjO9Pz1OBUSqvUxXKToUApXb0gPa5RieARUgqdNlJ7AjIt2WW4L1wmeDN2Y+SEIsr7EUqpSqiXu
NTLS4lCg0eJY7awiQz4Kj9X+WHp/kGJxbN8ktUGa1zL2rnB7LD831Opf0yzVOpgVpd5lhKLHzWxx
LJmdphDYLBnT4hXi6q0OUuGwYWbWdtG4KHreSIGbSQo0GsIQyFqyXYGnYQA3BFXXovbCjC4N9lIK
SG2hALihEJmPpVSmjqyR4dMRyqC7LoxR47KH2s9GPY+hUCsZq1uxQJlsk2EUBeiKZ9vlA9w6QbbH
cafQepSqtjtGZVUJKNWKGLJzDJpRaCjWuW5ISe2RupBxKoNphAKb9rlhS0XFhmvsazVshnSHKTZO
gGI24lZKN0T2h3vtLCEcif0o9nUuxdaoy1PY3WbM9+7xmAMnnci9fS/whaZpvrO32/NYO2p/H4GC
FP3udF4vMYjfT9RJ8f3XEN1/DcG+3EHFURsi1fgGCok/GziXWJSuI8DHBcTkOYoAPCfl+XoIwe4U
wYzsJIrCXUxoZE4BfokCEocQi8pKgnGZJLw8dTPjBECR8VDoKRvxDEoY2U9MdEW166lCUkuIzCZr
pegBygxYEM0wl4uchav01mVkNDICF73lpVT2UYdiTKAWeIGR4Rny+1Z7nKKKPZmdYr0KKephitGw
hoqVWUeoSp3jlFdlHZp2qGkZtTmg7fD+DAlpbK3rYMaAISXZD1N721VhFfbt33p2GkGBweZsh94l
zKzJIkgwPKQhMyxgfw9RdU8MXUxQRkS9kvdmKELWyXChNVG6qAJ/Fm0bpUrva8D7KYCj5sFMMg28
BdL2o7Z08DnIDGhozRyygKFjVHBhOr6hN5kLwY1/T1IVRg0bGI4cojabnKBYB5kwCxFOZVvHWvdv
iutiYo75rBTNCuKtGSPjYqabYGUptT+Ouhj1Q+3sMWuWCAKtL+Q9KVDXoMvgKQZup+qrI1pKzW8Z
HxlIwbVF9Wi9Zl8L2ExrV5gtC2pK/CTFMgqm1euoqZKtNbSp7m0/Ku1fp0Vw2VBl/pdT4Hw+sSHs
J3k0MCiPOXBC1Nd9EpHvtO/4KY6Z+/soIJ1tMN5MhGraRy/BqnyF7u6r6e7eQmThbCFQ9wWE0HZV
fvZI4K8IUPMKoubKGcREfycxiSH2CHKR7yFkRqL93yIyfl4DXE5MrOuoolSfAp5GiGwPIVgemYgh
YoL/CcUuzM/3b6Mm5cfzWmpA5lPiyy1EQbp27r9hjH5CL6PafYASrD6FWnStAoM5nWcAACAASURB
VNsuOa2nbRlyY/3Wb1A411BxYyhD3i4Mpq5hGeXFK/bVEBua0ptui+QMdZjlYcroOKUF6KW8vK2U
cNLPtNMmNQR9lHFWB6HQUc2BhnIBpTNpFwDTOxVseH5B2XCrXQIpdQP2czubR2bJeh+mvgoSRikm
yPobshx6x7JLesembpv6bBhFYCwA1DPWcMooyEZI6bf1Nfahn22HYdSUyBgILAYoRskwkoXN2iJK
mQuNl6yNDJQi6WVU3Ry1M4InQ4UC+bbeSR2LXvq81v8CCwXIUHsMDbbaouhdtnYRtduxGh9FrdYJ
8Vk770aozDTZPftfcbohwjbrB8UICbg3tz4v62NoViC1hQLx6m4cc+q3ZNOgWJrFVPhW0G0ozT6c
pjZhdJ5P5vk9zxClcVM/I/u5hJpzMpabibn4WWKN/Q329tHz0B959BydTudywl0/sWmadQ/1+fPP
P5/+/v4Zr51zzjmcc845D1MLHxvHxRdfwD/909nccUeT+/scTxj4M1qfmo1RGSP0Jzcj4/CSl5xJ
V1cPn/zkBtaseTlN8z5CWHsp8HmiJsqlhPB2LlEDxWJUXQS9+1WCbTmOWmTuJSaLXoJak2OISfWe
bNtZxM7LEKGpfyYm4tMpsd4UUQFX/bQe+fo8dz8BpvZnpnfjYrKNAFXuGUN+Rq/jz7JdAppd2a6b
qfCEVW3t161EOvVk3usgsS2AOhvDYDIP7r67hGArTKFeRC1Ghi5c2EeoVNVuwmPVGFg904wL2S+p
eFmZ8eyXjVRBKmPTVotdl5/Rg2sXqNpMeJ7qMTRo7SJzfVQdBp+ZHuRg9o8ZVBonAY8VT2WZzOYQ
TBjGMo1VbYIZDQq657bu3RRR709jtjrPv5YySsNUaECPV6GvmWHOIRmh/bOfthPjW4E31O7PFs+T
2ZJVMoPLKr/WqbF+jZVjpe0hQqMHUUZynKg8upMS3rovi+BG8Np2XtT9+JpAVt2E+hbrzqj7MMut
hwJKG1ufn6bCWgJWAWkXwWBuoXQm3pfg1ww6WQFB/DBV6l09UVfrf6u8CpaGqKJ/Haquj06K88fn
bE0fQ6NQ1WsFZ/1UlVi3FGhnohlyXZHf30A8x83UM99FabBslxl5+1HhG+ev3zFE5pqjJkfwLdCe
zntbR7Dcc4n18AfszeMxU74+gcmLgOc0TfPDh/js03iMlK/fW0d7f5+dO+eyadO/smvXu2kaQzgN
IUr9Qv4/BpwNvIpgU+IzXV3Xc/jh7+aWW66gaRre9KZ3379nUHf3KAsXTvP9769h1y4X/5WE6Pb1
BNvx4Xz9eiKD6NlE5dkVxAK4HridEO4eS7Ati4GPEsPhqvy9mliEpXf1Tj5GhIZOIjQ0fw88h9rX
ZT2xSH6dmJzPojzk5fn+YmLyPhe4hVgkTySYmgkiO+kPsw29wL8SIO7PiQneEAvOU4nwlN75Soqu
/t8E0+JCbJ0OjYehGDN7TNW8jyqm5oIjXb0+n7ZpipakNzxkSEuP/x6Kuu8mSqZ/h5kMhjVYPNdm
yjtW9GrKbDtragmxiPr+inxPMekSStiqARyjGAeZnMnsZ7Ui6oisb6OB8m9BiCEvwZEeJ1QBs2lK
96NgezR/llNeaw8lVNXwC7wMlw3ms5GR2pSfV1hrloZ9bb+o+ZHhkI1Sr2RarIBHpqpdaXeESn3v
afXxILU3leEUNUlWG7WGyhaKrRMEtivk+rzM/tk/r72x1ZcyIwo9zbQx1LIqPy+4UzC6hcqI28TM
0JcA1menYPSAPJdOgNosU6nN8DEjRu3MEAVAHd/rW58dJEoarKYYKoW8ikytu0J+fycBHk0Ll0FT
r7KNAIcbqHG6oPW3YUFF8FCFGGWTlxCgXcG22ijruqhXE6T4zA21OTa2EONXAfdfsG/jv5/g6HQ6
fwGcQ7ij32u9NdI0zY5ZPr8PnPwER9M0jI+P77EZYX9/F7ff/kqmp88gwhrHMlsefFfXdZx33v9r
78zj7KqqfP9dt6qIJKmMTJkrjKlMDFGBiJCQSbCJAzQ9qODz9eeRZihEAkaBBBS1RQWRBrX1STu1
AsHWYMLowwYZJVGgBfGpYTAYmUJVEiKEqtV/rL2yz711K6mEUFPW7/O5n6TO2WefvdfZZ+/fWdN+
gCuvvLiszmJq/ra2NsaMeR/PPnsI5mvyr9hLdS5GPB4FPoFpPpqxiWs6RmQuwsjA+8mT9e2YD4rn
WvkSpqlwlehkzMz0S4xUDMEmh59gVkH/IiXV9yXMt+YJLD/LK5h/y4NkZ7F7MILRHyMp08jaAv8q
uT21cyhwGqY5OgTbVHEE+YtwP8zZ+CmMzPwCOBMLt3ZzgjvgHk/WwvjiCHmTxofIUReCTdKemM41
JZAjC3xi9y8xNyG4r4t/nXnuBCEn2nNS9SRwGUYy3QTgtnHS33UYCXmSHJ3wLHmRc58LX0z9a7ZE
XoxdY9aW6vWJeyA2uY9I/fVIhrdhRPMZsk+L2919EYQ86bvzMuSN+VwO7rDo4cKeBMwJmpN49+lw
YuMEzxdgj5CozB8EWTvjMhJyZEfRD8gdHl1Lsjc5YsoJqWdH9gXZTRYjU9kB5Cy4Rd+boqO67xtT
9E9qxjSekPfDcm2DayDfQh5vrr0qksEisWlN17pZxuXoids8jN6fhWs73FzkRMW1EU6uaijX3u2R
2uv9dN+uYn4V77fX6Vofd3R3QuGavbWpXe6suluS1VNk/x+PgnItp0fB+bvm6fw3YGRU0nN5nbzP
0V7kLTE80Z5rQFzO7ssykGw2XUeOSnLtnMvKSaqbbSEnnSuGQZ9DT9j4r7f4nCzAnvrPsdnNfyd3
Y5v6DERkS8r71atv55lnfszq1bdz991LaWy8glLpZqr7nxja2t7FsmX3tKuziFKpxG67bcTIyCWY
b4rnWQFziHXzzuvYpH4INuE3YVqPG7EXdjqmaXlH+tdDom8Hvlc4PzW1eTI5FFAxjuuTw9np+EIs
Cd0BZL+Ie7AXeh05tNSdOgelNr+AkRj/sv7vVO9SjJDsBvxfbBI4D/OH6YdNQOdiKt+XMB+aJzD/
lTHkr1OA+8l7AHl+E/fneTa1ZzY5R4ZPZh6RdADZBDWaHFbrC677Lbj/x95kh81+6W9PPlVX+H2D
7K/hESFue/evtfEYiduYzh9EJiJOgFx2nkgP8iLnDqeKLQJudnAHUQ/Y25Dqv5fyDRKPI4foum+E
+wr5Au1fza59co0SZKdP9yNxOe5JNie5D0Y9ebdu9yVyJ1H30XDtyyvkEGl3cvTn4flNxpNT0g8j
mwGGkzUbrtUZRl6gBxTu734kHjbvi+1wsiPzX8l5TNy/yJ0t3YF5A9mx1Z9Xc2qH+2I5+XKi6Plg
dk9ycZ+XYuI09+fwbSV2I5vCags/z3brGkWX5fDCM3LnVvdnWYeNqU3kXCHuuzSoUNY/Btx3xRNK
elK/IdiYe5mcfdm1FO7D4vmOnAy41tAT+TkJKe4b5eYrjyDaPf2/P3kMD0/3nkT2Y/L3xp/NkCR/
NyV5DhXvl8vKNTieGM/9cNwpvIWcoPN0uhu9gpyoaklVa6r8vtPdbeuLcGLhmwieccb91NT4xFj1
CjZv7s+2tHDmiHsv9sIdRyYV92F5VfzLZznGQ7+AEZMTMBJxBPZST8acbqemf28mh9SehPl/jMS0
ExdiWpo1ZNJyAbaoHIZFD12Y7n02Zlrxiewu8j40/hXjnvaK+Yzcjml93LntitSHu1PfnMgMIeeW
8fwx92CaHM/QK6k9z2HJ51qxUGswjdXrmMPvPhi5OQ+bRNwWfzBGPl7FNAiulfCv+k3AB8kZPt2M
0IaZxjxkdSZ54h+e+u8RC2eQfWNuxCbHceSvdVezu0/Laiwiy00Ez5Gjv9xBeQNGWpwoeY6VUeSd
m32yfwlLse1foSVywjV3fm3FzH7rsPFTIuefGUb2CfB8FW52cIfcwYV6fOL/KNkPaSZGHDwkvpgE
zJ2Pi07OTvpcs+XaAL/PSLJmxAno3mTfFs9b4+TAQ5mh3HHUnS/9370KbXbSMIz8de+LmSeQc9Ll
i7JH4HiIt+dTcY2HRxS9SvZX8THg4c6DCm10eQ0lbwPg0TkbC3UML9TlRMV9Xtyk5uYqD8E9rvBM
3Xn1lfQbRXk0lee9cYf5fcgaE8gp7usxzZybH31h9/wlPt+5BtBNKp63xp9PC3lsDCL7fK0nhzv7
++MfIR6B5FrNr6Rj48mblDr58rnJk8y52dV9qIaTHaNdg1NpanJC/Ats3voq3Y1eQU4C3Yf6+nq+
8pVLGDOmmkraodTVbdzmDsuWQv9L5KRdW+6CRcu8SPmivx44P/1/D6CVk08+msbGf0PkNEwzsRkj
G1OwBflsbKIagGlinBCckMpcjr2AP8YW8zGYf0gr/tU7bNhAbPEfgZGkx7EJ5BZyGu9b0r8HpN9o
7OVeiml0zsBIloexFh0jB2IT5hWpLW6SWpPOnUDWNjRjk8rHsIX9ZeAGbNK7BPgmNvndnf7/VCr/
rVTW9zJaiy08n8Y0Nm52+Wvq97+Qv7I/luS9tlDHi6k915ITnbnD43+kfnmoaBu2oWR9kstlmAZL
scnXnf5clVxMKnZWOu/+Js2YNsm1PnUYwRqe7nUwWaPlobCDsazDJYzAHUZOv+8mON8k7iWMxPrC
W0zm5kSAJHNfGOdgZhgPJ3d1Oamu+vR89iQ7Tdak9ntSrP7k6JursEVkbKr/gFTHXLKjpKvt/et5
EHkhd/Lh+S42pPuuSde4Zss1CG6SgpznxCNbPDfPweRtHQZh7+dwsj9QPZncFiN+PGLKiYs7Zr9K
Hm+uKfJMvq4JeZ28s7ATaydakDfd24dM/nw7ht+nuqek8h51s4FMKl5Ksh1EuS+Nh497Rlxf2D2P
iGvY9iDPgZ4Qzt9rJwFODtzHxbUqvg2Cm+jcKdc1MB72647bg8kh33tgxoMhWM4pJ+PuAO6E2OVX
NCG1kMnj8NQP900bQt4rCYzwfhSbt7rf3SPISaBTKA8/LkepdAvz5x+1zTrq6+u5//4fUV/vJKTs
LPZF7Yv+gZiJ5I/Aw4gspqnpH7juuq/zwAP/yVlnPUpDw72MGjWIceOG0dR0EmPHjsTIiH+VF6ON
PomZIU7DzCQnYmn02xg6dHfWrPkZra2/QPUxnnzyPoYMKZETEtVji+kV2CQyGYsQujmd34SZbtow
knE5Zl64Clssl5O1La7dUbIKdS6WR+WtmGbH27o/2eHyAoz0vJTOfwE4JZV3k/AgzDQ1mJx34YOp
TR6V8PMkY598XdMyEPsq25za3paeh6Y6BmKLwm3YRPhK+v/L6VwD2TRQwvxo1mFakxOxidEzhT5C
znHh0TpuZvoWRihayLb9w1MbP0TeBHA2pupena4dSk6gtT71ea8kmwayNsO/Xt3Xwc1RnoDPSdMg
summFRs3Q9I9voiRYI+s8a/8NuA35EiVDeT06FPJDtsbKc8N8m2yxsn9Vo4ipykfjI0PT3rmmXQ9
d8k5ZALkppp9MQ3TOuyd8GfmhMMdXP0a77ub2Z7GCM5U8qK+EVsYjyU77bqW0cNq3Zz4Mjmk/lVy
KLCHvHp4tmdivZacMt9zeLhpxuU8ON1nYOqfk+NW8n4+vydrhg7BxtAisqO8m6LeQrkTuZvTfL5w
YvF2snOtP1d3Nt6bHPLenJ7B/uRMvKPSde58XCSETiigPNTdnaPXkR1wn8fel2bMn8rNT2BjyhO2
7UfWcnpeISezrj113xMnUVcX+rUfNj9cRU8IJQ5yEugUPvOZhTQ2Xp78T/zFUEqlm2lsvIJLLz23
U/XU19fz4Q+/uwOisxD4FCLFJEBKqXQbEyd+ecs9Kv1jnnzyDr785SW0trpDIdjk/kKhHs/P8ii2
+PanpuYPNDXN4amn7mHkyJGUSqUt9f/mN7cybNgFWEIi/8L/EfbKrMVe8B+S9yJ6GJvUr8BIywiM
OPway+GyGSMFX8Q0E7NTOy7GNEPDMPOTa3aWYpEyl2IL7C8xzckd6f9F/59i3hBfAMAmwe9gxKY/
MCv1/xZsEW3GyMBajIgNxRbBT2ET5fTUrgvIWxX4ROjl6jFtx4UYCVmf+u22d88A7IRnd4wEgZGO
gzGNwSQs2d7uWP6Z8dgCORxTMe+DLWBO8hYm+dxBJh1fIGeS9eiTYZgG7dhUx55k04In3luT2ngc
RoDcj2BjktXrWLj4ULIPxU1kk9TGJN8Tkjz2Je93NDX1+w/knWEHpX64783NqQ/udLoeIwOrMIK4
AXNIH4QRVfedGYYtZH9O8h+S2j0OI/X/gi1S81L9h5D9ENZjY9Tz1LyCET3/gm8ArscW+3nYeHwF
G4O/Sn308O26dJ9G8v5PI7H3Yi/yxoRORG8lJ0mrx0yW30/XePlNqX0byaHuzVg034vkXEGbUn1P
Y75krnkVjKCCZajeO7XzGbLJ0qPK6lM9e5Kz1I7GxuQzqczkVFdjas+IJGPfHHQTNpZfIuehcY3i
ZozcuobvZeB9SfZ/Q/bTaiTnWHKTVC15qw73w3HtX3+yP5CTzZHY+B5Fzopbl8odS86XMjj19Tiy
2bQt9esW7Nl3L4KcBDoF9z8588wHaGiYy6hR76GhYS5nnvkA9913I/X19duuJKFjovMLJkzYndNO
u7fT93BTUvvMtwuxl/bmQunsOCvyfzjjjJO48sqLq9Y7cuRInnzybpqaHqKhYR41NauxhWw+FlUz
C5uk/0J22h2PTUKuDXkPtmAfi00En8IW03nkZHU3Y5OC7zVyY7r+/dhE9AFskvWJ031pKk1o78Qm
aTCzwwosZPp0ciTIeYV7Dkxt/FW67hzsC+1icpjt1zETkJMJD8HcE/ONcdX8/alPl2CLxq9Tm33S
9v65s6+nBr8KW1h/i5GmkzAfnAbyBN+AqbRfw75i345Nnq7pGZT+XpeuH4Atzk+T85AMwMyD67CQ
8qmpzCZMq7Aolb0Y+PfUD9coPJzk8zymQRqS2uhapsGYCW4sRub8y9dNL7776x1k51zPMdIPU6Pv
jj33O8mL/eJU5yWpvnvJTrtOrl5MbfwpNu5cxuswcu45hxaS98UamJ7bZ7FxsZAcmj4g1XcgRlT2
wTQBn8HMgbWpPYL5w5xLjhK6gmyWdMf3MamsZ1ftl+R3UGrn6NSHT2Dj0DWet5Dz58zHiNQmLMpu
MjnkdzC2hN2f2vbW1P5+GHlyJ9Vz03MYjTnMe7g25AizKeRcPuswQvwQ9vzHYKbdWux9d3LgTtAv
kNMNvET2XxmBPfPDsFxPzRgRcxP0YIz0biSbB99beBae6v8ScrZmz/njzrKj0vPyD5R9ybsue8jx
36Q+n0/5ZpINZA3qHuQAg56BICeBTqNaRE9Hi/u26umI6Dz44E/46lc/u0P3KDc9uePpJylPx6yU
SiuYOPHKbWp7iv09/fT3proXYhlvj8Ymrocxh97PMXToKurqPoFNkrdhfi23USodzYQJgzjgADdT
uM3eicg8bDHw3A4XY9oUz1Y7iBxtBDlhVRFOdlZgk/0V2Jff1zBHYo/UuBFz9D0Y88s4G4sSeijd
+27yVgBLMdLwEqYVeIlsEnJ19e+wRdT7dAumSbkLm4ynJ1lsTO16mpwifRC20L+DHEZb7P9d2GT8
RWxRuhsjNFek+7gcRmALqaTn8k/p3AtJNr54uN/R89hi8xpGLJaSw0yXpWfhobpNmPbqGmySdzle
jO0ztT616enUzrbU59HY5H8GebPCy8laAY+ouCnVeUDq824YiXWH24EYyb2EnENlVJL5Ialvo1Lf
34mRr+Ykq+OxhfFHGLl4lez0+Y/YAuZf5TUYaRqc+j8tPTcP5d4TI4t/S97rZh55B+X3Y0T1lxhx
X4jl/tmELe6eRfW19Mw+m9o5E8tKOp7sR3IbeS+hY8ih7SuxMXQuRmbcZHUhpln6RpL3OHJEVmtq
p2d7/XRq07vJGZHvwEzIX0iyfpXsKF+PaUjBnv8/F56Ba9IuS306H3unfJ+fWzFi5+H4o5Jcn8O0
WpA/eA7CCNf0grw9WR+pzfti7+0wsjZpEDnaajP2Pu6B+Z6NwsbHI6nNA7B3pQYbP+5IO4pMKIsB
Bt2LICeBHcK2nF+3hc4Qne29R3uNzEhsgVtKXd1URow4IZGgB3dA23NeqttNLq4deRd1dQezYMGv
eeqp+3jxxZU0Nf0yka73lpGulSt/Sn295yuA8oX4vWR/G8gObV72HdiCVwyhLsLJzvXU1x/LiBH9
qK+/lIEDn6d//wuwyWd5KrsSm1D/G9NyPAQcR01NM3V15yDyX9ikfy826XvU057YojMaIyD7YkSh
mCvjQMwsdRW2uBxC3s7gHmwxPp7yRFtOvionRCcvx2DP0Tc7c1L3HEbGhGzCW0g2ZdWSSZUTVV/A
jsIm9fOwRXTPJB9/JndiC+B8LNeN5/eZV5DjJ7EFyts5A1uIJmNk5TGMsHg0hucwOTLdb3+MwLrJ
7yBsEfFINn/Ol5Az1q7BfFTuwTQhHlXkff8apgkq+k8chvkA/Q4z540oyNcJ3WhsATw63dtNjKPI
mra9UvmjMJJVSv1xp11/lv+Oja3HyITXnWVnp2fmTuqzMA2Ph66DEYiFmP/D58jh3W3Yov5Hcojt
27HF9kTKzbYe9eXOniPSsXNSu6en+40hk72TsPE8Chtfz2BjyDVIF5C1ifelPm1O15WwsTGKvH2A
m2h/ghHU72Jj5vTUn3nYc/8kZlp9HBsv7os1E9PynYl98DyOPXN3Rp+PjfvpmFYJbPwMxgjMhzFy
X0PWrApGsh5P97yZbMK9l/xudX8oMara537Y26grV67UwK6FlpYWbWpaog0Ns3XUqPna0DBbm5qW
aEtLi7a1te30us86a7G2tLRULV/tfmedtVhLpZsVtOLXonCEityk0JaOfVzhp4XzMxWOULhBYY7C
ikLZNi2VluukSXPa9bWtrU1bWlr0wANnKHwoXVd5f1WR5bpgwSJtalqiY8fO0NraAxVuUpiV7tOi
sEhhosJBheOLFar16ZjUzqWpLwek+toUzkr/11TPRR3UoQo3pTbNLPTXZTJHYbnCoYXrW1Kbjkj/
f6dCY7pfc+rDAUm2zansDIX9FZaVyRSWaW3tkRX3nFHoR0dtuiH1eaLCuEJfFylcrzCpIL+Pp7Yu
T3W7TJoLz7lZYa7CP6R2r1E4VuFtFfJvUViS6i+2q/ibqdCqMKXwXCelZ7BUYXqhLpfVkYW+evnW
1F4/PquDezanchNS/bMKz8JlNSf9/qZCpi2pnTekZ1x8NocrzE7XVd7T2zOzyv/PSfL+rtq4aFWY
X7j2olRvcVwW34ElCkcpjE7PpK3w3FRhWrruxlR2dkHWa9I1h2seK/58/d0ap/Z+3ZDaPDGdP0bh
7xUa1N7jGxUmq42nmen4pPR/f/f+LdXlsj4lPYOZCvsmOfix4pyyUjHGe5h21zreXTd+UzsV5CSg
1clBd9fd0tKikybN0VKpklis0AkTZuqCBZ/YQn7Gjp2hQ4dOLRCWFrWFrDFN9BNUZKIOGDBDx407
dgsJ29q96+undbCAWDsaGmZvKd/c3KxNTUu0vn6KZpLkE/+7CxN6i1YjSzaBXl+YoI9Pk/Q0hZkq
Ml7hJ6mejupYobW1B2pzc3MHxM4Xi4OqXF9JqqakX2NFf7yemWminp3aNFvhVK2rq1zo/Z6z1RbM
m6rUtURhug4YMEPHjDlGhw07WEul5WmRmKVGMj6ktvD5vU/VTCoWF84V5befZiLTpnCYlpMYb+dF
qUy153yKivw0ycKJqpOmOan+yv7O1XJiuyjJcGa61wrtmKSqiizVujpfDJemst6nRjUCdJAa4Zpf
cf0aNeI4t+L4tNT3jsb04vQ8V6Q2zi3I+m3p3CQtJ+De34laPi69nmL9f0ptLpLUNjWCVTmeL6q4
vpLsFMfc+UkeTtyO0fJx5UT6CIWTCjKdpEZW5hTavqTQxyLZ/GE6XiTr1xWey9Ea5OTN6FSQk0AP
xta0Ow4nPx2VbW5u3lKms0Spra1NR42qnPjLf6NGzW9XX3VCNavKhF4+yQ4cOFEbG2cVrrNfqbRC
J06crWvWrNGmpiVaU+MLcrWJerGOHXvMVtph9Q0bNlVFllZcX0mqVDv+wq9cWIvnfTGvJrMbEvFo
36ZJk+Zoc3Nzu+c4YsTxOnDgRBVp0Ew0mlPbvc3VyFqrwnU6dOgkHThwstbUTFH7+l1RRXYz1Bb9
Ze3aNWHCTG1sdIJ0hOYvd18M51aRW1Fzt1zbf4nP0fZf335P0+g98cQTOnToZDWS4+2cpXCKTpgw
Uz/ykY+lc9OrPJ812l4b5ASpI1LUokZCXNvo2qEi6ZuhcKC21yguKrSjuKgXNZttCienY4sL11cj
HsdXXL9Y25Mdq1dkuQ4YMEPLyUWlPJxUTNCs/TtSs7au8t0sPpeWJIfDK2TlxGR+kluQk53fqSAn
gV6C7dHA7AxNUENDR6p3mxwbGmZVva6SJJk2xb/829cjctMWwrUtImYakeoTdam0QpualnTYDq9v
zZo1FcSlLU3aR1QsKK3a/gu8uKBUW+DOV1OZly9MTkCcZG2tj9WeY0tLiy5Y8HGtr5+iNTVTtKZm
ug4ceIgOHTq1oGXxxW2u1tVN1gULPrGl3tbWVh0x4nitTmJWKMzU/v0Pqdouu/cira3dTzNZcM3W
ZDUNTXl/RZaWEaNS6XCtrd1fS6V9NX91z1DTJk1SkcN1zJiZZbIoPr+RI09o16YJE2amBbea1mdx
xfGW9NyuqyIDI0VOemy87psW8I4W+iJ5aFGYWuV+voDP1fr6abpgwSJtbJyViLG3oZqJ0us8Vevr
p+mIEcdrXd0BFWbcPKbKTZjViIzXWRzLbgp0AlhsQ5EoWdvbawSL9T6kQU7ejE4FOQkEqqJjn5f2
RKAjuA+LLSRFE4NPbDdpY+OsdotzR+RqaxoR96HpqB2V9VSShAULFpWZCbYecwAAD7JJREFUyhoa
ZlcxbbVpe1OCT+hz0iS/daKwrT52RqZb05Z15NtkZLPYNtc4LVFo3kI2tyb7pqbF7cjCn/70p60S
rvbtXbyl7Lhxs7Zo97bV52rt+chHztFSabxWan1EbtB+/Q5IxM2PNyucqrW1jdq//6FaWzu5QzPn
yy+/rLW106s85/y8+/c/dEs/Ro8+Svv1a68tKZWW68SJs9sRrrFjZ+iAAYdqTU2jiuxf5boVZT5h
WyPu5e9pdZNnqbSigmC4BmlNIijV380JE47VlpYWPe001zxVk8UVQU7elE4FOQkEqmJHiUBHdS1Y
sKjsy9++Jtsv2p2pa3u0D9tCtYXPj1UnaJ0x9WiZvDpD5N4otkV22vcl92F729jRvbpau6fanvAU
NWTbcnjfWhvaO1WXP9dKMre949Kvc3+t7b2u2P/y99S1NtO1tnb6FvJ12mmLOiAxrg1yTdjh7d7N
lpaWpPWp1JDdpA0NYdYJchIIdDF2NhFQLf+SfqN4Mx2ZVTsiaNUcSLdlApu97Zu9ydiZZLOnYmeQ
Jscb0Ry+Ea3YjmBr/mbFMtsiMWedtbhDLVZH97jrrru6nZyI2mLepyAihwErV65cyWGHHdbdzQkE
eixU9Q3nrOmNWL9+PRde+CWWLbuHzZv7U1PTwoYN63j55c/S1nZcKvVeLEdFdYwa9R6eeebH3S6/
yr7U1b3C/Pnv4NJLz93uBIl9HevXr+fII0/k8cfPoa3tXXhCwVLpFhobr9ju/Eddha29px09/09/
+mMMGjRoh+6xatUqpk2bBjBNVVdt9cI3CUFOAoHALg2flCsn+bVr/0Br66O03yoAQGlomMPq1Xd0
dXO3il2VbG4P+jKZ21nPP8jJm4QgJ4FA4I1AVTn77Iu5+uoj0xd2OUqlmznzzAe48sqLu75xgZ2G
IHPV0RPISaSvDwQCgQqIyE7biTvQcxHEpOciyEkgEAhUwc7ciTsQCGwfaru7AYFAINBT4RtUXnll
mAACga5EaE4CgUCgEwhiEgh0HYKcBAKBQCAQ6FEIchIIBAKBQKBHIchJIBAIBAKBHoUgJ4FAIBAI
BHoUgpwEAoFAIBDoUQhyEggEAoFAoEchyEkgEAgEAoEehSAngUAgEAgEehR6FTkRkTNEZLWIbBKR
+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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[11]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Plot the results</span>
<span class="n">final_embeddings</span> <span class="o">=</span> <span class="n">trained_word_vector</span><span class="p">[:</span><span class="n">vocabulary_size</span><span class="p">,</span> <span class="p">:]</span> <span class="o">+</span> <span class="n">trained_word_vector</span><span class="p">[</span><span class="n">vocabulary_size</span><span class="p">:,</span> <span class="p">:]</span>

<span class="k">def</span> <span class="nf">plot_with_labels</span><span class="p">(</span><span class="n">low_dim_embs</span><span class="p">,</span> <span class="n">labels</span><span class="p">,</span> <span class="n">filename</span><span class="o">=</span><span class="s1">&#39;tsne.png&#39;</span><span class="p">):</span>
    <span class="k">assert</span> <span class="n">low_dim_embs</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span> <span class="o">&gt;=</span> <span class="nb">len</span><span class="p">(</span><span class="n">labels</span><span class="p">),</span> <span class="s2">&quot;More labels than embeddings&quot;</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">(</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">18</span><span class="p">,</span> <span class="mi">18</span><span class="p">))</span>
    <span class="k">for</span> <span class="n">i</span><span class="p">,</span> <span class="n">label</span> <span class="ow">in</span> <span class="nb">enumerate</span><span class="p">(</span><span class="n">labels</span><span class="p">):</span>
        <span class="n">x</span><span class="p">,</span> <span class="n">y</span> <span class="o">=</span> <span class="n">low_dim_embs</span><span class="p">[</span><span class="n">i</span><span class="p">,</span> <span class="p">:]</span>
        <span class="n">plt</span><span class="o">.</span><span class="n">scatter</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">y</span><span class="p">)</span>
        <span class="n">plt</span><span class="o">.</span><span class="n">annotate</span><span class="p">(</span><span class="n">label</span><span class="p">,</span>
                    <span class="n">xy</span><span class="o">=</span><span class="p">(</span><span class="n">x</span><span class="p">,</span><span class="n">y</span><span class="p">),</span>
                    <span class="n">xytext</span><span class="o">=</span><span class="p">(</span><span class="mi">5</span><span class="p">,</span> <span class="mi">2</span><span class="p">),</span>
                    <span class="n">textcoords</span><span class="o">=</span><span class="s1">&#39;offset points&#39;</span><span class="p">,</span>
                    <span class="n">ha</span><span class="o">=</span><span class="s1">&#39;right&#39;</span><span class="p">,</span>
                    <span class="n">va</span><span class="o">=</span><span class="s1">&#39;bottom&#39;</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">savefig</span><span class="p">(</span><span class="n">filename</span><span class="p">)</span>
        

<span class="n">tsne</span> <span class="o">=</span> <span class="n">TSNE</span><span class="p">(</span><span class="n">perplexity</span><span class="o">=</span><span class="mi">30</span><span class="p">,</span> <span class="n">n_components</span><span class="o">=</span><span class="mi">2</span><span class="p">,</span> <span class="n">init</span><span class="o">=</span><span class="s1">&#39;pca&#39;</span><span class="p">,</span> <span class="n">n_iter</span><span class="o">=</span><span class="mi">5000</span><span class="p">)</span>
<span class="n">plot_only</span> <span class="o">=</span> <span class="mi">500</span>
<span class="n">low_dim_embs</span> <span class="o">=</span> <span class="n">tsne</span><span class="o">.</span><span class="n">fit_transform</span><span class="p">(</span><span class="n">final_embeddings</span><span class="p">[:</span><span class="n">plot_only</span><span class="p">,</span> <span class="p">:])</span>
<span class="n">labels</span> <span class="o">=</span> <span class="p">[</span><span class="n">r_dictionary</span><span class="p">[</span><span class="n">i</span><span class="p">]</span> <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">xrange</span><span class="p">(</span><span class="n">plot_only</span><span class="p">)]</span>
<span class="n">plot_with_labels</span><span class="p">(</span><span class="n">low_dim_embs</span><span class="p">,</span> <span class="n">labels</span><span class="p">)</span>
        
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
6667TpL06KOP6re//a1OnjwpX19fzZ49W7NmzdL48bU9kXv16qU5c+boD3/4g/74xz/+7OdNmzZN
N998c+M/GBrN6ZeJFhSkq7raVO1ObKdstgwlJv76y0QBAGgJ2JENAAAAwJLCwsJUVVWlxYsX68sv
v9Qrr7yiF198sc6c9PR05eXl6fnnn1dpaan+9Kc/KT8/30sV119kZKTnuHv37pLkabNSXFysOXPm
yN/f3/Nzelf3jz/++LNrnupL2ahOtzHZtWvXBd9zvhdenunMNim4uJeJAgDQEhFkAwAAAC3Qr4WE
VvFLbUGioqK0cOFCLViwQJGRkcrJydG8efPqzBk2bJiWLl2qxYsXa9CgQSooKPjF3clWd2abldN/
NjU1NZKk48ePa/bs2SouLvb8fPrpp3K73Wrfvv3PrtmxY8fGLVqN0+Ll4MGDGjVqVIOu2ZzZ7Xbl
5a2R2+1Wbm6u3G638vLWyG63e7s0AACaBK1FAAAAgBZo9erV5/Se/jl79+5VSEiIPv7443NevNjY
1q9ff87Y6tWrPccZGRnKyMioc33cuHF1zu+++27dfffddcamTZvWcEU2Al9f3zovabwQ0dHR+uc/
/6nQ0NALvqchw+X8/Hw9/fTT+vTTT2Wz2TRixAgtXrxYISEhCg0NlWEYGjRokCQpPj7+vP9sL0ZQ
UFBDlN3iOBwOWokAAFoldmQDAAAALVCXLl0ueCduc3xh4pncbrfWrl2rkpISb5dywXr37q0PP/xQ
e/fu1bfffquamhqZpnnOvDPHnnjiCa1cuVJz5szR559/rj179ui11177xR3o51vzUv3www+aMWOG
XC6X1q9fL5vNpltuuUWStH37dpmmqfXr1+vgwYN66623LmjNmpoaPfLII+ratau6d++u2bNne66d
2Vrkp59+0kMPPaQePXqoQ4cOCg0N1fz58xvs2QAAgPURZAMAAAAt0JmtRUJCQvTss8/qvvvuU0BA
gHr16qWlS5d65p7e4Tto0CD5+PjohhtukFQbgs6ZM0c9e/ZU+/btNXjwYEv1n66oqFBKymj17dtX
qampCg8PV0rKaB05csTbpf2qhx9+WDabTREREQoKClJ5efl5f5lw5lhSUpLeffddvffeexo6dKhG
jBihzMxM9e7d+7zzz3deH2PGjNHvfvc7hYaGKioqSkuXLtWuXbv0+eefe15aedlllykoKEhdunS5
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
nTqVuLg4du/ejUaj4eWXXwbg2rVruLi4EBgYyLVr15g2bRqHDx9GCMHu3bu5du0aP/74IwAbNmwg
ODiYBQsWcPbsWebPn09QUJCSX7bQ9OnTCQgIICEhAW9v7zK19WEqIi97SXJycvD39+eZZ57BxMSE
5557jqNHjwJ/H/Pdu3fTuXNnateujbu7O1qttsS69u3bh6GhIWlpaXrlkydPLneakMpS2muZpaUl
Go0GMzMz7OzslHQ4ly9fxt3dHRcXF5o0aYKvr6/Ss/W//w3HxsaYglRDjZWfanUy3t6+Rd77Ffu3
lKTyqMyURUlJSdjb29O1a1fs7OyoW7fuI323K8rc3Fzvc0uSJKkqyUC2JEmSJD2iwrzQkyZNwtLS
EltbW4KCgpT5N27cwM/PD2tra2rXro2vr6/eP8uhoaFYWVmxdetWnJ2dMTExwcfHhytXrijLlPQY
Z+Gj1w+yYcMGOnfujIWFBfb29gwfPlx5vDslJYXnn38eKHicXKPRMHbsWGV/ij5+Wtr279ixg8OH
D7N27Vr69u1LampqeQ6ndJ+alpt33bp12NracuTIEfz9/XnjjTcYPHgw7u7uHD9+nD59+uDn56cE
TV988UW6du3KyZMn+eqrr1i9ejXz5s1T6gsMDGTfvn1s27aNHTt2EB0dTVxcnN42ExMTSUtLY/Pm
zZw6dYrBgwfzyy+/IITAwcEBKysrDA0Nad26NZs3b2bnzp2cPHmS1q1bs2fPHjIzM3F2dmbdunWE
hIQQEhJSxUet+pTnBkhJ6YXKk8Ji0KBBvPzyyzRt2pS2bduyatUqTp06xa+//oqdnR0GBgaYmZlh
a2uLqakptra2AFhbW2NnZ4elpSUAwcHBLFq0iJdeegkHBwdefvll3n333WKpiwICApRlnnnmmTK3
90H+KWVFedNwTJs2jfDwcNavX8/x48dp3rw5Pj4+eilxZs6cyZIlS4iLi8PAwEC5gXG/5557jmbN
mukF9/Py8ti0aZNyba9uFXUt8/f3Z+7cufTo0YPg4GBOnTqlzLOysiIxMYEePYoOVnmCF17ozqZN
YZX2t5Sk8qisNDdjxozB39+fS5cuoVaradq0qd51/cMPP8TNza3Yem3btuXjjz9Wpt98802MjY1R
qVQYGBjw7LPPcufOHb3vpNevX8fe3p6FCxcq6x08eBAjIyP27NnzSPshSZJUokft0l3VL2RqEUmS
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
k5SUlMfdlceGt7e3TJo0yaQsODhYhg0bJj///LN4enpKpUqVpHfv3hIfHy/5+fl6PU3TZMmSJSbb
Ojk5yZw5c/Tl+fPnS/369aVChQpiZ2cnVlZWUr58eX390KFDJSQkRF+OioqSl19+WV/evXu3WFhY
yKlTp0REpHr16vKf//znwRz8YyQtLU0AgVgBKfGaK4Ckp6c/7i6WSsn7wK3XzunTpyU8PFxsbW3F
2dn5jmWlkZ2dLRERkTfHpOgVEREp2dnZD6XvIiKJiYliMBhk/fr1ellCQoIYDAa5fv26iBRdn0aj
UbKysvQ6OTk5YmlpKfPnzxcRkcaNG8u7774r7u7u8vnnn4uIyOzZs2873sWLF4vBYNCXn332Wenb
t69JnQYNGoi9vYOYmZW5eS20EygrBoOzREREiojIq6++Kh07dtS3ycrKeuhjdyvffPPNzX1tuOX6
PSGAJCQkmNSPiIi8eUyxN+vEiplZGf2YHjdhYWHy9ttvy9tvvy2Ojo7i6uoqn3zyib7+woULEhER
IYBYW1tLixYtJCMjQ19/6/keOnSoBAcH6+9v/R7esGFDqd8/+/fvl1atWomDg4PY29tLw4YN9e/L
HTt2SNOmTcXV1VUcHR2lUaNGsmvXLpPjKO2erFAoFAqFQvFPJDk5ufh/35pyn/ryY7MWEZGjwGng
+eIyTdMcgGeArY+rXwqFQvG4mDRpEnXr1qV3796cPn2aX3/9FXNzc1q2bMkzzzxDamoq06ZN49tv
v2XkyJH6du+//z6bNm1i2bJlrF69msTERJKTk03azsvLY+TIkaSmprJkyRKOHz9u4lvco0eP26IA
Z82aRaNGjfDx8Xmox323yF0m9LrVo/mfhMFgKJ7U1Sk+Xg8PD9LT0/nyyy+xsbGhT58+NGzYUPe4
1jTtjtsCbNu2jc6dO9OqVSt++OEH9uzZw0cffcSNGzfuun/BwcFUr16dmJgYdu3axYEDB+jWrdtf
PdwnhgftC/04fLZ37tzJv/71L315woQJnDlzhtTUVNLT0+9YVhqPyiN+27ZthISEmJSVtMtxc3MD
4OzZs3qZl5cXZcqU0ZczMzPJz8+nXr16QFF088SJEwkNDeXgwYN33PfJkycB9HOUlpZGnTp1TOqE
hobi4+NdIvHr98A5mjatq3s7u7m5mfTPNLL/BBCrJ4d80BTb4fx+3hsBLYFiO5zb7WAedjLPB0VM
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
jIwICgqiS5cuREVFsXPnTvT19ZEkiUuXLjFmzBgUCgWdO3fm9u3b3Lx5k0aNGrFgwQJsbW2ZOXOm
fF1at24tn8/TBm0ARo0axcCBA2ndujXffvttqYPUZSEiIgItLS0SEhIICwsjNDSUxYsXAzBs2DAO
HjzIunXrOHbsGN27d6ddu3ZylGh8fDyfffYZQUFBVKxYkdq1a7Nw4UI0NTXlaF89PT0++ugjTE1N
SUxMpF27dnTs2FFOf1NUzHDFihV89NFHHD16lKFDh7Jjxw6qV68u97PoZ6Qoiv/RFB4qlUrtKYWi
/hXPsQ2FUd0DBw5k9OjRcjqFuXPnoqGhobbvmjVrOHr0KGfPnuX27dtUqFABKCySeu/ePapUqUKn
Tp3Yu3cvmZmZ7Nq1i8DAQC5cuPDSn8mTPK6QZ1RUFM2bN2fAgAHUqVMHX19fsrOz5e9mmzZt2Lx5
M3/88QcuLi64uroyZ84crKysXmt/hZdT8j59D8hQu08rFIpSn+54+PDhU1NVAXTo0IGCggK2bNnC
X3/9xZ49e/Dz+29y81nT0pRWFPZJhWJfpN2idp5U8FYQBEEQBEGg8B99b9MLcAakxMRESRAE4Xnk
5ORIXl7eEiC/vLy8pZycnLLumlCKqKiofz+nbAmkYq9sCZCioqIeu29ZfNanTp3691grivW1QIIP
JEBq166d9NNPP0nXr1+Xbt++LSkUCklXV1fS09OTX5UqVZKqV68uSZIkDR06VHJ3d3/s8UxMTKRl
y5ZJ7u7uUlBQkCRJkjR37lxJR0dH6tatm3TmzBkJkObPny+dPn1aOn36tJSXlycZGhpKdevWlYKC
gqTOnTtLAwcOlNtUKBTSl19+KSmVSumff/6RMjMzJYVCISUnJ8vb7Nq1S15fJD09XZozZ47Upk0b
qVKlStJvv/32qi/vc3F3d5fq1auntmzcuHFSvXr1pOzsbElTU1O6ePGi2npPT0/pq6++kiRJknr2
7Cl16NBBkiRJ+vrrryVTU1OpadOmkoGBgZSUlCSFh4dLy5Ytk65duyZVqVJF6tq1q3T48GHJzs5O
6tu3r5SWliZJUuFnVKFCBWnt2rXSqVOnpLFjx0qAFBISIkmSJF/fpk0/VvuuAtLmzZslSZKkpKQk
SVNTU5o6daqUlpYmRURESDo6OtKyZcvkvltZWUlz586VcnNzJX9/f0lPT08CpP79+0seHh5SUFCQ
fCw3NzdJX19fqlatmqSnpycZGxtLkZGR0q5duyRNTU0pODhY8vHxkUxMTCRNTU3J1tZW+vTTT6Vb
t269ng9LeG897T5d9L0uTqFQSBs3bpS++uorqW7dumrr5s+fLxkaGqot69evn9S1a1dp5syZkkql
Ulvn5uYmDRo06Il9LDpekczMTEmpVD7xnvgi7UqSJBkZGUmRkZGSJEnSvn37JKVSKf59IgiCIAjC
OyExMbHo33vO0kuOC4vUIoIgvDeMjY2Jjt5Ceno6GRkZ2NraikjscuxlUoSUxWddes5XJRAFWGBi
YkJ4eDhff/01mzZtAgrTR7i4uKi1UxRBq62t/dRjKhQKKlSoIKfEkCSJihUrcuLECSwtLVEoFNSq
VUstX3DxwppSKVGNpR3jaWxtbQkMDCQwMBBfX1+WLl1Kp06dnrrf69SkSRO1966uroSGhnLs2DEK
Cgqwt7dXS9Fx//59uWjkqVOn6NKlCwBTp06latWqhISEcPPmTdq1a4ezszNBQUFMmzYNfX19Nm7c
KBdnu3v3LpMmTQIKo7JdXFwIDg7mypUrqFQqbGxs1I4rSRIHDqRQGJXaHIgG/sfkySG0b98eJycn
1q1bx4QJEwgJCaF69eqEhISo5dgu+ox0dXWJjIwkMjISDQ0NfHx86NixIwBZWVkoFAoWLFiAo6Mj
kZGRBAUFkZOTI7ezfv16pk6dyp9//omBgQE+Pj6sX7/+VXwcr1VaWhqnT58W9/S3TPH7dLdu3XB2
dpbTAz3N0KFDmTNnzmNTVRXx8/OjQ4cOnDhxAn9/f7V1L5qWpvjPb2nLXkW6m6L79++//463tzfa
2toliqEKgiAIgiC8j8RAtiAI752iXJtC+ZWTk8OIEUEUDgQPo3DytgUQh4ZGIJ6ez5Yi5E1+1k8b
eJ84cSK1a9fG0tKS+Ph4atWqxenTp+nZs2ep7Tk6OrJ48WJu3LiBkZFRifV169Zl7969WFlZcfDg
QbKysoiNjZWL9fXs2VNOLRITE8PatWvl1BpFVCqVXPyxyKlTp9TeP2nQ5u7du4wePZpu3bphbW3N
uXPnSEhIoHv37k+4UmXr9u3baGpqkpSUhFKpnmGtKC/0owP8w4cP5+HDh0yaNIlLly4BMGTIEHbs
2MGcOXOoXbs22tradO3aFQ8PDzmthUKhoF27dmzdulVuy8nJSU4fcO/ePQAePlzAf9+ZwYA2CQl9
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
pk2bUr9+fVauXMn58+f57bff5P3z8/PZvHkzDx8+pFOnTkRGRhIfH89PP/3EX3/9pXashg0bEh0d
zdChQ2nevDlHjhxh3LhxJfrUr18/vLy8sLKywsXFhTlz5rB161by8vLUtps6dSqtWrXC2tpaHjAS
hPdNYTHkKAoKwgA/wBzwo6BgLjExUe98mpEPP/yQVq1a8cEHH9CjRw8WLVrEjRs3uHXrFhcuXKBp
06Zq27u5uZGamgpAcnIyTk5OGBoaPvU4eXl5nD59moEDB6qlRPvmm284e/bsE/ft168f6enpHDp0
CCh8mqVHjx5oa2u/4FkLgiAIgiAIjyMGsgVBeG7u7u48fPhQHrQ2NjaWIzRtbW0B9QjN5s2b4+zs
rBahaWRkxC+//EKrVq1QqVT8+OOPrFmzRh7IDg4ORkNDA5VKhZmZGefOnSu1L4JQ3Lhx45g5cyYT
J04kNTWVVatWUbVqVfLz8/Hy8sLQ0JD4+Hji4+PlvO35+fny/rGxsZw5c4Zdu3axbNkyIiIiiIiI
AOCXX36hVq1aTJ06lUuXLnHx4kWg8NH0vLw8Zs6cyeLFizlx4gRmZmbcunWLfv36ER8fz8GDB7G3
t8fb25vbt2+/sevRpEkTtfeurq6kp6fz559/oqWlhYuLi7zOxMSEOnXqyINAAJqamkVFOQCoU6cO
RkZGats8r8TERDp27IilpSUGBgbyfSQ7O1veRqFQqB1XEN5XRWkyoPkjawqffsrIyHij/XnTlEol
27ZtIzo6mnr16hEeHo6Dg4M8uPxoehdJkuRlzzOQnJubCxTmyC5Kh5acnMzx48fZv3//E/c1NTWl
Q4cOLF26lCtXrrB161YGDhz4PKcpCIIgCIIgPCPNsu6AIAjlj4eHB05OTo99ZHr27NnMnj1bbVlp
kaZFEZqlcXNzIzY29rF9sLOze2Je3Kf1UXj/5ObmEhYWxoIFC+jdu/CRe2tra5o2bcrKlSuRJIkf
f/xR3n7x4sUYGxuza9cuPD09gcLB3Hnz5qFQKLC3t6d9+/bs2LGDgQMHYmxsjIaGBnp6epiZmakd
Oz8/n++//54PPvhAXubh4aG2zcKFC1m7di1xcXF4e3u/rsvwUooPAhUpLQ9w0TKlUokkSaSlpXH6
9GlsbW158ODBY9vPy8ujbdu2tGvXjlWrVmFqakpWVhZt27bl/v37atvq6uq+gjMShLdb7dq1//3b
bgojsovEAciTx+86V1dXXF1dGT9+PJaWluzYsYOaNWuyd+9ePv74Y3m7ffv2yalDHB0dWbx4MTdu
3HjqUx1mZmbUrFmT06dP07Nnz1K3qVChAlB68dlBgwbRs2dPatasia2tbYlJREEQBEEQBOHVEBHZ
giAIQqn69+9Ply5dXmmbWVlZKJVKUlJSXmm7AKmpqdy/f5+WLVuWWJecnEx6erraI+OVK1fm3r17
xSIeoV69emoDt9WrV+fKlStPPXaFChXUBrEBrly5wuDBg7G3t8fIyAhDQ0Nu376tFnn8uh04cEDt
/f79+7Gzs0OlUvHgwQMOHjwor7t27RppaWmoVCp5WX5+PocPH5bfnzp1ihs3blC3bl0A9PT0iI3d
pVaEbuXKVWpR7sWdPHmSnJwcpk+fjpubG/b29ly+fPlVnrIgvFPs7e3x8vJGQ2MEhTmyzwEr0NAI
xMvL+53Pv37o0CGmT59OYmIi586d4+eff+bq1auoVCqCg4P59ttvWbduHWlpaYwbN47k5GQCAwMB
6NWrF1WrVsXHx4d9+/Zx9uxZfvnlF7X7XnFFhR7Dw8NJT0/n+PHjREREyBP3ZmZmaGtrEx0dzZUr
V9SKUxc98fPNN9+IIo+CIAiCIAivkYjIFgSh3Cge1VkW/zl/+PAhCoWi1AjU91FYWNhryU3+uq7v
kx4jz83NpVGjRqxatarEORUV8ALQ0tJSW6dQKHj48OELHdvf35/r168THh6OhYUFFStWpEmTJiUi
j1+nc+fOERwczP/+9z8SExOZN28es2fPxtbWlk6dOjF48GAWLlyInp4e48aNw9zcnI4dO8r7a2pq
EhAQwNy5c+W/N23aVE77ER+/n3/+uQEMAXyB2dy48RsnTvxZan8sLCyoUKECYWFhDBkyhGPHjhES
ElJiO5ETXxD+s3r1Cnr16k1MTB95maenN6tXryjDXr0ZBgYG7N69m7lz53Lz5k0sLS0JDQ3Fy8uL
Nm3acOvWLYKDg7ly5QoqlYrff/9djmLX0tLijz/+4PPPP6d9+/bk5+ejUqmYP39+qccaOHAgurq6
zJw5kzFjxqCrq0v9+vUZOXIkABoaGoSHhzNlyhQmTJhAs2bN5ALVCoWCfv36MX36dPr06VNq+4Ig
CIIgCMLLExHZgvCey8vLw9/fH319fWrWrFkiVcf9+/cJDg6mVq1a6Onp4erqSlxcnNo28fHxeHh4
oKuri4mJCe3ateOff/4BCgekpk+fjo2NDTo6Ojg5OfHzzz/L+8bFxaFUKmnUyEUtqrNlS0/WrVuH
SqXC0NAQPz8/7t69q3bc/Px8AgICMDIywtTUlAkTJjxX3yMjI0st0icU0tfXx8DA4JW3+7oGKYsK
PO7YsaPEOmdnZ9LT0zE1NcXGxkbtpa+v/8zHqFChQqmPlZdm3759jBgxAi8vL+rWrYuWlhZXr159
5mO9Cv7+/ty5cwcXFxcCAgIICgpi0KBBQGGRyoYNG9KhQwfc3NxQKpVs2bJFLmIJhek9xo4di6+v
Lx9//DH6+vqsWbMGKJx4SkxMALoAG4FOgA3Qmpyca3IRuuITF1WqVCEiIoINGzZQr149Zs6cyaxZ
s0r0W0wmCcJ/jI2NiY7eQlpaGlFRUaSlpREdvQVjY+Oy7tpr5+DgwNatW7l06RJ5eXmkpqby2Wef
AYX3ia+//prs7Gzu3r1LUlISrVu3Vtvf3NycdevWcf36dW7dusXBgwdp1KgRABMnTiQpKUlt+549
e5KUlMSdO3e4evUqsbGxdOrUSV4/YMAAMjMzefDggTyIXeT8+fN4e3tTtWrV13EpBEEQBEEQBMRA
tiC894KDg9mzZw+///4727ZtY9euXSQmJsrrhw0bxsGDB1m3bh3Hjh2je/futGvXTk7HcPToUTw9
Pfnggw84cOAA8fHxdOjQQR7smzZtGitWrODHH3/kzz//JCgoiD59+rBnzx75GJIkkZh4BJgERAPV
iI2NY9iw4axZs4aoqCi2bdtGeHi4Wt8jIiLQ0tIiISGBsLAwQkNDWbx48TP3HSi1SN/7ZsOGDTg6
OqKjo0OVKlVo06YNd+7cKZFaxMPDg8DAQMaOHUvlypWpXr06kydPVmvr1KlTfPzxx2hra/PBBx+w
Y8cOlEolmzZteuzxjx8/jre3N/r6+lSrVg1/f3+uXbv23OdRsWJFxo4dy5gxY1i+fDlnzpzh4MGD
LFmyBD8/PypXrkynTp3Yu3cvmZmZ7Nq1i8DAQC5cuPDMx7CysmL37t1cuHDhqX20s7Nj+fLlnDx5
koMHD9K7d290dHSe+7xehpaWFvPnz+fGjRtcvXqVKVOmyOsMDQ2JiIggJyeH3NxctmzZUiwf7398
fHzIyMggLy+P6OhoatWqBRQvQjcHuADkAP8HLAL+K0K3c+dOtQmyTz75hNOnT5OXl8fevXtp3749
BQUFODo6AtCiRQsKCgpeyySKILzN7OzsaNeu3TufTuRtkpaWxs8//8zq1atZtWoVI0aMKOsuCYIg
CIIgvNPEQLYgvMdu377NkiVLmDVrFu7u7tSrV4/IyEh5EPrcuXNERESwfv16mjZtirW1NaNGjcLN
zY2lS5cCMHPmTD766CPCw8OpX78+devWZejQoZiYmHD//n2mT5/OkiVL8PT0xMrKCn9/f/z8/Pjh
hx/kYxQaA0wEvICRQAFXr/6NtrY2bm5udOvWrURxSAsLC0JDQ7Gzs6NXr14EBATIuSyzs7Of2nf4
r0hfkyZN5Ije98mlS5fw9fVl0KBBnDx5kri4OLp06fLYdBrLli1DT0+PQ4cOMXPmTKZMmSJHQEuS
RKdOndDX1ychIYEff/yRr7766onRtf/88w+tWrWiYcOGJCUlERMTw5UrV/jkk09e6HwmTJjA559/
zsSJE1GpVPTs2ZO//y78Hu3ZswcLCwu6du2KSqVi8ODB3Lt377kGTKdMmUJmZia1a9d+6qTHkiVL
uH79Os7OzvTt25fAwMAS+7zNkcfqReiKe7EidGlpaWzdulWO5BbePx4eHowaNQooLNQaFhYmr3va
hJggvEk5OTm0bdueOnXq0K1bN3x9falatRpOTk5l3TVBEARBEIR3msiRLQjvsdOnT/PgwQNcXFzk
ZcbGxtSpUweAY8eOUVBQgL29vVo6iPv378t5hZOTk+nRo0ep7RdFcbZu3Vpt/wcPHuDs7AxQLBq2
+MBlVUAHuE1GRgZ2dnZUrVqVhIQEtfabNGmi9t7V1ZXQ0FAkSeL48eOP7XuVKlXk96UV6XufXLx4
kYKCAjp37oy5uTlQWPDwcRwdHRk/fjxQOJA5b948duzYQatWrYiJieHs2bPs2bNH/n588803JR71
Lm7evHk4OzszdepUedmiRYuwsLAgIyPjuQdDAb744gu++OKLEsvNzMzUJjEeVdq6oomRIo0bN+bI
kSNqy/r27Uvfvn1L7Pvhhx+WKCr2aPHMZ01T8iJe9yB5URG67dtHUFAgAS2AODQ0AvH0fPYidDk5
Ofj69iEmJkpe5uVVmP/3fUidIJTu8OHD6OrqlnU3BKFUvr592L79AIUFOJsDuzl3bgS9evUmOnpL
GfdOEARBEATh3SUGsgXhPVY0wPu4Aa/c3Fw0NTVJSkpCqVR/gENPTw94eoE9gKioKGrUqKG2rmLF
igDFlh8EHP/9+3/9KRrIfNaie8/T96f1/33w4Ycf0qpVKz744AO5eFa3bt0wMjIqdfui9A9Fqlev
zpUrV4DCiFpzc3O14onFJ0lKk5yczM6dO0vkqVYoFHLhz3fFmy5m+mj+1uf1uAH64l5FEbrSBoS2
bxcDQu+7ypUrl3UXBKFUaWlp/068rQD8/l3qR0GBRExMH9LT00X6F0EQBEEQhNdEpBYRhPeYra0t
mpqaHDhwQF52/fp10tLSAHByciI/P5/Lly+XKJBXlCLB0dGx1OJ6ACqViooVK5KVlVVi/5o1awLI
UcBK5VgK/1N4DtgH5OHl9eSozuL9Bti/fz92dnYoFAqcnJwoKCh4Yt+Fwsf1t23bRnR0NPXq1SM8
PBwHBwcyMzNL3V5LS0vtffEJBkmSnjsKODc3l44dO5KSkkJycrL8Sk9Pp3nz5i90TuVN8UfQi4qZ
tm3bnuvXr5d1117ayxahKxoQKigIo3BAyJzCAaG5xMREiTQj77FHU4s8auLEidSoUYPjx48Dz1aY
WBBehf/qAzz6O6oF8F99AEEQBEEQBOHVEwPZgvAe09XVZeDAgYwePZrY2FiOHz9O//790dDQAAoL
S/n5+eHv78+vv/5KZmYmhw4dYsaMGWzduhUoTOOQkJDAsGHDOHbsGCdPnmThwoXk5OSgp6dHcHAw
QUFBLFu2jDNnznDkyBHmzZvH8uXL5X4oFAo8PBoBfQAL4Ec0NTWfGtV57tw5goODSUtLY/Xq1cyb
N4+RI0fKfff19X1i34X/uLq6MnHiRI4cOYKWlha//fbbc7fh4OBAdnY2f//9t7zs0KFDT9zH2dmZ
EydOYGlpWWLC4V2JllePOM4GVrB9+wF69epdxj17dV60CN27MiD0v//9j8qVK6NUKjExMZHzPD+L
yMjIpw78T548WeTeLSYgIIDly5cTHx8vp4Z6luK+wpMVz1EuPN5/9QEsgZRia16sPoAgCIIgCILw
7ERqEUF4z3333Xfcvn2bjh07oq+vz+eff87Nmzfl9REREYSEhBAcHMz58+epXLkyrq6udOjQASgc
wNq2bRtffvkljRs3Rltbm8aNG+Pr6wvA1KlTqVq1KjNmzODMmTMYGRnh7OzMl19+KR9DoVDwyy8b
uHz5MhkZGaSkpPDtt98+cXBHoVDg7+/PnTt3ujYa1AAAIABJREFUcHFxQVNTk6CgIAYNGvTMfRcK
B5p37NhBmzZtMDMz48CBA1y9epW6deuSnJz8XG21bt0aGxsb/P39mTlzJjdv3uTrr79GoVA8NlJ7
2LBhLFq0iJ49ezJmzBhMTExIT09n7dq1LF68+K0uhgjiEfSnUS8Y6VdszdszIBQdHc2yZcuIi4vD
2toapVL53JMwz/I9f9t/Fl6FBw8e0Lt3b44ePcq+ffvk9CNFhYnPnTtHtWrVABg1ahRbt25l6dKl
hISElGW3hXeMvb09zZt7sHt3LLAZMOZF6gMIgiAIgiAIL0CSpLfqBTgDUmJioiQIgiC8nNTUVKlt
27ZS1apVJW1tbcnBwUFasGCBJEmS1K9fP6lz587yth4eHlJQUJDa/j4+PlL//v3l96dOnZKaNWsm
VapUSVKpVNKWLVskhUIhbdu2TZIkScrMzJSUSqWUnJws75ORkSF17dpVMjExkXR1dSWVSiWNGjXq
dZ72GxMVFSUBEmRLIBV7ZUuAFBUVVdZdLHNeXt6ShoaJBMv/vS7LJQ0NE8nLy7usu/ZMwsPDJSsr
qxfePyIiQjI2Nn7iNpMmTZKcnJxe+Bhvi48//lhycHCQdHV1JQ0NDalz586Su7u7FBQUJCkUCklD
Q0OqXLmy9Mknn0iGhobyvWf+/Pn//pwVvjQ1NSVdXV2pQoUKUs+ePeU2inv03mVlZSVNnTpV6tWr
l6SrqyvVrFlTmj9/vto+EydOlCwsLKSKFStKNWvWlAIDA1//RXmDSrtO75r79++/knaSk5PVvnOA
5OXlLeXk5LyS9surzMxMSaFQqP0Of1aTJk2SGjRo8Bp6JQiCIAhCeZeYmFj0byZn6SXHhUVqEUEQ
3itpaWls3bpV5N79l4ODA1u3buXSpUvk5eWRmprKZ599BsDSpUv55Zdf5G137txJaGio2v6//vor
S5Yskd/b29uze/du7ty5w4kTJzA0NEShUMiRtZaWlhQUFKgVjaxduzYbNmzg2rVr5ObmcuLECWbN
mvU6T/uNUY84Lu7tiTh+3VavXoGnZxP+Sy3UB0/PJs9VMLKs9O/fnxEjRpCdnY1SqcTGxqZEeoYX
yd08Y8YMqlWrhqGhIYMGDeLu3buv+1TKhdOnT3PhwgU2b95M1apVOX36NElJSfJ6bW1trl27hpaW
FkeOHGH8+PHcuXOH8ePHo1Ao2Lp1KytXrqRGjRq0a9eO1NRU5s6dK+//tNQZ//d//4eTkxNHjx5l
3LhxBAYGyjUgNmzYwJw5c/jpp5/IyMjgt99+o379+q/vYrxmeXl5+Pv7o6+vT82aNUvc22/cuIG/
vz8mJibo6uri7e1dLlP95Obm4ufnh56eHjVr1mTOnDlqn7O1tTUhISH07dsXIyMjPv30UwD++usv
PvnkE4yNjalSpQo+Pj5kZWWptb1o0SJUKhXa2tqoVCq+//57eV3R77ZNmzYRFRXFyZMnqVGjKm5u
bpw/f/7NXYAy8DJPh4gnSwRBEARBeFliIFsQhPfCu1xwrzz57bff2L59O1lZWWzfvp1PP/2Ujz/+
GGtr68fu8y5PLtjb2+Pl5Y2Gxgj+K2a6Ag2NQLy8vJ94Xd4XL1swsiyFhYUxZcoUatWqxeXLl0lI
SCixzfPmbl63bh2TJ09mxowZHD58mOrVq7NgwYLXfSplLjc3l0uXLtGiRQvc3d2pUKECfn5+FBQU
yNvo6Ojg6urKzz//zKFDh7C2tmbFihVywVl9fX18fX1ZuHAhv/76K/r6+s9V3NfNzY3Ro0dja2vL
8OHD6datG7NnzwYK05dUr16dVq1aUatWLRo1asTAgQNf7UV4Dv3796dLly4vvH9wcDB//PEHeXl5
/PLLL+zatYsDBw7I37W+ffuSlJTE5s2bOXDgAJIk0b59e7XPozwICgpi//79bN68mT/++IM9e/ao
TX4AzJo1iwYNGsiTH/n5+Xh5eWFoaEh8fDzx8fHo6+vTtm1b8vPzAVi5ciWTJk1i+vTpnDx5kmnT
pjFhwgS1+h5QODnbqlUrvvjiC1JSUti7d69czPpdFBcXx8OHD/n444+pUqUKHTp04MyZM/L68+fP
06tXLypXroyenh4uLi4kJCQQGRnJ5MmTSU5ORqlUoqGhwbJly8rwTARBEARBeFuJgWxBEN4L70PB
vfLg1q1bDB06lLp16zJgwAAaN2782MKR7+LkQkxMDM2aNZOj/Dp06MD06SElIo4NDGD37lhWrVol
F/vbsmULDg4O6Orq0qNHD+7cuUNkZCTW1taYmJgQGBhYlGKLqVOnqkW1F2nQoAGTJk16k6f8yrxo
wciypK+vj76+PhoaGpiamso5m4tkZ2cTERHB+vXradq0KdbW1owaNQo3NzeWLl1aaptz585l8ODB
9OvXDzs7O6ZOnYpKpXoTp1Omzpw5gyRJVK1aVV5WqVIl6tSpo7Zdhw4dWL58OQMGDODnn3/m5MmT
ODs7qxUmrlWrFg8fPmT8+PHPVdzX1dW1xPvU1FQAunfvTl5eHtbW1vzvf//jt99+K9NB3bCwMCIi
Il5o39u3b7NkyRLCwsK4ePEijRs3JjIyUp4QyMjI4Pfff2fx4sU0bdqU+vXrs3LlSv76668XKgT8
uuTm5rJs2TJmzZqFu7s7KpWKpUuXlvhcWrVqRVBQENbW1lhbW7N27VokSeLHH39EpVJRp04dFi9e
THZ2Nrt27QJg0qRJzJo1i06dOmFpaYmPjw8jR45k4cKFcrsKhYJbt27Rvn17cnJyiI2NxcTE5E1e
gtdGkiRmzpyJnZ0dlSpVwsrKiunTp5OXl4dCoWDNmjXs3LkTpVJJo0aNsLGxQUdHB2traxISEti8
eTMpKSmMGTOGhIQE5s+fj6ZmYWkmFxcXDh8+zCeffEJKSgotW7bEwMAAQ0NDPvrooxITEYIgCIIg
CMWJgWxBEN55RQX3CgrCKCwoZ05hwb25xMREvZORwGWlT58+pKWlkZeXR3Z2NosXL35sZO27OLlw
+/ZtPv/8cxITE9m5cycaGhr069eP6OgtxMbGolAoMDc3Z8mSxaSmpuLl5QUUPuYfHh7OunXriImJ
ITY2ls6dOxMdHc3WrVtZsWIFP/zwAxs2bABgwIABpKamkpiYKB/7yJEjHD9+nP79+5fJuQslHT9+
nIKCAuzt7eVBb319fXbv3v3YiOzU1FRcXFzUlj06wPouKpqkKUo9UPTno8t1dXXp2rUrERER+Pv7
k56ejkKhkN8HBwfTqFEjJEni5MmTWFhYoFQq5XYePnzI2LFj2bJlC2vWrGHy5MkA5OfnM378eFJS
UuQ+3blzhzNnzrB7925q1arFokWLOHfuHH///Tc9evSgQoUKtGrVir///putW7eiUqkwNDTEz89P
LR1MaRNcxaNYs7KyUCqV/Prrr7Rs2RJdXV0aNGjAgQMHHnu99PX1MTAweKFrffr0aR48eICrq6sc
sW5sbCwXykxNTUVLS0vte2hiYkKdOnXkgf3HefDgwQv16UWcOXOG/Px8PvroI3mZgYFBicmPhg0b
qr1PTk4mPT1d7WeycuXK3Lt3j9OnT5OXl8fp06cZOHCg2jbffPMNZ8+elduRJIlevXqRl5dHTEwM
+vr6r/eE36Bx48Yxc+ZMJk6cSGpqKqtWraJq1aq0a9cOgFq1auHo6MjChQu5fv06M2fOZPz48Whq
anL58mXOnz+PjY0NnTt35quvvqJly5YMHTqUOnXqMGzYMExNTalYsSJ+fn6Ym5uTmJhIUlIS48aN
Q0tLq4zP/vWxtrYmLCysrLshCIIgCG81MZAtCMI7778Bo+aPrGkBUC7zfr7r3tXJhS5duuDj44ON
jQ2Ojo789NNPHDt2jD///FNOIzJmzBh8fHywtLSUo0/z8/NZuHAhjo6OfPzxx3Tr1o34+HiWLFmC
g4MD3t7eeHh4EBsbC0DNmjVp06aNWlTv0qVLadGiBZaWlm/+xIVS5ebmoqmpSVJSEsnJyfLr0dzN
j3of88jWrl2bChUqyANlZ86coV+/fvK9oKCgAB0dHXn77t27c/v2bTp27MjRo0e5f/8+EydO5PTp
0/z6669oamqyfv166tWrh6mpKRcvXgQgMjISHR0dzMzMaNSoEVOmTJHzYD/q8OHDau8rVKiAQqHg
ypUrrFixAkmSyMjIoEePHoSFhbFmzRqioqLYtm0b4eHh8n6lTXB17ty5xPG+/vprxowZQ3JyMvb2
9vj6+rJu3TocHR3R0dGhSpUqtGnThjt37pRILeLh4cGIESMICgrCxMSEatWqsXjxYvLy8hgwYAAG
BgbY2dkRHR0tD+ofOHAApVLJzZs31fpRtP7MmTP4+PhQrVo19PX1OXXqlNoAPDw+B/Wb8Ogkx6PL
i+jq6qq9z83NpVGjRqSkpKj9XKalpeHr60tubi5QmCO7+Prjx4+zf/9+tbbat29PSkoK+/bte9Wn
V2Zyc3MJCwvju+++o3fv3lhbW9O0aVMGDBhAZmYmkiTh7e2NoaEh9vb2KJVK9PT0+Ouvv2jcuDH9
+vVj3bp1ANy8eZObN2/Svn17jI2NqVSpEn369KFWrVpA4VMrnp6e2NnZUbt2bbp27fpW554XBEEQ
BOH1EwPZgiC8815Vwb24uLhS/9MvPL93dXIhIyMDX19fateujaGhITY2NigUCrKzs+VtHo0OhMLc
v1ZWVvL7qlWrYmVlhba2ttqyK1euyO8HDx7M6tWruX//Pg8ePGD16tVlmrNXKMnJyYmCggIuX76M
jY2N2utxuZvr1q1bIhL3SZG57wo9PT369u1LcHAwu3bt4sSJEwwcOBANDY0nDuz7+flRqVIl+vbt
y4kTJ4iNjWXEiBH4+/tjamoKQMuWLdmyZQvXrl3D1taWCxcukJubi62tLY0aNVIbyI6MjCQ9PZ35
8+ezceNGteVRUVEADB8+nGPHjqGjo0O/fv3YvXu3PBHl5uZGt27d5EknePIEV3GjR4+mbdu22Nra
MnnyZDIzM+nduzeDBg3i5MmTxMXF0aVLFzkFyKOWLVuGqakpCQkJjBgxgiFDhtC9e3fc3Nw4cuQI
bdq0wd/fn1q1aqGpqcmff/4pX9vr169z6dIlAFQqFf/P3pnH1ZT+cfxz723fL4qU9o1oEyOhIsq+
k7KHmcEg2ccoa8YylhnG2FOWmR+TbSKSEg1pUba6SpGlUMkSUn1/f+Se6bZQpIXn/XrdF+d5nvOc
5zndc+69n+d7Pt+3b9/i33//Re/evREWFoazZ8+ioKAA+/btw7179ySOW9aDurYwNDSElJQUoqOj
ubJnz559cCHUxsYGt27dgrq6ernrUuyrrqWlhdTU1HL1pRcKeTwevv/+e/j5+aFfv344d67sd4yG
yc2bN1FQUICuXbuWqxs/fjyAEuuV6OhoXLp0CcXFxZg6dSp27dqFyMhIbN26lfvMEwqFGDNmDHr0
6IF9+/bh0aNH3PsMAGbOnAlPT090794dP//8c7mFki+F2nxSgcFgMBiMLx0mZDMYjC8SJycnzJw5
E8CHE+5Vx5O3oURKRkVFwcLCAjIyMlzU3oULFyTKIiIiIBAIqizMlz6nVeF9wn9NLS7UN/r06YPc
3Fxs376d+5FPRCgoKODalI0OBFDuUWoej1dhWWkBq2/fvpCVlUVQUBCOHTuGwsLCT0r+xqh5jI2N
4e7uznk3p6enIzo6GitXrqzUu3n69OnYuXMndu/ejVu3bsHHxwfXr1+v5ZHXDevWrUPHjh3Rt29f
9OjRA506dYKZmRnk5OQAVHz/lZeXR0hICO7du4e2bdti8ODB6N69u0RE9Pjx4zFmzBgkJSXhxo0b
MDQ05EQ6TU1NiQWi69evw9raGitWrMCKFSu4Y6qpqeH48eMgIkyaNAlhYWE4fvw49PX1oaCgICFw
ll10qsoCFwCJSFRNTU0QEYqKijBw4EDo6OjA3Nwc3333XYX3EACwtLTEggULYGhoiHnz5kFOTg7q
6urw9PSEoaEhFi1ahCdPnnC2Gb///jsA4MaNGxg3bhz4/JKfBUZGRujfvz9+/vlnTtT+6aefYGho
CGNjYxw9elTiuGU9qGuLT1n8aNKkCfr374/z588jPT0d4eHhmD59Oh48eAAAXKLHX3/9Fbdu3cK1
a9ewe/durF+/nutHHPk9depULFu2DH379sWFCxc+76RrgdILqKXJycnB7du3wePx0L59e5iamnKR
1z169MCCBQugoKAAd3d3ic+8nTt34uLFi9DX10dubi5MTU25xQcfHx/cuHEDffr0QVhYGMzNzSUW
kOoKIoKfnx/n/W1tbY1Dhw4BKLEnmjBhAldnZmZWzi5k3LhxGDhwIFasWAEtLS2YmZmVO4anpyf6
9u0rUVZYWAgNDY2P9r9nMBgMBuNrQKquB8BgMBi1wf79gRgxYiRCQkZxZc7OvbB/f2AdjurzMXPm
TNjY2CAkJIQTPby9vSXKFBQU8PDhwyr7rAYFBVXbu7IyMUG8uBAaOg1FRYSSSOwICATT4excvcWF
+kJOTg5EIhF27NgBe3t7AMD58+c/2/EEAgFGjx6NnTt3QkZGBm5ubpzgx6g7yr7nd+/ejWXLlmHW
rFm4f/8+GjduDDs7u3IChphhw4bh9u3bmDt3Ll6/fo3Bgwdj8uTJCAkJqY3h1ymKiooICAjgtvPz
8+Hr68vZVVQUrZmTkwNv7zmc5cObN2+QlnYXb9684axIpKSk8Ntvv3Ei9Zw5c7j9Bw4ciOLiYu7v
9vPPP8PS0hIA8OTJE65t//79oaamhq5du+L+/fvcfdPf3/+Di059+vSBvr4+tm/fjubNm6O4uBjm
5uYSYh8guaAlHo+NjQ1at24NFxcX9OjRA0OGDIGamlqF5690AtilS5fizZs3EuK42Mro0aNHWL16
NVJTU3Hq1CkMGDAAs2fPRnJyMucBvWvXLkyZMgXdunVDQUEBBAIBZGVl8ebNm3ICfEVPmfD5fBw+
fBj9+vWrcKw1xbp16/Ddd9+hb9++UFFRwZw5c5CRkfHBxY9z585h7ty5GDx4MJ4/fw4tLS1069aN
+7t6enpCUVERq1atwpw5c6CoqIg2bdpgxowZXD+l+54+fTqKi4vRu3dvnDx5Eh06dPis8/6ciBM8
njlzhovABkqiq4VCIXJzc5GRkYEnT55wyS9dXV3Rs2dPBAYG4vDhw9DQ0EBaWhri4+OhpaWFb775
BmPGjEFUVBT09PSwc+dOWFlZQUZGBkZGRpg+fTqmT58Od3d37Nq1C/3796+r6QMAVqxYgX379mHr
1q0wMjLCuXPnMGrUKGhoaMDOzg4tWrTAwYMH0bhxY0RFRWHSpElo3rw5hgwZwvVx5swZqKqqIjQ0
tMJjTJgwAQ4ODsjKyuKuzWPHjuH169cYNmxYrcyTwWAwGIyGCBOyGQzGF8e4ceMQERGBc+fOYf36
9eDxeEhLS8P8+XPw8OE93Lx5E0KhENbWFlBVVeX2KygowKxZs/Dnn3/i2bNnsLW1xbp162Bra1vh
cV69eoVBgwbhxYsX+Oeffz468dbnIDU1Fd9//z00NTXfW1aZvUFFVCaefCxf2uKCUChE48aNsXXr
VjRr1gx37tzB/PnzP2sU/4QJE9CyZUvweLwvIhKwISIWYMSEhYVJ1AsEAvj4+MDHx6fC/ceMGYMx
Y8ZIlM2bNw/z5s2TKPPz86uhEddfrly5gqSkJLRv3x5Pnz7FkiVLwOPx3itqSSaN7QLgHEJDp2HE
iJE4efKfKh9bHI388OFDTsiOj48Hj8dDRkYGTpw4gZycnGrPqaoLXBXdJ3g8HtauXQtpaWnOd3vh
woWVWs1U5ckOoCSiVFFREQsWLEBoaChEIhFUVFQwe/ZsTvxXU1ODsrIyWrRogbVr18LQ0BDy8vIY
PHhwOQG+sgjx2uBjFj+Aks++0jkGKsLNzQ1ubm4V1unq6qKoqEiizMvLC15eXtUZfr1EVlYWc+fO
xZw5cyAtLQ17e3s8fvwY169fx6ZNm+Du7o7BgwejZcuWcHNzw4YNGxAfH4+WLVvC1dUVmzdvRmpq
KiwsLGBoaAhra2sQEdq1awcrKyucP38eV69eha2tLRISEjBkyBDo6+sjIyMDly9fxtChQ+t0/gUF
BfDz88OZM2fwzTffAAD09PQQGRmJP/74A507d5a4n+vq6iIqKgp//fWXhJCtpKSE7du3Q0qq4p/b
dnZ2MDExQUBAAGbNmgWgZOFz6NChEvkAGAwGg8FgSMKsRRgMxhfHhg0bYGdnh4kTJyIzMxMPHz6E
lJQUevfuDQcHB1y7dg3btm3Djh07sGzZMm6/2bNnIygoCAEBAYiPj4eRkRFcXFzw9OnTcsd4+vQp
unfvDh6Ph9DQ0FoXsQsKCjBt2jQ0bdoU8vLy6Ny5M2JiYnDnzh3w+Xzk5ORg3LhxEAgE8Pf3L1e2
Z8+eCq0/Lly4ACcnJygqKqJRo0bo2bMn8vLyAJS3Ftm7dy/atWsHFRUVaGpqwsPDA48fP67yHIRC
IU6e/AcikQjBwcEQiUQ4efIfCIXCmjtRtQiPx8Off/6J2NhYtGnTBt7e3lizZg1XV/rfmsLIyAgd
O3aEqakp2rVrV6N9M+oOkUiEEydONNikp5/CmjVrYGVlxSU1PH/+PBo1alRh25pMGsvn86Gnp4ef
f/6Z86OeP38+iouLMXLkSPTq1QsjR45EcXExcnNzq9xv6QWu1NRUhIWFwdvb+4MJCktjZ2cHHx8f
xMfHQ1pamrM4+NxERUVh7Nix6NevH8zNzaGhoYH09PRaOXZVuXLlCg4cOIDbt28jLi4O7u7uH1z8
qAm+9Gt00aJF8Pb2ho+PD1q1agU3Nzc8fvwYHTt2BJ/PR3R0NOLj47Fq1SqMHz8eGzZsQIcOHVBY
WIjZs2fDwsICz58/x6lTp5CXl4chQ4agTZs2uHfvHnx9fVFcXIwxY8YgOzsbY8aMgampKdzc3NC7
d2/4+vrW6dxTUlKQn5+P7t27Q1lZmXsFBARwCyObNm2Cra0tNDQ0oKysLOELLqZNmzaVithiJkyY
wC2oZGVl4cSJEyzXBYPBYDAYH4KIGtQLgA0Aio2NJQaDwagMR0dH8vLy4rYXLFhALVu2lGizefNm
UlFRISKily9fkoyMDB04cICrf/v2LWlpadGaNWuIiCg8PJz4fD4lJSWRpaUlDRs2jN6+fVsLsynP
tGnTSFtbm0JCQujmzZs0duxYatSoEeXk5FBmZiapqqrSr7/+SllZWZSfn09ZWVkSZa9fv+bmk5eX
R0RE8fHxJCcnR1OnTqXExES6ceMGbdq0ibKzs4mo/DndtWsXnTx5ktLS0ujSpUtkb29PvXv35urL
9s/4PBgZGdH69evrehiMGiA7O5tcXHoRAO7l4tKLcnJy6npo9ZLg4OB35+kuAVTqdZcAUHBwsER7
JycniXsYEdGAAQNo3LhxRER08+ZN6tixIykqKpKNjQ3Z2rZ/1//Cd33+SACoW7fu3P67d+8moVAo
0aevry9ZW1tz22fOnCFzc3OSl5cnKysrOnfuHPH5fDpy5AgREaWnpxOfz6eEhARun6dPnxKPx6OJ
EydS27ZtaezYsdSrV8l7w8rKitzd3UlXV5fU1dVJRUWF1NTUaOTIkRJjkJGRoQ0bNhAR0eXLl6l7
9+4EgBQVFcnBwYG2bdtGPB6P8vLySE9Pj3g8HgEgHo9H2tra1LFjRzI3N6d169ZRy5Ytic/nE5/P
Jzs7OyoqKiIiIj09PVq4cCF17tyZ5OTkyNzcnE6fPk08Ho+b3+ckPj6e2rZtS8rKytS4cWPq0aMH
Xb9+/bMdj12jXz6XLl0iHo9HkZGRlJqaKvG6d+8eHThwgOTl5WnLli105coVSk1NpW+//Vbimh87
diwNHDiwXN96enrcNUlU8n6Sk5Ojixcv0po1a8jU1LRW5shgMBgMRm0TGxsr/u5kQ5+qC39qB7X9
YkI2g8GoCmVF10GDBtH48eMl2iQkJBCfz6eMjAxKTEwkPp9Pd+/elWgzcOBA8vT0JKISYZbH41GL
Fi1oyJAhVFxc/PknUgFVEd3V1NTI399fYr+yZWWFZnd3d+rcuXOlxy17Tsty+fJl4vP59PLlywr7
Z9QcycnJtH//flq4cCEpKyvT06dP63pIjBrAxaUXCQSNCAh8J5wGkkDQiFxcetX10OolycnJ774Q
B5YRsgMIAIlEonrZd1W5efMmubq6krS0NAGgRo0aka+vL4lEImrevDlpampSXFwcpaSkUIsWLUhe
Xp5yc3OJqLyQHRYWRnv37iUej0ebNm2iiRMnUqNGjTgh+/Hjx8Tj8UhBQYEcHbtJCLXiYy9dupQs
LS1JVVWVlixZQkQlwpympiZ1796drl69SpGRkWRjYyMh1H9JsGu0eiQnJ1NwcHCF18v76uqS58+f
k5ycHAUGBlZY/8MPP5Czs7NEmbOz80cJ2UREbm5uNGnSJGrTpg2tXLmyBmbAYDAYDEb9oyaFbGYt
wmAwvgqIqNJHuXk8nsT/P7Rfnz59cO7cOVy/fv0zjrhyUlNTUVhYiI4dO3JlUlJSaN++PW7evPnR
/V65cgXdunWrcvvY2Fj069cPurq6UFFRgaOjIwCUe7y2qohtURITEytt4+/vX6nNwNdATk4OXF17
w9TUFCNGjMCyZcugr28okViO0TCpSZuMrwVx0liBYBpKPLIzAARCIJgOF5dPSxqbmpr67n9dytQ4
ACixH6hpytpVmJmZ4cSJE7C3t4eNjQ2ys7Ph4+ODR48eIT8/H3fu3IG1tTUMDQ1x9+5daGlp4eDB
g1x/5ubmmDZtGoASayh3d3cUFxdj8uTJ2LJlCwoLC3H8+HGoqKigSZMmAABT05aIjIxHyfm8C6A1
eDx5tGvXAQsXLsSVK1ewadMmLsnfH3/8gezsbAQEBKB169bo1KkTVqxYwX2mfixlrazqA+warTql
P6t69eoFExMTuLr2Rm5u7nvr6gNKSkoLduzuAAAgAElEQVSYNWsWvLy8sGfPHty+fRvx8fH47bff
sGfPHhgbGyMmJganTp3CrVu3sGjRIly+fPmjj+fp6Ql/f38kJSWVy5fAYDAYDAajPEzIZjAYXyQy
MjISiZhatWqFqKgoiTYXLlyAsrIytLS0YGRkBGlpaYkkXIWFhYiJiUGrVq24Mh6Ph5UrV2L06NHo
1q3bJwnHH0t1RPfqIC8vX+W2+fn5cHV1hZqaGvbt24eYmBgEBQUBQLlEYNXhQ+N3c3ODSCT66P4b
OpKJ7e4CCMT163cxYsTIKvdRlQWDsvD5fBw9evSj92d8mLoQTr8E9u8PhLNzBwCjAOgAGAVn5w6f
nDTW0NDw3f/OlamJAFDiT19TVEXYK510OCEhAc+fP0ejRo0kPHzT09NLvY8kefToESZOnAgTExOo
qalBVVUVL1++LLfwGB8fW0aozQJREUJCgqGkpARlZWVMmDABmZmZuHbtGpKSktCiRQs0bdqU68PO
zq7Gzk19gl2jVaeiz6rQ0IsYMWLke+vqC0uXLsWiRYuwcuVKtGrVCj179kRwcDAMDAzw7bffYtCg
QXBzc0OHDh2Qk5ODKVOmVKnfir7jODs7Q1NTE66urmjWrFlNT4XBYDAYjC+O92egYDAYjAaKnp4e
Ll26hDt37kBJSQmTJ0/Ghg0b8MMPP2Dq1KlISkqCr68vvL29AQAKCgr4/vvvMXv2bAiFQrRo0QKr
Vq3Cq1evMH78eK5fsYi8evVqFBUVoWvXrggPD4epqWmtza206O7m5gbgP9H9UyLYLCwscObMGfj4
+HywbVJSEnJycuDn5wctLS0AQHR09EcfW8yHovhkZWUhKyv7ycdpiIijAUt+/Hu8K/VAUREhJGQU
bt26VaUIVB0dHWRmZnIRmFUhMzNTIglnTSetZJQVTj1K1dS8cPolIU4ae+vWLaSkpMDIyOiTIrHF
iKO9Q0OnoaiIUCJWRkAgmA5n50+L9i6LpLDXBcA5hIZOw4gRI3Hy5D8AAEVFRa79ixcv0Lx5c0RE
RJS7Z6qpqVV4jNGjRyM3Nxe//vordHR0ICsriw4dOlSy8FhaqH0BYDaA5fDz88P//vc3IiPDAZQk
szMza1luDF/q/YFdo1XjQ59VJXza51htMHXqVEydOrXCuh07dmDHjh0SZcuXL+f+L07gWBZxssjS
5OfnIzc3lyV5ZDAYDAajirCIbAaD8UUya9YsCAQCtGrVChoaGigsLERwcDAuX74MKysrTJ48GRMn
TsSPP/7I7bNy5UoMHjwYo0ePhq2tLW7fvo1Tp05BVVWVa1P6B/ovv/yCYcOGoVu3brUaiVVadA8J
CcGNGzcwYcIEvHr1qto/hEoLEPPnz8fly5cxZcoUXL16FUlJSdiyZQtycnLK7aejowMZGRls3LgR
aWlpOHr0KJYtW/be/kuXrVq1CsbGxpCTk4Oenh78/Py4+tTUVHTt2hWKioqwsrLCxYsXuTp/f38J
QXXx4sWwtrZGYGAg9PX1oaamhhEjRuDly5cSx/Pz84OBgQEUFBRgbW2NQ4cOcfVPnz6Fh4cHNDQ0
oKCgAFNTU/j7+3P19+7dw/DhwyEUCtGkSRMMGDAAd+7cqcrprVFqKhqQx+NBQ0MDfH7VvwJoaGhA
Wlqa2/5U2wBGeT6nTUZ9oarWQKWfAKiIiIgICAQCPHv2jCszNjZGz549a/Q8fa5o79J8jF2FjY0N
MjMzIRAIYGBgIPGq7PxGRUVh2rRpcHFxQcuWLSEtLY0nT55ItJGSEse3lI5CtwFwAQDwv/8dQlRU
IkpH0opE95CWlo6srCyJY9WEmF1cXIy5c+eicePG0NTUxOLFi7m6jIwM9O/fH8rKylBVVcXw4cPx
6NEjAMCzZ88gJSWF+Ph4rn2jRo1gb2/PbQcGBkJHR6da4/kartGa4EOfVe+r+5qi2pOTk7F//37M
mDEDQqEQffv2reshMRgMBoPRIGBCNoPB+CIxNjbGhQsX8PLlSxQVFUFHRwedO3fGxYsX8erVK9y/
fx/Lly+XEPNkZWWxfv16ZGVlIT8/H+fOnYONjQ1X7+DggKKiIqioqHBlGzZswL1792o9Eqsi0T0k
JIQbW0UiwofKjI2NcerUKSQmJuKbb76Bvb09jh49yokbpds2adIEu3fvxsGDB2Fubo5Vq1Zh7dq1
VTrmvHnzsGrVKvj4+ODmzZvYt2+fxGPpCxcuxJw5c5CQkAATExPO17WyPlNTU3HkyBHusd9jx45h
5cqVXP2KFSsQGBiIrVu34saNG/Dy8sKoUaMQGRnJHS8pKQkhISFISkrC77//zkUrFxYWwsXFBaqq
qrhw4QJnR+Pq6orCwkKMGzcOgwYNKjfHz0F1rQ4qWzAobQ1CRGjRogW2bt0qsW9cXBwEAgEyMjIA
fFhYbAhUdw4RERHg8/kSYunnpjaE07qkrDWQeCGqutjb2+Phw4cS9+LPgTjaWyQSITg4GCKRCCdP
/iOxmPapfMwClbOzM+zs7DBgwACcPn0ad+7cQVRUFBYuXIi4uLgKj2NsbIyAgAAkJSXh0qVLGDly
JBQUFCTa6Ovro0ULXfD5UwH8gRKh1h5AOHR0dBEZGYGionkoeaBzKwAPFBdvAlExhgwZgsTERERG
RmLhwoUffT5K4+/vDyUlJURHR2PVqlVYsmQJzpw5AwDo378/nj59isjISISGhiI1NZV7QklFRQXW
1tYIDw8HACQmJoLP5yMuLg75+fkAgHPnznF5HarDl36N1gQf+qx6X93XENUuthIyMzODu7s7tm3b
BnX1psjLy6vroTEYDAaD0TD41GyRtf1CSWgIxcbGfkyiTAaDwWDUIc+fPyc5OTnauXNnubr09HTi
8Xi0a9curuzGjRvE5/MpOTmZiIh2795NQqGQq/f19SUlJSV6+fIlERE5OjqSra0t2dnZERHRmzdv
SFFRkS5evChxrAkTJpCHhwcREfXr1488PT0rHG9gYCC1bNlSouzNmzekoKBAp0+fprFjx9LAgQOr
eRY+HheXXiQQNCIggIC7BASQQNCIXFx6lWs7Z84caty4MQUEBNDt27fpwoULtGPHDkpPTyc+n08J
CQlERDRr1izq0qWLxL6zZs0iBwcHbpvH49GRI0eI6L+/k3j/hkJWVhYVFBRUuX14eDjx+XzKy8ur
tI2vry9ZWVnVxPAkEIlEFBwcTCKRqMb7rk/4+vqStbV1ufLS77cvneTk5HcZ3AMJoFKvAAJAIpGI
nJycyMvLS2K/Fy9e0PTp00lbW5tkZWVJV1eXRo0aRffu3SOi8uf2ypUr1L59e5KXlydTU1M6dOgQ
6evr04YNG7g2x44dIyMjI+Lx+OKs8gSA2rZtR2ZmZu+2VQjoQMD2d+O8SwCodevWJCcnR2ZmZnTq
1Cni8/mf9Dd0dHQsd19q3749zZ8/n06fPk3S0tJ0//59ru7GjRvE4/EoJiaGiIhmzpxJ/fr1IyKi
DRs2kLu7O1lZWdGpU6eIiMjY2Jh27Njx0eP7Wq7Rj+V9n1XV+Rz7Evlv/oHv5h/4Vc2fwWAwGF8n
sbGx4u+WNvSpuvCndlDbLyZkMxiMuiI5OZn9cP1EoqOjic/nU3p6erk6sUAqFiKIiHJzc4nH41Fk
ZCQRVSxkt27dmtt2dHQkBwcHMjQ0JCKi69evE4/HI2VlZVJSUuJesrKynNh94sQJUlBQICsrK5oz
Zw5FRUVx/c2ePZukpKQk9lVSUiKBQEBbtmypdSE7JyeHXFx6SYhMLi69KCcnR6JdVRYMxEJ0fHw8
CQQCunv3LhERFRcXk7a2Nm3bto3bp6EL2dURsMVUVciuSIj9mjh27Bipqalx21euXCEej0cLFizg
yiZMmECjR4+m3bt3c213795NPB6P+Hw+96+/vz8Rlbzftm/fTgMHDiQFBQUyNjamo0ePcv2Fh4cT
j8fj/jbifkNCQqhly5akpKRErq6ulJmZWRun4JOpj8JeWaG2KoJ7TeLo6EhTp06VKOvfvz95enrS
xo0bycDAoNw+QqGQAgICiIjo6NGj3GfFoEGDaOvWrTRjxgxasGABPXjwgHg8HqWkpNTomBn/8b7P
qqp+jn2J1PZ1xGAwGAxGfaEmhWxmLcJgMBgfQPwYqKmpKXr16gUTExO4uvZGbm5uXQ+tXiESiXDi
xIkKPV3FyMvLf7Cf0l7MYhuR0tYi72svpri4GAUFBVi+fDmICG/fvoWRkRG2bt2KhIQEXLp0CfHx
8Th16hRcXV1x9+5deHl54dKlS+jYsSOXNDMzMxOqqqrg8XiQkpJChw4dOIsBd3f3D86lpqmq1cHN
mzdRUFCArl27frBPKysrmJqaYv/+/QCA8PBwPH78GEOGDPksc6gNnJyc8MMPP8DLywvq6upwcXEp
Zy0SFRUFa2tryMvLo3379jhy5AhnuVKamJgYtGvXDoqKirC3t+fe3/7+/li8eDESEhLA5/MhEAiw
Z88eAICvry90dXUhJycHbW1tzJgxo/YmX8t06dIFL1684PyIIyIioK6uztk6iMscHEqsMsTX9PDh
w+Ht7Q1zc3NkZWXh4cOHGD58OLfPkiVL4ObmhqtXr6JXr17w8PDA06dPufqyFkP5+flYu3Yt9u7d
i8jISNy9exezZs36XNOuUeqjXUVZz/H3+UN36tQFKSkp7733fwxl7+08Hg/FxcUgogptq0qXd+7c
Gc+fP0dsbCwiIyPh6OgIBwcHnD17FhEREdDS0iplgcGoad73WVUblj31lZrKdcFgMBgMxtcME7IZ
DAbjA7i7j0Jo6EWUTnAVGnoRI0aMrOOR1Q+qI/SL/ZrFPqdlqYkEYWKmTJmCtLQ0yMjIYMWKFRg1
ahQ8PT1BRLC0tESfPn2wd+9eAEDjxo0xevRoqKurw87ODjt37kRhYSFCQ0Px4sULnDlzBhcvXkSz
Zs0wadIk6OjoQFlZucbGWl0+lNiuKgsGpfHw8MC+ffsAAPv27UPPnj2hpqb2yeOsS/bs2QNZWVn8
+++/2LJli0Tdixcv0K9fP1haWiI+Ph5Lly7F3Llzy73/iAgLFy7EunXrEBsbCykpKYwfPx5A5ULs
wYMHsX79emzbtg0pKSk4fPgw2rRpU2vzrm1UVFRgYWHBCdfh4eGYOXMm50f84MEDpKamlvMjlpOT
g5KSEqSkpKCurg4NDQ3Iyspy9ePGjcOwYcNgYGCAFStW4OXLl4iOjq50HIWFhfjjjz9gbW0NKysr
TJ06tdL7TH2joQh7FQnuamrSOH/+XK0u8rZq1Qp37tzB/fv3ubIbN24gLy8PLVu2BACoqamhTZs2
+O233yAtLQ1jY2M4ODggLi4Ox48f5xZWGJ+X931WfY4ErfWd6ua6YDAYDAaDUR4mZDMYDMZ7EIlE
CAkJRlHRRgAeAFoA8EBR0QaEhATXeARaQ6Q6Qr+srCzmzp2LOXPmICAgALdv38alS5ewc+dOABBb
SH0yhYWF2L17N/7++2/MmTMHfn5+aNKkCaytreHn54fffvsNWlpaOHz4MH788UccPXoUCQkJOHbs
GIgIrVq1woEDB6CiogI9PT3MmzcPjx8/xk8//YS0tDQMHToUDx48qJGxfg6qu2Dg7u6Oq1evIi4u
DocOHcLIke9fpKnJBYfPhZGREVauXAkjIyOYmJhI1AUGBoLP52Pr1q0wMzODi4sLZs+eXa4PHo+H
FStWoFOnTjAzM8O8efMQFRWFgoKCSoXYjIwMaGpqolu3btDW1oatrS08PT1ra9p1gqOjIydkR0ZG
YtCgQTAzM8OFCxcQERGB5s2bw8DAoFp9lhb/FRQUoKysjEePHlXaXkFBAXp6ety2pqbme9vXR+q7
sFdWcO/c2QFPn75FbS/yOjs7w8LCAh4eHoiPj0d0dDTGjBkDJyencgmaAwMDuUUUoVAIMzMz/Pnn
nx+V6JHB+FTe92SDi0uvenvtMxgMBoNRn2BCNoPBYLwH9hjo+/kYoX/RokXw9vaGj48PWrVqBTc3
Nzx+/BhAxQLpx4imBQUFKCoqgomJCdavX4+8vDyMHTsWUVFR2Lt3L4KDgzFgwAAIBAKkpqZiwYIF
+Oabb1BQUABNTU3s378fiYmJSE1NRUZGBs6dO4cuXbrA1NQUb968QXZ2NlRUVKo9rtqiugsGenp6
sLOzg6enJ4qLi9GnT5/39l9TCw6fE1tb20rrRCIRLCwsICMjw5W1b9++wralBVVNTU0AeK9AOnTo
UOTn50NfXx+TJk3C4cOHUVRUVN3hNygcHBwQGRmJhIQEyMjIcNGvYhuHjxENK7OVqE77hvA+bYgY
GxvD0NAQkZERn22R90P3/cOHD0MoFMLBwQE9evSAkZERDhw4INHG0dERxcXFcHJy4sqcnJxQXFzM
IrIZdUZ9tBJiMBgMBqMhIVXXA2AwGIz6jORjoB6lathjoEDVhP6KIozmz5+P+fPnlysvK/ipqqpK
lI0ZMwZjxozhtn18fODj4yOxj42NDSZPnoyRI0ciLi4OfL7kmq2SkhI0NDQAAEOGDMGjR49w7do1
9OjRA+bm5li3bh2AEvsJW1tb7Nu3r5wgpq6uDiUlpXLjr08sWrQI0tLS8PHxwYMHD6CpqYnvvvsO
QMUikYeHB6ZOnYoxY8ZIWDxU1L4hRGQrKipWWleRx25lomd1Pdu1tbUhEolw+vRphIaGYsqUKViz
Zg0iIiIgEAiqM4UGQ5cuXfDs2TOsX7+eE60dHR2xatUq5Obmwtvbu8L9ZGRkvniR/0vlY+/9VSUs
LKxcWVBQEPf/Fi1aSGxXRP/+/cu9v9atW8fd4xmMukD8ZMOtW7eQkpICIyMjFonNYDAYDEY1YEI2
g8FgvAfxY6ChodNQVEQo+ZEeAYFgOpyd2WOg9VXot7a2RmFhIbKysmBvb19pOw8PD7i4uODGjRs4
e/Ys/Pz8uDobGxvs378f8fHxaNOmTYP8W1d1wQAAvv/+e3z//fcV9lO6va6uboMXH83MzLBv3z6c
OXMG3bt3x9OnT3H58uVq91OZECsrK4s+ffqgT58+mDx5MszMzHD16lVYWVnVxPDrHWI/4sDAQGze
vBlASZT28OHDUVhYWGlEtp6eHtLS0pCQkABtbW0oKytLRMm/DxZtXbfU13t/RYhEIqSmpjLBkFGv
MDY2Zu9HBoPBYDA+AmYtwmAwGB+APQZaOfXV79HY2BgeHh4YPXo0goKCkJ6ejujoaKxcuRInTpzg
2jk4OEBDQwMeHh4wMDBA27ZtAZQksPzzz4N4+vQpBg8eDBMTEzg4OOHYsWOYPn16vfbHrmlEIhFO
nDjxRfjB//jjj5g5cybc3d1RVFSE1atXAwBCQ0Oxdu1aAJLR5hWJpaXLSgux2dnZKCgogL+/P3bu
3Inr168jLS0NAQEBUFBQgK6u7meeXd0itnEo7UfcqlUrSElJceJ2WQYPHgxXV1c4OTlBQ0ODs4Yo
/TdYvHgxrK2t3/tUwPbt2/HixYsanhHjfdTXe39pqpOImMFgMBgMBoPRMGBCNoNRj3FycsLMmTPr
ehhfPWUTXIlEIpw8+Q+EQmFdD61eUJ+E/tLi1u7duzF69GjMmjULZmZmGDhwIGJiYqCjoyOxz4gR
I5CYmAgPj/+iCt3dR+Hs2csANgEYCkAF586Fw83NDW/evKnX/tg1RUMWgT7kta6srIzjx48jNTUV
RITly5dzFjVycnJV7qciIVZNTQ3btm1Dp06dYGlpibCwMBw/fvyLv1+sW7cORUVFEgJmfHw8Onbs
yG2PGTMGOTk53LaMjAz++usv5OTkoKioCKNHjwZQ8gRAv379uHY8Hg85OTlcvYODA4qKirjr0MjI
qJyve0W2EoyapT7d+yuiOomIGQwGg8FgMBgNA15DezSTx+PZAIiNjY2VyEzOYHyJODk5wdraGr/8
8kuD7J/xdfGl+D2KRCKYmpqiRPwo/ch8IIBREIlEDXp+pXnfPcDVtTdCQy++S+bWBcA5CATT4Ozc
ASdP/vNR/b969QojR45EaGgoXrx4gdzc3FpbFBg3bhz8/f25JIA8Hg87d+7E+PHjcfr0aUyYMAFp
aWno0KED/P39YWJiwu2Xl5eHv//+m+vLy8sLV65cwdmzZwEABw8exJIlS5CSkgIFBQXY2NjgyJEj
kJeXr5W51Wc+9XNm8eLFOHLkCOLi4iptM27cONy/fx9eXl4N/v7TEKmP9/6v6T7OYDAYDAaDUd+J
i4sTP/3clogq/2JfBVhENoPBYDBqBGNjY/Ts2bPBiwP/JTEbBSCxVM1/Scy+FIKCgrB06VIAgL6+
PjZu3AigRAQKCQl+J2J7AGgBwANFRRsQEhL80TYj/v7+uHDhAi5evIiHDx/WamT7hg0bYGdnh4kT
JyIrKwsbN25EXl4eiouLMXnyZLx8+RL9+/eHjIwMPD09OUsLMePGjcOgQYO4bXFkdmZmJtzd3TFh
wgQEBwdj2bJl6NSpE4hI4px+zRQXF2Pu3Llo3LgxNDU1sXjxYq4uLy8PEyZMgIaGBlRVVeHs7IzE
xMT39jVz5kwIhUKoq6tj2rRpOHXqNE6fPt3gnhz4UqiP9/6qJKNkMBgMBoPBYDQ8mJDNYDQQ9u7d
i3bt2kFFRQWamprw8PDA48ePufqIiAjw+XyEhYWhXbt2UFRUhL29fTnBadmyZWjatClUVVWRnJyM
8+fPS4g1FdmZDBw4EOPHj6/yWADg6NGjMDExgYKCArp164Y9e/aAz+fj2bNnXJvz58+jS5cunH/s
9OnTkZ+fz9Vv3rwZJiYmkJeXR7NmzTBs2LBPO4kMRhX4L4lZWUqSmN2/f/+L8IsGSpL0KSoqliv/
XCJQamoqWrZsiZYtW0JDQ+Oj+vhYVFRUICMjAwUFBairqyM/P59L7vn8+XOMGjUKBw4cwLx58xAV
FYWioiIJG5GNGzdi9+7d5fp9+PAhioqKcOjQYTg5OeH777+Hj48PBg0aitDQUEyaNKm2plhv8ff3
h5KSEqKjo7Fq1SosWbIEZ86cAQAMGTIE2dnZCAkJQVxcHGxsbODs7IynT59W2NeaNWuwZ88e7N69
G+fPn8fffx9+51lvC2YfwRAjmYyyNPUvGSWDwWAwGAwGo+owIZvBaCC8ffsWy5YtQ2JiIo4cOYI7
d+5g3Lhx5dotXLgQ69atQ2xsLKSkpMoJ0CtWrMDq1asRGxsLWVlZJCQk4MGDB1ykXHp6Otc+IyMD
/fv3x/HjxxEYGIjhw4fj0aNH3Fg8PT2hoqKC6Oho6OrqQllZGVOnTkVaWhoGDRqEBw8eQEFBARoa
Gvjxxx85USgvLw/Dhg1Dly5dcPnyZVhbW2P58uW4cOECfvjhBwBATEwMpk+fjmXLlr2LDg1Bly5l
RTUGo+YxMTFBly5OAAjAcYiTmPF4PwDgY+LEiV9M1KeTkxO8vLzg5OSEO3fuwMvLC3w+v5Tf8N8A
+gFoBEAJQInfsVgEunbtGnr16gVlZWU0a9YMo0ePRnZ2dqXHWrt2Lbfo1rVr1889vUp5+/YtZs+e
jQMHDoDP5yMxMRFr1qyBnJwcNDU1AQAvX76U2EdZWbnCCHJLS0sIhY1w7lw4gPYAfgbwB0JDL2LK
lGkSnttfKxYWFvjpp59gaGiIUaNGwdbWFmfOnMGFCxcQExODv/76C9bW1jA0NMSqVaugqqqKgwcP
VtjXhg0bsGDBAvTv3x88Hg/372eg5P3ZAjX15EBDoqKof2trayxZsgQA4OvrC11dXcjJyUFbWxsz
Zsyoi2HWOg0hGSWDwWAwGAwGo/owIZvBaCCMHTsWLi4u0NPTQ/v27bF+/XqcOHFCIoKZx+NhxYoV
6NSpE8zMzLjIwoKCAgDAb7/9hokTJ2L06NEwMjKCnp4eioqKIBAIuEi59PR03L17F0BJsqynT5+i
U6dOcHFxQWpqKtzc3LixqKmp4eHDh9DT08Pr16/h7++P7du3w9nZGUKhEPHx8VizZg3+/PNP9OjR
gxvnkCFDEB0djcGDB+PatWuwt7fHzJkzsXTpUvj7+6OgoAAZGRlQUlJC79690aJFC1haWmLq1Km1
e9IZXzQhISHo3LkzhEIhmjRpgr59++L27dsAgF9/Xf+u1Y8QJzEjegXgd3xpUZ88Hg9BQUHQ1tbG
0qVLkZmZiYcPH8LFpReA2QDSAfwPwFLw+U/Rvn0HGBsbIy8vD926dUPbtm0RFxeHkJAQPHr0qNIn
J4KCgjBx4kR07NgRWVlZEp7TnxsnJyf88MMPSElJwZYtW+Dq6oq8vDysWrUKxcXFMDAw4CwtxAtu
4hwifD4fRCRhLfL27VsUFhbCw8MDysrKyM5+AqAHgEcAVgNYhKKinxASEoyffvqJG4d4cVBZWRmq
qqrc4qCYsvYlALiFBjEHDx6EhYUFFBQU0KRJE/To0QOvXr36LOetprCwsJDY1tTUxKNHj5CQkIDn
z5+jUaNGUFZW5l7p6emlngr4j2fPnuHhw4do3749gNJPDrQr05LZRwDAoUOHsH79emzbtg0pKSk4
fPgw2rRpU9fDqjXqezJKBoPBYDAYDEb1YUI2g9FAiI2NRb9+/aCrqwsVFRU4OjoCACc6iyn9I1Uc
WSgWSpKTk9GuneQP/mbNmqFZs2ZcpJyysjLu3r2L0NBQXLt2Dfv374eamhrU1dUREBCA8PBwBAYG
ol+/fli3bh2eP3+OqKgo8Hg8tGrVCk5OTsjKykL//v1hbGyMsWPHwtTUFEVFRQCAf//9FzExMWjS
pAmOHz8OKysr/P7773jy5AkGDBgAAEhLS0P37t2ho6MDfX19jB49Gvv27av3Yg2jYfHy5Ut4e3sj
NjYWYWFhEAgEGDhwIABAVVUVPB4PR48exdatW9/tsQPAJHyJUZ9qamoQCARQUlKChoYGNDQ0sH9/
IJSU5ABcBeAMYCa6d++CkyeDAZQsjNnY2GDp0qUwNjaGpaUltm/fjrNnz1YoIKqpqUFBQQEyMjJQ
V1eHmpparc5xz549kJKSwtChQ9hd6pQAACAASURBVLFlyxYMHToUz549A4/HQ0REBGdpUdr+CADU
1dXx8OFDibIrV64gJSUF//77LxYtWvSulA8gB8BIANIASqL1S9suiRcHIyMjERoayi0OfoiK/LiT
kpIQERGBQYMGob4n7paWlpbY5vF4KC4uxosXL9C8eXMkJiYiISGBeyUnJ2P27NmV9ic+H//ZRzwp
04LZRwAl3w80NTXRrVs3aGtrw9bWFp6ennU9rFpDKBTi5Ml/IBKJEBwcDJFIhJMn/4FQKKzroTEY
DAaDwWAwPhImZDMYDYD8/Hy4urpCTU0N+/btQ0xMDIKCggCAi7YWU1owEP/YLy4uLlcmRl1dXWJb
VlYW+fn5uHnzJlq0aIHmzZvj7du3AICWLVtCTU0N33//PdTU1DB48GCYmJjg8OHD3FiaNm0KJSUl
ieM0bdoUeXl5AEqsCJ4/f474+HgUFRWBiEBEEAgEGD9+PEQiEQwNDaGkpIT4+Hi0b98e//vf/+Dh
4QEzM7NyItOnUJEfeF3zucd0584dzkrha2fQoEEYMGAADAwMYGFhgW3btuHq1au4ceMG10ZXVxfa
2trvtj7dL7q4uLjei45ihEIh1q9fB2lpabRq1QpTp07F6tUrOREoISEBYWFhEpG0LVu2BI/HqzCa
tq4xMjJCjx49kJycjMTERERHR3MitIGBAWdpERoaKvE36tq1K2JiYpCamooXL17A19cXV69eRWZm
JtauXVtKTLUBUAjgFkqE1dcA/rvHnj59mlsctLKyQrt27bjFwdjY2CrNQezHPXDgQOjo6MDc3Bzf
ffcdFBQUauYk1TI2NjbIzMyEQCCAgYGBxKtRo0bl2ovzMly8eBFAiX1Ejx49AcShxDqC2UeUZujQ
ocjPz4e+vj4mTZqEw4cPc4vKXxP1MRklg8FgMBgMBuPjYEI2g9EASEpKQnZ2Nvz8/GBvbw8TExNk
ZWVVux9TU1NER0dLlJVN0igWsomIi5q7du0aV19YWIiXL1/Cz88POjo6UFRUlBgLj8eDqqoqLl++
LFEmjmh8+fIlmjdvjr59+6Jdu3ZITExEYmIikpOTsXz5chgYGEBKSgoAcOrUKYSGhiI8PBxpaWl4
8OABwsLCqj1vsSdvTYrgDRUdHR1kZmaidevWdT2UOiclJQXu7u4wNDSEqqoqDAwMwOPxJJ5y8PT0
xL59+95tmQFQByCOwC2J+jx48CC0tbWhpKQEOzs7REREcPv7+/tDKBTi2LFjMDc3h5ycHDIyMhAe
Ho5vvvkGSkpKEAqF6Ny5MzIyMrj9fv/9dxgZGUFWVhYtW7ZEYKDko/B8Ph87duzAoEGDoKioCBMT
Exw7dqzGz5GnpyfS0tIwffp0PHz4ELa2tti0aRMA4MWLF+jXr1+5aNpbt27VSz97W1tbzJo1CwKB
ACNGjEBeXh769esHIoKWlhZnaXHv3j2JhbgePXrgp59+QkxMDMLDw/HixQv06dMHRIR27dqhdevW
aNJEHcAKAK8AnAcwHALBdsjLy3NCdlJSErc4KEa8OHjz5s0qzcHS0hLdunVD69atMWzYMGzfvr3S
pIgNAWdnZ3To0AEDBgzA6dOncefOHURFRWHhwoWIi4urcJ/p06dj5cqVOHLkCJKTk6GpqQEpKT6A
GHyN9hFi65vSiBeftbW1IRKJsHnzZigoKGDKlClwcHD4KsVsBoPBYDAYDMaXAROyGYwGgI6ODmRk
ZLBx40akpaXh6NGjWLZsWbl2FUV6li774YcfsH37duzZswcpKSm4c+cOHj9+LCHaqKurIyMjA8+f
P8edO3cwevRoTii5ceMGXrx4AWlpaWzcuBG5ubnIy8srNxZ9fX0kJSVh3rx5uHXrFh49eoTr168D
AKysrJCZmYnJkycjISGBsycpLi5GZGQkl+zxn3/+wY4dO7gklCdOnABQIsZXh8LCQk6Ur41I2MLC
ws9+jE+Bx+NBQ0MDfD67/ffp0we5ubnYvn07oqOjcenSJRBRuaccjh49Cl1dPfD50gCGAVgLYAIE
gunQ0moBkUiEv/76C1evXsXQoUPRs2dPiYjk/Px8rFq1Cjt27MD169chFAoxcOBAODk54dq1a7h4
8SImTZrEXYdBQUGYMWMGZs+ejevXr2PSpEkYN26chEAOAEuWLIGbmxuuXr2KXr16wcPD45NETRkZ
mQoFLi0tLUyaNAkHDx6Et7c3tm3bBqAkmvb69evQ1dUtF00rLy//0eP4XCgqKsLY2BgXLlzAsmXL
0KJFC9y4cQOpqakSlharV69GUVERVFVVuX19fHwwfPhw9OnTB2vWrMGcOXPA5/PB4/FgZmYGkSgZ
Li49UZIgNA+AP5ydO0g88SK+D5WldPn7RElx/alTp3Dy5EmYm5vj119/hZmZGe7cuVOj56omqWjO
pTlx4gS6dOmC8ePHw9TUFO7u7rh79y6aNm1aYXtvb2+MGjUKY8eORceOHaGuro6RI0eie/fuX6V9
RFnrm2fPniEtLY3blpWVRZ8+fbB+/XqcPXsWUVFRuHr1al0MlcFgMBgMBoPB+GSYksFg1GPEAkCT
Jk3g7++PgwcPwtzcHKtWrcLatWsrbV9Zmbu7OxYsWIDZs2ejbdu2eP36NRclKkZXVxdGRkZYv74k
2d2///4LGxsbPH78GGPGjIGTkxP27NmDgwcPYtOmTcjKyio3FgUFBRw8eBBBQUGwtLTEgwcP8M03
3wAAXF1dYWdnh3nz5uHnn39GYmIiOnbsCHNzc8yZMwdaWloAgM2bN+PgwYN48OABdHV1MWPGDDRq
1AinT5+WOJa1tTWWLFnCbfP5fGzZsoVLqDZx4kR07doVQIlVgtjCRExxcTHmzp3LCeaLFy+W6D8v
Lw8TJkyAhoYGVFVVuYRwYhYvXgxra2vs2LEDBgYGEufyY3nfmNatWwcLCwsoKSlBR0cHU6ZMwcuX
LwGUCBgKCgo4deqURH9///03VFRU8Pr163LWIuJo9bCwMLRr1w6Kioqwt7cv5/u8bNkyNG3aFKqq
qpg4cSLmz58Pa2vrT55rXZGTkwORSISFCxfCyckJpqamyMnJqbBtixYtEB8fh+7d7QFsBpAPYAfs
7S2RlfUQ//vf/9CxY0fo6+tj5syZsLe3x65du7j9CwsL8fvvv6NDh5IkiYWFhXj27Bl69+4NPT09
mJqaYtSoUZyFydq1azF+/Hh8++23MDIygpeXFwYNGoQ1a9ZIjGvcuHEYNmwYDAwMsGLFCrx8+bLc
ExfVQU9PD+fOncODBw+QnZ0NoCTR4KlTp5Ceno64uDicPXsWrVq1AlDiOX3v3j24ubkhJiYGt2/f
RkhICMaPH1/v7VOqa2lRFkNDQ0hJSSE6OhoikQgXL16En98yKCoqYsCAAZyYWnrBqFWrVrh79y7u
37/Pld24cQN5eXncOa3Mj7ssdnZ28PHxQXx8PKSlpTmrqfpIWFgYfvnlF4myoKAg7Ny5E0DJAsP6
9euRkZGB169fIz09HXv27OE+C3x8fCSiswUCAX755Rfk5uYiOzsbq1evxq5du3Dq1Kmv0j6ia9eu
CAgIwPnz53H16lWMHTuWe6rJ398fO3fuxPXr15GWloaAgAAoKChAV1e3jkfNYDAYDAaDwWB8HEzI
ZjDqMaUFgOHDhyM1NRX5+fk4f/48evfujaKiIlhYWAAA97iwiooKt7+lpSWKioqgo6PDlf3444/I
yspCXl4ezMzMkJ2dLZEQi8fjwc7ODo8fP8bt27dhYWGBmJgYREZGwsjICAcOHODGsnDhQpiYmJQb
C1AS7ZqcnIz8/HxYW1vj1atX0NbWhoyMDIKDg9GlSxesXLkSly5dgrq6OoYPH46wsDDMmzcPAHDg
wAEsXboUOjo6ePToEe7fv19lH9jFixdj0KBBuHr1KpYsWYJDhw4BAG7duoWHDx9iw4YNXFt/f38o
KSkhOjoaq1atwpIlS3DmzBmufsiQIcjOzkZISAji4uK4hHClI19TUlLw999/IygoqELRqbq8b0wC
gQC//vorrl+/jj179uDs2bOYO3cugBL/2N69e2Pv3r0S/e3fvx+DBw/mRPaKFjwWLlyIdevWITY2
FlJSUhJi/969e7FixQqsXr0asbGx0NHRwe+///7BSMv6jFAoROPGjbF161akpqYiLCwM3t7eFc6p
Q4cOEknDFi1aBGlpacydOwtFRUUwMTGR8Ik+d+6cRES2jIyMhJWLUCjEmDFj0KNHD/Tr1w8bN25E
ZmYmV3/z5k107NhRYgz29vYIDQ2V8E8vndhVQUEBysrKXGLXqlJ6vkuWLEF6ejoMDQ2hoaEBACgq
KsLo0aOhr6+PXr16wczMjLMWEQgEmDFjBoqLi+Hi4gILCwvMnDkTQqGQ67e+vkecnZ1hZ2dXLUuL
0igpKcHNzQ0eHiNhamqKXr16wcbGBm/evEHz5s0rFFOdnZ3Rpk0beHh4ID4+HtHR0dzioHhRSOzH
HRAQgJSUFPj6+kpYO0VHR8PPzw+xsbHIyMjAoUOH8OTJE04Irw0mTZqExo0bQyAQ1JnXvkgkwokT
J76IRKufyvz589GlSxf07dsXffv2xcCBAznfdqFQiG3btqFTp06wtLREWFgYjh8//tVEqzMYDAaD
wWAwvkDEidYaygsl2ZQoNjaWGAxG9cjPz6dffvmFrl+/Tjdv3qRFixYRn8+nsLCwGj/W5s2b6fLl
y3T79m3as2cPqamp0aJFi6rVx/r160lfX5/b1tPTow0bNki0sbKyosWLF3PbPB6PvL29JdqEh4cT
n8+nvLw8iXJHR0fq0qWLRFn79u1p/vz5REQUGRlJampqVFBQINHGyMiItm3bRkREvr6+JCsrS9nZ
2dWaW2V8aExlOXjwIKmrq3PbQUFBpKKiQq9evSIiomfPnpG8vDydPn2aiIjS09OJx+NRQkICEf13
bs6ePcv1ERwcTHw+n968eUNERB06dKBp06ZJHLdTp05kbW39aZOtY86cOUPm5uYkLy9PVlZWdO7c
OeLz+XT06FFKT08nPp9Ptra25OnpKbHfkSNHSEZGhv766y+SlpamW7duUWpqqsQrKyuLiIh2795N
QqGwwuNfuXKFVq5cSR07diRlZWW6dOkSERE1atSIAgICJNquX7+e5OXlycvLi4hK3udHjhwhov/+
psrKyuTv71+tczB27FgaOHDge9vs2rWrwjno6emRj4+PxPvpUyl7rdUUTk5O3LkT8+LFC5o+fTpp
a2uTrKws6erq0qhRo+jevXtEVHJtl36Plz1X3br1IB5PhgA5ApoSMJIAARkYGHJt9PX1Je5ZGRkZ
NGDAAFJWViZVVVVyc3OjR48eSYzL19eXNDU1SSgUkre3N02bNo2cnJyIiOjmzZvk6upKTZs2JXl5
eTIzM6PNmzfX3In6ACdOnCBZWVm6ePEiZWVlUVFRUa0dm4goOzubXFx6EUo8XAgAubj0opycnFod
B4PBYDAYDAaDwag6sbGx4u/vNvSpuvCndlDbLyZkMxgfz6tXr8jZ2ZkaN25MSkpK1LZtWzp8+PBn
OZaXlxc1b96c5OXlydTUlJYvX86JHsnJyRQcHEwikajS/ZOTk2nSpEmkra3NlVVVyN63b59Em/cJ
2VOnTpUo69+/P3l6epKjoyN17dqVBAIBKSkpSbykpKRo3rx5RFQiOpmYmFTjzLyfsmNydHQkQ0ND
Tkw9ffo0devWjbS0tEhZWZnk5eWJz+dTfn4+EZUIgUKhkP78808iItq5cyc1a9aMiouLiahyIfvJ
kyfcMePj44nP51NGRgYREQmFwnLC6syZMxu8kF0VHB0dydzcXKJs3rx5ZG5uTrdu3SIej0fnz5+v
dP/3CdmlsbOzo+nTpxMRkb29PX377bcS9Xp6egSA+Hw+8Xg8AkDbt2+n8PBwsrS0JADE4/God+/e
EuLi8+fPyd3dnRQVFal58+a0bt06cnR05ETdZ8+e0ePHj8nb25u0tLRIUVGROnToQOHh4URU8v7g
8XjE5/M54VB8venp6dHy5ctpxIgRpKysTDo6OrR161aJcWdkZFDPnj1JSUmJ1NTUqH///pSens7V
jx07lgYMGEDLly+n5s2bk4GBwQfPVX0gOTn53fkIJIDevV4SoEAA3ntva8j8+uuvpKenV2fHd3Hp
RQJBo3fn/S4BgSQQNCIXl151Nqa6prLPt/+zd99hUVzrA8e/uxSpqxixIUUuRbGCylUxFEUpXmuu
XZHYGxoSLDE3ip0YRbFcY0uwa+LVX2LERhQsCVFBMRZcwBpj1AgWxAae3x/IhBWIqFiI5/M8+8ic
OXPmzOywK2feeY8QJfuulSRJkiRJkqSXrTQHsmVqEUl6ixgZGbFr1y7++OMPbt++zeHDh+nQocNL
2VdkZCSXLl0iOzublJQUxo8fz40bN/D3b6s8iu/k5IS/f1syMzOV7TIyMpQ6S5Ys4ddff1XqPG0i
tHympqYl7qeBgYHOskql4tGjRwA8ePCA6tWrc+zYMWUyuPwJ4UaPHv1c+3uePkFe3uzz58/Trl07
GjZsyKZNm0hKSuLevXsIIZTzYGBgwL///W/Wrl0L5KUV6d69+1NTPBTcZ37d/PNQsCzfk+9DWfa0
NAUXL14kLCwMrVbLunXrWLBgAR988AEODg706tWLoKAgNm/ezLlz5zh48CARERHK5KRFOXfuHOPH
jychIYELFy6wc+dOUlNTlfQQo0ePJjo6msWLF5OWlkZkZCS//vordevWZeDAgUoaErVaTdu2bZW0
FEZGRuzdu1dn8tXQ0FB++uknvv/+e3bt2sW+fftISkpS/hNgbm7Oxx9/zM8//1zkhJUeHh7MnTsX
jUZD9+7dCQwMJCwsTGl/zpw5eHp6cvToUYYNG8bQoUPRarUAXL16lVq1arNt2zaysrK4ceMGBw8e
onXr1jqTov7www9otVpiY2P5/vvvn/NdfLX+TB1zAzgDJAE9gbzfo7S0tJey39eZUuP9999n5MiR
XLhwAbVajb29PQAzZszA3t4eExMTXF1dlVROAI0bN2bOnDnKcseOHTE0NCQ7OxuAS5cuoVardSYn
LI5Wq2XHjhhyc+cBvQBroBe5uVHs2BHzt00zolar+e6775RlHx8fnRRDHh4eXL58WUkrlj/vga9v
m7/8rpUkSZIkSZKkskgOZEuS9Mr07NmH2NgEYDVwAVhNbGwCPXr0LqbORMBSqfPkRGi3bt0q0QCI
oaEhkJfv91lUqVLluSeEe9Z9lURiYiKPHj1i1qxZuLu76+Q2L6hXr15s376dkydPsmfPHnr3/vP8
FhycLilnZ+dCkwgePnz4mdt50xS8afJXgz1BQUHcvXsXd3d3QkJCCA0NZcCAAQBER0cTFBREWFgY
tWrVolOnThw+fFgnL/2TTExMSElJ4d///jfOzs4MGTKEkJAQBg0aBECHDh2Iiopi1qxZ1K1bl6VL
l7JixQoqVarEiRMn8PDwAGDEiBGYmJgQHh6OSqVCT08PU1NTJk6cSMOGDdm9ezcrV65k9uzZnD9/
Hg8PD7p27crt27eZN28eFy9epEuXLixfvlyZsDIxMZHo6Gju379PvXr1CAwMxNjYmHv37rFhwwa2
b9+OmZkZenp63Lt3Dy8vL4YNG0ZWVhZjx46lUqVK9OvXD3t7e6pWrcqdO1lAH/J/369cuUtaWhpe
Xl7Mnj2bDRs2kJWVhYmJCU5OTtSuXftlvNWlLj8HMcwGGgJtgLvAxwDF/m4+r5Jeqy/TvHnzmDx5
MjVq1ODKlSscOnSIadOmsXr1apYsWcLJkycJDQ2lT58+7Nu3DwBvb2/i4uKUNvbv34+FhQUHDhwA
IC4ujho1alCzZs2n7v/PmweeT6zxAl7ezYPX7ffffycgIKDY9fr6+kpO+3xCCPbsOUxx37X5kxRL
kiRJkiRJUpnzoiHdr/qFTC0iSWVS0Y/iCwGrlEfxC9eZK6CmUmfw4MGievXqYt++feLYsWOiU6dO
QqPRFEotkp87ON+lS5eEnp6eWLFihbh27ZrIysoSQgidFAv5OnbsKN5//31lnaenp7C1tRVOTk7C
zMxMvPPOO6JOnToiNjZWCJGXWsTBwUGoVCqxbds20ahRI1GuXDkRHx8vhBBiypQponLlykKj0YgB
AwaIcePGiYYNG+rsc+nSpaJ27drCyMhImJiYiJYtWyrrPD09hUajEfr6+kpqB0dHR3HmzBlRqVIl
nVyxKpVKBAQEiNTUVGFtbS0aNmwoqlatKipUqCC+++474eLiIvT19YVKpRLt27cXHTt2FEOHDhWA
sLCwEMOHDxc5OTni6NGjQqVSifPnzwshhFizZo0wMTERK1asEKmpqWLKlCmifPnyws3NrZSujtej
JGkKirpGXhdra2thZGQkVq1aJc6cOSO8vLxEixYtlHQxLi4u4r///a9Qq9Wibdu2wsrKSkkREx0d
LQwNDUWLFi2Es7OzCA4OFtnZ2cLX11cAwtzcXJiamgpAlCtXThgaGoqAgACxaNEisXjxYmFhYSG6
desmAgMDxdWrV8WVK1eEnZ2d+OSTT4RarVZS1dSvX1/4+PiITZs2Pb4u81OSGAkwe/xv3j6GDRsm
OnfuLNzc3ISpqalYtmzZaz7Dz+bP62fV4+tn1UtLc/GmpNQoOG/B/fv3hampqUhISNCpM2DAANGr
Vy8hhBDfffedklonOTlZVKtWTXzwwQdi/PjxQgghBg4cKPr06VOifZfkO+Tv5smc8cHBwUqqn/x/
o6OjhUqlUlKLDBo06PF5GiHA+XG6my4ClgtA1KhRQxgZGQlLS0sl5ZQQee9ncSmGhBDi/Pnzol27
dsLCwkKYmpqKunXrim3btr3Q8d2/f1+EhISIypUrCyMjI9GiRQtx+PBhIYQQjRo1EpGRkUrdDh06
CAMDA3Hnzh0hhBC//vqrUKlU4syZM0KIvFRH06dPF/369Ss21ZEkSZIkSZL0esjUIpIklTkliaZ7
Wp3WrVvj6elJu3btaNeuHZ06dSoQGZmnqBQa1atXZ9KkSYwbN46qVasSEhJS4n7HxMTg5ORERkYG
Dx48wMDAgKtXrzJjxoxCdT/++GM+++wzTp06Rf369VmzZg3Tp0/n888/JzExERsbGxYtWqTTxzVr
1hAeHs6MGTNISUnB3t6en376iVWrVgHw66+/cuvWLaytrYmPj8fPz4/U1FRq165NgwYNlHY2bNhA
fHw8QggCAwPp1q0bx44do1mzZmRnZzNz5kyWL1/Orl27lP3v2bOH3377DbVazZIlS4iOjiY6OrrQ
eezZsyfjx49n9OjRNGrUiPPnzxMcHIyRkVGJz+ObpqylKcjKyuLSpUt4enrSu3dvHj58yMOHD6la
tapSZ/To0TRv3hyAsLAwfvvtN+DP9zInJ4dFixZhYmKChYUFxsbGPHz4EJVKRVJSEuvWrUOlUhEb
G8upU6eIjo5myJAhlCtXDgBjY2PKlSuHpaWlEgGqr6+vk2ZGrVbj7e1d4NpoCAQBPkAysAuA8uXL
s2DBAjQaDba2trRt25YffvjhpZ2/l2HdutX4+jYlL+LcBuiDr29T1q1bXar7eVOv1bS0NLKzs2nd
ujXm5ubKa9WqVcpnuaenJ7dv3+bIkSPEx8fj4+OjE6UdHx+Pl5dXifbn5OSEn18genojyYs0vgis
Rk9vFH5+gTg6Or6U43yVfHx8lKc+LC0t8fPz00ktEhUVRd26dbGwsMDQ0JD69etz4cIFhBAcP34c
gBs3bjxubS+gB+QCm4HFAPj6+nLv3j2uXbuGWq1GT0+PlStXMnz48GJTDAEMGzaMBw8esH//fo4f
P85nn32GmZnZCx3v6NGj2bx5M6tWreLIkSM4ODjg5+fHjRs3niuaPzIykiZNmhSZ6kiSJEmSJEn6
m3jRkfBX/UJGZEtSmfR8EdmvL+LuryJxDx06JNRqtRIZlj8h3pYtW3TqNW3aVIwcOVKnrEWLFjqT
JDo4OIj169fr1Jk6darw8PAQQgglOq6ggpMNAmLmzJnKuuvXrwsTExOxceNGIUTeZINqtVr88ssv
Om0EBweLmjVr6kTkde3aVfTo0aP4k1JA69atRVBQUInqvoliYmIeX2sXnrjWLghAxMTECCGE8PHx
eSMisg8ePCgA0aNHD+HnF6gTie/p6SNUKpU4fPiwWLhwoShfvrzIzMwUgDAwMBCbNm0S0dHRwsjI
SNy8eVOYmZkpx9S5c2cBiP3794vc3FzRunVrodFoRJcuXcTSpUtFZmamWLt2rdBoNCI4OFh06tRJ
6ZOdnZ2YOHGizuShDRs2FG3bthV16tQp0EcDAf/U+V328fERQgilzVGjRolWrVq9+hNbCrRa7Uud
UK+k1+qrUDAi++effxYqlUrs27dPpKen67x+/fVXZRs3Nzcxe/Zs8d5774klS5aIjIwMYWRkpEyW
mpaWVuL9Z2RkFLr+/fwCRUZGRqkf6+vg7e0tNBqNGDt2rEhNTRWnT5/Wecro9u3bQl9fX7i4uIhT
p06J7du3C2trawGIAwcOCCEKRmTbCdgn4JSAagLyJon95ZdfRFhYmDAzMxPBwcHiypUrQqvVCn19
fXH58mWd/vj6+opPPvlECJH3tMXkyZNL7Vjv3LkjDA0Ndb7/Hj58KKysrMSsWbOeOZrfzs5O9O3b
V2cfVapUEYsXLy61PkuSJEmSJEnPR0ZkS5JU5pQkmu5NjbhLTEykffv22NraotFolAjCvXv3KnVU
KhWNGjXS2e706dM0adJEp8zd3V35OTs7m/T0dPr3768T0Tht2jTOnDkDQNWqVcnJycHZ2ZlRo0ax
a9cumjVrRmpqKidPngTyzm2+ihUr4uzszKlTp5QyQ0ND6tatW+i46tSpoxN5Xa1aNa5evVqo3t27
dxk/fjyLFy9m+/btTJw4kR9++IHg4OCnnrs31Z+R/HufWBMP/JnjePfu3URGRr66jhXD2NgYgO+/
38quXQeARcBBwIi9ew8g+7ryQwAAIABJREFUhGD//v2Eh4fz0UcfoVKpUKlU+Pn5ERYWxqlTpzA0
NKR///7o6ekp77tGo8Ha2pqgoCC+/fZblixZQmRkJBkZGUybNg1nZ2fKlStHVlYWly9f5v79+9y9
e7fYfmZmZrJjxw5CQkJwd29G3lQcZsBVYA5q9TBMTU2VKO98BSdZLWscHR0JCAh4aZ9PJb1WXzUX
FxfKlSvH+fPnC80hYGVlpdTz8vJiz5497Nu3D29vbywsLHB2dmbatGlUr1690FM1f8XCwoLt27ei
1WqJiYlBq9WyfftWLCwsXsYhvjRPTthYkIODAxERETg4OOh8tgOsXr0alUqFr68vtWrVws/Pj+7d
u+vUyZ+/Qa2+DpwDTAE7QNC6tT9169bFzMwMQ0NDbt++TeXKlUlNTSU3NxcnJyed76K9e/cqEdkj
R45kypQptGjRgvDwcH755ZcXOgfp6enk5OQoT5FA3hMe7u7unDp1Ck9PT27duvVM0fz16tXTWa5a
tWqR32mSJEmSJElS2aX/ujsgSdLbY9261fTo0ZsdO/ooZb6+gTqP4pekzquUnZ2Nv78/AQEBfPHF
F0yfHsH+/XkDSgEBAfj5BTJixFAATE1NC23/ZKoTUSANQ1ZWFgDLli3TGeAG0NPTA8Dc3Jxu3brx
r3/9i9jYWLp27YqLi8tf9lkIobPf/EHQJxkYGBTq65ODiRkZGXTr1pPY2B1KmUajYeXKlfj4+Pxl
P95k+TdNYmNHkpsryEtfE4+e3ih8fd+8NAWOjo6UK1eO27dvAeWA4cBZYCd5qS3OM3nyZIYMGcIn
n3zC7du3gbwJIVevXk1UVBT379+nRYsWXLx4USctTKNGjWjYsCFhYWFcunSJd955h2bNmvHdd98R
GBjIhQsXGDJkCF9++SX37t3j888/Z8KECUWm8cnOzsbGxobBgwfTtWtXOnfuQlzcD0Am8CFGRiZU
q1a90LUnFe9NvVbNzMwICwsjNDSU3NxcWrRowc2bNzlw4ADly5enT5+8z3AvLy/mz59P5cqVlb56
e3uzcOFCunXr9lz7dnR0fON+R0tL48aNi12n1WoxNTVVvh+AYidI9fL6J3v29NEpi4z8XGc5//M+
KysLfX19kpKSUKt1Y1zy04f0798ff39/tm7dys6dO4mIiGD27NkMHz685AdXQP53YVHfkSqVivLl
y1O/fn327NnDjz/+iJ+fH56ennTv3p20tDRSU1Px9vbW2bYk32mSJEmSJElS2SYjsiVJemVKEk33
pkXcpaSkcP36dWbMmEFU1AJ++uk4MIS8j8/pxMYmMHny1CK3dXZ25uDBgzplhw8fVn6uXLkyVlZW
pKenF4potLW1VeolJibSpUsXFi9ezIYNG/jxxx+xt7dXBrQLRl9fv34drVb71MHukurZsw979hwi
L0L+ArCaO3f0WbVqbam0/zq9qhzHpaFcuXJ06dLl8VIEkApcfvzvOgCmTJnCtGnTdAaijI2NWbVq
FV988QUVKlRg4MCBnD59WieKV6VSMXHiRNatW8fEiRP57rvvmDNnDikpKfzxxx+4uLiwcOFCJkyY
gJ2dHd27d1eus/fff1+nn59++ikZGRns3LmTP/74g3ffbY65uTn/+Mc/0Gq13LlzhxYtWqCvn3cf
/auvvmLTpk0v78T9Tbyp1+qUKVOYMGECERERuLi4EBAQQExMjE7eYk9PT4QQOje+fHx8ePToUaGB
SKnoG6L5hBCo1Wpyc3N1yoryf//3P+V7tEePHkDeTciiuLq6kpuby5UrVwp9F+XnwwewsrJi0KBB
bNy4kQ8//JClS5c+zyECeZHnBgYG7N+/XynLycnh8OHDyveXt7d3qUXzS5IkSZIkSX8PMiJbkqRX
riTRdG9KxJ2NjQ2GhoaEh4ezY0cMEArEPF7bltxcaw4d6lNkdGpISAgDBw6kUaNGNG/enPXr13Ps
2DGdP77Dw8MZNWoUGo0Gf39/7t+/z+HDh7lx4wYffPABFy9e5LfffqNfv35069aNiIgIVCoVH330
EQ4ODpiZmfH5559Tp04dKlSowPTp07G2tqZ9+/YvfOz5k8zlDWL3elzai9xcwY4dfUhNTX0j3qPn
lX/TJDU1lbS0NBwcHN7o4/n0009ZvXo1MB0YB1Qj76bKLQCsra116qtUKlJTU/ntt9+4evUqOTk5
9OzZE5VKRYcOHQq1r9Fo2Lt3L1FRUdy6dQtbW1siIyNp06YNAAMHDiQ+Pp7GjRtz584d9uzZg62t
rc61P3jwYI4ePUr37t1RqVT06NGDkJAQtm3bpnNus7Ky2LZt2xt/zt8Ub8q1OmrUKEaNGqVTNmLE
CEaMGFHsNhYWFuTk5OiUdejQQWcw9u8sOzubIUOGsHnzZjQaDR999JHO+hs3bjBy5Ei+//57bt68
yblz5xg2bJjOzaaTJ08ya9YsEhISePjwIRs2bGDo0KFYWloqNzK7d+/OtWvXdKK1879H8yeLzGdo
aKgzAO7o6EjPnj0JCgpi1qxZuLq6cvXqVXbv3k2DBg0ICAggNDSUgIAAZfLjPXv2vNANUxMTE4YO
Hcro0aOxsLDA2tqamTNncvfuXfr16we8nGh+SZIkSZIkqWyTA9mSJElFyB+cq1SpEitWrOCDDz54
vGYfMBvIHyj20qlfUM+ePTl79iyjR4/m3r17dO3aleDgYA4dOqTU6d+/P6ampsycOZMxY8ZgampK
vXr1lP3p6+tjZmbG6tWr+eqrrzAwMGDAgAEMGDAAyEtLMmjQINq3b49KpSIgIICtW7fqDGY8r/zc
qOD5xJq8Y05LS/tbDEK+KTdNnubPFBMJ5OYu48kUE+3atVPqli9fntzcXI4ePcqAAQPQarUYGhpy
9+5d9u/fr+TR/eqrr5RtatWqxbZt24rdf6VKldi+fXuh8oIDkoaGhixfvpzly5fr1Jk2bRqQl6rm
8uWr7Nq1i127dgHg55eXOqis5Tl+HcrKtVocrVZLenr6W3UDIywsjH379rFlyxYsLS35+OOPSUxM
xNXVFYC+ffuSnp7O999/z6hRo/jjjz9o27YtJ0+eRE9PDyEEkyZNYubMmSxYsAAPDw+uX79O3bp1
EUIovzeDBg2ib9++TJw4Uef3uih2dnbcvn2bmzdvcv36dczNzYmOjmbq1KmFUgzlf67k5uYyYsQI
fv31VzQaDQEBAS88f0BERARCCIKCgrh9+zaNGzdm586dlC9fHig+mn/+/PmFovmL+g4uqkySJEmS
JEkq4150tshX/QLcAJGYmPjcs2VKkiQ9q9OnTz+eZXe1AFHgtUoAQqvVlqid1q1bi6CgoJfc29JR
WscslZ6MjAzh5xeYP+OzAISfX6DIyMh43V0rET+/QKGnV/HxNXVBwGqhp1dR+PkFvu6uSS/R9evX
y/R1+7yysrJEuXLlxP/+9z+lLCMjQ5iYmIjQ0FCRmpoqVCqVSEhIEEII4ePjI4YOHSpMTEzExo0b
hRBCAMLf31/Z/qeffhIODg4CEI0aNRIffvihAMTRo0eFEELExcUJtVotbt68qWxz9OhRoVarxfnz
54UQQty/f1906dJFWFhYCLVaLVasWPHSz4UkSZIkSZL09kpMTMz/O8BNvOC4sIzIliRJKoHnmXDt
7t27fPHFF/j5+aFWq1m3bh0//PADsbGxL9SX0opqfFo7b+okc2+zNyXFxPP4u6eqkYrXs2cfYmMT
yHvvPYG9xMaOpEeP3mzfvvU19+7lSU9P5+HDhzqT+ebneYa8+Q0MDAyU9bt37wYgISFBSRnSpEkT
4uLiMDc3V9oQQqCnp8eaNWvYv38/KpWK1q1b4+/vj7+/P1lZWTqT/DZo0KDQkxNff/11iY+jLETS
l4U+SpIkSZIkSS9OTvYoSZJUQs864ZpKpSImJgZPT0+aNGnC1q1b2bRpk85j0gDx8fGo1Wpu3br1
l/vPyMjA378tzs7OBAYG4uTkhL9/WzIzM5/pOJ6lnTd1krm3naOjIwEBAWVqwKYkqWqkv5/8Gxi5
ufPIu4FhTd4NjCh27IghNTX1Nffw5RGP81AXl+Iif31R5fnbZGVlMXjwYI4dO0ZycjLh4eF8+eWX
7N69m+PHjxMeHk7v3r1Zv3491atXZ+LEiTRo0KDI7xOtVsu2bdtKfM5L6zvnZSoLfZQkSZIkSZJK
jxzIliRJKqH8aFitVktMTAxarZbt27cWm9vXyMiIXbt28ccff3D79m0OHz5c5CR7ULJcnrpRjReA
1cTGJtCjR+9nOo5naedZj1mSiqNW5/+XY+8Ta+KBvHzw0t/P23wDw8HBAX19fRISEpSyzMxMtFot
AC4uLjx8+JCff/5ZWX/9+nW0Wq0ykaKbmxsnTpygZs2a2Nvb8+jRI8aOHYu/vz9jxoyhW7duLFmy
hJYtWxIREUFycjLnzp1Torvh+Qd7S+s752UqC32UJEmSJEmSSo/8q1GSJOkZleaEazk5OSWqV1pp
GZ63nbI+yZz0+j169Ii8++cjyUuPlpeqBkYB6hL/Lkhlyz/+8Y/HP+3lz88cyL+B4eDg8Kq79MqY
mprSv39/Ro8eTcWKFbG0tOQ///mPMhmvg4MDHTp0YODAgXzxxReYmZkxbtw4rK2tad8+b0LhsWPH
0qxZM0JCQhgwYACdOnXCycmJ2NhY5s+fz9atW1m6dCmenp5YWFiwdetWhBBK+hJ4vtQuZSEVUFno
oyRJkiRJklS6ZES2JElSCa1atYpKlSrx8OFDnfIOHToQHBwMwKJFi3BwcKBcuXLUrl2b1at1U3Co
1Wq++OILOnTogLm5OdOnTy+0n7t37xIQEMC7776rPB5eWlGNb3N0pPR65Q1oPiI/RY3uv4/+1gOa
b7P8XPt6eiPJG3C8CKxGT28Ufn7Pn2v//fffp3PnzqXZ1Zfi888/591336V9+/a0adOGd999l0aN
Ginrv/rqKxo1akS7du3w8PBArVazdetWZbC7Xr16xMfHk5qaiqenJ25uboSHh2NlZQVAhQoV2LRp
E61atcLFxYUlS5awfv16ateuDTx/apey8F1RFvooSZIkSZIklS5Vcfn53lQqlcoNSExMTMTNze11
d0eSpLfIvXv3qF69OkuXLuW9994D4Nq1a9SoUYNdu3Zx/fp1unfvzrx582jVqhVbtmxhzJgxxMbG
4uWV94e1Wq2mSpUqRERE4OXlhb6+Punp6bRs2ZLMzEwePXrEv/71LzQaDZs3b6ZcuXJA3mBEXoRd
wcgzHi/3QavVljgiuzTayefj44OrqyuRkZEl3kZ6e/n7tyU2NoHc3I+BysBV9PRm4Ovb9G896d/b
LjMzkx49ej+Ons3j5xfIunWrn5qm6Pz589SsWZOjR49Sv359pfz27dsIIdBoNC+t338H27ZtIzAw
kLy0G9YF1lwEbIiJiSEgIKDQdqX9XfEylIU+SpIkSZIkSZCUlJQfzNFICJH0Im3JiGxJkqQSMjIy
okePHnz11VdK2apVq7CxscHT05PZs2fTr18/Bg8ejIODA6GhoXTu3JlZs2bptNOrVy/69u2LnZ0d
NWrUUMovX76Mt7c3VlZWfPfdd8ogNpReVOPLio58GUo6CaZUdvw5eehooC8wWk4e+hZ4kVz7BSc+
LMjc3FwOYvP0CRx1U7sU9NepXcrCd0VZ6KMkSZIkSZJUuuRAtiRJ0jMYOHAgO3fu5PLlywCsWLGC
999/H4BTp07RvHlznfoeHh6cOnVKp6zgY+X5hBC0bt0aR0dH1q9fX+TEd38OAv6ZluF5BgFLq52X
LX8Aq6w9OfS2WrFixVMHJuXkoW++jRs3Ur9+fUxMTKhUqRJt2rTh7t27CCGYPHky1tbWGBkZ4erq
yo4dO5Ttzp8/j1qt5ptvvsHT0xMTExPc3d1JTU3l0KFDNGnSBDc3N+bPn0/FihV19rls2TJcXFww
NjbGxcWFRYsWKevs7e0BaNiwIWq1mpYtWwIQHBysk1rEx8eHkSNHEhoaSsWKFalatSrLly8nOzub
fv36odFocHR0ZPv27Tr7Pn78OIGBgZibm1O1alWCgoK4fv36U8/H61bSCRxfZLC3LHxXlIU+SpIk
SZIkSaVHDmRLkiQ9g4YNG1K/fn1WrlxJUlISJ0+eVPJjA4UiB4uKJjQ1NS2y7X/961/s3buXEydO
FLm+tAYBS3swMScnh5CQECpUqIClpSUTJkxQ1j148ICwsDBq1KiBmZkZzZo1Iz4+Xll/4cIF2rdv
T8WKFTEzM6NevXps376d8+fPKwNWFhYW6Onp0a9fv+fqn/TqFLzWJ02ahKura5H1HB0dCQgIkBGT
b5jff/+dnj17MmDAAFJSUoiPj6dz584IIZg7dy5z5swhMjKSX375BT8/P9q3b18gT3Ge8PBwJkyY
wJEjR9DX16dnz56MGzeO+fPns3//ftLS0nQ+I9asWUN4eDgzZswgJSWF6dOnM2HCBFatWgXAwYMH
EUKwe/dufv/9dzZt2gQU/qwFWLlyJZaWlhw6dIiRI0cyZMgQunTpgoeHB0eOHKFNmzYEBQVx7949
AG7evEmrVq1o1KgRSUlJ7Nixg6tXr9K1a9enno/XTXcCxwvAamJjE+jRo3ehus872FsWbjyVhT5K
kiRJkiRJpUgIUaZegBsgEhMThSRJ0uuwaNEi4eTkJEaMGCH8/f2Vcg8PDzF48GCdul27dhXt2rVT
llUqlfj222916sTFxQm1Wi1u3rwpwsLCROXKlcXJkydf7kGUEm9vb2Fubi5CQ0OFVqsVa9euFaam
pmLZsmVCCCEGDBggWrRoIQ4cOCDOnDkjZs+eLYyNjUVaWpoQQoi2bdsKPz8/ceLECXH27FmxdetW
sW/fPvHo0SOxadMmoVarRVpamrhy5Yq4devW6zxU6Smio6OFhYWFshweHi5cXV1Lpe2cnJxSaUf6
a0lJSUKtVosLFy4UWmdlZSUiIiJ0ytzd3cWIESOEEEKcO3dOqFQq8dVXXynr169fL9RqtYiLi1PK
IiIiRO3atZVlBwcHsX79ep12p06dKpo3b67TbnJysk6d4OBg0alTJ2XZ29tbeHp6Ksu5ubnCzMxM
9O3bVyn7/fffhUqlEj///LOyn4Kf4UIIcfHiRaFSqURqaupfno/X6fTp0wIQsFqAKPBaJQCh1WqL
3E6r1YqYmJhi10uSJEmSJEnSy5CYmPj4/6+4iRccF5YR2ZIkSc+oV69eXLp0iWXLlulECY8ePZro
6GgWL15MWloakZGRbN68mdGjRz+1TfE4wu/zzz+nV69etGzZktOnT7+0YyhNNjY2REZG4ujoSI8e
PQgJCWHOnDlcvHiR6OhovvnmG5o3b07NmjX58MMP8fDwUPKMX7x4EQ8PD1xcXLCzsyMwMJAWLVqg
UqmU9AOWlpZUrlwZc3Pz13mYbwUhBDNnzsTR0REjIyPs7OyYMWNGkfnKk5OTUavVXLhwoVA7K1as
YNKkSUodPT09Vq5cqaSfOHbsmFL35s2bqNVq9u7Ny+Gbv6/t27fTuHFjjIyMOHDgAADffvstjRo1
wtjYGAcHByZPnsyjR49e8ll5ezRo0IBWrVpRt25dunbtyrJly7hx4wa3b9/mt99+K1HqpHr16ik/
V6lSBYC6devqlF29ehWA7Oxs0tPT6d+/P+bm5spr2rRpnD179pn7X3AySLVazTvvvFNkf/L3n5yc
zO7du3X2Xbt2bVQqFenp6TRo0ICWLVsWOh+v259R8J5PrMmbVDgtLa3I7eSTEJIkSZIkSVJZVzgJ
qyRJkvSXzM3Nee+994iJiaFjx45KeYcOHYiKimLWrFmMGjWKmjVrEh0dzbvvvqvUKepx+CfLIyMj
yc3NpVWrVsTFxRU7GdebomnTpjrLzZo1U9IP5Obm4uTkpPMo/oMHD6hUqRIAI0eOZOjQoezYsQNf
X1/ee+89nYEn6dUaN24cy5cvZ+7cuXh4eHD58mVSUlKAoq/d4q7nbt26cfz4cXbs2MEPP/yAEILy
5cvz+++/F7vNkz7++GNmzZqFvb09FhYW7N+/n759+7JgwQLeffdd0tLSGDRoECqVik8//fT5D1pS
qNVqdu7cyU8//cTOnTuZP38+//nPf9i5cydQstRJBgYGys/5654sy7/5kJWVBeTlyHZ3d9dpR09P
75n7X3A/+ft6sgzQ2X/79u2ZOXNmoXQh1apVQ61Ws2vXrkLn4+eff8bW1vaZ+1dadCdw7FVgzV9P
4ChJkiRJkiRJZZ0cyJYkSXoOly5donfv3oUGSQYPHszgwYOL3S43N7dQmZeXV6HyqKgooqKiSqez
r8mdO3fQ19cnKSkJtVr3ASAzMzMA+vfvj7+/P1u3bmXnzp3MmDGDyMhIhg8f/jq6/FbLyspi3rx5
/Pe//6V377w8uzVr1qR58+Y6ec1LwsjICDMzM/T19bG0tNRZ9+SAYXGmTJlCq1atlOVJkybx8ccf
K32ztbVl8uTJjBkzRg5kl7JmzZrRrFkzPv30U2xtbfnhhx+wsrJi//79tGjRQqn3448/8s9//lNZ
LulNinyVK1fGysqK9PR0unfvXmQdQ0NDoOjPzhfl5ubGpk2bsLW1LfQZVdCT52Pz5s188MEHpd6f
ksqfwDE2diS5uYK8SOx49PRG4ev71xM4SpIkSZIkSVJZJgeyJUmSnsGNGzfYs2cP8fHxLFq0qNTa
1Wq1pKen4+DgUOYGIRISEnSWf/rpJxwdHXF1dSUnJ4crV67g4eFR7PZWVlYMGjSIQYMGMX78eJYu
Xcrw4cNf6gCWVNipU6d48OCBMsnm66RSqWjUqJFOWXJyMj/++CNTp05VynJzc3nw4AH37t3DyMjo
VXfzb+fgwYP88MMPtGnThsqVK5OQkMAff/yBi4sLYWFhhIeHY29vT8OGDfnyyy9JTk5m7dq1yvZF
3aR42o2L8PBwRo0ahUajwd/fn/v373P48GEyMzMJDQ2lcuXKGBsbs337dqysrDAyMkKj0ZTK8Q4f
Ppxly5bRvXt3xowZQ8WKFUlNTWXDhg0sX76cQ4cOFXs+Xrd161bTo0dvduzoo5T5+gY+dQJHSZIk
SZIkSSrL5EC2JEnSM3B1deXGjRtKHuEXlZGRQc+efdixI0Yp8/PLG4ywsLB44fZfhYsXLxIWFsag
QYNITExkwYIFzJkzBwcHB3r16kVQUBCzZs3C1dWVq1evsnv3bho0aEBAQAChoaEEBATg5ORERkYG
e/bsUQaJbG1tUalUbNmyhcDAQIyNjTE1NX3NR/v3ZWxsXOy6/GjVgoOSDx8+fOZ9PEs7T77XWVlZ
TJ48mc6dOxeqKwexS4dGo2Hv3r1ERUVx69YtbG1tiYyMxM/PjzZt2nD79m3CwsK4evUqLi4ubNmy
pUCai2dLP5Ovf//+mJqaMnPmTMaMGYOpqSn16tVTIp719PSYP38+kydPZsKECbz77rvs3r27RPt5
Wlm1atU4cOAAY8eOxc/Pj/v372Nra4u/vz8qlarY89GmTZu/PKZXwcLCgu3bt5KamkpaWlqZvAkq
SZIkSZIkSc9KVdJHfN8UKpXKDUhMTEzEzc3tdXdHkiTphfj7tyU2NoHc3HnkTdy1Fz29kfj6NmX7
9q2vu3tP1bJlS+rUqcOjR49Ys2YN+vr6DBs2jMmTJwN5EbNTp05l5cqVXLp0iXfeeYdmzZoxadIk
6tSpw8iRI9m+fTu//vorGo2GgIAAIiMjlUH8adOmsXDhQq5evUpQUBBffvnl6zzcv7X79+9TsWJF
5s+frzOJKUBKSgouLi6cPHmSWrVqAbB06VKGDBnC2bNnsbGxYcWKFYSGhpKRkQHAjBkzWL9+PcnJ
yUo79+7dw8TEhJiYGPz9/QHYtWsX/v7+7NmzB09PT+Lj42nZsiWZmZk6kbctWrSgdu3aLF269GWf
CoWPjw+urq5ERka+kv29//773Lx5k02bNr2S/f2VmjVrEhoaysiRI193VyRJkiRJkiRJKsOSkpLy
n7htJIRIepG2ZES2JEnSa6LVah9HYq/mzwm7epGbK9ixow+pqalvfIRdwcjIhQsXFlqvp6fHxIkT
mThxYpHbz5s37y/b/+STT/jkk09erJNSiZQrV46xY8cyZswYDAwM8PDw4Nq1a5w4cYKgoCCsra0J
Dw9n6tSpnD59+qmDu3Z2dpw9e5bk5GRq1KiBubk5RkZGNG3alM8++ww7OzuuXLlSZH7rom6yT5gw
gXbt2mFtbc2///1v1Go1ycnJHD9+nClTppTaeZAkgBo1avCvf/2Ljz766I3/HJYkSZIkSZKkt0Xx
M9tIkiRJL1V6evrjnzyfWOMFQFpa2ivtz5tCq9Wybds2UlNTX3dX3joTJkzgo48+YuLEibi4uNC9
e3euXbuGvr4+69atIyUlhQYNGvD5558zbdq0v2zrvffew9/fHx8fHypXrsz69esB+PLLL3nw4AGN
Gzfmww8/LLKdolJCtGnThu+//55du3bh7u5Os2bNmDt3LnZ2dqVy7NLbacWKFTppnDIyMvD3b8ul
S5dYvHgxTk5O+Pu3JTMz8zX2UpIkSZIkSZIkkAPZkiRJr82fuWX3PrEmHgAHB4dX2p/XLX8AydnZ
mcDAQDmA9Jp8/PHHnDlzhnv37nH27FnGjh0LQPPmzTl69Ch37twhLi6Ozp07k5ubi42NDQB9+/ZV
0oqcP38eIyMj/vOf/5CRkUFubi5BQUEA1KpViwMHDrB161aOHDlCkyZNyM3N5ezZs1SsWBEvLy9y
c3OLnNCvdevW7Nu3j6ysLDIzM/npp5/o379/qRx3dnY2QUFBmJubY2VlVSji/MGDB4SFhVGjRg3M
zMxo1qwZ8fF5v6u3bt3CxMSEnTt36myzadMmNBoN9+7dA+DXX3+lW7duWFhYUKlSJTp27Mj58+eL
7dODBw8YOXIkVapUwdjYmHfffZfDhw8r611dXVGpVMTExGBoaIihoSHNmjXjxIkTOu3s378fT09P
TExMsLW1ZdSoUWQ46lgiAAAgAElEQVRnZyvrr127Rrt27TAxMeEf//iHzgSOZVlJ8rgLIXRunPTs
2YfY2ATAEggHVhMbm0CPHr1fSX8kSZIkSZIkSSqeHMiWJEl6TZycnPDzC0RPbyR56UUuAqvR0xuF
n1/gW/c4+58DSKuBC5TmAJL06j1tkr8n63Tv3h2tVlts3ZcdqR8WFsa+ffvYsmULO3fuJC4ujsTE
RGX98OHD+fnnn/n666/55Zdf6NKlCwEBAaSnp6PRaGjbti1r1qzRaXPdunV07twZIyMjcnJy8PPz
o3z58hw4cIADBw5gbm6Ov78/OTk5RfZp9OjRbN68mVWrVnHkyBEcHBzw8/Pjxo0bAEydOhWVSsWY
MWPYsGEDCQkJWFpa0r59e3Jzc4G8Jz8CAgLo0qULx48fZ8OGDRw4cICQkBBlP3379uXSpUvEx8ez
ceNG/vvf/3Lt2rXSPsUvnY+PDyEhIYSGhmJpaYm/vz9z5syhfv36mJmZYWNjw/Dhw5VB/Pj4ePr1
68fNmzdRq9Xo6emxY0fM4zkLTAFDYDe5udns2BHD1KlTdfb3tBsT77//Pp06dWL69OlYWVkp+eUl
SZIkSZIkSXpOQogy9QLcAJGYmCgkSZLKuoyMDOHnFygA5eXnFygyMjJKbR/e3t4iNDS01NorSnh4
uGjYsOFzb3/69OnHx79agCjwWiUAodVqS7G30st27tw5oVKpRHJycrF14uLihFqtFjdv3vzLtq5f
v/7Sf0eysrJEuXLlxP/+9z+lLCMjQ5iYmIjQ0FBx4cIFoa+vLy5fvqyzna+vr/jkk0+EEEJs3rxZ
aDQacffuXSGEELdu3RLGxsZi165dQgghVq1aJWrXrq2z/f3794WJiYlSJzg4WHTq1EkIIcSdO3eE
oaGhWL9+vVL/4cOHwsrKSsyaNUsIkXcOVSqV+Oabbwr1O79swIABYsiQITr73bdvn9DT0xP3798X
p0+fFiqVSuf/VSkpKUKlUomoqKhnPZWvlbe3t9BoNGLs2LFCq9UKrVYroqKiRFxcnDh37pzYs2eP
qF27thg+fLgQQogHDx6IqKgoUaFCBXH16lWxdu3ax9fYBQF2AioJWCRgnwCEWq0Wp0+fFkLkvRcu
Li5i4MCB4sSJEyIlJUX07t1b1KpVSzx8+FAIkfd+mpubi759+4qTJ0+KkydPvrZzI0mSJEmSJEmv
S2JiYv7fcm7iBceFZUS2JEnSa2RhYcH27VvRarXExMSg1WrZvn2rTs7WsqIkEbjFkfnC3yz5ka0h
ISFUqFABS0tLJkyYoKxXq9V89913OttYWFiwcuVKnbJTp07h4eGBsbEx9erVY+/eJ9Po/KlgrmIf
Hx8+/PBDtmzZQs2a9o8nRTUHAoDV7NgRQ6tWrUvrcElPT+fhw4e4u7vrHI+zszMAv/zyC7m5uTg5
OWFubo65uTkqlYq4uDjl2nVwcODOnTtoNBrc3NzYuHEj5cuXp1WrVgAcO3aM1NRUZXtzc3Peeecd
7t+/X+D61+1TTk4OzZs3V8r09fVxd3fn1KlTAHzwwQcANG3alJo1azJv3jyl3/l1kpOTiY6O1tmv
v78/AGfPniUlJQUDAwPc3NyU/Tg7O1OhQoVSO7+vkoODAxERETg6OuLo6MjIkSPx8vLC1tYWb29v
pkyZwtdffw2AgYEB5cuXR6VSYWlpmT+TOn+me2oLDAHOAVCxYkXi4uIAWL9+PUIIlixZgouLC87O
zixfvpwLFy4odQDMzMxYtmwZtWvXpnbt2q/gDEiSJEmSJEnS35f+6+6AJEmShDLo8rbSzRfeq8Ca
tzNf+Jtg5cqV9O/fn0OHDnH48GEGDhyIra3tM+WkHjNmDFFRUdSuXZvZs2fTrl07zp07V+yNmoI3
Q86cOcP8+fMfp92YCfgDW8m7Pm5w5MgIUlNTS+X3RuQ98VXszZisrCz09fVJSkpCrc6LAXBwcGDh
woV07NgRyEvzUbVqVerUqcP69evp1q0b3bt3V9rMysqicePGrF27VtlfPktLyxL3STyR07k4Bfc7
ePBgRo0aVWi/NjY2pKSkPLWtsqRx48Y6y7GxsURERJCSksKtW7fIycnh/v373L17F2NjY526+eme
YmNHkpurBqzJT/fk6xvI779f4urVq4DujYmC8m9M+Pr6AlCvXj309eV/tyVJkiRJkiSpNMiIbEmS
pLfImjVraNKkCRqNhmrVqtGrVy+dXLjx8fGo1Wp2795NkyZNMDU1xcPDo1Be4oiICKpWrUr58uUZ
MGCAMpnd85L5wt881tbWREZG4ujoSI8ePQgJCWHOnDnP1EZISAgdO3bE2dmZRYsWUb58eZYvX16i
bQ8ePIiXl9fjpe5APWDc4+X2QOlF6js4OKCvr09CQoJSlpmZqeTsdnV1JScnhytXrmBvb4+9vT0A
VatWpXLlykBeBHXr1q2Jj4/n8uXL7Nmzh969/8zv7ubmRmpqKpaWlkob+a8nB0Pz+2RgYMD+/fuV
spycHA4fPoyLi4tSJoQost/50b9ubm6cOHGCmjVrFtqvvr4+tWvXJicnRycf+OnTp5U83GWNqamp
8vP58+dp164dDRs2ZNOmTSQlJbFw4UKg+IkX161bja9vU+APYCrQB1/fpqxbtxqVSsWjR4+AP29M
HDt2jOTkZOWl1Wrp2bNnkf2RJEmSJEmSJOnFyIFsSZKkt8jDhw+ZOnUqx44d49tvv+X8+fO8//77
her95z//Yc6cOSQmJqKvr0+/fv2UdV9//TWTJk0iIiKCw4cPU61aNf773/++cN/+HEDqA9hQcABJ
evWaNm2qs9ysWTNSU1OVgbxnbUNPT4/GjRsrKS+e5tq1awUmQawHTCqw1hbIG+w9f/48arWab775
Bk9PT0xMTHB3dyc1NZVDhw7RpEkTzM3NCQwM5Pr160oLcXFx/POf/8TMzIwaNWpQsWJFQkND2bNn
D8ePH8ff35+7d+8yb948AgICqFevHn369GHz5s2cO3cOgI0bN7Jt2zbUajVJSUmsWLGC+/fv06pV
K+zt7QukqoBevXpRqVIlOnTowP79+zl37hxxcXGMGjWK3377rdDxm5iYMHToUEaPHs2OHTs4efIk
AwYM4O7duzq/jwCTJ0/m7t27/PbbbwQHB2NpaUmHDh0AGDt2LD/99BMhISEkJyeTlpbGt99+q0z2
mHcTyY9BgwZx8OBBEhMTGThwICYmJiV6n95kiYmJPHr0iFmzZuHu7o6DgwOXLl3SqWNoaKhMjAl/
pnuqUaMGgwcPLjbd07PemJAkSZIkSZIk6cXJgWxJkqS3SHBwMH5+ftjZ2eHu7s7cuXPZtm0b2dnZ
Sh2VSsX06dNp0aIFtWrVYty4cfz44488ePAAgKioKAYOHEhwcDCOjo5MmTJFJ0L0ef2d8oX/3alU
qkJpKoqLcC1q25LIzc2lYsWKvPuuFypVDnkD2evIi9gXuLo20onUDw8PZ8KECRw5cgR9fX169uzJ
uHHjmD9/Pvv37yctLU3J852bm0unTp3w8fHh+PHjJCQkMGXKFNzd3Wnfvj3e3t4cO3YMZ2dngoOD
Wbx4MVlZWdjZ2REWFkatWrUQQpCWloaNjQ2///47Li4uhIWFMXz4cK5cuUKvXr10jsfY2Ji9e/di
Y2PDe++9h4uLCwMHDuT+/ftoNJoiz0FERATvvfceQUFBNG7cmDNnzrBz507Kly+vcz4jIiLIyMgg
MjKSa9eusWXLFiWdRb169YiPjyc1NRVPT0/c3NwIDw/HyspKaSM6OhorKyu8vb3597//zeDBg5VI
87LMwcGBnJwc5s2bx9mzZ1m1ahWLFy/WqWNnZ0dWVha7d+/m+vXr3L17F8jLR+7i4lLs0yDPemNC
kiRJkiRJkqRS8KKzRb7qF+AGiMTExBeaMVOSJKms2bJli6hQoYKyfPToUaFSqcT48eOVsv79+4ug
oCAhhBAbN24UderUESqVSmg0GjF79mxx+PBh0a5dO2FjYyNUKpUwMDAQgDAxMRG2trZi+vTpQqVS
iYCAAGFmZibq168v1qxZI9Rqtbh48aIQQghzc3Ph7OwsjI2NhY2NjRg5cqQYMWKEcHV1FUIIYWdn
J6ZPny769esnzM3NhY2NjViyZMkrPFPSi/L29hZ16tTRKRs3bpxSVqVKFbFo0SJlnVarFSqVSqxY
sUIIIcS5c+eESqUSn3/+uVInJydH2NjYiFmzZgkhhIiLixNqtVrcvHlTCCFEdHS0sLCwUPZfvnx5
0adPH5GRkSH8/ALzZ7lWXmvWrNHZ11dffaXsa/369UKtVou4uDilLCIiQtSuXVsIIURGRoZQq9Vi
7969RR6/r6+viIiI0ClbvXq1qF69urKsUqnEt99+qyw3bNhQTJo0qdhz+jI0bNhQqFQqcfPmTWFn
ZyeioqJe6f7fND4+PiI0NFSnbO7cucLKykqYmpqKgIAAsXr1ap3rTgghhg0bJipVqiTUarXyHtas
WbPQ+XR1ddV5j69cuSKCg4NF5cqVhbGxsXBwcBCDBw8Wt2/fFkIIERwcLDp16vSyDleSJEmSJEmS
yoTExMT8v+PcxAuOC8vZZyRJksoIT09PsrKyOHLkCK6ursTHx2NpaUlcXJxSZ+/evXz88cckJSXR
rVs3Jk+ezLfffouFhQWffvoparWaTp06sXbtWrp160ZWVha3bt3i66+/Ztu2bUybNg0hBD169GDe
vHmMGTNGiWJ99OgR6enp3L59m3/+85/ExMRw9epVRowYwb179zA0NFT6ERkZyZQpU/jkk0/45ptv
GDp0KF5eXjg5Ob3q0yY9p4sXLxIWFsagQYNITExkwYIFSo7sli1bsmDBApo2bUpOTg7jxo3Tef/z
LVy4EAcHB2rXrk1kZCQ3btzQSWUjnojqLqhly5asW7cOe3t75s6dTXDwdTIzM/n+++9xdnbGzMxM
p369evWUn6tUqQJA3bp1dcryJ+qzsLCgb9++tGnThtatW+Pr60vXrl2pWrUqAMnJyfz4449MnTpV
2T43N5cHDx5w7949jIyMSnweX7a/OoclpdVqSU9Px8HBoUzno9+9e3ehslGjRjFq1Cidsiej5Rcu
XKjkzs535syZQm0lJSXpLFeuXJmvvvqq2P781TpJkiRJkiRJkp6dTC0iSZJURmg0GurXr68MXMfF
xfHhhx+SlJREdnY2v/32G+np6Xh5eREZGYmvry/jx4/HxMQEFxcXunTpQlZWFjNmzMDDwwMDAwPq
1auHSqXC2tqaTz/9lOzsbFQqFR06dMDBwYGxY8dy9uxZZbAsIiKCKlWqoNFosLe3p2nTpsydO5cT
J07o5E5u27YtQ4YMwd7enrFjx1KpUiWdAXfpzRcUFMTdu3dxd3cnJCSE0NBQBgwYAMDs2bOxtrbG
09OT3r17M3r06EI5lfNTXkRERNCwYUN+/PFHtmzZQsWKFXXqFMfOzo5vvvmGLVu24OrqypEjR3jw
4EGxA60GBgaF2n2yrOA1+uWXX5KQkICHhwcbNmzAycmJgwcPAnkT+U2aNElnEr/jx4+j1WrfqEFs
+PNYS5qypaCMjAz8/dvi7OxMYGAgTk5O+Pu3JTMzs7S7KUmSJEmSJEmS9MJkRLYkSVIZ4u3tTVxc
HKGhoezbt4/PPvuM9evXc+DAAf744w+qV6+Ovb09p06domPHjjrb+vr6smLFCqKiohg6dCjZ2dmc
Pn1aWZ8fxVowwrNKlSoFUzuRnJxMRkYGCxYsYNmyZejp6Sm5s/P/Bd3oWICqVasq0bBS2WBgYEBk
ZGShSFWAatWqsW3bNp2yjIwM5WdbW1tlAr1u3boV2b6Xl5fOJHt9+/alb9++OnU6duyoXMedOnUq
Nl/68wziAjRo0IAGDRowduxYmjdvztq1a3F3d8fNzY3Tp09jb2//XO2+KkeOHFF+LiqC+Gl69uxD
bGwCeXnHPYG9xMaOpEeP3mzfvrXU+vk2+btEt0uSJEmSJEnSm0hGZEuSJJUhXl5e7Nu3j+TkZAwN
DXF0dMTLy4s9e/YQHx+Pt7c3kDcY/WSkprm5OQYGBmzcuJE6depw8+ZNOnXqVGgfBQcFn2wjKyuL
YcOGMXr0aExNTZXo7SFDhlCuXDllu4KRsPnbF4yGlaSnyczMZNu2baSmpj61blHpNf4q5ca5c+cY
P348CQkJXLhwgZ07d5KamqpMWjphwgRWrlzJ5MmTOXnyJCkpKWzYsIFPP/30+Q+olGm12hKfn+K2
37EjhtzceUAvwBroRW5uFDt2xDx3u28rGd0uSZIkSZIkSS+fjMiWJEkqQzw9Pbl16xZz585VBq29
vb2ZOXMmmZmZfPTRRwC4uLiwf/9+4M+8sWPGjKFWrVocO3YMgJo1a1KnTh2dqFiA//u//0Oj0eiU
HT16FBsbG9zc3Dhx4gS7du1i5syZL/NQpdfoeSOcS0NGRgbHjv1CXFwc0dHRAPj5BaKvryo2jUZR
/f2rYzAxMSElJYWVK1dy/fp1qlWrRkhICIMGDQKgTZs2fP/990yePJmZM2diYGBArVq1lNQqJe3D
y5CRkUHPnn3YsSNGKfPzC2TdutXFRqwXJT09/fFPnk+s8QIgLS1NRhQ/AxndLkmSJEmSJEkvnxzI
liRJKkMqVKjA/7N373E53v8Dx1/3XaKSRJkkHajIMYecR4qSjcXGFhXGNhtZw9jmK6yfzETYxhxz
zMxhOaSaUznMfIUScleO+zpLSLZOn98f6Vp35ZxDfJ6PR4/d93V9ruv6XNd9dzfv632/340bN2bF
ihX89NNPQEGWdr9+/cjNzVWC26NGjcLZ2ZmgoCD69evHvn37+PHHH5k3b95THX/s2LG0bdsWHx8f
2rRpg4ODA3fu3GHbtm3MmTPnaU9PekmU1jTvefH29uHmTUHxgKCbWxsWLVoEoHXzpWgZk0LFy5aA
dumSGjVqsH79+gfOo2vXrnTt2vW+64vvv3gjwGelrAKmdevWvfcojoKM7EKxANSrV69sJvwaKMxu
L3hNCq9lf/LyBNHRPqSkpMibApIkSZIkSZJUBmRpEUmSpHKmc+fO5Ofns3DhQr744gtMTExwdHTE
3NxcCT45OTmxZs0afvnlFxwcHPD39ycoKAgfHx9lP4+axVp0mYWFBY0bN2PFihUMHz6crl274uPj
S7Vq1Zg0aRJOTk6PnR1bXqjVajZu3Piip/FKK0/lLp62tMeTHrOsro+9vT3u7p7o6PhTEIA9D6xA
R2ck7u6eMvD6GB4lu12SJEmSJEmSpKcnM7IlSZLKmZkzZzJz5kwyMjKUWtRFm74V8vLywsvLCxcX
F5ycnAgICNBaX1pzuOJZpsWzXb29ffjvf09QNBs0K8ufP/88SNu2zqhUqlL3+7yyVZ+lS5cuPVbp
BunxlYdyF2VV2qM4GxsbAgIC8Pf3v++Ysr4+4eEr+OCDAURH/3uDy82t4FykRyez2yVJkiRJkiTp
+ZAZ2ZIkSeVU1apVMTQ0fG7He1g26PXr15/bXF6EGjVqlGhiKZUt7YBgUS9PQFC7tMc5YAXbtu3n
gw8GPNH+cnJyHnlsWV8fExMToqK2oNFoiIyMRKPREBW1Rd6weUwyu12SJEmSJEmSng8ZyJYkSSqn
XFxc+OKLLwD46aefsLe3R19fn5o1a9K3b9/7brdy5UpatWpFlSpVMDc3p3///ly9elVZHxsbi1qt
ZseOHbRq1QpDQ0Pat29PXFxh8KwwG3QqUBP4FCjIWIYXU3Lhcaxdu5YmTZpgYGCAqakp3bp14+7d
uwAsXryYRo0aUalSJSwsLLSyY4uXFvnrr7/o168fJiYmmJqa8s4773D27Fll/aBBg/Dy8iIkJIRa
tWphamrK8OHDtTLcs7OzGTt2LHXq1KFSpUo4ODiwZMkSZX1SUhKenp4YGRlRs2ZNfH19X+kbBk8b
ECzttc3KytL6XSnk5eXF4MGDlec2NjYEBQXh7e1N5cqVqV27tlKHvpBarb53M8cSGAp0BipplfZI
SkrC1dVVmcPHH3/MnTt3lH0Uvi+mTJmChYUF9evXx8XFhbNnzxIQEIBarUZHR+eZXJ/7sbOzo3v3
7jLg+hTCw1fg5tYG8AHqAD64ubWR2e2SJEmSJEmSVIZkIFuSJKmci4+PZ+TIkQQFBd3Lmo7mzTeL
lx74V05ODkFBQSQmJhIREcHZs2cZNGhQiXHjx49n5syZxMfHo6urW6RRZBywBphEQTB7AgCRkZGk
pqbh4OCAp6cn9vb2eHj04MaNG2V9ypw9exa1Wk1iYuJjbXfp0iW8vb0ZMmQIycnJxMbG0rt3b4QQ
zJ07l+HDh/PJJ5+QlJTExo0b75vhmpubi7u7O8bGxuzdu5e9e/diZGSEh4cHubm5yridO3dy6tQp
du3axbJlywgLCyMsLExZ7+Pjwy+//MIPP/xAcnIy8+bNo3LlygDcvHkTV1dXWrRowaFDh4iOjubK
lSv069fv8S9YOfKkAcEHvbaPavr06Tg5OXHkyBHGjRvHyJEj2b59eykjfYBECr6Z8D5QG4Bjx47h
4eFB9erViY+PZ+3atWzbto0RI0Zobb19+3Y0Gg3btm1j8+bNbNiwgdq1a/Ptt99y6dIlLl68WObX
R3q2ZHa7JEmSJEmSJD0HQohy9QM0B0R8fLyQJEl6nXXu3FkEBASI9evXi6pVq4rMzMwHjruf//73
v0KtVos7d+4IIYTYtWuXUKvVYufOncqYyMhIoVarRdeuHkJHp5oAOwEDBSwXOjrVhLu7pzA2ripA
R8AKAecErFDWCSGEtbW1mDVrVpmc+5kzZ4RarRYJCQmPtd2hQ4eEWq0W586dK7HOwsJCTJgw4b7b
qlQqERERIYQQYvny5aJBgwZa6//55x9hYGAgfv/9dyGEEAMHDhQ2NjYiPz9fGdO3b1/xwQcfCCGE
OHnypFCpVGLHjh2lHi8oKEh4eHhoLTt//rxQqVQiJSXlEc62fNNoNCIyMlJoNJpHGv+g17a034F3
3nlHDBo0SHlubW0tPD09tca8//77okePHspzlUolgHvvcXHvp40ANwGIb7/9VlSvXl3cvXtX2SYy
MlLo6OiIK1euCCEK3hfm5uYiJydH61iP+/vxuNenuDNnzgiVSvXYv0OSJEmSJEmSJEmPIz4+/t6/
o2gunjIuLDOyJUmSyrlu3bpRp04dbGxs8PX1ZdWqVUqpjNLEx8fTs2dPrKysqFKlCp07dwbg3Llz
WuMaN26sPDY3Nwdgxozv72WDpgBhFGaDfvvtRG7ezKAgM7Vk/exHLTOSn5//yBm0jzquqKZNm+Lq
6kqjRo3o27cvCxcuJCMjg6tXr3LhwgW6dOnySPtJTEwkJSUFIyMj5ad69er8888/RRryQcOGDVGp
VMpzc3Nzrly5AkBCQgK6urr3zZ5PSEhgx44dWsdo0KABKpVK6xivqsctd3G/1/ZxtG3btsTzEydO
aC1r3LhpsdIeVYFduLt7cuPGDZo2bUqlSpWU8e3btyc/P5+TJ08W2UdjdHWfrt92WZQDKfrelKSy
VFo5H0mSJEmSJEl6WjKQLUmSVM4ZGhpy+PBhVq9eTa1atQgMDKRp06bcunWrxNisrCw8PDyoWrUq
q1at4uDBg2zYsAGAf/75h2nTptG/f3/y8/NxcnIiODgYgNTUVPLz82nZsiUHD/6Jnp4eI0eOVL4+
//XXX987wj9ALcAUGA50AODdd98ttQZwWFgYJiYmbNq0iYYNG1KpUiXOnz+PEILJkydjaWlJpUqV
cHJyIjo6+qmvlVqtJiYmhqioKBo2bMicOXOoX78+ly9ffqz9ZGZm0rJlSxITE0lISFB+NBoN3t7e
yrjizSFVKhX5+fkA6OvrP/QYPXv2LHGMlJSUB5aOeV3d77U9c+YMarW6xI2PR22yWDzY+9lnw4qV
9oiiWjVjwsNXIIS4b3C46PLn2aT1Qef5JDeDJOlRbNiwgW+//bZM9zlo0CB69+5dpvuUJEmSJEmS
yhcZyJYkSXoFqNVqunTpwtSpU0lISODMmTPs2LGjxLjk5GTS09MJDg6mffv22NvbK0Hc0NBQpk2b
hp+fH2q1mkWLFvHGG29w9+5dPvvsMwC2bNnC2rVrUalUxMTEKNmgVapUuXeEO8AuYBkFGdtBACxa
tKjUGsAqlYqsrCymTZvGokWLOHbsGDVq1CA0NJSZM2cyY8YMjh49iru7Oz179iyzTOS2bdsSGBjI
4cOHqVChAr///js2Njb3qYdcUvPmzUlJScHMzAxbW1utHyMjo0faR+PGjcnPzyc2Nva+xzh27BhW
VlYljvGwIPjrrPhr+9tvv2FmZqZVdzo/P5+kpKQS2+7fv7/E8/r162stO3r0qFYtZCcnJz744H1M
TExwdHTkyJEjWt+I2LNnDzo6Otjb25c6382bN2NiYoKenh55eXkkJCSgVqv55ptvlDFDhgzBz88P
gHXr1ikNSW1sbJgxY4bW/gqbVvr5+VG1alU+/vhjAA4cOEDz5s3R19fH2dmZw4cPawXXMzIy6N+/
PzVq1MDAwAAHBweWLl36wGstSfdTtWrV53rDRpIkSZIkSXo9yEC2JElSObdlyxbmzJlDQkIC586d
Y+nSpQghSgTgAOrUqYOenh6zZ8/m9OnTbNy4kaCggmDzqlWr+P777+nWrRtCCFq3bs3gwYNZsWIF
//zzDyqVCjs7Ozp37kxAQAAnTpxgzpw5pKSkFAkwZwEHgMZAI1Sq5bi7e9KyZUt0dHSoXLkyNWrU
oEaNGsqccnNzmTt3Lm3atMHOzo5KlSoREhLCuHHjeO+997Czs2Pq1Kk0a9aM0NDQp7pWBw4cIDg4
mPj4eM6fP8+6deu4du0ajo6OBAYGMn36dObMmUNqaiqHDh3ihx9+KHU//fv3x9TUlF69erFnzx7O
nDnDrl27GDlyJBcuXHikuVhZWeHr68vgwYOJiIjgzJkzxMbG8uuvvwLw2WefkZ6ezvvvv8/Bgwc5
deoU0dHRDJp9+CsAACAASURBVB48WGbSluJ+r22DBg3o0qULW7ZsITIykpMnTzJs2LBSy47s3buX
6dOnk5KSwo8//sjatWv5/PPPtcb8+uuvLFmyBCgIdB89epThw4cDBe+LSpUq4efnx7Fjx9i5cyf+
/v74+vpiZmZW6rzffPNNMjMzqVatGnFxcWzcuBFTU1N27dqljImLi6Nz584cOnSIfv364e3tTVJS
EpMmTeI///kPy5Yt09pnSEgIzZo14/Dhw/znP/8hKyuLt99+m0aNGnHo0CEmTpzI6NGjtbYZP348
ycnJREdHk5yczNy5czE1NX3s10EqH6Kjo+nYsSMmJiaYmpry9ttvc+rUKeDfZrobNmygS5cuGBoa
0qxZsxI3evbu3YuLiwuGhoZUq1aN7t27c/PmTaBkaZHs7GxGjx5N7dq1qVy5Mm3bttW6ibd06VJM
TEyIiYnB0dERIyMjunfvrtxonTRpEkuXLiUiIkL5Vk9cXNyzvkySJEmSJEnSS+bpCjRKkiRJL0xh
NqWJiQnr169n0qRJ/P3339jZ2bF69WolkF0069LU1JSwsDC+/vpr5syZQ/PmzQkJCaFnz57k5OTQ
pUsXzpw5o7VNcnIy9vb2xMfHK8u++uorpk6dSmBgIOPHj6dGjRrY2Nhw7dp1bt/2UcaZmFQnPHzF
A89DT0+PRo0aKc9v377NhQsXaNeunda49u3bk5iY+ARX6l9VqlQhLi6OWbNmcevWLaysrJgxYwbu
7u5AQXmVmTNnMmbMGExNTXn33XeVbYteE319feLi4hg7dix9+vTh9u3bWFhY4OrqWiQ7/eHmzZvH
119/zWeffcb169epU6eOUqbF3NycvXv3MnbsWNzd3fnnn3+wsrLCw8ND1jYuxYNe29zcXBITE/Hz
80NXV5eAgIBS66GPGjWKgwcPMnHiRIyNjZk5cyZubm5aYyZNmsTq1av57LPPMDc31/pd09fXJzo6
mpEjR+Ls7IyBgQHvvvsuISEhD5x3kyZNaN26NbGxsWzcuBEhBLdv3yYrK4uMjAzS0tLo1KkTEyZM
wM3NTXmP1KtXj2PHjvH999/j6+ur7NPV1ZWAgADl+fz58xFCsHDhQvT09GjQoAHnz5/n008/Vcac
P38eJycnnJycgIKbXtKr686dO4waNYomTZqQmZnJhAkT8PLyIiEhQRkzfvx4QkJCqFevHl9//TXe
3t6kpqaiVqs5cuQIbm5uDBkyhNmzZ6Orq8vOnTvJy8sr9XifffYZycnJrFmzBnNzczZs2ED37t05
evQodevWBQpKX4WEhLBy5UpUKhX9+/dn9OjRLF++nNGjR3PixAlu375NWFgYQgiqVav2XK6VJEmS
JEmS9BJ52m6Rz/sHaA6I+Pj4J2+XKUmSVIpdu3YJtVotbt68+cBx1tbWYtasWc9pVs/H0aNHhVqt
FmfOnCmxLiAgQLi6umotu3nzplCpVGLPnj1CCCEGDhwovLy8hBBCaDQaERkZKQYOHChcXFyUbUq7
bmFhYcLExERr2a1bt4RKpRK7d+/WWv75558LNzc3IYQQZ86cESqVSiQkJDzhGUuStkf5vVapVCIi
IqLMj/3FF1+Inj17CiGEMDU1FRqNRjRr1kzExMSIVatWidq1awshhGjevLmYPHmy1rYRERGiYsWK
Ij8/XzmPKVOmaI0p7Xc4ISFBqNVq5Xdo69atwsDAQDRr1kx8+eWXYt++fWV+ntLL68qVK0KlUolj
x44pn69LlixR1h8/flyo1Wpx8uRJIYQQ3t7eomPHjvfdX+fOnUVAQIAQQoizZ88KXV1dcfHiRa0x
bm5u4ptvvhFCFPwtUKvV4vTp08r6n376SZibmyvPi/6dkSRJkiRJksqP+Ph4AQiguXjKuLAsLSJJ
knRP+/btuXjxopJRW/hV59dBYUmP0mpEP27dXzs7O7p3707VqlW1lhfWAH4YIyMjatWqxZ49e7SW
79u3jwYNGijPX/WsZI1Gw9atW0lJSXnRU5GekcLX2M7Ojt27d5OQkICenh52dnZ06tSJnTt3Ehsb
S+fOnQFKbSYpSikzU7w2cWnbFefh4cG5c+cICAjg4sWLuLq68uWXXz7dCUovrdTUVLy9valbty7G
xsbY2tqiUqk4d+6cMqZx48bKY3Nzc4QQXLlyBYAjR47g6ur6SMdKSkoiLy8Pe3t7jIyMlJ+4uDit
vgcGBgZYW1trHbPweJIkSZIkSZIEska2JEmSQldXV6t286MEf8pKTk7OcznO/VSsWJGxY8fy5Zdf
snz5ck6dOsWff/7J4sWL6d+/PxUrVixR97dXr14cPHjwkQOt1tbWxMXFceHCBa5fv/7AsWPGjOG7
775jzZo1aDQaxo0bR0JCAiNHjlTGlBbAKyvZ2dn4+/vzxhtvoK+vT8eOHTl48CAAsbGxqNVqIiMj
adq0Kfr6+rRt25Zjx45p7WPPnj28+eabGBgYYGVlxciRI8nKylLW29jYEBwczIcffkiVKlWwsrJi
wYIFpKen4+HRAwcHBzw9PbG3t8fDowc3btx4ZucrPdqNkbL6PCj+GhfW7P7uu++UoHXnzp3ZtWsX
sbGxdOrUCSi4qVT8Bs/evXuxt7d/4NwcHR1JSEggOztbWfbHH3+UGFe9enV8fX1ZtmwZoaGhzJ8/
vwzOVnoZvfXWW9y4cYOFCxdy4MAB/vzzT4QQWu+RChUqKI8L31/5+fkAj9VwNjMzE11dXQ4dOkRC
QoLyc+LECWbNmlXq8QqP+Sw/5yVJkiRJkqTyRwayJUl6rQghCA4OxtbWFgMDA5ycnFi3bh3wb4Dy
1q1bxMbGMnjwYG7evKk0lpo8ebKynzt37pQIQBb1119/0a9fP6WR1jvvvMPZs2eV9YMGDcLLy4sp
U6ZgYWFRamPG523ChAmMGjWKwMBAHB0def/997l69Sr6+vrExMSQnp6Os7Mz7733HtnZOaxbt04J
tMbE/P7QYPzkyZM5c+YMdevW1bphUBp/f39GjRrF6NGjadKkCTExMWzatEmppfqsjRkzhg0bNrB8
+XIOHz5MvXr18PDw0GoQ+OWXXzJz5kwOHjyImZkZPXv2VDLO09LS6N69O++99x5JSUn88ssv7N27
lxEjRmgdZ8aMGbRq1YojR47w6aefMmzYMHr18mLbtv3ACuAcsIJt2/bzwQcDnsu5v65OnTqFv7//
A8fk5eXRs2fPpz6Wt7dPiddYCDWrV69WAtmdOnUiPj4ejUajLBs1ahTbt28nKCiIlJQUli5dyo8/
/siYMWMecjxvVCoVQ4YM4cSJE0RGRpao2x0YGMjGjRtJS0vj2LFjbN68GUdHx6c+V+nlk56ejkaj
Yfz48bi4uODg4EB6evpj7aNJkyalfoOnNE5OTuTl5XH58mVsbW21fh72t6CoR/1WjyRJkiRJkvQK
e9raJM/7B1kjW5JeW0Vrbj6poKAg4ejoKH7//Xdx+vRpsXTpUqGvry/i4uLErl27hEqlEm+99ZbI
zs4Ws2bNElWrVhVXrlwRly9fFnfu3BFCFNSgNTU1FXPnzhVpaWli6tSpQkdHR6kdmpOTIxwdHcXQ
oUPFsWPHRHJyshgwYICoX7++yMnJEUIU1Po0MjISfn5+4vjx4+L48eNPd3GeI3d3T6GjU03ACgHn
BKwQOjrVhLu751PtNyoqSnTo0EFUrVpVVK9eXbz11lsiLS1NCPFvTexffvlFdOrUSejr64ulS5cK
IYTYvXu36Nixo9DX1xd16tQR/v7+ymslhBArVqwQLVu2FEZGRqJmzZrC29tbXLlyRVl/48YN4e3t
LczMzIS+vr6ws7MTOjo6YvXq1cqYnJwcYWFhIaZPn668T3799VdlfXp6ujAwMFCWDRkyRHzyySda
57d7926ho6Mj/vnnHyFEwfvIz89Pa4ypqem92mErBIgiP8sFIDQazVNdY+nFO3ny5H1eY3cBiJiY
GGVss2bNhIWFhdb269evF40aNRIVK1YU1tbWYsaMGVrrbWxsSq31/eeffwonJydRqVIl0bx5c7Fh
wwatGtlBQUGiYcOGwtDQUJiamgovL69Sa+ZL5V9+fr4wNTUVvr6+IjU1VWzfvl04OzsLtVotIiIi
Su1BkJGRIVQqlYiNjRVCFPRCqFSpkvj0009FYmKiOHHihJg7d664fv26EKLk3+sBAwYIW1tbsX79
enH69Gnx559/iuDgYBEZGSmEKL1fwm+//SbUarXyfMqUKcLa2lqcPHlSXLt2Tfl7KkmSJEmSJL3c
ZI1sSZKkJ5CdnU1wcDCLFy/Gzc0Na2trfH196d+/Pz///LPW2AoVKmBsbIxKpcLMzIwaNWpgYGCg
rO/RoweffPIJtra2jB07FlNTU3bt2gXA6tWrEUIwf/58HB0dcXBwYNGiRZw7d04ZA1C5cmUWLlxI
gwYNtGo/v8w0Gg3R0ZHk5c0G+gOWQH/y8mYRHR35VPWc79y5w6hRo4iPj2fHjh3o6Ojg5eWFRqNh
586dAHz11Vd8/vnnnDhxAnd3d06dOvXQzOecnByCgoJITEwkIiKCs2fPMnDgQGX9+PHjSU5OJjo6
muTkZL788kvy8/Np166dMkZXVxdnZ2dOnDgBFHzlvU2bNsp6ExMTHBwclPUJCQmEhYVp1YP18PAA
4PTp08p2RWvQAkp9dniz2NUpKC2Rmpr6+BdWeqn8WxO4+Gtc8K2O3NxcZcnhw4f566+/tEZ5eXlx
9OhR/v77b06fPk1AQIDW+vtlljs7O3Po0CHu3r1LfHw877zzDnl5eTRp0gSAb775hqSkJDIzM7l6
9Srr16/Hysrq6U5WeimpVCp++eUX4uPjady4MaNGjWL69OnKuqL/Lb5dITs7O2JiYkhMTKR169a0
b9+ejRs3oqurW+r2YWFh+Pr6Mnr0aOrXr4+XlxcHDx6kTp06jzzvoUOH4uDgQMuWLalRowb79u17
7HOXJEmSJEmSyjfdFz0BSZKk5yU1NZWsrCy6du2qVXczJycHJyenx9pX8QBkzZo1laZUiYmJpKSk
YGRkpDXmn3/+IS0tDTc3N2Ufhf/oLy/uH4T7N9BqZ2f3RPvu3bu31vNp06bh4OCAg4ODskxPrxKd
OnVSmnAOHTqUAQMGKIFrW1tbQkND6dy5M3PnzkVPT08raG1tbU1oaCitW7cmKysLAwMDzp8/j5OT
k/IecHZ2RqVSldpU72E1kgvXZ2Zm8vHHHzNy5MgSNV6LBm6K14StWLHivUdxFNwoKBQLQL169R54
fOnl9295nJfrNdZoNKSlpVGvXr0n/h2Wyo8uXbqQlJSktaxo2Y7iJTyMjY1LLOvYsSO7d+8udf87
duzQeq6jo0NgYCCBgYGljvfz88PPz09rWa9evbSOaWpqSlRU1H3OSJIkSZIkSXodyIxsSZLKpYyM
DHx9falWrRqGhoZ4enpqZasuXboUExMTYmJicHR0xMjIiA8//BCAyMhIEhISOHz4MO+99x56enqc
PHmSefPmlXqs4k3/srOzlQBkYV3tO3fuMHfuXAwNDVm2bBmNGjUiMTFRq7GVRqPB29tb2a+hoeEz
vELPhnYQrqinD8Klpqbi7e1N3bp1MTY2LlKfdwywD1Ch0ZzXqhX9KJnP8fHx9OzZEysrK6pUqaLU
Gz537hwAw4YNIzw8HCcnJ8aOHcv169epUKGCVlO93NxcDh48qGTOCyHYv3+/sv7GjRtoNBplffPm
zTl27Bg2NjYlasI+6OZFxYoVqVvXDh0dfwrqJ58HVqCjMxJ3d08ZYHwF2Nvb4+7u+dK8xrK5qPQy
02g0bN269am+7SNJkiRJkiS9OmQgW5KkcsnPz49Dhw6xefNm9u/fjxACT09PreytrKwsQkJCWLly
Jbt37yYjIwO1Ws3Zs2extbVl/fr1bNy4keXLl/PHH39w+/ZtrexZPT097ty5U6Lp36VLl7h7967W
fC5cuICHhwfx8fFUqVKFpKQkzMzMSgQxi2dplzfPMgj31ltvcePGDRYuXMgvv/xy77VUAR2AWgDk
54/TKmFSmPlc9KZBYmIiGo2GunXrkpWVhYeHB1WrVmXVqlUcPHiQDRs2AAWlZgA8PDw4d+4cAQEB
XLx4kR49etCoUSPGjBlDdHQ0x48fZ8iQIdy9e1e5GQIFzSt37NhBUlISAwcOxMzMjF69egEwduxY
/vjjD0aMGEFCQgKpqalERESUaPZYmvfe64ObWxvAB6gD+ODm1obw8BVPfG2ll0t4+IqX5jUurfGk
bC4qvWjyBoskSZIkSZJUGhnIliSp3ElNTWXTpk0sWrSIdu3a0bhxY1auXMn//vc/fvvtN2Vcbm4u
P//8M05OTjRr1gx/f3/09fUJCAhg2bJlhISE4Ovry/nz5zlw4ABffPGF1nFq1qxJdnY2AwcOpEWL
FlhZWbFgwQJUKhV//PGHMk6lUlGrVi2srKyoX78+06ZNIzc3l7fffps9e/Zw5swZdu3axciRI7lw
4cJzu07PyrMIwqWnp6PRaBg/fjwuLi4lynH8qyXwb63oh2U+Jycnk56eTnBwMO3bt8fe3p7Lly+X
2Gv16tXx9fVl2bJlhIaGkpqaSp8+ffD19aVly5acOnWKmJgYjI2NgYLXfOrUqYwcOZJWrVpx9epV
Nm3apGRbN27cmNjYWFJSUnjzzTdp3rw5EydOxMLCQjnm/WrQ6uvrExW1BY1GQ2RkJBqNhqioLUo5
Fan8MzExeSle42dZ816SirKxsWH27Nlay5ycnJg8eTIAarWaefPm4enpiYGBAbVrW/L773EUvcHy
++97qFfPDgMDA0xNTfn444+5c+eOsr9Bgwbh5eVFSEgItWrVwtTUlOHDh5coiSJJkiRJkiSVX+Wr
OKskSRJw4sQJKlSogLOzs7KsWrVqWs32AAwMDLC2tlaem5ubc/fuXYKDg5kyZQpXrlxh6dKltG7d
mq+//rrEP3ZNTU0B+Omnn5gyZQqBgYFMmDCBihUrlgiG6uvrK4+tra2VJpF9+vTh9u3bWFhY4Orq
WqSZX/lVGIRLSUkhNTW1TGrqmpiYUL16debPn69Vb7ykg8C/JUzGjh1L27ZtGTFiBEOGDMHQ0JBj
x46xbds25syZQ506ddDT02P27Nl88sknHD16lKCgIK09BgYG0qJFCxo2bMjff//N5s2bcXR0JDQ0
lNDQ0PvOuUOHDhw9evS+61u0aPHAeq6nTp0qsezQoUPKYzs7O1lK5BX3ol/jZ1nzXpIe14QJE/ju
u+8ICAigW7dugA4FNy8tgd7k548gPf06kZGR6Ovr8+GHHzJixAgWL16s7GPnzp3UqlWLXbt2kZqa
St++fXFyctL6No0kSZIkSZJUfsmMbEmSyp37ZesWb8ZXvJGeSqVCCMHw4cM5cOAAKpWKjRs3EhkZ
SYcOHejUqRNeXl7KdkII1Go1CQkJ5OXlMWHCBAC6detGo0aNtPa9Z88eZX1ho8Dp06dz+fJlsrKy
SElJYd68eVSuXBmAJUuWsH79+rK5IC+InZ0d3bt3L5NAl0ql4pdffiE+Pp7GjRsTGhqKs3MbQAC7
gIJMdrX6O60SJg/LfDY1NSUsLIy1a9fSsGFDpk2bRkhIiNax9fT0+Prrr2natCmdO3dGV1eX8PDw
B873/hnjr6/SMi6ll9uzrHkvSY+rb9++DBo0iNzc3HtLmgJz7j3W/sZP586d+eGHH1i2bBlXr15V
llerVo0ffvgBe3t7PD096dGjB9u3b38u83+QSZMm0bx588faRq1Ws3Hjxmc0I0mSJEmSpPJJBrIl
SSp3HB0dycnJ4c8//1SWXb9+HY1GU6RB4INVqVIFc3NzrYZ9eXl5xMfHK8/r1at336Z/j3qcomTT
qgfr0qULSUlJZGVlcfjwYaKiInF39wRmAu0AQdeuHUqUMCnMfL558ya3bt3i8OHDjBs3Tlnfr18/
0tLSyMrKYs+ePfTo0YO8vDyaNGkCwDfffENSUhKZmZlcvXqV9evXY2Vl9cC5llYW5HGV1/dDYSNV
qfx72RpPSq+3Nm3aAEVvsNQACr9llQyYA//eYGnfvj35+fmcPHlS2UfDhg21Pp/Nzc0f8A2f52fM
mDEvRUBdkiRJkiSpvJOlRSRJKnfq1atHr169GDp0qJLlPG7cOCwtLenZs+cj72fkyJFMnTqVevXq
Ub9+fWbMmEFGRoay3sDAgGHDhjFmzBhMTEywtLRk2rRp3L17l8GDByvjSsvOLbosPT0db28foqMj
lWXu7p6Eh6+QAcEHeBYlTMpCp06dnqrmanl/PxT/5oNUvoWHr+CDDwYQHe2jLHNz85TNRaUypVar
S/ytzMnJKXVs4Q2WmJjtCFGPghssxwFNqTdYHvZNrPz8/LI4hadiYGCAgYHBi56GJEmSJElSuScz
siVJKjeK/mN1yZIltGjRgrfffpv27dujVqvZsmULOjo6j7y/UaNG4ePjw8CBA2nXrh1VqlShd+/e
WmOmTp36wKZ/xedV2jJvbx+2bdtP0aZV27bt54MPBjzyXF9nZVnCpKgXlRH9PN4Pa9eupUmTJkpT
tG7dunH37l2EEEyePBlDQ0N0dHRwcnIiOjpa2S42Nha1Ws2tW7eUZQkJCajVas6dO0dsbCyDBw/m
5s2bqNVqdHR0lGZtAHfu3OHDDz+kSpUqSnNU6eX2sMaTLi4uJRrhStLjMjMz4+LFi8rzW7ducfr0
aa0xRb8hFR6+AmNjfeAYBU2Fo6hQQcXixf9+puzZswcdHR3s7e3LbJ4P++y0tLSkUqVKJT47Af73
v//xwQcfUL16dSpXroyzszP//e9/gYLSIk5OTsrYgwcP0q1bN8zMzKhatSqdO3fm8OHDZXYekiRJ
kiRJryqZkS1JUrmxY8cO5XHVqlUJCwu771g/Pz/8/Py0lvXq1Usrk1ZHR4cZM2YwY8aM++6nYsWK
D2z6V1p2btOmTZVlGo3mXubtCqD/vRH9ycsTREf7kJKS8lJkGb9OXmRG9KO8H+rWravUWS8qJyen
RLZhaS5duoS3tzfTp0/nnXfe4fbt2+zevRshBKGhocycORNnZ2cqVKhA8+bN6dmzJ8ePH1e+zv+g
GzPt2rUjNDSUwMBANBoNQgil7jvAjBkz+Pbbb/nmm2/49ddfGTZsGJ06dSrTQJP0bJRF48nY2Fhc
XFzIyMh4JRrbSmWnS5cuLF26lLfeegtjY2MCAwPR1dX+Z8ivv/5KixYt6NChAytWrCAzM5OtW7ci
hKB27dp0796dzz//nMDAQK5cuYK/vz++vr6YmZmVyRwf5bNz/vz5NGvWjEWLFml9dt65c4c333wT
S0tLNm/ezBtvvMGhQ4e0ssGLfrbevn2bgQMH8sMPPyCEICQkBE9PT1JTUzE0NCyT85EkSZIkSXoV
yYxsSZKkZygtLe3eozeLrekEQGpq6nOdj/RsMqKFEEybNg07OzsqVaqEtbU1wcHBJTKc/30/+Nw7
NsBS4DMA3NzcqFSpEufPn2fQoEF4eXkxZcoULCwsqF+/PgDZ2dmMHj2a2rVrU7lyZdq2bUtsbKwy
l/nz55OTk0P16tXx8PCgTZs2REREcPv2bUJCQmjZsiWxsbFs376dadOmkZ2dzZgxYx7pPCtUqICx
sTEqlQozMzNq1Kih9XX5Hj168Mknn2Bra8vYsWMxNTVl165dT3xdpfKlsOyMbIYqFffVV1/x5ptv
8vbbb/P222/j5eWl3LQrNGnSJFavXk3Tpk1ZsWIFq1evxsPDg+7du9O4cWOio6NJT0/H2dmZvn37
0rVrV+bMmfOAoz6eixcvkpeXh5eXF3Xq1KFhw4Z88sknGBgYEBISwrhx43jvvfews7Nj6tSpNGvW
TLnJvXLlSq5fv05ERARt27bF1taWd999l9atW5d6LBcXF7y9vbG3t8fBwYF58+aRlZWl9VkuSZIk
SZIklSQzsiVJkp6SRqMhLS2t1BrO/zatiuPfDFyAgn+sFjatkp6PZ5UhP27cOBYtWkRoaCjt27fn
4sWLJCcnA9pZeP++H4rLAmD69Ok0a9ZMyTDcvn07xsbGbNu2TRn52WefkZyczJo1azA3N2fDhg10
796do0ePUrduXSwtLVGpVPj5+eHi4sK7777Lr7/+ysiRI7lw4QKLFy+mevXq3L59m7CwMP7zn/+g
0Wge+5xL07hxY63nNWvWfCkarUllY+XKlYSGhnLy5EkMDQ3p0qULoaGhmJmZcfbsWbp06YJKpcLE
xER5Dy5evBghBFOnTmXBggVcunQJBwcHxo8fT58+fV70KUnPiZGREeHh4VrLfHx8tJ7XqlWrRLmO
oho2bKj1WVjckiVLSiybOXPmI8+xadOmuLq60qhRI9zd3enWrRvvvvsuOjo6XLhwgXbt2mmNb9++
PYmJiUBBCSYnJyetsmMPcuXKFb755htiY2O5cuUKeXl53L17l3Pnzj18Y0mSJEmSpNeYzMiWJEl6
Qunp6Xh49MDBwQFPT0/s7e3x8OjBjRs3lDGFTat0dPwpCJ6eB1agozOy1KZV0rP1LDLkMzMzmT17
Nt9//z0DBgzAxsaGdu3aaTUELWRvb0/bth0AAayn4P2wD8ilXbuOSrafvr4+AJUrV2bhwoU0aNCA
Bg0acP78ecLCwvj1119p164dNjY2fPHFF7Rv314J4qjValQqFWvWrKFDhw5ERETwv//9TynNY2Bg
gL6+PhUrVsTMzAx9fX2ltrxaXfC/BUUzau/XkK00L2ujNals5OTkEBQURGJiIhEREZw9e5ZBgwYB
YGlpybp16wBISUnh4sWLzJo1C4ApU6awYsUK5s+fz/HjxwkICMDHx4fdu3e/sHORXk1P0/tArVYT
ExNDVFQUDRs2ZM6cOdSvX1+p5V287FLRxreFn9mPytfXl8TERObMmcMff/xBQkIC1apVIzs7+7Hn
LUmSJEmS9DqRgWxJkqQn9KglKsLDV+Dm1oaCchJ1AB/c3NoQHr7iuc/5daedIV/Uk2fInzhxguzs
bLp0sojMbAAAIABJREFU6fJI47/7bsq9RwEUvB/mo1ar2bw5osTYxo0ba9WRPXr0KHl5edjb22Nk
ZKT8xMXFFQnSFwSre/fuTWBgIIcPH0ZPT4/r169jYWHBnj17tI6xb98+GjRoABQ0ZBNCaDVlK96A
TE9Pr0RdeOn1MHDgQNzd3bG2tsbZ2ZnQ0FC2bt1KVlYWarWaatWqAShlZ4yMjMjOziY4OJjFixfj
5uaGtbU1vr6+9O/fn59//vkFn5H0siitNv/jeJQby4+qbdu2ymdnhQoV2L59+0M/O5s0acKRI0fI
yMh4pGPs27cPf39/3N3dadCgARUqVODatWuPPVdJkiRJkqTXjSwtIkmS9AQep0SFiYkJUVFbSElJ
ITU1tdQSJNLzUZghv22bP3l5goJM7Fh0dEbi5vZkGfIPysQrLcNZX18ftVrNjh07yMrKIjExke++
+67URpPFm35lZmaiq6vLoUOHlH0XKmy6eOrUKfLy8oiPj6dGjRrs379fqdE9evRoJk6cSNOmTdHT
02PcuHEkJCSwatUqoCCQb2lpycSJEwkKCuLkyZMlmqFaW1uTmZnJjh07aNq0qZLhLb364uPjmTRp
EgkJCdy4cUPJtj937pxSw7241NRUsrKy6Nq1a4lMfycnp+cy7/LMxcUFJycn5ffQxsaGgIAA/P39
X/DMytaT3BwbNGgQN2/eZP369cVuLL8JxLFtmz8ffDCAqKgtj7S/AwcOsH37drp166Z8dl67do2t
W7diYmLCd999h62tLc2aNWPx4sVan52LFi1CpVLxzjvvMGXKFMzNzTl8+DAWFhal1sm2s7Nj+fLl
tGjRgps3b/Lll19q9RuQJEmSJEmSSicD2ZIkSU/gUUpUFA+K2tnZyQD2SyA8fAUffDCA6Oh/67O6
uXk+cYZ8YYPH7du3lygnUjTDubB2amGGs42NDXXq1HmsGtJOTk7k5eVx+fJl2rdvX+oYfX19cnNz
6dGjB7du3cLKyorBgwezYMEC/P39uX37NlOnTuXu3btcu3aNTZs2KZnqurq6rF69mmHDhtG0aVNa
tWrF//3f//Hee+8p+2/bti2ffPIJ/fr1Iz09ncDAQCZMmFBqRuXTZlm+CB999BHr1q0jIyODw4cP
06RJkxc9pZdCVlaW0nhv1apVSl1sDw+PB5ZDyMzMBCAyMpJatWppratYseIznXN5Ehsbi4uLCxkZ
GVSpUkVZvmHDhhIleyRtZdX7oEqVKsTFxTFr1izls3PGjBkcOHAAQ0ND+vbty+jRo7ly5QqOjo5a
n51qtZo+ffpw8+ZNevToQW5uLo6Ojvz444+lHmvx4sV89NFHNG/enDp16jBlyhRGjx6tNaY8fn5K
kiRJkiQ9azKQLUmS9ARkE8fyq6wz5CtWrMjYsWP58ssvqVChAu3bt+fq1ascO3YMX1/fh2Y4Pw47
Ozu8vb3x9fVl+vTpODk5ceXKFSU7unv37pibm1O5cmUuXbqkbBcREcGCBQtQqVSMHz8eHR0d5s+f
z+rVq6levTq5ublKCZO2bdty5MgRreMWz5b88ccfSwRoTp06VWK+hw4deuJzfRGioqJYtmwZsbGx
2NjYYGpq+qKn9NJITk7m+vXrBAcHY2FhARRksBalp6cHaL9fHB0dqVixImfPnqVDhw7Pb8LlTGG9
5aJZ6wBVq1Z9QTMqP57kxnJp6tevz9atW0ssP3DggPLZOX78+Ptub2RkxIIFC0pdFxgYSGBgoPK8
adOm/Pnnn1pjevfurfVclnCSJEmSJEkqSdbIliRJegKyiWP5Z2dnR/fu3cvktZowYQKjRo0iMDAQ
R0dH3n//fa5evYquri7h4eEkJyfTtGlTvv/+e/7v//7vqY4VFhaGr68vo0ePpn79+nh5eXHw4EHq
1KnzyPsYOnQoDg4OtGzZkho1arBv376nmtOrIjU1FXNzc1q3bk2NGjVKlG95FK9q8KlOnTro6ekx
e/ZsTp8+zcaNGwkKCtIaY2VlhUqlYtOmTVy7do07d+5QuXJlRo8eTUBAAMuWLePUqVMcPnyYH374
geXLl7+gsyl7NjY2zJ49W2uZk5MTkydPBgoydhctWkTv3r0xNDTE3t6eTZs2AXD27Fmlxr6JiQk6
OjrKtztcXFz44osvnuOZvHzWrl1LkyZNMDAwwNTUlG7dunH37l1lfWxs7L1HjsBwoPB3sGD5zz//
TLVq1TA0NMTT01Orqe+kSZNKlLiZNWsWNjY2951PVlYWvr6+GBkZYWFh8VQ3Jws9TZNKSZIkSZKk
14kMZEuSJD0h2cTx1VdakON+vvrqK06dOsXff//N6dOnGTt2LADt2rXjyJEj3Llzh127dtG7d2/y
8vKUwLOfnx/p6ekl9rdkyRLWr19fYrmOjg6BgYGkpaXx999/87///Y+1a9fSsGHD++6vV69eWgFW
U1NToqKiuHXrFnl5ebz5ZvFMxsdXGIhZuXIlarVaqctdXgwaNAh/f3/OnTuHWq3G1taW7Oxs/P39
eeONN9DX16djx44cPHhQ2SY2Nha1Wk1UVBQtW7akUqVK7N27V3nfLFmyBCsrK4yMjBg+fDj5+flM
mzYNc3Nz3njjDaZMmaI1h4kTJ2JlZUWlSpWoXbs2n3/++fO+DCUUljcwNTVl6dKlyntt2rRphISE
aI2tVasWkyZNYty4cdSsWZMRI0YA8O233zJhwgSmTp2Ko6Mj3bt3JzIy8oHBwlfR5MmTef/99zl6
9Cienp7079+fjIwMLC0tWbduHQApKSlcvHiRWbNmveDZvhwuXbqEt7c3Q4YMITk5mdjYWHr37q3U
Z9+xYwe3b9+mQ4c3KbjvtBCYQeGNZTOzGqSmprJ582b279+PEAJPT0+tz8PHLYs0evRodu/ezaZN
m4iJiWHXrl3Ex8c/0fmVZZNKSZIkSZKk14EsLSJJkvSEZBPH18PzqlO6du1aJk+eTGpqKgYGBjRv
3pyIiAj09fVZuHAhM2bM4PTp09jY2DBixAiGDRumbPvXX38REBDAtm3b0NHRoUOHDsyaNQsrKyug
IEj7119/YW1tzcaNG8nLy+P9999n1qxZ6OjoPNW809PT8fb2uVej9l83btzQqvX7sps9ezZ169Zl
wYIFHDx4ELVazZgxY9iwYQPLly+nTp06fPfdd7i7u5OWlqZV8uGrr75i+vTp2NraYmJiws6dO0lL
SyMqKoro6GjS0tLo06cPaWlpODg4EBcXx969exk8eDBdu3alVatWrF27ltDQUNasWYOjoyOXLl0i
ISHhBV6RAjt27FAe9+vXj379+mmtL56B/s033/DNN9+U2M/w4cMZPnz4s5lkOTFo0CD69u0LwJQp
U5gzZw4HDhygW7duVKtWDSioq1+efm+etYsXL5KXl4eXlxeWlpYAyk07gGrVqvHDDz+QkZFxr/dB
JPAlAG3bdmLv3jg2bdqoNFxcuXIllpaW/Pbbb/Tp0+ex53Pnzh0WL17MqlWr6Ny5MwBLly6ldu3a
T3R+ZdGkUpIkSZIk6XUiM7IlSZKeUlmWqJCen5ycnBc9BUVpWYdnzpwhICCAbt268dFHH/HXX38x
dOhQpkyZwoQJEzAzMyMoKAgfHx+srKxITExk7969rFu3jiNHjmBra0v16tXx9PRk69Yotm3bxsKF
C7ly5Qp3797lxx9/xMjIiI4dO3L+/HllLhEREbRo0QJ9fX3q1avH5MmTtYKVxUskWFpa8vvvcRQE
YvYBBYF/a2trrRIJLzsjIyOMjIzQ0dHBzMwMfX195s2bx/Tp0+nWrRv169dnwYIF6Ovrs2jRIq1t
v/32W1xdXbGxsVEC3EIIlixZQv369enRowcuLi5oNBpCQ0Oxs7Nj4MCBODg4sHPnTgDOnz+Pubk5
rq6u1K5dm5YtW/Lhhx8+9+sgPTuNGzdWHhsYGGBkZPRYzV5fR02bNsXV1ZVGjRrRt29fFi5cSEZG
hrK+YcOGqFQq5cayn58fzZo1Q6PR8OWXo6hQoQLOzs7K+GrVquHg4MCJEyeeaD5paWnk5ORo7dPE
xAQHB4fH3ldhk8q8vNkU9NqwpKBJ5SyioyNlmRFJkiRJkqRSyEC2JEmS9FpwcXFhxIgRBAQEYGZm
hoeHB+fPn6dXr14YGRlhbGxMv379HhpYWrhwIY6Ojujr6+Po6MjcuXOfem5Fsw7r1KlDw4YNsbCw
IDw8nP/+97/MmDGDn3/+mcWLF3P9+nU+//xzbt++TUhICPn5+dja2hIVFYW9vT2ffvoprq6uVKxY
kenTp3PkSAKXL18CzIBTgAF37+ZjZmZGly5d+Oijj5Ss8z179uDn50dAQADJycn8/PPPLF26tEQJ
jMISCRs3biQrK4v8/FygB9AaWEdhMHvv3r3ltkRCamoqubm5tGvXTlmmq6uLs7OzVhBMpVLRokWL
EttbW1tjYGCgPH/jjTdwdHTUGvPGG28o77f33nuPrKwsbGxs+Oijj/jtt99emXrbr0P9X7VaXaJR
Y/GbZRUqVNB6rlKplBIZD1O8zNGgQYNKNAd8FanVamJiYoiKiqJhw4bMmTOH+vXrc+bMGaDkNTUx
McHExAQ7O7sSr0ehwsaahft/2OtWfFsom2/qPEqTSkmSJEmSJEmbDGRLkvRaOXv2LGq1msTExBc9
FekFWLZsGRUrVmTfvn3MnTuXXr16kZGRwe7du9m2bRtpaWm8//77991+5cqVTJw4keDgYJKTk5Xs
6KdtWlda1mFOTg4WFhbcvHmT8ePH89FHH5GTk8NHH31EUFAQubm5uLq6YmFhwZkzZ2jSpAlGRkYk
JyezZs0asrOzOX/+PBcvXqDgz31doCrwN0KM5urVq6Snp+Pj46N8LX7SpEl89dVXDBgwACsrK1xd
XZk8eTLz5s3Tmm9hiYTs7Ox7S7KBA/eOU43CQPaNGzcwMjJ6qmvzohUPWBUNghUyNDQssV1pQcsH
BTJr166NRqPhp59+wsDAgM8++4xOnTqV62D261T/18zMjIsXLyrPb926xenTpx95ez09PeDBzUKf
V5mjl1Hbtm0JDAzk8OHDVKhQgd9+++2h2zg6OpKbm8uff/6pLLt+/ToajUa5qWRmZsalS5e0tjt8
+PB991mvXj10dXXZv3+/suzGjRtoNJrHPSXq1q1771FcsTWxyrEkSZIkSZIkbTKQLUnSa6VOnTpc
unSJRo0aveipSC9AvXr1mDp1KnZ2dpw9e5akpCTCw8Np1qwZrVq1Yvny5Q9s3DVx4kRCQkLo1asX
VlZWvPPOO3z++eclAr2Pq7SswwMHDijlahYuXEhCQgJz5sxBR0eHpKQkzM3NadGiBZmZmbRs2ZLE
xER8fHyU4GjFihUJDg6+dwQB/A2YAH7A90DBjZ2iQZyEhAQmT56slNkwMjJi6NChXL58mb///lsZ
V1gi4d9ATCWgaCa7UK53eVWvXj0qVKjAnj17lGW5ubkcPHiwRGZ1WalYsSJvvfUWoaGh7Ny5k337
9nH06NFncqyHKYvSO9r1f88BK9i2bT8ffDDgqff9sunSpQvLly9nz549HD16lIEDB6Kr++itaKys
rFCpVGzatIlr165x586dZzjb8uPAgQMEBwcTHx/P+fPnWbduHdeuXaNBgwYP3bZevXr07NmToUOH
snfvXhISEhgwYACWlpb07NkTgM6dO3P16lWmTZvGqVOn+PHHH4mKirrvPg0NDfnwww8ZM2YMO3fu
JCkpiUGDBj1RrwF7e3vc3T3R0fGn4HfkPIVNKt3dPWW5MkmSJEmSpFLIQLYkSa+M3Nzch45RqVTU
qFEDtVp+/L2OWrZsqTxOTk7G0tKSWrVqKcsaNGhA1apVS62fmpWVRVpaGh9++KFWoPf//u//Hivz
8kGKZh2q1WouX75M7dq1SUtLw9bWlpo1a6JSqbC1tUVXVxdDQ0OaN29OSkoKZmZm6Orq0qpVK5KS
kjh69CibN28uPHMK6q8CLAb+AxRkjdrb23PgwAEAMjMzmTRpEgkJCcpPUlISGo2GSpUqKfMszCwu
DMTAXWAPBYGYGEDg6tq1XAdiDAwMGDZsGGPGjCE6Oprjx48zZMgQ7t69q1X3+37lCx6Hi4sL3bp1
o3v37hgbG2NmZsbQoUMxMDDAysqKmzdvMmTIEGrUqIGxsTGurq7Kt0o0Gg1qtbpERuiMGTO0biQk
JSXh6emJkZERNWvWxNfXl+vXr2vNoXjpnafxqtf/Xbt2LU2aNMHAwABTU1P2799Pu3btcHV1pXXr
1ujq6pKVlUVwcDBBQUEAhIWFUb16dSwtLQkLC9PKsJ49ezYmJiYMHDgQMzMz2rdvX2p29uuWlV2l
ShXi4uLo0aMgs3/ChAnMmDEDd3f3R9o+LCyMFi1a8Pbbb9O+fXvUajVbtmxRAs/169fnp59+4qef
fqJZs2YcPHiQMWPGPHCf33//PR07dqRnz55069aNjh07llpe6FGEh6/Aza0N4APUAXxwc2tDePiK
J9qfJEmSJEnSq05GciRJeqGKBwO6devG3bt3gQfXIi4sEbJmzRo6d+6MgYGB8pX8mJgYrWOsX7+e
KlWq8Pfff5daWuT48eO8/fbbGBsbU6VKFTp16qQVmHwWNZGlF6NoCYjSSkQ8aHlmZibwb3Z00UDv
H3/88VTzKi3rMCcnh0uXLhEYGEhwcDBz5sxhy5YtWFpasnTpUm7evAlA//79MTU1VWp9Jycnk5yc
zKxZs2jQoAHu7p6oVAnARf7N+JuBlZU1rVq1olGjRqxatQqA5s2bc/LkSWxtbUv83E94+Ap0dXWA
nykIxBTU016w4OenuiYvg6lTp9KnTx98fX1p2bIlp06dIiYmBmNjY2XM0wQWi267b98+kpKSgIL3
WlxcHJMmTcLExIR3332X69evEx0dzaFDh2jRogWurq5kZGRgb29Py5YtWblypda+w8PD8fHxAeDm
zZu4urrSokULDh06RHR0NFeuXKFv375a2xQtvfO03zJ4lev/ltactW/fvoSFheHt7U2FChWoWbMm
x48fZ+7cuUyYMAF3d3ecnZ05cOAAn3zyCR9//DFJSUn4+voCBQHbzZs3c+bMGTZv3syVK1eYOXMm
O3fuZMaMGcqxT506hb+//4s69eeufv36bN26lUuXLpGVlcWJEycYNmwYAEuWLGH9+vVa42fOnMmO
HTuU58bGxoSFhZGenk5mZiZbtmwp8k2SAh999BFnzpzh1q1bLFmyhHHjxnHq1CllffHjGBoasnTp
Um7fvs2FCxcYNWoUO3bs0HqdHlVhk0qNRkNkZCQajYaoqC2YmJj8P3t3HhdVvT5w/DMzgGyyKSji
AsomKom74kah4J6Z5ZLknl1Twy29mqLlcrkqqbduXinFNU0zNVEUF1JyA8oVBVHR+qmkuKGpMDy/
P4gTI1iae33fr9e8mrN9z/ecMzPkc77neR64LUVRFEVRlL8FEXmuXkAdQJKTk0VRlN+cPn1adDqd
HDhw4Gl35b6dO3dOzM3NZfbs2ZKZmSmHDx+W//73v3Ljxg1ZsmSJuLm5yddffy2nT5+WNWvWSNmy
ZWXRokUi8tvxVq1aVdasWSOnT5+Wc+fOSdeuXSUsLMxkP6+++qr07t1b206v12vn6aeffpIyZcpI
165dJSUlRdLT02XhwoWSlpYmIvKH/VCeHy1btpTw8HBtesuWLWJubi4//vijNu/IkSOi0+kkJSVF
REQiIiIkICBAW16xYkX58MMPH3nfUlNTJTQ0VMqVKydWVlbi6+srXl5eYmdnJyNGjJBZs2aJu7u7
AGJraystW7YUFxcXmT17toiIXLhwQXr37i0uLi6i0+nEyspKOnXqJIcPH5Z169aJjY2tUJDvQwBp
2LCxvPHGG/LCCy9I2bJlZd68eSIiEhcXJxYWFjJp0iQ5cuSIpKamyhdffCHjx4/X+qrT6WTt2rUm
/XdwcJB//etfEhsbKzt37hSDwSAxMTHy888/S05OziM/X381LVu2lObNm5vMa9CggYwdO1Z27dol
Dg4OcufOHZPlnp6eMn/+fBERiYqKEk9PT23Z8ePHRafTab9jH374oYSGhppsf/bsWdHpdJKenq71
oU6dOo/smI4fP/7r522JgBR5LRZA69vzKCUlRfR6vZw5c6bYst69e4uHh4fk5+dr83x9faVFixba
tNFoFFtbW1mxYsU99zFjxgypX7++HD9+XGJjY2XIkCEmv0W9e/eWzp07P5oDUh5Y4XV5nj/HiqIo
iqIoT0pycnLhv0XryEPGhe8/eZ+iKM+8Z/mR46CgIAICAkxGLJ07dw6j0Ujnzp2pVKkg7UGNGjUA
01zEUJA/9MiRI3z66afaKEOA8PBwXn75ZW26R48evPnmm9y6dQtLS0uuX7/Ohg0bWLdunbaOFEkF
8J///AcHBweWL1+uPWpc9HH8++2H8vwJDg6mVq1a9OzZk6ioKHJzcxk8eLD2WS1JREQEw4YNw87O
jtDQUG7fvk1SUhJXrlzh3Xff/dN9KRx1WFRQUBAhISH88ssvTJo0CTMzM95//30mT54MYDJK2sXF
hQULFgCQlZXFe++9R2xsLPXr18fNzY033ujJoEGDSE1NZcGCBRw9epQDB77H1dWVIUOGMHDgQABa
t27NN998w+TJk4mMjMTc3BxfX1/69++v7auk3xmdTkf58uVp06YNUFA0csyYMfTt25ewsDA+//zz
P31uHgcPDw/Cw8OfqZGtlStXZuPGjXh6euLl5YWrqytZWVkcOHCA69ev4+TkZLL+rVu3tFHP3bp1
Y9SoUezbt48GDRqwdOlS6tWrp6V2OXDgANu2bStWeFOn05GRkaH95hVNvfOwCtPOxMcPxWgUCkZi
J2AwDCM4+PnO/1u0OGtISAitW7fm1VdfxcHBASj4O1b0e1KuXDktrzwU5MQvU6YMWVm/5ZVfsWIF
c+fOJSMjg5ycHPLy8sjPz8fHx0dbp3RpOy5fvqxG6z5F2dnZ9OjRi7i4WG1eSEhbli9foq6LoiiK
oijKE6AC2YryF1I0QPuo5ObmavlwH7V7BQMsLCy0XMRFA2hGo9HkkX6gWF7Kdu3aYTAYWLduHa+9
9hqrVq3ScsqW5MCBAzRr1qzEQk1FcyLf3Y/CgIXy/CgpALt27VqGDBlCixYt0Ov1tGnThjlz5tyz
jX79+mFjY0NkZCSjR4/GxsaGWrVqPVQQ+/eYm5sza9YsPv7442LLij76XlTRoHZRaWlpODg48PHH
H/9uELFVq1a0atXqnstLytubnZ1tMj1u3DjGjRt3zzaU32RnZ3PgwEF27NjBkiUFeXFDQtpiZlZQ
tDMnJ4cKFSqQkJBQ7De+8HeofPnyBAUFsWzZMho0aMAXX3zB4MGDtfVycnLo2LEjkZGRxdpwdXXV
3hdNvfMoLF++hO7d3yAu7rebfsHBbZ/7/L+FxVl3797N5s2bmTt3LuPHj2fPnj0Axf5m6nS6Eufl
5+cDsHv3bt544w0++OADWrdujb29PaGhbTlxIp2CIoDNgXe5fn0t3bu/waZNG57AUSolMS1g2hz4
lvj4oeq6KIqiKIqiPCEqR7aiPGdEhMjISLy8vLC0tMTd3Z1p06ZpyzMyMnjxxRexsbGhdu3a2j+s
oXAkUQ8qVaqEjY0N/v7+fPHFFybt36vgV1RUFP7+/tja2lK5cmUGDx7MzZs3TbZNTEwkKCgIGxsb
nJycaNOmDVevXqVPnz4kJCQwe/Zs9Ho9BoOBM2fOoNfrmTVrFjVq1GDt2rW8/fbbuLq6kpiYCBTk
Iq5RowadO3ema9euWFlZFcvVe3fgxdzcnFdffVXL+btkyRLs7e0pXbo0bm5ufPbZZ4gI//73vwEo
VaoU+/fvp2LFitja2tK4cWMSEhKA33IiiwizZs2ifPny3Lp1i82bNxMYGEjnzp2ZNm0a5cuXx9HR
kQ8//BCj0cjo0aNNCnoVNWbMGHx8fLCxsaFatWpMmDDBJDA4adIkAgICWLJkCR4eHjg4ONC9e3du
3LhxH58O5feUlMO0YsWKrFmzhmvXrnHlyhWWL1+Os7OztnzixImkpKSYbNOtWzdSUlL45ZdfuHjx
Itu3b9dG7D+LsrOzCQ0tKJTWtm1bvL29CQ1tx+XLlx/pftLS0ti4ceNzX8TvSevRoxeXL18DQoEz
wBLi4/ewf38SUJC3/Pz58xgMhmJ5y4uO0u7ZsycrVqxgz549nDx5ktdff11bVqdOHY4cOUKVKlWK
tWFlZfXYju2vnv+3aHFWc3Nzvv766z/Vzu7du3F3d2fMmDHUqVMHo9HIiRNpgDW/Fcr0Byr+JQpl
Pq/+6gVMFUVRFEVRngcqkK0oz5kxY8YQGRnJxIkTSU1NZdmyZZQrV05bPn78eEaPHs2BAwfw9vam
R48e2qivW7duUa9ePWJjYzly5AhvvfUWYWFh7N+/32QfJRX8MhgMzJ07lyNHjrBo0SK2b9/O6NGj
tW1++OEHgoODqVmzJnv27CExMZEOHTpgNBqZPXs2jRs3ZsCAAVy4cIFz585RqVIlrQDZSy+9xOHD
h9m3bx8iwuDBg6lYsSIZGRlYWVmxdu1aXFxc2LNnj0lg+F6pVHr27MmmTZs4evQo27dv5/r163zz
zTds2bKl2LFmZmaSkZHB8uXLOXToEF27dqVNmzZkZGTg4uKCo6Mjt2/fZtGiRSxevJijR49St25d
bG1t2bZtG+fOnWPnzp1ERUUxYcIE2rdvj5OTk0lBr//7v//T9mdnZ8eiRYtITU1lzpw5REdHExUV
ZdKnjIwM1q5dS2xsLBs2bCAhIYHp06c/wKdEeZyeVMD2UaUKMh1B+FugtHv3Nx5J+w8TKM/JyaFn
z57Y2tri5ubGRx99RFBQEMOHDwfgypUrhIWF4eTkhI2NDW3bti1WJHD16tXUrFkTS0tLPDw8it2s
+Pnnn+nQoQPW1tZUq1ZNu8n1LCgMjIEXUJ2igbGsrAtcu3aN4OBgGjVqxMsvv8yWLVvIzMzku+8t
280MAAAgAElEQVS+Y/z48SY3WV555RWuXr3K22+/zYsvvmjyd2Hw4MFkZ2fTrVs3kpKSOHnyJHFx
cfTt2/exPMlzNy8vL9q0afNcpxMpqqTirBcvXqR69ep/qj0vLy/OnDnDihUrOHnyZJHP8N0PThak
hnmeC2U+z/7KBUwVRVEURVGeGw+bZPtJv1DFHpW/sevXr4ulpaV8/vnnxZYVFj9csGCBNu/o0aOi
1+vl+PHj92yzffv2MmrUKG36fgt+rVq1SpydnbXpHj16SLNmze65/t2F9kREBg0aJN7e3pKUlCRn
zpyRlStXSqlSpUSn08mUKVPExsZGPD09pUaNGnLo0CFZsGCBREVFmRzvvYpbVqpUSfz9/QWQr776
Spt/6NAhAeSNN96QM2fOiMFgkDJlykiXLl0kKSlJ0tPTpUaNGvL222+LiEifPn0EkDFjxkhaWprW
j/r16z/Sgl6FIiIixNbWVm7cuKHNGz16tDRu3PiebShPxqVLlyQkpK1J0cSQkLaSnZ39tLt2T0+i
4F5ISFsxGJx+3ccZgSViMDhJSEjbP9y2f//+4uHhIdu3b5cjR47IK6+8InZ2dtpvRceOHaVGjRqS
mJgoBw8elNDQUPH29pa8vDwREUlKShKDwSBTpkyR9PR0iYmJEWtra4mJidH20aZNGwkICJB9+/ZJ
SkqKBAYGio2NjVYo82mKjY399fo0EQgvcn3OCCCtWrUSEZGcnBwZNmyYVKxYUUqVKiVVqlSRXr16
mRQqFRF57bXXRK/Xmxx/oRMnTkiXLl3EyclJbGxsxM/PT4YPH64tDwoKKvYbrZSspOKsn3zyiYiU
XISxpHPr4eFh8hl87733xNnZWezs7KR9+/a/fi5sinwmIgSqaN9bVezxyfsrFzBVFEVRFEV5nB5l
scenHpiWguD0YOAU8AuwB6j/O+uqQLbyt7Vv3z7R6/Vy+vTpYssKA7tJSUnavMuXL4tOp5OdO3eK
SEFgdfLkyVKrVi1xcnISW1tbsbCwkNdff13bpmXLljJw4MBi7W/ZskVeeuklcXNzk9KlS4uVlZXo
9Xq5efOmiIj4+flJRETEPfteUiA7NDRUdDqd6HQ6AUSv10upUqVEr9fLpk2bZPny5WJra6sFm1u2
bClff/21drx6vf6egezRo0eLXq8XnU4nZ8+eNTlPhYHsDRs2iE6nE2trazEYDFpwUqfTSfv27UVE
ZOHChWJubi4BAQFiaWmp9ePFF1/U1inUokULeeedd0zmValSRebOnatNf/HFFxIYGCjly5cXW1tb
sbS0lHLlymnLIyIipGbNmiZtREVFSbVq1e55bhVTJX3WHoWHCdg+Lb8FSs/cFXgpCJTGxsY+VPsP
E9i5fv26WFhYmNxounr1qtjY2Eh4eLikp6eLTqeTPXv2aMsvXbok1tbWsmrVKhER6dmzp4SEhJi0
O3r0aO07dPz4cdHpdCb/z3Ds2DHR6XTPRCBbBcaUe/nt92bxr9/Xxc/8783fgbouiqIoiqIoD+5R
BrKfemoRnU73OjATmAgEAAeAOJ1OV/apdkxRnkH3k8u0aEGpwtQEhalFIiMjmTt3LmPHjmXHjh0c
OHCA1q1bc+fOHZM27s47nZmZSYcOHahduzZfffUVKSkpWvG53Nzc++7b3XQ6HV26dCEjI4OMjAzS
09M5evQo6enpNG/enG7dulGvXj2GDh1aLBdxlSpVMBqN+Pv7l9j2v/71L1JSUtDpdCYpGqpUqUJA
QADOzs7k5ORgZmbGgQMHSEtL0/px4sQJPvvsM20bW1vbYjmRK1eu/KcLerVv354NGzbwww8/MG7c
uGLn//faUJ6cxMREdDodq1atem5zo1arVu3Xd9/etaQgD7ynp+dDtf8wj9qfPHmSvLw86tevr82z
s7PDx8cHgNTUVMzNzWnQoIG23MnJCR8fH1JTU7V1AgMDTdoNDAwkPT0dEdHaqFOnjrbcx8fnmSnW
6u3tTUhIWwyGoRSkfjkLLMFgGEZISNsnkopD5TZ/Ni1fvoTg4EZAL6Ay0Ivg4EbPfaHM5526Loqi
KIqiKE/X3cn3noZwYJ6ILALQ6XSDgHZAXyDyaXZMUZ41hQUet27dSt++fYst/6Ocut999x2dOnWi
e/fuQMETGenp6fj5+f3udsnJyeTn5zNjxgxt3t1FIv39/dm6dSsTJ04ssQ0LCwuTooZQUIDsq6++
okqVKuj1j/6+WrVq1TAzM2Pfvn107twZgGvXrpGenk7Lli0JCAggLy+PCxcuFAuGFTp//jy5ubmk
p6c/dFCpaEGvQqdPn36oNpXHR+S33MH3E7B9FvP/FgZK4+OHYjQKBf1NwGAYRnDwwwdKTQPlPYss
+eNAeeH5vft3q3B+0fN/9/LCbYq+v3v758Xy5Uvo3v0N4uJ6afOCg9s+9sBYQfHfXr/m6C4QElKw
379KMcbnWWGhzPT0dE6cOIHBYMBoNHLx4kV1fZ6iu6+Lp6fnM/nbryiKoiiK8lf1VEdk63Q6c6Au
sLVwnhT8CzQeaPy0+qUoz6pSpUrx3nvvMXr0aBYvXszJkyfZu3cvn3/+OfDHARwvLy+2bNnC7t27
SU1N5a233uL8+fN/uF9PT0/y8vKYM2cOp06dYvHixcybN89knbFjx7J//34GDx7MoUOHOHbsGJ9+
+inZ2dkAuLu7s3fvXjIzM7l06RLw+AuQ2dra8uabbzJy5Eh27NjBkSNH6NevHwaDAZ1Oh5eXFz17
9iQsLIw1a9Zw+vRp9u3bx/Tp01m5ciWhoe0YM2YMOTk5D1TA7l7uLug1Z84cvv7664c+zr+jmJgY
nJyc/nC9pUuXUr9+fezs7HB1daVnz578/PPP2vIrV67Qs2dPXFxcsLa2xsfHh5iYGACaNWsGQNeu
XWnXrt2vWzyekc2P0+McQXi/I4oTEhLQ6/Vcu3ZN27bojaZC165d4+DBgyQkJODn50dubi579+7V
ll+6dIm0tDTt5pufnx+7du0y6VNiYiLe3t7odDqqV69OXl4eycnJ2vLjx49z5coVbbpPnz688sor
D30u/qzCwFhaWhqxsbGkpaWxadOGxx6sfNxFQJVHo0yZMsye/R9CQkIeuJiq8vj81QqYKoqiKIqi
PC+edmqRsoABuHDX/AtA+SffHUV59k2YMIERI0YwceJE/Pz86NatmxaYK2lEdtF548ePp06dOoSG
hvLiiy/i6uqqjVQuaf1C/v7+zJo1i8jISGrVqsXy5cuZPn26yTpeXl5s3ryZgwcP0rBhQwIDA1m3
bh1mZgUPfowcORKDwYCfnx8uLi6cOXMGV1dXEhMTyc/PJyQkBH9/f4YPH46jo6PWjz8aZf5HoqKi
aNKkCR06dKB169Y0bdoUX19fLC0tAVi4cCFhYWGMHDkSX19fOnfuTFJSEnPm/OfXIM9AwJ77CfL8
0fnv0KED4eHhDBkyhICAAPbs2cOECRMe6vj+rrp160ZaWtofrpebm8uHH37IwYMHWbt2LZmZmfTu
3VtbHhYWxtq1a7l16xaWlpY4OTmRl5cHwLp16wCIjo7m/PnzvPhiK/T6t4FqgCXgiE43gNatfwtm
BAUFMWzYMN577z3KlCmDq6srkyZNMunT8ePHadq0KVZWVtSsWZOtW7ei1+u1/T1qjztQej+B8sKR
00VvUN3rRlMhT09POnXqxIABA0hMTOTAgQO88cYbVKpUiY4dOwIwYsQItm7dyocffkh6ejoxMTF8
/PHHjBo1CigMtIcwcOBA9u3bR3JyMgMGDMDa2vqRHPuj9KgCY/cTmH9eU+X8HakbDoqiKIqiKIpS
xMMm2X6YF+AK5AMN75ofCXx3j23qANK8eXPp0KGDyWvZsmUPkXpcUZS/gxs3boiDg4N8/vnn91xH
FWB7tuXm5v7u8t8r9rh//37R6/Vy48YNERGpV6+evPTSS5KRkSEHDhyQTp06ib+/v4iI7Nq1SwD5
8ssvRUTkyJEjJkVBAbGwsJAxY8aY7NvBwUEmT54sJ06ckEWLFoler5f4+HgREcnPzxcfHx8JDQ2V
Q4cOSWJiojRs2FD0er2sXbv2oc/No/Dll19KrVq1xMrKSsqUKSOtWrWShIQEMTc3lwsXLpisO3To
UGnRooWIiOzYsUMaNmwo9vb2YmNjIzVr1pSNGzdqhWgLi6/q9Xrp06ePiBQUfKxdu7ZW8NXNzU2s
rKykQYMGIiKyfv16AcTW1lb0er3o9Xpp3LixZGVlSWxsrFSvXl2srKzE3t5eSpUqJe7u7jJr1iyT
Y3B0dJSyZcuKlZWVuLu7y5IlS8TDw0Mr9ti7d2/p3LnzkzvBj9n9HM/jLgKqPBrqb5GiKIqiKIry
vFm2bFmxeG3z5s0fWbHHpx3INgdygY53zV8IrLnHNnUASU5OfoSnWVGUZ8nx48clNjb2kfwj/fvv
v5fly5dLRkaGJCcnS6dOncTR0VEuXbp0z22edpDnUR7/o7Rp0yZp2rSpODg4SJkyZaR9+/aSkZEh
IqIFK1euXCnNmjUTKysrqV+/vqSlpcm+ffukXr16YmtrK23atJGLFy+atDt//nypXr26WFpaSvXq
1eWTTz7RlhW2u2LFCmnRooVYWVlJTEyMLFy4UBwcHEzaWbdundSvX1/0er1YWVlJly5dJCkpSTp0
6CBlypQRvV6vBaDbt28vWVlZsnHjRrG2tpbatWvL6NGjZcOGDaLT6eTIkSPFAtn//Oc/pXr16pKW
lqZdn08++UTs7Oy0PrRs2VKaN29u0q8GDRrI2LFjRURk48aNYmFhIVlZWdry+Ph40el0z0Qg+9y5
c2Jubi6zZ8+WzMxMOXz4sPz3v/+VnJwc8fX1lRkzZmjr5ubmirOzs8TExIiISLt27SQkJESOHDki
p06dkg0bNsjOnTslPz9fvvrqK9Hr9XLixAm5cOGCXLt2TUREJkyYIPb29mJlZSXlypWTrl27CiD1
69cXEZEtW7ZoNwysrKzE399f3NzcpGXLlhIcHCyWlpYya9YsKVu2rERGRoqISHR0tAAyY8YMyczM
lPj4eKlbt672ue3UqZOcPn1aO467A7+3b9+WIUOGiIuLi1haWkrTpk1l//792vIdO3aITqeTDRs2
iL+/v1haWkqjRo3k8OHD2jqFn89vvvlGfHx8xNraWrp27So3b96UhQsXiru7uzg6OsrQoUMlPz/f
ZN8jRowQNzc3sbGxkUaNGsmOHTuKtRsXFyfVq1cXW1tbCQ0NlfPnz4uISERERLGbBgkJCcWuswqQ
Ph+e9t8iRVEURVEURXkUkpOTH1kg+6mmFhGRXCAZeKlwnq7gOfyXgO+eVr8URXk6srOzCQ1th4+P
zyPNBTpjxgxq165N69at+eWXX9i1a9fv5lc2LWBX1OPNh/y4jv9RuXHjBiNGjCA5OZlt27ZhMBiK
paaJiIhgwoQJfP/995iZmdGjRw/GjBnD3Llz2bVrFydOnDBJp7J06VIiIiKYNm0ax44dY+rUqUyY
MIHFixebtDt27FjeffddUlNTCQkJAUzTtmzYsIFXXnmF9u3bU69ePV599VX8/f0JDQ3FwcGBt956
i//9738sWrQInU7Hjz/+SJ8+ffD09CQ0NJSffvqJqKgoLRf2mTNnih3/sWPHaNy4sUkKiMDAQHJy
cvjxxx+19fz9/U22c3V1JSsrCyhI6VCpUiWcnZ215Q0aNHig6/A4nTt3DqPRSOfOnalcuTI1atRg
0KBB2NjY0LdvXxYsWKCtu27dOm7fvk3Xrl0BOHv2LIGBgfj5+eHu7k7btm1p2rQpOp1O+745Ozvj
4uJC6dKluXPnDlOmTEGn0xEdHc3cuXP59tuC71xhDuuPPvoIgJkzZ3LkyBHefPNNsrKySEhIIDo6
mvbt2/PDDz/w6quvsn37duC3QrSvvfYaFSpUYNCgQTg7O7Ns2TISExMpXbo0oaGhWgqZu40aNYo1
a9awePFivv/+ezw9PQkJCTHJqw0wevRooqKiSEpKwtnZmY4dO5oUtL158yZz585l5cqVxMXFsX37
djp37symTZvYuHEjS5YsYd68eaxatUrbZvDgwezdu5eVK1dy6NAhunbtSps2bYoUGy1od+bMmSxd
upSdO3dy5swZRo4cCRSkcHrttdcIDQ3lwoULnDt3jiZNmhQ7xvvNba48XU/rb5GiKIqiKIqiPLMe
NhL+sC/gNeAXIAzwBeYBlwDne6yvRmQryl9USEhbMRicfh0leEZgiRgMThIS0vYp9mXxr31Z/Nj7
8iwd//3IysrSRi8XjpxesGCBtvyLL74QvV5vMqJ0+vTpUr16dW3a09NTvvjiC5N2P/zwQ2nSpImI
/DYie+7cuSbrLFy4UBwdHbXpJk2aSFhYmIj8llokOTlZdDqd/Pjjj9p6ixcvFr1eL8uWLRO9Xi9e
Xl4SGhoq27Ztk2PHjsnEiRMFkLVr18q+ffsE0PrXuXNn6devn0k/fvjhB9Hr9do+Skpr8vLLL2up
ND766CPx9PQ0WX7t2rVnZkS20WiUVq1aiZ2dnXTt2lXmz58vly9fFpGC621hYSF79+4VEZGOHTtK
//79tW2jo6PF3NxcAgMDZeLEiXLw4EFt2Y4dO0Sv18vVq1e1efv37xdASysCaKlbXF1d5cyZM2Iw
GESn05mM4vfz8xNzc3MREVmzZo3Y2dnJuHHjpG7dunLt2jWxsrKSOnXqSOnSpcXOzt4kFUxISFs5
f/68WFtby5YtW0TEdET2jRs3xMLCwuQzmZubK25ubtpo9MIR2YUj9UVEsrOzxdraWpu3cOFC0ev1
curUKW2dQYMGia2trdy8eVObFxoaKm+//baIiGRmZoqZmZmcO3fO5JoEBwfLuHHj7tnuJ598Iq6u
rtr0/aZKyc7OlpCQtsXOT3Z29h9uqzw5T+NvkaIoiqIoiqI8Sn+ZEdkAIrISGAFMBr4H/IEQEfn5
qXZMUZQn6lkrPnY/BewepWft+Ety4sQJevToQbVq1bC3t6dq1arodDqT0cu1atXS3pcrVw6AmjVr
mswrHJ188+ZNMjIy6NevH6VLl9ZeU6ZM4dSpUyb7rlu37u/27YcffuDFF180mVe5cmUsLCyYM2cO
69ato0GDBvTp04f8/HytqGB6ejotW7akcuXK5OXlsWXLFm37MmXKAJCYmEhWVhbVqlXju+9MHxYq
HOHr5ub2+yfvV76+vpw5c0Yr0Aqwb9+++9r2SdDr9WzevJlNmzZRo0YN5s6di4+PD5mZmTg7O9Oh
QwcWLFhAVlYWGzduNCnO2K9fP06dOkVYWBiHDx+mXr16fPzxx/fc1/HjxwFYtWoVGRkZZGRkkJaW
Ro0aNWjfvj2HDh0iPz8fEcHd3V37fBQt8tmuXTsMBgPHjx8nPz+fVatWYW9vT1JSEn5+Nbl27cav
a+qAUsTFxeLm5sbt27dNRjkXysjIIC8vz2QUs5mZGQ0aNCA1NVWbp9PpaNSokTbt6OiIj4+PyTrW
1ta4u7tr0+XKlcPd3R0rKyuTeYXfh8OHD2M0GvH29jb5Pnz77bcmfb273aIj/h/E4y4CqjwaT/pv
kaIoiqIoiqI8y8yedgcAROQT4JOn3Q9FUZ6e3wI1ze9a0gIoCKI+ycfdC4M86enpnDhxAk9Pz8e6
/2ft+EvSvn17PDw8iI6OpkKFChiNRmrWrMmdO3e0dczNzbX3hak/7p6Xn58PQE5ODgDR0dHF0msY
DAaTaRsbm9/tW9HgYOF+y5YtS0xMDGPGjCEyMhJnZ2emTp3Ke++9R1RUFP/4xz+wtLRk2rRpTJo0
CXNzcwwGA3q9XuuDTqdj1apV/Pe//6VBgwacPXuWIUOG8M4773Ds2DEiIiIYMWLE/Z1AoFWrVlSt
WpWwsDAiIyO5du0a48ePR6fTmaRKedoaN25M48aNef/996lSpQpr1qzh3XffpX///nTr1g03Nzc8
PT1NgrkAbm5uDBw4kIEDB/LPf/6T+fPnM3jwYCwsLABMUm9UrVoVgJ9++olXXnlFm29hYYGtrS05
OTkYDAaMRiO7du2idOnSAKxevZopU6YABZ+tV199lW+//RZra2uWL19Ot27dSE9PZ+/e3RRkKrsB
nAb6AU4YjSOIj48vMaWLFDz5VexaiMh9XZ+i6xT93BcuK2le0e+DmZkZKSkp2mewkK2t7e+2W9jv
P8PLy+up/7Yo9/ak/xYpiqIoiqIoyrPsqY/IVhRFgWc3F2jRfMiP04Mef1BQEMOHD9emPTw8mDNn
zmPrX3Z2NmlpaYwfP56goCB8fHzIzs5+qDZdXFxwc3MjIyODqlWrmryqVKmirXc/AUR/f3+2bt0K
wLZt25g1axYAr7/+OqtXr0av1/P9998zatQo8vPztcD4nDlzqFixIlAQWF27dq3JPnU6HZs2bSI3
N5fExERiY2PZv38/tWvX5h//+AcDBgxg3Lhx991XvV7P2rVruXHjBg0aNGDgwIG8//77iAiWlpb3
e+oem3379jFt2jSSk5M5e/Ysq1ev5uLFi1SvXh2AkJAQ7O3tmTJlCn379jXZNjw8nM2bN3P69GlS
UlLYvn07fn5+AFSpUgWdTsf69eu5ePEiN27cwN/fH4PBwPjx41m0aBEnT54kISGBI0eOcPToUQIC
AjAajYgIHh4e2mfDxcXFJNDbs2dPTpw4wS+//ML27dupXbs2U6dO/XVpA+AIcJmCm0QF+bzv3Lmj
BcaL8vT0xNzcnF27dmnz8vLyfh3h7afNExH27NmjTV++fJm0tDTtPP0Zhcd74cKFYt8HFxeX+27H
wsLC5IaB8tfwpP4WKYqiKIqiKMqz7JkYka0oilJYfCw+fihGo1AwEjkBg2EYwcF//eJjz/rxOzo6
UqZMGf73v/9Rvnx5MjMzGTt27B8Gbv9opGhERATDhg3Dzs6O0NBQbt++TVJSEleuXOHdd9+9rzYA
Jk6cSHBwMFWrVqVbt27k5uayadMmRo0aZZJiZNCgQRw6dIgPP/wQgIYNG3L48GGTtlJTU8nIyODO
nTvFAoLNmjUzCWDebdu2bcXmrVmzxmTa29tbK2oIBelJdDrdM1G4zc7Ojm+//ZbZs2dz7do1qlSp
wqxZs0wKbPbu3Ztp06bRq1cvk22NRiPvvPMOP/74I3Z2drRp00a7oVChQgUmTZrEmDFj6Nu3L2Fh
YXz++ecMHDiQlStX8v7773Pu3Dn0ej35+fnY29vj5eVFcHAwW7ZsYf369QQGBpKVlcU333xDbm6u
tt8WLVpgY2NDZmYmVatWpWHDhnz22We/Lp1BQVoRD8AaKCis+MUXX/DCCy9QoUIFk2Owtrbm7bff
ZtSoUTg6OlKpUiUiIyP55ZdfigXuJ0+ejJOTEy4uLowbNw5nZ2c6der0p8+9l5cXPXr0ICwsjBkz
ZhAQEEBWVhbbtm3jhRdeoE2bNvfVjru7O5s3byYtLY0yZcpgb2+PmZn63z1FURRFURRFUZ5/akS2
oijPjL97LtDly5fw4osNeBaPX6fTsWLFCpKTk6lVqxYjRoxgxowZ2rKi/717u9/Tr18/oqOjWbBg
Af7+/rRs2ZKYmBg8PDzuuw0oCGZ++eWXrF+/noCAAIKDg7Xc02XLlmXhwoWsWrWKGjVqEBkZycyZ
M4u1kZ2dTWhoO3x8fGjbti3e3t6Ehrbj8uXLf7j/B/H1118THx9PZmYm8fHxvPXWWzRt2tTkmJ8W
X19fNm7cyPnz57l58yapqam8/fbbJuv89NNPtG3blmPHjmEwGLh27RpQMLo9LS2Nmzdvcv78eRYs
WMC6deu0nMvjxo3j//7v/8jLy+Pzzz8H4N///jcVK1bkxx9/pGzZskyZMoWyZcuSkpICwMaNG4mI
iGDChAn4+vrSuXPnYqOhAQYNGsTt27fp2bMnvr6+fPvtt4SEtMVgKA3MoqD8RjtgONbW1lhZWWFn
Z1fiOZg+fTpdunQhLCyMevXqcfLkSTZv3oy9vb22jk6nY/r06QwbNoz69evz888/s379+ocOGC9c
uJCwsDBGjhypHW9SUhKVK1e+7zYGDBiAj48P9erVw8XFpVhed0VRFEVRFEVRlOfWw1aLfNIvoA4g
ycnJf7papqIoz7a0tDSJjY2VtLS0x7aP69evS48ePcTGxkYqVKggUVFR0rJlSwkPDxcRkdu3b8uI
ESPEzc1NbGxspFGjRrJjxw5t+4ULF4qDg4PExcVJ9erVxdbWVkJDQ+X8+fMm+5k/f75Ur15dLC0t
pXr16vLJJ59oy06fPi06nU5WrFghLVq0ECsrK4mJiZF9+/ZJixYtpHz58mJtbS21atWS5cuXm7Rb
tK8iIu7u7jJ79mwREenbt6+0b9/eZP3c3FxxdnaWBQsWPJLz91cUEtJWDAYngSUCZwSWiMHgJCEh
bR/pfv71r39JhQoVxNLSUipVqiR9+/aV7OzsR7qPx+Hq1auyc+dOsbKykq1bt0pubq5cuHDhd7dZ
uHChODo6/u46EREREhAQoE337t1bOnfu/ND9zc7OlpCQtoXVsQWQkJC2D32ud+zYIXq9Xq5evfrQ
fVQURVEURVEURfmrS05OLvw3WR15yLiwetZUUZRnzpMoPhYeHs7u3bv55ptvcHFx4f333yclJYWA
gAAABg8ezLFjx1i5ciWurq6sWbOGNm3acOjQIS2f9c2bN5k5cyZLly5Fp9PRs2dPRo4cyeLFiwFY
unQpERERfPzxx9SuXZvvv/+eAQMGYGtra5KWYezYscyaNYvatWtjaWmJ0WikY8eOtGrVitKlS7Nh
wwbCwsKoVq0a9evX/8Nj69+/Py1atODChQuUK1cOgPXr13Pr1i1ee+21R30qnwtpaWlkZGTcs1Ba
WloacXGxwBKg569ze2I0CnFxvUhPT3/oz2R2djY9evT6dT8F/PxqMWPGDG3U8rOsU6dO7N+/n3/8
4x+8+OKLAA+Uu/lJuPs6P64iefIQxRUVRVEURVEURVGUP0elFlEU5W8nJyeHRYsWMXPmTHp+EH8A
ACAASURBVFq2bImfnx8LFizQ8iGfPXuWhQsX8uWXX9KkSRM8PDwYPnw4gYGBLFiwQGsnLy+PefPm
ERAQQO3atXnnnXe0goNQkP955syZdOrUiSpVqvDyyy/z7rvv8umnn5r0Jzw8XFunXLlyVKhQgeHD
h1OrVi3c3d0ZPHgwISEhfPnll/d1fI0bN8bb21sLqENByoKuXbtibW39MKfuuXO/6UIyMjJ+fdf8
rhZaAHDixImH7kuPHr2Ij99DQbD8DLCE+Pg9dO/+xkO3/SgEBQUxdOhQwsPDcXJyonz58nz22Wfc
vHmTvn37kpycjKurK8HBwQAkJCSg1+u11CJQ8DmrUqUKtra2dOnShUuXLhXbz/Tp0ylfvjz29vb0
79+fW7du/W6/RIRp06ZRtWpVrK2tCQgIYPXq1Sbr/N51fhxF8u4n3c2TlJaWxsaNG0lPT3/aXVEU
RVEURVEURXlsVCBbUZS/nZMnT5KXl2cyutnOzg4fHx8ADh06hNFoxNvbm9KlS2uvb7/9tkjAs6Aw
nLu7uzbt6upKVlYWUDBaOyMjg379+pm0MWXKFE6dOmXSn7p165pM5+fn88EHH+Dv70+ZMmUoXbo0
mzdv5syZM/d9jP3799eC7hcuXGDjxo3069fvvrf/q7jf4HHhKHv49q4WEgAeuhBj4Yhvo3EOBSO+
K1Ew4ns2cXGxz0wActGiRTg7O7N//36GDh3KoEGD6Nq1K4GBgXz//fe0bt2asLAwLfhcNKC7d+9e
+vfvz9ChQ/nhhx8ICgrSimoWWrlyJZMmTWL69OkkJSXh6urKJ5988rt9mjp1KkuWLOF///sfR48e
JTw8nF69erFz505tnSd5k6BFixYYjcZ75th+kp5UXndFURRFURRFUZRngUotoijK305hWoC7R1UW
zs/JycHMzIyUlBT0etP7fba2ttp7c3Nzk2U6nc6kDYDo6GgaNGhgsl6LFi2YM2cOnTp1AsDGxsZk
eWRkJHPnzmX27NnUrFkTGxsbhg0bxp07d+77GMPCwhg7dix79+5l165dVK1alSZNmtz39n8FD5Iu
xNvbm5CQtsTHD8VoFApGYidgMAwjOLjtQ4/mvZ8R3487nc79eOGFF/jnP/8JwJgxY5g2bRrOzs7a
TZAJEybw3//+l4MHDxbbds6cObRp04YRI0YA8M4775CYmEhcXJy2zuzZsxkwYAC9e/cG4IMPPiA+
Pp7bt2+X2J87d+4wbdo0tm7dSsOGDQFwd3dn586dzJs3j2bNmj2RtDDPKtMAfnPgW+Ljh9K9+xts
2rThKfdOURRFURRFURTl0VIjshVF+dupVq0aZmZm7Nu3T5t37do1bVRsQEAAeXl5XLhwgapVq5q8
7jcnsIuLC25ubmRkZBRr44cffmDgwIFAySkKvvvuOzp16kT37t2pVasWixYtYsuWLQ90jE5OTrz8
8st8/vnnxMTE0KdPnwfa/q/gQdOFLF++hODgRkAvoDLQi+DgRixfvuSh+/K4R3w/Kv7+/tp7vV5P
mTJlqFWrljavMOd64ZMHRaWmpmrB5kKNGzcuts7dN3buXqeoEydOcPPmTS1ffOFr8eLF2vV9Emlh
nkXPyyh/RVEURVEURVGUR0WNyFYU5W/H1taWN998k5EjR+Lo6IizszMREREYDAZ0Oh1eXl707NmT
sLAwZsyYQUBAAFlZWWzbto0XXniBNm3a3Nd+IiIiGDZsGHZ2doSGhnL79m2SkpK4cuUK7777LlBy
0TgvLy9Wr17N7t27cXBwYP369eTm5j7wcfbr14/27duTn5/Pm2+++cDbP+9Mg8c9iywpOXjs6Oj4
2IoDPu4R349KSU8Z3D0PCtLf3E1E7it39IPkly58siE2NpYKFSqYLCtVqhTw4Nf5r+J5GeWvKIqi
KIqiKIryqKgR2Yqi/C1FRUXRpEkTOnToQOvWrWnatCm+vr5YWloC0KFDB3JycujSpQseHh40b96c
vXv3UqlSJSZPnszw4cO5fPkyAQEBJqkT8vPztdQM/fr1Izo6mvnz5+Pt7U1gYCAxMTFMmzaNOXPm
AAVBvevXr9O/f39cXFywt7cnKSmJatWqERoaSuPGjUlJSUFEWLNmDQaDgUWLFhULBpYUHAwODsbV
1ZXQ0FDKly//uE4lQUFBDB8+/LG1DyUXFvwjhcFjg2EoBakXzgJLMBiGERJy7+Dx4ygOCI93xPez
wM/Pjz179pjM2717t8l09erVi61z9/TdbZYqVYrMzMxiTza4ubkBf/46P++el1H+iqIoiqIoiqIo
j4oaka0oynNj4MCBrF69mitXrvD999+bpEF4UDY2NixevFibvnnzJhEREbz11lvo9Xr0ej2zZs3i
5Zdf5vr16+zcuZOwsDDmzZtHVFQU//vf/6hduzafffYZHTt25OjRo3Tq1In//Oc/zJgxg6lTpwLQ
rVs3Ll68yMyZM7Uijx4eHgBUqVIFo9FIq1atsLW1JS4uDjs7O+bNm8fChQvJzMzE0tKS999/n7i4
OLZu3YqIYG9vT1hYmMnxnDx5stgx3rx5k8uXLz93RR6DgoIICAhg1qxZJvMfZCRvoeXLl9C9+xvE
xfXS5gUHt30qwePHOeL7cTl//jxr1qxh6NChJS4v+kTB0KFDadq0KTNnzqRTp05s2rTJ5CYPwLBh
w+jTpw9169YlMDCQJUuWsGfPHi0ofTdbW1tGjhxJeHg4RqORpk2bcvXqVRITE7G3t6dXr4Lr+ixd
5yfleRnlryiKoiiKoiiK8qioQLaiKM+FTZs2sWjRIhISEvDw8KBs2bIP1d4PP/zAsWPHaNCgAVeu
XGHy5MnodDo6depE5cqVadWqFZ07d6ZSpUoA1KhRA4CZM2cyZswYunbtCsD06dPZvn07H330EXPn
zuX1119n+PDhJCYmEhgYCMDy5cvp0aNHif3YtWsXSUlJZGVlaSkcIiMjWbNmDatWraJ///7Y2tpi
ZmaGs7PzfR3b8ePHSUlJYfv27Tg6OtKhQ4eHOlfPs2cxeOzl5fXU+1CS+71RUHS9ou8bNmzI/Pnz
mThxIhMnTiQ4OJj333+fDz74QFvntdde4+TJk7z33nvcunWLLl26YGdn97v7++CDDyhXrhzTp0/n
5MmTODg4UKdOHe3JB3g2r/OT8HcM4CuKoiiKoiiK8velUosoivJcOHHiBK6urjRs2BAXFxf0+gf/
+TIajSbTM2bMoHbt2rRu3ZpffvmFXbt24eTkRFBQEMHBwdSsWZPXXnuN6Ohorly5wvXr1/m///s/
mjRpYtJOYGAgqampAJQtW5bg4GCWLl0KwKlTp9i9e/c9A9kHDx7k+vXrODk5mRSzO336dJEcuPcn
Ozub0NB2+Pr60qNHD+bPn4+zczmuXr36QO38nps3bxIWFkbp0qVxc3MrNmr6zp07jBw5kooVK2Jr
a0vjxo1JSEgw6WOPHj2oVKkSNjY2+Pv788UXX2jL+/TpQ0JCArNnz0av12MwGDhz5oy2PCkpifr1
62NjY0NgYOB9F7R7XOlC/kq2bdtW7Ho2atSIgIAAk3lGo5GOHTvSokULjEajSSC6d+/eZGZmkpOT
w9dff014eDjZ2dkm248ZM4YLFy5w9epVPv/8cxwdHRk1apS2fMGCBXz11Vcm27zzzjscPXqUW7du
cf78eWJjY2natGmxY3jQ6zxw4EDKlCmDwWDg4MGDf7i+Xq9n3bp1AGRmZqLX6+9ru8elMICflpZG
bGwsaWlpbNq0AUdHx6fWJ0VRFEVRFEVRlMdFBbIVRXnm9enTh6FDh3LmzBn0ej1Vq1blzp07DB06
lHLlymFlZUWzZs1ISkrStinMqbxp0ybq1auHpaUliYmJAKxdu5Z+/fpx5MgRXFxcGDp0KLGxsfj5
+QFgZmbGO++8w6ZNm6hRowbTp0/H2dkZZ2dnRIRdu3aZBLDOnj3L1q1b2bZtG/Xr12fr1q3Mnz+f
Y8eOsWzZMl544QVtRPfdcnJyqFChAgcPHuTAgQPa6/jx4ybBvfvRo0cv4uP3UJAn+AywhJSUdLp3
f+OBz/m9jBw5kp07d7J+/Xo2b97Mjh07SE5O1pYPHjyYvXv3snLlSg4dOkTXrl1p06aNFpS/desW
9erVIzY2liNHjvDWW28RFhbG/v37AZg9ezaNGzdmwIABXLhwgXPnzmmj4kWE8ePHExUVRXJyMmZm
ZvTt2/eRHZtSsry8PIYMGYKDgwPOzs5MmDBBW3blyhXCwsJwcnLCxsaGtm3bcuLECZPtV69eTc2a
NbG0tMTDw6NYsPxu0dHRODo6sn37dgBWrVqFj48PlpaWODo6ajeeHlbhUx6xsbGcO3eOmjVrPnAb
fybdzeOgbtQoiqIoiqIoivK3ICLP1QuoA0hycrIoivLs2LFjh+h0Orl69eo914mIiJCAgIAHbvva
tWvi4OAgjo6OkpWVJRcvXpShQ4dKxYoVJS4uTlJTU6V3797i5OQkly9fNulP7dq1JT4+Xk6ePCmX
L1+WnTt3ir29vSxevFhOnz4t8fHxUrVqVZk8ebK2P51OJ2vXrhURkevXr0uZMmXE2tpa3nvvPSlb
tqw4OzuLXq+XAwcOiIiIr6+vANK4cWPZuXOnpKSkiMFgED8/P6lRo4b8+9//Njked3d3mT17toiI
bNmyRczNzSUzM/Oexz916lTx9/f/3XN0/PhxAQSWCEiR12IBJC0t7YHP+91ycnKkVKlSsnr1am1e
dna2WFtbS3h4uJw5c0bMzMzk3LlzJtsFBwfLuHHj7tlu+/btZdSoUdp0y5YtJTw83GSdHTt2iF6v
l+3bt2vzYmNjRa/Xy+3btx/yyJR7admypZQuXVrCw8MlLS1Nli1bJjY2NhIdHS0iIh07dpQaNWpI
YmKiHDx4UEJDQ8Xb21vy8vJERCQpKUkMBoNMmTJF0tPTJSYmRqytrSUmJkbbR9Hvw7/+9S9xdnaW
/fv3i4jI0aNHRafT/frZLnj5+dWQH3/88aGPbe7cueLu7v5A2xT9bTh9+rTodDrtd0BRFEVRFEVR
FEUpLjk5ufDfc3XkIePCakS2oih/SlBQEMOHDzeZ90ejE0eNGsXWrVsfeF+lS5fWCjA6OztjZWXF
p59+yowZM2jdujW+vr7Mnz8fKysrPvvsM5NtP/jgA1566SU8PDxwcHBg0qRJjB07ljfeeIMqVarw
0ksvMXnyZD799FOT7VatWkVycjJz5swhNzcXo9FIUFAQ48ePJycnBxHh9OnTjBkzhoyMDPR6PVOn
TqVp06YEBATQrFkzjh49SmpqKt27d7/nsQUHB9O4cWNefvlltmzZQmZmJt999x3jx48nJSUFAHd3
d06dOsWBAwe4dOkSd+7cKdbOb2lImt+1pAVAsVGyADExMTg5Of3B2TfdR25uLg0aNNDmOTo64uPj
A8ChQ4cwGo14e3ubpEn59ttvtf7l5+fzwQcf4O/vT5kyZShdujSbN282SR/ye2rVqqW9d3V1BSAr
K+u+j0F5cJUrV2bWrFl4eXnRvXt3hgwZQlRUFCdOnGD9+vV89tlnNGnShFq1arF06VJ+/PFHvv76
awCioqIIDg7mn//8J56enoSFhfHOO+/w73//u9h+xowZw5w5c0hISKBevXoA9Os34Neb2LMpfMrg
+PFz9Os38KGOqehTHgaDAQ8PDzw8PJgzZ47JegEBAUyePPmh9qUoiqIoiqIoiqI8GqrYo6IoT4y1
tTXW1tb3XJ6bm6sVPPw9J06cIC8vzyRXtZmZGQ0aNNByVUNBYL1u3bom2x44cIDvvvuODz/8UJtn
NBq5c+cOt27dwtLSEoAjR47Qrl07Ll68SKlSpYiKiiIkJITWrVuTnp7Oxx9/zKuvvkrNmjWZNm0a
o0ePNgmydunShR07dtCwYUPc3NxM+nB3wD82NpZx48bRt29ffv75Z8qXL0/z5s0pV66c1taaNWsI
Cgri6tWrLFiwgLCwMJM2qlWr9uu7b4GeRZYU5Kf29PQsdh67detGu3btSjjDJSsIKN77hkVOTg5m
ZmakpKQUy2Fua2sLFBSynDt3LrNnz6ZmzZrY2NgwbNiwEoPzJSn6+SjsR35+/n0fg/LgGjVqZDLd
uHFjZs2axdGjRzE3Nze5seHk5ISPj4/2PUxNTeXll1822T4wMJDZs2cjIto1nDFjBjdv3iQpKQl3
d3cA0tLS2L07EagJvA/sAlpjNE4lLm4Q6enpfzqVxpw5c6hWrRrz588nKSkJnU5H/fr1/1RbiqIo
iqIoiqIoypOhRmQrivLASirId/r0aaB4Mb60tDRtu0mTJpkUjuvTpw+dO3dm6tSpuLm54evrC8DP
P/9Mhw4dsLa2plq1aixbtqzEftwdUC0aGCtkY2NjMp2Tk8OkSZNM8lEfPnyYtLQ0LYgNMHHiRM6f
P8+QIUNo0qQJb7/9trbPgQMHotfrSUpKIiUlRRs9WjTI2qxZM/R6vUkhw0InT55k6NChJn386KOP
OHv2LLdu3eL06dMsWrRIC4BbWFiwcuVKsrOzMRqNxYLYAN7e3oSEtMVgGEpBjuyzwBIMhmGEhLQt
FvDLy8ujVKlSlC1btsRzWxJPT0/MzMzYs2ePNu/y5cvaNQ4ICCAvL48LFy5QtWpVk5eLiwsA3333
HZ06daJ79+7UqlULDw+PYgUbLSwsihXmVJ4fRb+HJX0nC2+IFNW8eXOMRiMrVqzQ5v32lEEssAmo
AcylIKhd8lMG96vwaQGDwYCzs/MDfQ8URVEURVEURVGUp0MFshVFeWD3KsgnJRTj69evn8m2dwe1
tm7dSlpaGvHx8XzzzTcAvPnmm/z0008kJCSwatUqPvnkE3JycrRtPD09MTc3Z9euXdq8vLw8kpKS
tIKN91KnTh2OHz9eLNBatWrVEtf39fXl4MGD5ObmavMKCxM+aatWrcLf3x9ra2vKli1rUvQuOjqa
U6dOIHIF6AVUBnoRHNyIyMhp6PV6Vq5cScuWLbG2tmbZsmXExMTg6Ohoso+1a9dSt25drKys8PT0
ZPLkyVpQ2cbGBn9/f15//XUsLCwoV64c9erVw2AwAAUF53r27ElYWBhr1qzh9OnT7Nu3j+nTp7Nx
40ZtnS1btrB7925SU1N56623OH/+vEkf3N3d2bt3L5mZmVy6dEkLfJYUAC1pnvJoFb1xAbB79268
vLzw8/MjNzeXvXv3assuXbpEWlqa9j308/Mz+Z4CJCYm4u3tbfJb0KBBAzZt2sTUqVOZMWMGcPdT
Bo2BicD3QMHnsaSnDBRF+esoKYWZoiiKoiiK8vemAtmKojwwOzs7LCwssLa2xtnZGRcXFwwGAzqd
TssT7evry5gxY/juu+9+N22Era0t0dHRVK9enerVq5Oens6mTZuIjo6mfv36BAQE8Nlnn5m0YW1t
zdtvv82oUaOIi4vj6NGj9O/fn19++YW+fftq65UU5JwwYQKLFi1i8uTJHD16lGPHjrFixQref//9
EvvXo0cPjEYjAwYM4NixY8TFxTFz5kzANCj/qIOsaWlpbNy4URutfP78eXr06EH//v05duwYCQkJ
vPLKK4gIS5cuJSIigsjISE6ePMnHH3+MnZ0dkZGRbNq0AXt7ewDGjh3Lu+++S2pqKiEhIcWOYdeu
Xbz55puEh4dz7Ngx5s2bR0xMDFOnTgUKAulpaWkEBQVhYWFBfn4+devWNUnfsnDhQsLCwhg5ciS+
vr507tyZpKQkKleuDMD48eOpU6cOoaGhvPjii7i6utK5c2eTYx85ciQGgwE/Pz9cXFw4e/Zssb4W
+qO87MrDO3v2LCNHjiQtLY3ly5fzn//8h3f/n717j8vx/h84/rrvu+NdSVKOoXSgKDnmmGSiLYc2
Q5GzfW2jn+W0zTR2Ml/f5jBjDlPYYrNh5pARmeRULYUpoTKnEdvCFnef3x/pWncHQg7Z5/l49FjX
+XNddV/Z+3pf7/f//R+Ojo706dOH0aNHEx8fT0pKCoMHD8bOzo7evXsDEBYWxs6dO3n//ffJyMgg
KiqKhQsXMmnSpFLHadeuHVu3buW9995j7ty5ODs7065dB1Sq0cB7wAEgFMilVas2D1xWpDxqtbrU
Z7b4AyxJkqom+TmWJEmSJEl6hjxst8jH/QW0BERiYuIDdcqUJKlydO3aVUyYMEGZ3r17t1Cr1eLy
5cvKvOTkZKFWq0VOTo4QQoh3331XeHp6KsuHDRsmevToobffjRs3CiMjo1LHMzU1FdbW1sr0X3/9
JUJDQ4Wtra0wNTUVnTt31rsvFI3n999/L7Wv7du3i06dOgkzMzNRvXp14eXlJZYtW6YsV6vVYuPG
jcp0QkKCaNGihTAxMRFt2rQRa9asEWq1WqSnp5d7rJ9//lmo1WqRlZV1l6tY2pUrV4Sfn39RR18B
CD8/f+UY2dnZpbZxdHQUa9as0Zv3/vvviw4dOgghhDhz5oxQqVRiwYIFeutERkYKKysrZbp79+5i
1qxZeuusXr1a1K1bVwghREREhGjSpIm4ffv2fZ2TVHX5+PiI119/Xbz66qvC0tJSWFtbi3feeUdZ
fu3aNTF06FBhZWUlzMzMhL+/vzh58qTePr777jvRrFkzYWxsLBo1aiQiIiL0ltvb24t58+Yp03v2
7BEWFhZiwYIFYv/+/aJmTRu9z0PTpm4iNzf3oc9t7ty5wt7eXplu166dmDJlijL9+++/C61WK2bM
mKHMU6lUyr3hzJkzQq1Wi5SUlIcei1RxRfezouu+e/duoVKpyrzXF4mMjBTVq1d/XEN8pm3atEnv
Wv78889CpVKJt956S5k3cuRIERISIoQQ4qeffhKdO3cWpqamokGDBmL8+PHi+vXryroLFy4UTk5O
wsTERNSqVUv0799fCFH47wOVSiXUarXy36K/p6mpqaJXr17C3Nxc1KpVSwwZMkTv3x5du3YVr7/+
uvi///s/UbNmTdGtWzchROHnd9myZaJfv35Cq9UKJycn8f333z+6iyVJkiRJkiQJIYRITEws+v+5
luIh48Ky2aMkSZXqfpvxlaxhLcrJYjYxMWH69OnKtLGxMXPnzmXu3Lllru/t7V1uneXnnnuO5557
rtwxldzOy8uL5ORkZfrLL7/E0NBQyTIu61geHh4PVOc5KGgIO3bsp7DOdRdgDzt2jEeIj/H19aVZ
s2ZK08mXXnoJIyMjMjMzGTlyJKNGjdI7h+rVq+vtu2Tjy5Lu1Qizf//+zJ07F3t7e3r27Im/vz8B
AQFKaZFHKT09nczMTBwdHSs9E7eIj48Pnp6eREREPJL9V0WxsbHK9wsXLiy13NLSksjIyLvuo1+/
fqWy7os7deqU3nTnzp35448/lOnffrtERkYGJ0+efKQ//27duhEVFcULL7yApaUl4eHhGBjc/Z9J
5d2vpEenQYMGXLhwQa+ueUXezJBvb1SOLl26kJeXR3JyMp6ensTFxWFjY8Pu3buVdfbs2cObb77J
qVOn6NWrFx9++CGRkZFcunSJ119/nXHjxrF8+XIOHz5MaGgoX375Je3btyc3N5effvoJKCxhlp6e
TvPmzXnvvfcQQmBjY8Pvv/+Or68vY8aMYd68edy4cYMpU6bw8ssvs3PnTmUMK1euZOzYsezbt09v
/DNnzuS///0vc+bMYf78+QQHB5OdnV3q76UkSZIkSZL0dJKlRSRJeiCPqiFf06ZNuX37NomJicq8
EydOcO3atUo/VkWtWrWK+Ph4zpw5w4YNG5g6dSoDBgzA2NhYWadkKZAHkZ6eTkzMFnS6+UAwYAcE
o9PNY/v2rSxcuJBt27bh5ubGggULaNKkCWlpaUBhjeySDSwTEhL09l/yoUFJ92qEWb9+fdLT0/ns
s8/QarW89tprd31gUBlyc3Pp2fN5XFxc8Pf3x9nZmZ49n+fq1at33U6tVvP999+XuzwrKwu1Ws2R
I0cAiIuLY/fu3fz999/3HFNcXBxqtVov2FpZ7jXuf5uizxVAr169HlkQGwpL73Tp0oWAgAACAgLo
169fsTrdhUoGQ2Vw9PFTqVTY2tqiVst/wj4J1apVw93dXQlc7969mzfeeIOkpCRu3LjBuXPnyMzM
xNvbm48++ojBgwczbtw4HBwc8PLyYu7cuURFRZGfn09OTg7m5uY8//zz2NnZ4eHhweuvv64cp2QJ
M5VKxaeffkrLli157733cHJywsPDg2XLlrFr1y69BrCOjo7MmjULJycnvfvG8OHDefnll3FwcODD
Dz/k+vXrHDx48LFeQ0mSJEmSJOnByf8LkCTpgZRsyFdQUFApdaKdnZ3x8/NjzJgxHDx4kMTEREaP
Ho1Wq62sod+3CxcuMHjwYFxdXQkLC2PAgAF8/vnnwIMHWsuSmZl557suJZZ4A3Dy5Enat29PeHg4
ycnJGBoaEh8fT/369cnMzCzVvLJhw4bKHioScKtII0xjY2NeeOEF5s6dy65du9i3bx+pqan3fa4V
kZWVhbW1NT/+uJfCDPVsYDU7duxn0KDBD73/4tekY8eOdOjQQe/hREW3fZyKNz+zt7dn/vz5T2Qc
j1plfq7KExoaqpcNbmFhQXR0NFevXuXMmTMMGTKEpKQkvTdBdDqdUv+7YcOG6HQ63N3dK21MVYmP
jw/jxo1j3LhxVK9eHRsbG71rde3aNUJCQqhRowZmZmb4+/vrBRqzs7Pp3bs3NWrUwNzcnObNm7Nt
2zZl2+DgYGxtbdFqtbi4uBAVFQWUfghVZO/evXh4eGBqakr79u05evToXcdfVmPbu709JP2ja9eu
SiD7p59+IjAwkCZNmhAfH09cXBx169bFwcGBlJQUIiMjsbCwUL569uwJwOnTp3nuuedo0KAB9vb2
hISE8NVXXykNjMuTkpJCbGys3j6bNm2KSqUq9jcUWrduXeb2zZs3V77XarVYWFhw6dKlh7wikiRJ
kiRJ0uMiA9mSJD2Qkg35srOzK60ZX2RkJPXq1aNr16689NJLvPLKK9ja2lbGsB/IwDES7wAAIABJ
REFUpEmTOH36NDdu3CAzM5M5c+ZgYmIClCwF8nCB1n+yP/eUWBIHwI4dO0hMTCQnJ4dvv/2Wy5cv
4+rqSnh4OB999BELFiwgIyODtLQ0IiMj9cquVOSBwr0aYUZFRfHFF19w9OhRTp8+zapVq9BqtXoB
88pUFJQoKJhKyQz1mJgtD5X9DvrXxMDAACMjI2U6Pz+fiRMnUr9+fczNzWnfvj1xcXF62w8YMOC+
g3CV6fDhw4wZM6bS9/s0qMzPVWWqjDcvniUrV67E0NCQQ4cOMX/+fCIiIli+fDkAQ4cOJSkpiR9+
+IH9+/cjhMDf3195g+PVV18lPz+fvXv3kpaWxscff4y5uTlQ2BS2qLnuL7/8wqJFi+5aSkQIweTJ
k/nkk084fPgwNjY29O7du9y3RcprbPvBBx88isv0zPH29uann34iJSUFIyMjnJyc8Pb2ZteuXcTF
xdG1a1eg8C2fV155hSNHjihv+Rw5coT09HQaN26Mubk5ycnJrFmzhrp16xIeHo6Hh8dd33bJy8uj
d+/eevtMSUkhIyODLl3+eQhc3htIxcufQeHvknyAIUmSJEmSVIU8bJHtx/2FbPYoSdJT4sSJE3ca
FqwWIIp9rRKA0gzyfvj5+QuNpsadfWQLWCU0mhqiY8cuomfPnqJWrVrC1NRUNGnSRHz22WfKdtHR
0cLT01OYmJgIa2tr0bVrV7FhwwYhRPlN6Uo2exTi7o0wN2zYILy8vET16tWFhYWF6NChg9i1a9c9
z6mgoEB8+OGHwt7eXpiamooWLVqIdevWCSGEuHr1qggKChI2NjbC1NRUODs7i8jISCFEYWOuwuur
uvPlc+f6bhKAqFatmrC0tBTe3t4iKSlJ75gqlUosWrRI9OrVS5iamgoHBwflmEXXpGTDOEC8+uqr
QgghBg4cKGrUqCEsLCyEVqsVtWvXFkZGRuLkyZPKuq1btxZubm7C1NRUNG3aVHz11VdCCCFee+01
0bJlSxERESGaNWsmjIyMRJ06dcSMGTOETqdTxpCRkSE6d+4sTExMhJubm/jxxx/1mgmWpWST1WfR
o/hcPazymrBWRtPJqqpr167Czc1Nb97UqVOFm5ubyMjIECqVSuzfv19ZduXKFaHVapXPobu7u5g5
c2aZ++7du7cYOXJkmcvKa/b4zTffKOvk5uYKrVarzLvfxrbS3V29elVoNBoxbNgwERQUJIQQYv36
9aJ9+/aiSZMmYunSpUIIIYKDg0X37t0rvN/r168LQ0NDsX79eiGEED169BDjx4/XW+ftt98WTZs2
1buXllTefbKs+2v16tVFVFRUhccoSZIkSZIk3b/KbPYoM7IlSXrqVJWsx4qUArlf0dGr6d7dCxgC
NACG0L27F5s2bWDr1q1cuHCBGzducPz4ccaOHatsN3DgQJKSkrh58yaXL19m165d9OnTByi/BMLQ
oUPJzc3Vm/fcc8/x008/kZeXx9WrV0lISGDkyJEA9OnTh4SEBK5evcoff/xBfHy8knl3Nx9++CGr
V69myZIlHDt2jAkTJjBkyBD27NnDO++8U27m5TfffHNnD28CF4Dv7kzvU5YfOHAAZ2dn/P39uX79
ut5xp0+fTv/+/Tly5AjBwcEMHDiQEydO3HO8OTk5rF27Fnd3d/bv38/Ro0dZvnw57u7urFixQlnv
4sWLLF68mKSkJGxsbPjss8+U7evUqcOMGTOYMmUK6enprFq1Si/jUwhBv379MDEx4dChQyxevJgp
U6bc1xsMJUuLqNVqli9fTmBgIGZmZjg7O7Np0ya9bdLS0vD398fCwoLatWsTEhLClStXKnzMx+FR
fK4e1tOaIf6keXl56U23b9+ejIwMjh07hqGhIW3btlWW1ahRAxcXF44fPw7A+PHjee+99+jUqRPv
vvuuXomisWPHEh0djaenJ1OmTClV778klUqlNxYrKyu9Y5WUkpLCzJkz9cpTjB49mosXL/LXX3/d
93X4t6levTrNmzdn9erVyt8Ab29vEhMTSU9PV+YV/ezGjRtHSkoKJ0+eZOPGjYwbNw6AzZs3s2DB
AlJSUsjOziYqKgohBE2aNAFKlzADeO2118jNzWXgwIEcPnyYU6dOERMTw4gRI2TzVUmSJEmSpH8B
GciWJOmp8Tjq4lame5UCcXR0vO99WllZsW3bZtLT09myZQvp6els27YZKyurhxvsQ3rQhwv5+fl8
9NFHfPHFF3Tv3p1GjRoREhJCcHAwn3/+OTk5OXh6euLp6UmDBg3o1q0bzz//PPBPjVO1+lNgO/An
sBqN5nP8/Pzp0aMHLi4uLF68mBs3bpQq/fHyyy8zfPhwpf5t69atWbBgwT3HnJqaihCCffv20a5d
O5o3b86AAQM4cuSIEmRVqVScO3eOqVOnsmbNGgYMGMC+ffvIz89n7NixbN26Fa1WS2pqKufOncPX
15eZM2eyePFiAH788UclwN2sWTM6derEhx9++NCBmJkzZzJw4EBSU1Px9/cnODhYaZT6+++/4+vr
S6tWrUhKSiImJoZLly4xYMCAhzpmZXsUn6uHcbcmrJVR4ubfRAihPKwZOXIkp0+fJiQkhLS0NNq0
acPChQsB6NmzJ9nZ2UyYMIHz58/j6+vL5MmT7/t45T0YuldjW+neunbtSkFBgRK0trKywtXVlTp1
6iif0ebNmxMXF6eU/WjZsiXvvvsu9erVAwoD4t999x2+vr64urqyZMkS1qxZowSyyyphVqdOHeLj
4ykoKMDPzw93d3feeOMNrKyslJ93eT/3yip/JkmSJEmSJD1BD5vS/bi/kKVFJOmZ9U9ZjdV3ymqs
FhpNDeHn5/+kh1auunXrCTAsVQqkvDHfq3TE0+ZhSyocPXpUqFQqYWFhIczNzYWZmZkAhJGRkfDy
8hLbtm0TWq1WtGjRQkyePFns27dP2baohECHDp30jt+1q68YMmSIcHJyEpaWlsLc3FxoNBqxaNEi
ZVuVSiVWrVqlN5YJEyaIbt266e27rNIia9euFRqNRhgaGopWrVqJ8ePHiy1btojMzExx8eJFsXv3
bqFWq0Vqaqr4/PPPxYsvvigMDQ2FSqUSOTk5QgghatasKYyMjISBgYEAhKGhoTA1NRUajUbcvHlT
zJs3TzRu3FhvfL///vt9lRZp1KiRmDdvnt45h4eHK9PXr18XarVaxMTECCGEeP/990XPnj319peT
kyNUKpXIyMi4+w/yMSuvxM6TuBds2bLlzu9edolSJ9kCEFu2bHnsY3oaVKS0SEJCgrLs8uXLQqvV
im+//bbM/b355pvCw8OjzGWff/65sLS0FEJUvLSImZmZUsakZGmRjh07ilGjRj3AWUuSJEmSJEmS
dL9kaRFJkp45VTXrMSFhH76+XSlZCiQ6evWTHVglediSCnl5eQBs2bKFlJQUtm7dikqlYv369axb
tw4/P797Zl4uWrRQL0Pd2NiAEydOsGDBAhISEkhJSaFGjRrk5+ffczwqlYqsrCwaNWpU7jqenp4U
FBTw9ddfM2bMGH799Vf69u3L1q1b9ZqONmjQgDFjxrBu3TqGDBmCEEJpGnb9+nU++OADTpw4wfvv
v4+JiYmS8WlsbKyXmVp8bA+refPmyvdarRYLCwsuXboEFJZTiI2N1Sun0LRpU1QqVbFyHk+H8krs
PInP1dOWIf40ycnJYeLEiaSnpxMdHc2nn37K//3f/+Ho6EifPn0YPXo08fHxpKSkMHjwYOzs7JSS
RxMmTGD79u2cOXOGpKQkdu3ahaurKwDh4eF8//33ZGZmcvToUX744QdlWXlmzpxJbGwsaWlpDBs2
DBsbG+VYJd2rsa30bKoqZcskSZIkSZKk8hk86QFIkiRBxeriOjk5PdYxVUSDBg3YsWM7GRkZnDx5
EkdHx6dynA+i6OFCYRA7+M7cYHQ6QUzMEDIyMu55rq6urhgbG5OVlUWnTp3QaDQA1K9fX3m93Nra
mpCQEEJCQujUqROTJ09m9uzZGBkZAaDT6XByclKOtW/fPhYtWoSfnx9QGEy7fPlyqWPv37+fwYMH
6023bNmyzCBycU5OTgQHBxMWFsacOXOYM2cO5ubmfPDBBzg4OKDVahFCsHPnTjw9PcnNzeXQoUPK
PsPDw2nUqBGHDh2iV69eHDhwgGbNmuHg4KB3XbKzs7l48SK1atVSzuthg9mGhoZ60yqVSgmu5+Xl
0bt3b2bPnl2qhEmdOnUe6riVrajEztPwuXJ2dsbPz58dO8aj0wkK70lxaDShdO/u/8x83h9ESEgI
N2/epG3bthgYGDBhwgRGjRoFQGRkJKGhoQQEBJCfn4+3tzebN29W7gE6nY7XX3+ds2fPUq1aNXr1
6kVERAQARkZGvPXWW5w5cwZTU1M6d+5MdHS0ctyyHgLNmjWL0NBQTp48iaenJ5s2bcLAoOx/5vbo
0YMffviBmTNnMnv2bAwNDWnSpIkydunZkpubS1DQkDt/zwr5+fkTHb36iZftkiRJkiRJku7Tw6Z0
P+4vZGkRSXomnThx4s6rJqtLvL6/SgAiPT39SQ+xTMOGDRP9+vUTQpQu9SCEEC1atBAzZsxQpouX
jujWrZt4/fXX9db/7bffhJGRkdi1a9ejHXgFPGhJhW3btolOnTqJ6tWrC2tra+Hk5CRq1KghoqKi
xJ49ewQgpk6dKqKiosTQoUMFIFasWCGaNGki1Gq1sLS0FJcuXRKbNm0SKpVKGBsbi8DAQHHx4kUh
hBAtW7YUzz33nAgODhZWVlZCpVIJtVotwsLClDGoVCphYmIiLCwshLGxsahRo4bQaDTil19+ESqV
SqhUKqVUiY+Pj15pESGEGD9+vBg8eLCws7MThoaGwtDQUNjZ2Ym0tDRlXQcHB2Fqaipq1aolevfu
LVQqlcjKyhLvv/++0Gg0AhBarVb4+vqKHTt2iDVr1ohp06YJIYQoKCgQbm5uokePHiIlJUXs2bNH
tG7dWqjV6ocqLVJyWyMjI9GqVSshhBBvv/22aNq0qdDpdPf7q/Cvl5ub+1Aldp5FxX8XJelpVhXL
lkmSJEmSJD1LZGkRSZKeOUVZjxrNeAozgHMobOwXip/fs5n1OGrUKKKjo7l165Yyb9WqVdSvX19p
oPUkPWhJhevXrxMWFkZiYiKxsbG4urpiYmLCrFmz6N69OwB79+7FwcFByZgcOXIkFy5coGvXrlhZ
WfHyyy+zcOFCwsPDsbKy4rvvvqNDhw4ALF++nCNHjvDVV19hZmbG3Llz0Wq1LFq0SGlsCGBjY4Ob
mxsqlQpjY2MmT56Mi4sLBw8eLPwDqFYTGxvLd999B4Bareajjz4CCh/yHjhwgMuXL1OjRg2Cg4NJ
SUnBzc1NWTc5OZkbN25w4cIFZs6cqWSJvv3229jZ2TF27FhatmzJ/v37eemll5g7d65S0kSlUrFh
wwb++usv2rVrx5gxY/jwww8f/IdVAa+99hq5ubkMHDiQw4cPc+rUKWJiYhgxYkSpDG1J39PahFV6
cLLMxL9DVS1bJkmSJEmSJJVNlhaRJOmpER29mkGDBhMTM0SZ1727/zNTb7qkF198kXHjxrFx40Ze
euklAKKiohg+fHilHketVrNhwwZ69+59X9s9aEmFwMBAvemlS5dSq1YtfvzxR8zMzLC3t2fhwoW4
u7uj0+lYsWIFO3fuVIL3H3/8MW+99RanTp2iYcOGhIeHM3bsWLKyspRxXb16lejoaAYMGADAq6++
SqNGjVi+fDlhYWEEBARgY2PDsmXLSo3PxsYGlUpFcnIy7u7uAHh7e6PT6ZR15s+fX+51KbkugIeH
R6l5TZo04bPPPit3P46OjsTFxenNK7mPklQqlRIwv98a23Xq1CE+Pp4pU6bg5+fH33//TcOGDenZ
s2el1Of+Nyhe4ubfrqr+zsgyE/8uVbVsmSRJkiRJklQ2mZEtSdJT49+W9WhkZMTgwYP54osvAEhK
SiItLY2hQ4dW6nEuXLhAr169HmjbB2m6d/LkSYKCgmjcuDGWlpY4ODigUqnIzs4ud5viTQpr1aqF
VqulYcOGevOKmhZmZmZy+/ZtJUMbwMDAgLZt23L8+HEAxo4dS3R0NJ6enkyZMoWEhIQHOv/y+Pj4
MG7cOMaNG0f16tWxsbFh+vTpSpbn7du39db/5JNPcHd3x9zcnAYNGhAcHMz69evJyMjgxo0bWFpa
KpnhRdavX4+5uTnXr18H4OzZs9jY2PDFF19Qs2ZN3N3d9ZrZ3bp1i927d2NlZYWNjQ1Tpkxh0KBB
NGjQQFmncePGrFu3jitXrpCXl8fRo0f53//+V6nXRvp3iI2NVWpaVyUP28BWqlpks1ZJkiRJkqRn
iwxkS5L01HFycqJXr15VLktKrVaXKtFQvGxIWUaNGsWPP/7IuXPnWLFiBb6+vtjZ2VXamG7duoWt
rW2pJoAVVZGHCwUFBXrn/cILL3D16lWWLVvGwYMHOXDgAEII8vPzyz1O8fGpVKq7Ni0sOlbJjFBR
rIljz549yc7OZsKECZw/fx5fX18mT578QNegPCtXrsTQ0JBDhw7x4Ycf8uGHH+Li4oK/vz9nz55l
0aLPuXr1KgAajYYFCxYQHx9P7dp1+eqrrwgMDMTZ2ZnAwP7069ePFStW6O0/KiqKl19+GTMzM27f
vo2fnx+WlpbEx8cTHx+PhYUFPXv2VILmc+bMYeXKlURGRrJ3715yc3NZv3693j5lOQWpqlq3bh3u
7u5otVpq1qxJjx49uHnzJkIIZs6ciZ2dHSYmJnh6ehITE6Nsl5WVhVqtZv369Xh5ed0pM2EONEaW
mXj2/RvLlkmSJEmSJD3LZCBbkiSpktjY2HD+/Hll+o8//uD06dN33aZZs2a0bt2aJUuWEB0dzciR
Ix9qDEWZwhMmTMDGxgY/Pz/UajXff/89AB06dOCtt97S2+by5csYGRkRHx8PQH5+PhMnTqR+/fqY
m5vTvn17zp07pzxciIqKwsrKik2bNuHm5oaJiQk5OTlA4Wv76enpTJs2DR8fH1xcXMjNzX2ocyrJ
0dERQ0ND9u7dq8y7ffs2hw8fpmnTpso8a2trQkJCWLlyJXPnzmXJkiVAYSY83LuMx73Y2dkRERGB
k5MT3367gYICQ6A+hVmeNpw4cUbJ8hw/fjze3t5MmfIWSUkZwHjAmqJs0BMnMoiJieHChQsA/Pbb
b2zZsoURI0YAsGbNGoQQLFmyBFdXV1xcXFi+fDnZ2dns3r0bgHnz5vHWW2/Rp08fXFxcWLx4MZaW
lkDhz6Vnz+eVQLuzszM9ez6vBNol6Wl24cIFgoKCGDVqFL/88gtxcXEEBgYihGDu3Ll88sknRERE
kJqaip+fH7179y5WUqLQtGnTeP755+9MNQeCgII70/+UmZCePQ/yZpEkSZIkSZL0dJKBbEmSpErS
rVs3Vq1axd69e0lNTWXYsGFKM8O7GTlyJLNmzUIIQd++fR96HCtXrsTY2JiEhAQWL16styw4OJjo
6Gi9eWvWrKFevXp07NgRKGwKeODAAb7++mtSU1Pp378/vXr10gsM3bhxg9mzZ7N8+XKOHj2Kra0t
UJjBbW1tzZIlS8jMzCQ2NpawsLC71tO930aDWq2WsWPHMmnSJGJiYjh27BijRo3i5s2byoOA8PBw
vv/+ezIzMzl69Cg//PADrq6uANja2mJqasq2bdu4dOkSf/zxx30dv4iXlxfwTzMxIcYClygMZpsh
RKCS5bljxw46dOhwJxv0BrAUuAoEotPNY//+fTRu3JiVK1cChU0/GzVqRKdOnQA4cuQIGRkZWFhY
KF/W1tb8/fffZGZm8scff3D+/Hnatm2rjE+j0dC6dWtAllOQqrbz58+j0+no168fDRo0wM3Njf/8
5z9otVr+97//MXXqVPr374+TkxOzZs2iRYsWzJ07V28fkyZNUmrqF9ZLzgKKAteyzMSz7N9WtkyS
JEmSJOlZJgPZkiQ9Ej4+PrzxxhtPehiP1ZtvvkmXLl0ICAggICCAfv36FavPWaisgO6gQYMwMDAg
ODhYyRZ+GI6OjsyaNQtHR0ecnZ31lg0YMIBz584p2dcA0dHRBAUFAZCdnU1kZCTffPMNHTp0wN7e
njfeeIOOHTvqlb64ffs2ixYtwsvLCycnJ0xMTJTzW7t2LYmJiTRv3pywsDDmzJmjd+7326SwLLNm
zeLFF18kJCSE1q1bc+rUKbZv365kIBsZGfHWW2/h4eFB165dMTAwUAL4RWU+Pv/8c+rVq/fQDw/+
CfC7lVhSGBSLj48nICCAOnXq3Jm/HVh45/tbFGWD+vj4KNc4KipKycYGyMvLo3Xr1hw5coSUlBTl
Kz09XfnZQdnXMi8v704AfT4QjCynIFU1Hh4e+Pr60qxZM15++WWWLVvGtWvX+PPPPzl37pxevXyA
jh07KvXyizRv3lwpM6FWfwQIIBVZZuLfo6qWLZMkSZIkSZL+ce9UQUmSJKlcf//9N+bm5gBYWFiU
ynYeMmSI3nRZ5Sx+++03/vrrr4cuK1KkKAu3LDVr1qR79+58+eWXdOzYkdOnT5OQkMDSpUsBSEtL
Q6fT4ezsrJcpnZ+fT82aNZVpIyMjmjVrVuYxunXrRlpamt684udd/Htvb+9S12To0KGlGl6Gh4cT
Hh6uTBsbGzN37txSWZdF3n77bd5+++0ylwGMGDFCL1D8IPbv3w8Ubya2EXACioLJhdmeeXl5FBQU
8NFHH91p6JgN/FpsT4XZoCNHjiQqKooFCxZw7NgxQkJClDVatmzJ119/jY2NjfL7VlKdOnXYv3+/
klmv0+lITEykfv36d9boUmKLf8opyMCO9DRTq9Vs376dhIQEtm/fzoIFC5g2bRrbt28H7l4vv0hR
3f3o6NW89NIAYmN/BF4CoHt3f1lmQpIkSZIkSZKqAJmRLUlSpRs+fDhxcXHMmzcPtVqNRqMhOzub
tLQ0/P39sbCwoHbt2oSEhHDlyhVlu5iYGDp37oyVlRU1a9YkICCAU6dOKcuLmnZ98803dOnSBa1W
S9u2bcnIyODQoUO0adMGCwsL/P399fb7KOh0Oo4dO0ZCQgJubiUzcSvm9u3bxMfHM2LECFq0aIGH
h0eljM3MzOyuy4ODg1m3bh06nY6vvvoKDw8PpexGXl4eBgYGJCUl6WX+Hj9+nHnz5in7MDU1rZSx
Pi6PoslhTk4OEydOBMDdvQWwCfCisJlYHirVd/j5+dOlSxdu377Ntm3b6Ny5KyrVK8And/ayVskG
bdWqFf369WPSpEn4+flRt25d5VjBwcHUrFmTPn36sHfvXs6cOcPu3bsJDQ3l3LlzAISGhjJr1iw2
btzIiRMnePXVV7l27Vqx34c9Jc5AllOQqpb27dsTHh5OcnIyhoaG7Ny5k3r16unVywfYt2+fXr38
4kFtKysrvvvuG1QqFR9//LEsMyFJkiRJkiRJVYgMZEuSVOnmzZtH+/btGT16NBcuXOD8+fOYm5vj
6+tLq1atSEpKIiYmhkuXLvHyyy8r212/fp2wsDASExOJjY1Fo9HQr1+/Uvt/9913mT59OsnJyRgY
GBAUFMTUqVNZsGABe/fu5eTJk0yfPv2RnmNaWhpt2rShefPm/Oc//7nv7XNzc+nQoROdOnVi165d
JCYmPrbme3379uWvv/5i69atREdHExwcrCzz9PREp9Nx8eJFHBwc9L6K6mBXJY+yyWFISAg3b96k
bdu2nD2bjYODI7CcwmZil3FxaUR09Grc3d2JiIhg9uzZJCUdwtpaC+RS2GhujF7TsZEjR5Kfn18q
W9zU1JQ9e/bQoEEDXnzxRVxdXRk9ejR///031apVAyAsLIwhQ4YwbNgwOnToQLVq1QgMDMTc3Bw/
P380mvEU1sjOQZZTkKqSgwcP8tFHH5GYmEhOTg7ffvstly9fxtXVlYkTJ/Lxxx/z9ddfk56eztSp
U0lJSSE0NFTZvrw6/EWlkSRJkiRJkiRJqhpkaRFJkipdtWrVMDIyQqvVKsHPDz74gJYtW/Lee+8p
6y1btowGDRpw8uRJHB0dCQwM1NvP0qVLqVWrFseOHVMyhqGwaVf37t2BwizUoKAgYmNjleZ7RSUa
HiUPDw+uX7/+wNsHBQ0hKSmDwsBiF2APO3aMZ9CgwWzbtrmyhlkmrVZL7969eeedd/jll18YNGiQ
sszJyYmgoCBCQkKYM2cOnp6eXLp0idjYWDw8POjVq9cjHVtl029yWLnX2dDQkIiICBYuXKjMy8jI
UH6fiwfIQkND9QJr5a139uxZatasSe/evUsdz9bWVq9OeUkajYaIiAgiIiJKLbt69SqDBg0mJuaf
UjeynIJUVVSrVo09e/Ywb948/vjjDxo2bEhERAR+fn706NGDP//8k4kTJ3Lp0iVcXV3ZtGmTXn+C
smrHP0htfkmSJEmSJEmSniwZyJYk6bFISUkhNjYWCwsLvfkqlYrMzEwcHR2VTOoDBw5w+fJlCgoK
UKlUZGdn6wWymzdvrnxfq1YtAL16zbVq1eLSpUuP+IweXHp6OjExWygMrhZlQwej0wliYoaQkZHx
wFmCFQ3YBAcH88ILL+Dt7U29evX0lkVGRvL+++8zceJEfv31V6ytrWnfvj0BAQEPNKYn5VFe5/I4
OTlVaJ8l17t58ybnzp3j448/5j//+Q8GBg/25zk9PV35PBXfv5WVFdu2bS43gC5JT7MmTZqwdevW
MpepVCqmTZvGtGnTylzesGHDUnX4LS0ty+xXIEmSJEmSJEnS000GsiVJeizy8vLo3bs3s2fPLvWa
d506dQB44YUXsLe3Z9myZdStW5eCggLc3NzIz8/XW7+oaRf8E6QtOa+goOBRncpDy8zMvPNd5Tff
i42NLTWvrIBNr169yg3kaDSaUs0ViyurGeODGDNmDN9++y3Xrl0jOTkZd3f3h95ncf9c5+KBbB+g
sCb0w1znys7mnD17Nh988AFdu3Zl6tSp9719bm4uQUFD7gTuC/n5FWZcF69+suOMAAAgAElEQVT9
W9FAuyQ9S8p7wCNJkiRJkiRJUtUia2RLkvRIGBkZ6QVKW7ZsydGjR2nYsGGp2sumpqbk5uaSnp7O
tGnT8PHxwcXFpcyGjXcLIC5ZsoT69euXmt+7d29Gjx5dOSdWCf555b1qNd+rzIaJ27ZtY+XKlWzZ
soXz58/rZdRXln+uc2CJJWeBh7vOsbGxZZbweFDh4eHk5+ezfft2tFrtfW+vX0IlG1jNjh37GTRo
cKWNUZKqmkdZI1+SJEmSJEmSpMdPBrIlSXokGjVqxIEDB8jKyuLKlSu89tpr5ObmMnDgQA4fPsyp
U6eIiYlhxIgRCCGwsrLC2tqaJUuWkJmZSWxsLGFhYaUC12U17Sqa179/f65cucLx48eVZdeuXWP7
9u0MHvz0BPScnZ2rVPO9RxEMOnnyJHXq1KFdu3bY2tqiVlf+n6N/rvNU/rnOF1Gpdj2V1/lBFZVQ
0enmU5h5bkdhCZV5xMRsqZQHD9LTZcyYMVhbW6PRaDhy5MiTHs5TSz7gkSRJkiRJkqRniwxkS5L0
SEycOBGNRoOrqyu2trbcunWL+Ph4CgoK8PPzw93dnTfeeAMrKytUKhUqlYq1a9eSmJhI8+bNCQsL
Y86cOaX2e7ca0FZWVvj5+ZGQkKAs+/rrr7GxscHb2/vRnewDiI5eTffuXsAQoAEwhO7dvZ7K5nuV
HQwaPnw448ePJzs7G7VajYODAzExMXTu3BkrKytq1qxJQEAAp06dUrbJyspCrVbzzTff0KVLF7Ra
LW3btiUjI4NDhw7Rpk0bLCws8Pf318vkr1HDEmtrQ/65zsdp0KAO0dGree+998osZ9KiRQvefffd
Bzq3J6EipWqkZ0dlv80wY8YMPD09K2l0Tw/5gEeSJEmSJEmSnj2yRrYkSY+Ek5MT8fHxpeavW7eu
3G26detGWlqa3rzi5UnKatrl7e2tNy84OJhXXnmFixcvAvDZZ5/x66+/8scff1CtWrVyj21vb8+E
CRMYP3783U+sklSV5nuPomHi/Pnzady4MUuXLuXw4cOo1Wr27NlDWFgY7u7u5OXlMX36dPr160dK
Soretu+++y7z5s3Dzs6O4cOHExQURLVq1ViwYAGmpqb079+f6dOns3DhQgCMjY3p2LEDH3/8MSdP
nmTGjBl06NABKysrRowYwcyZM0lMTKRVq1YAJCcnk5aWxsaNGx/yyj0++qVqgostebpL1UgPpvjb
DJWlsmu+Pw0eZS8CSZIkSZIkSZKeDJmRLUnSMyUgIACdTsfmzZs5e/YsR44cYefOnUoQOyoqSq/5
XZHDhw8zZsyYxz1cnJyc6NWr11MbUHkU2b4WFhZYWFig0WiwsbHB2tqafv360bdvXxwcHHB3d2fp
0qWkpqZy7NgxvW0nTZpE9+7dcXFxITQ0lKSkJKZPn46XlxceHh6MHDmSXbt2lTpm0XU2NTVV5tWr
V48ePXqwYsUKZd6KFSvw9vamYcOG931eT0pVK1UjPbgHeZsB4Ndff2XQoEFYW1tjbm5O27ZtOXTo
EFFRUcyYMYOUlBTUajUajYaVK1c+obOrXFW1F4EkSZIkSZIkSeWTgWxJkqq84k0ITUxMCAwMZPXq
1URHR9O0aVN8fHyUdYUQZWYfWltbY2Ji8jiHXSU8rmDQyZMnCQoKonHjxlhaWuLg4IBKpSI7O1tv
vebNmyvf16pVC0CvtEKtWrW4dOlShY87evRooqOjyc/P59atW0RHRzNy5MiHPJvHryqVqpEe3Pz5
85k5cyb169fn4sWLHDp0iBs3bhAWFkZiYiKxsbFoNBr69eunbHP9+nW6dOnC+fPn+eGHHzhy5AiT
J0+moKCAgQMHEhYWhpubGxcvXuT8+fMMGDDgCZ5h5ZEPeCRJkiRJkiTp2SNLi0iS9MT5+PgowchV
q1ZhaGjI2LFjmTlzJlDYsHH8+PH88MMP/P3333h7ezN//nxq1KhBUNCQO6UvCmk0GurVq8f58+c5
evQonTp1Qq1Wc+3aNZKTkxk+fDgAarUalUpFeHg406dPL1VaJCcnh9dff53Y2FjUajU9e/ZkwYIF
2NraAoV1ZTds2EBYWBjvvPMOV69epVevXixbtgwzM7PHefkeqaJg0I4d49HpBIWZ2HFoNKF07155
waAXXngBe3t7li1bRt26dSkoKMDNzY38/Hy99QwNDZXvix5IlJxXUFBQ4eMGBARgbGzM+vXrMTQ0
5Pbt2wQGBj7k2Tx+VaVUjfRwSr7NAOgFrQGWLl1KrVq1OHbsGK6urnz55ZdcuXKFpKQkLC0tAXBw
cFDWNzc3x8DAQNnfsyQ6ejWDBg0mJmaIMq97d3/5gEeSJEmSJEmSqiiZkS1J0lNh5cqVGBoacujQ
IebPn09ERATLly8HYOjQoSQlJfHDDz+wf/9+hBD4+/szaNDgO00IW1AYYP0YIcyxtrahWrVqZGRk
0L17dyXg2aFDYa1kS0tLJftw4sSJZY6nT58+XLt2jZ9++okdO3aQmZnJwIED9dbJzMxk48aNbNmy
hc2bNxMXF8esWbMe4VV6Mh51tm9ubi7p6elMmzYNHx8fXFxc9Bo2FnkUdXw1Gg0hISF88cUXrFix
goEDB1bpzPynvVSNVPnu9TZDSkoKnp6eShD736ToAU96ejpbtmwhPT2dbds2l1leSpIkSZIkSZKk
p5/MyJYk6algZ2dHREQEUBiMO3LkCJ988gne3t5s2rSJhIQEpbnZl19+Sf369cnIyKDwlfHZgC8w
mYKCuiQnDyE9PR0nJyfi4uKUYxgaGlKrVi3UavVdsw9//PFH0tLSOHPmDHXr1gUKM8Xd3Nz0GgMK
IYiKikKr1QIwZMgQdu7cyXvvvffQ1+P27dsYGDwdt+hHne1rZWWFtbU1S5YsoXbt2mRlZfHmm2+W
ClwLIUptW9a8+zVq1CiaNm2KSqUqs0FpRWVlZWFvb8/PP/+Mu7v7Q49LkiriXm8zFK8L/2/l5OQk
H+5UgFqtZsOGDfTu3bvM5fIeJ0mSJEmSJD1pMiNbkqSngpeXl950+/btycjI4NixYxgaGtK2bVtl
WY0aNZQAc2ETwvHAe0AnIBEovwnhsmXLyMvLA9Brkpadnc2SJUs4deoUv/zyC3Z2dty6dQu1Ws36
9et57bXXEEIQGBjI/v37AWjUqBH//e9/8fT0BKBOnTpcunSJefPmYW9vrxzz8OHD9OjRAxsbG6pX
r07Xrl1JTk7WG5darWbx4sX06dMHCwsL3n//fZycnJTgfpGff/4ZtVrN6dOn7+PqVo5Hle2rUqlY
u3YtiYmJNG/enLCwMObMmVPmehWZd69jleTo6EiHDh1wcXGhTZs297W/hx2PJD2MirzN4O7uzs8/
/8y1a9fK3IeRkRE6ne5xDFd6yl24cIFevXrddR15j5MkSZIkSZKeJBnIliSpSjIyMrrz3R5gJHAa
CAEKM2p37dp1z31cv35daZJWu3ZtVCoV/fr1K9UQctq0aUyePJlq1apRu3ZtgoKCEEIotZmL1i1e
n7n49n/++SfDhg0jPj6eAwcO4OzsjL+/P9evX9cbz4wZMwgMDCQ1NZVRo0YxYsQIVqxYobfOihUr
8Pb21guUV0WhoaGcOnVKme7WrRtpaWncuHGD5ORkOnfujE6nUzIDGzZsiE6n08sC9Pb2RqfTUa1a
NWXe0KFDyc3NVaZXrFjBd999p0zHxsaWejgAcO7cOUaNGvXQ51UZGeKSVFHF32bIzMwkNjaWsLAw
vfvPoEGDqFWrFn379mXfvn2cPn2a7777jgMHDgCFD+ROnz5NSkoKV65cKVWXXvr3sLW11es5UBZ5
j5MkSZIkSZKeJBnIliTpqVCU5VwkISEBJycnXF1duXXrlhJ0Abhy5QpZWVm0aNESlep1CsuLFABa
4CSgYfHixWUeR61WK/8jHhgYSN++fXFwcMDIyIhBgwaRmpqKmZkZ2dnZXLhwAYBJkybRoEED/vzz
TyZPnkxWVpZesPRefHx8CAoKwtnZGRcXFxYvXsyNGzf0yp4ABAcHM3ToUBo1akT9+vUZPnw4J06c
4PDhw0BhuZHo6GhGjhxZ4WM/q4QQzJ49GycnJ0xMTGjUqBEfffQRAFOnTsXFxQUzMzMaN27M9OnT
9TJOZ8yYgaenJ//973+xtbXFxMSEM2fO0L9/f2Wd4tn6NWvWJCAgQC/wDnDw4EFatmyJqakpbdu2
JTk5WS+AWFBQwKhRo3BwcECr1dKkSRPmz5//iK+M9G9SkbcZDA0N+fHHH7G1teX555/H3d2djz/+
GI1GA8CLL75Iz5498fHxwdbWljVr1jyJU3nqDB8+/KEbv8bFxaFWq/njjz8qaVT3tm7dOtzd3dFq
tdSsWZMePXpw8+bNCr8Z9P333yvT97rHSZIkSZIkSdLj9nQUYJUk6V8vJyeHiRMnMmbMGBITE/n0
00/55JNPcHR0pE+fPowePZrFixdjbm7O1KlTsbOzY9GihbRv35HCJoRFOgLn+PPP03dqaOtnkJmb
m3P79m1iY2MxNzdnzpw5JCYmkpWVxYwZM1CpVNSrV4/mzZsTGhqqZGcPHToUHx8ffH19EUKUyqa+
m0uXLvH2228TFxfHpUuX0Ol03Lx5U2nGVqSo9naR2rVr4+/vzxdffEHr1q35/vvvyc/P56WXXrrf
y/vMmTp1KsuXL2fu3Ll07NiR8+fP88svvwBQrVo1Vq5cSZ06dUhNTWX06NFUq1ZNaex58+ZNUlPT
mDx5srI/AwMDIiIilCBgUba+u7s7eXl5TJ8+nX79+pGSkgLAjRs3CAgIwM/Pjy+//JLTp08zfvx4
vTEWFBRgZ2fHunXrsLa2Zt++fYwZM4a6devKn6H0wEJDQwkNDVWmi95mKK5kqRA7Ozu+/vrrMvdn
ZGRU7rJ/s/nz51dK9vHjDPxeuHCBoKAg5syZQ9++ffnzzz/56aefEEIobwZ9+umnCCH43//+h7+/
PydPnsTMzKzUvipyj5MkSZIkSZKkx01mZEuS9FQICQnh5s2btG3blnHjxjFhwgSl1ENkZCStWrUi
ICCAjh07olar2bx5M1evXqUwEzsQqAuYUJiR3Rr4p0528UCCra0t9vb2DBgwgHbt2pGcnMyyZcuo
V68eYWFhCCHIz89n48aNWFpaAjBu3DgcHR1Zs2aNsq+iAEfxDO8it27dKnVuR44cYcGCBSQkJJCS
kkKNGjVKvcJfVjBh1KhRrFmzhr///pvIyEgGDBiAiYnJA1zhZ0deXh7z58/nv//9L4MHD8be3p4O
HTowYsQIAN566y3atWtHgwYNeP755wkLC9ML1K1b9x063W1gOZANrEanM2D58uXKOsWz9d3d3Vm6
dCmpqakcO3YMgNWrVyOEYNmyZTRt2hR/f38mTZqkN04DAwPCw8Np2bIlDRs2ZNCgQQwbNqzSgoY+
Pj688cYbANjb2z9wtnfJLEzp3yE9PZ2tW7cqD/ykQgUFBQghsLCw0CtbVBWcP38enU5Hv379aNCg
AW5ubvznP/9Bq9VW+M2gIhW5x0mSJEmSJEnS4yYD2ZIkPRUMDQ1ZuHAh165d4/Lly8ycOVNZZmlp
SWRkJLm5ueTl5bF582YaN25M48aN76wRCPwK3AQuAIV1lR0dHcuso9yiRQtOnDiBSqUiMjISHx8f
cnJy8Pf3V9apX78+S5YsQa1Ws3fvXqKjo7GxsVGWDxs2jKSkJGxsbJQSJEV1n0u+rr1v3z7Gjx+P
n58fTZs2xdDQkMuXL1fouvj7+2NmZsZnn33Gtm3bZFkR4Pjx4+Tn59OtW7cyl69du5ZOnTpRp04d
LCwsmDZtmpL9np6eTmZmBlAfGAHYAcEI8SLXrl1TgnonT54kKCiIxo0bY2lpiYODAyqVStnPL7/8
gru7e7Fa7YUNSktauHAhrVu3xtbWFgsLC5YsWVIqE78yHD58mDFjxijTZQWni0qqSP9uubm59Oz5
PC4uLvj7++Ps7EzPns/feTBY9fj4+DBu3DjGjRtH9erVsbGxYfr06cry/Px8Jk6cSP369TE3N6d9
+/Z6wduoqCisrKzYtGkTbm5umJiYkJOTU6q0SH5+PuPHj6dWrVqYmprSuXNnpexTkS1btuDi4oJW
q8XX15czZ8488vMvzsPDA19fX5o1a8bLL7/MsmXLlCafly5dYvTo0Tg7O1O9enUsLS25fv16ufej
it7jJEmSJEmSJOlxkoFsSZKqLGdnZ/z8/NFoxlNYJzsHWI1GE4qfnz9OTk7lbluRJmlw98ZW6enp
qNVqfvvtN2bPns2pU6dYuHAh27Zt01vPycmJVatW8csvv3DgwAEGDx6MVqut0Dmq1WqGDh3Km2++
iZOTE1OmTFGycCtbVQl0mpqalrts//79DB48mBdeeIHNmzfz888/8/bbbyvZ75mZmXfWrF5iS0fg
nyz+F154gatXr7Js2TIOHjzIwYMHlWx9oFRD0LKsWbOGSZMmMXr0aH788UdSUlIYPnz4I2mmZ21t
XaFMfVnfVgoKGsKOHfspvGcWvpGwY8d+Bg0a/IRH9uBWrlyJoaEhhw4dYv78+URERChvWLz22msc
OHCAr7/+mtTUVPr370+vXr2K3QsKy2jMnj2b5cuXc/ToUb2HlkUmTZrE+vXrWbVqFcnJyTg6OuLn
56cEis+ePcuLL75Inz59SElJYdSoUUydOvXxXIA71Go127dvZ9u2bbi5ubFgwQKaNGnCmTNnKvxm
UJGK3OMkSZIkSZIk6XGTgWxJkp64h/mf5ejo1XTv7kVhnewGwBC6d/ciOnr1PY+5Zs2auzZJK29s
KpWKiROn4OLiwiuvvIJOpyM8/F08PDw4fPhwqdevv/jiC65evUrLli0ZOnQooaGh2Nra3vM4RUaO
HEl+fv5jycauCoGLogaPO3fuLLVs3759NGrUiKlTp9KyZUsaN26slxX5Txb/nyW2LAxqOTo6kpub
S3p6OtOmTcPHxwcXFxeuXLmit7arqyspKSl6QaCEhIRSY+nYsSOvvPIKHh4eODg46AXPKlPx0iL2
9vaoVCr69u2LWq3GwcGBqKgoZsyYQUpKCmq1Go1Gw8qVK8vc19mzZxkwYIDS6LJv375kZWU9knFL
j1d6ejoxMVvQ6eYDwRS9kaDTzSMmZkuVLTNiZ2dHREQETk5ODBo0iHHjxvHJJ5+Qk5NDZGQk33zz
DR06dMDe3p433niDjh07smLFCmX727dvs2jRIry8vHBycir1sOzGjRssXryYOXPm0KNHD5o0acLS
pUsxNTVVAuafffYZjo6OShPaolJCT0L79u0JDw8nOTkZQ0ND1q9ff99vBlXkHidJkiRJkiRJj5ts
9ihJ0hMXGxv7wNtaWVmxbdtmMjIyOHnyJI6OjnfNxP77778xNzcHwNfX965N0ho2bFiqaZqlpSXP
PdezWEbjRuA0t26dwtvbSwmOFM/E8/Dw4MCBA3r7Kf7KesnjlnT27FkMDQ0ZMmQImzZtKne9itLp
dGg0mofez5NibGzMlClTmDx5MoaGhnTs2JHffvuNo0eP4uTkRHZ2NmvXrqVNmzb88MMPbNiwQdnW
2dmZxo2dyMw8ReHPzxuIQ6X6DhMTU5ycnBBCKNn6tWvXJisrizfffFMvyB8UFMS0adMYNWoUb775
JqdPn+Z///uf3jiLMvG3b9+Ovb09q1at4sCBA/z5558cOXIEd3f3R3J9Dh06hK2tLVFRUfj5+aHR
aDA3NyctLY2YmBh27tyJEEKpAV/c7du38fPzo2PHjsTHx6PRaHj//ffp2bMnqampGBjIfzZUZf88
SOlSYok3UPhGwt3un08rLy8vven27dsTERFBamoqOp0OZ2dnvbdr8vPzqVmzpjJtZGREs2bNyt1/
ZmYmt2/fpkOHDso8AwMD2rZty/Hjx4HCUhzt2rUrNY7H6eDBg+zcuZMePXpga2vL/v37uXz5Mq6u
rjg7O7Nq1SpatWrF77//zuTJk+/6ZlBF7nGSJEmSJEmS9LjJjGxJkp4JTk5O9OrVq9wgjE6n49ix
YyQkJODm5nbf+1+3bh3u7u6YmpreyWisC6QA64AkdLqrxMRs4auvvgIKA9kuLi6YmZnRuHFjpk+f
rhesLirjsXr1auzt7alevTqDBg3i+vXryjqHDx+mY8eOdO3aFY1Gw6pVq0qN68svv6RNmzZUq1aN
OnXqEBwczG+//aYsj4uLQ61Ws23bNlq3bo2JiQnx8fEAzJo1i9q1a2NpacmoUaP466+/7vu6PCnT
p08nLCyM8PBwXF1dGThwIL/99hsBAQFMmDCBcePG4enpyf79+/Xq5QK89FIgFhZmFM/id3FpqGTJ
q1Qq1q5de9dsfTMzMzZt2kRaWhotW7bknXfeYfbs2XrrvPLKKwQGBjJw4EC8vLzIzc0lJCTkEV6V
QkUBOktLS2xtbbG2tsbY2Bhzc3MMDAywsbHB1tYWY2PjUtuuWbMGIQRLlizB1dUVFxcXli9fTnZ2
Nrt3737kY5cerX/eSNhTYklhzWhHR8fHOp5H7fr16xgYGJCUlERKSorydfz4cebNm6esd7dyRfBP
iamySk8VbwD8pN9oqVatGv/P3r3H5Xj/Dxx/3fdddC46OCUkURGFSE4lypnZbE6b4w4m5mybQ/Gd
sMnmsN/mMI3mNAybxBzSHBpC5VA3UZmJVjFJ4u7z+yNduh3GJufP8/G4H9/uz+e6Ptfnuu779tj3
fX2u9zsmJoaOHYtyoE+ePJmwsDACAgJYvHjxv3oy6FH+jZMkSZIkSZKkp04I8UK9AE9AxMXFCUmS
pEd19OhRYWJiIjp37iwuX778r/a9cOGCMDQ0FF999ZUIDw8XgIDPBFwT8KaADgKOCED8/PPPQggh
PvvsMxEbGyvS0tLEL7/8IipVqiQ+//xzZczg4GBhbm4uXn/9dXHixAmxZ88eUalSJTFx4kSRlZUl
AgI63D5O0atx4yYiMDBQmJubi5EjRyrjLF26VERFRYmzZ8+K33//Xfj4+IiOHTsq/dHR0UKlUokG
DRqI7du3izNnzoicnByxevVqYWRkJJYuXSq0Wq2YOHGisLCwEB4eHo95pV8cWq1WREZGCq1W+9SO
mZqaKlQqlYiPj3/ssVq3bq18F6pXry6++uorpU+lUomNGzfqbR8cHHzfz7fktmPHjhUGBgbCzMxM
76XRaMQ333zz2HN+lURFRYnmzZsLKysrYW1tLTp16iRSUlKEEHe+B2vWrBEtWrQQxsbGonHjxkKr
1YoDBw6IRo0aCTMzM9G+fXvx119/KWMWFhaKkJAQYW9vL8qWLSsaNGggoqKilP7icdevXy98fX2F
iYmJqF+/vti/f7+yTUBAB6FSmQiwFmAioJFQqUyEgYHB07s4pah169bCzc1Nr23ChAnCzc1NnDp1
SqhUKrFnz54H7h8eHi7KlSt3T3v//v1F9+7dhRBCXLt2TZQtW1asXLlS6b9586awt7cXYWFhQggh
PvnkE1GvXr175qFWq8WVK1f+8/lJkiRJkiRJ0osuLi6uOLbhKR43Lvy4AzztlwxkS5L0tB0+fFio
1WqRnp4ukpOTb/8DHCFACOgvoLuA5QJ4YFD0iy++EI0bN1beBwcHCzMzM3Ht2jWlbdy4ccLb21sE
BHQQanU5AYYCvhUQITSa8sLPr60wMTHRC2Tf7eDBg0KtVivjFgeyiwPsxZo1ayaCgoL02po2bfpK
BbKfpMLCQjFz5kzh5OQkypYtK6pVqyamT5/+SIHGrKws0atXL2Fvby9MTExEvXr19AJoQhQF76pU
qSIaNWokypcvLzQajQgMDFT6VSqVWLBggfDx8RFGRkbCzc1NvP322wLQC3CfO3dOAMLU1FRYW1uL
6tWrCw8PD3HmzBmRkpKi9/r777+f/IV7iaxbt0789NNPIiUlRcTHx4uuXbsKd3d3IcSdgLOrq6v4
9ddfRVJSkvD29haNGjUSfn5+Yv/+/eLo0aOiVq1aYujQocqYYWFhwsrKSqxZs0ZotVoxfvx4UaZM
GXH69Ol7xt2yZYs4deqUeOONN0SNGjWETqcTQggRGRkpVCqV3o0yQ0NDYWVl9fQvUilo3bq1sLCw
EKNHjxbJyclixYoVwszMTCxatEgIIUTfvn2Fo6OjWL9+vXLDLzQ0VERGRgohHi2QLYQQH330kbC3
txdRUVHi+PHj4p133hHW1tbKjdH09HRhZGQkxo4dK5KTk8UPP/wgKlWq9EIHspOTk5/6zT5JkiRJ
kiTp5SMD2TKQLUnSU6TT6UTbtm2FhYWFeOONN4SbWz2hVlvdDl6/IaCR0GjKi4CADso+q1atEj4+
PqJixYrCzMxMGBkZiQoVKij9wcHBom7dunrHmTNnjnBwcLj9D/x0AWoB524HzIsC5a6urnqB7EOH
DonOnTsLBwcHYW5uLkxNTYVarRYnT54UQhQFstVqtfjzzz/1jlWuXDmxfPlyvbaRI0fKQHYpGTdu
nLC2thazZs0S3333nVi1apVYsmTJIwUaz58/L2bPni0SEhLE2bNnxfz584WhoaE4cOCAMn7r1q2F
gYGB8Pb2FqdPnxY2NjZCpVKJ7du3CyGEMDQ0FFWqVBGBgYEiMTFR7N27V1StWlUvkH3z5k3h6uoq
ADFv3jyRlJQkmjZtKjQajcjJyXn6F+0ld+nSJaFSqcTx48eV78HSpUuV/lWrVgm1Wi2io6OVthkz
ZggXFxflfZUqVcSMGTP0xvXy8hLDhg0TQoj7jnvixAmhVqtFcnKyEEKIt956S3Tu3FnviYS+ffve
N5j7ImjdurUYNmyYGDp0qLC0tBTW1tZi0qRJSv+tW7dEcHCwcHR0FGXLlhWVK1cWPXr0EMeOHRNC
PHogOz8/X4wYMULY2dkJY2Nj0aJFi3v+W3Tz5s3C2dlZGBsbi1atWonw8PAXMpB9v6eCAgI6iOzs
7Gc9NUmSJEmSJOkFVJqBbJkjW5Ik6SHUajXbtm0jKirqdn7tQgwM8srzVGcAACAASURBVCjKsfwj
cAh//6asXBkBQGxsLH379qVTp05s3ryZo0eP8umnn1JQUKA3rqGhod57lUpVYhvP4tbb/1tUjO3G
jRvK9nl5eQQGBmJlZcWKFSs4dOgQP/30E8A9xzI1Nb3nvJ51PteXVW5uLnPnzqVSpcqMGzeOgQMH
8tZbb7FmzTquXLkCwNixYwkMDMTJyYmQkBDS0tI4ffo0AJUrV2bUqFHUq1eP6tWr8+GHHxIQEMCP
P/6odxxTU1OaNm1KzZo1MTMzw8HBgR07dgBgZ2fHhQsX+OKLL7C3t6dZs2b069cPgLNnz5KVlUVE
RARCFOX1dXBwoHbt2kRFRVFYWIivry979uwhNTWV6OhoRowYwZ9//vkUr+KL7/Tp0/Tu3ZuaNWti
aWmJo6MjKpWK9PR0ZZt69eopf1eoUAFAr+hghQoVuHTpEgBXr17lzz//1Cs4CODj46MUHLzfuJUq
VUIIoYyTnJyMl5eXXl0BLy+vUjrrZ8PQ0JAFCxZw+fJl/vrrL6ZOnar0aTQapkyZQkpKCvn5+Zw/
f561a9cqtRLeeecdsrOz7xlz6dKlrF+/XnlftmxZvvzySy5evEheXh4xMTF4enrq7dOhQweSk5PJ
y8sjOjqad955B51Oh4WFxRM68yejd+9+JQoapwMRbN8eS69efZ/xzCRJkiRJkqRXnQxkS5IkPSJv
b2+mTJlCQkICdnZ2fPLJJ7Rv3542bdoQFbWZcuXKAbBv3z6qV6/OhAkT8PT0pGbNmqSmpj7SMQwM
DG7/9QdgAMTefl9UjO3ChQvKtklJSWRnZxMaGoqPjw/Ozs5cvHjxkY7j4uJCbGysXtvd76X/5uTJ
k+Tn53PiRFEAqGQgKCjoI+CfA42FhYVMmzYNd3d3rK2tMTc3Z9u2bXoBUAAzMzPlZoRKpcLCwkIZ
o0OHDmg0Gjw9PZVg26hRowD49NNPsbOz48cff+TUqVMIIXjzzTcxNzfH3t4etVqNsbExPXr0wNXV
lSFDhnDjxo0XLhj3rHXq1ImcnBwWL17MgQMH+P333xFC6N1kKnkzq/izvLutsLBQb9x/Kjj4T+MW
j3O/7UXRE2/SY9JqtWzZsoVTp04966n8Z1qt9nZB47lAH6Aq0Aed7iu2bo18oc9NkiRJkiRJevEZ
PHwTSZKkV9uBAwfYsWMH7dq1w87OjtjYWP766y9atmyJmZkZCxcuRKvVYm1tjaWlJbVq1SI9PZ3V
q1fTuHFjfvnlFzZs2PBIxzI0NCQgoAPbt49Dp2sBjATiUKsXYGNTgfz868q2Dg4OlClThrlz5/L+
+++TmJjI//73v3vGvF+QasSIEQwYMICGDRvi4+NDREQEx48fp2bNmv/1Mkm3Fd9MKCwMoSgQBEWB
IEFMTD9UKtU/BhpnzZrFvHnz+Oqrr6hbty6mpqaMGDHinlX2PXv2ZPbs2QCcOXOG7t27K2O4ublR
rVo1vaBTmTJlUKlUrFixgi5dujB06FAaNWrEihUr7vmO2NraYm5uXmrX5GF8fX3x8PAgLCzsqR3z
ScrOzkar1bJkyRJ8fHwA2LNnz2ONaW5uTuXKldmzZw/NmzdX2vft20eTJk2U9w970qJOnTocOHBA
r+3gwYOPNbdn6Xl4siQ7O5vevfuxdWuk0hYQ0IGVKyOUG5wvipSUlNt/tbyrp+ipoNOnT1OrVq2n
OidJkiRJkiRJKiZXZEuSJD2EhYUFMTExdOzYkdq1azN58mTCwsIICAhgyJAh1K5dm0aNGmFnZ8e+
ffvo3LkzI0eOJCgoCA8PD2JjY5k8efIjH2/lygj8/ZsCO4BzQCiGhjcYNuxDGjZsqGxnY2NDeHi4
8pj8rFmzlMBmSfcL9PTs2ZNJkyYxfvx4GjVqxLlz5xg6dOh/uDrS3e6soL15V09RIOhhgbd9+/bR
tWtXevXqRb169ahRo8a/XgVZp04d0tPTyczMVNruDl56enpy6tQpbG1tcXR0VF63bt1iz549cuXl
YyhXrhzW1tYsXLiQlJQUdu7cyejRox/62T9sZfTYsWOZOXMma9asQavVMmHCBOLj4xkxYsQjjxEU
FERkZCRz5szh9OnTfPvtt0RFRT0XAeH/YufOnc/8BsjLlIrjzs3MmLt6ip4KcnJyeqrzkSRJkiRJ
kiQ9j5tk+2m/kMUeJUl6jrVu3VqvGOPjKFmMTXpxJCcn3y5kYSZgmYAUAbECBgtAqFQqER8fr2x/
+fJloVKpxO7du4UQQowaNUpUq1ZN7Nu3T5w4cUIMGTJEWFpa6hWeu9/3rFu3bmLAgAFCiKICpXXq
1BGBgYEiISFB7NmzRzRt2lSo1WqxadMmIYQQeXl5onbt2sLPz0/89ttv4siRI6Jx4ybPpMBbaf5u
nhc7duwQbm5uwtjYWDRo0EDExMQo1z81NVWo1Wq970FxYdaShQHvLkRYWFgopk2bJqpWrSrKli0r
PDw8xLZt25T++417+fJloVarle+XEEIsXrxYVK1aVZiamorXXntNfPbZZ6Jy5cpP6lK81O783iNu
F+YtfhUV6H0R//0OCOggNJryt88hXcDyewoaS5IkSZIkSdKjksUeJUmSXgEli7GVtpchl+vzytnZ
mYCADqhUOmA04Ap0QqX6gZYtfe+78rVk28SJE/H09CQwMBA/Pz8qVapE9+7dH7j9/ajVajZu3Mi1
a9fw8vLi3XffZdKkSQghMDIyAsDY2JiYmBgcHBzo0aMHDRs2vJ1iwg84ydNeVXrr1i2CgoKwsrLC
1tZW7ymGgoICxowZg729PWZmZnh7e7N79269/ffu3Yuvry+mpqaUL1+e9u3bK8U1CwoKGD58OBUq
VMDY2JgWLVpw6NAhZd/du3crRV09PT0xMTHB39+fzMxMtmzZgqurK5aWlvTp04f8/HxlPyEEoaGh
ODo6YmJigoeHB+vWrQPAz8+PY8eOkZeXx5EjR2jRogU6nY7OnTtTrVo1dDod7u7uylitWrW6pzDg
3YUIVSoVEydOJD09nfz8fA4fPkzbtm2V/vuNa2lpiU6no2XLO6kiBg0aRHp6Orm5uaxbt46zZ8/K
lbb/0aOk4njR3HkqqB/gAPTTK2gsSZIkSZIkSc+KzJEtSZL0CnmZcrk+z1aujKBXr74lrvMN2rW7
/3UuDjQWK1euHOvXr//H8Xfu3HlP208//aT33tnZmZiYO+kB9u7di0ql0gtY2tnZsXTpUrRaLbVr
16YoNUJxXu866HSCrVv7cerUqSeeFzc8PJzBgwdz8OBBDh06xJAhQ6hWrRqDBg3iww8/JCkpiTVr
1lCpUiV++ukn2rdvT2JiIjVr1uTo0aP4+/szePBg5s6di4GBAbt27VKu69ixY/npp59Yvnw5Dg4O
zJw5k4CAAFJSUrCyslLmEBISwtdff42xsTFvvPEGPXv2xMjIiFWrVnH16lW6devGvHnzGDt2LADT
p09nxYoVLFy4ECcnJ2JiYujXrx92dna0aNHiiV6v/0qr1fL555/TpUsXXF1diYyMZPny5fzf//3f
s57aC0k/FUefEj0vbiqOcuXKERW1mVOnTnH69GmcnJxkXmxJkiRJkiTp+fC4S7qf9guZWkSSpOdY
69atxYgRI8S4ceNE+fLlRcWKFUVwcLDSn56eLrp06SLMzMyEhYWF6Nmzp7h48aLS379/f70UEkII
8dFHH4nWrVsr73/88UdRr149YWxsLKytrUXbtm1FXl6e0r9o0SLh4uIijIyMhIuLi/j666+VvjuP
jEfcfmQ8Qj4y/gRptVrRp08f4eLi8tBtVSqV2LhxY6kdu27duqJHjx4iNTVV/Prrr8LNzU20bNlS
6U9OTlZS10RGRt5+1Cv9rvQI6QIQkZGRpTav+2ndurVwc3PTa5swYYJwc3MT6enpwsDAQFy4cEGv
39/fX3z66adCCCF69eolWrRocd+xr127JsqUKSNWrVqltN28eVNUqVJFfPHFF0KIO2k9du3apWwz
Y8YMoVarRWpqqtL2/vvvi/bt2wshhLhx44YwNTUVsbGxescbPHiw6NOnz7+8Ak9eVlaWCAjooJc6
RqPRCBcXF7Fw4cJnPb0XmkzFIUmSJEmSJEkPVpqpReSKbEmSpFL2/fffM2rUKA4cOMC+ffvo378/
zZs3p02bNnTt2hVzc3N+++03bt68yQcffMBbb7113xW2JRWnksjIyKB379588cUXdOvWjatXr/Lb
b78V3+jjhx9+IDg4mAULFtCgQQOOHDnCkCFDMDMzo0mTJrdXCJdcddvnqa66fZaSk5Pp378/R48e
xcXFhcOHDz/xY9aqVYtatWpx4sQJpS0kJIQNGzZw5MgRvW0zMjJKdVW8Tqdjx44duLi4YGNjQ9u2
bfniiy/uuyq/efNWt/96dqtKmzZtqvfe29ubsLAwEhMT0el0ODs7K99zKEoXYmtrC0B8fDw9e/a8
77gpKSncunWLZs2aKW0GBgZ4eXlx8uRJvW3r1aun/F2hQgVMTEyoVq2aXltR+pWilBF5eXm0bdtW
b143b97Ew8Pj357+E6dfkLAlRZ/1cBwcajBkyJBnO7kX3J0nMPopbf7+HWQqDkmSJEmSJEkqZTKQ
LUmS9C/4+vri4eFBWFjYA7dxd3dn0qRJQNFj5/Pnz2fHjh0IITh27BipqalUrlwZgOXLl+Pm5kZc
XBwNGzbUGyctLY0aNWrQu3dvpe3ChQvodDq6d+9O1apVAXBzc1P6g4ODmT17Nl27dgWKcuYeP36c
b775Bhsbm9tbPTiX68scyJ4yZQpmZmacOnUKU1NT5foePXpUL6fwg9y8eRNDQ8PHmkNxqov75bi2
s7N7rLHvVqFCBQIDA+/5rgYGdrwnoLl//3CsrStw+fJwdDpB0XdiN2r1cNq27fBMvxfXrl3DwMCA
w4cPo1brl/YwMzMDivJ9P0hxkPnuay6EuKet5OerUqnu+bxVKhWFhYUA5ObmAhAZGan8nouVLVv2
oef1NGm12lf6JtaTJlNxSJIkSZIkSdLTIYs9SpIklbK7g6KVKlXi0qVLnDx5kqpVq+oFvVxcXLCy
srpnZWixuwNt9evXp02bNtStW5eePXuyePFiLl++DEBeXh4pKSkMGjQIc3Nz5fXZZ59x9uxZtmzZ
cnuUmLuO8uLmcv03UlJSaN68Ofb29pQrV+6+gcySypUrh7u7Ow0aNECtVmNqasq4ceMYPHgwdnZ2
mJiYYGFhgZmZGZUqVaJPnz5kZmYyY8YMKlasiKmpKSqVihMnTpCUlISRkRERERGEhIQQHx+PWq1G
o9GwbNkyoKhA46ZNm5Tjnz9/nl69emFtbY2ZmRleXl7KauABAwbw2muv6c135MiR+Pr6PvB8fvjh
B+rVq8fWrZG3A+qRgBFFAc2vyMq6iE6XTckCbw0b1n5qq0pjY2P13u/fv59atWrh4eHBrVu3uHjx
Io6Ojnqv4uC/u7s7O3bsuO+4Tk5OGBoasmfPHqXt1q1bHDp0CFdX1/88X1dXV8qWLUtaWto986pS
pcp/HvdJeBkLEj6PnmSBXkmSJEmSJEmSZCBbkiSp1D1oFeeDAqcl29VqtV6aAiEEt27dUt6r1Wq2
bdtGVFQUbm5uzJs3j9q1a5OWlqasEF28eDHx8fHK69ixY+zfvx9ra2vMzS3QaIZTtDLzHBCBRjOC
gIBHX3Vbcj5P29q1a3F3d8fExAQbGxvatWvH9evXEUIwdepUqlatipGRER4eHmzdulXZT61Wc/jw
YUJCQtBoNISEhODo6AigBKr9/Pw4duwYGo2G7OxsABITE4mPj6dVq1bMnDmTsLAwIiMjqVq1KsHB
wbRr146bN28ihGDVqlVUrVqVyZMnM2PGDBYuXAjAmjVrUKvVDBs2jPHjx2NhYYGbmxvnzp3jvffe
4+OPP8bMzExZsQ9Fq5BbtmzJhQsX+OWXX0hISGDcuHHKauAH+afA/M2bN3nzzTdvv1sOpAEDbr9v
pezv4uLC9OnT2bFjB9u2bXlqRUDPnTvHmDFj0Gq1rFy5kvnz5/PRRx/h5OREnz59ePvtt/npp59I
TU3lwIEDzJgxQ7k58/HHH3Pw4EE+/PBDEhMTSUpK4ptvviE7OxsTExM++OADxo4dy9atWzlx4gSD
Bw/m+vXrDBw4UDl+yd/dozAzM2PMmDGMHDmSZcuWcebMGY4cOcL8+fNZvnx5qV6bx6VfkLCkV+Mm
liRJkiRJkiRJLwcZyJYkSfqXhBDMmjULR0dHNBoNGo2GMmXK0KFDB7Kysli7dq0SaO3atSu//fYb
y5cvZ+LEiaSkpNCmTRtCQ0MpV64cBgYGXL58mQ8//BAnJyciIiKIjIwkPDxcOV5iYiK7du1i9erV
+Pj4YGxszLvvvouvry9HjhyhTJkyfPzxx9SuXZsqVaqQkpKCo6MjCQkJODk54ejoSHR0NCEhIVy7
lnvPqttWrRpia1seOzs7LC0t8ff3JyEhQTl+SEgIHh4eLFmyBEdHR4yMjJ72JQfu5AcfPHgwSUlJ
7N69m9deew0hBF9++SVz5sxRcioHBATQpUsXZSVqRkYGrq6ujBkzhoyMDMaOHcuBAwcQQrBz504y
MjJYv349devWxcbGht27iwJ8hoaG2NracurUKby8vDAwMODvv/+mY8eOjBs3jlWrVmFmZsaQIUPY
sGEDN27cQAiBmZkZ9vb2qFQqLCwsuH79On/99Re7du2ib9++GBgYEBwcTGJiIj/++COJiYmoVCpC
QkJISUnhhx9+4Pz58+Tk5ODt7Y2joyOvv/46TZo00bsm91uZ/SD9+/cvkUf6b+BLYAuQR3FAE2DW
rFl8/PHH+Pn5YWVl9Xgf2iNSqVS8/fbbXL9+HS8vL4KCghg5ciSDBw8GIDw8nLfffpsxY8ZQp04d
unfvzqFDh3BwcACKVsJu27aNhIQEmjRpgo+PD5s2bcLAoCiD2owZM+jRowdvv/02jRo14syZM2zb
tg1LS0u9Ofxb06ZNU25cuLq60r59eyIjI6lRo0YpXJXS4+zsTEBAh8e+iSVJkiRJkiRJkvQsqf7t
CqRnTaVSeQJxcXFxeHp6PuvpSJL0ivH19SU3N5ezZ89SrVo1cnNzGTVqFBcvXmTPnj38+uuvODk5
sWnTJvbu3cu7776LqampErxu3Lgx169fp2fPntjb2/P999+TmZmJj48POTk5XL16lfPnz6NSqVi9
ejWvv/46JiYm5OXl4eDgwIcffkhGRgZnz55l+/btzJ07l6FDhzJs2DCWLFnC559/zogRIwgNDcXA
wIAPP/yQ7777jszMTC5dusTWrVvZsWMHKSkpXLp0CRcXF4YOHYqZmRmTJ0/GwsKCb7/9lvDwcLRa
LVZWVoSEhPDFF1/QsmVLpk+fjkajoW7duk/92h85coRGjRqRmpqq5AcvZm9vT1BQEOPHj1famjRp
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
k5NYtGjRvz9JSSQnJ9/+NyBCgCjxWi4AodVqn8o8AgI6CI2m/O3jpgtYLjSa8iIgoMM/7te/f3/R
vXv3pzJH6b9JTU0VarVaxMfHP3Cb/Px8kZmZ+RRnJUmSJEmSJEnPr7i4uOJYjad4zLiwXJEtSc+x
+vXr06ZNG+rWrUvPnj1ZvHix3krN+vXrU7ZsWeW9t7c3ubm5SkqD06dP07t3b2rWrImlpSWOjo6o
VColHUJ8fDweHh5YWlre9/jx8fFMnToVc3Nz5TVkyBAuXrxIfn7+Ezzzf+dlTI/wPPP19SUoKIig
oCCsrKywtbVl8uTJz3pa/+hBv6WrV6/y559/0qxZM73tfXx8OHny5L86RpkyZahbt67yPjMzkz//
/BM/P7/7bh8fH8/Vq1cpX7683m8sNTVVbzW49OieZs58X19fhg8fzsiRIylfvjwVK1ZkyZIl5OXl
YW1tBfxNydzjbdo0wda2PI6OjpiYmFCnTh3mzp37j8c4ePAgdnZ2fP755wAEBwfj4eGh9BenmJo9
ezaVK1fGxsaGYcOGodPplG0yMjLo2LEjJiYm1KxZk5UrV1KjRo2HHlt6MPGQ/Pdly5bFxsbmKc1G
kiRJkiRJkl4dMpAtSc8xtVrNtm3biIqKws3NjXnz5lGnTh1SU1P/cb/ilAedOnUiJyeHxYsXc+DA
AQ4cOIAQgoKCAgCMjY3/cZzc3FxCQkKIj49XXseOHUOr1WJkZFQq51iaXqb0CM+7ZcuWYWhoyMGD
B5k7dy5hYWEsWbLkWU/rgR70Wzp79ixwb5oQIYTSplarlbZiN2/evOcYd/+eHuX3VblyZRISEvR+
Y8nJyYwdO/bfn6T01HPmL1u2DFtbWw4ePMjw4cN5//33eeONN/Dz8yM5OYnevXtjYWFBYmIimzcX
pZVZu3YtJ0+eZMqUKXz66aesXbv2vmPv3LmTdu3aMX36dOX7oFKp7vmu7tq1izNnzhAdHc2yZcsI
Dw8nPDxc6e/Xrx8ZGRnExMSwbt06Fi5cSGZmZqleh5eREIJZs2ZRq1YtjIyMqF69OqGhoUp/SkoK
fn5+mJqa0qBBA2JjY5W+4pz5xUJCQvDw8CAiIoIaNWpgZWVFr169uHbtmrLNo9S0kCRJkiRJkqRX
nQxkS9ILwNvbmylTpnDkyBEMDQ3ZsGEDULSi88aNG8p2+/fvx8zMDHt7e7Kzs9FqtUycOBFfX19q
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
t47k5GTmz5/PL7/88srz+hTv3XdhxowZzJw5k7179/LLL78wevRoOnfuXOC/By/j4ODA3r172bhx
I0OHDn1Hs/24tWrViqysLLZu3cqVK1fYv38/AQEB+fqlpaUBmr9IiI+P58yZM8ovEgAaNmzI3r17
iY6OxsvLCzc3Nx4/fsxvv/1GTExMgZnekiRJkiRJkiRJ74Nc7FGSPkL16tWjXr16jBs3jgoVKvDL
L79QvHhxsrKyPvTUNCQlJZGZmUn9+vWVNh0dHWrXrk1CQsIbjflXIDYcyA3GBJCVJYiM7I5arf6o
FmosLM+X6khLS6NmzZqsXr06X+DYwsICgGXLljFkyBAiIiJYt24d48aNY+LEic96zQWmA1uBbUA0
kBNMznv9VCoV69atIzg4GFdXV5ycnJg/fz5eXl4vLDXxoiB3xYoVn73bx1/fHcqxHRwcXuFKFMzb
25uqVauio6NDeHg4bm5ubNy4kZCQEDZv3syTJ0+oVasWs2fPxsTEhH379jFv3jzu3LmDEIJixYqx
YcMGzM3NMTc3Z/ny5YwcORIhBMbGxixZsgQAX19fXF1d8ff3RwiBhYUFPXv2ZNmyZTlnEh2Nt7c3
u3btYtSoUfz2229Ur16dFStWIIT4R967ryM1NZWuXbs/u0459PUNCArqxcyZM195nLz3YKVKldi9
ezfe3t7o6Ojw7bffFuqcP3Z6enq0b9+e8PBw1Go1zs7OuLm55etnaWlJ2bJlSUpKokuXLi8cz8vL
iyVLlqCrq8vUqVNRqVQ0aNCAb7/9loyMDI1/7yVJkiRJkiRJkt4nGciWpI/I0aNH2b17N82aNcPS
0pLDhw9z+/ZtKleuzKNHj9ixYweJiYmYmZlRokSJ166T3atXL+7fv8/GjRuBnOCgu7s7s2fPfqP5
5gZYnw9sCiFemtH7Mq+S1VsUg4GHDx/W+Hzo0CEcHR1feJ08PDyUWrdGRkYvHLdatWpUq1aNUaNG
Ub9+fU6cOPFsS24wecizV33gUIHB5CZNmij1o3PlfWiS933jxo1f+EClUqVK+Pr6sWtXMFlZgpzv
LBpt7SH4+Pi99fcWFhbGgAEDiImJAaBTp04YGhoSGRmJiYkJP/zwAz4+Pkp96h9//JG+ffuycOFC
6tevz5o1a5g1axb29vYcP34c+Otvok2bNgCMGDGCGzduEBERQfny5Zk+fTrLly8nOTlZYy5fffUV
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
abHutr59o5WcvPKS95VF0U0Kt2zZopCQkFKD2Pbt2yspKUnnzp1zh9abNm2Sr6+vwsLC5Ofnp9at
W2vt2rXq3bt3sfvDw8N19OhR+fr6qlWrVqWOKyoqSrVq1dL06dO1evVqrVmzxr3ZZNu2bXXmzBn3
P3J8+eWXatWqlU6cOCFjjOrUqSNJ8vPz07Zt2zR48GD96U9/0nvvvafXX39dtWvX1vLly3XjjTe6
n3fo0CG9++67ysnJ0YIFC9SjRw+NHDlSa9eu1Y4dOzzG9mshdfv27Uv8XAEAAAAAQPkQZAOwlTNn
zrgDxz59+kiSR+B4+PBhvfvuuzp8+LCaNWsmKa8MxZo1a7Rs2TK98MILOnz4sB588EG1b99ektS6
detSn7d48WJFR0drxowZkvLKdGzevFmrV6/2uM6yLC1fvtwdkMbGxmrt2rW/GmRXlICAAKWmrpbT
6VRmZqaCg4MrbCV2QemTCRMmaOfOnVq8eLEWLlxY6vUxMTF69tlnNXr0aM2dO1fHjh1TfHy8Ro0a
pcaNG0uSnn32WU2ePFmBgYHq37+/Tp06pc8//1xTp05V37591b17dw0ePFi///3vFRoaqu+//14p
KSkaMmSI2rdvr1mzZunBBx/U+PHjNXXqVNWsWVNDhgzRrl279Pjjj+uOO+5QeHi4LMtSvXr1lJmZ
qaFDh+rmm292r4qWpHbt2umdd95RYGCgLl68qC1btmjPnj1q166dAgICFBYWpvPnz0uS9u7dK5fL
JWOM+vTpo5o1ayo3N1c///xzsc+goOxKaeLj49WzZ08tWLBA9913n1JTU5WWllaePx4AAAAAACBK
iwCwmQMHDujixYvq0qWLu60gcJSkL774Qi6XS6GhoR71lTdu3OiurxwfH6/nn39ePXv21LPPPqsv
vvii1Od9/fXXHs+SVOxYygvDC0JsKa8mckE95PJyOBxas2aNnE5nme8JCQlR//79K7ScyKVKn5S0
8rh27dpKS0tTdna2unTpoqFDh+qee+7RokWLPPp8/fXX9d///d+69dZbNWjQIGVmZrrPp6SkqFev
XWbUJwAAIABJREFUXoqLi1NYWJhGjhypQ4cOqWnTpvL19dXx48c1evRo/fGPf5SUV05m6dKl6t+/
vw4ePKjk5GQ98sgjkqSBAwfqH//4h2655RZ3OZLDhw9Lklq2bKk5c+YoISFBubm5+v777/XII494
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
1q9fr4yMDMXFxSknJ0ezZs3S0KFD1a9fP/3www/617/+pTvvvFNS3qrsAkeOHNGAAQPUtWtX7dmz
R2+99ZaWLl2qF154wWMcSUlJ8vPz07Zt2/TKK6/oueee09q1ayvg0/mlHIjD4VBKSoocDodSU1cr
ICCgQvoHAAAAAABXjtIiAFCKyqx3XFKt6MIB7/Lly/XYY4/pxIkTV/wsf39/+fv7y9fXV4GBgZd1
75gxYzR06FBJ0vz587Vo0SJt27ZN9957rxYvXqwGDRooOTlZvr6+kjxLrtSuXVsXLlwo9kzLstyv
33zzTbVq1cq9Ojw0NFTz5s3Tk08+qWeeecZ9XceOHfX0009Lyiv7snjxYq1du1Z33333Zb2fS6Ec
CAAAAAAA9kWQDQC/ojICzl+rFW1Zlkew7S0dOnRwv65Tp478/f117NgxSdLu3bt11113uUPs8ti/
f7+6d+/u0dajRw+dPn1a3333nW688UZJeUF2Yc2bN3ePAwAAAAAAXPsoLQIA5ZSTk6Np06apQYMG
CgwM9FhB7OPjo7///e8e1wcEBCgpKUlS8dIihW3YsEFxcXE6efKku7504drVFcHHx8djZbQkXbx4
sdh11atX9zg2xrjrV9euXfuKx1FSYF8wrsLtlxoHAAAAAAC49hFkA0A5vfvuu6pevbq2b9+uxMRE
JSQkaOnSpWW+v7QV13feeadef/111atXz11f+oknnqioYUuSAgMD9a9//ct9fOrUKR08ePCy+ujY
saM+++wzuVyuEs/XqFGj1HMF2rdvr88//9yjbfPmzfL399cNN9xwWeMBAAAAAADXLoJsACinVq1a
KSEhQSEhIRoxYoSmTZumhQsXlvn+oiuiC1SvXl3169eXMUaBgYFq0qSJ6tSpU1HDliT913/9l1as
WKFNmzbpiy++0COPPKJq1S6v2tTUqVN16tQpDRs2TDt37lRmZqZWrlwpp9MpSWrdurX27Nkjh8Oh
48ePKycnp1gfjz76qA4fPqxp06bp66+/1kcffaRnn31WM2fOrJD3eS1r06aNu7Y4AAAAAADXOoJs
ACinbt26eRx3795dTqfzqih58dvf/la9evXSwIEDNXDgQN1///1q166dxzUlrRgv3NawYUOtW7dO
Z86cUZ8+fXT77bfrnXfecZcBGT9+vMLCwnT77berSZMm7pXXhfto0aKFUlJStH37dt1222169NFH
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
AAAAALA1gmwAAAAAAAAAgK0RZAMAAAAAAAAAbI0gGwAAAAAAAABgawTZAAAAAAAAAABbI8gGAAAA
AAAAANgaQTYAAAAAAAAAwNYIsgEAAAAAAAAAtkaQDQAAAAAAAACwNYJsAAAAAAAAAICtEWQDAAAA
AAAAAGyNIBsAAAAAAAAAYGsE2QAAAAAAAAAAWyPIBgAAAAAAAADYGkE2AAAAAAAAAMDWCLIBAAAA
AAAAALZGkA0AAAAAAAAAsDWCbAAAAAAAAACArRFkAwAAAAAAAABsjSAbAAAAAAAAAGBrBNkAAAAA
AAAAAFsjyAYAAAAAAAAA2BpBNgAAAAAAAADA1giyAQAAAAAAAAC2RpANAAAAAAAAALA1gmwAAAAA
AAAAgK0RZAMAAAAAAAAAbI0gGwAAAAAAAABgawTZAAAAAAAAAABbI8gGAAAAAAAAANgaQTYAAAAA
AAAAwNYIsgEAAAAAAAAAtkaQDQAAAAAAAACwNYJsAAAAAAAAAICtEWQDAAAAAAAAAGyNIBsAAAAA
AAAAYGsE2QAAAAAAAAAAWyPIBgAAAAAAAADYGkE2AAAAAAAAAMDWCLIBAAAAAAAAALZGkA0AAAAA
AAAAsDWCbAAAAAAAAACArRFkAwAAAAAAAABsjSAbAAAAAAAAAGBrBNkAAAAAAAAAAFsjyAYAAAAA
AAAA2BpBNgAAAAAAAADA1giyAQAAAAAAAAC2RpANAAAAAAAAALA1gmwAAAAAAAAAgK0RZAMAAAAA
AAAAbI0gGwAAAAAAAABgawTZAAAAAAAAAABbI8gGAAAAAAAAANgaQTYAAAAAAAAAwNYIsgEAAAAA
AAAAtkaQDQAAAAAAAACwNYJsAAAAAAAAAICtEWQDAAAAAAAAAGyNIBsAAAAAAAAAYGsE2QAAAAAA
AAAAWyPIBgAAAAAAAADYGkE2AAAAAAAAAMDWCLIBAAAAAAAAALZGkA0AAAAAAAAAsDWCbAAAAAAA
AACArRFkAwAAAAAAAABsjSAbAAAAAAAAAGBrBNkAAAAAAAAAAFsjyAYAAAAAAAAA2BpBNgAAAAAA
AADA1giyAQAAAAAAAAC2RpANAAAAAAAAALA1gmwAAAAAAAAAgK0RZAMAAAAAAAAAbI0gGwAAAAAA
AABgawTZAAAAAAAAAABbI8gGAAAAAAAAANgaQTYAAAAAAAAAwNYIsgEAAAAAAAAAtkaQDQAAAAAA
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
gg==
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[12]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Hand pick several words to show the distances</span>
<span class="n">visualizeWords</span> <span class="o">=</span> <span class="p">[</span><span class="s2">&quot;a&quot;</span><span class="p">,</span> <span class="s2">&quot;an&quot;</span><span class="p">,</span> <span class="s2">&quot;the&quot;</span><span class="p">,</span> <span class="s2">&quot;one&quot;</span><span class="p">,</span> <span class="s2">&quot;first&quot;</span><span class="p">,</span> <span class="s2">&quot;two&quot;</span><span class="p">,</span> <span class="s2">&quot;three&quot;</span><span class="p">,</span> <span class="s2">&quot;four&quot;</span><span class="p">,</span>
                  <span class="s2">&quot;good&quot;</span><span class="p">,</span> <span class="s2">&quot;great&quot;</span><span class="p">,</span> <span class="s2">&quot;well&quot;</span><span class="p">,</span> <span class="s2">&quot;poor&quot;</span><span class="p">,</span> <span class="s2">&quot;bad&quot;</span><span class="p">,</span> <span class="s2">&quot;evil&quot;</span><span class="p">,</span> <span class="s2">&quot;god&quot;</span><span class="p">]</span>

<span class="n">visualizeIdx</span> <span class="o">=</span> <span class="p">[</span><span class="n">dictionary</span><span class="p">[</span><span class="n">word</span><span class="p">]</span> <span class="k">for</span> <span class="n">word</span> <span class="ow">in</span> <span class="n">visualizeWords</span><span class="p">]</span>
<span class="n">visualizeVecs</span> <span class="o">=</span> <span class="n">final_embeddings</span><span class="p">[</span><span class="n">visualizeIdx</span><span class="p">,</span> <span class="p">:]</span>
<span class="n">temp</span> <span class="o">=</span> <span class="p">(</span><span class="n">visualizeVecs</span> <span class="o">-</span> <span class="n">np</span><span class="o">.</span><span class="n">mean</span><span class="p">(</span><span class="n">visualizeVecs</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="mi">0</span><span class="p">))</span>
<span class="n">covariance</span> <span class="o">=</span> <span class="mf">1.0</span> <span class="o">/</span> <span class="nb">len</span><span class="p">(</span><span class="n">visualizeIdx</span><span class="p">)</span> <span class="o">*</span> <span class="n">temp</span><span class="o">.</span><span class="n">T</span><span class="o">.</span><span class="n">dot</span><span class="p">(</span><span class="n">temp</span><span class="p">)</span>
<span class="n">U</span><span class="p">,</span><span class="n">S</span><span class="p">,</span><span class="n">V</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">linalg</span><span class="o">.</span><span class="n">svd</span><span class="p">(</span><span class="n">covariance</span><span class="p">)</span>
<span class="n">coord</span> <span class="o">=</span> <span class="n">temp</span><span class="o">.</span><span class="n">dot</span><span class="p">(</span><span class="n">U</span><span class="p">[:,</span><span class="mi">0</span><span class="p">:</span><span class="mi">2</span><span class="p">])</span> 

<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">xrange</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">visualizeWords</span><span class="p">)):</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">text</span><span class="p">(</span><span class="n">coord</span><span class="p">[</span><span class="n">i</span><span class="p">,</span><span class="mi">0</span><span class="p">],</span> <span class="n">coord</span><span class="p">[</span><span class="n">i</span><span class="p">,</span><span class="mi">1</span><span class="p">],</span> <span class="n">visualizeWords</span><span class="p">[</span><span class="n">i</span><span class="p">],</span> 
    	<span class="n">bbox</span><span class="o">=</span><span class="nb">dict</span><span class="p">(</span><span class="n">facecolor</span><span class="o">=</span><span class="s1">&#39;green&#39;</span><span class="p">,</span> <span class="n">alpha</span><span class="o">=</span><span class="mf">0.1</span><span class="p">))</span>
    
<span class="n">plt</span><span class="o">.</span><span class="n">xlim</span><span class="p">((</span><span class="n">np</span><span class="o">.</span><span class="n">min</span><span class="p">(</span><span class="n">coord</span><span class="p">[:,</span><span class="mi">0</span><span class="p">]),</span> <span class="n">np</span><span class="o">.</span><span class="n">max</span><span class="p">(</span><span class="n">coord</span><span class="p">[:,</span><span class="mi">0</span><span class="p">])))</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylim</span><span class="p">((</span><span class="n">np</span><span class="o">.</span><span class="n">min</span><span class="p">(</span><span class="n">coord</span><span class="p">[:,</span><span class="mi">1</span><span class="p">]),</span> <span class="n">np</span><span class="o">.</span><span class="n">max</span><span class="p">(</span><span class="n">coord</span><span class="p">[:,</span><span class="mi">1</span><span class="p">])))</span>

<span class="n">plt</span><span class="o">.</span><span class="n">savefig</span><span class="p">(</span><span class="s1">&#39;q3_word_vectors.png&#39;</span><span class="p">)</span>
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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[13]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Check similarity of embedding words for top words</span>
<span class="n">nom</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sqrt</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">square</span><span class="p">(</span><span class="n">final_embeddings</span><span class="p">),</span> <span class="mi">1</span><span class="p">,</span> <span class="n">keepdims</span><span class="o">=</span><span class="bp">True</span><span class="p">))</span>
<span class="n">normalized_embeddings</span> <span class="o">=</span> <span class="n">final_embeddings</span> <span class="o">/</span> <span class="n">nom</span>

<span class="c1">#randomly pick some words from top distribution</span>
<span class="n">valid_size</span> <span class="o">=</span> <span class="mi">16</span>
<span class="n">valid_example</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">choice</span><span class="p">(</span><span class="mi">50</span><span class="p">,</span> <span class="n">valid_size</span><span class="p">,</span> <span class="n">replace</span><span class="o">=</span><span class="bp">False</span><span class="p">)</span>
<span class="n">valid_matrix</span> <span class="o">=</span> <span class="n">normalized_embeddings</span><span class="p">[</span><span class="n">valid_example</span><span class="p">,:]</span>
<span class="n">similarity</span> <span class="o">=</span> <span class="n">valid_matrix</span><span class="o">.</span><span class="n">dot</span><span class="p">(</span><span class="n">normalized_embeddings</span><span class="o">.</span><span class="n">T</span><span class="p">)</span>

<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">xrange</span><span class="p">(</span><span class="n">valid_size</span><span class="p">):</span>
    <span class="n">valid_word</span> <span class="o">=</span> <span class="n">r_dictionary</span><span class="p">[</span><span class="n">valid_example</span><span class="p">[</span><span class="n">i</span><span class="p">]]</span>
    <span class="n">top_k</span> <span class="o">=</span> <span class="mi">8</span> <span class="c1"># number of nearest neighbors</span>
    <span class="n">nearest</span> <span class="o">=</span> <span class="p">(</span><span class="n">similarity</span><span class="p">[</span><span class="n">i</span><span class="p">,:])</span><span class="o">.</span><span class="n">argsort</span><span class="p">()[</span><span class="o">-</span><span class="n">top_k</span><span class="o">-</span><span class="mi">1</span><span class="p">:</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span>
    <span class="n">close_words</span> <span class="o">=</span> <span class="p">[</span><span class="n">r_dictionary</span><span class="p">[</span><span class="n">k</span><span class="p">]</span> <span class="k">for</span> <span class="n">k</span> <span class="ow">in</span> <span class="n">nearest</span><span class="p">]</span>
    <span class="k">print</span> <span class="s2">&quot;&#39;{}&#39; are closest words to &#39;{}&#39;&quot;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="s1">&#39;, &#39;</span><span class="o">.</span><span class="n">join</span><span class="p">(</span><span class="n">close_words</span><span class="p">),</span> <span class="n">valid_word</span><span class="p">)</span>

    
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>&#39;this, from, state, international, at, some, and, an&#39; are closest words to &#39;in&#39;
&#39;zero, one, five, seven, four, eight, six, three&#39; are closest words to &#39;two&#39;
&#39;eight, two, four, five, nine, zero, three, seven&#39; are closest words to &#39;six&#39;
&#39;only, some, would, they, known, an, it, he&#39; are closest words to &#39;be&#39;
&#39;sometimes, being, published, but, united, became, while, called&#39; are closest words to &#39;also&#39;
&#39;who, such, which, from, their, his, or, this&#39; are closest words to &#39;s&#39;
&#39;both, its, in, some, would, an, international, this&#39; are closest words to &#39;and&#39;
&#39;more, their, where, if, not, at, are, was&#39; are closest words to &#39;were&#39;
&#39;act, however, place, there, english, they, any, what&#39; are closest words to &#39;UNK&#39;
&#39;in, or, such, and, this, into, from, was&#39; are closest words to &#39;by&#39;
&#39;from, its, will, states, all, this, but, his&#39; are closest words to &#39;their&#39;
&#39;their, an, its, not, some, when, they, be&#39; are closest words to &#39;he&#39;
&#39;both, united, some, there, often, he, not, its&#39; are closest words to &#39;they&#39;
&#39;if, new, during, an, when, other, from, this&#39; are closest words to &#39;or&#39;
&#39;many, after, not, this, can, some, were, but&#39; are closest words to &#39;at&#39;
&#39;which, its, not, some, in, it, and, this&#39; are closest words to &#39;an&#39;
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span></span> 
</pre></div>

</div>
</div>
</div>

</div>
    </div>
  </div>
</body>
</html>
