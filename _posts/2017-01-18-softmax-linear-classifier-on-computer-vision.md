---
layout: post
title: "Softmax Linear Classifier on Computer Vision"
description: ""
category: 
tags: 
 - Deep Learning
 - Neural Network
 - Linear Classifier
---
{% include JB/setup %}
<html>
<head><meta charset="utf-8" />
<title>Softmax Linear Classifier for Computer Vision</title>

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
.highlight .n { color: #040404} 
.highlight .c { color: #408080; font-style: italic } /* Comment */
.highlight .err { border: 1px solid #FF0000 } /* Error */
.highlight .k { color: #008000; font-weight: bold } /* Keyword */
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
<h1 id="Softmax-Classifier">Softmax Classifier<a class="anchor-link" href="#Softmax-Classifier">&#182;</a></h1><p>Using a softmax regression function on image recognization.</p>
<p>Softmax classifier is a linear classifier, we won't expect much in accuray because images are highly nonlinear with both high-frequency and low-frequency data. Vision is a  complicated system somehow can abstract huge data into simple perception. The interesting part of this project is what features are extracted by this first order classifier</p>

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
<span class="kn">from</span> <span class="nn">utilities.data_utils</span> <span class="kn">import</span> <span class="o">*</span>

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
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Load preprocessed CIFAR-10 data</span>
<span class="c1"># Mean image has been substracted from test, validation and training</span>
<span class="c1"># images to normalize the data</span>
<span class="c1"># Images has been flatten to NxD (N test cases, D features)</span>
<span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">X_val</span><span class="p">,</span> <span class="n">y_val</span><span class="p">,</span> <span class="n">X_test</span><span class="p">,</span> <span class="n">y_test</span><span class="p">,</span> <span class="n">X_dev</span><span class="p">,</span> <span class="n">y_dev</span> <span class="o">=</span> <span class="n">get_CIFAR10_data</span><span class="p">()</span>

<span class="c1"># Print out data shape to verify</span>
<span class="k">print</span> <span class="s1">&#39;Train data shape: &#39;</span><span class="p">,</span> <span class="n">X_train</span><span class="o">.</span><span class="n">shape</span>
<span class="k">print</span> <span class="s1">&#39;Train labels shape: &#39;</span><span class="p">,</span> <span class="n">y_train</span><span class="o">.</span><span class="n">shape</span>
<span class="k">print</span> <span class="s1">&#39;Validation data shape: &#39;</span><span class="p">,</span> <span class="n">X_val</span><span class="o">.</span><span class="n">shape</span>
<span class="k">print</span> <span class="s1">&#39;Validation labels shape: &#39;</span><span class="p">,</span> <span class="n">y_val</span><span class="o">.</span><span class="n">shape</span>
<span class="k">print</span> <span class="s1">&#39;Test data shape: &#39;</span><span class="p">,</span> <span class="n">X_test</span><span class="o">.</span><span class="n">shape</span>
<span class="k">print</span> <span class="s1">&#39;Test labels shape: &#39;</span><span class="p">,</span> <span class="n">y_test</span><span class="o">.</span><span class="n">shape</span>
<span class="k">print</span> <span class="s1">&#39;dev data shape: &#39;</span><span class="p">,</span> <span class="n">X_dev</span><span class="o">.</span><span class="n">shape</span>
<span class="k">print</span> <span class="s1">&#39;dev labels shape: &#39;</span><span class="p">,</span> <span class="n">y_dev</span><span class="o">.</span><span class="n">shape</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>Train data shape:  (49000, 3072)
Train labels shape:  (49000,)
Validation data shape:  (1000, 3072)
Validation labels shape:  (1000,)
Test data shape:  (1000, 3072)
Test labels shape:  (1000,)
dev data shape:  (500, 3072)
dev labels shape:  (500,)
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[3]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Define Softmax Classifier in Vanilla Python/Numpy</span>

<span class="k">class</span> <span class="nc">LinearClassifier</span><span class="p">(</span><span class="nb">object</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot; </span>
<span class="sd">  Linear Classifier with stochastic gradient descent</span>
<span class="sd">  &quot;&quot;&quot;</span>

  <span class="k">def</span> <span class="nf">__init__</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>
    <span class="bp">self</span><span class="o">.</span><span class="n">W</span> <span class="o">=</span> <span class="bp">None</span>
    <span class="bp">self</span><span class="o">.</span><span class="n">b</span> <span class="o">=</span> <span class="bp">None</span>

  <span class="k">def</span> <span class="nf">train</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> 
            <span class="n">learning_rate</span><span class="o">=</span><span class="mf">1e-3</span><span class="p">,</span> 
            <span class="n">reg</span><span class="o">=</span><span class="mf">1e-5</span><span class="p">,</span> 
            <span class="n">num_iters</span><span class="o">=</span><span class="mi">100</span><span class="p">,</span>
            <span class="n">batch_size</span><span class="o">=</span><span class="mi">200</span><span class="p">,</span> 
            <span class="n">verbose</span><span class="o">=</span><span class="bp">False</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;</span>
<span class="sd">    Train the linear classifier using SGD.</span>

<span class="sd">    Inputs:</span>
<span class="sd">    - X: A numpy array of shape (N, D) containing training data; there are N</span>
<span class="sd">      training samples each of dimension D.</span>
<span class="sd">    - y: A numpy array of shape (N,) containing training labels; y[i] = c</span>
<span class="sd">      means that X[i] has label 0 &lt;= c &lt; C for C classes.</span>
<span class="sd">    - learning_rate: (float) learning rate for optimization.</span>
<span class="sd">    - reg: (float) regularization strength.</span>
<span class="sd">    - num_iters: (integer) number of steps to take when optimizing</span>
<span class="sd">    - batch_size: (integer) number of training examples to use at each step.</span>
<span class="sd">    - verbose: (boolean) If true, print progress during optimization.</span>

<span class="sd">    Outputs:</span>
<span class="sd">    A list containing the value of the loss function at each training iteration.</span>
<span class="sd">    &quot;&quot;&quot;</span>
    <span class="n">num_train</span><span class="p">,</span> <span class="n">dim</span> <span class="o">=</span> <span class="n">X</span><span class="o">.</span><span class="n">shape</span>
    <span class="n">num_classes</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">max</span><span class="p">(</span><span class="n">y</span><span class="p">)</span> <span class="o">+</span> <span class="mi">1</span> <span class="c1"># assume y takes values 0...K-1 where K is number of classes</span>
    <span class="k">if</span> <span class="bp">self</span><span class="o">.</span><span class="n">W</span> <span class="ow">is</span> <span class="bp">None</span><span class="p">:</span>
      <span class="c1"># lazily initialize W</span>
      <span class="bp">self</span><span class="o">.</span><span class="n">W</span> <span class="o">=</span> <span class="mf">0.0001</span> <span class="o">*</span> <span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">randn</span><span class="p">(</span><span class="n">dim</span><span class="p">,</span> <span class="n">num_classes</span><span class="p">)</span>
        
    <span class="k">if</span> <span class="bp">self</span><span class="o">.</span><span class="n">b</span> <span class="ow">is</span> <span class="bp">None</span><span class="p">:</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">b</span> <span class="o">=</span> <span class="mf">0.0001</span> <span class="o">*</span> <span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">randn</span><span class="p">(</span><span class="n">num_classes</span><span class="p">)</span>
        
    <span class="c1"># Run stochastic gradient descent to optimize W</span>
    <span class="n">loss_history</span> <span class="o">=</span> <span class="p">[]</span>
    <span class="k">for</span> <span class="n">it</span> <span class="ow">in</span> <span class="nb">xrange</span><span class="p">(</span><span class="n">num_iters</span><span class="p">):</span>
      <span class="n">X_batch</span> <span class="o">=</span> <span class="bp">None</span>
      <span class="n">y_batch</span> <span class="o">=</span> <span class="bp">None</span>
        
      <span class="n">idxs</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">choice</span><span class="p">(</span><span class="n">num_train</span><span class="p">,</span> <span class="n">size</span><span class="o">=</span><span class="n">batch_size</span><span class="p">,</span> <span class="n">replace</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span>
      <span class="n">X_batch</span> <span class="o">=</span> <span class="n">X</span><span class="p">[</span><span class="n">idxs</span><span class="p">,:]</span>
      <span class="n">y_batch</span> <span class="o">=</span> <span class="n">y</span><span class="p">[</span><span class="n">idxs</span><span class="p">]</span>


      <span class="c1"># evaluate loss and gradient</span>
      <span class="n">loss</span><span class="p">,</span> <span class="n">dw_grad</span><span class="p">,</span> <span class="n">db_grad</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">loss</span><span class="p">(</span><span class="n">X_batch</span><span class="p">,</span> <span class="n">y_batch</span><span class="p">,</span> <span class="n">reg</span><span class="p">)</span>
      <span class="n">loss_history</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">loss</span><span class="p">)</span>

      <span class="bp">self</span><span class="o">.</span><span class="n">W</span> <span class="o">+=</span> <span class="o">-</span> <span class="n">dw_grad</span> <span class="o">*</span> <span class="n">learning_rate</span>
      <span class="bp">self</span><span class="o">.</span><span class="n">b</span> <span class="o">+=</span> <span class="o">-</span> <span class="n">db_grad</span> <span class="o">*</span> <span class="n">learning_rate</span>

      <span class="k">if</span> <span class="n">verbose</span> <span class="ow">and</span> <span class="n">it</span> <span class="o">%</span> <span class="mi">100</span> <span class="o">==</span> <span class="mi">0</span><span class="p">:</span>
        <span class="k">print</span> <span class="s1">&#39;iteration </span><span class="si">%d</span><span class="s1"> / </span><span class="si">%d</span><span class="s1">: loss </span><span class="si">%f</span><span class="s1">&#39;</span> <span class="o">%</span> <span class="p">(</span><span class="n">it</span><span class="p">,</span> <span class="n">num_iters</span><span class="p">,</span> <span class="n">loss</span><span class="p">)</span>

    <span class="k">return</span> <span class="n">loss_history</span>

  <span class="k">def</span> <span class="nf">predict</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">X</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;</span>
<span class="sd">    Use the trained weights of this linear classifier to predict labels for</span>
<span class="sd">    data points.</span>

<span class="sd">    Inputs:</span>
<span class="sd">    - X: D x N array of training data. Each column is a D-dimensional point.</span>

<span class="sd">    Returns:</span>
<span class="sd">    - y_pred: Predicted labels for the data in X. y_pred is a 1-dimensional</span>
<span class="sd">      array of length N, and each element is an integer giving the predicted</span>
<span class="sd">      class.</span>
<span class="sd">    &quot;&quot;&quot;</span>
    <span class="n">y_pred</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">zeros</span><span class="p">(</span><span class="n">X</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">1</span><span class="p">])</span>
    
    <span class="n">scores</span> <span class="o">=</span> <span class="n">X</span><span class="o">.</span><span class="n">dot</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">W</span><span class="p">)</span>
    <span class="n">y_pred</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">argmax</span><span class="p">(</span><span class="n">scores</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>

    <span class="k">return</span> <span class="n">y_pred</span>
  
    

<span class="k">class</span> <span class="nc">Softmax</span><span class="p">(</span><span class="n">LinearClassifier</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot; A subclass that uses the Softmax + Cross-entropy loss function &quot;&quot;&quot;</span>

  <span class="k">def</span> <span class="nf">loss</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">X_batch</span><span class="p">,</span> <span class="n">y_batch</span><span class="p">,</span> <span class="n">reg</span><span class="p">):</span>
      <span class="sd">&quot;&quot;&quot;</span>
<span class="sd">      Softmax loss function.</span>
<span class="sd">      Inputs have dimension D, there are C classes, and we operate on minibatches</span>
<span class="sd">      of N examples.</span>

<span class="sd">      Inputs:</span>
<span class="sd">      - W: A numpy array of shape (D, C) containing weights.</span>
<span class="sd">      - b: A numpy array of shape (C,) for bias</span>
<span class="sd">      - X_batch: A numpy array of shape (N, D) containing a minibatch of data.</span>
<span class="sd">      - y_batch: A numpy array of shape (N,) containing training labels; y[i] = c means</span>
<span class="sd">        that X[i] has label c, where 0 &lt;= c &lt; C.</span>
<span class="sd">      - reg: (float) regularization strength</span>

<span class="sd">      Returns a tuple of:</span>
<span class="sd">      - loss as single float</span>
<span class="sd">      - gradient with respect to weights W; an array of same shape as W</span>

<span class="sd">      &quot;&quot;&quot;</span>
      <span class="n">loss</span> <span class="o">=</span> <span class="mf">0.0</span>
      <span class="n">dW</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">zeros_like</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">W</span><span class="p">)</span> 
      <span class="n">N</span> <span class="o">=</span> <span class="n">X_batch</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span>
      <span class="n">scores</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">dot</span><span class="p">(</span><span class="n">X_batch</span><span class="p">,</span> <span class="bp">self</span><span class="o">.</span><span class="n">W</span><span class="p">)</span> <span class="o">+</span> <span class="bp">self</span><span class="o">.</span><span class="n">b</span>
      <span class="c1"># Numerically stable softmax probability</span>
      <span class="n">probs</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">exp</span><span class="p">(</span><span class="n">scores</span> <span class="o">-</span> <span class="n">np</span><span class="o">.</span><span class="n">max</span><span class="p">(</span><span class="n">scores</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">,</span> <span class="n">keepdims</span><span class="o">=</span><span class="bp">True</span><span class="p">))</span>
      <span class="n">probs</span> <span class="o">=</span> <span class="n">probs</span> <span class="o">/</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">(</span><span class="n">probs</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">,</span> <span class="n">keepdims</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span>
      <span class="n">loss</span> <span class="o">=</span> <span class="o">-</span><span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">log</span><span class="p">(</span><span class="n">probs</span><span class="p">[</span><span class="nb">xrange</span><span class="p">(</span><span class="n">N</span><span class="p">),</span> <span class="n">y_batch</span><span class="p">]))</span> <span class="o">/</span> <span class="n">N</span>
      <span class="n">loss</span> <span class="o">+=</span> <span class="mf">0.5</span> <span class="o">*</span> <span class="n">reg</span> <span class="o">*</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">W</span><span class="o">**</span><span class="mi">2</span><span class="p">)</span>
      <span class="n">dscores</span> <span class="o">=</span> <span class="n">probs</span><span class="o">.</span><span class="n">copy</span><span class="p">()</span>
      <span class="n">dscores</span><span class="p">[</span><span class="nb">xrange</span><span class="p">(</span><span class="n">N</span><span class="p">),</span> <span class="n">y_batch</span><span class="p">]</span> <span class="o">-=</span> <span class="mi">1</span>
      <span class="n">dscores</span> <span class="o">/=</span> <span class="n">N</span>
      <span class="n">dW</span> <span class="o">=</span> <span class="n">X_batch</span><span class="o">.</span><span class="n">T</span><span class="o">.</span><span class="n">dot</span><span class="p">(</span><span class="n">dscores</span><span class="p">)</span> <span class="o">+</span> <span class="n">reg</span> <span class="o">*</span> <span class="bp">self</span><span class="o">.</span><span class="n">W</span>
      <span class="n">db</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">(</span><span class="n">dscores</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="mi">0</span><span class="p">)</span>
      
      <span class="k">return</span> <span class="n">loss</span><span class="p">,</span> <span class="n">dW</span><span class="p">,</span> <span class="n">db</span>
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
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1">#Sanity Check on loss function</span>
<span class="n">softmax</span> <span class="o">=</span> <span class="n">Softmax</span><span class="p">()</span>

<span class="n">softmax</span><span class="o">.</span><span class="n">train</span><span class="p">(</span><span class="n">X_dev</span><span class="p">,</span> <span class="n">y_dev</span><span class="p">,</span> <span class="n">learning_rate</span><span class="o">=</span><span class="mi">0</span><span class="p">,</span> 
            <span class="n">reg</span><span class="o">=</span><span class="mi">0</span><span class="p">,</span> 
            <span class="n">num_iters</span><span class="o">=</span><span class="mi">0</span><span class="p">,</span>
            <span class="n">batch_size</span><span class="o">=</span><span class="mi">0</span><span class="p">,</span> 
            <span class="n">verbose</span><span class="o">=</span><span class="bp">False</span><span class="p">)</span>

<span class="c1">#softmax.W = np.random.randn(3072, 10) * 0.0001</span>
<span class="c1">#softmax.b = np.random.randn(10) * 0.0001</span>
<span class="n">loss</span><span class="p">,</span> <span class="n">dW</span><span class="p">,</span> <span class="n">db</span> <span class="o">=</span> <span class="n">softmax</span><span class="o">.</span><span class="n">loss</span><span class="p">(</span><span class="n">X_dev</span><span class="p">,</span> <span class="n">y_dev</span><span class="p">,</span> <span class="mf">0.0</span><span class="p">)</span>
<span class="k">print</span> <span class="n">loss</span>
<span class="c1"># Loss value should be around log(0.1) = 2.3</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>2.37010671374
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
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Search hyper parameters for the best combination</span>
<span class="n">results</span> <span class="o">=</span> <span class="p">{}</span>
<span class="n">best_val</span> <span class="o">=</span> <span class="o">-</span><span class="mi">1</span>
<span class="n">best_softmax</span> <span class="o">=</span> <span class="bp">None</span>
<span class="n">learning_rates</span> <span class="o">=</span> <span class="p">[</span><span class="mf">5e-8</span><span class="p">,</span> <span class="mf">1e-7</span><span class="p">,</span> <span class="mf">5e-7</span><span class="p">]</span>
<span class="n">regularization_strengths</span> <span class="o">=</span> <span class="p">[</span><span class="mf">1e4</span><span class="p">,</span> <span class="mf">5e4</span><span class="p">,</span> <span class="mf">1e3</span><span class="p">]</span>

<span class="k">for</span> <span class="n">lr</span> <span class="ow">in</span> <span class="n">learning_rates</span><span class="p">:</span>
    <span class="k">for</span> <span class="n">rs</span> <span class="ow">in</span> <span class="n">regularization_strengths</span><span class="p">:</span>
        <span class="n">softmax</span> <span class="o">=</span> <span class="n">Softmax</span><span class="p">()</span>
        <span class="n">loss_hist</span> <span class="o">=</span> <span class="n">softmax</span><span class="o">.</span><span class="n">train</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">learning_rate</span><span class="o">=</span><span class="n">lr</span><span class="p">,</span> <span class="n">reg</span><span class="o">=</span><span class="n">rs</span><span class="p">,</span>
                      <span class="n">num_iters</span><span class="o">=</span><span class="mi">1500</span><span class="p">,</span> <span class="n">verbose</span><span class="o">=</span><span class="bp">False</span><span class="p">)</span>
        <span class="n">y_train_pred</span> <span class="o">=</span> <span class="n">softmax</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_train</span><span class="p">)</span>
        <span class="n">train_accuracy</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">mean</span><span class="p">(</span><span class="n">y_train</span> <span class="o">==</span> <span class="n">y_train_pred</span><span class="p">)</span>
        <span class="n">y_val_pred</span> <span class="o">=</span> <span class="n">softmax</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_val</span><span class="p">)</span>
        <span class="n">val_accuracy</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">mean</span><span class="p">(</span><span class="n">y_val</span> <span class="o">==</span> <span class="n">y_val_pred</span><span class="p">)</span>
        <span class="n">results</span><span class="p">[(</span><span class="n">lr</span><span class="p">,</span> <span class="n">rs</span><span class="p">)]</span> <span class="o">=</span> <span class="p">(</span><span class="n">train_accuracy</span><span class="p">,</span> <span class="n">val_accuracy</span><span class="p">)</span>
        <span class="k">if</span> <span class="n">val_accuracy</span> <span class="o">&gt;</span> <span class="n">best_val</span><span class="p">:</span>
            <span class="n">best_val</span> <span class="o">=</span> <span class="n">val_accuracy</span>
            <span class="n">best_softmax</span> <span class="o">=</span> <span class="n">softmax</span>
   
<span class="c1"># Print out results.</span>
<span class="k">for</span> <span class="n">lr</span><span class="p">,</span> <span class="n">reg</span> <span class="ow">in</span> <span class="nb">sorted</span><span class="p">(</span><span class="n">results</span><span class="p">):</span>
    <span class="n">train_accuracy</span><span class="p">,</span> <span class="n">val_accuracy</span> <span class="o">=</span> <span class="n">results</span><span class="p">[(</span><span class="n">lr</span><span class="p">,</span> <span class="n">reg</span><span class="p">)]</span>
    <span class="k">print</span> <span class="s1">&#39;lr </span><span class="si">%e</span><span class="s1"> reg </span><span class="si">%e</span><span class="s1"> train accuracy: </span><span class="si">%f</span><span class="s1"> val accuracy: </span><span class="si">%f</span><span class="s1">&#39;</span> <span class="o">%</span> <span class="p">(</span>
                <span class="n">lr</span><span class="p">,</span> <span class="n">reg</span><span class="p">,</span> <span class="n">train_accuracy</span><span class="p">,</span> <span class="n">val_accuracy</span><span class="p">)</span>
    
<span class="k">print</span> <span class="s1">&#39;best validation accuracy achieved during cross-validation: </span><span class="si">%f</span><span class="s1">&#39;</span> <span class="o">%</span> <span class="n">best_val</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>lr 5.000000e-08 reg 1.000000e+03 train accuracy: 0.363510 val accuracy: 0.363000
lr 5.000000e-08 reg 1.000000e+04 train accuracy: 0.357327 val accuracy: 0.380000
lr 5.000000e-08 reg 5.000000e+04 train accuracy: 0.326776 val accuracy: 0.342000
lr 1.000000e-07 reg 1.000000e+03 train accuracy: 0.379347 val accuracy: 0.399000
lr 1.000000e-07 reg 1.000000e+04 train accuracy: 0.371061 val accuracy: 0.386000
lr 1.000000e-07 reg 5.000000e+04 train accuracy: 0.326571 val accuracy: 0.342000
lr 5.000000e-07 reg 1.000000e+03 train accuracy: 0.408571 val accuracy: 0.408000
lr 5.000000e-07 reg 1.000000e+04 train accuracy: 0.371735 val accuracy: 0.387000
lr 5.000000e-07 reg 5.000000e+04 train accuracy: 0.329143 val accuracy: 0.343000
best validation accuracy achieved during cross-validation: 0.408000
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
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># evaluate on test set</span>
<span class="c1"># Evaluate the best softmax on test set</span>
<span class="n">y_test_pred</span> <span class="o">=</span> <span class="n">best_softmax</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_test</span><span class="p">)</span>
<span class="n">test_accuracy</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">mean</span><span class="p">(</span><span class="n">y_test</span> <span class="o">==</span> <span class="n">y_test_pred</span><span class="p">)</span>
<span class="k">print</span> <span class="s1">&#39;softmax on raw pixels final test set accuracy: </span><span class="si">%f</span><span class="s1">&#39;</span> <span class="o">%</span> <span class="p">(</span><span class="n">test_accuracy</span><span class="p">,</span> <span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>softmax on raw pixels final test set accuracy: 0.394000
</pre>
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
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Visualize the learned weights for each class</span>
<span class="n">w</span> <span class="o">=</span> <span class="n">best_softmax</span><span class="o">.</span><span class="n">W</span>
<span class="n">w</span> <span class="o">=</span> <span class="n">w</span><span class="o">.</span><span class="n">reshape</span><span class="p">(</span><span class="mi">32</span><span class="p">,</span> <span class="mi">32</span><span class="p">,</span> <span class="mi">3</span><span class="p">,</span> <span class="mi">10</span><span class="p">)</span>

<span class="n">w_min</span><span class="p">,</span> <span class="n">w_max</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">min</span><span class="p">(</span><span class="n">w</span><span class="p">),</span> <span class="n">np</span><span class="o">.</span><span class="n">max</span><span class="p">(</span><span class="n">w</span><span class="p">)</span>

<span class="n">classes</span> <span class="o">=</span> <span class="p">[</span><span class="s1">&#39;plane&#39;</span><span class="p">,</span> <span class="s1">&#39;car&#39;</span><span class="p">,</span> <span class="s1">&#39;bird&#39;</span><span class="p">,</span> <span class="s1">&#39;cat&#39;</span><span class="p">,</span> <span class="s1">&#39;deer&#39;</span><span class="p">,</span> <span class="s1">&#39;dog&#39;</span><span class="p">,</span> <span class="s1">&#39;frog&#39;</span><span class="p">,</span> <span class="s1">&#39;horse&#39;</span><span class="p">,</span> <span class="s1">&#39;ship&#39;</span><span class="p">,</span> <span class="s1">&#39;truck&#39;</span><span class="p">]</span>
<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">xrange</span><span class="p">(</span><span class="mi">10</span><span class="p">):</span>
  <span class="n">plt</span><span class="o">.</span><span class="n">subplot</span><span class="p">(</span><span class="mi">2</span><span class="p">,</span> <span class="mi">5</span><span class="p">,</span> <span class="n">i</span> <span class="o">+</span> <span class="mi">1</span><span class="p">)</span>
  
  <span class="c1"># Rescale the weights to be between 0 and 255</span>
  <span class="n">wimg</span> <span class="o">=</span> <span class="mf">255.0</span> <span class="o">*</span> <span class="p">(</span><span class="n">w</span><span class="p">[:,</span> <span class="p">:,</span> <span class="p">:,</span> <span class="n">i</span><span class="p">]</span><span class="o">.</span><span class="n">squeeze</span><span class="p">()</span> <span class="o">-</span> <span class="n">w_min</span><span class="p">)</span> <span class="o">/</span> <span class="p">(</span><span class="n">w_max</span> <span class="o">-</span> <span class="n">w_min</span><span class="p">)</span>
  <span class="n">plt</span><span class="o">.</span><span class="n">imshow</span><span class="p">(</span><span class="n">wimg</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="s1">&#39;uint8&#39;</span><span class="p">))</span>
  <span class="n">plt</span><span class="o">.</span><span class="n">axis</span><span class="p">(</span><span class="s1">&#39;off&#39;</span><span class="p">)</span>
  <span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="n">classes</span><span class="p">[</span><span class="n">i</span><span class="p">])</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
hwbRA+86g2aGzOAPgfGK+ZxRlYOIjmulyZxQb8zAkJmgwRwA+/u/7XNnt41GZzD64JVag6vQ8xQ6
RMgcfpt/hcu82QsSEQkf0407t8BfY34RvFJT5utSQcPm/rvKHGp0eIkPvvT6q84UKh+Kh9EImijN
fKYfiswQEvz1/x3Ml1yRUERsBmK4w5grgdbAfXoa0TodDqHEK+rXBV7RF7PCJ15BGn9PxXxdo8i0
cdnLkGfy+qOgzFY1whyi0tnO81fk53glesrfldEuRMxhwL8Hv2gEpmAp0K6EJDxexrrYgYZEvP4M
NCqE8fefWGLukH/xNuBl/Jr38EljdvpVEU0oA4uBhVLUWLO8LJYgpmhKeCpESXgWxOf1lipz2M6c
IT6VzSGIzL9LJlgwk+SSM7ITacyhRKmovMJKZaZghioSghKk11Dk0EAM0L//7I7pvArDwE3mLrn8
PS769RwI87/UMROSCUPms+zhsyegA1Uwm9ctI+aw5Cx6x//5vZ/PzNe+hEKNkDmcmFMnasyMi5gl
67wsmG3fHmNGvxJI6OsnEbpOc54IuDj+MtCNl9glAJXZNp4nZ8GY+Qd7crokqhrZpgY6RBhD8AE5
4qX0fP0sCh5TyhQv0dE8azKlUjF33nuTV6aJov76dBHBXWnhVBdSzDb18MFwZzhon8FewpxJQufV
X9eYv7Njnsx7CkaCLy2qA8odMNQyljb0kPlcyezQZonXZ8EUronKa8gbxBJ4JqmwyEyktQSU1+fU
mHkt6oLZ7EqRlGGKyMsFoiAmaE4Uz6yWGQRtGB4vA6FON0XWWfMuJizJ8CyzU5qcXKAUwyWR86Cl
oBRYylxJT4ehmjHROb+UfF6HWbDk4LIIdYUkL516moFgFkoJyC9raJfZEdZXGJF9IcVU4qtB0Ccn
JycnJyf/Jfmqcvvk5OTk5OTkvyhnEXBycnJycvKTchYBJycnJycnPylnEXBycnJycvKTchYBJycn
JycnPylnEXBycnJycvKTchYBJycnJycnPylnEXBycnJycvKTchYBJycnJycnPylnEXBycnJycvKT
chYBJycnJycnPylnEXBycnJycvKTchYBJycnJycnPylnEXBycnJycvKTchYBJycnJycnPylnEXBy
cnJycvKTchYBJycnJycnPylnEXBycnJycvKTchYBJycnJycnPylnEXBycnJycvKTchYBJycnJycn
PylnEXBycnJycvKTchYBJycnJycnPylnEXBycnJycvKTchYBJycnJycnPylnEXBycnJycvKTchYB
JycnJycnPylnEXBycnJycvKTchYBJycnJycnPyn/P0Bx6GqvbNmMAAAAAElFTkSuQmCC
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
