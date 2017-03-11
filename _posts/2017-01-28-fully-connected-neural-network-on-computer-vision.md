---
layout: post
title: "Fully Connected Neural Network on Computer Vision"
description: ""
category: 
tags:
 - Deep Learning
 - Neural Network
 - Fully Connected Network
---
{% include JB/setup %}
<html>
<head><meta charset="utf-8" />
<title>FC_NeuralNetwork_batchnorm</title><script src="https://cdnjs.cloudflare.com/ajax/libs/require.js/2.1.10/require.min.js"></script>
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
<h1 id="Fully-Connected-Neural-Network-with-Batch-Normalization">Fully-Connected Neural Network with Batch Normalization<a class="anchor-link" href="#Fully-Connected-Neural-Network-with-Batch-Normalization">&#182;</a></h1><p>Two layers of fully connected nerual network.<p>
Adapated based on class project</p>
<p>Activation function uses Rectified Linear Unit <a href="https://en.wikipedia.org/wiki/Rectifier_(neural_networks">(ReLU)</a></p>
<p>To help activations pass through layers of network, <a href="jmlr.org/proceedings/papers/v37/ioffe15.pdf">Batch Normalization</a> layer is added to center and normalize the activations</p>

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
<span class="kn">from</span> <span class="nn">utilities.solver</span> <span class="kn">import</span> <span class="n">Solver</span>

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
<span class="n">data</span> <span class="o">=</span> <span class="n">get_CIFAR10_data</span><span class="p">()</span>
<span class="k">for</span> <span class="n">k</span><span class="p">,</span> <span class="n">v</span> <span class="ow">in</span> <span class="n">data</span><span class="o">.</span><span class="n">iteritems</span><span class="p">():</span>
  <span class="k">print</span> <span class="s1">&#39;</span><span class="si">%s</span><span class="s1">: &#39;</span> <span class="o">%</span> <span class="n">k</span><span class="p">,</span> <span class="n">v</span><span class="o">.</span><span class="n">shape</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>X_val:  (1000, 3072)
X_train:  (49000, 3072)
y_train:  (49000,)
X_test:  (1000, 3072)
y_val:  (1000,)
y_dev:  (100,)
X_dev:  (100, 3072)
y_test:  (1000,)
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
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Define FC layer (affine), ReLU, batchnorm</span>
<span class="c1"># Both forward and backward pass</span>

<span class="k">def</span> <span class="nf">affine_forward</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">w</span><span class="p">,</span> <span class="n">b</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot;</span>
<span class="sd">  Computes the forward pass for an affine (fully-connected) layer.</span>

<span class="sd">  Inputs:</span>
<span class="sd">  - x: A numpy array containing input data, of shape (N, d_1, ..., d_k)</span>
<span class="sd">  - w: A numpy array of weights, of shape (D, M)</span>
<span class="sd">  - b: A numpy array of biases, of shape (M,)</span>
<span class="sd">  </span>
<span class="sd">  Returns a tuple of:</span>
<span class="sd">  - out: output, of shape (N, M)</span>
<span class="sd">  - cache: (x, w, b)</span>
<span class="sd">  &quot;&quot;&quot;</span>
  <span class="n">out</span> <span class="o">=</span> <span class="bp">None</span>
  <span class="n">N</span> <span class="o">=</span> <span class="n">x</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span>
  <span class="n">x_mat</span> <span class="o">=</span> <span class="n">x</span><span class="o">.</span><span class="n">reshape</span><span class="p">(</span><span class="n">N</span><span class="p">,</span> <span class="o">-</span><span class="mi">1</span><span class="p">)</span>
  <span class="n">out</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">dot</span><span class="p">(</span><span class="n">x_mat</span><span class="p">,</span> <span class="n">w</span><span class="p">)</span> <span class="o">+</span> <span class="n">b</span>
  <span class="n">cache</span> <span class="o">=</span> <span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">w</span><span class="p">,</span> <span class="n">b</span><span class="p">)</span>
  <span class="k">return</span> <span class="n">out</span><span class="p">,</span> <span class="n">cache</span>


<span class="k">def</span> <span class="nf">affine_backward</span><span class="p">(</span><span class="n">dout</span><span class="p">,</span> <span class="n">cache</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot;</span>
<span class="sd">  Computes the backward pass for an affine layer.</span>

<span class="sd">  Inputs:</span>
<span class="sd">  - dout: Upstream derivative, of shape (N, M)</span>
<span class="sd">  - cache: Tuple of:</span>
<span class="sd">    - x: Input data, of shape (N, d_1, ... d_k)</span>
<span class="sd">    - w: Weights, of shape (D, M)</span>

<span class="sd">  Returns a tuple of:</span>
<span class="sd">  - dx: Gradient with respect to x, of shape (N, d1, ..., d_k)</span>
<span class="sd">  - dw: Gradient with respect to w, of shape (D, M)</span>
<span class="sd">  - db: Gradient with respect to b, of shape (M,)</span>
<span class="sd">  &quot;&quot;&quot;</span>
  <span class="n">x</span><span class="p">,</span> <span class="n">w</span><span class="p">,</span> <span class="n">b</span> <span class="o">=</span> <span class="n">cache</span>
  <span class="n">N</span> <span class="o">=</span> <span class="n">x</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span>
  <span class="n">x_mat</span> <span class="o">=</span> <span class="n">x</span><span class="o">.</span><span class="n">reshape</span><span class="p">(</span><span class="n">N</span><span class="p">,</span> <span class="o">-</span><span class="mi">1</span><span class="p">)</span>
  <span class="n">dx</span> <span class="o">=</span> <span class="n">dout</span><span class="o">.</span><span class="n">dot</span><span class="p">(</span><span class="n">w</span><span class="o">.</span><span class="n">T</span><span class="p">)</span><span class="o">.</span><span class="n">reshape</span><span class="p">(</span><span class="o">*</span><span class="n">x</span><span class="o">.</span><span class="n">shape</span><span class="p">)</span>
  <span class="n">dw</span> <span class="o">=</span> <span class="n">x_mat</span><span class="o">.</span><span class="n">T</span><span class="o">.</span><span class="n">dot</span><span class="p">(</span><span class="n">dout</span><span class="p">)</span>
  <span class="n">db</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">(</span><span class="n">dout</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="mi">0</span><span class="p">)</span>
  <span class="k">return</span> <span class="n">dx</span><span class="p">,</span> <span class="n">dw</span><span class="p">,</span> <span class="n">db</span>


<span class="k">def</span> <span class="nf">relu_forward</span><span class="p">(</span><span class="n">x</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot;</span>
<span class="sd">  Computes the forward pass for a layer of rectified linear units (ReLUs).</span>

<span class="sd">  Input:</span>
<span class="sd">  - x: Inputs, of any shape</span>

<span class="sd">  Returns a tuple of:</span>
<span class="sd">  - out: Output, of the same shape as x</span>
<span class="sd">  - cache: x</span>
<span class="sd">  &quot;&quot;&quot;</span>
  <span class="n">out</span> <span class="o">=</span> <span class="n">x</span><span class="o">.</span><span class="n">copy</span><span class="p">()</span>
  <span class="n">out</span><span class="p">[</span><span class="n">out</span><span class="o">&lt;=</span><span class="mi">0</span><span class="p">]</span> <span class="o">=</span> <span class="mi">0</span>
  <span class="n">cache</span> <span class="o">=</span> <span class="n">x</span>
  <span class="k">return</span> <span class="n">out</span><span class="p">,</span> <span class="n">cache</span>


<span class="k">def</span> <span class="nf">relu_backward</span><span class="p">(</span><span class="n">dout</span><span class="p">,</span> <span class="n">cache</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot;</span>
<span class="sd">  Computes the backward pass for a layer of rectified linear units (ReLUs).</span>

<span class="sd">  Input:</span>
<span class="sd">  - dout: Upstream derivatives, of any shape</span>
<span class="sd">  - cache: Input x, of same shape as dout</span>

<span class="sd">  Returns:</span>
<span class="sd">  - dx: Gradient with respect to x</span>
<span class="sd">  &quot;&quot;&quot;</span>
  <span class="n">dx</span><span class="p">,</span> <span class="n">x</span> <span class="o">=</span> <span class="bp">None</span><span class="p">,</span> <span class="n">cache</span>
  <span class="n">dx</span> <span class="o">=</span> <span class="n">dout</span><span class="o">.</span><span class="n">copy</span><span class="p">()</span>
  <span class="n">dx</span><span class="p">[</span><span class="n">x</span><span class="o">&lt;=</span><span class="mi">0</span><span class="p">]</span> <span class="o">=</span> <span class="mi">0</span>
  <span class="k">return</span> <span class="n">dx</span>


<span class="k">def</span> <span class="nf">batchnorm_forward</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">gamma</span><span class="p">,</span> <span class="n">beta</span><span class="p">,</span> <span class="n">bn_param</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot;</span>
<span class="sd">  Forward pass for batch normalization.</span>

<span class="sd">  running_mean = momentum * running_mean + (1 - momentum) * sample_mean</span>
<span class="sd">  running_var = momentum * running_var + (1 - momentum) * sample_var</span>

<span class="sd">  Input:</span>
<span class="sd">  - x: Data of shape (N, D)</span>
<span class="sd">  - gamma: Scale parameter of shape (D,)</span>
<span class="sd">  - beta: Shift paremeter of shape (D,)</span>
<span class="sd">  - bn_param: Dictionary with the following keys:</span>
<span class="sd">    - mode: &#39;train&#39; or &#39;test&#39;; required</span>
<span class="sd">    - eps: Constant for numeric stability</span>
<span class="sd">    - momentum: Constant for running mean / variance.</span>
<span class="sd">    - running_mean: Array of shape (D,) giving running mean of features</span>
<span class="sd">    - running_var Array of shape (D,) giving running variance of features</span>

<span class="sd">  Returns a tuple of:</span>
<span class="sd">  - out: of shape (N, D)</span>
<span class="sd">  - cache: A tuple of values needed in the backward pass</span>
<span class="sd">  &quot;&quot;&quot;</span>
  <span class="n">mode</span> <span class="o">=</span> <span class="n">bn_param</span><span class="p">[</span><span class="s1">&#39;mode&#39;</span><span class="p">]</span>
  <span class="n">eps</span> <span class="o">=</span> <span class="n">bn_param</span><span class="o">.</span><span class="n">get</span><span class="p">(</span><span class="s1">&#39;eps&#39;</span><span class="p">,</span> <span class="mf">1e-5</span><span class="p">)</span>
  <span class="n">momentum</span> <span class="o">=</span> <span class="n">bn_param</span><span class="o">.</span><span class="n">get</span><span class="p">(</span><span class="s1">&#39;momentum&#39;</span><span class="p">,</span> <span class="mf">0.9</span><span class="p">)</span>

  <span class="n">N</span><span class="p">,</span> <span class="n">D</span> <span class="o">=</span> <span class="n">x</span><span class="o">.</span><span class="n">shape</span>
  <span class="n">running_mean</span> <span class="o">=</span> <span class="n">bn_param</span><span class="o">.</span><span class="n">get</span><span class="p">(</span><span class="s1">&#39;running_mean&#39;</span><span class="p">,</span> <span class="n">np</span><span class="o">.</span><span class="n">zeros</span><span class="p">(</span><span class="n">D</span><span class="p">,</span> <span class="n">dtype</span><span class="o">=</span><span class="n">x</span><span class="o">.</span><span class="n">dtype</span><span class="p">))</span>
  <span class="n">running_var</span> <span class="o">=</span> <span class="n">bn_param</span><span class="o">.</span><span class="n">get</span><span class="p">(</span><span class="s1">&#39;running_var&#39;</span><span class="p">,</span> <span class="n">np</span><span class="o">.</span><span class="n">zeros</span><span class="p">(</span><span class="n">D</span><span class="p">,</span> <span class="n">dtype</span><span class="o">=</span><span class="n">x</span><span class="o">.</span><span class="n">dtype</span><span class="p">))</span>

  <span class="n">out</span><span class="p">,</span> <span class="n">cache</span> <span class="o">=</span> <span class="bp">None</span><span class="p">,</span> <span class="bp">None</span>
  <span class="k">if</span> <span class="n">mode</span> <span class="o">==</span> <span class="s1">&#39;train&#39;</span><span class="p">:</span>
    <span class="n">x_mean</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">mean</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="mi">0</span><span class="p">)</span>
    <span class="n">x_var</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">var</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="mi">0</span><span class="p">)</span>
    <span class="n">running_mean</span> <span class="o">=</span> <span class="n">momentum</span> <span class="o">*</span> <span class="n">running_mean</span> <span class="o">+</span> <span class="p">(</span><span class="mi">1</span> <span class="o">-</span> <span class="n">momentum</span><span class="p">)</span> <span class="o">*</span> <span class="n">x_mean</span>
    <span class="n">running_var</span> <span class="o">=</span> <span class="n">momentum</span> <span class="o">*</span> <span class="n">running_var</span> <span class="o">+</span> <span class="p">(</span><span class="mi">1</span> <span class="o">-</span> <span class="n">momentum</span><span class="p">)</span> <span class="o">*</span> <span class="n">x_var</span>
    <span class="n">x_nom</span> <span class="o">=</span> <span class="p">(</span><span class="n">x</span> <span class="o">-</span> <span class="n">x_mean</span><span class="p">)</span> <span class="o">/</span> <span class="n">np</span><span class="o">.</span><span class="n">sqrt</span><span class="p">(</span><span class="n">x_var</span> <span class="o">+</span> <span class="n">eps</span><span class="p">)</span>
    <span class="n">out</span> <span class="o">=</span> <span class="n">gamma</span> <span class="o">*</span> <span class="n">x_nom</span> <span class="o">+</span> <span class="n">beta</span>
    <span class="n">cache</span> <span class="o">=</span> <span class="n">x</span><span class="p">,</span> <span class="n">x_nom</span><span class="p">,</span> <span class="n">x_mean</span><span class="p">,</span> <span class="n">x_var</span><span class="p">,</span> <span class="n">gamma</span><span class="p">,</span> <span class="n">beta</span><span class="p">,</span> <span class="n">eps</span>

  <span class="k">elif</span> <span class="n">mode</span> <span class="o">==</span> <span class="s1">&#39;test&#39;</span><span class="p">:</span>
    <span class="n">out</span> <span class="o">=</span> <span class="p">(</span><span class="n">x</span> <span class="o">-</span> <span class="n">running_mean</span><span class="p">)</span> <span class="o">/</span> <span class="n">np</span><span class="o">.</span><span class="n">sqrt</span><span class="p">(</span><span class="n">running_var</span> <span class="o">+</span> <span class="n">eps</span><span class="p">)</span>
    <span class="n">out</span> <span class="o">=</span> <span class="n">gamma</span> <span class="o">*</span> <span class="n">out</span> <span class="o">+</span> <span class="n">beta</span>
  <span class="k">else</span><span class="p">:</span>
    <span class="k">raise</span> <span class="ne">ValueError</span><span class="p">(</span><span class="s1">&#39;Invalid forward batchnorm mode &quot;</span><span class="si">%s</span><span class="s1">&quot;&#39;</span> <span class="o">%</span> <span class="n">mode</span><span class="p">)</span>

  <span class="c1"># Store the updated running means back into bn_param</span>
  <span class="n">bn_param</span><span class="p">[</span><span class="s1">&#39;running_mean&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">running_mean</span>
  <span class="n">bn_param</span><span class="p">[</span><span class="s1">&#39;running_var&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">running_var</span>

  <span class="k">return</span> <span class="n">out</span><span class="p">,</span> <span class="n">cache</span>


<span class="k">def</span> <span class="nf">batchnorm_backward</span><span class="p">(</span><span class="n">dout</span><span class="p">,</span> <span class="n">cache</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot;</span>
<span class="sd">  Backward pass for batch normalization.</span>

<span class="sd">  </span>
<span class="sd">  Inputs:</span>
<span class="sd">  - dout: Upstream derivatives, of shape (N, D)</span>
<span class="sd">  - cache: Variable of intermediates from batchnorm_forward.</span>
<span class="sd">  </span>
<span class="sd">  Returns a tuple of:</span>
<span class="sd">  - dx: Gradient with respect to inputs x, of shape (N, D)</span>
<span class="sd">  - dgamma: Gradient with respect to scale parameter gamma, of shape (D,)</span>
<span class="sd">  - dbeta: Gradient with respect to shift parameter beta, of shape (D,)</span>
<span class="sd">  &quot;&quot;&quot;</span>
  <span class="n">dx</span><span class="p">,</span> <span class="n">dgamma</span><span class="p">,</span> <span class="n">dbeta</span> <span class="o">=</span> <span class="bp">None</span><span class="p">,</span> <span class="bp">None</span><span class="p">,</span> <span class="bp">None</span>
  <span class="n">x</span><span class="p">,</span> <span class="n">x_nom</span><span class="p">,</span> <span class="n">x_mean</span><span class="p">,</span> <span class="n">x_var</span><span class="p">,</span> <span class="n">gamma</span><span class="p">,</span> <span class="n">beta</span><span class="p">,</span> <span class="n">eps</span> <span class="o">=</span> <span class="n">cache</span>
  <span class="n">m</span> <span class="o">=</span> <span class="n">x</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span>
  <span class="n">dgamma</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">(</span><span class="n">dout</span> <span class="o">*</span> <span class="n">x_nom</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="mi">0</span><span class="p">)</span>
  <span class="n">dbeta</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">(</span><span class="n">dout</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="mi">0</span><span class="p">)</span>
  <span class="n">dx_nom</span> <span class="o">=</span> <span class="n">dout</span> <span class="o">*</span> <span class="n">gamma</span>
  <span class="n">d_var</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">(</span><span class="n">dx_nom</span> <span class="o">*</span> <span class="p">(</span><span class="n">x</span> <span class="o">-</span> <span class="n">x_mean</span><span class="p">)</span> <span class="o">*</span> <span class="p">(</span><span class="o">-</span><span class="mf">0.5</span><span class="p">)</span> <span class="o">*</span> <span class="p">((</span><span class="n">x_var</span> <span class="o">+</span> <span class="n">eps</span><span class="p">)</span> <span class="o">**</span> <span class="p">(</span><span class="o">-</span><span class="mf">1.5</span><span class="p">)),</span> <span class="n">axis</span><span class="o">=</span><span class="mi">0</span><span class="p">)</span>
  <span class="n">d_mean</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">(</span><span class="n">dx_nom</span> <span class="o">*</span> <span class="o">-</span><span class="mi">1</span><span class="o">/</span><span class="n">np</span><span class="o">.</span><span class="n">sqrt</span><span class="p">(</span><span class="n">x_var</span> <span class="o">+</span> <span class="n">eps</span><span class="p">),</span> <span class="n">axis</span><span class="o">=</span><span class="mi">0</span><span class="p">)</span> <span class="o">+</span> <span class="n">d_var</span> <span class="o">*</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">(</span><span class="mi">2</span><span class="o">*</span><span class="p">(</span><span class="n">x_mean</span> <span class="o">-</span> <span class="n">x</span><span class="p">),</span> <span class="n">axis</span><span class="o">=</span><span class="mi">0</span><span class="p">)</span><span class="o">/</span><span class="n">m</span>
  <span class="n">dx</span> <span class="o">=</span> <span class="n">dx_nom</span> <span class="o">*</span> <span class="mi">1</span><span class="o">/</span><span class="n">np</span><span class="o">.</span><span class="n">sqrt</span><span class="p">(</span><span class="n">x_var</span> <span class="o">+</span> <span class="n">eps</span><span class="p">)</span> <span class="o">+</span> <span class="n">d_var</span> <span class="o">*</span> <span class="mi">2</span><span class="o">*</span><span class="p">(</span><span class="n">x</span> <span class="o">-</span> <span class="n">x_mean</span><span class="p">)</span><span class="o">/</span><span class="n">m</span> <span class="o">+</span> <span class="n">d_mean</span><span class="o">/</span><span class="n">m</span>

  <span class="k">return</span> <span class="n">dx</span><span class="p">,</span> <span class="n">dgamma</span><span class="p">,</span> <span class="n">dbeta</span>

<span class="k">def</span> <span class="nf">softmax_loss</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">y</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot;</span>
<span class="sd">  Computes the loss and gradient for softmax classification.</span>

<span class="sd">  Inputs:</span>
<span class="sd">  - x: Input data, of shape (N, C) where x[i, j] is the score for the jth class</span>
<span class="sd">    for the ith input.</span>
<span class="sd">  - y: Vector of labels, of shape (N,) where y[i] is the label for x[i] and</span>
<span class="sd">    0 &lt;= y[i] &lt; C</span>

<span class="sd">  Returns a tuple of:</span>
<span class="sd">  - loss: Scalar giving the loss</span>
<span class="sd">  - dx: Gradient of the loss with respect to x</span>
<span class="sd">  &quot;&quot;&quot;</span>
  <span class="n">probs</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">exp</span><span class="p">(</span><span class="n">x</span> <span class="o">-</span> <span class="n">np</span><span class="o">.</span><span class="n">max</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">,</span> <span class="n">keepdims</span><span class="o">=</span><span class="bp">True</span><span class="p">))</span>
  <span class="n">probs</span> <span class="o">/=</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">(</span><span class="n">probs</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">,</span> <span class="n">keepdims</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span>
  <span class="n">N</span> <span class="o">=</span> <span class="n">x</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span>
  <span class="n">loss</span> <span class="o">=</span> <span class="o">-</span><span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">log</span><span class="p">(</span><span class="n">probs</span><span class="p">[</span><span class="n">np</span><span class="o">.</span><span class="n">arange</span><span class="p">(</span><span class="n">N</span><span class="p">),</span> <span class="n">y</span><span class="p">]))</span> <span class="o">/</span> <span class="n">N</span>
  <span class="n">dx</span> <span class="o">=</span> <span class="n">probs</span><span class="o">.</span><span class="n">copy</span><span class="p">()</span>
  <span class="n">dx</span><span class="p">[</span><span class="n">np</span><span class="o">.</span><span class="n">arange</span><span class="p">(</span><span class="n">N</span><span class="p">),</span> <span class="n">y</span><span class="p">]</span> <span class="o">-=</span> <span class="mi">1</span>
  <span class="n">dx</span> <span class="o">/=</span> <span class="n">N</span>
  <span class="k">return</span> <span class="n">loss</span><span class="p">,</span> <span class="n">dx</span>
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
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Create two layer neural network: FC --&gt; BatchNorm --&gt; ReLU --&gt; FC --&gt; Softmax</span>
<span class="c1"># Neural Network construction will be wrappered in a class in later projects</span>
<span class="c1"># Here two layers means the two FC layers. BatchNorm are for data initialization purpose</span>
<span class="c1"># ReLU adds nonlinear function to the network</span>


<span class="c1"># In this project, parameter initialization (random numbers for weights) is </span>
<span class="c1"># done outside the class. This is for exercise purpose, it is not idea</span>
<span class="c1"># Next one I will encapsulate the random number generation in initializer</span>

<span class="k">class</span> <span class="nc">TwoLayerNet</span><span class="p">(</span><span class="nb">object</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;</span>
<span class="sd">    Two layer fully connected neural network</span>
<span class="sd">    FC layer -&gt; Batchnorm -&gt; ReLU nonlinear -&gt; FC layer -&gt; Softmax</span>
<span class="sd">    &quot;&quot;&quot;</span>
    
    <span class="k">def</span> <span class="nf">__init__</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">w1</span><span class="p">,</span> <span class="n">b1</span><span class="p">,</span> <span class="n">w2</span><span class="p">,</span> <span class="n">b2</span><span class="p">,</span> <span class="n">gamma</span><span class="p">,</span> <span class="n">beta</span><span class="p">,</span>
        <span class="n">weight_scale</span><span class="o">=</span><span class="mf">1e-3</span><span class="p">,</span> <span class="n">reg</span><span class="o">=</span><span class="mf">0.0</span><span class="p">,</span> <span class="n">verbose</span><span class="o">=</span><span class="bp">False</span><span class="p">,</span> <span class="n">dtype</span><span class="o">=</span><span class="n">np</span><span class="o">.</span><span class="n">float32</span><span class="p">):</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">params</span> <span class="o">=</span> <span class="p">{}</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">bn_params</span> <span class="o">=</span> <span class="p">{}</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">verbose</span> <span class="o">=</span> <span class="n">verbose</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">params</span><span class="p">[</span><span class="s2">&quot;W1&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">w1</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">params</span><span class="p">[</span><span class="s2">&quot;b1&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">b1</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">params</span><span class="p">[</span><span class="s2">&quot;W2&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">w2</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">params</span><span class="p">[</span><span class="s2">&quot;b2&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">b2</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">params</span><span class="p">[</span><span class="s2">&quot;gamma&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">gamma</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">params</span><span class="p">[</span><span class="s2">&quot;beta&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">beta</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">ws</span> <span class="o">=</span> <span class="n">weight_scale</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">reg</span> <span class="o">=</span> <span class="n">reg</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">dtype</span> <span class="o">=</span> <span class="n">dtype</span>
        
        <span class="k">for</span> <span class="n">k</span><span class="p">,</span> <span class="n">v</span> <span class="ow">in</span> <span class="nb">sorted</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">params</span><span class="o">.</span><span class="n">iteritems</span><span class="p">()):</span>
            <span class="c1">#if verbose: print &quot;params %s, shape %s&quot; % (k, v.shape)</span>
            <span class="bp">self</span><span class="o">.</span><span class="n">params</span><span class="p">[</span><span class="n">k</span><span class="p">]</span> <span class="o">=</span> <span class="n">v</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">dtype</span><span class="p">)</span>
            
                
                
    <span class="k">def</span> <span class="nf">loss</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="o">=</span><span class="bp">None</span><span class="p">):</span>
        <span class="sd">&quot;&quot;&quot;</span>
<span class="sd">        Evaluate loss and gradient for the network</span>
<span class="sd">        </span>
<span class="sd">        Inputs:</span>
<span class="sd">        - X: Array of input data of shape (N, *input_dim)</span>
<span class="sd">        - y: Array of labels, of shape (N,), y[i] gives the label for X[i]</span>
<span class="sd">        </span>
<span class="sd">        Returns:</span>
<span class="sd">        If y is None, then run a test-time forward pass of the model and return:</span>
<span class="sd">        - scores: Array of shape (N,C) giving classification scores, where</span>
<span class="sd">          scores[i, c] is the classification score for X[i] and class c.</span>
<span class="sd">          </span>
<span class="sd">        If y is not None, then runa a training-time forward and backward pass and</span>
<span class="sd">        return a tuple of:</span>
<span class="sd">        - loss: Scalar value giving the loss</span>
<span class="sd">        - grads: Dictionary with the same keys as self.params, mapping parameter</span>
<span class="sd">          names to gradients of the loss with respect to those parameters.</span>
<span class="sd">        &quot;&quot;&quot;</span>
        <span class="c1">########################################################</span>
        <span class="c1"># Forward pass</span>
        <span class="c1">########################################################</span>
        <span class="n">X</span> <span class="o">=</span> <span class="n">X</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">dtype</span><span class="p">)</span>
        <span class="n">mode</span> <span class="o">=</span> <span class="s1">&#39;test&#39;</span> <span class="k">if</span> <span class="n">y</span> <span class="ow">is</span> <span class="bp">None</span> <span class="k">else</span> <span class="s1">&#39;train&#39;</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">bn_params</span><span class="p">[</span><span class="s1">&#39;mode&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">mode</span>
        <span class="n">caches</span> <span class="o">=</span> <span class="p">[]</span>
        <span class="c1"># FC 1</span>
        <span class="n">a1</span><span class="p">,</span> <span class="n">cache</span> <span class="o">=</span> <span class="n">affine_forward</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="bp">self</span><span class="o">.</span><span class="n">params</span><span class="p">[</span><span class="s2">&quot;W1&quot;</span><span class="p">],</span> <span class="bp">self</span><span class="o">.</span><span class="n">params</span><span class="p">[</span><span class="s2">&quot;b1&quot;</span><span class="p">])</span>
        <span class="n">caches</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">cache</span><span class="p">)</span>
        <span class="c1"># Batch Normalization</span>
        <span class="n">a_bn1</span><span class="p">,</span> <span class="n">cache</span> <span class="o">=</span> <span class="n">batchnorm_forward</span><span class="p">(</span><span class="n">a1</span><span class="p">,</span> <span class="bp">self</span><span class="o">.</span><span class="n">params</span><span class="p">[</span><span class="s2">&quot;gamma&quot;</span><span class="p">],</span> <span class="bp">self</span><span class="o">.</span><span class="n">params</span><span class="p">[</span><span class="s2">&quot;beta&quot;</span><span class="p">],</span> <span class="bp">self</span><span class="o">.</span><span class="n">bn_params</span><span class="p">)</span>
        <span class="n">caches</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">cache</span><span class="p">)</span>
        <span class="c1"># ReLU</span>
        <span class="n">a_relu1</span><span class="p">,</span> <span class="n">cache</span> <span class="o">=</span> <span class="n">relu_forward</span><span class="p">(</span><span class="n">a_bn1</span><span class="p">)</span>
        <span class="n">caches</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">cache</span><span class="p">)</span>
        <span class="c1"># FC 2</span>
        <span class="n">scores</span><span class="p">,</span> <span class="n">cache</span> <span class="o">=</span> <span class="n">affine_forward</span><span class="p">(</span><span class="n">a_relu1</span><span class="p">,</span> <span class="bp">self</span><span class="o">.</span><span class="n">params</span><span class="p">[</span><span class="s2">&quot;W2&quot;</span><span class="p">],</span> <span class="bp">self</span><span class="o">.</span><span class="n">params</span><span class="p">[</span><span class="s2">&quot;b2&quot;</span><span class="p">])</span>
        <span class="n">caches</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">cache</span><span class="p">)</span>
        
        <span class="k">if</span> <span class="n">mode</span> <span class="o">==</span> <span class="s1">&#39;test&#39;</span><span class="p">:</span>
            <span class="k">return</span> <span class="n">scores</span>
        
        <span class="c1">########################################################</span>
        <span class="c1"># Backward propagation</span>
        <span class="c1">########################################################</span>
        <span class="n">loss</span><span class="p">,</span> <span class="n">grads</span> <span class="o">=</span> <span class="mf">0.0</span><span class="p">,</span> <span class="p">{}</span>
        <span class="n">loss</span><span class="p">,</span> <span class="n">dout</span> <span class="o">=</span> <span class="n">softmax_loss</span><span class="p">(</span><span class="n">scores</span><span class="p">,</span> <span class="n">y</span><span class="p">)</span>
        <span class="c1"># add regularization</span>
        <span class="n">loss</span> <span class="o">+=</span> <span class="mf">0.5</span> <span class="o">*</span> <span class="bp">self</span><span class="o">.</span><span class="n">reg</span> <span class="o">*</span> <span class="p">(</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">params</span><span class="p">[</span><span class="s1">&#39;W1&#39;</span><span class="p">]</span><span class="o">**</span><span class="mi">2</span><span class="p">)</span> <span class="o">+</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">params</span><span class="p">[</span><span class="s1">&#39;W2&#39;</span><span class="p">]</span><span class="o">**</span><span class="mi">2</span><span class="p">)</span> <span class="p">)</span>
        
        <span class="c1"># back propagate gradient        </span>
        <span class="c1"># last affine layer</span>
        <span class="n">cache</span> <span class="o">=</span> <span class="n">caches</span><span class="o">.</span><span class="n">pop</span><span class="p">()</span>
        <span class="n">dout</span><span class="p">,</span> <span class="n">dW</span><span class="p">,</span> <span class="n">db</span> <span class="o">=</span> <span class="n">affine_backward</span><span class="p">(</span><span class="n">dout</span><span class="p">,</span> <span class="n">cache</span><span class="p">)</span>
        <span class="n">grads</span><span class="p">[</span><span class="s1">&#39;W2&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">dW</span> <span class="o">+</span> <span class="bp">self</span><span class="o">.</span><span class="n">reg</span> <span class="o">*</span> <span class="bp">self</span><span class="o">.</span><span class="n">params</span><span class="p">[</span><span class="s1">&#39;W2&#39;</span><span class="p">]</span>
        <span class="n">grads</span><span class="p">[</span><span class="s1">&#39;b2&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">db</span>
        <span class="c1"># ReLU</span>
        <span class="n">cache</span> <span class="o">=</span> <span class="n">caches</span><span class="o">.</span><span class="n">pop</span><span class="p">()</span>
        <span class="n">dout</span> <span class="o">=</span> <span class="n">relu_backward</span><span class="p">(</span><span class="n">dout</span><span class="p">,</span> <span class="n">cache</span><span class="p">)</span>
        <span class="c1"># Batch Normalization</span>
        <span class="n">cache</span> <span class="o">=</span> <span class="n">caches</span><span class="o">.</span><span class="n">pop</span><span class="p">()</span>
        <span class="n">dout</span><span class="p">,</span> <span class="n">dgamma</span><span class="p">,</span> <span class="n">dbeta</span> <span class="o">=</span> <span class="n">batchnorm_backward</span><span class="p">(</span><span class="n">dout</span><span class="p">,</span> <span class="n">cache</span><span class="p">)</span>
        <span class="n">grads</span><span class="p">[</span><span class="s1">&#39;gamma&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">dgamma</span>
        <span class="n">grads</span><span class="p">[</span><span class="s1">&#39;beta&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">dbeta</span>
        <span class="c1"># FC 1</span>
        <span class="n">cache</span> <span class="o">=</span> <span class="n">caches</span><span class="o">.</span><span class="n">pop</span><span class="p">()</span>
        <span class="n">dout</span><span class="p">,</span> <span class="n">dW</span><span class="p">,</span> <span class="n">db</span> <span class="o">=</span> <span class="n">affine_backward</span><span class="p">(</span><span class="n">dout</span><span class="p">,</span> <span class="n">cache</span><span class="p">)</span>
        <span class="n">grads</span><span class="p">[</span><span class="s1">&#39;W1&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">dW</span> <span class="o">+</span> <span class="bp">self</span><span class="o">.</span><span class="n">reg</span> <span class="o">*</span> <span class="bp">self</span><span class="o">.</span><span class="n">params</span><span class="p">[</span><span class="s1">&#39;W1&#39;</span><span class="p">]</span>
        <span class="n">grads</span><span class="p">[</span><span class="s1">&#39;b1&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">db</span>
        
        <span class="k">return</span> <span class="n">loss</span><span class="p">,</span> <span class="n">grads</span>
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
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Create a small network to validate gradient calculation</span>

<span class="n">N</span><span class="p">,</span> <span class="n">D</span><span class="p">,</span> <span class="n">H1</span><span class="p">,</span> <span class="n">H2</span><span class="p">,</span> <span class="n">C</span> <span class="o">=</span> <span class="mi">5</span><span class="p">,</span> <span class="mi">10</span><span class="p">,</span> <span class="mi">6</span><span class="p">,</span> <span class="mi">8</span><span class="p">,</span> <span class="mi">6</span>   <span class="c1"># number of test cases, features, number of hidden unit, number of classes</span>
<span class="n">y</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">randint</span><span class="p">(</span><span class="n">C</span><span class="p">,</span> <span class="n">size</span><span class="o">=</span><span class="n">N</span><span class="p">)</span>
<span class="n">x</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">randn</span><span class="p">(</span><span class="n">N</span><span class="p">,</span> <span class="n">D</span><span class="p">)</span>
<span class="n">w1</span> <span class="o">=</span> <span class="mf">0.001</span> <span class="o">*</span> <span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">randn</span><span class="p">(</span><span class="n">D</span><span class="p">,</span> <span class="n">H1</span><span class="p">)</span>
<span class="n">b1</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">randn</span><span class="p">(</span><span class="n">H1</span><span class="p">)</span>
<span class="n">w2</span> <span class="o">=</span> <span class="mf">0.001</span> <span class="o">*</span> <span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">randn</span><span class="p">(</span><span class="n">H1</span><span class="p">,</span> <span class="n">H2</span><span class="p">)</span>
<span class="n">b2</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">randn</span><span class="p">(</span><span class="n">H2</span><span class="p">)</span>
<span class="n">gamma</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">ones</span><span class="p">(</span><span class="n">H1</span><span class="p">)</span>
<span class="n">beta</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">zeros</span><span class="p">(</span><span class="n">H1</span><span class="p">)</span>

<span class="c1"># with regularzation turned off</span>
<span class="n">model</span> <span class="o">=</span> <span class="n">TwoLayerNet</span><span class="p">(</span><span class="n">w1</span><span class="p">,</span> <span class="n">b1</span><span class="p">,</span> <span class="n">w2</span><span class="p">,</span> <span class="n">b2</span><span class="p">,</span> <span class="n">gamma</span><span class="p">,</span> <span class="n">beta</span><span class="p">,</span>
        <span class="n">weight_scale</span><span class="o">=</span><span class="mf">0.03</span><span class="p">,</span> <span class="n">reg</span><span class="o">=</span><span class="mf">0.00</span><span class="p">,</span> <span class="n">verbose</span><span class="o">=</span><span class="bp">True</span><span class="p">,</span> <span class="n">dtype</span><span class="o">=</span><span class="n">np</span><span class="o">.</span><span class="n">float64</span><span class="p">)</span>

<span class="n">loss</span><span class="p">,</span> <span class="n">grads</span> <span class="o">=</span> <span class="n">model</span><span class="o">.</span><span class="n">loss</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">y</span><span class="p">)</span>
<span class="k">def</span> <span class="nf">rel_error</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">y</span><span class="p">):</span>
  <span class="sd">&quot;&quot;&quot; returns relative error &quot;&quot;&quot;</span>
  <span class="k">return</span> <span class="n">np</span><span class="o">.</span><span class="n">max</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">abs</span><span class="p">(</span><span class="n">x</span> <span class="o">-</span> <span class="n">y</span><span class="p">)</span> <span class="o">/</span> <span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">maximum</span><span class="p">(</span><span class="mf">1e-8</span><span class="p">,</span> <span class="n">np</span><span class="o">.</span><span class="n">abs</span><span class="p">(</span><span class="n">x</span><span class="p">)</span> <span class="o">+</span> <span class="n">np</span><span class="o">.</span><span class="n">abs</span><span class="p">(</span><span class="n">y</span><span class="p">))))</span>

<span class="k">for</span> <span class="n">name</span> <span class="ow">in</span> <span class="nb">sorted</span><span class="p">(</span><span class="n">grads</span><span class="p">):</span>
   <span class="n">f</span> <span class="o">=</span> <span class="k">lambda</span> <span class="n">_</span><span class="p">:</span> <span class="n">model</span><span class="o">.</span><span class="n">loss</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">y</span><span class="p">)[</span><span class="mi">0</span><span class="p">]</span>
   <span class="n">grad_num</span> <span class="o">=</span> <span class="n">eval_numerical_gradient</span><span class="p">(</span><span class="n">f</span><span class="p">,</span> <span class="n">model</span><span class="o">.</span><span class="n">params</span><span class="p">[</span><span class="n">name</span><span class="p">],</span> <span class="n">verbose</span><span class="o">=</span><span class="bp">False</span><span class="p">)</span>
   <span class="k">print</span> <span class="s1">&#39;</span><span class="si">%s</span><span class="s1"> relative error: </span><span class="si">%.2e</span><span class="s1">&#39;</span> <span class="o">%</span> <span class="p">(</span><span class="n">name</span><span class="p">,</span> <span class="n">rel_error</span><span class="p">(</span><span class="n">grad_num</span><span class="p">,</span> <span class="n">grads</span><span class="p">[</span><span class="n">name</span><span class="p">]))</span>

<span class="c1"># With regularization turned on</span>
<span class="k">print</span> <span class="s2">&quot;</span><span class="se">\n</span><span class="s2">With regularization turned on:&quot;</span>
<span class="n">model2</span> <span class="o">=</span> <span class="n">TwoLayerNet</span><span class="p">(</span><span class="n">w1</span><span class="p">,</span> <span class="n">b1</span><span class="p">,</span> <span class="n">w2</span><span class="p">,</span> <span class="n">b2</span><span class="p">,</span> <span class="n">gamma</span><span class="p">,</span> <span class="n">beta</span><span class="p">,</span>
        <span class="n">weight_scale</span><span class="o">=</span><span class="mf">0.03</span><span class="p">,</span> <span class="n">reg</span><span class="o">=</span><span class="mf">0.6</span><span class="p">,</span> <span class="n">verbose</span><span class="o">=</span><span class="bp">True</span><span class="p">,</span> <span class="n">dtype</span><span class="o">=</span><span class="n">np</span><span class="o">.</span><span class="n">float64</span><span class="p">)</span>

<span class="n">loss</span><span class="p">,</span> <span class="n">grads</span> <span class="o">=</span> <span class="n">model2</span><span class="o">.</span><span class="n">loss</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">y</span><span class="p">)</span>

<span class="k">for</span> <span class="n">name</span> <span class="ow">in</span> <span class="nb">sorted</span><span class="p">(</span><span class="n">grads</span><span class="p">):</span>
   <span class="n">f</span> <span class="o">=</span> <span class="k">lambda</span> <span class="n">_</span><span class="p">:</span> <span class="n">model2</span><span class="o">.</span><span class="n">loss</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">y</span><span class="p">)[</span><span class="mi">0</span><span class="p">]</span>
   <span class="n">grad_num</span> <span class="o">=</span> <span class="n">eval_numerical_gradient</span><span class="p">(</span><span class="n">f</span><span class="p">,</span> <span class="n">model2</span><span class="o">.</span><span class="n">params</span><span class="p">[</span><span class="n">name</span><span class="p">],</span> <span class="n">verbose</span><span class="o">=</span><span class="bp">False</span><span class="p">)</span>
   <span class="k">print</span> <span class="s1">&#39;</span><span class="si">%s</span><span class="s1"> relative error: </span><span class="si">%.2e</span><span class="s1">&#39;</span> <span class="o">%</span> <span class="p">(</span><span class="n">name</span><span class="p">,</span> <span class="n">rel_error</span><span class="p">(</span><span class="n">grad_num</span><span class="p">,</span> <span class="n">grads</span><span class="p">[</span><span class="n">name</span><span class="p">]))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>W1 relative error: 4.70e-06
W2 relative error: 1.60e-09
b1 relative error: 2.08e-09
b2 relative error: 2.49e-10
beta relative error: 2.64e-07
gamma relative error: 8.44e-08

With regularization turned on:
W1 relative error: 6.42e-06
W2 relative error: 1.34e-09
b1 relative error: 2.08e-09
b2 relative error: 2.49e-10
beta relative error: 2.64e-07
gamma relative error: 8.44e-08
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
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Declare network for Cifar10</span>
<span class="n">D</span><span class="p">,</span> <span class="n">H1</span><span class="p">,</span> <span class="n">H2</span><span class="p">,</span> <span class="n">C</span> <span class="o">=</span> <span class="mi">3072</span><span class="p">,</span> <span class="mi">100</span><span class="p">,</span> <span class="mi">100</span><span class="p">,</span> <span class="mi">10</span>   <span class="c1"># number of test cases, features, number of hidden unit, number of classes</span>

<span class="n">w1</span> <span class="o">=</span> <span class="mf">0.001</span> <span class="o">*</span> <span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">randn</span><span class="p">(</span><span class="n">D</span><span class="p">,</span> <span class="n">H1</span><span class="p">)</span>
<span class="n">b1</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">randn</span><span class="p">(</span><span class="n">H1</span><span class="p">)</span>
<span class="n">w2</span> <span class="o">=</span> <span class="mf">0.001</span> <span class="o">*</span> <span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">randn</span><span class="p">(</span><span class="n">H1</span><span class="p">,</span> <span class="n">H2</span><span class="p">)</span>
<span class="n">b2</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">randn</span><span class="p">(</span><span class="n">H2</span><span class="p">)</span>
<span class="n">gamma</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">ones</span><span class="p">(</span><span class="n">H1</span><span class="p">)</span>
<span class="n">beta</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">zeros</span><span class="p">(</span><span class="n">H1</span><span class="p">)</span>

<span class="n">model</span> <span class="o">=</span> <span class="n">TwoLayerNet</span><span class="p">(</span><span class="n">w1</span><span class="p">,</span> <span class="n">b1</span><span class="p">,</span> <span class="n">w2</span><span class="p">,</span> <span class="n">b2</span><span class="p">,</span> <span class="n">gamma</span><span class="p">,</span> <span class="n">beta</span><span class="p">,</span>
        <span class="n">weight_scale</span><span class="o">=</span><span class="mf">0.03</span><span class="p">,</span> <span class="n">reg</span><span class="o">=</span><span class="mf">0.0001</span><span class="p">,</span> <span class="n">verbose</span><span class="o">=</span><span class="bp">True</span><span class="p">,</span> <span class="n">dtype</span><span class="o">=</span><span class="n">np</span><span class="o">.</span><span class="n">float64</span><span class="p">)</span>
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
<div class=" highlight hl-ipython2"><pre><span></span><span class="n">solver</span> <span class="o">=</span> <span class="n">Solver</span><span class="p">(</span><span class="n">model</span><span class="p">,</span> <span class="n">data</span><span class="p">,</span>
                 <span class="n">update_rule</span><span class="o">=</span><span class="s1">&#39;adam&#39;</span><span class="p">,</span>
                 <span class="n">optim_config</span><span class="o">=</span><span class="p">{</span>
                   <span class="s1">&#39;learning_rate&#39;</span><span class="p">:</span> <span class="mf">1e-3</span><span class="p">,</span>
                  <span class="p">},</span>
                  <span class="n">lr_decay</span><span class="o">=</span><span class="mf">0.95</span><span class="p">,</span>
                  <span class="n">num_epochs</span><span class="o">=</span><span class="mi">10</span><span class="p">,</span> <span class="n">batch_size</span><span class="o">=</span><span class="mi">100</span><span class="p">,</span>
                <span class="n">print_every</span><span class="o">=</span><span class="mi">100</span><span class="p">)</span>
<span class="n">solver</span><span class="o">.</span><span class="n">train</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>(Iteration 1 / 4900) loss: 4.807757
(Epoch 0 / 10) train acc: 0.161000; val_acc: 0.173000
(Iteration 101 / 4900) loss: 1.969828
(Iteration 201 / 4900) loss: 1.788941
(Iteration 301 / 4900) loss: 1.787009
(Iteration 401 / 4900) loss: 1.657621
(Epoch 1 / 10) train acc: 0.449000; val_acc: 0.428000
(Iteration 501 / 4900) loss: 1.620931
(Iteration 601 / 4900) loss: 1.608835
(Iteration 701 / 4900) loss: 1.579913
(Iteration 801 / 4900) loss: 1.603053
(Iteration 901 / 4900) loss: 1.413051
(Epoch 2 / 10) train acc: 0.496000; val_acc: 0.442000
(Iteration 1001 / 4900) loss: 1.553973
(Iteration 1101 / 4900) loss: 1.341107
(Iteration 1201 / 4900) loss: 1.440078
(Iteration 1301 / 4900) loss: 1.478979
(Iteration 1401 / 4900) loss: 1.365082
(Epoch 3 / 10) train acc: 0.535000; val_acc: 0.488000
(Iteration 1501 / 4900) loss: 1.369063
(Iteration 1601 / 4900) loss: 1.370673
(Iteration 1701 / 4900) loss: 1.227712
(Iteration 1801 / 4900) loss: 1.586937
(Iteration 1901 / 4900) loss: 1.439272
(Epoch 4 / 10) train acc: 0.540000; val_acc: 0.502000
(Iteration 2001 / 4900) loss: 1.194432
(Iteration 2101 / 4900) loss: 1.470331
(Iteration 2201 / 4900) loss: 1.350353
(Iteration 2301 / 4900) loss: 1.139255
(Iteration 2401 / 4900) loss: 1.380816
(Epoch 5 / 10) train acc: 0.553000; val_acc: 0.521000
(Iteration 2501 / 4900) loss: 1.370767
(Iteration 2601 / 4900) loss: 1.171781
(Iteration 2701 / 4900) loss: 1.420740
(Iteration 2801 / 4900) loss: 1.178949
(Iteration 2901 / 4900) loss: 1.307808
(Epoch 6 / 10) train acc: 0.578000; val_acc: 0.495000
(Iteration 3001 / 4900) loss: 1.404282
(Iteration 3101 / 4900) loss: 1.234116
(Iteration 3201 / 4900) loss: 1.370880
(Iteration 3301 / 4900) loss: 1.219765
(Iteration 3401 / 4900) loss: 1.310481
(Epoch 7 / 10) train acc: 0.586000; val_acc: 0.526000
(Iteration 3501 / 4900) loss: 1.328657
(Iteration 3601 / 4900) loss: 1.248913
(Iteration 3701 / 4900) loss: 1.195643
(Iteration 3801 / 4900) loss: 1.164770
(Iteration 3901 / 4900) loss: 1.262836
(Epoch 8 / 10) train acc: 0.653000; val_acc: 0.530000
(Iteration 4001 / 4900) loss: 1.255078
(Iteration 4101 / 4900) loss: 1.133213
(Iteration 4201 / 4900) loss: 1.144853
(Iteration 4301 / 4900) loss: 1.113077
(Iteration 4401 / 4900) loss: 1.111701
(Epoch 9 / 10) train acc: 0.600000; val_acc: 0.510000
(Iteration 4501 / 4900) loss: 1.202155
(Iteration 4601 / 4900) loss: 1.197927
(Iteration 4701 / 4900) loss: 1.295892
(Iteration 4801 / 4900) loss: 1.375950
(Epoch 10 / 10) train acc: 0.602000; val_acc: 0.525000
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
<div class=" highlight hl-ipython2"><pre><span></span><span class="n">plt</span><span class="o">.</span><span class="n">subplot</span><span class="p">(</span><span class="mi">2</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">1</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">solver</span><span class="o">.</span><span class="n">loss_history</span><span class="p">,</span> <span class="s1">&#39;o&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;iteration&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;loss&#39;</span><span class="p">)</span>

<span class="n">plt</span><span class="o">.</span><span class="n">subplot</span><span class="p">(</span><span class="mi">2</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">2</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">solver</span><span class="o">.</span><span class="n">train_acc_history</span><span class="p">,</span> <span class="s1">&#39;-o&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">solver</span><span class="o">.</span><span class="n">val_acc_history</span><span class="p">,</span> <span class="s1">&#39;-o&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">legend</span><span class="p">([</span><span class="s1">&#39;train&#39;</span><span class="p">,</span> <span class="s1">&#39;val&#39;</span><span class="p">],</span> <span class="n">loc</span><span class="o">=</span><span class="s1">&#39;upper left&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;epoch&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;accuracy&#39;</span><span class="p">)</span>
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
<div class="prompt input_prompt">In&nbsp;[9]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span></span><span class="n">y_test_pred</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">argmax</span><span class="p">(</span><span class="n">model</span><span class="o">.</span><span class="n">loss</span><span class="p">(</span><span class="n">data</span><span class="p">[</span><span class="s1">&#39;X_test&#39;</span><span class="p">]),</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>
<span class="n">y_val_pred</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">argmax</span><span class="p">(</span><span class="n">model</span><span class="o">.</span><span class="n">loss</span><span class="p">(</span><span class="n">data</span><span class="p">[</span><span class="s1">&#39;X_val&#39;</span><span class="p">]),</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>
<span class="k">print</span> <span class="s1">&#39;Validation set accuracy: &#39;</span><span class="p">,</span> <span class="p">(</span><span class="n">y_val_pred</span> <span class="o">==</span> <span class="n">data</span><span class="p">[</span><span class="s1">&#39;y_val&#39;</span><span class="p">])</span><span class="o">.</span><span class="n">mean</span><span class="p">()</span>
<span class="k">print</span> <span class="s1">&#39;Test set accuracy: &#39;</span><span class="p">,</span> <span class="p">(</span><span class="n">y_test_pred</span> <span class="o">==</span> <span class="n">data</span><span class="p">[</span><span class="s1">&#39;y_test&#39;</span><span class="p">])</span><span class="o">.</span><span class="n">mean</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>Validation set accuracy:  0.529
Test set accuracy:  0.533
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
