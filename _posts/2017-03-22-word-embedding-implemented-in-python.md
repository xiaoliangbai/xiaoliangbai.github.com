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

<span class="n">vocabulary_size</span> <span class="o">=</span> <span class="mi">5000</span>
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
<pre>Most common words: [[&#39;UNK&#39;, 2735459], (&#39;the&#39;, 1061396), (&#39;of&#39;, 593677), (&#39;and&#39;, 416629), (&#39;one&#39;, 411764)]
Sample data: [0, 3084, 12, 6, 195, 2, 3137, 46, 59, 156] [&#39;UNK&#39;, &#39;originated&#39;, &#39;as&#39;, &#39;a&#39;, &#39;term&#39;, &#39;of&#39;, &#39;abuse&#39;, &#39;first&#39;, &#39;used&#39;, &#39;against&#39;]
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
<div class=" highlight hl-ipython2"><pre><span></span><span class="n">embedding_size</span> <span class="o">=</span> <span class="mi">128</span>
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
<pre>&gt;&gt;&gt; iter 20100: 1.953956
&gt;&gt;&gt; iter 20200: 1.922596
&gt;&gt;&gt; iter 20300: 1.904774
&gt;&gt;&gt; iter 20400: 1.886119
&gt;&gt;&gt; iter 20500: 1.854997
&gt;&gt;&gt; iter 20600: 1.837172
&gt;&gt;&gt; iter 20700: 1.810312
&gt;&gt;&gt; iter 20800: 1.794571
&gt;&gt;&gt; iter 20900: 1.772483
&gt;&gt;&gt; iter 21000: 1.771986
&gt;&gt;&gt; iter 21100: 1.776612
&gt;&gt;&gt; iter 21200: 1.778633
&gt;&gt;&gt; iter 21300: 1.768682
&gt;&gt;&gt; iter 21400: 1.752776
&gt;&gt;&gt; iter 21500: 1.742118
&gt;&gt;&gt; iter 21600: 1.735377
&gt;&gt;&gt; iter 21700: 1.724266
&gt;&gt;&gt; iter 21800: 1.725502
&gt;&gt;&gt; iter 21900: 1.727812
&gt;&gt;&gt; iter 22000: 1.724075
&gt;&gt;&gt; iter 22100: 1.713913
&gt;&gt;&gt; iter 22200: 1.716034
&gt;&gt;&gt; iter 22300: 1.710629
&gt;&gt;&gt; iter 22400: 1.696416
&gt;&gt;&gt; iter 22500: 1.673351
&gt;&gt;&gt; iter 22600: 1.666443
&gt;&gt;&gt; iter 22700: 1.667904
&gt;&gt;&gt; iter 22800: 1.679916
&gt;&gt;&gt; iter 22900: 1.667690
&gt;&gt;&gt; iter 23000: 1.659292
&gt;&gt;&gt; iter 23100: 1.644989
&gt;&gt;&gt; iter 23200: 1.645646
&gt;&gt;&gt; iter 23300: 1.648299
&gt;&gt;&gt; iter 23400: 1.659830
&gt;&gt;&gt; iter 23500: 1.654235
&gt;&gt;&gt; iter 23600: 1.660365
&gt;&gt;&gt; iter 23700: 1.647172
&gt;&gt;&gt; iter 23800: 1.659632
&gt;&gt;&gt; iter 23900: 1.665102
&gt;&gt;&gt; iter 24000: 1.648008
&gt;&gt;&gt; iter 24100: 1.647752
&gt;&gt;&gt; iter 24200: 1.654970
&gt;&gt;&gt; iter 24300: 1.649674
&gt;&gt;&gt; iter 24400: 1.639948
&gt;&gt;&gt; iter 24500: 1.642838
&gt;&gt;&gt; iter 24600: 1.638508
&gt;&gt;&gt; iter 24700: 1.620972
&gt;&gt;&gt; iter 24800: 1.616759
&gt;&gt;&gt; iter 24900: 1.629624
&gt;&gt;&gt; iter 25000: 1.616341
&gt;&gt;&gt; iter 25100: 1.602123
&gt;&gt;&gt; iter 25200: 1.592497
&gt;&gt;&gt; iter 25300: 1.592320
&gt;&gt;&gt; iter 25400: 1.594618
&gt;&gt;&gt; iter 25500: 1.590584
&gt;&gt;&gt; iter 25600: 1.578454
&gt;&gt;&gt; iter 25700: 1.581224
&gt;&gt;&gt; iter 25800: 1.591607
&gt;&gt;&gt; iter 25900: 1.600072
&gt;&gt;&gt; iter 26000: 1.586118
&gt;&gt;&gt; iter 26100: 1.587736
&gt;&gt;&gt; iter 26200: 1.570529
&gt;&gt;&gt; iter 26300: 1.574145
&gt;&gt;&gt; iter 26400: 1.581486
&gt;&gt;&gt; iter 26500: 1.586999
&gt;&gt;&gt; iter 26600: 1.573856
&gt;&gt;&gt; iter 26700: 1.563914
&gt;&gt;&gt; iter 26800: 1.565445
&gt;&gt;&gt; iter 26900: 1.563444
&gt;&gt;&gt; iter 27000: 1.548416
&gt;&gt;&gt; iter 27100: 1.545619
&gt;&gt;&gt; iter 27200: 1.542652
&gt;&gt;&gt; iter 27300: 1.533192
&gt;&gt;&gt; iter 27400: 1.527055
&gt;&gt;&gt; iter 27500: 1.525292
&gt;&gt;&gt; iter 27600: 1.523593
&gt;&gt;&gt; iter 27700: 1.549005
&gt;&gt;&gt; iter 27800: 1.552057
&gt;&gt;&gt; iter 27900: 1.565260
&gt;&gt;&gt; iter 28000: 1.551230
&gt;&gt;&gt; iter 28100: 1.549710
&gt;&gt;&gt; iter 28200: 1.545411
&gt;&gt;&gt; iter 28300: 1.537904
&gt;&gt;&gt; iter 28400: 1.538123
&gt;&gt;&gt; iter 28500: 1.542434
&gt;&gt;&gt; iter 28600: 1.532893
&gt;&gt;&gt; iter 28700: 1.540170
&gt;&gt;&gt; iter 28800: 1.544613
&gt;&gt;&gt; iter 28900: 1.557344
&gt;&gt;&gt; iter 29000: 1.549625
&gt;&gt;&gt; iter 29100: 1.538087
&gt;&gt;&gt; iter 29200: 1.531683
&gt;&gt;&gt; iter 29300: 1.537240
&gt;&gt;&gt; iter 29400: 1.527687
&gt;&gt;&gt; iter 29500: 1.531357
&gt;&gt;&gt; iter 29600: 1.523680
&gt;&gt;&gt; iter 29700: 1.520342
&gt;&gt;&gt; iter 29800: 1.533904
&gt;&gt;&gt; iter 29900: 1.526332
&gt;&gt;&gt; iter 30000: 1.514875


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
<pre>&lt;matplotlib.text.Text at 0x7f762b6744d0&gt;</pre>
</div>

</div>

<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAicAAAF5CAYAAABEPIrHAAAABHNCSVQICAgIfAhkiAAAAAlwSFlz
AAAPYQAAD2EBqD+naQAAIABJREFUeJzs3Xl8VdW99/HPOknInDA4AaJokaGKWLAqg1oHZFLAap+n
9PbetvdpK61DxdmKQ6toreDQSqu9z631trf0tlURFURrex2QaoVHrYpWrxOCI5A5ISFnPX/81naf
hCSQEDgnJ9/363VeOWefvfdZeyeQX37rt9Zy3ntEREREMkUi3Q0QERERSaXgRERERDKKghMRERHJ
KApOREREJKMoOBEREZGMouBEREREMoqCExEREckoCk5EREQkoyg4ERERkYyi4EREREQySkYEJ865
Y51zy5xzG5xzSefczDb2GeWcu985V+Gcq3HOPeOc2z8d7RUREZHdJyOCE6AYeB44G9husR/n3GeA
J4FXgOOA0cC1QMMebKOIiIjsAS7TFv5zziWB2d77ZSnblgCN3vuvpa9lIiIisidkSuakXc45B8wA
XnfOPeyc+9A591fn3Kx0t01ERES6X8YHJ8A+QAlwKbAcmAzcB9zrnDs2nQ0TERGR7peb7gbshCiA
Wuq9/0l4/qJzbgIwF6tFacE5NwCYAryN6lJEREQ6owAYCqz03m9KRwN6QnDyCbANWNdq+zpgYjvH
TAH+c3c2SkREJMv9E/DbdHxwxgcn3vsm59zfgBGt3hoOvNPOYW8D/OY3v2HUqFG7sXXZZ968edxy
yy3pbkaPonvWNbpvnad71jW6b52zbt06vvrVr0L4XZoOGRGcOOeKgWGAC5sOds6NATZ779cDNwG/
c849CfwFmAacChzfzikbAEaNGsXYsWN3a9uzTXl5ue5ZJ+medY3uW+fpnnWN7luXpa0sIiOCE+BI
LOjw4bEobL8b+Ffv/VLn3Fzg+8BtwGvAF733q9PRWBEREdl9MiI48d4/zg5GDnnvfwX8ak+0R0RE
RNKnJwwlFhERkV5EwYm0MGfOnHQ3ocfRPesa3bfO0z3rGt23nifjpq/vDs65scCaNWvWqAhKRESk
E9auXcu4ceMAxnnv16ajDcqciIiISEbJ6uBk3LgvkpMzlCef3G4SWREREclQWR2cACSThRx33P9W
gCIiItJDZHlwUopNm+I47rgvpbsxIiIishOyPDi5C1uC504gj+rq6jS3R0RERHYky4OT/wOMBn4K
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
AABJRU5ErkJggg==
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
Oq/3U089ZZt39uxZpk+fTpMmTXBxcSEkJIT09PRy11q+fDnNmzfHxcWFwYMHc/To0et+BhERERER
kdpGiWwRERGpUaZPn47RaCQwMBBPT0/OnTvHpk2bKC0tJTw8nLZt2zJ16lRMJpOtuvpqVdZXGr/W
sSv55z//yeLFi1m2bBl5eXl88skn5XpwP/HEE2zdupXVq1ezc+dOhgwZQmRkpK2X99atWxk/fjyT
Jk3i+++/JzQ0lDlz5lzTvUVERERERGozw41UKtmTwWAIArKysrIICgqydzgiIiJyi2nRogVTpkxh
0qRJtrEOHTowcOBAXF1defvtt9m1axdGo7HceUVFRfj4+FBUVETjxo1t4/fffz+dO3dmzpw5xMTE
cOLECT7//HPb8eHDh5OSkkJxcXHlP5yIiIiIiEgFys7OJjg4GCDYarVm38y1VJEtIiIichGz2cza
tWvJzc297nOHDBnC6dOnadGiBY8++iiffPKJrZ/3zp07sVgsBAQE4Orqavu1YcMG9u3bB8CePXvo
3LlzuWuGhITc/EOJiIiIiIjUcFrsUURERAQoLi4mOnokKSlJtrHw8CgSExMwmUy2MQcHh8v6aJ87
dw6AJk2aYDab+frrr0lNTeXxxx9nwYIFpKenc/LkSRwdHcnOzr5sUUoXFxegrBe3FpsUERERERG5
nBLZIiIiIkB09EhSUzOABKA7sIHU1EkMHz6C5OQvbfM8PDw4ePCgbf/EiRP8+OOPtv3bbruNvn37
0rdvXx5//HFatWrFzp076dChAxaLhcOHD9O1a9crxhAYGEhGRka5sS1btlTkY4qIiIiIiNRISmSL
iIjILc9sNp+vxE4AYs6PxmCxWElJGUlubi7+/v4A9OrVi/j4ePr27Uv9+vV58cUXcXQs+ydVfHw8
FouFzp074+zszMqVK3F2dqZ58+aYTCaio6MZNWoUCxYsoEOHDhw5coS0tDTatWtHZGQkkyZNolu3
brz22msMGDCA5ORkUlJS7PKaiIiIiIiIVCfqkS0iIiK3vPz8/PNb3S850gOAvLw828izzz5L9+7d
6devH/369WPgwIH4+voCYDKZWLZsGd26daNdu3akpaXxxRdf2FqTLF++nFGjRjF9+nRatWrFwIED
yczMpFmzZgB07tyZZcuWERcXR/v27UlNTeX555+v1GcXERERERGpCQyX9nis7gwGQxCQlZWVRVBQ
kL3DERERkVrAbDbTsmVLyldkc35/JGaz2VaRLSIiIiIiItcmOzub4OBggGCr1Zp9M9dSRbaIiIjc
8gICAggPj8JonERZ8roISMBonEx4eJSS2CIiIiIiInamRLaIiIgIkJiYQFhYF2Ak0AwYSVhYFxIT
E6o8FrPZzNq1a8nNza3ye4uIiIiIiFRHWuxRREREhLL+1snJX5Kbm0teXh5+fn5VXoldXFxMdPTI
8wtPlgkPjyIxMcHWZ1tERERERORWpIpsERERkYv4+/sTGRlpl3Yi0dEjSU3NoKy9SSGQQGpqBsOH
j6jyWERERERERKoTVWSLiIiIVANms/l8JfbFC07GYLFYSUkZSW5urnp1i4iIiIjILUsV2SIiIiLV
QH5+/vmt7pcc6QFAXl5elcYjIiIiIiJSnSiRLSIiIlIN+Pr6nt/acMmRdAD8/PyqNB4REREREZHq
RIlsERERkWogICCA8PAojMZJlLUXKQISMBonEx4epbYiIiIiIiJyS1MiW0RERKSaSExMICysCzAS
aAaMJCysC4mJCXaOTERERERExL6qxWKPBoPhCWA60BjYDky0Wq3f2TcqERERkaplMplITv6S3Nxc
8vLy8PPzUyW2iIiIiIgI1SCRbTAYhgGvAY8C24ApQIrBYAiwWq3/tWtwIiIiInbg7++vBLaIiIiI
iMhFqkNrkSnAW1ardYXVat0L/Bk4DYy1b1giIiIiIiIiIiIiUh3YNZFtMBjqAMHAugtjVqvVCqQC
IfaKS0RERERERERERESqD3tXZDcEjMDhS8YPU9YvW0RERERERERERERucXbvkX0VBsD6exOmTJlC
/fr1y40NHz6c4cOHV2ZcIiIiIiIiIiIiInKJxMREEhMTy439/PPPFXZ9Q1knD/s431rkNDDYarV+
dtH4cqC+1WodeIVzgoCsrKwsgoKCqixWEREREREREREREbl22dnZBAcHAwRbrdbsm7mWXVuLWK3W
c0AW0PvCmMFgMJzf32yvuERERERERERERESk+qgOrUUWAvEGgyEL2AZMAZyB5fYMSkRERERERERE
RESqB3sv9ojVal0NTANigRygLRButVr/Y9fAREREKlF6ejoODg6cOHHC3qGIiIiIiIiIVHt2T2QD
WK3W/89qtXpbrVYnq9UaYrVaM+0dk4iISEUKDQ1l6tSp5cbKumndnBYtWhAXF3fT1xERERERERGp
zqpFIltEpCJcKVFob2PGjGHQoEH2DkNEREREREREpEZTIltERKSSjRkzhvT0dJYsWYKDgwNGo5H9
+/cDkJmZSadOnahXrx5du3bFbDbbztu3bx8PPvggjRs3xtXVlXvuuYd169bZjoeGhlJQUMCUKVNs
1xURERERERGpjZTIFhERqWRLliwhJCSECRMmcPjwYQ4ePEjTpk2xWq3MmjWLRYsWkZWVhaOjI+PG
jbOdd/LkSR544AHS0tL4/vvviYyMpH///hw4cACAjz/+mCZNmvDSSy9x6NAhDh48aK9HFBERERER
EalUSmSLSK1SUlLCxIkTcXd3x8PDgxdeeMF27P3336dTp064ubnh5eVFTEwM//nPb+vKHj9+nJiY
GDw9PXF2dqZly5bEx8fbji9atIi6detiMplo2LAhDz74IAUFBbbjpaWlTJ06FZPJhIeHB8888wxW
q7VqHlyqNTc3N+rWrYuzszMeHh54enpiNBoxGAzMnTuXbt260apVK2bOnMnmzZs5e/YsAG3btmXC
hAkEBgbi6+vL7Nmz8fHx4bPPPgPAZDJhNBpxcXHB09MTT09Pez6miIiIiIiISKVRIltEapXly5dT
p04dvvvuO+Li4li4cCHvvvsuAOfOnWPOnDns2LGDTz/9lIKCAh555BHbubNmzWLv3r2kpKSwd+9e
/t//+380bNgQKEuQL1iwAIPBwKZNm9i0aROurq5ERERQUlICwIIFC1ixYgXLly/n22+/pbi4mDVr
1lT5ayA1S5s2bWzbXl5eABw5cgSAU6dOMX36dAIDAzGZTLi6urJ3714KCwvtEquIiIiIiIiIvTja
OwARkYrUrFkzFi5cCIC/vz87duxg0aJFjBs3rlzS2tvbm8WLF9O5c2dOnz6Ns7MzRUVFdOjQgQ4d
OtiudcGqVasAqFevHoGBgQC8++67mEwm1q9fT1hYGEuWLOG5555jwIABALz55pukpKRUxWNLDVan
Th3btsFgAMqq+wGmTZvGunXreO211/D19cXJyYnBgwfbKrZFREREREREbhWqyBaRWqVLly7l9kNC
QsjNzcVqtZKVlUX//v1p3rw5bm5u9OzZE4DGjRsD8Nhjj/H+++9jMBgICQlhy5YtAEyYMIFXXnmF
w4cPc+zYMZydnTEajdx2222cOXOGnJwcTpw4wcGDB+nUqROxsbE0bdqUevXqceLECQ4fPlylr4FU
T3Xr1sVisVzXOZs3b+aRRx6hf//+tG7dGk9PT9sikTdzXREREREREZGaRolsEbklnDlzhoiICNzd
3WQ7wT0AACAASURBVPnggw/IzMy0tf04ffo0OTk5RERE8MILL+Dq6kp+fj69e/fm6aefJj09HQ8P
D7y9valTpw7BwcF88sknfP755/j6+pKVlWW7zz/+8Q8WLVrEwoUL2blzJ40aNWLLli3k5+fb69Gl
mvD29mbr1q0UFBRw9OhRSktLr9hD/eIxf39/Pv74Y7Zv38727duJiYm57Bxvb282bNjATz/9xNGj
Ryv9OURERERERETsQYlsEalVMjIyyu1v2bIFf39/9u7dy9GjR3nllVfo2rUrAQEBtkppf39/1q9f
D8B3333HX/7yF3755Rfmz5/PW2+9RX5+Pn369OHw4cOUlJSwcuVK+vXrR9++fZk6dSobNmywLSAZ
Hx/PzJkzGTJkCD4+Pvz666+4u7uzePHiqn4pbilnz55l0qRJNGrUCCcnJ+677z4yMzMBSE9Px8HB
gbS0NDp16kS9evXo2rUrubm5VRrj9OnTMRqNBAYG4unpSWFhoa2VyMUuHlu4cCEmk4muXbsyYMAA
IiIiCAoKKjc/NjaW/fv34+vrq8UeRUREREREpNZSIltEapWioiKmT5+O2WwmMTGRpUuX8tRTT9Gs
WTPq1q1LXFwcP/74I5999hlz5swBoFOnTqxfv54XX3yR1NRUOnbsSPPmzXn//fdp1KgRd955J089
9RQuLi44ODhw4MAB9u/fz/r16/nyyy9tCfE///nPnDhxAovFwg8//MDjjz/O8ePHadCgAXv27LHn
y1LrzZgxgzVr1rBy5UpycnLw8/MjIiKC48eP2+bMmjWLRYsWkZWVhaOjI2PHjq3SGP39/dm0aROn
Tp3CYrEwevRoLBYLbm5utjnt2rXDYrHY+rM3b96c1NRUTp48yf79+3nsscdIS0uz9YEH6Ny5Mzk5
OZw5c0YtRkRERERERKTWUiJbRGoNg8HAqFGjOHPmDPfccw8TJ05kypQpjB8/noYNGxIfH89HH31E
69atmT9/Pq+99hoAHTt2ZOPGjRw9epQzZ84wYMAACgsLKS4uplOnTvTs2RMnJyeee+45jEYjgwcP
JjAwkAkTJlBSUmJr9TBx4kQAXnnlFe69917c3NwYNGgQVqv1ipW3UjFOnz7Nm2++yYIFC+jTpw+t
WrVi2bJl3H777bz77ru2eXPnzqVbt260atWKmTNnsnnz5hq7aKLZbGbt2rVVXlUuIiIiIiIiYi+O
9g5ARKSipKWl2bbfeOONy44PGzaMYcOGlRuzWCwcP36cqVOncurUKYYOHcr777/PJ598wvz588nO
zmbatGkAuLm5Ua9evXKLN3766ad8/fXXALi7u3PXXXfx5JNPMnPmTNuczp07c/fdd1fos8pv8vPz
KSkp4d5777WNOTo6cs8997Bnzx46duyIwWCgTZs2tuNeXl4AHDlyhCZNmlR5zDequLiY6OiRpKQk
2cbCw6NITEzAZDLZMTIRERERERGRyqWKbBG55bm7u9OmTRsSEhLo2bMnAD169CArKwuz2WwbuxYz
Zszg1VdfZfXq1ZjNZmbOnMn27duZPHly5QQvtor4S6veL62Er1Onjm37wnhpaWkVRFhxoqNHkpqa
ASQAhUACqakZDB8+ws6RiYiIiIiIiFQuJbJFRICePXtSWlpqS1qbTCYCAwPx8vLCz8/vmq8TERFB
v379eOqpp2jbti1fffUVn3/+Ob6+vpUUufj5+VGnTh2+/fZb21hJSQmZmZm1qhLebDaTkpKExRIH
xABNgRgsliWkpCSpzYiIiIiIiIjUakpki4gAixYtwmKx4O/vbxvLycnhwIEDtv3Ro0dTXFxc7rwB
AwZgsVgoLi4mIuIBWrVqxcqVKzl48CA9e/Zm3bp13H///VX2HLciZ2dnHnvsMWbMmEFKSgq7d+9m
/PjxnDlzhnHjxgG/VW1f7Epj1Vl+fv75re6XHOkBQF5eXpXGIyIiIiIiIlKVlMgWEakAavlgX/Pm
zWPw4MGMGjWKjh07sm/fPr766ivq168PXN525Gpj1dlvVf0bLjmSDnBd3xwQERERERERqWmUyBYR
uUlq+WB/t912G4sXL+bw4cOcPn2aDRs2EBQUBJT1O7dYLLi5udnmt2vXDovFQrNmzewV8nULCAgg
PDwKo3ESZR+YFAEJGI2TCQ+PKvdtgtogJSWF++67D5PJRMOGDenXrx/79u0DoKCgAAcHB9asWUOv
Xr2oV68e7du3JyMjA4DTp09Tv359Pv7443LXXLNmDS4uLpw6darKn0dERERERERujhLZIiI3SS0f
qjez2czatWtrxQcKiYkJhIV1AUYCzYCRhIV1ITExwc6RVbxTp04xbdo0srKySEtLw2g0MnDgwHJz
Zs2axdNPP8327dsJCAggOjqa0tJSnJ2defjhh3nvvffKzY+Pj2fo0KHUq1evKh9FREREREREKoCj
vQMQEanpHBwufCa4gbKK7AvKWj44OuqvWnsoLi4mOnokKSlJtrHw8CgSExMwmUx2jOzGmUwmkpO/
JDc3l7y8PPz8/GpdJfYFgwYNKre/bNkyGjVqxO7du22J6BkzZhAREQHA7Nmz+dOf/kReXh4BAQGM
Hz+erl27cujQIRo3bsx//vMfkpKSSEtLq/JnERERERERkZunimwRkZtUWlpK2V+n5Vs+wGTAgZKS
EjtGd+uqzX3L/f39iYyMrLVJbCj7JkN0dDS+vr7Ur18fHx8fDAYDhYWFtjlt2rSxbXt5eWG1Wjly
5AgAnTp1IjAwkBUrVgCwcuVKvL296datW9U+iIiIiIiIiFQIJbJFRG5S2SJ8pVxo9VD+91ItwmcH
6lte8/Xt25djx47xzjvvsG3bNrZu3YrVauXs2bO2OXXq1LFtX1i8s+yDpTLjx4+3tReJj49n7Nix
VRS9iIiIiIiIVDQlskVEbtJvi/AVAn8D4oG/YTQW1spF+GoC9S2v2YqLizGbzcyaNYvQ0FBatmxJ
cXHxdV9nxIgRFBYW8vrrr7N7925GjRpVCdGKiIiIiIhIVVDjVhGRCpCYmMDw4SNISZlhGwsLi6qV
i/DVBGVV8nC1vuWqkq/eTCYTDRo04O2336Zx48YUFBTw7LPP2qqur5W7uzsDBw5kxowZhIeHc+ed
d1ZSxCIiIiIiIlLZVJEtIlIBLizCZzabSUpKwmw2k5z8ZY1dVLCm+61KvnzfcqNxsqrkawCDwcCq
VavIysqiTZs2TJs2jQULFtiOXfz7peddaty4cZw9e1ZtRURERERERGo4VWSLiFQgf39/JUmrid+q
5EfaxlQlX3P06tWLXbt2lRuzWCxX3AaoX7/+ZWMABw4coGHDhvTv379yAhUREREREZEqoUS2iIjU
Sheq5HNzc8nLy8PPz08fMtxCduzYQWZmJvPmzePPf/4zjo76J49cv9DQUDp06MDChQvtHYqIiIiI
yC1P/6sTEZFaTVXyt5bi4mKio0eSkpJkG9uyZRvHjh1Tqx8REREREZEaTD2yRUREpNaIjh5JamoG
Zb3RC4EEvvnmO4YPH2HnyKS6CA0NZerUqfYOQ0RERERErpMS2SIiIlIrmM1mUlKSsFjigBigKRCD
xbKElJQkcnNz7Ryh1ESlpaU888wzNGjQAC8vL2bPnm07tmjRItq2bYuLiwvNmjXjiSee4NSpU7bj
hYWF9O/fnzvuuAMXFxfatGlDcnKyPR5DRERERKTGUyJbREREaoX8/PzzW90vOdIDgLy8vCqNR2qH
+Ph4XFxc2LZtG/Pnzyc2NpZ169YBYDQaef311/nXv/7FihUr+Oabb3jmmWds5z7++OOcPXuWb7/9
ll27dvHqq6/i4uJir0cREREREanRlMgWERGRWsHX1/f81oZLjqQD4OfnV6XxSPV1rVXWW7ZswdnZ
malTp+Lr68uAAQOwWq0sW7YMgEmTJtGjRw+ysrLo378/zz//PKtXr+bAgQMMGzaMtWvXsmHDBp57
7jkMBgNRUVF069bNXo8tIiIiIlKjKZEtIiIitUJAQADh4VEYjZMo65FdBCRgNE4mPDxKi36KzbVW
Wd99992cOXPGVmXt5uaGl5cXWVlZAKSmphIWFsaIESP49ddfGTduHEePHuX++++nfv36/PWvf6Wk
pITNmzcTHBxMTk6O3Z5ZRERERKSmUyJbREREao3ExATCwroAI4FmwEjCwrqQmJhg58ikOmnbti3P
P/88vr6+jBw5ko4dO9oS2ReqrJs3b467uztdu3Zl9erVtnObNm1KQUEBP/zwA/369SMwMJDS0lKW
LVvGG2+8gdVqpbS0lLfffpvnn3+eH3/8kb/+9a8cP36czp0788Ybb9jrsUVEREREajRHewcgIiIi
UlFMJhPJyV+Sm5tLXl4efn5+qsSWy7Rt27bcvpeXF0eOHAHKqqznzZvH3r17OXToEABWq5UzZ87g
5OREo0aNMBgMvP3225SWltKhQwdMJhOjRo3i5ZdfBsr6tbu6ul523969e7Ns2TKeeOKJSn5CERER
EZHaRxXZIiIiUuv4+/sTGRmpJLZcUZ06dcrtGwwGSktLKSgooF+/frRv356PP/6Yjh070rt3bwDO
nTsHgIODA97e3mRnZ1NSUsKrr75KZGQkCQkJvPXWWwB06NCBHTt2MGTIEJYuXcqXX37Jxx9/zNGj
RwkMDKzahxURERERqSVUkS0iIiIiAmRlZVFaWsqCBQsAcHZ25uTJk5fN8/X1JS0tjaeffpp58+ZR
WFjIoUOHmDdvHiNHjiQ/Px8PDw9cXFx4+eWXOXDgAG5ubkRGRrJw4cKqfiwRERERkVpBFdkiIiIi
IoCfnx8lJSXExcXx448/MmbMGAoLC8vNWbNmDUlJSXh6epKcnExAQACnT58mKSmJmJgYTp06haen
JwMGDGDo0KF89dVXJCUlMWzYMF5++WVMJpOdnk5EREREpGZTIltEROQ6paen4+DgwIkTJ+wdiohc
J4PBcNVjbdu2ZeHChcyfP582bdqQmJjIvHnzrjh3+PDh7Nixg5iYmHLjTk5ObNiwgWbNmjF48GAC
AwOZMGEC//vf/3Bzc6vQZxERERERuZUYrFarvWO4LgaDIQjIysrKIigoyN7hiIjILSA0NJQOHTrY
WgKkp6fTq1cvjh07dsslpi59LUTk6sxmM/n5+Vp0VERERERuWdnZ2QQHBwMEW63W7Ju5liqyRURE
qomSkhJ7hyAiFWDbtm0EB99Dy5YtiYqKIiAggIiIBzh27Ji9QxMRERERqbGUyBYREfkdY8aMIT09
nSVLluDg4IDRaGT//v0AZGZm0qlTJ+rVq0fXrl3Jzc0td+6nn35KcHAwTk5O+Pn5ERsbi8VisR13
cHDgzTffZMCAAbi4uDB37lwAdu3aRVRUFK6urjRu3JhRo0Zx9OjRKntmEbkxxcXFREQ8QOfOIWRn
m4EEoBBIIDU1g+HDR9g5QhERERGRmkuJbBERkd+xZMkSQkJCmDBhAocPH+bgwYM0bdoUq9XKrFmz
WLRoEVlZWTg6OjJ27Fjbed9++y2jR49mypQp7N27l7feeov4+HhbsvqC2bNnM2jQIHbt2sXYsWP5
+eef6d27N8HBwWRnZ5OSksKRI0cYNmxYVT/6VZWUlDBx4kTc3d3x8PDghRdesB07e/Ys06dPp0mT
Jri4uBASEkJ6erodoxWpOtHRI/n6601AKfAGEAM0BWKwWJaQkpJ02QdeIiIiIiJybZTIFhER+R1u
bm7UrVsXZ2dnPDw88PT0xGg0YjAYmDt3Lt26daNVq1bMnDmTzZs3c/bsWaAsQf3ss88yYsQImjdv
Tu/evYmNjeXNN98sd/2YmBhGjx6Nt7c3TZo0YenSpQQFBfHSSy/h7+9Pu3bteOedd0hLSyMvL88e
L8Flli9fTp06dfjuu++Ii4tj4cKFvPvuuwA88cQTbN26ldWrV7Nz506GDBlCZGQk+fn5do5apHKZ
zWZSUpIoLX30/Ej3S2b0AKg272MRERERkZrG0d4BiIiI1FRt2rSxbXt5eQFw5MgRmjRpwvbt29m8
eTNz5syxzbFYLJw9e5Zff/2V22+/HeDCohc227dvJy0tDVdX13LjBoPBtmicvTVr1sy22KO/vz87
duxg0aJF9OnTh+XLl1NUVETjxo0BmDp1KmvXruW9994r91qI1Da/fVjzAPA3YANlFdkXlH0zoTq8
h0VEREREaiIlskVERG5QnTp1bNsGgwGA0tJSAE6ePElsbCyDBg267LwLSWyAevXqlTt28uRJ+vfv
z/z587FareWOXUiW21uXLl3K7YeEhLBw4UJ27tyJxWIhICCgXOxnz56lYcOGVR2mSJXy9fU9v3UA
iAImAVbKKrHTMRonExYWhb+/v71CFBERERGp0ZTIFhER+QN169Ytt0jjtQgKCuKHH37Ax8fnus/7
+OOPad68OQ4ONasD2KlTp3B0dCQ7O/uy2F1cXOwUlUjVCAgIIDw8itTUSVgsc4FfgZG242FhUSQm
JtgtPhERERGRmq5m/Q9ZRETEDry9vdm6dSsFBQUcPXqU0tLSy6qlgXJjL7zwAitWrCA2Npbdu3ez
d+9eVq1axfPPP/+793riiScoLi7m4YcfJjMzk3379pGSksLYsWOveE97yMjIKLe/ZcsW/P396dCh
AyUlJRw+fBgfH59yvzw9Pe0UrUjVSUxMICysC/BnIA2AoKCOfPfddyQnf4nJZLJrfCIiIiIiNZkS
2SIiIn9g+vTpGI1GAgMD8fT0pLCw0NZK5GIXj/Xp04cvvviCr7/+mnvuuYeQkBAWL16Mt7f3Fedf
4OXlxaZNmygtLSU8PJy2bdsydepUTCbTFefbQ1FREdOnT8dsNpOYmMjSpUt56qmn8PPzIyYmhlGj
RrFmzRr279/Ptm3bmDdvHmvXrrV32CKVzmQykZz8JWazmaSkJMxmM1lZ39GxY0d7hyYiIiIiUuMZ
qkt117UyGAxBQFZWVhZBQUH2DkdEROSW0qtXL1q3bk1paSnvv/8+jo6OPP7448TGxgJlC1rOmTOH
FStW8O9//5sGDRoQEhLC7Nmzad26tZ2jFxERERERkaqUnZ1NcHAwQLDVas2+mWspkS0iIjflo48+
IjY2lry8PJydnQkKCuLTTz/FycnJ3qHVWGazmfz8fPz8/LQwnIiIiIiIiNRYFZnIVmsRERG5YYcO
HSI6Oprx48ezd+9e0tPTGTRoULXp5VzTFBcXExHxAC1btiQqKoqAgAAiIh7g2LFj9g7tmpnNZtau
XUtubq69QxEREREREZFaRIlsERG5YQcPHsRisTBw4ECaNWtG69at+fOf/4yzs7O9Q6uRoqNHkpqa
ASQAhUACqakZDB8+ws6R/bHakIQXERERERGR6kuJbBERuWHt2rWjd+/e/OlPf2Lo0KG88847HD9+
3N5h1Uhms5mUlCQsljggBmgKxGCxLCElJanaVzjX5CS8iIiIiIiIVH9KZIuIyA1zcHDgq6++Ijk5
mdatW/P666/TqlUrCgoK7B1aOaGhoUydOtXeYfyu/Pz881vdLznSA4C8vLwqjed61PQkvIiIiIiI
iFR/SmSLiMhNCwkJ4cUXXyQnJ4c6deqwZs0ae4dUoQoKCnBwcGDHjh2Vdg9fX9/zWxsuOZIOgJ+f
X6Xd+2bV5CS8iIiIiIiI1AyO9g5ARERqrm3btrFu3Tr69OmDp6cnGRkZ/Pe//yUwMNDeoVUoq9WK
wWCo1HsEBAQQHh5FauokLBYrZUngdIzGyYSFReHv71+p978Z5ZPwMRcdqf5JeBEREREREakZVJEt
IiI3zM3NjQ0bNvDAA2WL/L3wwgssXLiQPn362Du0y5SUlDBx4kTc3d3x8PDghRdesB1zcHDgs88+
KzffZDKxYsUKAHx8fABo3749Dg4O9OrVq1JiTExMICysCzASaAaMJCysC4mJCZVyv4pyIQlvNE6i
rEd2EZCA0TiZ8PDqnYQXERERERGRmkEV2SIicsNatWrF2rVr7R3GNVm+fDnjx4/nu+++IzMzkwkT
JtC8eXPGjRv3h+du27aNe+65h7S0NAIDA6lbt26lxGgymUhO/pLc3Fzy8vLw8/OrMUngxMQEhg8f
QUrKSNtYWFhUtU/Ci4iIiIiISM2gRLaIiFw3s9lMfn5+jUq0NmvWjIULFwLg7+/Pjh07WLRo0TUl
sj08PAC444478PT0rNQ4oSy+mvK6XlCTk/AiIiIiIiJS/am1iIiIXLPi4mIiIsraiERFRREQEEBE
xAMcO3bM3qH9oS5dupTbDwkJITc3l9LSUjtFVDv5+/sTGRmpJLaIiIiIiIhUKCWyRUTkmkVHjyQ1
NYOyPsiFQAKpqRkMHz7CzpHdHIPBgNVqLTd27tw5O0UjIiIiIiIiIpdSIltERK6J2WwmJSUJiyUO
iAGaAjFYLEtISUkiNzfXzhH+voyMjHL7W7Zswd/fHwcHBzw8PDh48KDtWG5uLqdPn7btX+iJbbFY
qiZYqVTx8fGYTCZ7hyEiIiIiIiLXQYlsEbklhYaGMnXqVHuHUaPk5+ef3+p+yZEeAOTl5VVpPNer
qKiI6dOnYzabSUxMZOnSpTz11FMA9OrVi6VLl/L999+TmZnJY489Vm5BR09PT5ycnEhOTubIkSOc
OHHCXo8hFcRgMNg7BBEREREREbkOSmSLiMg18fX1Pb+14ZIj6QD4+flVaTzXw2AwMGrUKM6cOcM9
99zDxIkTmTJlCuPHjwfgtddeo2nTpnTv3p0RI0YwY8YMnJ2dbecbjUZef/113nrrLe666y4efPBB
ez2KiIiIiIiIyC1JiWwRkVqqons8BwQEEB4ehdE4ibIe2UVAAkbjZMLDo6r14n5paWm8/vrrvPHG
Gxw/fpz//ve/xMbG2o57eXmxdu1aTpw4wd69ewkPD6e4uJhRo0bZ5owdO5b9+/dz7tw50tLS7PEY
t6SUlBTuu+8+TCYTDRs2pF+/fuzbtw+AgoICHBwcWLNmDb169aJevXq0b9/+sjYyy5cvp3nz5ri4
uDB48GCOHj1qj0cRERERERGRm6BEtojcskpLS3nmmWdo0KABXl5ezJ4923asqKiIAQMG4OrqSv36
9Rk2bBhHjhwB4MSJEzg6OpKTk2Obf8cdd9C1a1fbfkJCAs2aNbPtHzhwgGHDhtmScQ8++CAFBQUA
fPXVVzg5OV3WrmLSpEncf//9tv1vv/2W7t274+zsTPPmzZk8eXK5Ps4tWrRgzpw5jB49Gnd3d/7v
//6vgl6p3yQmJhAW1gUYCTQDRhIW1oXExIQKv1d1YDabWbt2bZX1/1bLm8udOnWKadOmkZWVRVpa
GkajkYEDB5abM2vWLJ5++mm2b99OQEAA0dHRlJaWArB161bGjx/PpEmT+P777wkNDWXOnDn2eBQR
ERERERG5CUpki8gtKz4+HhcXF7Zt28b8+fOJjY1l3bp1AAwYMIDjx4+zceNGUlNTyc/P5+GHHwbA
zc2NDh06sH79egB27NiBg4MD2dnZtsTyhg0b6NmzJwAlJSWEh4dTv359Nm3axKZNm3B1dSUiIoKS
khLCwsIwmUz885//tMVWWlrKP/7xD0aMGAGU9aeOjIxkyJAh7Nq1i1WrVrFp0yYmTpxY7plee+01
2rdvT05ODs8//3yFv2Ymk4nk5C8xm80kJSVhNptJTv6y1i2cV1xcTETEA7Rs2ZKoqCgCAgKIiHiA
Y8eO2Tu0W86gQYN48MEH8fHxoW3btixbtoydO3eye/du25wZM2YQERGBn58fs2fPpqCgwNazPS4u
jsjISKZNm4afnx9PPvkk4eHh9nocERERERERuUFKZIvILatt27Y8//zz+Pr6MnLkSDp27Mi6detI
TU1l165dJCYm0r59ezp16sTKlStZv349WVlZAHTv3t2WyF6/fj3h4eG0atWKTZs22cYuJLI//PBD
rFYrb7/9NoGBgbRs2ZJ3332XwsJC1q9fj4ODA0OHDuWDDz6wxZaamsrPP//MoEGDAJg3bx4jRoxg
4sSJ+Pj40KVLFxYvXkx8fDxnz561nde7d2+mTJlCixYtaNGiRaW9dv7+/kRGRlbrdiI3Izp6JKmp
GZS1UCkEEkhNzWD48BF2jqxyVOdK8Ly8PKKjo/H19aV+/fr4+PhgMBgoLCy0zWnTpo1t28vLC6vV
avsGxZ49e+jcuXO5a4aEhFRN8CIiIiIiIlJhlMgWkVtW27Zty+17eXlx5MgR9uzZQ9OmTbnzzjtt
x+6++27c3d3Zs2cPAD179mTjxo0ApKen07NnT3r27Mn69es5ePAgeXl5tkT2jh07yM3NxdXV1far
QYMG/O9//yM/Px+AmJgY1q9fz6FDhwD44IMP6Nu3L66urgBs376d5cuX2853dHSkV69eAPz444+2
OIODgwFwcHDgs88+q+iX7JZgNptJSUnCYokDYoCmQAwWyxJSUpIqvc3I77W8+fnnnxk/fjyenp7U
r1+fsLAwduzYcdP3XLNmDS+99BJQ1qImLi7upq9ZUfr27cuxY8d455132LZtG1u3bsVqtZb7AKdO
nTq2bYPBAGBrLWK1Wm1j1+rRRx+lQYMGGI3GCnl9RURERERE5OYpkS0it6yLk19QlgArLS29auLr
4vH77ruPX375haysLDZu3EjPnj3p0aMH33zzDenp6dx11134+PgAcPLkSTp27MiOHTvYvn277ZfZ
bCY6OhqATp064ePjw4cffsivv/7KmjVrbG1FLlzj//7v/2zX6NixIyNGjMBsNuPr62ubV69ePQAO
HTpEZGRkxb5gt4gLHy5A90uO9ACwtayoLL/X8uahhx7i6NGjpKSkkJ2dTVBQEGFhYRw/fvym7unu
7m772alOiouLMZvNzJo1i9DQUFq2bElxcfF1XSMwMPCyxR+3bNly1fnJycmsWLGCpKQkDh48yJ/+
9Kcbil1EREREREQqlqO9AxARqW4CAwMpKCjg3//+N3fddRcAu3fv5ueff+buu+8GyhJ/bdq0M06u
VgAAIABJREFUYenSpdSpUwd/f38aNmzIww8/zBdffEGPHj1s1wsKCmL16tV4eHjg4uJy1ftGR0eT
kJDAXXfdhaOjY7lEdFBQEP/6179s7UKcnJxwd3e3Jcsv5enpedOvw63qtw8GNlBWkX1BOgB+fn6V
ev8LLW8uxLJ06VLWrVvH7bffTmZmJkeOHLF9CDN//nzWrFnDRx99xPjx42/4nqGhobRv357vv/+e
goICpkyZwlNPPYXBYMBisVTIc90Ik8lEgwYNePvtt2ncuDEFBQU8++yz11VhPWnSJLp168Zrr73G
gAEDSE5OJiUl5arz8/Ly8PLyuqwdyQXnzp277EMwERERERERqXyqyBYRuURYWBht27YlJiaGnJwc
tm3bxujRowkNDSUoKMg2r0ePHiQkJNhaiJhMJlq1asWqVatsY1DWNqRhw4YMGDCAb7/9lv3797N+
/XomT57MTz/9VG5ednY2L7/8Mg899FC5ZNkzzzzDli1bmDhxItu3b+f06dPk5uYSHBxsa0FxcVXu
xa1Fzp07x5NPPsmdd96Jk5MTPj4+vPrqq5X06tV8AQEBhIdHYTROoqxHdhGQgNE4mfDwqErvC361
ljfbt2/nl19+4Y477ijXpmb//v0XVZHfOIPBwJo1a2jSpAkvvfQShw4d4uDBgzd93ZuNadWqVWRl
ZdGmTRumTZvGggULbMcu/v3S8y7o3Lkzy5YtIy4ujvbt25OamnrVhVDHjBnDpEmTKCwsxMHBAR8f
H0JDQ5k4cSJTpkzBw8ODiIgIAIqKihgwYACurq7Ur1+fYcOG2fpyA8yePZsOHTrw3nvv0bx5c1xd
XXnyyScpLS1l/vz5eHl50ahRI+bOnVthr5eIiIiIiEhtpopsEbkl/VFF5yeffMKkSZPo0aMHDg4O
REZGXtY3uGfPnsTFxREaGmobCw0NZefOneUqsp2cnNiwYQPPPPMMgwcP5pdffuGuu+6id+/euLm5
2eb5+fnRqVMnMjMzWbJkSbl7tWnThvT0dP7yl7/QvXt3Tp06Zbvf6tWr2bx5M6NGjcJsNl/2LEuW
LOGLL77go48+omnTphQVFVFUVHTtL9YtKDExgeHDR5CSMtI2FhYWRWJiQqXf+2otb06ePMmdd95J
eno6Vqu13Bx3d/cKube7uztGoxEXF5dqU9Xfq1cvdu3aVW7s4irxSyvG69evf9nYI488wiOPPFJu
bMqUKZfdKy4uDl9fX5YtW0ZmZiYODg489NBDrFixgscee4zNmzfb5l5IYm/cuJFz587x2GOP8fDD
D5OWlmabk5+fb6sAz8/PZ/DgweTn59OyZUs2bNjApk2bGDt2LPfffz+dOnW67tdGRERERETkVqJE
tojcki5ONl2wZs0a23bTpk3L7V/JgAEDLkuYLVq0iEWLFl0219PTk/fee+8P49q6detVjwUHB5Oc
nAyUJbBLS0v5+uuvgd9aUFycGL+gqKgIf39/7r33XqDs2eT3mUwmkpO/JDc3l7y8PPz8/Cq9EvuP
BAUFcejQIYxGI82aNbNrLDWN2WwmPz//D/8cL1S5G41GPDw8bON+fn7MmzfPtv/111+za9cu9u/f
b1sUduXKlbRu3ZqsrCzboqtWq5X33nsPZ2dnWrVqRWhoKGazmbVr1wLg7+/Pq6++yjfffPO7iexH
H32Uf/7znxw/fpycnJzLqvZFRERERERuBWotIiJSQ7Vt29aWFMvNzbW1oLjUI488Qk5ODi1btmTy
5Mm25Lf8MX9/fyIjI+2exIayljddunThwQcf5Ouvv6agoIDNmzcza9YssrOz7R1etVRcXExExAO0
bNmSqKgoAgICiIh4gGPHjl3XdTp27Fhuf+/evTRt2tSWxAa4++67cXd3Z8+ePbYxb29vnJ2dbfuN
GjUiMDCw3LUaNWp0xfftBVp8UkREREREpIwS2SIiNVBJSQmff/5FuQTdli0ZnDlz5rK5HTp0YP/+
/cyZM4dff/2VoUOHMnToUDtELX/kj1rerF27lu7duzN27FhatmxJdHQ0hYWFNGrUqMJiqFu3rl0X
eKxI0dEjSU3NoKzXeSGQQGpqBsOHj7iu69SrV6/cvtVqveKf1aXjV2oTc7XWMVdz8eKTnp6eODhc
/z/dasufp4iIiIiI3NqUyBYRqYH+9a/dFBYe5OIE3ZEjxaSnb7jifBcXF4YMGcJbb73FqlWrbG0K
pHpJS0tj4cKF5cbWrFnD3//+d6Asobp48WKKior49ddf2b9/PytWrOCuu+6qsBi8vb3ZsGEDP/30
E0ePHq2w61Y1s9lMSkoSFkscEAM0BWKwWJaQkpJEbm7uDV87MDCQwsJC/v3vf9vGdu/ezc8//3xZ
xfXNuNLik2fPnmXSpEk0atQIJycn7rvvPjIzM23npKen4+DgQHJyMh07duT2229n06ZNFRaTiIiI
iIiIvSiRLSJSw5jNZo4dK8ZqDeXiBB205d//PnBZgm7x4sWsWrWKH374AbPZzOrVq2ncuHGFLRAo
VefiVjIV6eIq4tjYWPbv34+vr2+1WfDxRuTn55/f6n7JkbKFWPPy8m742mFhYbRp04aYmBhycnLY
tm0bo0ePJjQ0lA4dOtzwdS8VFxdHbGwsTZo04fDhw3z33XfMmDGDNWvWsHLlSnJycvDz8yM8PPyy
D6aeffZZXn31Vfbs2aOe2iIiIiIiUisokS0iUsP8lqBrcsmRhkBZgu7ixKSLiwuvvvoqnTp1onPn
zhQWFpKUlFQ1wd6kC9WlJ06cuOqc2bNnExQUVIVRVb2K6vV8NRdXgnfu3JmcnBzOnDlTo1tS+Pr6
nt+69FsK6UDZAo7X4mrtXj799FNMJhM9evSgT58++Pn58eGHH153nL/XTubSxSednJx48803WbBg
AX369KFVq1YsW7YMJycn3n333XLnvvTSS/Tu3ZsWLVroQysREREREakVDFar1d4xXBeDwRAEZGVl
ZdX6xIWIyJWYzWZatmxJWVuRmIuOJAAjMZvN1WJxwhtxoaL1QlI1PT2dXr16cezYMdzc3K54zunT
p/nf//6HyWSqylCrVETEA6SmZpxvk9Ed2IDROImwsC4kJ39509c3m83k5+fj5+dXY392ruS3120J
ZZXY6RiNkyvsdasKS5YsYcmSJezbt48dO3bYet43bdrUNmfQoEHccccdvPPOO7b3zIEDB/Dy8rJj
5CIiIiIiIpCdnU1wcDBAsNVqzb6Za6kiW0SkhgkICCA8PAqjcRJlyesiIAGjcTLh4VGXJSIrqx1F
deHs7Fyrk9iV2eu5siu97S0xMYGwsC7ASKAZMJKwsC4kJibYJZ6Kei9eWsV9pcUnL12gUkRERERE
pKZTIltEpAa6lgRdTUtSjhkzhvT0dJYsWYKDgwNGo5H9+/cDkJmZSadOnahXrx5du3bFbDbbzps9
e3a5vsTr16+nc+fOuLi4YDKZuO+++ygqKqrqx6kwldnrOTp6JKmpGVy8aGhqagbDh4+44WtWJyaT
ieTkLzGbzSQlJWE2m0lO/rLKP/ioqPein58fderU4dtvv7WNlZSUkJmZWaGLTIqIiIiIiFRHSmSL
iNRA15Kgq2lJyiVLlhASEsKECRM4fPgwBw8epGnTplitVmbNmsWiRYvIysrC0dGRcePGlTv3QjWq
xWJh4MCBhIaGsmvXLjIyMnj00Ud/tw8xQHx8/B8mN8eMGcOgQYOu6VkKCgpwcHBgx44d1zT/91RU
r+dLVWald3Xj7+9PZGSk3dqmVNR70dnZmccee4wZM2aQkpLC7t27GT9+PGfOnGHs2LG2eTWtbZyI
iIiIiMi1cLR3ACIicuP8/f2vmJy7kKQs30c7BovFSkrKSHJzc6tdL2Q3Nzfq1q2Ls7MzHh4eABiN
RgwGA3PnzqVbt24AzJw5k759+3L27Fnq1q1b7honTpzgxIkTPPDAA3h7ewOc7yf+x/4o2R0XF3dd
CcI/ut61utBKJjV1EhaLlfK9ni9vJXOtrqXSu7r9jNREFf1enDdvHlarlVGjRvHLL7/QsWNHvvrq
K+rXr2+bU1E/eyIiIiIiItWJKrJFRGqhymxHYQ9t2rSxbV9YwO7IkSOXzTOZTIwePZo+ffrQv39/
4uLiOHToUIXE4OrqetUFJ6+kIqtiK6PXc2VVekt5N/tenDx5Mvv27bPt33bbbSxevJjDhw9z+vRp
NmzYUG7x6x49emCxWK7rZ/WPxMfHc8cdd/zhPAcHBz777LMKu6+IiIiIiMjFlMgWEamFaluSsk6d
OrbtC9WmpaWlV5z797//nYyMDO644w6mTp1Ky5Yt2bZtG9u3b8fBwYG//OUvtrkTJkxg9OjRtv2v
vvqKwMBAXF1diYyM5PDhw7Zjl7YWsVqtzJ8/H39/f26//Xa8vb155ZVXysWSn59Pr169qFevHu3b
tycjI+OGnr8yej1f76KhcmOq6r1YmYu6Pvzww7/bl15ERERERKQqKJEtIlIL1dQkZd26dbFYLDd9
nXbt2hEXF4fBYMDb25sPPviA9PR0PDw8WL9+vW1eeno6PXqUVcaeOnWK1157jffff5+NGzdSWFjI
9OnTr3qPmTNnMn/+fF588UX27NnDBx98QKNGjcrNmTVrFk8//TTbt28nICCA6Ojoqybgr0VF93qu
jEpvKa+y34tVsajrbbfdRsOGDcuNqX2JiIiIiIhUNSWyRURqqZqYpPT29mbr1q0UFBRw9OhRSktL
r9ii42ptO/bv389zzz1HRkYGx48fx9vbm/z8fAIDA1m/fj1Tp04lOzub06dP89NPP5Gfn0/Pnj0B
KCkp4a233qJDhw60b9+eJ598knXr1l3xPidPniQuLo6//e1vjBgxghYtWnDvvffi6+uLg4MDv/zy
CwAzZswgIiICPz8/Zs+eTUFBQbVq61IZld5yucp8L97oQpJffPFFuT/n3/vGwsWLocbHxzN79mzb
fKPRyIoVK2zn/Oc//2HQoEHUq1ePgIAAPv/885t+RhEREREREVAiW0Sk1qqJScrp06djNBoJDAzE
09OTwsLCK1Z+Xq0a1NnZmb179/LQQw/RsmVLjhw5QpMmTXj00UfZuHEjgwYNolWrVmzatIn09HTu
vPNOfHx8bOdeWCASynpxX6kPN8CePXs4e/Ysb7/9NlOnTr1qbJf29rZarVe9pj1VdKW3lFdZ78UL
C0laLHGULSTZlLKFJJeQkpL0u21GunfvzsmTJ8nJyQH4w28sXPi5HjZsGNOmTaN169YcPnyYgwcP
MmzYMNs5sbGxPPzww+zcuZOoqChiYmI4fvz4TT2niIiIiIgIKJEtIlLr1aQkpb+/P5s2beLUqVNY
LBZGjx592cJ17dq1w2Kx0KxZMwBefPFFsrOzAfD09OTjjz/mwIEDnDlzhpUrV3LkyBG2b99O3bp1
8ff3p0ePHnzzzTekp6fbqrGhfB9uKEvcXa3y28nJ6Zqe53p6e0vtV9HvxZtZSNLNzY22bdvaEtd/
9I2FC26//XZcXFxwdHTEw8MDT09PbrvtNtvxMWPGMHToUHx8fJg7dy6nTp1i27ZtN/mkIiIiIiIi
SmSLiEgtcumCd927d+fEiRMsXrzYlpDr2bMn69evL1dter38/f0xGAxs3bqVJUuW2Fos7N+/H4Cd
O3ditVrp3LkzXbt2vawy9tNPPyU4OBgnJyf8/PyIjY21JbjHjRtHv379ys0vKSnB09OT5cuX31C8
Ujvd7EKSF94LwB9+Y+FaXfwtBGdnZ1xdXavltxBERERERKTmUSJbRERqvKsteGe1WmnTpg0JCQm2
RHaPHj3IysrCbDZfVm16rW677TaefvppjEYjPXr0YOvWrXzxxRfs2rULq9XKggULAPjwww9xdHRk
7NixtnN37NjB6NGjmTJlCnv37uWtt94iPj6el19+GYDx48eTkpLC4cOHbed8/vnn/PrrrwwdOvTG
XiCplW52IckePXqwcePGa/rGwrW60jcb9C0EERERERGpCEpki4hIjfd7C9717NmT0tJSW1LOZDIR
GBiIl5fXH1as/p65c+fStGlTsrKyuO+++3j88cc5ceIEBoOBGTNm4ODgQIsWLZg5cyabN2/m7Nmz
GAwGli9fzrPPPsuIESNo3rw5vXv3JjY2ljfffBOAkJAQAgICWLlype1ey5cvZ8iQITg7O9/4i3Te
7Nmz6fD/s3fnYVHW6x/H38MIKSqKC6XmArJJoYHpES0RRUHMXCoXVMit8uSSS2mlpmZWngIt6+ep
XONEmuWvX7mQiKJiaiKhmDaABZ7cSvSYoqHD/P4g5jCi5sKqn9d1cZ2Z7/PM97m/k3Bd537u5/76
+d3yPFIx3MpGkjf7xIKDgwNms7nE1iAiIiIiInI9lMgWEZFK7a82vPv73/+O2Wy2qU5NSUnh3//+
t/V9ZGQkOTk5NvP26tXLJlm3ZMkSvvjiC5tzmjZtyvDhw7lw4QI//fQT4eHhAHTt2hWz2UzLli1p
0KABAH/88Qdms5ns7GxmzZpFzZo1rT8jR47k+PHjXLhwASioyl6yZAkAx48fZ926dQwfPrykvrKr
bpYplc+tbCRZu3btm3pioVmzZvz000+kpqZy8uRJ8vLySnBFIiIiIiIiV6ZEtoiIVGq3suFdabG3
t7f2687Ozgb+u8nj2bNnmTlzJqmpqdaftLQ0TCYTVatWBSAiIoJDhw6xc+dOYmJicHNzo3379gAE
BQUxbtw4Jk+eTN26dWnQoAEzZ860Xvvw4cP06tWLmjVrUqtWLfr372/tUbxs2TLrtQv7ei9fvrws
vxopJTe7keTNPLHw2GOPERoaSlBQEC4uLnz66afAlW+Q6KaJiIiIiIiUlCrlHYCIiMitsN3wblCR
I9e34d2tuFqLhb59H2fjxg02Y//5z38A8Pf358cff7zmJnp16tShd+/eLF68mG+//ZahQ4faHF++
fDkTJkxg165dbN++nSeffJKHHnqILl26WJPYW7du5eLFi4waNYoBAwaQkJBA//79SUtLIy4ujo0b
N2KxWKhVq1YJfBNSWUVHRxMdHW0zlpKSYvM+MjKSyMhI63sHBwdWrlxZbK4r/S5c/qSDiIiIiIjI
zVIiW0REKrXCDe/i48diNlsoqMROxGgcR3DwX294dyuaNWvGzp07ycrKokaNGuTn55Ofn8+mTbsp
6NfdEfgYeJnRo8eRmJjA9OnT6dmzJ40bN+bxxx/Hzs7OWpX96quvWucePnw4jzzyCPn5+TZJRICW
LVsybdo0oCCRv2DBAmtiOi0tjZ9//pmGDRsC8PHHH3PfffeRnJxM69atqVGjBlWqVKF+/fql9r3I
nclkMpGZmYm7u3up/t6JiIiIiMidSa1FRESk0ruVDe9uxaRJkzAajfj4+ODi4sKuXbsAyM9/k//2
6+4BGNiyZRPp6el069aNr7/+mg0bNtC2bVsCAgKYN28ezZo1s5k7ODiYBg0aEBoayj333GNzrGXL
ljbvGzRowIkTJzhw4ACNGze2JrEBWrRoQe3atTlw4EDJfwEiFFRdh4b2wMvLi7CwMDw9PQkN7cGp
U6fKOzQREREREbmNqCJbREQqvcIN79LT08nIyCizilAPDw+SkpKs79etW/fnq9AiZ7UCsoAmZGRk
4OHhQdeuXenates1587NzeXUqVNX3OTR3t7e5r3BYCA/Px+LxXLFnsRXGxcpCeHhQ4iP38F/n0LY
Qnz8WAYOHMz69WvKOToREREREbldKJEtIiK3DQ8Pj3JtaVAS/botFgs7duwgKiqKmjVr0rNnz+u+
vo+PD1lZWfzyyy80atQIgB9++IH//Oc/+Pj4AFfv6y1yM0wmE3FxaylIYhf+mx+E2WwhLm4I6enp
ajMiIiIiIiIlQq1FRERESkhhv26jcSwFib3DQAxG4zhCQv66X3dOTg6dOnWhffv2rFq1in//+9+E
hfW87hYNwcHBtGzZkkGDBpGSksKuXbuIjIwkKCgIPz8/oKCv908//URqaionT54kLy/v1hYtd7TM
zMw/X3W87EggABkZGWUaj4iIiIiI3L6UyBYRkTIRFBTE2LFjGT9+PHXq1OGee+5h0aJF5ObmMmzY
MJycnPDw8GD9+vUA5OfnM2LECNzc3HB0dMTb25t33nnHZs6hQ4fSp08f3n77bRo2bEi9evUYPXq0
teL41VdfLdZPGuCBBx5gxowZpbLOW+nXHR4+hKSkVAqS4NlADPHxOxg4cLD1nL9qEfK///u/ODs7
ExgYSLdu3XB3d+fTTz+1Hn/ssccIDQ0lKCgIFxcXm2MiN8r2KYSirv8pBBERERERkeuh1iIiIlJm
li9fzgsvvMB3333HihUreOaZZ/jiiy/o27cvL7/8MlFRUQwZMoTDhw9TpUoVGjduzKpVq6hbty7b
t2/nqaeeomHDhjz++OPWOTdt2kTDhg3ZvHkzGRkZ9OvXDz8/P4YPH86wYcOYNWsWycnJtG7dGoCU
lBTS0tL48ssvS2WNN9uv+3pbNCQkJBT77OrVq62vGzdubPP+cg4ODqxcufIGVyVyZYVPIcTHj8Vs
tlBQiZ2I0TiO4OC/fgpBRERERETkehksFkt5x3BDDAaDP5CcnJyMv79/eYcjIiLXKSgoiPz8fBIT
Cyo18/PzqVWrFo899hhLly4F4Pjx4zRo0IAdO3bQtm3bYnOMGTOG48ePWxOxQ4cOJTExkczMTGul
cv/+/TEajXzyyScA9OjRA1dXVxYsWADA2LFj2b9/Pxs3biztJd+QdevWERYWRkElduMiRw4DTVi7
di3du3cvn+BEruHUqVMMHDj4zxsxBUJCwoiNjcHZ2bkcIxMRERERkfK2Z8+ewsKy1haLZc+tzKXW
IiIiUmaKtvmws7Ojbt26+Pr6WsfuvvtuAE6cOAHAe++9x4MPPoiLiws1a9bkgw8+IDs722bO++67
z6bdRoMGDayfBxg5ciSxsbHk5eVx8eJFYmNjGT58eKms71aUdosGk8nEunXrSE9Pv6V5RC5X+BSC
yWRi7dq1mEwm1q9foyS2iIiIiIiUKLUWERGRMmNvb2/z3mAwFBuDgmrtFStW8PzzzxMdHU27du2o
WbMmc+fOZdeuXX85Z35+vvV9z549ueuuu1i9ejX29vZcunSJvn37luCqSkZptWjIyckhPHyIqmWl
1Hl4eKiViIiIiIiIlBpVZIuIlKHExETs7Ow4c+bMLc1jZ2fH//3f/5VQVBVTUlISHTp04Omnn6ZV
q1a4ubmRmZl5w/MYjUYiIiJYvHgxS5YsYcCAAVStWrUUIr51t7JR5NWEhw8hPn4H19pAUkRERERE
RKSiU0W2iEgpCgoKws/Pj6ioKOtY0TYYN+vYsWO3fTWth4cHH3/8Md988w2urq58/PHHfPfdd7i5
ud3wXCNGjKBFixYYDAaSkpJKIdqScbMbRV7N9W4gKSIiIiIiIlLRKZEtIlIJubi4XPP4pUuXqFKl
Yv2Jv1IC/2pjBoOBZ555hu+//54BAwZgMBgYOHAgzz77LOvWrbvha7u7u9O+fXtycnJo06bNTcVf
lkqqRcN/K9g7XnYkEICMjAwlskVERERERKRSUGsREZFSMnToUBITE5k/fz52dnYYjUZ+/vlnAHbv
3k2bNm2oXr06HTp0KLYB35dffknr1q2pVq0a7u7uzJo1C7PZbD1etLVIVlYWdnZ2rFy5kk6dOuHo
6Mgnn3xS6uuLi4vj4YcfxtnZmXr16tGzZ08OHTpkE9Pq1avp3Lkz1atXJycnh379+tnMcejQIcaO
HWszZjab6dmzJ/b29ixatIicnBxOnjzJggULeO2119iz57+bHC9ZsoQvvvjC5vPR0dEkJCQUi/fI
kSOMGDGipJZfKZT2BpIiIiIiIiIiZUWJbBGRUjJ//nwCAgIYOXIkx48f5+jRozRu3BiLxcLUqVOJ
jo4mOTmZKlWqMGzYMOvntm3bRmRkJOPHj+fgwYP885//ZNmyZcyZM+ea13vxxRcZP348Bw4cICQk
pLSXx7lz55g4cSLJyckkJCRgNBrp06ePzTlTp07lhRdeIDU1FU9PT8LDw202YiwLO3bsYNSoURw9
epQnn3yyTK9d3go3kDQax1LQXuQwEIPROI6QkJvfQFJERERERESkrCmRLSJSSpycnHBwcMDR0ZH6
9evj4uKC0WjEYDAwZ84cHnroIby9vZkyZQrbt28nLy8PgJkzZ/Liiy8yePBgmjZtSpcuXZg1axYL
Fy685vXGjx9Pr169aNq0KXfffXepr69v37707t0bNzc3WrZsyYcffsi+ffv44YcfrOc8//zzhIaG
4u7uzsyZM8nKyiIjI6PUYwPIyckhNLQHAQEBLFy4kHPnztG/fzinTp264vmrVq2iZcuWODo6Uq9e
Pbp168b58+exWCzMmjWLxo0bU7VqVfz8/IiLi7N+rrD6/LPPPqNjx444OjrStm1b0tPT+e6772jT
pg01a9YkLCyMkydP2lzzo48+wsfHh2rVquHj48P//M//lPj3UBobSIqIiIiIiIiUNSWyRUTKga+v
r/V1gwYNADhx4gQAqampzJo1i5o1a1p/Cqu6L1y4cNU5W7duXbpBXyYjI4Pw8HCaN29OrVq1cHNz
w2AwkJ2dbT3n8nVaLBbrOktbePgQ4uN3UFCJnA3EEB+/g4EDBxc799ixY4SHhzNixAgOHjxIYmIi
ffv2xWKxMG/ePKKjo4mKimLfvn2EhITw6KOPFuk/XWDGjBlMnz6dlJQUqlSpQnh4OFOmTOHdd99l
27ZtZGRkMH36dOv5//rXv5gxYwavv/46Bw8eZM6cOUyfPp2PP/64RL+Hwg0kTSYTa9euxWQysX79
mtt+s9CSFBQUxIQJE8o7jGsqvKGyd+/e8g5FRERERESkVFSsncBERO4Q9vb21teFGx4Wttw4e/Ys
s2bNom/fvsU+V7Vq1avOWb169RKO8toeeeQRXF1d+eijj2jYsCFms5n777/fWlkO117ys5A2AAAg
AElEQVRnaTKZTMTFraUgiT3oz9FBmM0W4uKGkJ6ebtNW4+jRo5jNZvr06UPjxo0BuO+++wB4++23
mTJlCk888QQAb7zxBps2bWLevHm8++671jmef/55goODARg3bhzh4eEkJCTQrl07AIYPH86yZcus
58+YMYO3336bXr16AdC0aVP279/PwoULGTJkSIl/JyW1geSdaPXq1Tb/lisii8Vyxc1TRURERERE
bheqyBYRKUUODg42mzReD39/f3788Ufc3NyK/VxNWSewcnJyMJlMTJ06laCgILy8vMjJySnTGK7l
v9XSHS87EghQrL1Jq1at6NKlC/fffz/9+vXjo48+4vTp0/z+++8cOXKE9u3b25zfoUMHDhw4YDNW
tPq8sLXL/fffbzNWWI2em5tLZmYmw4cPt6m8f+211/jpp59udtlSSmrXrl3mN4qu5EobrBb+eyn8
+/DAAw9gZ2dH586dyzNUERERERGREqdEtohIKWrWrBk7d+4kKyuLkydPkp+fj8ViKXZe0bHp06ez
fPlyZs2axQ8//MDBgwdZsWIF06ZNu+p1rjRnaXJ2dqZu3bp88MEHZGZmkpCQwMSJEytMRWjz5s3/
fLXlsiOJALi7u9uM2tnZ8c0337B+/Xruu+8+3n33Xby9va1JwsvXdaXq1ytVn18+VrTqHgp6ZKem
plp/0tLS+Pbbb298wZXM9u3badmyJQ4ODld88qCiKdpaxNXVlddff53hw4fj5ORE06ZN+fDDD8sk
jmttsLpr1y4sFgsJCQkcO3aML774okxiEhERERERKStKZIuIlKJJkyZhNBrx8fHBxcWF7OzsKyZ7
i45169aNr7/+mg0bNtC2bVsCAgKYN28ezZo1u+L5V3pf2gwGAytWrCA5ORlfX18mTpzIW2+9ZRPL
X62zNHl6ehISEobROJaC9iKHgRiMxnGEhIRdtcVGQEAAr7zyCikpKdjb27Nx40YaNWrEtm3bbM7b
vn07LVq0sL6/0XW5uLjQqFEjMjMzi1XdN23a9AZXW/lMmDABf39/srKyWLp0aXmHc8OioqJo06YN
33//PX//+98ZNWoUJpOp1K97pQ1W9+7dyw8//ED9+vUBqFOnDi4uLtSuXbvU4xERERERESlL6pEt
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
OzNkyBBcXFwYPXo0VapUYdOmTQDY29sDULlyZRwcHLCxsQHg448/ZsyYMbzwwgu4u7vzwQcf0KRJ
E6ZPn14sY3rS5M+Sv93AgQPp0aNHie27cePGvP3227i6ujJmzBgqVqyIvb094eHhuLq6EhUVRUZG
BikpKXz22Wf4+Pjw7rvv4u7uTuPGjZk7dy4bN27USlj06NGDbt264eLigpeXF19++SX79+/n4MGD
RvsdOXIkgYGBuLm5ER0dzfHjx7U+fvvtN3x9falfvz7Ozs4EBQXRqlWrO8ZeUpKSkvjoo4/4+uuv
iYiIeGj7/beWLFn8d6mUfkBtoB/+/s+wZMniUh6ZEKKkbN68GRMTEy5evFiq47jb95cQQgghhCgZ
EsgWQhRZmzZtuHz5Mnv37gVy/5i0t7fXgr95y9q2zQ1EX7lyhY8//pivv/6arVu3cuLECUaMGKG1
/eWXX/7+qQtwCJgERAHvA+Ds7AzA2LFjGTVqFMnJyXh4eBASEkJOTs4DH0+jRo2MnlerVo2zZ88W
2v7SpUucOnWKli1bGi339fXl119/feDxCGMzZsxgwYIFJda/l5eX9rNer8fOzs7oPVG1alWUUpw9
e5bk5GQ2bNiApaWl9qhXrx46nU67IJOWlkZISAiurq5YW1vj4uKCTqfjxIkTRvvNv4/q1atr+wCI
iIjg3XffpVWrVkyYMIH9+/eX2PHnl1ervmnTpowcOZLr16/z4Ycfl0it+uJka2urlUqJjY3FYDAQ
F7e6SPX5hRCPJl9fX06fPo2VlVWpjuP2CaTr1KnDjBkzSnFEQgghhBCPPwlkCyGKzMrKCi8vLy1w
vWnTJt58802SkpK4evUqp06dIj09HT8/PwCysrKYPXs23t7eNGnShNdff53169dr/c2ePRsvryaY
mMQAW4GmgB8wj4CAIOrUqQPcPYP1QZiamho91+l0RQqQ3177WyaGLBmWlpYlGqgo6Pd/+zKAnJwc
Ll++zPPPP09KSgrJycnaIzU1lTZtcicbfO6557hw4QJz585l165dWnmamzdvFrrfvPdN3vsuPDyc
o0eP0r9/fw4cOMBTTz3FZ599VqzHXZCHWau+JLi7u9OpUycpJyLEE6BcuXI4ODiU6D5u3bp1zzb3
M4G0EEIIIYQoHhLIFkLcFz8/Py2QvXXrVnr06EHdunVJSEhg8+bN1KhRQ5so0dzcXMuqhtzs07zM
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
ohwdHVWHDh1Ur169lLW1tapVq5a2f2dnZ/XJJ58YjaVJkyYqOjq60N9/Scv/+syfP1/FxcWpo0eP
qp07dypfX18VFBSktR0+fLh6/vnnted2dnbKwcFBrV27Viml1OLFi5Wjo+PDPYB7OH/+vAoICFKA
9rCwsFDTpk0r7aGVirxzwl9//VXaQ3lg4eHhqmvXrqU9jGJz+PDhv9+jixWofI9FClAGg6G0hyiK
yM/PT1laWqrIyEhlMBjUN998oypVqqTmzp2rlCr4XNu5c2dt+5MnTyo7Ozv1wgsvqKSkJJWamqoW
LFigvQfCwsJU9+7dlVJKrV+/XtnY2Kgvv/zy4R+oeKwU9P+lgv7fotPp1KpVq9TSpUuVmZmZ+uKL
L9S+fftUenq6euWVV5S3t7dSSqm//vpL6XQ6tW3bNqPtu3fvrr1/d+7cqXQ6ndq6datKT083evz+
++8leLRCCCGEKKrExMS8v6V91APGhSUj+zGTnp7O+vXradCgwT3bSv3MJ8uCBQswNTVl9+7dzJgx
g6lTpzJv3jwA/vOf/7Bz506WLVvG/v37eeGFF+jUqRPp6en4+voyffp0rKys+OOPPzh9+jQjRozA
z8+PgwcPahnOW7Zswd7eXpt0MCsri59//hk/Pz8Atm3bxoABA4iMjOTQoUPMnj2bmJgY3n//fW2M
vXr14vz588THx5OUlISPjw/+/v5Gk/mlp6ezatUqYmNjWb16NZs3b+aDDz4o8Jh1Oh3//e9/SUxM
pFGjRgwfPpyPPvpIW5f/Xyg807IoVq1aha2tLW3btqVjx454enrSsGFDFi9ejJ+fHx07dmTkyJGk
paVx5MgRHBwcGDBgAObm5vz000/8/PPPvPLKK+j1en777TcSEhJo1aoVdevWRa//51Rd1GzU0hIW
FkZAQADOzs40b96c6dOnExcXp2Vct23bVqtZmZKSQvny5QkJCdHeN3nZ6mVJQRmu166VJy7up0K3
eZzPr+rvOzTUI1yS6uLFi2zbto1vvvmGiIiIUhtHcb9P/sk+bHPbmrZAbuZinuPHj6PX60lJSSm0
v5iYGK3uu3j4ateuzdSpU3F3dyc4OJihQ4dqd7QUdK5ds2aNdq799NNPsbGxYcmSJXh7e+Pm5saA
AQPumAhz1apVdOvWjTlz5mgTFQvxsNxr7p+8Ow527NihLcvOziYxMVF7XpxzFAghhBDiEfCgkfCH
/UAysguVmZmpKlSooNq0aaNOnDhRaLuCsgsDAoJURkbGQxyteJj8/PxUgwYNjJaNGTNGNWjQQJ04
cUKVK1dOnT592mi9v7+/euedd5RSSi1YsEDZ2tre0W+VKlXUihUrlFJKeXt7qylTpqiaNWsqpZTa
tm2bqlChgrp27ZrW3wcffGC0/eLFi1WNGjWUUkpt3bpV2djYqJs3bxq1cXNz07LEJkyYoCwsLNSV
K1e09aNGjVItWrS4vxfkIXnjjTeUXq83yoJs0qSJ9hoppVRGRobq3r27srKyUtWqVVNRUVFaptyV
K1eUjY2Nqlu37h0ZTmVJ/gysPXv2qC5duqjatWsrS0tLValSJaXX69Wvv/6qlMo9T5UrV04lJSWp
GTNmqJCQEPXdd9+pli1bKqWU8vDw0DIOy4J/Mlw7KnhDga2CqgrCFaB69uypLC0tlZubm1qzZk2B
59cKFSqoN954Q7v7YPbs2UbvgTxdunTRsvOVKvgOhqysLG29TqdTs2fPVs8995wyNzdX9erVUz//
/LNKS0tTfn5+qlKlSqply5bqyJEjRvspSr9z585V3bt3V+bm5srd3V19//33Siml3cWQ/w6N/Hcm
PCryXp/hw4fftd3hw4dVbGxssWcyl9T38P1kZB87dkzp9Xqju15ud/36dXXu3LkHGpP4d/z8/FR4
eLjRslWrVqny5curnJyce55rg4KCVFhYWKH9h4WFqerVq6ty5cqpVatWleixiCfH/WZkz5gxQ9nY
2Kj4+HhlMBjUuHHjlLW1tZaRrZRSU6ZMUVWqVFHfffedOnTokHr55ZeVlZWVlpGtlFJjx45V9vb2
KiYmRqWnp6ukpCQ1c+ZMtXDhwpI9YCGEEEIUiWRkiwJZW1tz/fp1Nm/ejKOjY6HtpH7mk+mZZ54x
et6iRQtSU1PZv38/2dnZeHh4GNUW3LJlyz1rC7Zp04ZNmzbx119/cejQIV577TWuX79OamoqW7Zs
4amnnqJixYoAJCcnM3HiRKN9vPTSS/zxxx9cv36dlJQULl26ROXKlY3aHDt2zGgczs7O2iSJANWr
V9fqLJY106ZNIzs72ygDbu/evfz+++/ac1tbW1asWMFff/3FmjVrqFevHuPGjWPs2LGEhISg0+lI
SEhg6tSpQNnO9L169SqBgYHY2NjwzTffsGfPHlauXAmgTa5pbW2Nl5eXUa3wNm3akJSURFpaGqmp
qWUqI/uf994OwB7YDUQAMQDUqlWLvXv30rFjR/r378+LL4bw00/bgQpAGPB/3LplyqxZs3jvvfcA
eOGFFzh//rw2sSRAZmYma9eupW/f3PNwYXcwTJo0yWh87733HmFhYSQnJ1OvXj1CQkIYMmQI77zz
DomJiSileP3117X2Re134sSJ9OnTh/379xMUFERoaCiZmZk4Ojry7bffApCamsrp06f55JNPiuW1
fpg2btzI5cuXtTs0bpeRkUFgYG697qCgIDw8PAgM7FxsE96W1Pewh4cHAQFBmJhE/N33b8BiTEyG
ERAQdEc2rrpHVn2FChW02uCi7Lh27do9z7VmZmb37MfNzY169eoxd+5cbt26VaJjFk+Gkpj7Z/jw
4fTr14+wsDBatmyJlZUVPXr0MGpTlDkKhBBCCPGYeNBI+MN+IBnZD0TqZz6Z7pbZtWzZMmVqaqpS
U1PvqC34xx9/KKUKz8j+5JNPlJeXl/rhhx+0jNpu3bqp2bNnq4CAADV27FitrZmZmfq///u/O/aR
np6ucnJy1JQpU5Sjo6M6cuTIHevPnz+vlMrNyM6fpaOUUtOnT1d16tQp1tertOzdu1c1bdpUWVpa
Kjs7O9WqVSv1xRdfKIPBcF8ZnHmZTg9LXgZWYmKi0ul0RjUpFy1adEfWZ2RkpHruueeUg4ODds5p
3LixCgsLKzBTuTT9c86sm+98ma2gotE588yZM0qv1//dtquCenecXy0sLLR+u3btapR9PXv2bFWr
Vi3t+b3uYFAq9/c8fvx47fmOHTuUTqdTCxYs0JYtXbpUmZubP1C/V65cUXq9XsXHxyulcmtk6/X6
x6JGdmECAoKUiUnlv78rTyhYrExMKquAgKB7b3wPJf09nJGRcce5wsPDU7m4uKgKFSooJycnNWnS
JC27fsWKFapdu3bK3NxcNW7cWP38889aXwsWLFA2Njba86LMUxAXF6datWqlbGxslJ2dnXruuedU
enr6Ax3Tk+hud1IV5VwbHR2tXF1dje62yC/vzp9z586p+vXrq+7duxfaVgghhBBCiAchGdniX7uf
+pni8ZK/viDAzz//jLu7O97e3mRlZfHHH3/cUVvQwcEBgPLly5OdnX1Hn35+fhw4cIDly5drWbRt
27Zl3bp1/Pzzz7Rt21Zr6+Pjw+HDh+/Yh4uLCzqdDh8fH86cOYOJickd65+UGq1NmjRhz549HDt2
jGbNnmbbtm0MGTIEDw8PPDzq58vgbAEEFprBeebMGTp16lSkfer1er7//vtiGX/t2rUpX748M2bM
4OjRo3z//fdaFnJ+bdu2JS4ujnLlymkZon5+flo98bLEw8MDW9vK6HRH+SfD9RvgJp6edbXxV61a
NV92601yf0d5cj8HV69e1bLxQ0ND+fbbb7UsyG+++Ybg4GBti3vdwZCnUaNG2s9Vq1YFoGHDhkbL
rl+/zuXLl/91v+bm5lhaWpbZOx+Km8FgID4+luzsGUAo4AiEkp39CfHxsQ98N0RJfw/b2toSF7ca
g8FAbGwsL7300v+zd+5xPZ7/H39+Pp+ETipEQko5pCJfwhoVmfN5ZFkZ2TCnpTDmFIbZnO27zblE
DpvGtsghNcchNIdaOVU/X6fJOVuq6/dH+9zrUyGE5Ho+Hvejz31d131d131/rs99d7+v9/V6c+PG
nwQHB5OQkMC6deuUsQIwceJExo4dS3x8PHXq1MHHx4ecnBwlP7835ZPiFNy/f5/AwEDi4uKIjo5G
o9HQo0eP5zqnN5W0tDSCgoJISkoiPDycJUuW8MknnxTpXjt8+HDu3LmDt7c3cXFxnD17lrCwsALj
t1KlSkRHR5OYmEjfvn0LfdZLJCWdkrxaTSKRSCQSSfEiDdlvGLVr1/7n06/5cmKB3GWmktLJo16I
7ezs6NevH35+fkRERHDx4kUOHz7M7Nmz2bZtG5Ar53Hv3j2io6O5ceMGDx48AMDZ2RkzMzPWrVun
GCA9PDyIiIjgr7/+ws3NTWl/8uTJhIaGMm3aNM6cOUNiYiIbNmxg0qRJAHh5edGiRQu6d+/Ozp07
SUlJ4cCBA0ycOJFjx4693Iv1iikoO/AlN25czWNYKwvUf6RhzcLCgjJlyry0/qpUKnJycqhUqRIh
ISF8//33NGjQgDlz5jB37twC5Vu1aoUQAk9PTyXN09OTnJycEmfIBmjQwIGaNS0BX6Am4Ev58mX5
4IP+jzjiOpDX+BerfNIaBbt06UJ2dja//PIL//d//8fevXvp16+fUu7evXsEBwcTHx+vbKdOnSIp
KUmR6wF0vmdt3YWlaQ2Tz1Kvtp68xs3SzIs2NL+s57C9vT0tW7ZkzZo1fPnll7z//vvY2Njw1ltv
MXDgQKXcmDFjaN++PXZ2dgQHB5OSkvLYcxRCEBISQv369XFzc8PX15fdu3cr+T179qR79+7Y2tri
7OzMsmXLOHnyJGfOnCmW83pTUKlU+Pn58eDBA1xdXRkxYgQBAQEMGjSoSPdac3NzoqOjuX//Ph4e
HjRp0oTly5cX+myoUqUK0dHRnDp1ivfff/+JkjMSSUnhRctASSQSiUQiKXlIQ/YbxtPqZ0pKB497
IQZYvXo1fn5+BAUFUa9ePXr06MHRo0epWbMmkKunPWTIELy9vbGwsODLL79U6m7ZsiVqtVoxWjds
2JAKFSrQtGlTHY3Od955h59//pmdO3fi6upKixYtWLBgAbVq1VLKREZG0qpVKwYOHEjdunXx8fEh
NTVVx3uwtFO4N2iDf3LzGtZygP0ANGvWjODgYCUnr5f1w4cPGT58OGZmZqhUKmxtbfniiy8AsLGx
QaVS0b17d9RqNba2tkod33zzDXZ2dpQtW5b69esTFham00+1Ws23335Lt27dOHLkCKamptjb23Pp
0iXOnTtHRkYG+/btw8rKCiEExsbGyrFmZmZkZWXp1NmtWzeys7OVMVmS0NPTo2fPHoqHa1JSElWq
VNHRatfi4vIfVKpTwDby3l/r12+AsbExVlZWAJQrV46ePXsSFhZGeHg49erVo2HDhko9OTk5bN68
WWdlQq9evZRrplbnPr6Dg4MxMDCgdu3abNu2rVAt0rw8bmVEUdHX1wcotZ6bL9rQ/DKfwwkJCWRm
ZtK6detHlsnrfW9paYkQ4rHe90+KU3D27Fl8fHyoXbs2FSpUUFbdpKamPufZvFlER0ezePFivv76
a27dusWff/7JtGnTlHxvb2+de22nTp3Izs7G2dlZKePo6Mi2bdu4e/cut27dIiYmRnnmrlq1is2b
Nytlq1atSkJCAuHh4U+8j0gkJQUZ90cikUgkkjeQ59UmedkbUiP7uSlMP/NRWrsSieTlEhkZ+c/v
MjWPdm5+TV0PAaYCeglAzJkzR6jVarFr1y4hhK5G9pdffimsra3Fnj17xIkTJ8T+/fvF+vXrhRBC
XL9+XahUKhEaGiquXr0q/vzzTyGEEJs3bxb6+vri22+/FcnJyWLevHlCT09PxMTEKP1UqVSiatWq
YvXq1eLChQsiLS1NzJw5Uzg6Ouqcz8iRI4WHh8cjz/ePP/4QkZGRJVqfX6sBnpdatWqJhQsX6qSp
VCqxdu1a4e7eWuf+6uLyH1GpUiUxbdo0nfI7d+4U5cqVE/Xq1RMzZ87UyatSpYrQaDQiODhYnD59
WiQkJAhra2vRqlUrpS1AjBgxQiQnJ4tJkyYJjUYjVCqVjh55TEyMUKlUip51VFSU0NfX16l3/fr1
Onr2hWmsm5qaipCQECGEEJcuXRIajUaEhISI69ev6+gjlxb+1che889vcU2xaWQL8fKewydPnhRq
tVpcvHixQJ5WIzvveLl165ZQqVQiNjZWCFEwPkJR4hTUrVtXtG/fXkRHR4vExERx5syZl67bL3ky
r8O9VyJ5HDLuj0QikUgkrw9SI1vyXOTXz0xKSmL79l8wMzN71V2TSJ5IaddBLNwbtA7QCBhGrtfR
30AVNJo9tGvXkTFjxtCkSROd5f1a0tLSsLOzw8PDg4YNG/LWW2/h7e0N5GqjAlSoUAELCwsqVqwI
wNy5cxk4cCCDBw/Gzs6OgIAAevbsyVdffaVTd79+/ejfvz+1atWievXqDBgwgD/++IOjR48CkJWV
RXh4OP7+/gX69TotBy7MO/FRaUZGRsTE7Gbt2rXUrVuXsmXLcvXqZT766CM+++wznfKtW7fG3Nyc
5ORkfHx8dPLKly/PRx99pLOC4fr165iamuq05+XlhZ2dHdOmTdPxxHxUX4uyMuJJ51utWjWCg4P5
9NNPqVq1KiNGjCi03deZ8PAwvLyak1dOxsurOeHhYU84smi8rOewvb095cqVK/TeAIV/189Deno6
SUlJTJw4EU9PT+rWrcuNGzeKtQ3J8/E63Xslksch4/5IJBKJRPJmoveqOyB5ddjb20spEclrQ3p6
Oj4+vkRFRSpp7dp1JDw8rMROwkRFRTFjxgxOnTqFRqOhRYsWLFy4EFtbW1JSUrCxsWHDhg0sXryY
o0eP4ujoyNq1a2ne/C0OHeoPDCI3aGBv1OqLmJmV48YNX6V+IdRcuHCWb775Rlnen5KSghCCffv2
MW/ePA4dOkSZMmWwtLQkPT2dn3/+mbZt2wLw008/IYTg3XffpUKFCri7u/P999+TkJCAk5MTTZs2
5Y8//sDQ0BArK6sCBqm5c+fSsWNHxo0bx5kzZ2jUqBGtWrVi5cqVNGnShK1bt5KZmcm7775b4Nro
LgduBfzKrl0jee+999m+/ZcX9ZU8E9HR0QXSzp8/XyAtr9SGj49PAeN0ftRqNZcuXXpkfr169fjv
f/+r7Lu4uPCf//xH2Q8NDaVr167KvoeHB2ZmZjoGbXd39wISIG3btlXGQGEUJhmSnp6us//ZZ58V
MMyXJrSG5uTkZM6ePYudnd0LCfBO5QAAIABJREFUeV6+6Odw2bJlGTduHGPHjqVMmTK4ublx/fp1
Tp8+TZs2bYpdC9nMzIyKFSuydOlSqlatSkpKCuPHj5dSFSWI1+neK5E8Dt2J/355cmTcH4lEIpFI
SjPSI1sikbwWvI46iPfv3ycwMJC4uDiio6PRaDT06NFDp8zUqVOZPHkyx48fR09PDx8fH/T19WjW
zBX4C9gDfEzbtm+RnJzAV199hZ6eHq1bt+b8+fN88cUXTJ48mf/7v//TCcYXGhrKJ598wh9//EF8
fDw9e/YEoE+fPvTu3ZtffvmFnj17olKpWLhwIdHR0TRp0kQ5Pjs7mxkzZvD777+zZcsW0tPTC9XN
nThxIvPnzycuLg49PT0uX77M+vXr+fvvv1m9ejXe3t46QQThUTrg/R4ZvPJNRK1WFzAyPnz48InH
SYNh8WJvb0+HDh1e60nfyZMnExgYyJQpU3BwcKBv375cv34dKPpqg6KiUqnYsGEDcXFxODk5ERgY
WGAlh+TVIe+9ktKEjPsjkUgkEskbyvNqk7zsDamRLZG8cZQWHcRr164JlUolTp8+rejTrlq1Sslf
v369UKvVihZ1UlKSGDBggKhdu7ZSxs7OTjg4OOhoNs+YMUOYm5uLAQMGiIsXLwpAfPTRRzpta7Vu
o6KihEqlEq6ursLPz0/o6+uLzZs365R1c3MTgwcP1knz8vISgLh//74QIldHWaVSiT179ihlIiMj
hUqlEtWrVxfz5s0TZcqUEb/99luB61C4Drj4Zx8RGRn5dBe2FNKsWTMxbtw4Zf/27dvCwMBABAcH
CyFyr/+wYcN0jmnRokWBtOJEaupKJK838t4rKW3IuD8SiUQikbweSI1siUTyRvG66iCePXsWHx8f
ateuTYUKFbC1tUWlUpGamqqUcXJyUj5XqVIFAEdHRyDXG7RVq1bcunULgIyMDM6dO0diYiJLlizB
2NgYY2NjPv/8c+7fv6/TtnbJ7YIFC9iwYQOXL18mOzubjRs3YmlpyalTp2jdujW1atVi9+7dXL16
VWlnzJgxrFq1CmdnZ6pVq0a5cuXYtWtXgb7n77+lpSUqlYoePXowfvx47O3tcXV1LXBdCtcBB7kc
+F9at27NmjVr2LdvHydPnuSDDz5AT09XDWzTpk2sWrWK5ORkpkyZwpEjR16IXrXU1JVISgfy3gsH
DhzA2dkZfX19ZaXS/v37ddJiY2PRaDTcuXOnSHV6enoyevToIvchNjYWtVpd5Polj0bG/ZFIJBKJ
5M1DamRLJJISz+uqg9i5c2dsbGxYvnw51apVIzs7G0dHRzIzM5UyZcqUUT5rl/TnT9NKhty7dw/I
1U5u3ry5jkbx0KFDdSQBtHIeRkZGfPHFFyQkJPD333+TmppKZGQkbdq0AXJ1rgMDA1m2bBlWVlac
P3+etm3bUqZMGS5evMjff/9N9erV6dOnD3PmzFH6rlKpEEIU2v8+ffqwZMmSQoM8wr/LgXftGkl2
tiB3QiIWjWYUXl5yOTDA+PHjuXDhAl26dKFChQpMnz6dixcv6nzHwcHBrF+/nmHDhmFpacn69eup
W7dusfdFaupKnoakpCTOnTv3wnTFJc+OvPfC6NGjady4MVFRURgaGgIQGBiok2ZgYMDly5cxMTEp
Up0RERE6z8KiIGWgihcZ90cikUgkkjcHaciWSCQlntfx5Ts9PZ2kpCRWrFiBm5sbAPv27XuuOi0s
LLCyssLHx6dAoL2oqCgAUlJSUKvVeHh4ADBo0CAGDRpESEgIAQEB7NixAwBnZ2d2795NaGgonTt3
1qkrMTGRBw8ekJqaipWVFQBhYWE6ZaKjo2ndunWh/bxy5QplypTB19e30HyA8PAw3nvvfaKi/i3j
5ZUbvFMCxsbGhIeH66Tlv57VqlVTvvfC8PT0xMXFhXnz5j1zP7SaurlGbO0kUj+yswVRUb4kJyeX
yN+f5OXzOgbkfRN50++9586dY+jQoVhaWj42zcLCosh1mpqaFmsfJZKnITg4mB9//JHjx4+/6q5I
JBKJRPJSkNIiEonktSA8PAwvr+aAL1AT8MXLq3mJffk2MzOjYsWKLF26lHPnzhEdHU1gYOATvbBE
vgB/+Zk6dSqzZs1i8eLFJCcnc+rUKVavXs2CBQuKXAfAlClTCA8PZ+rUqSQmJnLy5Em+/PJLAGrW
rIm+vj6LFi3iwoULbN26lRkzZjyxr2fPniUnJ4dZs2bh7e1N5cqVH9m+XA78/Fy6dIlt27a90ABt
r6usj+Tl8zoG5H0TKe333szMTEaOHEmVKlUoX748LVu25OjRo8okb3p6OgMGDECj0RASElIgLTQ0
tFDpj/379+Pp6YmhoSHm5uZ06NCB27dvAwWlRdauXUvTpk0xMTHB0tKSfv36KQFWJZIXgfTwl0gk
EsmbhDRkSySS1wIzMzMWLpxHo0aN0NfXx8HBoUS/fKtUKjZs2EBcXBxOTk4EBgby1VdfKXl5/+Y/
7nH4+/uzfPlyRcPaw8ODkJAQbGxsilwHgLu7O5s2beKnn37CxcUFLy8vDh8+DEClSpVYvXo133//
PQ0aNGDOnDnMnTv3kX3Vaii/++67ABw7doy0tEtF0lC2t7enQ4cO0qv3KUhPT0cIwccff/zCNaul
pq6kKGg997OzF5HruV+DXM/9hURFRb7QyRbJs1Fa771jxowhIiKCNWvWcPz4cezs7GjXrh0mJiZc
vnwZY2NjFi1axOXLl+nTpw9XrlzRSfP29gZ0n6MnTpzAy8sLR0dHDh06xP79++nSpQvZ2dmF9uHh
w4fMmDGD33//nS1btpCSksKAAQNeyvlLSiZCCGbNmoWtrS0GBga4uLjwww8/AJCTk8OgQYOUvHr1
6rFo0SKd42NiYmjWrBlGRkaYmZnRsmVL0tLSCAkJITg4mPj4eNRqtTIZI5FIJBJJqeZ5o0W+7A1o
DIi4uLjnDZopkUheM7y9vYWXl5dIS0sT6enp4uLFi0KlUon4+PhX3bU3mnbtOgqNxlxAmIBUAWFC
ozEX7dp1fNVde+F4eHiIgICAl9pmUa+3h4eHGDVqlBg7dqwwNzcXVatWFVOnTlXyU1NTRdeuXYWR
kZEwMTERffr0EVevXhVCCHH79m2h0WjEsWPH8rRnKOA/AtYIjcZcODk1FDVq1Hip5y4pmURGRv4T
hTxVgMizpQpAREZGvuouSt4A7t+/L/T19cX69euVtIcPHworKyvx1VdfCSGEMDU1FSEhITrH5U+L
iYkRarVa3L59WwghhI+Pj2jZsuUj233Sc+DIkSNCrVaL+/fvF1q/pPQzY8YM4eDgIHbu3CkuXLgg
QkJCRPny5cWvv/4qHj58KKZOnSri4uLExYsXxbp164SRkZHYtGmTEEKIrKwsYWpqKsaNGycuXLgg
EhMTRWhoqEhLSxN//fWXCAoKEk5OTuLatWvi6tWr4q+//nrFZyuRSCQSSUHi4uL+eV+gsXhOu7DU
yJZIJK8N586do3PnzlSvXh2A27dvF9tyyqysLPT05C2xqGgDumk0Gqmh/BJ5Ws3qkJAQRo8ezeHD
hzlw4AAffPABb7/9Nm3atKFbt24YGxuzd+9eHj58yNChQ+nbty/R0dGYmJjg4uJCTEwM4eFhdO7c
lQMH9gFx5Mr6dKRKlUpFkrGRvDxsbGwICAhg5MiRL7Xd1zUgr6R0ce7cObKysnjrrbeUND09PVxd
XUlISHjmek+cOEGfPn2KXD4uLk7xkr1586YSsDk1NZV69eo9cz8kryeZmZnMmjWL3bt306xZMwBq
1arF3r17+e6772jZsiVTpkxRyltbW3PgwAE2btzIu+++y507d7hz5w6dOnWiVq1aADqBnY2MjNDT
03usnJtEIpFIJKUJKS0ikUhKDFFRUbRs2RIzMzMqVapEly5duHDhAgBqtZpjx44RHByMRqMhODgY
W1tbABo1aoRardYJPrh8+XIcHBwoX748Dg4OfPPNN0qeVitz48aNeHh4YGBgwLp1617uyb6maGVE
6tatS8eOHWnXrt0/OaVLQzkrK+tVd6FQnlaz2tnZmUmTJlG7dm18fX1p0qQJu3fvZteuXZw6dYrw
8HAaNWpE06ZNWbNmDTExMcTFxeW20KoVMTExmJmZ4e3dmy5dumBra8uqVavYvv0XDh48qAQVlbzZ
aAPyajQjyZ1kSQPC0GhG0a5dyQzIKyl9aCfW8k9wCyGea9K7fPnyRS6bkZFB+/btMTU1Zd26dRw9
epSIiAgg16ApefM4e/YsGRkZtG3bFmNjY2Vbs2YN58+fB+Drr7+mSZMmWFhYYGxszNKlS0lNTQVy
pfX69+/PO++8Q9euXVm0aBFXrlx5lackkUgkEskrRRqyJRJJieH+/fsEBgYSFxdHdHQ0Go2G7t27
A3DlyhUcHBwICgriypUrjBkzhsOHDyOEIDo6mitXrrB582YgN9CSNihiYmIiM2fOZPLkyaxZs0an
vfHjxxMQEEBCQkIeg6zkcRQM6PblPznPpqF87949+vXrh5GREVZWVixYsEAncFZmZiZBQUFUr14d
IyMjWrRoQWxsrHJ8SEgIZmZm7NixAwcHB4yNjenQoQNXr17VaedZJjbS09Px8fGhRo0aGBoa4uzs
zPr165/hqhUfT6tZ7ezsrLNvaWnJtWvXSEhIoEaNGlSrVk3Jq1+/PqampornooeHB3v37s2tPTaW
Ll260LVrV5KTk7l8+TJnz57F3d29+E5O8lrzugXklZQ+7OzsKFOmDPv27VPSsrKyOHr0KA4ODs9c
r7OzM7t37y5S2cTERNLT05k1axZubm7UqVOnwPNI8mZx7949ACIjI4mPj1e2M2fOsGnTJjZs2MCY
MWP48MMP2blzJ/Hx8QwYMEBn4mPlypUcOnQINzc3NmzYQJ06dZS4JhKJRCKRvGlIQ7ZEIikx9OzZ
k+7du2Nra4uzszPLli3j5MmTnDlzBgsLC/T09DAyMqJy5coYGBgoyyjNzc2xsLDA1NQUgKlTpzJ3
7ly6deuGtbU13bt355NPPuHbb7/VaS8gIEApU6VKlZd+vq8bhQd0CwIaAcN4Fk/MgIAADh48yM8/
/8zOnTvZu3cvx44dU/KHDRvGb7/9xsaNGzl58iS9e/emQ4cOeTyTcz3g5s6dy9q1a9m7dy+pqakE
BQUp+c86sfHXX3/RpEkTIiMjOX36NIMHD8bPz48jR44855V8dp7W87VMmTI6+yqVipycnEd6KOZN
b9myJXfv3iUuLo69e/fi4eGBu7s7e/bsITY2FisrqzyGdUl+PD09GTlyJAEBAZibm1O1alVWrFhB
RkYGAwcOxMTEBHt7e7Zv3w7A6tWrCwSv3bJlC2q17r9qP/30E66urpQvX57KlSsrQVa13L9/H39/
f0xMTLC2tmbZsmUv9kT/wczMjO3bfyEpKYnIyEiSkpJKdEBeSenDwMCAoUOHMmbMGKKiojhz5gyD
Bg3iwYMH+Pv7P1VdeWWTxo8fz5EjRxg2bBgnT54kMTGRb7/9lvT09ALH1axZE319fRYtWsSFCxfY
unUrM2bMeGz9ktKNg4MDZcuWJSUlBVtbW53NysqK/fv34+bmxuDBg2nYsCG2trY6/+NoadiwIePG
jWP//v04OjoqKwn19fUfGXhUIpFIJJLSiDRkSySSIqH1Wv39998fWSY2Nha1Ws2dO3eeqY2zZ8/i
4+ND7dq1qVChAra2tqhUKmV5ZVHIyMjg3Llz+Pv76yzh/PzzzxWZEi3/+c9/nqmfbyqPlrUIBe7y
tJ6Y9+7dIzQ0lLlz5+Lh4YGDgwOrVq1SXsjS0tJYvXo1mzZt4q233sLGxobRo0fj5ubGqlWrlHqy
srL47rvvcHFxoVGjRgwfPlzHe+5ZJzaqVavG6NGjcXJyolatWgwbNox27dqxadOmZ7p+xUVxeL46
ODiQkpLCpUuXlLQzZ85w+/Zt6tevD4CpqSlOTk4sWbKEMmXKYG9vj7u7O8eOHePnn3+W3thFIDQ0
lMqVK3PkyBFGjhzJkCFD6N27N25ubhw/fpx33nkHPz8//vrrL1QqVaGTC3nTfvnlF3r27Ennzp05
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
zeXff/8lGRkZ2r9/f524hs5lTk4OETVOWqT6Wqspc/PkyRNiGIYiIiLYumrKEVVja2tL69at44Qd
PnyYNDU1m9jj5lNTWoRIfB126tSJQkJCKCUlhaZNm0aqqqr05MkTInrZt1dJi5w8eZKkpaXpp59+
ooyMDNq8eTO1a9eOLl26xKZ5/PgxSUhIULt27dh3jKCgIJKUlCQtLS1O++qTFqk9xo8dO5bc3NyI
iKiyspKMjIzI3t6ekpKSKCoqigYMGEACgYD++OOPljhkjaJmO//991+SkpKi33//nY1/+vQpycvL
U6dOnTj9OXXqFCkrK9Mvv/xCAOjZs2fk7e1Nzs7OBIA++eQTIiLq3r07DRw4kBiGoUuXLrFjjJOT
E9nZ2RERUWlpKcnLy9PVq1fZZyoRkbu7Ozk7OzfY/srKSurUqRNt2bKFdHV16dtvv31l2vrGFiUl
JTp48CARES1btqyOtMgPP/xA7du3JyLxs1xaWpoCAwPZ+PLycrZ+oraTFnlTebKm8vI5fejFc/pQ
qz2nRSIRBQcHv9fv8/U9M3l4eHhampaUFpF8azPoPDw8PP8BqpcfXrjghcpKgtgSOwISEt6wteWX
H74OkUiEzMxM6Ovrt9mxGjJkCExMTLBly5Y2qa8h/Pz8oKenhz179iAuLg4CgYDjtElbWxvr16+H
nZ0dMjMzoaSkBKBxlpGZmZk4deoUgoODUVBQgIkTJ2LdunWstdnChQsRGRmJ06dPQ01NDUuWLMG1
a9ca5ZytWlIHMAbQHS8ldQglJS4ca77qtjEMgzlz5uD69euYPHkyGIbBlClTMG/ePFbmpqU4dOgQ
fHx8cP/+fY6l25gxY6CsrAx/f3/8+OOP2Lx5M+7cuQNdXV0sW7YMZmZmL/q1DWIrrOtsv0JDXSAQ
CBAeHo7Bg2uvwHh3qO2ADgDGjRvHSbNnzx5oaGjg5s2bHEvRRYsWwdbWFgDg7e0NJycnXLx4EQMG
DAAgXkWxZ88eHD16FCkpKcjPz8eKFSswceJEAGIHo2FhYdi2bRt27NjRYDulpaXx119/4c6dO/j0
00/ZdowbNw5ff/011NTUIBQKm3wcpKSkWOePr+PKlSv48ccfYWdnB0As1fTo0aMm1/2+kpqairKy
stfKILQFDMNwHOYCYmv+K1eucJzcVVZWoqysDM+fP4eMjExbN7MO69atAxHB1dUV//77L/r161ev
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
VxQcHEyJiYmUlZVF27dvJwUFBfrjjz/ea9tUfuaUlpaSgoICeXp6Muvu3r1LPB6vxmvax8eHhg8f
ziyLr58DBw6QoqIi7d69m7U/CQkJ6t69O4lEItq+fTtJSEgQIE2AkAAdAgTE4wmoRw97yszMpFev
XpGFhQVNnDiR/vnnH0pNTaVvvvmGzMzM6NWrV/T69WtSUVGhwMBAun37NqWmplJkZCTl5uYSEVFc
XBwpKytTVFQUZWVl0alTp8jQ0JAWLFjA1IvH45Guri6FhYW96e/OBCgS8JCAUgL8CACdOnWKvvrq
K5o2bdq7OgUc74n6vqdwNG/s7e1p+vTp5OPjQ8rKyqSurk7z5s1jtr948YICAgJIR0eHZGRkyMTE
hDZv3vwRa8zBwcHRcBITE9+8f8CWmmoXbmoBH/rHGbI5ODg4qrJy5UoyMDBocjn29vakoqJCCxYs
oFu3blFkZCTx+Xw6deoUEVVvyLawsKCTJ09Samoqde3alTp27Ei9e/emv//+m5KTk8nY2Ji+/fZb
1j58fHxY+3VzcyNvb29avXo1GRoaVqmXUCikqKioWuv9rg3Z9WXGjBnE5/NZH5LW1tbUqlUrIqJq
DdkvXryg4cOHk1AoJD6fzxiq+Xx+FUO2UChkGbIrHtfnaMguKioiaWlp2rNnD7OusLCQ5OXlyd/f
n9LT04nH49GuXbuYD/iCggISCAS0d+/ej1jzxhMcHEw2NjZV1p85c4b4fD49evSowWWePHmSZGVl
yczMjBYvXsysP378OElLS1NISAj9888/dPPmTQoMDHzzYplTyZCdQwAoOjqayT937lySkZFhGccr
U9FIrK+vT6tWrWJtt7a2ppCQEGZ5/vz5pKurSzIyMtSyZUvy8/MjovJ+zePxiM/ni198KTQ0lHR0
dGodtNiwYQOpqanR06dP61VHMZ+qIfvp06ckKytbb8PG8uXLyc7OjlkODg4mBQUFKi4uZtYFBARQ
165dayzj3r17xOPx6J9//iEiovXr15OGhgYzKEdEtG7dOpYhuzoqG4jfB9U9c/T09Gj58uWsdTwe
jw4dOkRERGvXrqUOHTqQhoYGKSgokLS0NHXu3JlJO27cONLW1iZJSckq92yxIVsgEJCCggIpKCiQ
lJQUcw2Lf87OLlRYWEhERFu3biVzc3NWOS9evCCBQEAnT56kwsJC4vP5dO7cuWqPsU+fPrR06VLW
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
37lzh0u7dOkSsSxL169fJyIibW3teh/ZAQEBZGFhQURE169fJ2NjY2rbti3997//pbCwME7UjoiI
IIZhSF1dnSe+iEQikkql9Ntvv1FOTg7t2bOHxGIxnT59uknC6IoVK0gikZCPjw9dvnyZrly5QkQ1
gZqMjIwoKiqK0tLSaMKECaStrc0FDZQL2Q4ODnTy5EnuQ8bc3Jxrc2ZmJkkkEgoMDKSsrCz6448/
6IMPPiA/P7/nO1BvGfV9O8uF7Brfzo6OjvU+CJOTk4llWQoICKDs7GwKCQkhIyOj5xay9+zZQ6qq
qhQYGEgZGRmUmJjIC3jYo0cPcnJyohMnTlBubi7Fx8fT4sWL3/rnYUM+6180eNuhQ4eoXbt2XDA8
f39/Xv7ff/9N3t7epK6uTjY2NnT8+HHS0tLiCdl16y4pKSGWZTkhm6hmoMjY2JjU1NRo4MCB5O/v
T1paWrR69Wqyt7dv8Jr8999/acWKFZSYmEi5ubm0b98+kkgk9L///Y+rd8KECaSurk7jx4+nP//8
k/7880+6e/cutW3bltasWUOFhYVUWFhIRE0LEPo2c+XKlUaF7D/++IMUFBRo3bp1lJiYSJmZmbRq
1SreNdKQD9WGAg/Wvl9v2LCB2rZtS9nZ2ZSVlcX7FRUVNVvfags58u0/yy983YBzzUFjgRjfJLXj
CHh5+RDLqhMgIuACJwq7uvbg+aqve6wtLS1p//79vHpXr15N3bp1e6E2NTUQ9Ls4GDFt2jQyMzOj
mJgYunLlCg0cOJCkUinNmTOHbt++TcrKyjR//nzKzs6m8PBwsrGxafD+u3jxYlJWViZ7e3teenBw
MO3atYtSU1MpOzublixZQmpqas8dZPtFeJlrrri4uN4gS/fuPV9Zu4uKipolGPmL8DxCdmlpKSkr
K9PBgwe5tLp+1Wvf/86cOdNo/I5u3bqRr68vdevWjWbOnMnL79q1qyBkCwgICLxntBQh2wvALgAe
+H/2zjyupvz/469z7q3bvbd9lUjai1K2SZEiiqEwYytlK8OIprGMMZZmGIavsYwxxi6SYaw/oylj
SxhbWULcyhIz1jBUQrf374/co9Oiog3n+XicR53P53w+53POuWd7n/f79QYsAPQAcBvA3GLLaAG4
BSAagAOAfgByAYS+pl/BkC0gIFAhb/OCU5lkj2fOnOESEhEVGbJVyY9ULFy4kKytrbn5/Px82rVr
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
gObPn8/L3+Ht7c0le5TJZFyyx2nTpgnJHivJ77//Tk5OTiSVSsnAwIC6dOnCPfevWrWKmjVrRhKJ
hBo2bMjTIS95zb9x4wb169ePdHV1ycDAgAICAnj5K1SJqOfNm0empqZkYGBAo0eP5klfPXv2jCZO
nEiNGzcmiURCtra2tHr1aq4+NTWVunXrRpqammRiYkLBwcG83EICAgICdaqRDWA2gMLXTEoAtiXa
mKEo2eOyEuVlGbIdy+qjWH1LAOTp6Uk9e/bkTbGxsTW1zwUE3muq25C9du1a0tXVLVV+//59evr0
abWtp7LUF4NkVZkyZQoZGRlRdHQ0ZWZmUkpKCi1evJjWrVtHDx48IE1NTYqIiKDMzEzasGEDmZmZ
VWjIJiL64osvqFGjRhQfH08XLlygwYMHk4GBAT169IiIXhmynZycaN++fZSamkr+/v5kYWHBGVXO
nTtHcrmcwsPD6cyZM5Senk47duwo9bJUGeqrIbu+wDewZhAgIZbV5mlrqnSaVUlIs7KyiIiosLCQ
GjVqRCtWrCCi1ydmUi2jShKam5vL1U+cOJHatWtX05taZ1TW0FDeORkdHU0//fQT6erqUkJCAikU
Cpo6dSrp6OhUypDdtWtX6tWrF/3zzz/ci59gyK46ly9frpZrvZeXFzVr1oxXNmnSJK6sLI1sIqJT
p05Rz549ydDQkNN5ZlmWNm/eTGpqapxhOzU1ldTU1CgpKYmIiGQyGTVs2JC3fldXV2JZlv766y/K
zc0lAKSurs5pRsvlcmIYhiQSSYXbc+fOnVLnfHFel2C1qhTXXy7LKCwWi6lPnz509+5drk1Z96qN
GzeSq6sraWhokIGBAXl5edGOHTveenyV5V19bqgN6lLv+W2pK6Pyq322/uU+W1/j+8zLy4vGjBnD
5dUwMTGhlStXUm5uLpmbm5NYLKYmTZqQuro6jRs3jv7++2/q27cvGRgY8M7X/v37k1gspi+//JIz
ZIeGhhLLstSyZUuSSCQEgIyMjEgkEpGamhoFBweTn58fmZubU69evah79+7EsiwxDEP29vY0ceJE
7py/desWde/enaRSKVlaWlJsbOw7/cxWXdy6dYvU1NRo0aJFdP36dTp//jwtXbqUcnNz6ZdffiGp
VEqLFy+m9PR0OnXqFG9/FTdkv3jxghwdHbkPpZcuXaJBgwaRvb0990w/ZMgQ0tHRoc8//5wuX75M
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
QK5Uwrx58zhw4ADbt2+nW7du2NramtXj5ubGunXrOHHiBOfOnSvck1uImK9uuWb469y5213Vc6Mu
eIkSJbCyssLOzg4LCwucnZ1xcXHBysoqX9lFixYhInz77bd4e3tTuXJlqlatyt9//83GjRv1fBER
Efj5+fHhhx/y2muvMXz4cFJTU3WddMj/fbZo0YLffvuNNWvWULduXRo0aMDUqVNxc3O7aRnIlQ+J
jo5GRIiOjqZGjRoMHjwYJycnPf+dSKaEh4dTp04dunTpQrVq1Rg+fLguPZKnZZ6YmIifnx++vr6M
GTOGZ555BrimZd6sWTO8vb359ttvWbRoEVWrVr1tu08yU6dOpXHjxsTFxdGqVSu6d+9Oz5496d69
O7t27aJixYr07NlTz3/58mVq167NrFmzrk4edQO+BdLIm+Ret241mzZt0sfC5s2b2blzp1m7b775
Jtu3b2fJkiXs3r2bDh060LJly+ueORQKheJfwv1Gi3zYH8AXkNjY2HuOlqlQKBQKxb+JoKAQMRqL
C8wTSBWYJ0ZjcQkKCnnUXXtiuHDhgowbN07Kly8vJ0+elNOnT8v48ePF29tb1qxZI0eOHJG5c+eK
jY2NLFiw4GpU7hCBNgJy9WMngMyePVtERObPny/lypV7tAemUPwL8ff3Fz8/P33bZDKJnZ2d9OzZ
U09LS0sTTdNk+/btBdbx1ltvSYcOHfTt0NBQcXV1lStXruhpCQkJommarF+/vsA6Vq5cKZqmibW1
tZQpU0amTp0qlStXFk3T5J9//hF3d3eZNm1avnInTpyQ0NBQcXFxERsbG/H09JT+/fvL33//LSIi
cXFxUrduXbGxsZHKlSvLzz//nK+uX3/9VSpVqiSWlpbi7u5+ZyfuIXPw4MGr19L5111H5eq9DElI
SMhXxt/fXwYNGiRZWVni5uZmdsyapsny5cvN8o8ZM0Z8fHzM0kJDQwXQ8w4bNkwsLCzEzs7O7GM0
GuXrr79+AEeey439L4jQ0FBp167dA+uD4tqYEsn9Tgq6TowZM0ZP+/3338VgMMiJEyfM6omIiLg6
nlMFWgkMuzqe9wsgI0eO1POeP39eihYtqrebkpIiFhYWcvz4cbM6AwMD5YMPPijsQ1YoFIpCJzY2
9uo1EF+5T7uw0shWKBQKheIpZ+HC+XTu3I3IyO56WmDgrXU7FebY29tjb2+P0WjE2dmZrKwsJkyY
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
ql27tgJU/fr11c6dO1WtWrWUkZGRcnR0VI0aNVLr1q1TkZGRytbWVk2bNu2RY7h169Zzn8+8CgoK
uv9ZSHrgs5B0//hiBUuVsXFx5e3ta3Dv7t271X//+1+1b98+lZSUpFatWqWKFCmigoOD1axZs5S1
tbX65Zdf1LFjx9To0aNV4cKFVUJCglJKqZMnTypN01RMTIy+vatXrypN01RERMRznYOC8uuvv6pq
1aopMzMzVaJECdWyZUuVkpKiMjIy1IQJE9Qbb7yhChcurGrUqKGCg4P192mapoyMjPQ/x48fb3BM
0zTVrFkzFRsbq4yMjNTly5eVUkpduXJFaZqm/P399W1NmjRJNW7cWCmlVHp6uurfv79ydnZWZmZm
ys3NTc2ePdugz3369FEdOnRQX3zxhSpTpowqX768Ukqp1NRUNXLkSOXg4KDMzc1V3bp1VXh4eEFP
oRBCvBKioqLu/28mnuoZY8smPCeaphUnc+l6u1Iq/f7husBWpVRatktDgI81TbNSSl17Xv0TQggh
hBBCCPinnEZo6DDS0xWZmdgRGBsPx8sr93IaBSn7xoGOjo4AVK1aFQAHBweWL1/O119/TXh4OK1a
tWLZsmW0adOGs2fPcuvWLby8vGjatKk+SzvL8uXL2blzJ3Z2dhQrVgwzMzMKFy7MnDlz2Lx5M2+9
9RZffPEF9evX54033uDs2bO0a9eO1NRUunTpwgcffEDdunWxsLCgdOnSnDlzhm3btunLX3Tu3Jkt
W7YwatSoR47hZWVYI7x7tjMR93/2BsDLy5cVK5YZ3FusWDG2bt3K7NmzuX79Ok5OTnz99dd4e3vT
qlUrbty4wUcffcTFixepUqUK69evz/a8F5/1XJDOnz+Pv78/06dPp0OHDty4cYNt27ahlGLWrFnM
nDmT+fPnU6NGDRYsWEC7du04fPgwFSpU4Pz587Ro0YLWrVszatQozM3NadOmDXXq1CEsLIwqVapQ
qFAhrK2tsbW1JSIigo4dO7J161b9+yxbt26lSZPMb1pkZGTg6OjI6tWrKVGiBDt27GDQoEGUKVOG
zp076+/ZvHnvdi0LAAAgAElEQVQzVlZWhIaG6o99+OGHHD16lFWrVlG6dGnWrFlD69atiY2NNfib
CiGEeDYFHsjWNG0KMAQoCuwE3s52uhRw/IFbLmQ7J4FsIYQQQgghxHO3YsUy/Px6EBLSU3/sYcHK
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
D4D58+cTGxvLypUr8fLy4rXXXuOjjz6ybOBX9t7PPPMMO3futLQZjUbeeOMNWrduzbfffsuYMWN4
4YUXWLJkiaXPmTNneOONN1i/fj2//fYb/fv3p3///jg6OrJ161aOHTvGgAED6Nq1K48//ngVr2AJ
d3f3KvszLw2Wp6enk5GRgZub23Xz+7Vr1y6rz1999RXu7u74+flRWFhITk4OXbp0ueD1LVu2ZNSo
UYwaNYq//vWvvPvuu4wdO5Y6deoAJS9FRERuJgpki4iIiIjcQjIyMpg2bRpff/01v/zyC8XFxRgM
BrKzs2nbti0AAQEBVzzu/v37ueOOO8rUpL10/507dzJnzhxLW1FREfn5+fz+++/Uq1fviucgN4br
vW7xlbjzzjsrrHFcGsju3bs30dHRlv7vvvsuv//+O6tWraJevXq0bduWJUuW0LdvX15++WWcnJxY
smQJf/3rX+nXrx8AS5YsqbBEj5ubG/Pnz7dqi4qKshw7Ozsze/ZsnnnmGatAdmFhIW+99ZblRdNj
jz1GTEwMx48fx9bWFi8vL3r16sVnn31WbYHs6rBz506io6PJzc2t6alYfP/990ycOJFRo0aRmprK
kiVLePXVV3FzcyM8PJzIyEgWLlyIn58fx48fJykpibvvvpuQkBCio6MJCQnBw8OD3NxcPvvsM0u9
bGdnZwwGA5s3byY0NBRbW9sr2phXROR6pdIiIiIiIiK3kIceeogTJ06wdOlSdu/ezddff43ZbCY/
P9/S52oCHra2tlfUPy8vj5kzZ1p9bf7QoUOYTKYbMoidnJyM0Wjkt99+A/4s4VBq5syZ+Pv719T0
rivXe93iK3GhGselZTnOfyl09OhR7r77bqvf8S5dulBcXMx//vMffvvtN3Jycmjfvr3lvI2NTYUv
l+69995ybYmJiQQGBnLHHXfg4OBAREQEv/76K2fPnrX0sbOzs/q2RNOmTWndurXV3+GmTZty/Pjx
y1yFG8OgQYMwmUw1PQ0Lg8FAZGQkZ8+epUOHDpZSMSNGjABgxYoVREZGMnHiRLy8vOjfvz8pKSm0
atUKKHnx9+yzz+Lt7U1oaCheXl6W0iItWrRg5syZTJ48mWbNmjFu3Lgae04RkcqkjGwRERERkVtE
bm4uJpOJZcuWWb6uvn379kteV6dOnUt+Rd3X15cffvjB8tX9S/H39+c///kPrq6ulzf561yXLl34
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
8MILBAUF8ccff+Ds7ExwcHCF194IlKUsIiJy/VAgW0RERERERABISkqyHB87dszqXFFRUbn+ubm5
Vp/btGnDhg0bqmZyIiIicktTIFtEREREREQqhclkIjMzUxsGioiISKVTjWwRERERERG5Jrm5uQQH
P4inpyehoaF4eHgQHPwgJ06cqOmpiYiIyE1CgWwRERERERG5JmFhESQm7gJigGwghsTEXQwePKSG
ZyYiIiI3C5UWERERERERkatmMplISIijJIgdfq41nKIiMwkJEaSnp6vMiIiIiFwzZWSLiIiIiIjI
VcvMzDx31P28Mz0AyMjIqNb5iIiIyM1JgWwRERERERG5am3atDl39MV5Z5IBcHNzq9b5iIiIyM1J
gWwRERERERG5ah4eHgQFhWI0RlFSXuR7IAajcTxBQaEqKyIiIiKVQoFsERERERERuSaxsTEEBnYE
IoBWQASBgR2JjY2p4ZmJiIjIzUKbPYqIiIiIiMg1cXR0JD5+C+np6WRkZODm5qZMbBEREalUysgW
ERERERGRSuHu7k5ISMhVBbFHjRpF48aNMRqNHDhwoApmV8LGxoZ///vfVTb+jaRXr148//zzALi4
uLB48eKrulZERKQ6KCNbREREREREalR8fDyrVq0iOTkZFxcXmjRpUmX3+umnn3B0dKyy8W9UKSkp
1K9f/7L7f/jhh9SuXbsKZyQiImJNgWwRERERERGpURkZGTRv3pz77rvvqscoKirCaDRest/tt99+
1fe4mTVu3PiK+t92221VNBMREZGKqbSIiIiIiIiI1JihQ4cSFRVFdnY2NjY2uLq6kp+fT1RUFE2b
NsXW1pZu3bqRkpJiuSY5ORkbGxvi4+O59957qVevHjt27ABg06ZNBAQEYGtri5ubG7NmzaKoqMhy
7fmlRXbu3Imfnx+2trZ06NCBTZs2YWNjYylvUnqvpKQk2rdvT/369enSpQvp6enVtELVo2xpkbCw
MAYPHmx1vrCwECcnJ95//32gfGkRFxcX5s2bx/Dhw3FwcMDZ2Zl3333XaoxLrbWIiMjFKJAtIiIi
IiIiNWbx4sXMmjWLO+64g5ycHPbs2cOkSZP48MMPWb16NXv37sXNzY2goCBOnjxpde2UKVN4+eWX
OXLkCL6+vmzfvp0nn3yS6Ohojh49yttvv83KlSuZO3duhffOy8ujX79+3H333ezdu5fZs2fzwgsv
YDAYyvV98cUXefXVV0lNTaVWrVoMGzasStbjehAeHs7mzZs5c+aMpS0+Pp6zZ88yYMCAC173yiuv
0L59e/bt28eYMWN45plnMJlMwJWttYiISEUUyBYREREREZEaY29vj729PUajEScnJ2xtbXnrrbdY
uHAhffr0wcvLi3fffRdbW1uWLVtmde3s2bPp3bs3Li4u3HbbbcycOZMpU6YwZMgQnJ2d6d27N7Nm
zeKtt96q8N4xMTHY2Njwzjvv4OXlRVBQEJMmTSrXz2AwMHfuXLp27YqXlxeTJ09m586d5OfnV8ma
1LSgoCDs7Oz48MMPLW2xsbE8/PDD2NraXvC6Bx98kNGjR+Pq6soLL7xAkyZN+Pzzz4HLX2sREZEL
USBbRERERERErhsZGRkUFhbSuXNnS1utWrXo0KEDR44csbQZDAYCAgKsrt2/fz+zZs2yBMft7e0Z
OXIkOTk5/P777+XuZTKZ8PX1pU6dOpa2Dh06VDgvHx8fy3Hz5s0BOH78+NU95HWuVq1aPP7445Yy
ImfOnGHTpk0MGTLkoteVXSOAZs2aWdboStZaRESkItrsUURERERERK4755ecMJvN5drq169v9Tkv
L49Zs2ZVWP6iXr165doqGtNsNlc4n9q1a5ebW3Fx8UWe4MYWHh5Oz549+eWXX0hISMDOzo4+ffpc
9JqyawQl61S6Rley1iIiIhVRRraIiIiIiIhcN9zc3Khduzbbt2+3tBUWFpKSkoK3t/dFr/X39+c/
//kPrq6u5X4q4uXlxYEDBygoKLC07dmzp3Ie5AbXuXNn7rzzTtauXcuaNWt44oknMBqNVz2e1lpE
RK6VAtkiIiIiIiJy3bCzs+OZZ55h0qRJJCQkcPjwYUaMGMHZs2etNlisKJt32rRprFq1ilmzZnH4
8GGOHj3KunXrmDp1aoX3CgsLo6ioiJEjR3L06FESEhJYtGgRYJ0RXtG9boVs4sGDB/PWW2+RmJhI
eHj4NY11uWstIiJyIQpki4iIiIiIyHVl/vz5PProo0RGRnLvvfdy7Ngxtm3bRsOGDS19Kgp+9unT
2+2B4wAAGX1JREFUh48//phPPvmEDh060KlTJ1577TVat25d4XX29vZ8/PHH7N+/Hz8/P6ZOncr0
6dMB61IkFd3rZgi+GgwGy3NU9Dzh4eEcOXKEO+64g06dOpW79mKfz2+73LUWERG5EMON9hbZYDD4
A6mpqan4+/vX9HRERERERETkJvL+++8zfPhwTp06Rd26dWt6Ojc1rbWIyM0vLS2tdHPmALPZnHYt
Y2mzRxEREREREbllrV69GldXV1q2bMm+ffuYPHkyAwcOtAqsmkwmMjMzcXNzw93dvQZne2NbsGAB
NjY2BAQEcOrUqQrXWkRE5EIUyBYREREREZFb1k8//cS0adPIycmhefPmDBw4kDlz5gCQm5tLWFgE
CQlxlv5BQaHExsbg6OhYU1O+4VS0jra2dgwbNpSFCxfW4MxERORGohrZIiIiIiIicsuaNGkS3377
LWfOnCEzM5OFCxdaajaHhUWQmLgLiAGygRgSE3cxePCQS447dOhQBgwYUKVzv1FUtI75+fXIyPhW
9bFFROSyKSNbRERERERE5Dwmk+lcBnEMEH6uNZyiIjMJCRGkp6dftMzI4sWLudH2pKoK17qOIiIi
pZSRLSIiIiIiInKezMzMc0fdzzvTA4CMjIyLXm9vb4+Dg0PlT+wGc63rKCIiUkqBbBEREREREZHz
tGnT5tzRF+edSQbAzc3toteXLS2SkJBAt27dcHR0pEmTJvTt25djx45Z+mZlZWFjY8O6devo0qUL
tra2+Pj48MUXf967uLiYESNG4Orqip2dHV5eXixevLjcPfv378+iRYto0aIFTZo04dlnn6WoqMjS
Jz8/n4kTJ3LHHXfQoEEDOnXqRHJysuV8dnY2/fr1o1GjRjRo0AAfHx/i4+Mt5w8dOkRoaCj29vY0
a9aMyMhIfv311ypbRxERkVIKZIuIiIiIiIicx8PDg6CgUIzGKErKYnwPxGA0jicoKPSKymGcPn2a
CRMmkJqaSlJSEkajkf79+5fr95e//IVJkyaxb98+OnXqRL9+/Thx4gRQEsi+88472bBhA0eOHGH6
9On87W9/Y8OGDVZjfPbZZxw7dozPP/+cVatWsWLFClasWGE5P3bsWL7++mvWr1/PwYMHefzxxwkJ
CbFkTo8ZM4b8/Hy2b9/OoUOHePnll2nQoAEAp06donfv3gQEBJCWlkZCQgLHjx9n4MCB1bKOIiJy
azPcaDW7DAaDP5CampqKv79/TU9HREREREREblInTpxg8OAh52o8lwgKCiU2NgZHR8eLXjt06FBO
nTrFxo0by537+eefadq0KYcOHcLb25usrCxcXFxYsGABEydOBKCoqAgXFxeioqIsbecbN24cOTk5
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
<div class="prompt input_prompt">In&nbsp;[58]:</div>
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
<div class="prompt input_prompt">In&nbsp;[59]:</div>
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
<pre>&#39;but, with, called, through, were, from, over, at&#39; are closest words to &#39;for&#39;
&#39;two, three, zero, four, five, six, eight, nine&#39; are closest words to &#39;seven&#39;
&#39;at, state, see, s, some, its, however, his&#39; are closest words to &#39;their&#39;
&#39;it, more, often, they, some, he, be, there&#39; are closest words to &#39;not&#39;
&#39;term, society, the, first, a, including, revolution, english&#39; are closest words to &#39;UNK&#39;
&#39;two, zero, five, six, three, seven, nine, eight&#39; are closest words to &#39;four&#39;
&#39;about, i, not, which, it, some, there, he&#39; are closest words to &#39;they&#39;
&#39;two, zero, three, six, nine, four, seven, eight&#39; are closest words to &#39;five&#39;
&#39;where, was, but, are, at, some, he, called&#39; are closest words to &#39;were&#39;
&#39;at, this, all, many, some, or, were, he&#39; are closest words to &#39;but&#39;
&#39;been, by, from, since, were, within, at, western&#39; are closest words to &#39;with&#39;
&#39;other, from, in, are, state, were, similar, at&#39; are closest words to &#39;by&#39;
&#39;could, where, what, would, was, should, are, french&#39; are closest words to &#39;is&#39;
&#39;for, with, own, state, use, and, theory, at&#39; are closest words to &#39;from&#39;
&#39;although, other, army, could, many, all, but, relations&#39; are closest words to &#39;on&#39;
&#39;against, three, zero, five, four, nine, seven, eight&#39; are closest words to &#39;six&#39;
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
