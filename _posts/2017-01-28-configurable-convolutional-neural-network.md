---
layout: post
title: "Configurable Convolutional Neural Network"
description: ""
category: 
tags: 
 - Convolutional Neural Network
 - Deep Learning
 - Computer Vision
---
{% include JB/setup %}
<html>
<head><meta charset="utf-8" />
<title>ConfigurableConvolutionalNetwork</title>

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
<h1 id="Convolutional-Network-Framework-in-Python">Convolutional Network Framework in Python<a class="anchor-link" href="#Convolutional-Network-Framework-in-Python">&#182;</a></h1><p>To test configurable CNN network on CIFAR10
Based on 2016 cs231n project</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[1]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Setup environment</span>
<span class="kn">import</span> <span class="nn">numpy</span> <span class="kn">as</span> <span class="nn">np</span>
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="kn">as</span> <span class="nn">plt</span>
<span class="kn">from</span> <span class="nn">cs231n.classifiers.convnetGenerator</span> <span class="kn">import</span> <span class="o">*</span>
<span class="kn">from</span> <span class="nn">cs231n.data_utils</span> <span class="kn">import</span> <span class="n">get_CIFAR10_data</span>
<span class="kn">from</span> <span class="nn">cs231n.gradient_check</span> <span class="kn">import</span> <span class="n">eval_numerical_gradient_array</span><span class="p">,</span> <span class="n">eval_numerical_gradient</span>
<span class="kn">from</span> <span class="nn">cs231n.layers</span> <span class="kn">import</span> <span class="o">*</span>
<span class="kn">from</span> <span class="nn">cs231n.fast_layers</span> <span class="kn">import</span> <span class="o">*</span>
<span class="kn">from</span> <span class="nn">cs231n.solver</span> <span class="kn">import</span> <span class="n">Solver</span>

<span class="o">%</span><span class="k">matplotlib</span> inline
<span class="n">plt</span><span class="o">.</span><span class="n">rcParams</span><span class="p">[</span><span class="s1">&#39;figure.figsize&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="mf">10.0</span><span class="p">,</span> <span class="mf">8.0</span><span class="p">)</span> <span class="c1"># set default size of plots</span>
<span class="n">plt</span><span class="o">.</span><span class="n">rcParams</span><span class="p">[</span><span class="s1">&#39;image.interpolation&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="s1">&#39;nearest&#39;</span>
<span class="n">plt</span><span class="o">.</span><span class="n">rcParams</span><span class="p">[</span><span class="s1">&#39;image.cmap&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="s1">&#39;gray&#39;</span>

<span class="o">%</span><span class="k">load_ext</span> autoreload
<span class="o">%</span><span class="k">autoreload</span> 2

<span class="k">def</span> <span class="nf">rel_error</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">y</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot; returns relative error &quot;&quot;&quot;</span>
    <span class="k">return</span> <span class="n">np</span><span class="o">.</span><span class="n">max</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">abs</span><span class="p">(</span><span class="n">x</span> <span class="o">-</span> <span class="n">y</span><span class="p">)</span><span class="o">/</span> <span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">maximum</span><span class="p">(</span><span class="mf">1e-8</span><span class="p">,</span> <span class="n">np</span><span class="o">.</span><span class="n">abs</span><span class="p">(</span><span class="n">x</span><span class="p">)</span> <span class="o">+</span> <span class="n">np</span><span class="o">.</span><span class="n">abs</span><span class="p">(</span><span class="n">y</span><span class="p">))))</span>
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
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Load preprocessed CIFAR10 image</span>
<span class="n">data</span> <span class="o">=</span> <span class="n">get_CIFAR10_data</span><span class="p">()</span>
<span class="k">for</span> <span class="n">k</span><span class="p">,</span> <span class="n">v</span> <span class="ow">in</span> <span class="n">data</span><span class="o">.</span><span class="n">iteritems</span><span class="p">():</span>
    <span class="k">print</span> <span class="s1">&#39;</span><span class="si">%s</span><span class="s1">: &#39;</span> <span class="o">%</span><span class="k">k</span>, v.shape
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>X_val:  (1000, 3, 32, 32)
X_train:  (49000, 3, 32, 32)
X_test:  (1000, 3, 32, 32)
y_val:  (1000,)
y_train:  (49000,)
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
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Load convnetGenerator</span>
<span class="kn">from</span> <span class="nn">cs231n.classifiers.convnet</span> <span class="kn">import</span> <span class="o">*</span>
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
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Sanity check on loss value</span>
<span class="n">layers</span> <span class="o">=</span> <span class="p">[</span>
    <span class="p">[</span><span class="s1">&#39;conv&#39;</span><span class="p">,</span> <span class="p">{</span><span class="s1">&#39;num_of_filters&#39;</span><span class="p">:</span><span class="mi">5</span><span class="p">,</span> <span class="s1">&#39;filter_size&#39;</span><span class="p">:</span><span class="mi">3</span><span class="p">}],</span>
    <span class="p">[</span><span class="s1">&#39;spatial_batchnorm&#39;</span><span class="p">],</span>
    <span class="p">[</span><span class="s1">&#39;relu&#39;</span><span class="p">],</span>
    <span class="p">[</span><span class="s1">&#39;dropout&#39;</span><span class="p">],</span>
    <span class="p">[</span><span class="s1">&#39;pool&#39;</span><span class="p">],</span>
    <span class="p">[</span><span class="s1">&#39;affine&#39;</span><span class="p">,</span> <span class="p">(</span><span class="mi">20</span><span class="p">)],</span>
    <span class="p">[</span><span class="s1">&#39;batchnorm&#39;</span><span class="p">],</span>
    <span class="p">[</span><span class="s1">&#39;affine&#39;</span><span class="p">,</span> <span class="p">(</span><span class="mi">10</span><span class="p">)],</span>
    <span class="p">[</span><span class="s1">&#39;relu&#39;</span><span class="p">],</span>
    <span class="p">[</span><span class="s1">&#39;dropout&#39;</span><span class="p">]</span>
<span class="p">]</span>

<span class="n">N</span> <span class="o">=</span> <span class="mi">10</span>
<span class="n">X</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">randn</span><span class="p">(</span><span class="n">N</span><span class="p">,</span> <span class="mi">3</span><span class="p">,</span> <span class="mi">4</span><span class="p">,</span> <span class="mi">4</span><span class="p">)</span>
<span class="n">y</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">randint</span><span class="p">(</span><span class="mi">10</span><span class="p">,</span> <span class="n">size</span><span class="o">=</span><span class="n">N</span><span class="p">)</span>

<span class="n">model</span> <span class="o">=</span> <span class="n">convnetGenerator</span><span class="p">(</span><span class="n">input_dim</span><span class="o">=</span><span class="p">(</span><span class="mi">3</span><span class="p">,</span> <span class="mi">4</span><span class="p">,</span> <span class="mi">4</span><span class="p">),</span> 
                         <span class="n">layers</span><span class="o">=</span><span class="n">layers</span><span class="p">,</span> <span class="n">verbose</span><span class="o">=</span><span class="bp">False</span><span class="p">,</span> 
                         <span class="n">weight_scale</span><span class="o">=</span><span class="mf">1e-1</span><span class="p">,</span> <span class="n">seed</span><span class="o">=</span><span class="mi">0</span><span class="p">,</span> 
                         <span class="n">dtype</span><span class="o">=</span><span class="n">np</span><span class="o">.</span><span class="n">float64</span><span class="p">)</span>
<span class="n">loss</span><span class="p">,</span> <span class="n">grads</span> <span class="o">=</span> <span class="n">model</span><span class="o">.</span><span class="n">loss</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">)</span>
<span class="k">print</span> <span class="s1">&#39;Initial loss (without regularization): &#39;</span><span class="p">,</span> <span class="n">loss</span>

<span class="k">for</span> <span class="n">param_name</span> <span class="ow">in</span> <span class="nb">sorted</span><span class="p">(</span><span class="n">grads</span><span class="p">):</span>
    <span class="n">f</span> <span class="o">=</span> <span class="k">lambda</span> <span class="n">_</span><span class="p">:</span> <span class="n">model</span><span class="o">.</span><span class="n">loss</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">)[</span><span class="mi">0</span><span class="p">]</span>
    <span class="n">param_grad_num</span> <span class="o">=</span> <span class="n">eval_numerical_gradient</span><span class="p">(</span><span class="n">f</span><span class="p">,</span> <span class="n">model</span><span class="o">.</span><span class="n">params</span><span class="p">[</span><span class="n">param_name</span><span class="p">],</span> <span class="n">verbose</span><span class="o">=</span><span class="bp">False</span><span class="p">,</span> <span class="n">h</span><span class="o">=</span><span class="mf">1e-6</span><span class="p">)</span>
    <span class="n">e</span> <span class="o">=</span> <span class="n">rel_error</span><span class="p">(</span><span class="n">param_grad_num</span><span class="p">,</span> <span class="n">grads</span><span class="p">[</span><span class="n">param_name</span><span class="p">])</span>
    <span class="k">print</span> <span class="s1">&#39;</span><span class="si">%s</span><span class="s1"> max relative error: </span><span class="si">%e</span><span class="s1">&#39;</span> <span class="o">%</span> <span class="p">(</span><span class="n">param_name</span><span class="p">,</span> <span class="n">e</span><span class="p">)</span>
    
<span class="n">model</span><span class="o">.</span><span class="n">reg</span> <span class="o">=</span> <span class="mi">1</span>
<span class="n">loss</span><span class="p">,</span> <span class="n">grads</span> <span class="o">=</span> <span class="n">model</span><span class="o">.</span><span class="n">loss</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">)</span>
<span class="k">print</span> <span class="s1">&#39;Initial loss (with regularization): &#39;</span><span class="p">,</span> <span class="n">loss</span>

<span class="k">for</span> <span class="n">param_name</span> <span class="ow">in</span> <span class="nb">sorted</span><span class="p">(</span><span class="n">grads</span><span class="p">):</span>
    <span class="n">f</span> <span class="o">=</span> <span class="k">lambda</span> <span class="n">_</span><span class="p">:</span> <span class="n">model</span><span class="o">.</span><span class="n">loss</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">)[</span><span class="mi">0</span><span class="p">]</span>
    <span class="n">param_grad_num</span> <span class="o">=</span> <span class="n">eval_numerical_gradient</span><span class="p">(</span><span class="n">f</span><span class="p">,</span> <span class="n">model</span><span class="o">.</span><span class="n">params</span><span class="p">[</span><span class="n">param_name</span><span class="p">],</span> <span class="n">verbose</span><span class="o">=</span><span class="bp">False</span><span class="p">,</span> <span class="n">h</span><span class="o">=</span><span class="mf">1e-6</span><span class="p">)</span>
    <span class="n">e</span> <span class="o">=</span> <span class="n">rel_error</span><span class="p">(</span><span class="n">param_grad_num</span><span class="p">,</span> <span class="n">grads</span><span class="p">[</span><span class="n">param_name</span><span class="p">])</span>
    <span class="k">print</span> <span class="s1">&#39;</span><span class="si">%s</span><span class="s1"> max relative error: </span><span class="si">%e</span><span class="s1">&#39;</span> <span class="o">%</span> <span class="p">(</span><span class="n">param_name</span><span class="p">,</span> <span class="n">e</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>Initial loss (without regularization):  2.48318674289
W0 max relative error: 9.883919e-08
W10 max relative error: 1.759215e-08
W5 max relative error: 6.472835e-07
W7 max relative error: 2.026246e-07
b0 max relative error: 1.019150e-09
b10 max relative error: 3.745815e-08
b5 max relative error: 7.806256e-10
b7 max relative error: 1.484453e-08
beta1 max relative error: 7.822434e-09
beta6 max relative error: 1.102359e-07
gamma1 max relative error: 1.011301e-08
gamma6 max relative error: 6.094902e-08
Initial loss (with regularization):  6.86712538153
W0 max relative error: 2.300431e-07
W10 max relative error: 1.047184e-06
W5 max relative error: 2.451635e-05
W7 max relative error: 1.070334e-07
b0 max relative error: 1.019150e-09
b10 max relative error: 6.404624e-08
b5 max relative error: 7.806256e-10
b7 max relative error: 7.096623e-09
beta1 max relative error: 2.393115e-08
beta6 max relative error: 1.102359e-07
gamma1 max relative error: 2.030903e-08
gamma6 max relative error: 6.094902e-08
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
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Test three layer model clone</span>
<span class="c1"># Overfit small data</span>
<span class="n">num_train</span> <span class="o">=</span> <span class="mi">100</span>
<span class="n">small_data</span> <span class="o">=</span> <span class="p">{</span>
    <span class="s1">&#39;X_train&#39;</span><span class="p">:</span> <span class="n">data</span><span class="p">[</span><span class="s1">&#39;X_train&#39;</span><span class="p">][:</span><span class="n">num_train</span><span class="p">],</span>
    <span class="s1">&#39;y_train&#39;</span><span class="p">:</span> <span class="n">data</span><span class="p">[</span><span class="s1">&#39;y_train&#39;</span><span class="p">][:</span><span class="n">num_train</span><span class="p">],</span>
    <span class="s1">&#39;X_val&#39;</span><span class="p">:</span> <span class="n">data</span><span class="p">[</span><span class="s1">&#39;X_val&#39;</span><span class="p">],</span>
    <span class="s1">&#39;y_val&#39;</span><span class="p">:</span> <span class="n">data</span><span class="p">[</span><span class="s1">&#39;y_val&#39;</span><span class="p">],</span>
<span class="p">}</span>

<span class="n">layers</span> <span class="o">=</span> <span class="p">[</span>
    <span class="p">[</span><span class="s1">&#39;conv&#39;</span><span class="p">,</span> <span class="p">{</span><span class="s1">&#39;num_of_filters&#39;</span><span class="p">:</span><span class="mi">32</span><span class="p">,</span> <span class="s1">&#39;filter_size&#39;</span><span class="p">:</span><span class="mi">7</span><span class="p">}],</span>
    <span class="p">[</span><span class="s1">&#39;relu&#39;</span><span class="p">],</span>
    <span class="p">[</span><span class="s1">&#39;pool&#39;</span><span class="p">],</span>
    <span class="p">[</span><span class="s1">&#39;affine&#39;</span><span class="p">,</span> <span class="p">(</span><span class="mi">100</span><span class="p">)],</span>
    <span class="p">[</span><span class="s1">&#39;relu&#39;</span><span class="p">]</span>
<span class="p">]</span>
<span class="n">model</span> <span class="o">=</span> <span class="n">convnetGenerator</span><span class="p">(</span><span class="n">layers</span><span class="o">=</span><span class="n">layers</span><span class="p">,</span> 
                         <span class="n">verbose</span><span class="o">=</span><span class="bp">False</span><span class="p">,</span> 
                         <span class="n">weight_scale</span><span class="o">=</span><span class="mf">1e-2</span><span class="p">)</span>

<span class="n">solver</span> <span class="o">=</span> <span class="n">Solver</span><span class="p">(</span><span class="n">model</span><span class="p">,</span> <span class="n">small_data</span><span class="p">,</span>
               <span class="n">num_epochs</span><span class="o">=</span><span class="mi">10</span><span class="p">,</span> <span class="n">batch_size</span><span class="o">=</span><span class="mi">50</span><span class="p">,</span>
               <span class="n">update_rule</span><span class="o">=</span><span class="s1">&#39;adam&#39;</span><span class="p">,</span>
               <span class="n">optim_config</span><span class="o">=</span><span class="p">{</span>
                    <span class="s1">&#39;learning_rate&#39;</span><span class="p">:</span> <span class="mf">1e-3</span>
               <span class="p">},</span>
                <span class="n">verbose</span><span class="o">=</span><span class="bp">True</span><span class="p">,</span> <span class="n">print_every</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>
<span class="n">solver</span><span class="o">.</span><span class="n">train</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>(Iteration 1 / 20) loss: 2.501378
(Epoch 0 / 10) train acc: 0.140000; val_acc: 0.079000
(Iteration 2 / 20) loss: 4.735779
(Epoch 1 / 10) train acc: 0.110000; val_acc: 0.107000
(Iteration 3 / 20) loss: 2.662372
(Iteration 4 / 20) loss: 2.312295
(Epoch 2 / 10) train acc: 0.280000; val_acc: 0.142000
(Iteration 5 / 20) loss: 2.336332
(Iteration 6 / 20) loss: 2.030852
(Epoch 3 / 10) train acc: 0.350000; val_acc: 0.137000
(Iteration 7 / 20) loss: 1.874209
(Iteration 8 / 20) loss: 1.803743
(Epoch 4 / 10) train acc: 0.440000; val_acc: 0.168000
(Iteration 9 / 20) loss: 1.730151
(Iteration 10 / 20) loss: 1.712336
(Epoch 5 / 10) train acc: 0.590000; val_acc: 0.169000
(Iteration 11 / 20) loss: 1.350723
(Iteration 12 / 20) loss: 1.347327
(Epoch 6 / 10) train acc: 0.610000; val_acc: 0.220000
(Iteration 13 / 20) loss: 1.458294
(Iteration 14 / 20) loss: 1.056061
(Epoch 7 / 10) train acc: 0.770000; val_acc: 0.224000
(Iteration 15 / 20) loss: 0.802197
(Iteration 16 / 20) loss: 0.818013
(Epoch 8 / 10) train acc: 0.740000; val_acc: 0.202000
(Iteration 17 / 20) loss: 0.925857
(Iteration 18 / 20) loss: 0.721106
(Epoch 9 / 10) train acc: 0.830000; val_acc: 0.191000
(Iteration 19 / 20) loss: 0.668794
(Iteration 20 / 20) loss: 0.691209
(Epoch 10 / 10) train acc: 0.850000; val_acc: 0.213000
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
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Plot traint loss, accuracy, validation accuracy</span>
<span class="n">plt</span><span class="o">.</span><span class="n">subplot</span><span class="p">(</span><span class="mi">2</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">1</span><span class="p">)</span>
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
rkJggg==
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
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Test tree-layer model on full test set</span>
<span class="n">layers</span> <span class="o">=</span> <span class="p">[</span>
    <span class="p">[</span><span class="s1">&#39;conv&#39;</span><span class="p">,</span> <span class="p">{</span><span class="s1">&#39;num_of_filters&#39;</span><span class="p">:</span><span class="mi">32</span><span class="p">,</span> <span class="s1">&#39;filter_size&#39;</span><span class="p">:</span><span class="mi">7</span><span class="p">}],</span>
    <span class="p">[</span><span class="s1">&#39;relu&#39;</span><span class="p">],</span>
    <span class="p">[</span><span class="s1">&#39;pool&#39;</span><span class="p">],</span>
    <span class="p">[</span><span class="s1">&#39;affine&#39;</span><span class="p">,</span> <span class="p">(</span><span class="mi">500</span><span class="p">)],</span>
    <span class="p">[</span><span class="s1">&#39;relu&#39;</span><span class="p">]</span>
<span class="p">]</span>
<span class="n">model</span> <span class="o">=</span> <span class="n">convnetGenerator</span><span class="p">(</span><span class="n">layers</span><span class="o">=</span><span class="n">layers</span><span class="p">,</span> 
                         <span class="n">verbose</span><span class="o">=</span><span class="bp">False</span><span class="p">,</span> 
                         <span class="n">weight_scale</span><span class="o">=</span><span class="mf">1e-3</span><span class="p">,</span>
                         <span class="n">reg</span><span class="o">=</span><span class="mf">0.001</span><span class="p">)</span>

<span class="n">solver</span> <span class="o">=</span> <span class="n">Solver</span><span class="p">(</span><span class="n">model</span><span class="p">,</span> <span class="n">data</span><span class="p">,</span>
               <span class="n">num_epochs</span><span class="o">=</span><span class="mi">1</span><span class="p">,</span> <span class="n">batch_size</span><span class="o">=</span><span class="mi">50</span><span class="p">,</span>
               <span class="n">update_rule</span><span class="o">=</span><span class="s1">&#39;adam&#39;</span><span class="p">,</span>
               <span class="n">optim_config</span><span class="o">=</span><span class="p">{</span>
                    <span class="s1">&#39;learning_rate&#39;</span><span class="p">:</span> <span class="mf">1e-3</span>
               <span class="p">},</span>
                <span class="n">verbose</span><span class="o">=</span><span class="bp">True</span><span class="p">,</span> <span class="n">print_every</span><span class="o">=</span><span class="mi">20</span><span class="p">)</span>
<span class="n">solver</span><span class="o">.</span><span class="n">train</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>(Iteration 1 / 980) loss: 2.304609
(Epoch 0 / 1) train acc: 0.118000; val_acc: 0.104000
(Iteration 21 / 980) loss: 2.166419
(Iteration 41 / 980) loss: 1.845205
(Iteration 61 / 980) loss: 1.651621
(Iteration 81 / 980) loss: 1.911876
(Iteration 101 / 980) loss: 1.907545
(Iteration 121 / 980) loss: 1.949062
(Iteration 141 / 980) loss: 1.965104
(Iteration 161 / 980) loss: 1.789602
(Iteration 181 / 980) loss: 1.732072
(Iteration 201 / 980) loss: 1.711157
(Iteration 221 / 980) loss: 1.714963
(Iteration 241 / 980) loss: 1.610209
(Iteration 261 / 980) loss: 1.673627
(Iteration 281 / 980) loss: 2.374440
(Iteration 301 / 980) loss: 1.450597
(Iteration 321 / 980) loss: 1.714960
(Iteration 341 / 980) loss: 1.782738
(Iteration 361 / 980) loss: 1.547322
(Iteration 381 / 980) loss: 1.838150
(Iteration 401 / 980) loss: 1.505023
(Iteration 421 / 980) loss: 1.743893
(Iteration 441 / 980) loss: 1.769522
(Iteration 461 / 980) loss: 1.470960
(Iteration 481 / 980) loss: 1.665716
(Iteration 501 / 980) loss: 1.334806
(Iteration 521 / 980) loss: 1.596020
(Iteration 541 / 980) loss: 1.633129
(Iteration 561 / 980) loss: 1.789139
(Iteration 581 / 980) loss: 1.359481
(Iteration 601 / 980) loss: 1.672585
(Iteration 621 / 980) loss: 1.626993
(Iteration 641 / 980) loss: 1.493078
(Iteration 661 / 980) loss: 1.327803
(Iteration 681 / 980) loss: 1.415701
(Iteration 701 / 980) loss: 1.897976
(Iteration 721 / 980) loss: 1.414025
(Iteration 741 / 980) loss: 1.599150
(Iteration 761 / 980) loss: 1.424620
(Iteration 781 / 980) loss: 1.736903
(Iteration 801 / 980) loss: 1.475317
(Iteration 821 / 980) loss: 1.592283
(Iteration 841 / 980) loss: 1.541136
(Iteration 861 / 980) loss: 1.503937
(Iteration 881 / 980) loss: 1.418334
(Iteration 901 / 980) loss: 1.731127
(Iteration 921 / 980) loss: 1.595903
(Iteration 941 / 980) loss: 1.439913
(Iteration 961 / 980) loss: 1.370036
(Epoch 1 / 1) train acc: 0.501000; val_acc: 0.498000
</pre>
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
<div class=" highlight hl-ipython2"><pre><span></span><span class="kn">from</span> <span class="nn">cs231n.vis_utils</span> <span class="kn">import</span> <span class="n">visualize_grid</span>

<span class="n">grid</span> <span class="o">=</span> <span class="n">visualize_grid</span><span class="p">(</span><span class="n">model</span><span class="o">.</span><span class="n">params</span><span class="p">[</span><span class="s1">&#39;W0&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">transpose</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">3</span><span class="p">,</span> <span class="mi">1</span><span class="p">))</span>
<span class="n">plt</span><span class="o">.</span><span class="n">imshow</span><span class="p">(</span><span class="n">grid</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="s1">&#39;uint8&#39;</span><span class="p">))</span>
<span class="n">plt</span><span class="o">.</span><span class="n">axis</span><span class="p">(</span><span class="s1">&#39;off&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">gcf</span><span class="p">()</span><span class="o">.</span><span class="n">set_size_inches</span><span class="p">(</span><span class="mi">5</span><span class="p">,</span> <span class="mi">5</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAa4AAAGtCAYAAABOYZA0AAAABHNCSVQICAgIfAhkiAAAAAlwSFlz
AAAPYQAAD2EBqD+naQAAIABJREFUeJzt3Xlw5Hl53/Gnb6nVklq3RtLoGElz7M61xyy77C677C6w
XAWUE3OZJGWo4EqFJC6Mq8A2sSuVSgIUNhiDY5PEBlexphxIbDCGZdl72YvZYefYuTW677PVUqtb
3Z1/8m8+j4IqrL6p9+vfT+v3+6rV3c901X72iVSrVQMAIBTR1/sAAAD832BwAQCCwuACAASFwQUA
CAqDCwAQFAYXACAoDC4AQFAYXACAoDC4AABBYXABAILC4AIABCX+eh/AzOwPej4u/4eJ6/G8e42N
MT2DZ6PzMu8pz8n80P5W9wz7etMyf9+z/0PmX/7GX8g8m0q6Z8iP6+dqaXFc5jPjV917zCwuy/zW
O94q80//wW/KfGjofvcMVxOTMn/w5gMyf9/7PuDe44N3VPQZlgZk3lozLfPBEx92z/Cerz4q81gl
JfOmeJ3MGyL73DPE6/R7K17skPlmpeDe448+Vivz9z/cJ/MHC/qjbKhZX9/MbLC+Tea960WZl1qP
6RvUbbhnSH7xGzL/009+SuaJqj6jmZnVJmRcietrxMpbMl/b8H9Pq9bI+F9/8c8iKucbFwAgKAwu
AEBQGFwAgKAwuAAAQWFwAQCCwuACAARlT/zn8ItDB2WeSOj/pNfMLNGvf5WaFX2NsfFnZb6auuae
oebKgvsYZS6i/xPRW/uPu9eIZ9dk/sIrMzKfPav/M3Mzs4nJ6zLvmNZ/T88nPvLr7mO+9tgPZP50
XP8nu5WL+j8zNzMrlptknmpYkflAc869h6d6Vv8n9ZdH9Wvu/NVX9PXz/r9d4w2dMj/uvC73t+ua
yE60pWMyrzRty7ywpHMzs5nIeZlPJXpkvr49K/PMjGz97MhtN+n6Qmdrxr1GW3+LzBPxssyjzved
hcUp9wyTk37FSZ8BAICAMLgAAEFhcAEAgsLgAgAEhcEFAAgKgwsAEBQGFwAgKAwuAEBQ9kQBeTTf
KPOaNl3MNTPbaD0l8/I+vROo/cCQzLcrV9wz5K6e0Q+Ye0bGh9t0yfLAgW7/DKu6PJg+r//k6zm9
a8vMbGFySeaFqVH3Gkr/W/SeKzOzj3W+Q+Y/u3hO5jOTuthrZvZ4RZc5h53nqv6I3lO1E90pvRtp
aEjviRto18/l0oIuUZuZJZz9TY2VVZk3lNxbuG60HZJ5pll/RlQS+jVrZrbRrJ+rSkn/LZJFXbTe
KPnPtaewpPcGzlc23WvE47oInazXnxExZy/Z7Jg+o5lZobCDvWEC37gAAEFhcAEAgsLgAgAEhcEF
AAgKgwsAEBQGFwAgKAwuAEBQ9kSPayGjF9Vttvl9mGQsqa/Rq3sg+Zhe+te/qrtmZmYrGecx5z8v
41xNVuY1zQ3uGQoF3QWzku6zRbf8fkV01VsCt+heQ6mJ3eM+5mj/oMyv1PTJPPK47tSZma1M6H7S
9wt6OemNrP577sTBI/0yP3lcLzfsGfwVmVcT/r9dt8d1B+r8Fd1nW7qol5eamX3Tyadrjso8NlKR
ebleL2A0M5tY1O+dYoPTcVzTn0GRhH5N7sSrs7q3lx7R728zsysjGzJ3XxMRPTbWVnTvz8zMYvoe
b3B+nG9cAICgMLgAAEFhcAEAgsLgAgAEhcEFAAgKgwsAEBQGFwAgKHuix7XWuC3z8ra/O+l6tVnm
0fFxmW8k9QzPpXWnx8xs0Py9YUopqvc/bZV0V8XMrFTUXZRIUp+x0fROITOz5qZamWece3jWnnT2
mpnZSqZF5u/M6tfD5v73uPcYnzgt8/uS+rmemdr9/qWa0VdkPr15VeaR6/r6mZT+W5qZVdP6NdE0
o3tBI2tj7j0856tvlHmqVX+UpcoR9x4rMd3Tqsvr13WrU7McSPifIZ7nRnXftDLr9zAnCwv6ASt6
p9/+Lt1PzDam3DO0p3bXceQbFwAgKAwuAEBQGFwAgKAwuAAAQWFwAQCCwuACAASFwQUACMqe6HEV
K2syL9Xqzo6ZWalGdxMi3bqvUlytl3nK2ddlZhZt211PY2ZC/w4Xmmbda1RGdF+tYpsybx32946t
FfRjknV6L5Hn2vP+79ld0Tuilpv1zrC2Tm+nmNmhFt1nuTCqe1pDs+fce3ju2a/fG9v5CX2BBf1v
03hp3T1DJK33K2VjQzJv7NfvrZ2oa75D5pO2JfPCin+Gpbh+jzds6d7ewvSIPkOL3qW1E69c1L/n
8ob/ObW2qj+n8pu6V5vN69dk2w76rA0dumf5Wefn+cYFAAgKgwsAEBQGFwAgKAwuAEBQGFwAgKAw
uAAAQWFwAQCCwuACAARlTxSQIzG97a4zpsumZmbpuC5SJmb0jC4V9D3a4n65OFrW5V5P0lnYNzfn
F3ML63oZXmpdl2qHu/e797Cifi4zcb/ErGRXLrmPWejQz0XN9K0yr2Z0UdvM7L47naWaiUEZ3+y9
HH7kHsF6Uk7hNKdfl6WyLknn50bdM0yv6793Mqrfv9vR3X/MLG7p0msxrUuvtc6iWDOzSFr/weam
OmTedrxH5uVZ/3XtaerX78+mqL8w0xL6M2Cr5FyjohfalnL+53XZ/GWTCt+4AABBYXABAILC4AIA
BIXBBQAICoMLABAUBhcAICgMLgBAUCLVavX1PoNFIpHX/xAAgD2hWq3KMhnfuAAAQWFwAQCCwuAC
AASFwQUACAqDCwAQFAYXACAoDC4AQFD2xD6uN7/7n8g8btvuNQ4c7JX5XbcdkPnd/Tpf3iq5Z3js
uZdk/unf+azMH3nHH8l83NkpZmZ2fW5R5pWlnMxLG9fcewz26N1HrU36ufr42e/I/K+//q/cM0yu
1cm8fEPvqbrv/gn3HuOVbpknLpyS+R/nL8j80f/0BfcM//7LfyXzhqzeIXU90SnzUt2Ge4btef3+
e7WzS+bPNe3g38dvvE/G3/3Sl2X+8qUzMh9f0HvNzMzWN/SOqN5e/Rlx4sRNMo83Jt0zfOQD75L5
sW/p56n/L/VeQjOzM+n7ZV74zj6dd+h9Xkf6fsU9Q9cd+nPIwzcuAEBQGFwAgKAwuAAAQWFwAQCC
wuACAASFwQUACAqDCwAQlD3R4xroy8j8tn2D7jX6b+6X+YF0WuabCwWZv3ruqnuGyUtL7mOUxex+
mW/WZt1rFBuKMs/P6P7S1qTfNZlLrMl8aX13z8P5v/mR+5iHskMyP9s4KvNrF0+69yi2d8h8uKq7
ZP9o+S6ZP+qewGzf+SdlvnD4iMxbG/Iy355tcc+QPtYu88KBPplHRvXzZGb2rJPXRudkfvHCCzIf
XZfrnczMLNOgu6Bv6H6jzIdP6r/FzMzu3hdmZr9ap+8xeYvfj+pejsn8796p82r0QZmf2sHndfOd
uuPo4RsXACAoDC4AQFAYXACAoDC4AABBYXABAILC4AIABIXBBQAICoMLABCUPVFAfsf9b5L5nQcP
u9fIxPVys9NPXZT53z7yQ5n/6NUR9wx9Q3ppn2ezrEvSW+16wZuZWU2zXixYzDTpMzT6L4m10rjM
kyv6DJ5/8bH3uY9ZyulycLVhRuYn4v6/2dqv3CLz8a5Wmd86qUuzO5Hu0GXvo5GfyLyuuVnmi226
XGxmtlg9KPOTzfp/ILAcSbj38BSX5mW+4BTrc0W/BN3Xrkvtg4O6oDx80yGZzy294p7BM/D3szJ/
IbvsXqNvSS/+nLpHvzfe/uTPZN7/sC7/m5nFn3Vedx/WMd+4AABBYXABAILC4AIABIXBBQAICoML
ABAUBhcAICgMLgBAUPZEj+v+B98l8+ai7miZmT3x3BmZf+lb35f5o08+L/NUyu+B3N19u/sYZSvu
LIps9xdJbs7pzlv6UEnmNQ3+PUorugeymW7TF7j+32T8wo+fcc8w+Pb3yLxjq17mdUV/qd+F/kmZ
p6oLMr/e6y/189TG9eu6Oaf/FtGX9WLRzl7dEzMzy1T0c3kp0aDvYcPuPTxTs7qXt7y6KvOalO5I
mpklYimZJ+t0Hy1telllMar/FjuReEB3Od/1zHH3Ghca9DlPjeo+Wt0Jff30uQPuGb5Ro3uz/8b0
Ela+cQEAgsLgAgAEhcEFAAgKgwsAEBQGFwAgKAwuAEBQGFwAgKDsiR7X+qzuYLz43M/da3z9kb+R
+dnLV2X+trc9KPM77r/XPcNb7jol8z//7h/KPFdekXk64nesvArVVl73QDajMfceDZmCzDPlpHsN
Jdnm/54z13W/KfIT3Zl54Ra9W8nM7O42vWeqtU7v47pjTj/XH3RPYNa4oPeO3RTTvbzpOqevVrzZ
PcNgzZTMJ8f1zq/lLf263oliUneoUvUtMm9p9XfZdQzpvlmyWpH51JJ+rsubW+4ZPEcade/uer3f
N5247w6ZP/C4/hCZbG2U+Yb1uGfoffq6+xiFb1wAgKAwuAAAQWFwAQCCwuACAASFwQUACAqDCwAQ
FAYXACAoe6LH9dWvfF3mL//0vHuNzbLu7dz1Ft3T+ugH3ybz9vb97hlKud3tX2ro1f+OSCX8nULp
hO5QpVryMm9O6109ZmbZFd3biSbW3WsoX0i83X3Mb9fdkPmFfRdkHiuPu/d43vRz9eEZ/VxXB/XP
70SlXe+6urilXzOd03qPVaxe76AyM2sf0T3LQx2635Qu6Q6Wmdm3nTyf0x9VjQ26e7Sve8g9Q6qq
73FufFbmW6a7ohcv6D7cTtyYPSfz0j1+X60xov+e43foz5nOGzqPRi67Z8gf9D9P5T129dMAAPyS
MbgAAEFhcAEAgsLgAgAEhcEFAAgKgwsAEBQGFwAgKAwuAEBQ9kQB+anTelFkc4te6GdmdvubHpL5
g+8+KfPedr1EbuySLrSamZ17zS/eKcUZ/fORGr/IGd3WSxgbU4dknk9suPeIZbZlXs3trnh75fKj
7mM+OTsn86GVizK/Or7o3qP3HXrJ4pfGjsv83fuvuPfwVGo/JPOXqyMyz3bpJY7Dr73snqEpf5fM
e9pGZT5bPOjew1OO6df+8H79uu4Z8Bdmpmp1sX5pXBfrX4vpUvvWxrJ7Bs/1Lb0ocuinZfcaoyv6
PT4+/EOZXzivF2KeHPKXWV7/28/pB3zlN2XMNy4AQFAYXACAoDC4AABBYXABAILC4AIABIXBBQAI
CoMLABCUSLVafb3PYJFI5PU/BABgT6hWq3KjLd+4AABBYXABAILC4AIABIXBBQAICoMLABAUBhcA
ICgMLgBAUPbEPq7f/sN/LPOFaNq9xoVySublmN5TVd3Q+dF+v2rWtlmR+ed//fdk/taPfE/m9w7r
fUFmZp/43Q6Z557+rMyferzdvcedD9wj8yvjeu/Qwx/+mMxvPa73s5mZpat6N9J0okXmDalV9x6l
7YK+Rn2bzNe29Q6pc0/pHXBmZu/71KdkfvDgAZk3JvS/TQ/06+fJzGx9Te9XW8/pHVAXr+idYWZm
f/r7/07m73mxUebpin5/dtcPume4dknv01qc1H/PgRa9dyxR0e9NM7Ov/9q3Zf4fPvpRmS+uzrr3
WBipl3lz4h0yf+8B57P03h73DC0X9E4/D9+4AABBYXABAILC4AIABIXBBQAICoMLABAUBhcAICgM
LgBAUPZEj6vuoV/TD6jRHQ4zsxN1+2S+WtDdhWSdnuH7i7rLYma2vZlzHqF7XNHBIZ3HnnbP8PVv
Tcg8WaqReWz0mnuP0XO6OxQ5s+ReQ2mO656ImVlrWf8eTe26U5Ot9XtcFtW9nXLVefsUFmV8zj+B
5aL697w6tiXzTFafMVfdcM9Qm4zJvLyhOzmVfK17D08+2iDz+rK+x8Ss/3tul/XnTKGie5pLJZ03
ZXf/PeHQQ3Uyz853ute4elz3QY+2OZ3YFf33fvGlM+4ZvvtfX5X5M1++XeZ84wIABIXBBQAICoML
ABAUBhcAICgMLgBAUBhcAICgMLgAAEFhcAEAgrInCshTpYzMY1l/AVu+VpcH8zW6VLexpp+KZMxf
fFaKFN3HKJVmXWC+NHndvcZ733mrzM9994LM10745d9TQ/rfO9+cmnGvoZy8+gP3MZGkfq6qC05p
vb7JvUcqru+xteEUcyub7j088bJe0jhxQy9pvDExJ/NUVZdmzcwikZLMOzp1+b+rU5eHd6K6rd9/
6ax+nkrburhrZtbWq8veAwP691ye1n/v/IZeTLoT6bRePhrp8svePclJmV+e1dfIjevPoWdW/fd/
5m5/Ma/CNy4AQFAYXACAoDC4AABBYXABAILC4AIABIXBBQAICoMLABCUPdHjeuzqvMyjkwvuNeYr
aZmXnUV0a6srMh9IJt0zFFb9cyqt87MyT2Tvcq8x/vxlmV9d1L2ffa/ovpuZWfzkEZlff173fjzv
9PeGWrRed+bmkjpvjOrn2syssuV0g+ItMp9fXXPv4emM6kWRG2W9rLK8oheDjq0su2eI5JzOTVX3
l1rre9x7eC5fnZZ5pLVL5nfcopefmpltjur+0cjoDZnn5ltl3t7if4Z4hpvGZN7S0Ode42pzt8zj
Vf15/PhpvSh2OO2//29//6D7GIVvXACAoDC4AABBYXABAILC4AIABIXBBQAICoMLABAUBhcAICh7
osdVV+vMz5pm9xrbc3pfT7lZ75hpsHWZN2b9/U11Md2B0k0Us/Y7j8l8dvo19wyLL+mdP3dN3ynz
5qN+v+LlzvfKvDDzNfcaSneN3iFlZtYb0d2h1Wy7zIuZNvceUWdV1WJFPyC9OaQv4FfJ7OGbdVes
5p79Mo/X6f1sVki4Z1jbyMt8fkm/90qbG+49/t7JE+u63Nc2pLtJA+3+6/qZV/VnwPNPnJb54aP6
NdXRpndp7UR8WHfiZtf9Hldy/mmZr6zosdDe/ZzM6+uc172Z7UvpzpuHb1wAgKAwuAAAQWFwAQCC
wuACAASFwQUACAqDCwAQFAYXACAoe6LHdWRwQObZzl73Gv0Fvbco0qB7A8vzesfMPX1+72D+iu4f
nXN+Pn/6MZnXzeu+jJlZsf6vZT7Tpbsm+ZEb7j2SX31E5uPn9G4zz9z4i+5jIoWIzLezujXX2pdx
71FI6Q6VxXSnpqNe94J2oqmqd7ztr9d/z96+DpnX1fn/ds1t1sl8ZFTv9Jod093Cneho1R2orW3d
9fzeD66695iZ1891Q/8hmWfb9edYtK7TPYOnsKX3Dsa2dcfKzOy5Zf33qIvq123rPfr10Fqud88Q
q/VarRrfuAAAQWFwAQCCwuACAASFwQUACAqDCwAQFAYXACAoDC4AQFAYXACAoOyJAvK1F1+WeUur
Xx68MK+X1VWr+lfdWNQ/nxjURU4zs+mrE+5j5M/36BJlPqmXJ5qZtTW/WeaNTtG6rclfLPjUqi6D
TsWr+gJOj7rUr5cjmpld3xzV1yjov+fVG5PuParVksxnYrqU3t6rC6k78dSP9Xsjv6GL97atl13G
Yvp3NDOLpxtkXtOs83RKL4HciaH+kzIfn7gh82sX/MJrV5teNnvigF5GWZ/Si2Qnr864Z/CsLOtl
lomlKfcax/cVZd7Qc1DmN/dmZf7UWX9J63ruuvsYhW9cAICgMLgAAEFhcAEAgsLgAgAEhcEFAAgK
gwsAEBQGFwAgKJFq1enc/DIOEYm8/ocAAOwJ1WpVborlGxcAICgMLgBAUBhcAICgMLgAAEFhcAEA
gsLgAgAEhcEFAAjKntjHNdF1v8xrCjn3Gi0lvZdoNaJ3BuWrehfWSiLmnmGpWe/juffqt2X+T2/7
C5kPHG/yz7BakPl8/7jM6xKd7j3Otx+V+d3ZEzL/wkdlRcO+8Rv/0j3DVPSKzDN6XZc17tM7h8zM
jvTovUI1xbfK/PBB/ZqL/7Ob3DN87e8+LfPajN4R9czKT2V+uLPOPcNsNCnzsdKCzG/Ktrv3+LdH
PyfzL3/+P8q8r69P5iOX1twzXB6dlfkDb75N5okavWju/KVz7hk+85nfkXlr3wdkftOi3pVlZla9
tUvmp+L6+8xrL+ZlPpO+2T3D3Oqq+xiFb1wAgKAwuAAAQWFwAQCCwuACAASFwQUACAqDCwAQFAYX
ACAoe6LHlS/o7lFTXvcjzMzWyrrHtRbVXbCVou6q5FK6o2VmtpL2OzHKvubHZF6e070gM7PvN+jV
Znde032W2Zoe9x6ZuRGZn71pwr2GMtDZ6z6mo1l32lbXdJFr9ib/b7U1U5J5tUv3l86UdV9mJ9Y6
9Dm7MmWZH9vskHmpVv+8mVkmqvtHB6v677X/5oR7D0+lsiLznoFbZT4663dBz3zvoszvvGtY5scG
9Xvn2mX9etqJr36oRebPTs6517j8/ZdkvnzipMwHMrrruRbRXVEzsztaKu5jFL5xAQCCwuACAASF
wQUACAqDCwAQFAYXACAoDC4AQFAYXACAoDC4AABB2RMF5NEuvQSutDLjXqNsrTLf2NCFt3JcL2Cb
qdXXNzObbdTLKM3p5a6X9b8jil1+WfTUki7/Fcu6uBvL+mXRxWi9zNsKRfcayg8P+eXEGmeZ3Xq/
Lu5GxubdezQ161J6un5K5m2NfunV02/671Gu06+ZVM+mzA906tzMLF7VRerNjH5vtG75pXbPxoZe
PNjdp5d+Jk/rv5WZ2cUrl2W+uLwu87b9+nlIp/z3r6dnUP+9j2+Nudd47rD+nxCUf/IzmffFT8n8
wCF/SWtNXn+GePjGBQAICoMLABAUBhcAICgMLgBAUBhcAICgMLgAAEFhcAEAgrInelznnf7Scjbj
XqOy5fSP0nqJW7HcKPOtZMQ9w1St7v146rYXZZ6OtbvXqER118Q69KLJ2o20e4+tmF5WVzqwux7X
Lb0PuI/Jx3QXJbZ0RublYb0E0sys55p+TSXbdRflyKbuJ+5E74z+Pa9Uzsq8L657fc01R9wzTEzo
v3dzvX7/TiV3tzTQzKxU1H2zjhbd22vN+otDl1b1cz0xNS3ztPMR0dq8u0WzZmYrW05frUYv1DUz
663Tr9v3n9J91KvTugs60THonmF/tN99jMI3LgBAUBhcAICgMLgAAEFhcAEAgsLgAgAEhcEFAAgK
gwsAEJQ90eO6eKhT5jOb/o6o2liNzJNbut+wUtH7uIr1/j6upZTTN3tBx5WS3hFVs+7/uSKlbZlv
bOvf49IB3RMxM8tUdOetWLu7XTuJf0i5j9ke0D2sREX/m2zfVb3fycys0Kqf783CqMxf7Ljm3sNT
Tepu4P7issyXRi/JfLat2z1Do+mCUt2y7kiemvN7mJ6Nbf26Lm/rXVdNDQ3uPeozup+0PKv3q00u
6DwV81/XnuY79V6xric73GvE3xSTeWZRfxaWHj0v8+Mjh9wzXK7V/UOz35Ap37gAAEFhcAEAgsLg
AgAEhcEFAAgKgwsAEBQGFwAgKAwuAEBQ9kSPa7JJd4cWs7qjZWbWUCzIvOx1j0zvyllo8PdxreZ0
n8VzYVN3zYp1/j6fyRszMp8Z0/u2EgXdhzEzmy3rvWGRUr97DaVSes19TGb05zJvzOrnYaln0r3H
vjN5mdcMvCrzfEH3E3fipZ8/IfOOWr07aX5V959aap51z7AY1XvgOkv6vTF2cnf72czMUiXd5Zwa
0x3IrYKzp87MTh3Ve6Qyzr69hbFZfYaS3oW3E/WVfTKfeesN9xozT56Q+eiY/gwY29Q73n6w+pfu
GQob/c4j6HEBAP4/wuACAASFwQUACAqDCwAQFAYXACAoDC4AQFAYXACAoDC4AABB2RMF5PFGPT/T
MV2aNTPLR3U5d7ukl7xZRf/8Vl3FPUMpu7t/B8Si98j8rqS/oO109JjM64/qBYqlFb1kzsysGhuW
eaFDL6tcc65/6PCEe4bI4pLMG+s39M+v+0seO96tHzO6eUTm3Ytd7j08I4/p8m7yXl0G71jXiwUz
1/QiSjOzauUlmT/XoEvOie/5pXZPQ7N+TU3N6t9je1P/DwrMzG4+3Cvz+rQuQc8t6BJ0pbi7/0GB
mdmPb78o8/J3/M+g8+P/U+bDWf1ZeaNOL9xsm9L/IwUzs3jzz5xH6BIz37gAAEFhcAEAgsLgAgAE
hcEFAAgKgwsAEBQGFwAgKAwuAEBQItXq7peb7foQkcjrfwgAwJ5QrVbldlK+cQEAgsLgAgAEhcEF
AAgKgwsAEBQGFwAgKAwuAEBQGFwAgKDsiX1cv/XNL8k8o/+T/v9N7wSqL+lrlBb0XqNSTO/iMTOL
FDMy/93PfFLmv5X4lMyXsne7ZyhU9O9Zm5yReXfyCfceB5vyMm+t1TuDHv7pZZn/efJV9wxd9z0u
81ef1q+Hq1t6X5eZWUP1RZnvP/QhmZ9e1XuN/mrmn7tnOP9gvczPzOjXxFL6lMwvFU+6Z2io1Tvc
WrfOyfzmZn8X1tse+6rMj/5nfYbqlN6FVS7q/W1mZttjKX0PZ29gtLZZ5oV5/zNk/BvtMr/poUf0
Gdb1/jYzs6OV6zK/rzkp876mGzLvv909gm1MN/gPEvjGBQAICoMLABAUBhcAICgMLgBAUBhcAICg
MLgAAEFhcAEAgrInelx3zo/IvHZ92b3GWk53i9pS+lfNJHUHKx7vdc8wt7LuPkZZr7tF5oc6/D7M
C1ttMk+a7olErwy790j0PS/z9rg+g5nucfU8MO2e4Yztl/nh4/rn35B+xr3Hz3vfIvOTxw7JfG1U
n9G+4ve4nni2X+bXM/rvtTowKPOZrqPuGeI1WZkPT+lOXMT8DpWna3JS5mtrczKvX/X/jR5N6h5X
T4u+Rsz5DEr1+n3UP3by7aP6c6p2seTeoz6hu39zaxdkXo7r9+eBnPf+N+vq1Z03D9+4AABBYXAB
AILC4AIABIXBBQAICoMLABAUBhcAICgMLgBAUBhcAICg7IkCcuzCuMxzK3rJo5lZOTcr81S7Lt42
9HTIfNv88m9qXS/982QP6KLn6egB9xrbKV3ErBnTBcbciap7j5lCk8yzG3qpn6c+7i/Dazg8IPPN
9TWZZ4f0gkUzs4dfS8s8Va8XA378Pfo18/tfcY9ga8fulHk1oUvQlbYjMt/YQbE+tq3ff8sNnTIv
xP3XlKfc5/ilAAAIUklEQVR/bVTm2ZKzGDTb5d6jL6V/z2hcF5StVi8vLW/rfCeWF/WSx8KS/z9r
2ByskXmsRr/u56/r9/f1Pv/9f6rBLykrfOMCAASFwQUACAqDCwAQFAYXACAoDC4AQFAYXACAoDC4
AABB2RM9rief/6nMO0p+/yHb2iDzugHdkcqvxmQ+saSXxJmZLeZ3tzAvv6l7Itmi7pqZma0mdIci
36g7Uk1ruidiZpZo1P2lqczu/j30zKru7JiZlS7rZXaxvn6ZV/Sf28zMzmXKMj9S1s/lYFV35nbi
2sKQzEtJ/Zp4paK7hZMtutNjZta4qZf+LS01yrwzseXew3Pz/pzMu1d0b687seDeY6mqe3cR079n
LL4q842tOvcMnuYWvShyPO9/pPen9d+zo0UvvLwwop/r3JheDGxm1trn9ygVvnEBAILC4AIABIXB
BQAICoMLABAUBhcAICgMLgBAUBhcAICg7Ike1+FPfF7mhw7o3UtmZl37dEei29nH8/3Hzsj8zNlJ
9ww3ZvyulxLvq5V568pp9xpPzzwg8/bEMzJfr+q9ZWZmpaTuip2a291esrnVq+5jmlqOyfzWG/r3
nHqz/2+2ulXdyzlceELm3fX+/jRPo9NPKrTpflPntO4vxSt6f5uZWSGi+2zxit5jlRrdXb/RzOyW
xEWZ19brfXwdN/TzaGbWk5mR+XRKvz/jU/r6IwXdn9qJjS29K2ujqLtmZmZzUd0/vPugPufES30y
H13Rz6OZ2UhFjx7vE59vXACAoDC4AABBYXABAILC4AIABIXBBQAICoMLABAUBhcAICh7osc12/+w
zKdKev+TmVn1it7ZNTWpuyZP/GhM5isJf2/RUHbQfYyyNbEs87W03tdlZtZj52Re3dKdnM2Ifh7M
zCKZDZlXlivuNZTYlN8tGk2elfmf1eqdQsOv+K+pQ/aEzH+SPyTzN75w3b2Hp3VTd8EWo/pv0Rwb
l3l+fZ97hkxEv+76avVyswP97i3sO86ffP+27mllF/UOqGyd7uSZmVVyuqtZM613YeUSOu9a9V9z
nrt7dAdrvez31epNP6Yucljm7QebZL55TX+OmZnlt3Uvz8M3LgBAUBhcAICgMLgAAEFhcAEAgsLg
AgAEhcEFAAgKgwsAEBQGFwAgKHuigPzqtRWZn3/xZ+41xpzS60ZZL9zL1rTJ/Nhdp9wzHD+iy5wv
/Bf98+mcPsP0ti5Zm5kV63TR+mxTQebDI3rhpplZZUGXOUerm+41lJHGJ9zHXBrtkPnNA7qwalN+
WXx76ILMbx3SCzVbJ/zCuKe28JLMc2M9Ml8vd8t8X9dr7hkizbp8f2hJl9aTid0V0s3M8tt6ier2
vF5eONfql9pjVZ2Xt/R7p7Soi9jLJV0e3olIk14k2ba97l6jUtYf+/E2vRA3M5iReaTQ6Z5hc1u/
fz184wIABIXBBQAICoMLABAUBhcAICgMLgBAUBhcAICgMLgAAEGJVKtOeeGXcYhI5PU/BABgT6hW
q3ITLN+4AABBYXABAILC4AIABIXBBQAICoMLABAUBhcAICgMLgBAUPbEPq5f/b0vynx4eNi9RmlF
7+NJx2UtwG7Mbcj82s/1biYzs8vTN2Q++/w/6Avc8zkZ78+NuGeozx6V+YkOvSunnGtx7/HgMb1v
a+3MG2T+qR81u/cAgP8TvnEBAILC4AIABIXBBQAICoMLABAUBhcAICgMLgBAUBhcAICg7IkeV9P+
bpmvFlbcaywsjMl8aVb3tHKrOZlvlfLuGd5825DMH3le//zQYf3viFVrc88wMKH7avNl/fPN+cfd
ezz5nR59ho4F9xoA8IviGxcAICgMLgBAUBhcAICgMLgAAEFhcAEAgsLgAgAEhcEFAAgKgwsAEJQ9
UUBejely78SlCfca1y++JvNSYVHmNdGSzAf6mtwzvPGhEzJ/5E/0zzdFD8g8Oz3uniG1ppc8Rvbp
a4wutbr3ePfBbf2AGIsiAfy/wzcuAEBQGFwAgKAwuAAAQWFwAQCCwuACAASFwQUACAqDCwAQlD3R
4zr9w/8u85nZZfcaa2uXZD6Y0j9/6N6DMj/c5T9Vh465D5GK/XUyv2ef3yU7e1ovxEzNn5V5a6zT
vce+1qrMszndiQOA3eAbFwAgKAwuAEBQGFwAgKAwuAAAQWFwAQCCwuACAASFwQUACMqe6HENNW3I
/OHhfv8at9wh8766iswHhgdkvp7XO8PMzBKR3T2db22plXkpV3Cv0del9231ruifz8acB5hZOXuT
zCO119xrAMAvim9cAICgMLgAAEFhcAEAgsLgAgAEhcEFAAgKgwsAEBQGFwAgKAwuAEBQ9kQB+TMf
fJvM270tkGbW3ZyVebqiC8TzuYTMr41suWd4+emL7mOUUvu9Mr+w/LJ7jdZ8r8xXuyf0z3cece/R
u56R+VZm0L0GAPyi+MYFAAgKgwsAEBQGFwAgKAwuAEBQGFwAgKAwuAAAQWFwAQCCsid6XPO5TZmP
v7DuXuOprRsyn752WeZzc0mZL+YW3TPM5Xb3dDa2zMu8baHFvUZ7m/49ijVHZd6avOLeo+amsswz
CzH3GgDwi+IbFwAgKAwuAEBQGFwAgKAwuAAAQWFwAQCCwuACAASFwQUACEqkWq2+3mcAAGDH+MYF
AAgKgwsAEBQGFwAgKAwuAEBQGFwAgKAwuAAAQWFwAQCCwuACAASFwQUACAqDCwAQFAYXACAoDC4A
QFAYXACAoDC4AABBYXABAILC4AIABIXBBQAICoMLABAUBhcAICgMLgBAUBhcAICgMLgAAEFhcAEA
gsLgAgAEhcEFAAgKgwsAEBQGFwAgKAwuAEBQGFwAgKD8L7ynXhDQV1+UAAAAAElFTkSuQmCC
"
>
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
<div class=" highlight hl-ipython2"><pre><span></span><span class="n">history_7x7</span> <span class="o">=</span> <span class="n">solver</span><span class="o">.</span><span class="n">loss_history</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[11]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Try filter size 3x3</span>
<span class="n">layers</span> <span class="o">=</span> <span class="p">[</span>
    <span class="p">[</span><span class="s1">&#39;conv&#39;</span><span class="p">,</span> <span class="p">{</span><span class="s1">&#39;num_of_filters&#39;</span><span class="p">:</span><span class="mi">32</span><span class="p">,</span> <span class="s1">&#39;filter_size&#39;</span><span class="p">:</span><span class="mi">3</span><span class="p">}],</span>
    <span class="p">[</span><span class="s1">&#39;relu&#39;</span><span class="p">],</span>
    <span class="p">[</span><span class="s1">&#39;pool&#39;</span><span class="p">],</span>
    <span class="p">[</span><span class="s1">&#39;affine&#39;</span><span class="p">,</span> <span class="p">(</span><span class="mi">500</span><span class="p">)],</span>
    <span class="p">[</span><span class="s1">&#39;relu&#39;</span><span class="p">]</span>
<span class="p">]</span>
<span class="n">model</span> <span class="o">=</span> <span class="n">convnetGenerator</span><span class="p">(</span><span class="n">layers</span><span class="o">=</span><span class="n">layers</span><span class="p">,</span> 
                         <span class="n">verbose</span><span class="o">=</span><span class="bp">False</span><span class="p">,</span> 
                         <span class="n">weight_scale</span><span class="o">=</span><span class="mf">1e-3</span><span class="p">,</span>
                         <span class="n">reg</span><span class="o">=</span><span class="mf">0.001</span><span class="p">)</span>

<span class="n">solver</span> <span class="o">=</span> <span class="n">Solver</span><span class="p">(</span><span class="n">model</span><span class="p">,</span> <span class="n">data</span><span class="p">,</span>
               <span class="n">num_epochs</span><span class="o">=</span><span class="mi">1</span><span class="p">,</span> <span class="n">batch_size</span><span class="o">=</span><span class="mi">50</span><span class="p">,</span>
               <span class="n">update_rule</span><span class="o">=</span><span class="s1">&#39;adam&#39;</span><span class="p">,</span>
               <span class="n">optim_config</span><span class="o">=</span><span class="p">{</span>
                    <span class="s1">&#39;learning_rate&#39;</span><span class="p">:</span> <span class="mf">1e-3</span>
               <span class="p">},</span>
                <span class="n">verbose</span><span class="o">=</span><span class="bp">True</span><span class="p">,</span> <span class="n">print_every</span><span class="o">=</span><span class="mi">20</span><span class="p">)</span>
<span class="n">solver</span><span class="o">.</span><span class="n">train</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>(Iteration 1 / 980) loss: 2.304682
(Epoch 0 / 1) train acc: 0.157000; val_acc: 0.149000
(Iteration 21 / 980) loss: 2.061422
(Iteration 41 / 980) loss: 2.017416
(Iteration 61 / 980) loss: 1.694147
(Iteration 81 / 980) loss: 2.088317
(Iteration 101 / 980) loss: 1.877042
(Iteration 121 / 980) loss: 1.958555
(Iteration 141 / 980) loss: 1.732520
(Iteration 161 / 980) loss: 1.558876
(Iteration 181 / 980) loss: 2.015591
(Iteration 201 / 980) loss: 1.784223
(Iteration 221 / 980) loss: 1.623718
(Iteration 241 / 980) loss: 1.446056
(Iteration 261 / 980) loss: 1.461913
(Iteration 281 / 980) loss: 1.467658
(Iteration 301 / 980) loss: 1.527802
(Iteration 321 / 980) loss: 1.499437
(Iteration 341 / 980) loss: 1.628613
(Iteration 361 / 980) loss: 1.454831
(Iteration 381 / 980) loss: 2.153976
(Iteration 401 / 980) loss: 1.617547
(Iteration 421 / 980) loss: 1.431443
(Iteration 441 / 980) loss: 1.473944
(Iteration 461 / 980) loss: 1.313490
(Iteration 481 / 980) loss: 1.570247
(Iteration 501 / 980) loss: 1.431398
(Iteration 521 / 980) loss: 1.456620
(Iteration 541 / 980) loss: 1.356616
(Iteration 561 / 980) loss: 1.351886
(Iteration 581 / 980) loss: 1.275274
(Iteration 601 / 980) loss: 1.699909
(Iteration 621 / 980) loss: 1.495320
(Iteration 641 / 980) loss: 1.635343
(Iteration 661 / 980) loss: 1.383922
(Iteration 681 / 980) loss: 1.443174
(Iteration 701 / 980) loss: 1.290799
(Iteration 721 / 980) loss: 1.469113
(Iteration 741 / 980) loss: 1.620972
(Iteration 761 / 980) loss: 1.765069
(Iteration 781 / 980) loss: 1.391391
(Iteration 801 / 980) loss: 1.437773
(Iteration 821 / 980) loss: 1.720682
(Iteration 841 / 980) loss: 1.365103
(Iteration 861 / 980) loss: 1.441266
(Iteration 881 / 980) loss: 1.355539
(Iteration 901 / 980) loss: 1.402413
(Iteration 921 / 980) loss: 1.501388
(Iteration 941 / 980) loss: 1.531445
(Iteration 961 / 980) loss: 1.574137
(Epoch 1 / 1) train acc: 0.541000; val_acc: 0.527000
</pre>
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
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># plot both runs to compare</span>
<span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">history_7x7</span><span class="p">,</span> <span class="s1">&#39;o&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">solver</span><span class="o">.</span><span class="n">loss_history</span><span class="p">,</span> <span class="s1">&#39;o&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;iteration&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;loss&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">legend</span><span class="p">([</span><span class="s1">&#39;7x7&#39;</span><span class="p">,</span> <span class="s1">&#39;3x3&#39;</span><span class="p">],</span> <span class="n">loc</span><span class="o">=</span><span class="s1">&#39;upper right&#39;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[12]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>&lt;matplotlib.legend.Legend at 0x7fe52ea73b10&gt;</pre>
</div>

</div>

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
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Check number of filters impact</span>
<span class="n">filter_numbers</span> <span class="o">=</span> <span class="p">[</span><span class="mi">8</span><span class="p">,</span> <span class="mi">16</span><span class="p">,</span> <span class="mi">32</span><span class="p">,</span> <span class="mi">64</span><span class="p">]</span>
<span class="n">stats</span> <span class="o">=</span> <span class="p">[]</span>
<span class="k">for</span> <span class="n">f</span> <span class="ow">in</span> <span class="n">filter_numbers</span><span class="p">:</span>
    <span class="n">layers</span> <span class="o">=</span> <span class="p">[</span>
        <span class="p">[</span><span class="s1">&#39;conv&#39;</span><span class="p">,</span> <span class="p">{</span><span class="s1">&#39;num_of_filters&#39;</span><span class="p">:</span><span class="n">f</span><span class="p">,</span> <span class="s1">&#39;filter_size&#39;</span><span class="p">:</span><span class="mi">3</span><span class="p">}],</span>
        <span class="p">[</span><span class="s1">&#39;relu&#39;</span><span class="p">],</span>
        <span class="p">[</span><span class="s1">&#39;pool&#39;</span><span class="p">],</span>
        <span class="p">[</span><span class="s1">&#39;affine&#39;</span><span class="p">,</span> <span class="p">(</span><span class="mi">500</span><span class="p">)],</span>
        <span class="p">[</span><span class="s1">&#39;relu&#39;</span><span class="p">]</span>
    <span class="p">]</span>
    <span class="n">model</span> <span class="o">=</span> <span class="n">convnetGenerator</span><span class="p">(</span><span class="n">layers</span><span class="o">=</span><span class="n">layers</span><span class="p">,</span> 
                         <span class="n">verbose</span><span class="o">=</span><span class="bp">False</span><span class="p">,</span> 
                         <span class="n">weight_scale</span><span class="o">=</span><span class="mf">1e-3</span><span class="p">,</span>
                         <span class="n">reg</span><span class="o">=</span><span class="mf">0.001</span><span class="p">)</span>
    <span class="n">solver</span> <span class="o">=</span> <span class="n">Solver</span><span class="p">(</span><span class="n">model</span><span class="p">,</span> <span class="n">data</span><span class="p">,</span>
                    <span class="n">num_epochs</span><span class="o">=</span><span class="mi">1</span><span class="p">,</span> <span class="n">batch_size</span><span class="o">=</span><span class="mi">50</span><span class="p">,</span>
                    <span class="n">update_rule</span><span class="o">=</span><span class="s1">&#39;adam&#39;</span><span class="p">,</span>
                    <span class="n">optim_config</span><span class="o">=</span><span class="p">{</span><span class="s1">&#39;learning_rate&#39;</span><span class="p">:</span> <span class="mf">1e-3</span><span class="p">,},</span>
                    <span class="n">verbose</span><span class="o">=</span><span class="bp">True</span><span class="p">,</span> <span class="n">print_every</span><span class="o">=</span><span class="mi">100</span>
                   <span class="p">)</span>
    <span class="n">solver</span><span class="o">.</span><span class="n">train</span><span class="p">()</span>
    <span class="n">stats</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">solver</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>(Iteration 1 / 980) loss: 2.303082
(Epoch 0 / 1) train acc: 0.097000; val_acc: 0.107000
(Iteration 101 / 980) loss: 1.638973
(Iteration 201 / 980) loss: 1.593063
(Iteration 301 / 980) loss: 1.578063
(Iteration 401 / 980) loss: 1.630801
(Iteration 501 / 980) loss: 1.706995
(Iteration 601 / 980) loss: 1.738532
(Iteration 701 / 980) loss: 1.297444
(Iteration 801 / 980) loss: 1.598771
(Iteration 901 / 980) loss: 1.449220
(Epoch 1 / 1) train acc: 0.577000; val_acc: 0.520000
(Iteration 1 / 980) loss: 2.303643
(Epoch 0 / 1) train acc: 0.085000; val_acc: 0.107000
(Iteration 101 / 980) loss: 1.790572
(Iteration 201 / 980) loss: 1.545909
(Iteration 301 / 980) loss: 1.655494
(Iteration 401 / 980) loss: 1.378390
(Iteration 501 / 980) loss: 1.348919
(Iteration 601 / 980) loss: 1.805475
(Iteration 701 / 980) loss: 1.394510
(Iteration 801 / 980) loss: 1.295717
(Iteration 901 / 980) loss: 1.317254
(Epoch 1 / 1) train acc: 0.535000; val_acc: 0.515000
(Iteration 1 / 980) loss: 2.304612
(Epoch 0 / 1) train acc: 0.099000; val_acc: 0.107000
(Iteration 101 / 980) loss: 1.746556
(Iteration 201 / 980) loss: 1.641346
(Iteration 301 / 980) loss: 1.832679
(Iteration 401 / 980) loss: 1.675884
(Iteration 501 / 980) loss: 1.827131
(Iteration 601 / 980) loss: 1.553097
(Iteration 701 / 980) loss: 1.720324
(Iteration 801 / 980) loss: 1.384032
(Iteration 901 / 980) loss: 1.171511
(Epoch 1 / 1) train acc: 0.503000; val_acc: 0.530000
(Iteration 1 / 980) loss: 2.306743
(Epoch 0 / 1) train acc: 0.133000; val_acc: 0.142000
(Iteration 101 / 980) loss: 1.793919
(Iteration 201 / 980) loss: 1.847362
(Iteration 301 / 980) loss: 1.582304
(Iteration 401 / 980) loss: 1.630551
(Iteration 501 / 980) loss: 1.517153
(Iteration 601 / 980) loss: 1.656106
(Iteration 701 / 980) loss: 1.705829
(Iteration 801 / 980) loss: 1.708226
(Iteration 901 / 980) loss: 1.591098
(Epoch 1 / 1) train acc: 0.525000; val_acc: 0.524000
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[15]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># number of filter does not have big impact</span>
<span class="k">print</span> <span class="s1">&#39;# train_acc val_acc&#39;</span>
<span class="k">for</span> <span class="n">i</span><span class="p">,</span> <span class="n">s</span> <span class="ow">in</span> <span class="nb">enumerate</span><span class="p">(</span><span class="n">stats</span><span class="p">):</span>
  <span class="k">print</span> <span class="n">filter_numbers</span><span class="p">[</span><span class="n">i</span><span class="p">],</span> <span class="n">s</span><span class="o">.</span><span class="n">train_acc_history</span><span class="p">[</span><span class="o">-</span><span class="mi">1</span><span class="p">],</span> <span class="n">s</span><span class="o">.</span><span class="n">val_acc_history</span><span class="p">[</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre># train_acc val_acc
8 0.577 0.52
16 0.535 0.515
32 0.503 0.53
64 0.525 0.524
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[18]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Add batch norm and check the impact</span>
<span class="n">layers</span> <span class="o">=</span> <span class="p">[</span>
  <span class="p">[</span><span class="s1">&#39;conv&#39;</span><span class="p">,</span>  <span class="p">{</span><span class="s1">&#39;num_of_filters&#39;</span><span class="p">:</span><span class="n">f</span><span class="p">,</span> <span class="s1">&#39;filter_size&#39;</span><span class="p">:</span><span class="mi">3</span><span class="p">}],</span>
  <span class="p">[</span><span class="s1">&#39;relu&#39;</span><span class="p">],</span>
  <span class="p">[</span><span class="s1">&#39;pool&#39;</span><span class="p">],</span>
  <span class="p">[</span><span class="s1">&#39;spatial_batchnorm&#39;</span><span class="p">],</span> <span class="c1"># normalize before affine</span>
  <span class="p">[</span><span class="s1">&#39;affine&#39;</span><span class="p">,</span> <span class="p">(</span><span class="mi">500</span><span class="p">)],</span>
  <span class="p">[</span><span class="s1">&#39;relu&#39;</span><span class="p">],</span>
  <span class="p">[</span><span class="s1">&#39;batchnorm&#39;</span><span class="p">]</span> <span class="c1"># for last affine layer</span>
<span class="p">]</span>

<span class="n">model</span> <span class="o">=</span> <span class="n">convnetGenerator</span><span class="p">(</span><span class="n">layers</span><span class="o">=</span><span class="n">layers</span><span class="p">,</span> <span class="n">weight_scale</span><span class="o">=</span><span class="mf">0.001</span><span class="p">,</span> <span class="n">reg</span><span class="o">=</span><span class="mf">0.001</span><span class="p">)</span>

<span class="n">solver</span> <span class="o">=</span> <span class="n">Solver</span><span class="p">(</span><span class="n">model</span><span class="p">,</span> <span class="n">data</span><span class="p">,</span>
                <span class="n">num_epochs</span><span class="o">=</span><span class="mi">1</span><span class="p">,</span> <span class="n">batch_size</span><span class="o">=</span><span class="mi">50</span><span class="p">,</span>
                <span class="n">update_rule</span><span class="o">=</span><span class="s1">&#39;adam&#39;</span><span class="p">,</span>
                <span class="n">optim_config</span><span class="o">=</span><span class="p">{</span>
                  <span class="s1">&#39;learning_rate&#39;</span><span class="p">:</span> <span class="mf">1e-3</span><span class="p">,</span>
                <span class="p">},</span>
                <span class="n">verbose</span><span class="o">=</span><span class="bp">True</span><span class="p">,</span> <span class="n">print_every</span><span class="o">=</span><span class="mi">100</span><span class="p">)</span>
<span class="n">solver</span><span class="o">.</span><span class="n">train</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>(Iteration 1 / 980) loss: 2.309418
(Epoch 0 / 1) train acc: 0.121000; val_acc: 0.118000
(Iteration 101 / 980) loss: 1.681039
(Iteration 201 / 980) loss: 1.709945
(Iteration 301 / 980) loss: 1.535179
(Iteration 401 / 980) loss: 2.062533
(Iteration 501 / 980) loss: 1.524193
(Iteration 601 / 980) loss: 1.458269
(Iteration 701 / 980) loss: 1.832951
(Iteration 801 / 980) loss: 1.978657
(Iteration 901 / 980) loss: 2.207330
(Epoch 1 / 1) train acc: 0.549000; val_acc: 0.550000
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[19]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span></span><span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">stats</span><span class="p">[</span><span class="mi">2</span><span class="p">]</span><span class="o">.</span><span class="n">loss_history</span><span class="p">,</span> <span class="s1">&#39;o&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">solver</span><span class="o">.</span><span class="n">loss_history</span><span class="p">,</span> <span class="s1">&#39;o&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;iteration&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;loss&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">legend</span><span class="p">([</span><span class="s1">&#39;No BN&#39;</span><span class="p">,</span> <span class="s1">&#39;BatchNorm&#39;</span><span class="p">],</span> <span class="n">loc</span><span class="o">=</span><span class="s1">&#39;upper right&#39;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[19]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>&lt;matplotlib.legend.Legend at 0x7fe52e9c0790&gt;</pre>
</div>

</div>

<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAA10AAAKvCAYAAACRVqX5AAAABHNCSVQICAgIfAhkiAAAAAlwSFlz
AAAPYQAAD2EBqD+naQAAIABJREFUeJzs3Xt8lNW59//PumEEEgYQTyXsYCKoHWuxJlZ3RKu1CJSS
4CN796kWrdUWfWwMohRrMxTURIsVNOroVn91a2s3PYGQIMhh89QDRtwltdo2j4IQpAHFEzCAhCGz
fn9MTpPMhCRkMpPc3/frxQtyz31YM0mGue7rWtcy1lpEREREREQkMZxkD0BERERERKQvU9AlIiIi
IiKSQAq6REREREREEkhBl4iIiIiISAIp6BIREREREUkgBV0iIiIiIiIJpKBLREREREQkgRR0iYiI
iIiIJJCCLhERERERkQRS0CUiIiIiIpJASQ+6jDF3GmPeMMbsM8Z8aIx53hhzRgeOG2qMCRhjdhpj
PjfG/D9jzKSeGLOIiIiIiEhH9U/2AICLgUeAPxMZz33AGmOMz1r7eawDjDEeYB3wAXAlsBM4FdjT
IyMWERERERHpIGOtTfYYohhjTgR2A1+z1r4aZ5+bgNuBL1pr63tyfCIiIiIiIp2R9PLCGIYBFvi0
nX3ygUrgMWPMB8aYtxvKFFPx+YiIiIiIiIulQnlhE2OMAR4CXrXW/qOdXU8DLgOeA74JnA48BvQD
ShI9ThERERERkY5KqfJCY8zjwERgnLV2Vzv7vQMMALJtwxMwxswCZltrR8Y55oSGc9cAh7p56CIi
IiIi0nsMBLKA1dbaTxJ9sZTJdBljHgUmAxe3F3A12AUcttERYzXwBWNMf2vtkRjHTAR+0z2jFRER
ERGRPuC7wH8l+iIpEXQ1BFxTgUuste934JANwFWttp0J7IoTcEEkw8Vzzz2Hz+fr6lBFOmTWrFk8
+OCDyR6GuIB+1qSn6GdNeop+1qQnVFdXM336dGiIERIt6UGXMeYxIgFUAXDAGHNKw0N7rbWHGvZ5
Fqi11v604bHHgUJjTBnwKHAGcCeR+WDxHALw+Xzk5OR0/xMRaWHo0KH6OZMeoZ816Sn6WZOeop81
6WE9Mu0o6UEXcBORboV/arX9+8CvGv6dCTS1hrfW/tMYMwF4EPgrUNvw7/sTPVgREREREZHOSHrQ
Za09apt3a+1lMbZtBC5MyKBERERERES6ida1EhERERERSSAFXSIJcNVVrfu8iCSGftakp+hnTXqK
ftakL0qpdboSyRiTA2zatGmTJmeKiIiIJNH777/Pxx9/nOxhSB924oknMmrUqLiPV1VVkZubC5Br
ra1K9HiSPqdLRERERNzj/fffx+fzcfDgwWQPRfqwtLQ0qqur2w28epKCLhERERHpMR9//DEHDx7U
2qmSMI1rcH388ccKukRERETEvbR2qriJGmmIiIiIiIgkkIIuERERERGRBFLQJSIiIiIikkAKukRE
RERERBJIQZeIiIiIiEgCKegSEREREekGzz77LI7jkJaWxq5du9o8fumllzJ27Nhuu95dd92F4zhN
f/r160dGRgb5+fls3Lgxat/t27c37ff888+3Odf8+fNxHIdPP/2028YnzRR0iYiIiIh0o7q6On7+
85+32W6M6fZrGWN44okneO6553j22We55ZZb+Nvf/sYll1zCW2+9FXP/u+++O+b2RIxPIhR0iYiI
iEhKs9b2qnN/5Stf4amnnuKDDz7o9nPHMm3aNK6++mqmT5/OnXfeyQsvvMDhw4f5wx/+EHNsb731
FsuWLeuRsUmEgi4RERERSTnBYJCionlkZ48nM/MKsrPHU1Q0j2AwmNLnNsbw05/+lCNHjsTMdrVW
X1/PPffcw5gxYxg4cCDZ2dn4/X4OHz7c5TGccsopAPTv37/NY9/5znc4/fTTY2a7JHEUdImIiIhI
SgkGg+TlTSMQyKOmZi21tcupqVlLIJBHXt60YwqOEnnuRtnZ2Vx77bUdynbdcMMNzJs3j/POO4+H
HnqISy+9lHvvvZerrrqqw9f75JNP+OSTT/joo4/4y1/+wg9/+EMGDRrEt7/97Tb79uvXD7/fz5tv
vqlsVw9S0CUiIiIiKaW4+AGqq28jHJ4ENM4zMoTDk6iunoXfvzAlzx19nWJCoRALFiyIu89bb73F
r371K2bMmMFvf/tbbrrpJv7zP/+T2bNns2zZMl566aWjXsday5lnnslJJ53EKaecQm5uLi+99BLL
li3D5/PFPObqq69WtquHKegSERERkZRSUbGBcHhizMfC4UmUl29IyXO3lJ2dzTXXXMOTTz7Jhx9+
GHOflStXYoxh1qxZUdtvv/12rLW88MILR72OMYbnn3+edevWsXbtWp555hnOOOMMrrzySl5//fWY
xziO05TtWr58eeefnHSagi4RERERSRnWWkKhdJqzUK0ZQqG0LjXASOS5Y/H7/YRCobhzuxrbuI8Z
MyZq+ymnnMKwYcPYvn17h65z8cUXc9lll/GNb3yDa6+9lnXr1uH1ernlllviHvPd735X2a4epKBL
RERERFKGMQaP5wAQL/CxeDwHutTePJHnjiU7O5vp06fz5JNPxpzb1RjcdXer9vT0dC644AKqqqr4
/PPPY+7jOA7FxcW8+eablJeXd+v1pS0FXSIiIiKSUvLzx+E4q2M+5jgvUlBwUUqeO5bGbFesuV1Z
WVmEw2E2b94ctX337t3s2bOHU089tcvXPXLkCAD79++Pu8/06dMZPXo0d911V0Lb8ouCLhERERFJ
MaWls/H5FuE4q2jOSlkcZxU+34OUlNyekueO5bTTTmP69Ok88cQTbbJdkydPxlrLQw89FLV94cKF
GGP41re+1aVrfvrpp7z22muMGDGCk046Ke5+jXO7/vKXvyjblWBtm/eLiIiIiCSR1+ulsnIJfv9C
yssXEQql4fEcpKBgHCUlS/B6vSl5boi92HJxcTG//vWveeeddzj77LObto8dO5bvfe97PPnkk3z2
2WdccsklbNy4kV/96ldceeWVXHLJJR263h/+8AcGDx6MtZba2lqefvpp9uzZ027nxEbTp0+npKSE
N998s9vLHKWZgi4RERERSTler5eysvmUlUUCi+4MCBJ57ljnGj16NNdccw3PPvtsm8d/+ctfMnr0
aJ555hmWLVvGF77wBYqLi/nZz37W4evdfPPNTV+np6czduxY7rvvPq688so2+7a+fuPcruuvv15B
VwIZt9RvGmNygE2bNm0iJycn2cMRERERcaWqqipyc3PRZzJJlI78jDXuA+Raa6sSPSbN6RIRERER
EUkgBV0iIiIiIiIJpKBLREREREQkgRR0iYiIiIiIJJCCLhERERERkQRS0CUiIiIiIpJACrpERERE
REQSSEGXiIiIiIhIAinoEhERERERSSAFXSIiIiIiIgmkoEtERERERCSBFHSJiIiIiPRRzz77LI7j
UFVVleyhuJqCLhERERGRbtIY5LT8c8opp3DZZZfx4osvdumc9913H8uXL+/ymIwxHdrv0ksvxXEc
pk6d2uax7du34zgOixYt6vI43ExBl4iIiIhINzLGUFJSwnPPPcevf/1r7rjjDj7++GMmT57MypUr
O32+e++995iCro4yxmCMYcWKFfzlL39J+PXcpH+yByAiIiIi0h5rbYezNaly7kmTJpGTk9P09fXX
X88pp5zC4sWLmTx5crdfr7uMGjWKYDDIXXfdxbJlyxJ2nbq6Oo477riEfV9TjTJdIiIiIpJygsEg
RXOKyM7JJvP8TLJzsimaU0QwGEzpc8czbNgwBg0aRP/+zTmPBx54gHHjxnHiiSeSlpbGeeedx5Il
S6KOcxyHgwcP8swzzzSVK15//fVNj+/cuZMbbriBkSNHMnDgQE477TRuvvlmjhw5EnWeuro6brvt
Nk4++WQGDx7MlVdeySeffNJmnF6vl1mzZlFeXs6bb7551Oe1bds2/v3f/50TTjiB9PR08vLy2mTz
XnrpJRzH4Xe/+x1+v5/MzEzS09MJBoNNz2vDhg0UFRVx8sknc/zxx3PTTTdx5MgR9u7dy7XXXssJ
J5zA8OHDueOOOzr0eqcaZbpEREREJKUEg0HyJuRRPaaacEEYDGAhsDXA+gnrqVxTidfrTblzt7R3
714++eQTrLXs3r2bhx9+mAMHDnDNNdc07fPwww8zdepUpk+fzuHDh/ntb3/Lt7/9bVasWME3v/lN
AJ577jluuOEGLrjgAmbMmAHA6NGjAdi1axdf/epX2bdvHzfeeCNnnnkmtbW1/PGPf+TgwYMMGTIE
iGTzCgsLGT58OPPnz6empoYHH3yQwsJCFi9e3GbsM2fOZNGiRcyfP7/dbNfu3bvJy8vj0KFDzJw5
k+HDh/Pss8+Sn5/P0qVL28wNu+eeexgwYACzZ89uk+m65ZZbGDFiBHfffTevv/46Tz31FMOGDeO1
117j1FNP5d5772XlypU88MADfPnLX2b69OnH8N3peQq6RERERCSlFN9THAmKxoSbNxoIjw5Tbavx
l/gpW1CWcuduZK3lG9/4RtS2gQMH8vTTT3PZZZc1bdu8eTMDBgxo+rqwsJBzzz2XRYsWNQVdV199
NTfeeCOnnXYaV199ddQ5f/KTn7B7927eeOMNzj333Kbt8+fPbzOmk046KaqRR319PY888gjBYLBN
kDl48GBuvfVW5s+fz5tvvslXvvKVmM/zvvvu46OPPuLVV18lLy8PgB/84AeMHTuW2267rU3QVVdX
R1VVFccdd1ybc40YMYIXXngBgJtuuonNmzfzi1/8gptvvplHHnkEgB/+8IdkZWXx9NNP97qgS+WF
IiIiIpJSKtZVEB4djvlYeHSY8nXlKXnuRsYYHn/8cdatW8e6dev4zW9+w9e//nVuuOGGqMxRy4Br
z549fPbZZ1x88cUdau9urWX58uUUFBREBVzxxtOYJWt08cUXU19fz/bt22MeM3PmTIYNG8Zdd90V
97yrVq3i/PPPbwq4ANLT05kxYwY1NTX84x//iNr/uuuuixlwGWOiSiYBLrjgAgC+//3vN21zHIfz
zjuPrVu3xh1TqlLQJSIiIiIpw1pLqF8oUvYXi4GQE8Jam1Lnbu2rX/0ql112GZdddhlXXXUVK1as
4Etf+hKFhYVN861WrFhBXl4egwYNYvjw4Zx88sk8/vjj7N2796jn/+ijj9i3bx9f+tKXOjSezMzM
qK+PP/54AD777LOY+w8ZMoRbb72V8vJy/vrXv8bcZ/v27Zx55plttvt8vqbHW8rKyoo7vlGjRkV9
PXTo0JjjHjp0aNwxpzIFXSIiIiKSMowxeOo9EC/useCp93Sp610iz92Ra1966aXs2rWLzZs388or
rzB16lTS0tJ4/PHHWbVqFevWrePqq6/uUNDX2cCwX79+nT7PzJkzGTp0aLvZrs4YNGhQ3MfijS/W
9u4Iinuagi4RERERSSn54/Nxtsb+mOq851BweUFKnvtoGjNc+/fvZ+nSpQwaNIjVq1dz3XXXMXHi
RC677LKYAUWsIPDkk09myJAh/O1vf0vYeBuzXcuXL4+5btepp57KO++802Z7dXV10+MSoaBLRERE
RFJK6dxSfJt9OFuc5qyUBWeLg2+LjxJ/SUqeuz1Hjhxh9erVHHfccfh8Pvr164cxJqq1e01NTcxF
kNPT09mzZ0/UNmMMV1xxBRUVFR2aA9ZVt956K0OHDuXuu+9uE/xNnjyZN954g40bNzZtO3DgAE8+
+STZ2dmcddZZCRtXb6PuhSIiIiKSUrxeL5VrKvGX+CmvKCfkhPCEPRSML6DksZJjaumeyHM3stay
cuXKpozP7t27+c1vfsN7773HnXfeyeDBg5kyZQqLFi1i4sSJXH311Xz44Yc89thjnH766bz11ltR
58vNzWXdunU8+OCDZGRkkJ2dzfnnn8+9997L2rVr+drXvsaMGTPw+Xzs3LmTP/7xj2zYsCGqZXy8
cR7NkCFDmDlzJnfddVeboOsnP/kJixcvZtKkSRQVFTF8+HCeeeYZtm/fztKlSzv1evV1CrpERERE
JOV4vV7KFpRRRhnW2m6dZ5XIc0MkCzVv3rymrwcOHMgXv/hF/uM//oMf/vCHAFx66aU8/fTT/Pzn
P2fWrFlkZ2dz//33s23btjZB16JFi7jxxhuZO3cun3/+Od/73vc4//zzycjIYOPGjcydO5f/+q//
Yt++fYwcOZLJkyeTlpYWNZ544+zItltvvZWysrI2DT5OPvlkKisrueOOO3j00Uc5dOgQY8eOZcWK
FUyaNOmo5+3IY92xfyowbogsAYwxOcCmTZs2kZOTk+zhiIiIiLhSVVUVubm56DOZJEpHfsYa9wFy
rbWJq89soDldIiIiIiIiCaSgS0REREREJIEUdImIiIiIiCSQgi4REREREZEEcmXQ5ZbmISIiIiIi
knyuC7qmTLmJzMwryM4eT1HRPILBYLKHJCIiIiIifZjrgq5dux6ntnY5NTVrCQTyyMubpsBLRERE
REQSxnVBF5imv8PhSVRXz8LvX5jUEYmIiIiISN/lwqArWjg8ifLyDckehoiIiIiI9FH9kz2A5DOE
QmlYazHGHH13ERERETlm1dXVyR6C9FGp+LOloAuLx3NAAZeIiIhIDzjxxBNJS0tj+vTpyR6K9GFp
aWmceOKJyR5GE9cHXY7zIgUFFyV7GCIiIiKuMGrUKKqrq/n444+TPRTpw0488URGjRqV7GE0cWHQ
ZZv+dpwX8fkepKRkSVJHJCIiIuImo0aNSqkPxCKJ5rqga8SIm3GcL+DxHKSgYBwlJUvwer3JHpaI
iIiIiPRRrgu6Vqx4nHPPPVdzuEREREREpEckvWW8MeZOY8wbxph9xpgPjTHPG2PO6MTx3zHGhI0x
SztxTNcGKyIiIiIi0klJD7qAi4FHgAuA8YAHWGOMGXS0A40xpwK/AF5O6AhFRERERES6KOnlhdba
yS2/NsZcB+wGcoFX4x1njHGA54CfAV8DhiZulCIiIiIiIl2TCpmu1oYRaTH46VH2mwfsttb+Z+KH
JCIiIiIi0jVJz3S1ZCKTrR4CXrXW/qOd/cYB3wfO6amxiYiIiIiIdEVKBV3AY8BZwLh4OxhjBgO/
Bn5orf2spwYmIiIiIiLSFSkTdBljHgUmAxdba3e1s+to4FSgwjS3IXQaznEYONNauy3ewbNmzWLo
0OjpX1dddRVXXXXVsQxfRERERERS0OLFi1m8eHHUtr179/boGIy1tkcvGHMQkYBrKnCJtXbrUfY9
DhjTanMpMBgoAjZba4/EOC4H2LRp0yZycnK6Z+AiIiIiItLrVFVVkZubC5Brra1K9PWSnukyxjwG
XAUUAAeMMac0PLTXWnuoYZ9ngVpr7U+ttYeBf7Q6xx7AWmure3DoIiIiIiIiR5X0oAu4iUi3wj+1
2v594FcN/84E6ntwTCIiIiIiIt0i6UGXtfaobeuttZcd5fHvd9+IREREREREuk8qrtMlIiIiIiLS
ZyjoEhERERERSSAFXSIiIiIiIgmkoEtERERERCSBFHSJiIiIiIgkkIIuERERERGRBFLQJSIiIiIi
kkAKukRERERERBJIQZeIiIiIiEgCKegSERERERFJIAVdIiIiIiIiCaSgS0REREREJIEUdImIiIiI
iCSQgi5xLWttsocgIiIiIi6goEtcJRgMUlQ0j+zs8WRmXkF29niKiuYRDAaTPTQRERER6aP6J3sA
Ij0lGAySlzeN6urbCIfnAwawBAKrWb9+GpWVS/B6vUkepUjvZa3FGJPsYYiIiKQcZbrENYqLH2gI
uCYRCbgADOHwJKqrZ+H3L0zm8ER6pWAwSNGcIrJzssk8P5PsnGyK5hQpeywiItKCgi5xjYqKDYTD
E2M+Fg5Porx8Qw+PSKR3CwaD5E3II7ArQE1BDbVTaqkpqCHwQYC8CXkKvERERBq4NuhSEwV3sdYS
CqXTnOFqzRAKpennQqQTiu8ppnpMNeEx4ZbJY8Kjw1SPqcZf4k/q+ERERFKF64Ku++//DzVRcCFj
DB7PASBeUGXxeA5oPopIJ1SsqyA8OhzzsfDoMOXrynt4RCIiIqnJdUHX738/lpqatdTWLqemZi2B
QB55edMUeLlAfv44HGd1zMcc50UKCi7q4RGJ9F7WWkL9Qu0ljwk5IWWPRUREcGHQZe2FqImCO5WW
zsbnW4TjrKI542VxnFX4fA9SUnJ7Mocn0qsYY/DUe9pLHuOp9yh7LCIigguDrljURMEdvF4vlZVL
KCzcSFbWBEaOnEpW1gQKCzeqXbxIF+SPz8fZGvu/Eec9h4LLC3p4RCIiIqnJuKX0wxiTA2yCTUBO
m8dHjpzKjh3LdFfWRbSmkMixaexeWD2mOjK3K7L0Hc57Dr4tPirXVOpmhoiIpKSqqipyc3MBcq21
VYm+njJdgJoouJO+3yLHxuv1UrmmksKMQrIqshi5YiRZFVkUZhQq4BIREWmhf7IHkArUREFEpGu8
Xi9lC8ooo0zZYxERkTjcl+nyXg4DioAgkSYKK9VEQUSkGyjgEhERic19QddVn8KVj8DgkfTr9yUK
C99QEwUREREREUkYd5YXnglwgLO3eikrm5/kwYiIiIiISF/mvkxXozPCfHpoV7JHISIiIiIifZx7
gy4Dnx7cg1ta5ouIiIiISHK4N+iycGhPSBO/RUREREQkodwbdL3rMDA8QpkuERERERFJKHc20njH
gQofJww/UZkuERERERFJKPcFXYtHwOF/xxz+Gldc/3ayRyMiIiIiIn2c+4KuYAWOsxvfWQ9SUrIk
2aMREREREZE+znVzukaMuJnCwo1aEFlERERERHqE6zJdK1Y8Tk5OTrKHISIiIiIiLuG6TJeIiIiI
iEhPUtAlItJAS0iIiIhIIrgu6Jpy9RSK5hQRDAb1AUtECAaDFM0pIjsnm8zzM8nOyW56jxARERHp
DsYtgYcxJgfYxAwwBwz9V6Vx4oBLGDCgjvz8cZSWzlZjDRGXCQaD5E3Io3pMNeHRYTCABWerg2+z
j8o1lXpfEBER6YOqqqrIzc0FyLXWViX6eq7LdAHY0y2hiZ+z69Mx1NSsJRDIIy9vmu5si7hM8T3F
kYBrTEPABWAgPDpM9Zhq/CX+pI5PRERE+gZXBl0AnBGGtHLAEA5Porp6Fn7/wmSPSkR6UMW6ikiG
K4bw6DDl68p7eEQiIiLSF7k36DLAwBAQKa8MhydRXr4hahe3lF6KuJG1llC/UHOGqzUDISek94EE
0+srIiJu4N6gywKHPLSsKQqF0ti3bx9FRfPIzh5PZuYVZGePp6honkoPRfoYYwyeek/jfZe2LHjq
PRgTLyqTrlLzEhERcRvXLY7c5F0HDha02BCmX7+9XHjhv1FdfRvh8HwaZ9UHAqtZv34alZVLNKle
pA/JH59PYGsgZomh855DweUFMY6SYxHVvKSguXlJYGuA9RPWq3mJiIj0Se7LdK0G/j9gxTCo+xEM
KILjs2HEyeyq28jf3xtEODyOlhkwzfkS6ZtK55bi2+zD2eI0Z7wsOFscfFt8lPhLkjq+vkjNS0RE
xI1c2TKeEcDfDaw5DqaE4PTmu62860CFD/ZXAi3vtlqysiawbdvaJIxeRBIlGAziL/FTvq6ckBPC
E/ZQML6AEn+JMi4JkJ2TTU1BTey5dBayKrLYtmlbTw9LRERcpqdbxruzvNAAH1nIr4PTW20/MwxU
w1I/1JVFPRgKpWGt1RwPkT7E6/VStqCMMsr0+51gnWleou+DiIj0Je4rL2z0PjAmzmNN7eRbsng8
B/RBQKQP0+93Yql5iYiIuJU7gy4LHEe7d1tbtpMHcJwXKSi4KPFjExHpw/LH5+Nsjf1fj5qXiIhI
X+XOoMsAh2n3bmtzO3mL46zE53uQkpLbo3dzyXw4EZHuouYlIiLiRu4MugBGAVviPPaugYP1wFTg
Ir785Yeb2sVrfRkRka7zer1UrqmkMKOQrIosRq4YSVZFFoUZhWoXLyIifZa6F34rFJnDFbN74WCA
pq6FUevLjG4+xtnq4Nvs0wcGEZFOUtMMERFJBnUvTLSlx0G9AwdnQN0dsHQBpD0FA4dHSgoPFkBd
CS3bxTd2LYxaX6ZR4/oyNrK+TNmCsrbXPAb6QCIifZne30RExA3cV1748Vj4bEJDO/iMyN+fXQi7
3ofPtjVsj16fq7FrYcW6ikiGK4bw6DDl61p3POyaYDBIUdE8srPHk5l5BdnZ4ykqmqcSRhERERGR
Xsh9mS6+AHxMpJaw8Q7rOGANMKnN3o1dC3tqfZlgMEhe3jSqq28jHJ5PYw1jILCa9eunNc0tExER
ERGR3sF1ma6srA+AT4FVLbbOBhY1bGtup+U4q5q6FvbU+jLFxQ80BFyTaI7wDOHwJKqrZ+H3Lzym
84uIiIikKrf0GhD3cV3Q9atfLeL667+J4xQCFUSiKC/wR+C3eDxjGTEin6ysCRQWbqSycgkARUXz
+OSfR2Bz7PN21/oyFRUbCIcnxnwsHJ5EefmGY76GiIiISKpQZ2hxA9eVF6anp/PLXy7ioYfuwu9/
gPLyhwmF0vB4DlJQMI6SkkcZPHhwU8Yqutzvdii/EPKrozoeOu81rC/z2LGtL2OtJRRKp70axsam
Hj0x+VxNPERERCSRojpDFzR/tgpsDbB+wnp1hpY+w3VBVyOv10tZ2V2UlbUNLlqmtqPL/Yi0kl/q
h7RyGBjEe1w93//f11LyWMkxvykYY/B4DhA936yl5qYeiRIMBikufoCKig2EQul4PAfIzx9Haels
vemJiIhIt0pGZ2iRZHBdeWEsxpi4qe3ly19qVe7nbeh4uA127eYEcx5lC8q6LSDJzx+H46yO+Vhj
U49EaczqBQJ51NSspbZ2OTU1awkE8sjLm6Y0v4iIiHSrnuoMLZJsrs10tdReatsJpgP7iW4j38jp
9nK/0tLZrF8/jepq26KZhsVxXmxo6rGkW64TS5usHtDcxMPi9y+krGx+wq4vIiIi7tFTnaFFUoEy
XbRKbTc3DCQ8OsyRSUEY4I9zZPeX+3m9Xiorl1BYuJGsrAmMHDk1qqlHIkv81MRDREREekpPdYYW
SQXKdNF9/cBwAAAgAElEQVSQ2i6IndrmDCD9dw2LJkdLVLlfZL7Z/JjzzRIl1Zp4iIiISN+XPz6f
wNZAzBLD7uoM7Qb6fJb6XJ3p2rlzJ2PHTqDmg3+2m9ruP3gPxqwk3hpeidRTv0DRTTxiSXwTDxER
EXGX0rml+Db7cLY4LT9m4Wxp6AztP7bO0H2ZWu33LkkPuowxdxpj3jDG7DPGfGiMed4Yc8ZRjvmB
MeZlY8ynDX/WGmO+2pnr7ty5k9NOu5S3374VDv1Lu6ntjOGncMstb/R4uV9PS2YTDxEREXEfr9dL
5ZpKCjMKyarIYuSKkWRVZFGYUah28e1o7EcQ2BWgpqCG2im11BTUEPggQN6EPAVeKcgke+VvE0kh
LQb+TKTc8T7gbMBnrf08zjG/BjYArwGHgJ8A/ws4y1q7K84xOcCmTZs2kZOTwznnTOStt2YCk2FA
EVwZgDNjpLa3OBRmFDa1K+3L6dvmNclmxWzi0deCTBEREUktfflzVncqmlNEYFcgutV+g9afXSW2
qqoqcnNzAXKttVWJvl7Sg67WjDEnAruBr1lrX+3gMQ7wGfAja+1zcfaJCrr69z+b+vq3iQQWQRic
F3fRYzfdaQkGg/j9Cykv39Bq0ejbXfMaiIiIiKSy7Jxsagpq4i3rSlZFFts2bevpYfUqPR10pWIj
jWFEiv0+7cQx6YCno8eEw2GsHUbzT6q31aLHIaj7mB/dMIPSx0pdFWwko4mHiIiIiHSMWu33TikV
dJnIT8ZDwKvW2n904tAFQC2wriM7O46DMXuIxHYtAq+6soYuhWH69RvLw/c/3Ikh9D36RRURERFJ
LVGt9uNkutRqP/WkVNAFPAacBYzr6AHGmJ8A3wYusdYePtr+s2bNYujQoaSl7SYY/FfgFOCqhj+N
VnH22f/SuZG3orsLIiIiIpIIarXfOYsXL2bx4sVR2/bu3dujY0iZOV3GmEeBfOBia+37HTxmNvBT
4BvW2r8cZd+oOV2N3Qvr6h4EJtM0kYuVDBgwi61b/0RGRgbQ8QAqGAxSXPwAFRUbCIXS8XgOkJ8/
jtLS2a4qURQRERGRxGnsXlg9pjoSeLm4H0FX9fScrqS3jIemgGsq8PVOBFw/BoqBiUcLuGLJyMhg
69Y/cc45j9C//1gc5yL69x/LOec8wtatf8Lr9VJUNI/s7PFkZl5BdvZ4iormxW3B2dj5LxDIo6Zm
LbW1y6mpWUsgkEde3jS17hQRERGRbqFW+71P0jNdxpjHiNT2FQDvtnhor7X2UMM+zwK11tqfNnw9
B7i74bjXWhyz31p7IM51ojJdrYXDYRwnEoM2t06/jXB4Is2t01fj8y2K2Tq9qGgegUBeQ6v1RpFi
W8dZRWHhRsrK5nf0ZRERERER6RBNa+k8N2a6bgKGAH8Cdrb48+0W+2QCX2jx9f8h0q3wj62Oub2r
g2gMuACKix9oCLga16oCMITDk6iunoXfv7DN8RUVGxoCtCAwDxgPXAGMJxyuZNmyl7o6NBER6cWS
fXNTRPo+BVypL+lBl7XWsdb2i/HnVy32ucxae32Lr7PjHHN3d4ypOYBqKxyeRHn5htbPgVAoHdgP
TAPygLXA8oa/L2Tnzp3s27evO4YnIiIpLhgMUjSniOycbDLPzyQ7J5uiOUUqNRcRcamkB12ppjmA
ir/4QSiUFnXn0hiDx3MA+AVwGxCdIYNJHDmykLlzFyVw5ImlO7UiIh3TOME9sCtATUENtVNqqSmo
IfBBgLwJeQq8RERcSEFXK80BVLwgw+LxHGiTxs3PHwf8NxA7QwbfapMhS3XBYLBTzURERASK7ymO
dBQbE466/xYeHaZ6TDX+En9SxyciIj1PQVcM+fnjcJzVMR9znBcpKLiozfaSktvp3x86kyFLZerG
KCLSNRXrKmKunQORwKt8XXkPj0hERJJNQRdtS+dKS2fj8y3CcVbRnPGyOM4qfL4HKSlp269jyJAh
ZGQMoLMZslTVlWYiIiJuZ60l1C/U3v03Qk6o19yAExGR7uHaoKu9Sc5er5fKyiUUFm4kK2sCI0dO
JStrAoWFG2O2i280derFnc6QparONhMREZGGEvV6T3v33/DUe3rNDTgREeke/ZM9gGSIWsW7oHkV
78DWAOsnrG9aVK6sbD5lZR1f+6C0dDbr10+jutq2yBBZHOfFhgzZkkQ/tW7RmWYi+uAgIhItf3w+
ga2BmCWGznsOBZcXJGFUIiKSTK7MdHV2knNHA4uuZshSTVebiYiICJTOLcW32YezxWlZoY6zxcG3
xUeJvySp4xMRkZ7nyqArkZOcGzNk27atZceOZWzbtpaysvm9JuBq1JVmIiIi0nADbk0lhRmFZFVk
MXLFSLIqsijMKGyqpBAREXdxXXlhZyY5N2ZyulpG15FjUrVEr6+USoqIJIPX66VsQRlllKXs+7yI
iPQc12W68r+bzwf//OCok5z3798ft9HGseoN61/1lVJJEZFkU8AlIiLGLW1rjTE5wCZmAO8A/wKc
3nY/Z4vDdUOvY9mKCj4d91Fkn4ZGG85WB99m3zGVhzSufxVpxz6R5gzSany+RSkb0OhOrYikMr1H
iYhIZ1RVVZGbmwuQa62tSvT1XJfpAuBCoBLYTJtJzme+eyZLl67m03Efwxl0qNFGZ/TW9a/0YUZE
Uk17S3+IiIikEndmujKAOuA1YAf0O9KPzBMzKRhfQN3eQTzx+2eg6MPY874sZFVksW3Tti6NIzt7
PDU1a4l38qysCWzbtrZL5xYRcYuopT9Gh7u1IkFERPq+ns50ua6RRpMBwNcj/zyl4hS2/s9WjDFk
ZX0DBvbvVKONjtL6VyIi3SNq6Y9GjRUJNlKRULagLHkDFBERacGd5YUtWTgufBzGGKy1HDkyGA55
jtpoo2VQ1NFsoda/EhHpHolc+kNERKS7uT7oct5zKLi8AGgRFB3Mh3fjvDTvQsHlBV3uQKj1r0RE
jk1nlv7oaW4p2RcRkc5xb9DV0DjDt8VHib+kaXN+/jjM4UuhwgfvOFGNNnjHYfhrJ3HHzDvIy5tG
IJBHTc1aamuXU1OzlkAgj7y8ae0GXqWls/H5FuE4q2h5csdZ1bD+1e0JesIiIn2DMQZPfecqEhJJ
DT1ERORoXNdIY8QXR+AMdvCEPRSML6DEXxI12bqxpfs//nEj9riXIa0cBoag7gjDBx7H2//zOj//
+RMEAnkNHQijOc4qCgs3UlY2P+7crGAwiN+/kPLyDYRCaXg8BykoGEdJye2a+C0i0gFFc4oIfBCI
WWLobHEozCjskTldaughItI79XQjDdcFXZs2beLcc89t9w5o66Cof/8DTJ16UVNQ1H4Hwn14vRdx
wgknEwql4/EcID9/HKWls2P+x6umGSIinRc32HkvUsHQU8FO0ZwiArsC0Q09GvRk8CciIp2joCtB
WgZdOTk5MfeJFQC13matJTPzCmprl9E26NoH/BswE5hMb1n4WESkNwoGg/hL/JSvKyfkhOJWMCRS
dk42NQU1CVliREREEkct43tYMBik+J5iKtZVEOoXwlPvIX98PqVzS/F6vVEBV+O+HxxeAyMyI10O
D06EumHAn4FPgXuAb7W4QuPCxxa/fyFlZfN79PmJiPRVXq+XsgVllFGWlKqBzjT0UEWDiIi7uTro
iipPKWguTwlsDbB+wvqo8pSofW8Og6mNTOJ+9wmoOBX2vwVcSSTD1VY4PIny8kWUqcpERKTbJSOo
iWroESfT1ZMNPUREJHW5t3shrRbXbPw/sXFxzTGRxTWPti9nAvk7YMBcoGMLH4uISN+QPz4fZ2vs
/0pbLkkiIiLu5uqgqzOLa7a3L2eEI10O0cLHIiJuUjq3FN9mH86W6CVGYi1JIiIi7uXaoKsjtfh1
pg5rLfv27eOj/Z+0uy8DQ8CFgBY+FhFxC6/XS+WaSgozCsmqyGLkipFkVWRRmFGodvEiItLEtXO6
OlKL//E/P2PXrl1MmHAdBz5OAxuMuy+HPMCPgWkNGybR3L3wxYaFj5ck6umIiEiSJLuhh4iIpD7X
ZrogUotvtsT5z/Fdh9DeCUye/H2qq2+Dg9+Gd+O8XO86cLAA8AJLgI3ARaSnf52srAkUFm5Uu3gR
ERdQwCUiIrG4NtMFkVr8/8h6mlD488i8rIbuhbzrQIUPDv2av/3tQsLhiVA3DirWA9Wt9gUq/gXq
7mk462Ac53x8vtd47bU/MmTIkCQ9OxERERERSQWuDroGDx7MiQMuYdfSMZFGGANDDWtvFUBdCZCO
tcOIRFhe2F8JS/0N+9bBoc/g4NehbiyRssI04BOGDQuyZs0qBVwiPUQlXSIiIpLKXF1eaIxhwIA6
qHsIPtsGu3bAZ28BFo4fCyNGER72BgwoAoKAF+rK4LOtsOsH8NlSqFsJ/BxYCywDXmXPnp+zYMGT
SXxmIn1fMBikaE4R2TnZZJ6fSXZONkVziggGg8kemoiIiEgU12a6Gu+M5+ePIxBYTTg8CdgPg/Og
oBpOb1lCGICKdbC/APgzkfW43gPuanXWyAFaCFkksTqzsLmIiIhIsrku03V/2f1Rd8YP9/uQM864
H8dZBQOKIwHXGa0XQA5DfjUMqAbWEMlojaZ5pyAwDxgPXAFczkcffcK+fft6+NmJuENnFjYXEZHk
szbeOqYi7uC6oOv3H/2emoIaaqfUUlNQw1OfPIUZ8gEzZrxMvyFPRTJcrdUBtcDgF2DEKDj+NBhQ
BewjEnBNA/KIlBguB9Zy4MA9XHjhv6nUSSQBOrOwuYiIJIfKwEWaua680GbaNnfG37HvMN57gC+c
egK1pjb6gDrgd0Riqq/Xg6ltKDk0UDEW9n8HuI3Iulw0n5hvUV3t4PcvpKxsfsfHp4YAIu3qyMLm
ISek3yURkSRSGbhINNdlumIJjw5T8d8VzYslt/QakYDrdFqVHFrI3w4DngUmxj5veBLl5RuOev1g
MEhR0Tyys8eTmXkF2dnjKSqapztBIjFELWweiwVPvUcBl4hIEqkMXCSagi5oujOePz4fZ2url+R9
YEyc484A0vbQ3i33UCit3TrmYDBIXt40AoE8amrWUlu7jJqatQQCeeTlTTvmwEs11NIXxfxdbeC8
51BweUEPj0hERFpSGbhINAVd0HRnvHRuKb7NPpwtTuQuugWOo90yJgaGgdhvKmDxeA60e8e9uPgB
/vGPmwh7Vkbmio3IhONPI+xZyd//PgO/f2Gnn44yZ9LXtfldBbDgbHHwbfFR4i9J6vhERNysM2Xg
Im7hujldsTTeGfd6vVSuqcRf4qe8opyQE+KDPR9Qb+tjv3FYcA5bcFYTDn+z7XmdFykouKjday9f
/hI2fUlzm/rDwAZg6yMQfpzA4n7YAZ9SOre0Q7XPjZmz6urbCIfn01hEHQisZv36aVRWLlENtfR6
sX5XPWEPBeMLKHmsRD/jIiJJFFUGHufzk8rAxW2MW+4yGGNygE3mmwZ7vm2a0Om8F7kzHmtCp7WW
mXfMJPBBIGaK3LxruP7463n9T+9TXT2rYa2vyIkd50V8vgfbDXKstXhPGs2BidsjbepbNu0YQ/MY
tzr4NsceY2tFRfMIBPIaxhLNcVZRWLixU409RHoDNc0QEUktRXOK4n5+crY4FGYUUrZAC5pK8lRV
VZGbmwuQa62tSvT1XBd0fefa7/D6316PvjPuj39nPKr7zuhwm2DttdWvYYzB719IefkGQqE0PJ6D
FBSMo6Tk9qMGSf1PHkT9zYci5/2/wL8QadrRSus3qHgfMrOzx1NTs5Z4t5aysiawbdvadsckIiIi
ciyO9vlJ3Qsl2Xo66HJdeeGPZ/6YnJycTt0Zv+icKby/dC8H+QQGhEnrN5BTTxrDvt2DOeusa/B4
DpCfP4633lrK4MGDO3xeay0Dh3k4YA5FNrwPXBp73/DoMM8vex77+TAqKjYQCqU3Xbe0dDZerzdS
Qx1KpyONPZQVEBERkURRGbhINNcFXY06EnREz4+6j0gws5cgk/jbdj8wmWOZM2WM4YT04zlgGxpc
HKVpxz8/3sWjj/4r1s6Pe12P5wDtFVEfrbGHiIiISHfwer2ULSijjDLd8BXXU/fCdhQXP9AQcDXO
1QJYBMwDvtVimyEcnkR19ayY3QbbK+GcevnUSOtrQ6SJRjtrD9mDw7H2m+1eNz9/HI6zOuYpOtLY
Q0RERKS7KeASt1PQ1Y6Kig2Ew60XPn6FjiyG3NG27VGtrzOBLXEG8y5w8DtHvW5p6Wx8vkU4zipa
9tJ2nFX4fA9SUnL70Z62iPQibpmXKyIi0psp6Ioj9vyofURaDLY/Z2rfvn2tFjxeHnfB48aa58KM
Qvr9fQCs7A/vELX2EO84UOGFunhrDzXP1fJ6vVRWLqGwcCNZWRMYOXIqWVkTKCzcqHbxIn1EMBik
aE4R2TnZZJ6fSXZONkVzirQWn4iISIpy7ZyuozHGxJgf1Vg62P6cKb9/YYuyxKYzNpQCWvz+hVFt
2xtrnu3nw3jkkbGw9GVIK4eBITjkgYMFULcRGBxntNFztbxeL2Vl8ykrUyttkb4mqiNYQXNHsMDW
AOsnrFdHMBERkRSkTFc72s6P2gB8A4g9ZwpeoKDgojhliREtSwFbKym5nS996Qmc0CT4bCvs2gGf
bcUJTWL48M9xnBdjHtfeXC0FXCJ9S/E9xZGAa0y45fROwqPDVI+pxl/iT+r4REREpC0FXS20nBth
rW01PyoMpAM/JtJMI3rOFKyif//bufvuWR1u2w7Rc7/OOusagsHDnH32Q5x66nhGjryiqTTw7bcj
c7I0V0uk56TifKmKdRUxFxuFSOBVvq68h0ckIiIiR+P68sJgMEhx8QNUVGygrm4A+/fvAI5j8OAR
DBjwORMnnsfFF7/Ciy8uYseOD6mvHwwsIVJquAhIAw4CF5KRMYKhQ4d2uG17dEv6+TTWCf3zn6vx
+Rbx2mu/ZsiQIU1HVlYuaViEeVGrRZg1V0ukuwSDQYrvKaZiXQWhfiE89R7yx+dTOrc06b9n1lpC
/ULtLi0RckIqKxYREUkxrg66ooOe24F/AxYAkwgGIwHQU09FAqC33lpKcfEvCARWN8zVmt9wlkhw
5TiruOKKyIec/PxxLfaL1rIUMLolfaPmuV9z5y5qO/dLc7VEEibV50sZY/DUe9q7p4On3qP3BhHp
VvrMIXLsXF1eeOed97cIehYCtwHx18EqLf1xjHbstCnx62jb9q7O/YLmuVo9Xf6UiuVWIt2lN8yX
yh+fH1nbLwbnPYeCywt6eEQi0hepS6pI93Jd0PXRRx9xzrhz6P+F/gSWlxA+fgqknQP8N0dbf6uj
7dg7sl/slvQtRc/9aqmja4B1l2N541WQJr1Jb5gvFbW2X4tppc4WB98WHyX+eEtLiIh0TGPWP7Ar
QE1BDbVTaqkpqCHwQYC8CXkKvES6wLjlQ7ExJgfY5DneQ2hyCMbQVDrEFqDCgX07gIyYx48cOZUd
O5ZFpdc7mm6Pt1929nhqatYSr04oK+tytm1bF7U1uiRyYtOTcJxIGWR3r8UVVW41urncytnq4Nvs
i1lu1XKeXCiUjsdzgPz8cZSWzk76nBiReKy1ZJ6fSe2U2rj7jFwxkh1v7Eh6mU0wGMRf4qd8XTkh
J4Qn7KFgfAEl/hL9jonIMSuaU0RgVyCS9W/F2eJQmFFI2YKyJIxMpPtUVVWRm5sLkGutrUr09VyX
6Qr9awhOJ6p0iNOBKWFImxznqOh1sBp19INXvP3atqRvFq8NfPQ8sNhlkN2ps+VWjUFhRxaGlvjc
cjMklUTNl4olheZLNa7tt23TNna8sYNtm7ZRtqBMAZeIdIvekPUX6W1cF3SRGWf76cCgt2M+1N46
WF3VtiV9x9rAH8s8sK7o7BtvTweFfUlPl41KW71xvlQqBIEi0nd0pkuqiHSc+4KueAwwKAysIFHr
YLX+UD127P/iootymDHjlXbniDU6lnlgXdGVN97OBIV6w26mDGFq0HwpEXG73pT1F+lNXN0yPooF
Dhm83p8C8xvW6TrUbetgxVuTq2VL+sGDB7f7JmaM6fAaYN2hs+2pOxIU1tUdR1HRz6ioeE3zvVo4
2vIBfv/CqOUDJDG8Xi+Vayoj86UqWs2XekzzpUTEHfLH5xPYGohZ6ZKqWX+RVOe6Rhp8E7ggxg7v
wjnbz+HNV98Eun9NiqKieQQCeXHW7lpFYeHGDn2o7q7zdFTRnCICH8R5440xmbb95iD78HjOo77+
4R5pAtKbHL2pygS2bVvb08NyPa1NIyJuFLeJ1nuRrH+y1ywU6Q5qpJFgntc98C5RpUO8CwPWDWDl
71c27dfdH7S6ay5W7Hlg4W4tg4y6XifLrdprDgK3EAo9pPlerfR02ah0nAIuEXGjxqx/YUYhWRVZ
jFwxkqyKLAozChVwiXSR64KuisUVnLP9HPo/0R/nPx36P9Gfc7afw9a/bCUjIwNrbbd/uO3OD9WN
a4DNmPEyXu859Os3ln79LiY9fS4XXZTbreNuul4n3njbaw7i8Wwisvh0W4loAtJbRJeNxtK9ZaMi
IiJHoy6pIt3LdUHXSSedxJuvvkloV4jQ1hChXSFeWfUKd//iboZkDcMzahCek9MZcnImN930k7gN
DDoTmCXiQ/Urr2ziwIH7qa//K/X1GwgG/4ennrokIU0XOvPG23ph6BEjvoXXew5paX7q64ehbE5s
XVk+QEREpCfopp/IsXNd0NWS4zgEg0EuGH8BT+x+guB1e6n/QR31P/qc4PidPPFfv+X886c2BTHH
0tK7Oz9UJ7Mte0feeL1eL2Vl83nrraUMHx7iwIH72b//z4TDA1E2J7auLB8gIiIi0hPcelO8O7k6
6IKGxX9Pr4YziF4w+cwwTNnB/6vx4vcvPOaW3t35obqn1+rqqrbB4ThA2ZxYWmcIj7Z8gIiIiEgi
BYNBiuYUkZ2TTeb5mWTnZFM0p0jL2HSR61vGV6yrgHidT88Iw6C3KC8/iLX2mFp6N36o9vsXUl6+
iFAoDY/nYKdb0ndmfliys0aR4HB+iy2zgWlEgs7GQMziOC82BJ5LkjDK1NGYISwrU9c8ERERSZ6o
DpYFzR0sA1sDrJ+wXg1VusDVma6OLP7LwBCHDw/qluxS44fqbdvWsmPHMrZtW0tZ2fyYP7Tx0riJ
mB+WiJRx7ODQCywBNgITcJyLlM2JQwFX76Tyi47R6yQiktqK7ymOBFxjwlGVYOHRYarHVOMv8Sd1
fL2Rq4Oujqy6ziEPHs+Bbm/pHetDdUfnjHXH/LBjmZ/WEfGDQy8wH1hDZuaAdgNPkd5A5Rcdo9dJ
RKT3qFhXEXONVogEXuXrynt4RL2f68sL88fn8+iWR7GntwoOLPCuA5+PZeo151Je/mrDxtiL1x5r
E4jGOWOREsb5NOZxA4HVrF8/LSoTVFo6m/Xrp1FdbVvMl+p4mV7sa4UJBNa0udaxPJ8hQ/oBK4Fv
tXnccV5k6tSLj+kaIsmm8ouO6Y2vk0p8Rfoe/V53TEcqwUJOSK9nJyU902WMudMY84YxZp8x5kNj
zPPGmDM6cNy/G2OqjTGfG2P+aoyJvQDUUZTOLeWLm78I7wCHgP8LPAs8B6wxDDt+E3fcMSPhLb07
05GwuenC611qutB8rXEwYCYcnw0jRhEe+n/4+3uDmDPn3mN6Lo1B3dtv3wiUAa2bh6xURz7pE1R+
0TG95XVSNs4dVN7qLvq97ryOVIJ56j0KuDrJJPvNxxizElgM/JlI5u0+4GzAZ639PM4xecDLwB3A
C8DVwE+Ac621/4hzTA6wadOmTeTk5EQ9FgwGufXOW3lm8TOEJ4XhdJruxDpbHXybfaxZsoYJE66j
unpWzOzSsWaHsrPHU1OzlniZtKysCWzbtpZgMEhx8QNUVGwgFErH4znAlCkXcu+9P+7w9SPXWgqD
L4SCaji9+c4z7zp4Vg/ik5pdXX4+RUXzCATyGl6nILAQ2ACkAR9zzjleXnnlDyl3Z1uks7Jzsqkp
qIn3a0tWRRbbNm3r6WGlnN7wOkVl40aH2/wfkIrZOOm4YDBI8T3FVKyrINQvhKfeQ/74fErnlur7
2ofp97rriuYUEfggELPE0NniUJhRSNmCsiSMrPtUVVWRm5sLkGutrUr09ZKe6bLWTrbW/tpaW22t
fRu4DhgF5LZz2ExglbV2kbX2HWvtPKAKKOzKGLxeL+lp6TCZNq3jG+/ELihbELOl949+9PoxB1wd
7Ui4b9++mG3rH3vswg4vitx0rQH+SMB1RvSdZ84ME5p4oM2d584E59FNRxrncK0FlgGvsndvvd7k
pNfrTPmFm/WW16m3ZOOk8xo/eAd2BagpqKF2Si01BTUEPgiQNyFPGY8uSPbva0fp97rrSueW4tvs
w9nitCxWwtni4Nvio8RfktTx9UZJD7piGEbk2/tpO/vkAetabVvdsL1TGt84OjJhsOWiv1defSoc
v4Wllb9k7CVjjylV3dGOhH7/wmNeFLnpWmkVkQxXLGdA+bryLjXbaD+ANHSl6YhIKlL5Rcf0ltcp
EZPG9T6XGnrqg3df/34nukwvEa+fmkF0ndfrpXJNJYUZhWRVZDFyxUiyKrIozChUhrCLUiroMpH/
dR8CXo1XJtjgC8CHrbZ92LD9qFq/cWSdm8VHBz5q907sjt27uOWWn7Fz586E3DGLnjMW/cbTOGes
uxZFnjLlQhgYbPf51pk6/vVfr+z0YtCJaGkvkqryx+fjbI39Nuq851BwebxFAN0l1V+n7szGaf5I
6knkB2+3fL8TlS1M5OvXW7Lsqczr9VK2oIxtm7ax440dbNu0jbIFZQq4uijpc7paMsY8DkwExllr
d7WzXx1wrbX2dy223Qz4rbUZcY7JATZdeOGFvF39NsG0IKQ3PHg28D/A9cSdc8DDWTh7H2fYF2aw
57LayB2zVtqrcT1ah5fa2lrGnp/Hp58fhoH94ZAHDuZjDl/CWWc9wWuv/ZGzzrqG2trlcc8xcuRU
dldQanoAACAASURBVOxYdtSAJhgMcsLpJxO66VDc5+t9ZigHdvy21WLQDc/TWUVh4ca4i0FHz+nq
3LEivUnc+QLvRcovdDcwoje8Tkedd1aexbaq9uedaf5I6rHWknl+JrVTauPuM3LFSHa8saPTNwPd
9P0umlNEYFeg05992tMTr193/F5L37B48WIWL14ctW3v3r28/PLL4JY5XY2MMY8SmVV1aXsBV4MP
gFNabTuZttmvNjLHZHLgWwfgh0Tab1wNjAVOA7bEOehdBw4WEA5P4tPPD3f4jtnR7uA0lu+deuql
ZH3Zx6eX7oCiD+HGWiiqgWmPcPyo/8OaNc8wZMiQbssgeb1err/qe5gtsfd13nPgoLfLWbXS0tn4
fItwnNZdC1epa6H0GdZalV90UG94nbojG6f5I6knkeWtbvp+JyJb2BOvX6pn2aXnXHXVVZSXl0f9
efDBB3t0DCkRdDUEXFOBr1tr3+/AIZXAN1ptu7xhe7te3vhy7DeOCxuOfoeoCYO840CFD+pKIhsG
9u9Qqnrfvn3tpuJ37tzZ1BTj/Q/HcuSbB9o08eAM2HPxJywoWwB0z6LIjX5x9y84672z4k6QHNx/
LPGfKO3Oy2puab+xSy3tRVJVrBspxfcUU+IvUfnFUaR6mUp3TBrX/JHUlKgP3m75fieqTK8nXj81
g5BUkvSgyxjzGPBdIjmnA8aYUxr+DGyxz7PGmJaLR5UB3zTG3GaMOdMYM59It8NHj3a9I86R2G8c
A4D/Dekb0un32CB4YiQ8nAVLC2F/JZEufCZS9hfvfeUQ7PtwH6flnkbGlzP4+2l/j3sHZ+LUAv7+
95mRErx2mlq0fOPpzgzS0e48DxhQR/QTDQLz/n/2zj0+qvLO/+8zSQgkmQgEqxBCACtyqbC9Kher
rYhYG6LSbmu7tdb+qhQl1tbbbmB1C2m9V5ToIltb27pqVykQV7l4owiote0WBCQKCcEEFMIlMwEm
lzm/P86cuZ77ZeZMMp/Xy1ckmXPmOc95nu/zvX6+wEzgCg4e3MPNN9+tmnctk440NW1g//5VNDVt
YOnSuz2jYOXgXXgp5TkeRmoaMlGr6NX50oIXazrtRuNy9SPehRuKd396325EC3XnD2fmLxui7Dn0
H2Tc6ALmAaXAG0Bb3H//HPeZCuJIMkRR3ApcDVwP/B9wFVCtQ74BQH44X11wDIDTy06nongaHGiB
o00QWopkcEVwogo+ULg2BPwBAl8O0Dynmc68TqnflwLCZ4V5b+82pGxKEQYaE9xOR5C0PM+JUbUA
MBeJHHIDsJre3u26pBrRR/CggpWDc3BCqciGYnQvpRJlw3xlI+xE47KFpdFJZItB4Ybi3d/et9PR
QsX5CwGvA08Bz8LB/Qe5+Y6bbcs1r0fZc+g/8BSRhpuQiTS+dc23+B/xfzSbvYknB6sSQQjCCwwZ
9WOOXdCeUPjJKmASUoqgCDyLZBaqYXkhHDgJCDBkjFTDZbLQU4ucQ4+4Qw+BQICpU+dGmkFvRcq/
zBFj5CDByUaj2VKM7pUGv9kyX/0R/aGZaF9oMmz3fJTRF9+32ty4QYaTMH8h4Dkk3+6nycm1HNKC
ftccOd248f/dqJtmoJXGN3HicrZv+b8Uj5n/uD8W2RKALjQ9YJyM+/eJKomsQwFaHqRkwWilr5Ya
4qNqeXkrkUglU2GGqj6HvgGnqYO9FEFSg5dSibJhvvor+nr9SF9pMuxU9KmvvG8jkXM3ooUJ87cZ
yeA6m5xcy6HPot9Fuv76179y9tlns3DJQta8soZuXzcF4QLmzJzDkoVLooIjEAiwcOGDrFmzme7u
IgoKTjBnznSWLPlZgnCR5y+FkvZ1YCSJKYYhYAuwBwgXwMmhcOKfIXQnlMyCql0wzpoHKRaZ+mmE
dVC6ic+3jgkTHrJMYCGKIhUVVzhCVZ9D34DT1MFeiSDpwSvUw9kyX/0VgUBA93zJVpjd+05FlLyM
bH/fViPnTr1bef7qn6qnd15vTq7lkFakO9LVL42uz33uc9HfGxEcRj6Togglh8q7UAyd0xhhRwyu
h8J7oeg5GHiYyjNGUj2r2rDgdrM31pgxM2lu3oCaNBw9+hKaml6xdO8csg9OKv1u9tBxGl5IJcqm
+cqh7xkdRvb+tje2UVv7AA0Nm+nuLqagoJOqqunU1d2aFUaIHWTj+3aj/5ZZ5ORaDplCLr0wzTCy
gY18JqXINMKGyEfAk8AT+XA+KaFzzglD1Q4onAGhnXB0NjfMuZXmvzebKvRsaNhsua+WHpykqncC
Rh0F/cWhkE44nWaXTcXoXkglyqb5yqFvkQgZ2fshIcT5519Fff1Umps30Nq6mubmDYZJl7Id2fi+
vUB7n5NrOfQX9HujyykoKmQDgBE+ODoJwiNU2QwZBxSJ+Hw/ZdKkNu6/v9bUd4uiSHd3MVqnoVZf
LT14odmx0Xq1HKubu3DjcMyW5pVeoR7OlvnKoW/ByN4PHj7B++//LJJxEfMuhsOz2bXrFhYufDBN
o83BCLxUq5qTazn0B+SMLoeQrJD5/mtgXJ+vLTBQJVcZQIC84gPceONblmqvBEGgoKATrdOwoKDT
spfIDlW9U3TiciNpLe9pW1sboyeP5tHWR7O6yNvrcPpw9EIEySgyRT0c70x4/pXnyVubh9AoeH6+
+jv6WrRdb+9zwu9axkUOzsNLEaZsOgdyyMEqckaXQwgEAtTWPsCaP+6g++PJ0DYWju6N9Pkq1W6q
LELF6cN55JH/sKy8uZ0CaKbZsRSV+ndHWBQBamsfiBCEqHtPA4EA504/lyPTj0iRwxz7kWtw+nD0
SgTJLNKV6pLMGHeg+gDdP+xG3ClSsLyA4Q3Ds2K++gucZJH1GvT2fkn+ZNzKuMgksnHMRuGVCFO2
ngM55GAG/Z5Iwwl0dHQwbdo3kpgD/x2piOtr0ocKa+CqeqmGKwlOFKvGxnBLnHEi4vOtZcKEX1lm
LzSDQCDAbbfV8eSTK+nu/hXSs9tnUdQn8phF1Tcn8Oizj8J1qh/LsR85CDcZu7KxGN1N6BW63zj8
Rh6575EMjMwa+vL7dYtF1kvQ2vuTJ1/ZZ0iX+kI/MiNwo/+WE/CSnPDSWHJwFjn2QpfgtNEVL5AP
BdvpPFwUoX+vA/xAAJgL3IxkfAShZKotWnjFMcSxROXlHWfw4EKOH++hp6dElebeDcjKxo4dI5AY
RC5L+YwVFkWjlPX5p/+DfSf3aTakzrEfuYPcgeQu+gJFfLKs6quMdm6yyHoRyXu/rzx/f2tAnu20
926gvxjd/R05o8slOGl0qQnkGP37ViTDqw34AbAfn28ognCEwWcGKRoG4YKwLcGm51HdsuV5SktL
bT2nGcQO2wcA7ahUU9MGU/fWi3RVVs6k5/TdtLa3wjWqH0tbHyWnkDNmcugLVMr9Ifojw0hU3qz8
yybE3nXmMi6cgBdo1DOF3LnT/4zu/owcZXyGYMb4rF1cK23GT4cV6N93QeFCpEjXtcAtwA7C4U30
9u7g6IEnKO0Zz85Xd9oqwterc1q06CHT97QDibJ+FuA8i6JevVp19QVSMXAF8KHKTRrJCvajHPti
DvHwUqG7VRipyewLcJtFNhtgh3TJKTgxv6s3rNakUV+9Xj3zItvhZVmSLqjpeLn68Bzsol8bXUYV
3GQhrtXXgnFhKFoDPAD8FJAVDek/LaPIzGHhZl8us4gpGz7AeRZFI5T1VTOrEEYIsBX4IOFj0AhD
tw71PPtRMmFCjn0xB/BOobtVeElWuQm3WWSzBWZIl5yCk84qURRpP9GuyTZ8+MThPm0893d4oXdZ
Dn0T/dbo0lJwz7/kfNra2hSFeEdHh25fCwZ2A28C+oqGlcPCax7VRGVjOuAsi6IR72ndojomNk9E
+KIgNaT+PfAM8CQM3TKU7Zu3ez4dIOddy0EJTrNFWpELVmWJ12SV2/BaI/lMIx0GptPOKkEQOHX8
lGZ0+dTxU448W19Z930JXupdlkPfQ781ulIU3BDwBoTfDLPzk51UnFvBo22p/Z6mXTqNvJ48TYHM
qQKgBD1Fo6Ojw9JhYdej6oawiCkbtwIPAYlRKUF40VYjZT3vqUw3u6ByAaMDoykfWk5lUSU1V9fQ
vK2ZESNGOPCU7iLnXctBCU5QKVtx7jgRPehv0R8vNJLvb3DaWSWKIgMLB6qnqn8IAwsHJpyjZs7U
XAq5t9EXUrpz8C76rdGVoOCGgOeAkUhEDKMgfFkYzkZRiA8pGqKa7kMjFPsE8vL2oKdoLFyy0PJh
Ydaj6ragjykbbwLPA28Ds4BLKSiYzA03bDGU02/k8FISdqIopjSubf5bc1oa1zoBp71r2eqFy9Zx
uw07TZmtRAKcjB70p+iPF2qa+hucdlYJgkDZ4DLlVPUPgK1QNriMYDBoyZGRSyH3PrI9pTsH76Jf
Gl0pCu4WYCoxI6sF+LTyteGzwhztPKqa7jOpaRJte/+P+fPn6ioadg4LMx7VdAj6RGVjLuXlf2f0
aFiw4Hza27fw+OO/UFU4rDYT1bou27xQTnjXsrUpa87zaw5m17aVSICT0QMjssqOse01Qz0TNU39
FW6lglVfWo3wpaRU9d8DH4HwRYGvfeVrls7UXAq59/arEpxO6c4hBxn9ljI+offNU8SoxkXgWTT7
PQ1vGM77r73PorpFqn0t9Khzt2x5nokXTzRFBZ1M5RoIBFi48EHWrNlMd3eRal+uTNDfGqWdtUon
3RdpqGtur6H+YL2iIa73nozOh9fogHPUvO7DSp8vp3uDKcmq2bO/gDjwKOs2rjPdByfXQycHGbpr
1UKrkBS5FIHcV3PG+TNYcXiF6TO1L/Tcs4Js3K+53mX9A7k+XS4h2eiKKrhjw6lGVrwRJkMkqhAW
/OdA2j/4JLrx1BTZZEUjP7+T6uoZ0ShU+bkVBK49rnlYbNu4zVBTUS1lWk/QV66upPnvzSoz5y6s
NtPsK00446FqgBhooK01H4LwApMnP8Hx472ea0zbn/vhpANW+ny53RtMFEWCwaBlY9uMoe41J0MO
zsOOs0oLWkr35Asnmzae+kLPPSvoC461nBzpu8j16UoTouHjPT7oIjGtaxRSEW0IeB3JCHs28vNP
0H3sqwm9ZdQ2o9/vl+jMq6ZRUNBJT08xa9a8yW231XHeeVcS+PhCqaGyAnx7fMy+aDZTp86lvn4q
zc0baG1dTXPzBurrpzJ16tyEFAYt0gy99IvWIwfp6OhQ+YC7sEonnSkaaiNOCquODDuECerzEUAU
l/OPf9TorqFMIEceYg1G15iVtFW3C8kFQbCVZqV37e2Lbs+lq/YjuJUKplZHWVJSYimlsb8SNPSF
lMq+9k5yyBz6rdEVr+D6e/xSgayMacBmpBxumVzj6sjPSUBBE6tWbQS0lR855SvZaFq+/CC7dt0C
p/4ADRNgd+JhITQKTPhwAuKJ02w3FTUi6HsCg9PeTBms00mnm4baSK2UU3VJVggTtOdD7hd3OVbX
kFvIUfOag9U1ZqUo3O1CcjvGtua1I8P8+r9/nSMq6Edwgt1TD045JfojQUPOsZZDDjH0W6MLYgpu
645WJu2dFPOUFQLlwJdJYTDkHGD2+7R1/FVX+amtfUDRaJKqc78G+CG4FVbeBI+MhuXl8MhoSjaM
ZOv6raxb964j0ZyqmVWJRmU8Gn1w4lusWbM57cqtVTrpdNJQqxnO8ZEit4hKjI5fez42Y6RfnBLc
Xg/91fNrBXbWmJVIgJuF5HaMbd1rt0L3Jd1Z7VXPwTzssHtagVXjqb8RNOQcaznkkIh+bXTJUPKU
sRvJ4EpGCPibSM/XArrKj3LKlwjERyX8EFoKR5vgwH442kTpgM9SXFzsWDRnycIl5L/sT4mosdsH
DedAaBD793+cEcY7q3TSTtJQa82hmuEcHynyQvqE8nwkr7VkpK6hdDMJ9kfPrxXYWWNWIgF2owda
e8qOsa17bQvKcpucV72/IB1OGqvGUzqicl5CzrGWQw6J6LdEGloIh8OUjh9M53cVFM3XkVIOFQ52
4QOBBeULWHrvUqlotuIKWltXK3zDTGADalW4o0dfQlPTK4wZM5PmZv3PGUFl5UW0fDwFitbAwG6p
gfOJ2RDaDdwGxDMsqjMAOl1QqsfyqM9eaO66+OuNEJTov4NZMOTDjDNSqc0HzADexMgaykTBsx3y
kP4EJ1nPrOxhI9eYYSizQ36geq0I/AH4nvoY+yJRgRpyxf/uwgl2u/7wjtwiOskhByeQI9LwAHw+
H2XFQ5S9M8k9vOLINsR3Reqfqqfm9hqCwaBGytd0YK3Kd8eiNE5Gc6qrL8TXfVlCRI3Qp4DbgcvQ
qvdxs/+T1WaidpqQGkkZBGO1Y11dgzyRPqE2H1OmlODz6a81yEzBc3/z/FqB0yk6VpQ8IwaXmfRH
O2lWqtfu8VHQ2b+96rmed+mDEymNfXktyuhvKZU55KCFXKRLBYremeQeXiHgOaTGyp9GUorC4GuS
IgMzpnydFSsuUqDxDgCzEIRaRFEmOEiN0tiN5iR8o+K99CJus9i2bWVa+2FZ9fwlX6d1HzN080ai
jQzZ43ifGLuQn9/MGvJCD5ls8PxmYoxu9CJyElao/+1ECtSuDXWFWNG+ol961fsCNXcOfRN6ez0b
5H4OfRO5Pl0uwazRpXaA8SRwHdK/5VTDUcAWpCjYACQK+lK4bsZ1vP3GfkWFd9y4+7noovNZu/Yv
CY2NFy/+KaWlpQnjMNIAOR5G+oZ1dQ3i44/b6e1VJ1IoL6/mqqumUF8/LSv6YTmZMtjUtAEwZqCJ
hUc8nT5hZA15qYeMFw/gTDf39HqKjl2D3c47j7+2P6er5nre2YMX5U5fRLxDMNsaJufQ95AzulyC
WaMLlL0zJQNKeG/sezAOqW/Xt4A/khjtEoEPIX9dPvv+sY97731CU+Ht6Ohg4cIHbTVANivARFFk
7NhL9KM4YNhAySRiER3tiJx2rZ2E8vJq9u9fZThSBGSNomenibab0RSjBrNV2FGovBBB8LIx4SWD
HdS96otrFyc4tPoaNPdvGEa/6H6kOtuQU/wzg3TK1JwxnYMWcjVdHoJSzvb0KZdDQyW8L0hRra1I
BpdMLR8C3gC2QM9pPYyfPp7wgHa2bVvJ/v2raGrawNKld0cFSiAQYNq0b9hqgGyFTloQBN2asaqq
6Wnth2UHRlgGwTzdvJHasWyqS9I6fDLFJGi0xs7KfZ2ob/ECO6WX15jXGMri5fbOV3dSdXEVazas
YeLFE/tsjZNi3V9cvTHPwf62/X3y2a3CrVYfavDCOekVuC1Tc7WNOXgVuUiXSUipaSuhcBGU1ENp
r9Q0WTa45BqvCiSDrAXwga/Dx7XfvJaH73k4QUFSTl8TAcFw+p7VtBIjUZzJk690jEHRTTidMqg2
50a8Zm6xw7mNTEVT7LwPNTjpSfVCrVvK13pgvcTDi+mPdtaA1+Y3HmpjS1inSvXGHqzvsjvPdq5P
RzpmLpKmDDdlqtl97+W9noP7yEW6PIwYm12p1Fsr8FlpBuX9ugXpkBuFlHI4Eskg+x6E54d58tiT
nDfzPJVeXgHgLiRyiyuAmYTDW1m1aqPuuKx2fDcSxbn00i8iCC8pXm+WQdEtGGEZjI/I1dXdyoQJ
D+HzvUw8nZLP9zITJvyKJUt+pvpdRoSzUQHuNW9cpqIpyv3sJJhpAh4PpzypXm3u6TUlwYsMZWbX
gJssrfGwslaMyIqESLV8FskZGOCZJtF25Z5TctPquWkU6Y6kZQtUZaq8LQzKVLW/G9n36drrOeSQ
jFykywRS66AugrItcFNEgDyFZGS9gXovr0aBBSOTe3n9AZgL/BSI1SPBOvLzb6a9/S+qtQhO1lMk
e3wCgQBf+lI1779/ElhEjFpeBP6XCRMe5u23/+QJj53ZnmZWCEqchNM57W5469LhATRbY2cUTnpS
vc4c6BU40bfISZhZA0ZrQq3CTsTDqKxI+NzmcCwDQ+fZ0wm7cq+trY1zp5/LkWlHYgalBbmZjjrE
HLGJOqJ7s4tUErIKGHVsFPv+sS/lOiP7SG/fV66upKR7XNoYmXNwFk7rJblIl8eQ7FVrF9+FgVcA
HcBpELwOGgXJDpGFRiOJvbziIJ4tRj1osfqi+5EMrsR6JJhNT8+DLFr0kOr4nKynSP5Mbe0DNDbe
DqwH3gFmAdWRn89z4YVf9IxwqqqajiAY60cFkbqPpXfT1LRBsdbObTgRiXE7UpaOaIrZGjsjcDo6
lalaN7fhtMPNib5FTsHsGjBaE2oFdiMeRmWFHKm+cfiN5PXmeS46C/bkXiAQkAyu6UckIisbEbx0
1CG6HUnLZlTNrELYLUgpsHJG0NWRnxUQ7Aim7Asj+8jIvj/ceYSdO29xZa/n4A68lhVkBzmjSwNK
mzxw7XG4ag34JwPHIXQfNEyERh+cQurjVYThA6+qajrwKlKESwmX66ZXuaUUxtK+/MDdSD29VkV+
/oa1a9+1dF8nIW/G1Zt+S17FlTDkTCisQUrXdC5l0GloHshj9Q9kO4qc16LbTjYBB+cVKi+mzllF
ug6vTKc/ml0DbqS4yrDrYDGjvPv9fh657xEqyio8Q2wSD6uGiCiK1C6u5UjvEVWHpllDxk1nilfT
kr2CukV1DHlriGIKLGfDsRnHUvaFkX1kZN+fOtaNKKbWD4P9vZ6D8+hrabo5o0sBsmJSPqmcHWN3
pGxyxoFQ1UKB/z1gEwS3wsqb4GgBTAPCGD7wliz5Gfn58o2VoM8Q6IZSqF4nFZuITDMXxm/GluoW
eq4LQc3HMPdR8oeUM2rUVxPq07wCJ5jGLNWreNRTZKfGTg12Far4de1l5kAzsHp4ZatiaHQNmK0J
NQs7EQ+ryrvb0Vkrc2H2WZJlVv1T9aYcmnpw05niNUZPr8Hv91MyuMSUAW10H+mt/YHh4WQDI3MO
ErzAHuwkckZXEuIVk0B+QLEuC6Q0wRFnlTBp0lJ8vjch9DDkDZeEyCjgQ+XrhA+EhAOvtLSUESMK
sZNe5YZS6Ebal9NQ24yMg/DlnVzx7clpTRk0ipQDWWYai0uz6L2hV1MZNqPIed1TZITQxSysKFRa
hqmXUueswszh1RcKzY2uATdlnd2Ih1Xl3Q2Dwu6aMPMsKTLr8lbCQ8JS+r7S9SKmDRm3nSl9NS3Z
CYiiSG9+r+F9YWYf6a39suJReFmvySERfS1NN2d0JSGqmJwVlmq0VIoxEaAnv4ctW57nppveprLy
EnzFn0ifn4ZEF/8BCZue3TD+w/EpB1519QW206vcUAqdTvtyGtm8Ge0wjZmuVzGobGfSu+d0jZ1Z
hcqMYWq2vszO352E0f2S2jdtlSN909INM2vALVnnRMTDivLutEHhVC89o8+SIrMEoiQLUYdmfHbA
s8Cv4bRBp5lan246U/pSWrLTMLsvzHxeb+1XV1/oab0Gsje7wGn0xTTdHHthEhKYb2Q2QgFJwCex
7Ph7/LTuaFVmzZE/vx8oALqhpKuEtp1tygqfTr+sdHnU45lhMjkuPYaadLBPuQm7TGNmGPU0P3sK
/E/7KRtW1qf7yOitJyeZxgKBALW1D9DQsJnu7mIKCjqpqppOXd2tUZa5dPfuMbNfbr75bpYtm4Io
/gPYDBQDncB0BGEyCxZsN903zQvQWgNuyjq7Pcyc6J9nl/HLqV56Rp9FUWa9DpwBvAt8IfLT433I
MsnoqfTOvdSTyuy+sLqPlFiZvaJvxSPX000ZbrMHp5u9MGd0xSFFMXkdKeVrFIqNJoUPBSbumRgV
8KpCIXKoaB2umaQw11ISgbSNS09ZTYbdzZjpA0gWso899xi91/Wqfk7JeDR6AGkq23Ja4/nYol/O
dgQCAconlxP4fsA2xbYe9fj69b9l1txZjrUKMAOj+6Wy8iJaWgag1MICHmLUqG727XvdlTFmEh0d
HSxa9JDjss4JoynTdPxmms/rQe9ZVGWWLK++APwVOA+JxTAJXqVjT8d5o6S4X/rlS0GAdRvXeUqZ
N7svnNhH8ffS02vSqR843UKmL8Gu00oPOaPLJViKdMlC3g98BsX6rviX7pRQ0NrsTgsCM/1p3BRC
VvrkWNmMXvQmVX62kpbqFlPGo5m1pqpsy04FnXXdlxEIBDj/kvPZeXgnfE/9c0ajpnoRgXO/eDfb
z343I717jOyXh+95GL//83R2/gKphUUyXqa4uJZA4K+e8ZjbgZo8WLJwiWpvRKvf45TRlG5nkVu9
9OR7K12jKrPkDJIdwI3YdpL0JSieCaeAPwBfxpOONbP7wg3nQ3J2Tyb0g1xPN3U4aWwrIWd0uQSj
RleKYhICfgtcjyEBb1YoGDlAzUaAzMCptBG7sDIOxzxlGTyAAoEAoyePlnrPmDR+jK41VWU7Pn02
Gf1EcYkednopngZTGPQiAnmnF9E7/1RG5tzofsnP/wy9vdtVnyE/fzLd3dtdGWM6kSl5kOkIuxWY
bT5vF1oOAuEDgaK/FNH5nU7V672cWu4WFBX3LHKsmd0XrjigM6QfmGnk3h/hZqQ/1xw5w0gpfh0A
lGK4kM9IYa4Z+u6Ojg5HCpjVYLU/jdPGupVxmC0W9yL1aO3iWo6ed1SZeKURBr85WLXg2mgRuGJB
dxhp9/ehAlUriJJLaDCOGmUa06ceB7FQ488uz7mR/SKKIgMHnq45yMLCYX1iXSjKA9yXB9loCKST
VEmPgW7inomUFZXl6NiToEiU04Jjfc3chtn35fT7zZR+0BfJIpxGX2APlpGf6QF4DbJisnDJQtY0
SFb1wWMH6RVV6E01BLzS7xK8KXNi3pT6vfW8Nus1tq7fChCNbB06dITOzsUkpvrI3dNFFi580HIk
ykx/GpnG142Im9lxxEPejEtZquv5anilQZpzBYTPCrOmYQ1LSa/Xr+GVBsQ5IoxFSpvZSpR4hQoo
Oa3E0NwaaSkQv6YLwgW097YTENXrmKwqLtniyU847KYhpRJDQt0mjTChaQJLHtNnGkukHld+5Jzc
rwAAIABJREFUfiGk8ec0KIt6+0UQBMrKBDo71QdZViZkxfvVQ1QeKJAkhSvCrNq+yjNRgEyjru5W
XnttLrt2iYrkA0uWvGDr/mq1SBf4LmBtw9pE7/ZjS6hdXEv9XpVU2X5Ix66ouMtOYwPKfF/Yz3aR
Kf0ggZkxQ+dCNiHb5yEX6VJAslU9/5r5jvXb0POm3H7X7QmRrc7OocDXFO9lt3u6mf40TlEG2x2H
3n3U4EVvUsKYCoGvIKW4fTvy8yvQW9DryJiUPEXXfvNax9a1l5svqyHhsCsEvgV8BPweeEb66X/T
byqtRC8i8Jmxkz3Tu0dtv0gtLNYq/s3ne5krrviym8NKC6J7r4uUHnlcA1RAW1sbHR0dmRymZ+BG
Lz0ZbW1tjJ48mkdbH01o17DiyAo2bd3Etje2pXi3c3TsiVCkVBdQ72sGOWU+DpnWD3I93foPckaX
DgRBcFTA6/XKeXrlsxEyCTmyZSwCZFUYGE0bqa19IG5cMWtRirjdwsKFD2p+j9743E5fcaJfjtNQ
HZM8BJfGJN/PqXXt9ebLWkg47JIMX980Hz+4+gemFMq6uluZMOEhfL6XiZ9Un+9lJkz4FS+t/JPn
lUXpGX6l8gwPs2TJzzI5PEcQ3XubUeyRx9nQM7OHRXWLMjZGr8HpXnogyY5zp58r1bSOQzWtSynD
wW4fsr6WrnXphZcifJh0VjiQNt0f4LR+YHZt5ZwI/Qc5o8sAnGo0acSbcqL3JOHwrMgvgkAr6pKg
g46uvzH282MtRxf0lERZwbJSc2Um+mF0HHrQEnZe9CZZGZNTyoJT69pLtXKOHXZ7rB12ehGBESNG
ONq01g24GdXwEqpmVkETqjUvjMNTNS9uwKosccoRVLu4liO9RyzVHVmp88jGiLwRBAIBNm7eiLhR
hEZismwqsBHYTU6Z14Fd/cDM2kred043M8/Bu8ixF1qAnRxoPZaavPpB9B4+AQSAucAIpLyny5I+
HAD/uTBnn+3mkHo9K6xQBlthArLaq8xorZnb1KNWYHRMbjJYyrC6rjPNvGR3btxkRjLS5Nvr6T3Z
MEYr6OjooGxyGT0/6FH9TF9kwXOKFtuJdTH6s6PZd3KflNapguKn/bS9+5FtCn8vstc6hShzYUVY
qk/cT6w2uAg+U/IZgl3BjPR4yxbY0Q+MrC3A8L5zYm/1VbntNHKU8S7BSaNLCUYXuF6vnOJ1Iwgc
agHuRnJTTUcyvm5BItOI7OaBc+CqFx1vDqnaN8UkZbDdvhNG59Nsf69MNxlVewalMS2uXUxpaaml
Hmbpgmbz5QjcVFztzk3yOssdVP0LVnrkZTPsGh5O9jGKyo72Vs12DTxyBpNGTLYt5/pyLyRFx5dM
zBDn+MrJN21Y1Q/01tb1Zdez6e1Nrhv8XuxD6nXkKOOzCGZTFQKBAF1dXeStzVMN93/nqu9Gapve
BC5F6sz8AvA2MAuoBmYhFK9T7L0B9qhg1QSy2Zorvdo1vfEZPRjM1pp5kXo0fkw7X91J1fRrWPPH
HUyc+D3GjJnJjBnfYNeuWyzX07mJTNfKWak11Nq3/VEh6S+ONyVcdtFlUqsGJTTC7IuUGkR7C2be
n51UYKdrN6OyowLVuiMagRPfiu5lO2vV7pnkVaiWLcS93xxLoTGY0Q/iz5HHfv+YTq3+066n4Gdz
bXV/Qs7osggzCzwQCDDvJ/MoO6uM5YeW0/3DbmhDYkn7PRQsL+D6069n/QvrYdAx8oZdCcM3w5Cx
UFgTucvdwAZgFbAeYVCeZm3YoUC7o8xbZmqu0skEZLXPGHiPejQQCDBt2jdSGCK3bQsqNo0G+wyW
TiCTtXJm33/uYJLQV2tbTOPkYGiohN2JNX3s9sGLldLfPQir78+O4eFG7WbVzCqEEYJqn0JeHAqh
OwgXvEz9M/daXquZZqdzE5l2fKUDmXgvWvOVcI5UNdN7mkpLIZBq9btPuG7we6m2Ogd15IwuizC6
wOXNufyN5XTP6pbSAQcSY0n7F+id2QthmDV3FisOr6D7x6fghhDUNMNV9VAyFanGK/IliLF+P0oQ
ofNwEdOmfcMxJUqruH7LluejdUc1t9cw9vNjOfjRQfXxhZ05BMz098oGKEdtAIbh5WfMFPOSlfef
O5hyhmc81q17FwLbYOVN8MhoWF4u/Vx5EwS2sXbtu5keYgqsvj+7hocbkaK6RXVMbJ6I8EUhsV3D
k0DDUAhshZJZMLee3vmnLK/Vvm6YeI0kyonzyMuOoYRzxIc2NX8Yw/3S7KCvRnL1kC36nYyc0WUR
Rhe4vDnpQJmhSdAOP3NOGKp2QeHtwF3ATOAyfKf8qfSwMhp9CSkZTiGeMnjnzt9T9c0JrNn0FBMv
nkjllEpGTx4dVQR6z+lNTBkJAa8DTwFPQ/vR9hQBanbzWOnv5eUNqhy1EQD7PczcRKaYl6y8fysH
k5fXjBXkDE8JMaO9FEJL4WgTHNgv/QwtBUo1HRqZWhdW358dw8OtSJEsOxZULiB/50A4WQ4fV8In
NRBohsJlMGcXjLO/Vr1mmDgJL1COO2kked0xlHKOaFHz7/VR5Cty1eDvy5FcJQQCAWpq7mLMmJlU
VFzBmDEzqam5K+PrwghyRpcFmFngDa80EB4b1vV0aIWfGReGot8C5yOlGK6jO/Ah4ppRKbVh7PZB
wwQILXEt9SwQCDDt0mkJArFlcAtHph+JKQLTiKWMnCKxAen3IPD9AMvalvGFr3yBeT+ZZ1lQG6k1
y4YNqh21mQ5oP2OmhWmmauXM1Bqa2bde9rLaRX/1iCZD2WhPZCJINtrV1kU6myjbeX9WDQ8jBlt+
T74lxVGWHT/+9u0IB1fAseaI0euHogY4295alWWjFwwTt5BpynGnjSQvO4YUz5F4fUepVv+K77hq
8Pf1SG48ZPKs5DKM+vqpTJ061/NndM7osgCjCxyQNqcD4WcGFhNjLwQojaTFVKSmxQS3IhFwuJN6
pigQ95MYyStEYrr/CClV5HwSG5B2gdgs0ri3keWHllsW1Hq1ZnfccX1WbFDtqM2twEPAi8Q/oyC8
wOAzb2DVn3/jKcMgnYLdTK2h0X0bDAY97WW1g/7mEdWCKIqmjPYUxfKSVpr9zTz67KOUTS6j8rOV
tvefPO9a0TU778+O4aFosMkZDE/C4ROHbcmgurpbmTgxvim3CAOtPauScVy7uJb1L6zvs72QMkkS
5bSR5GXHkOI5Eq/v/B7ynsxLWFv3//x+1w3+vhzJjYcV8iwvIWd0WYSRBZ6wOW2GnzklGVGJKIXQ
ODi6Fw60xKXF+KMXupF6tnrD6kSBKKJsNBYi1a4Vk8i0GEKKfAWBryHVuVkU1HqNXO+5Z3laN6gd
ZVVdAfQjCDcwZcqy6DOOGvVVhoz6Mce+2kpLdUufMgzMwGwjXyP71steVrvoTx5RJSRHvVev3sjg
wXfi872EntGesC66kGRYBXAd9Pygh5bqFkv7TzYQKqdU4h/tJ//MfPzj/YpGnN33ZycikmKwyXJ8
pDQHnd/ptCWDUvfyFeT1tJt+Vq2oy6y5s1iycImn2GvdQLr3r5NGUjY4hhTPkYi+45vmY/635ies
rXREIvtyJDcedsjTvIBcny6LMNpIL9qXa2RYOqCmktDMWPhAYOLeicw4fwYr2lcoC67dwMqaiEEV
jw4onAlF+2BgAZwqgBNVEKoD/Ph8L3PTTW+zdOndus9jlE62o6ODsnM/Rc91ocQ/PIVyrxUReJbE
5pevIx3UW1SuiVxnpalu8nMo9xeLNTAZPXoWTU0bTH1HMpxqXBzrORVPDy/i861lwoRfRY0IURS5
+Y6b+1zPmXQ0hDSybydfODmjzZ7NwMqc6fUKtLJ2soGOWq2nmyD8iSFD/gO/fxg9PSWqTdkTeiHJ
MkyhbYeZOZTX487KnYh/EVPOB6U+PvNumccTh55APDv17Db7/sz0Q6xdXMvqdatpP9ZOqEuS/z1f
7XG8V6SMcDjMT+78iem16rV+XNmwN+zAjV6Nin3Hol+Y2j8v3XNsp5Gym+P1Yh9SJyGKIhUVV9Da
ulr1M+Xl1ezfv8rw/Ob6dGUJjHouot6H/T74Z2IMTRGq+BvOuEE3/FywrhhCiyO/DEg08oMrYUgZ
zP0L1HwCN7QmsB0KwgspntpkmK11EkWRhQsfpCcwONX7qBbJU+KBaAHOwhVGn2TSDKlOCqLzNmQM
DK+QfhbeTCg0wJbHrK2tjdGjL+DRR7+UlL54vun0RaNRG0EQPJ1+YQZO19vpCVq9fVtSUuJ5L6vd
ObPqEU1+Zi/UvZnqUaWSliKKV3Hs2D1UV1/A/v2raGrawNKldycoKSne9xaUiZEwt//k6Jl4MGJw
xadgq7Dhbty8EXGjKFGqJ9TzwjmN55jyaBtuQB+JHLVc2ULndZ303NBDT0GP470i49fUqPNGsXrd
agZvGqy7VuPXgRdkoxf2RrrgRvTcSEZCJufYbuTKLQPRi31InYQV8iyvIT/TA8hmyAt8KUtVPRfy
5ly4ZCFr1ke8D4MLqLq4iiULl1BaWhr9bPRzDYleitA3B7FixRbC4ekSffycXfBRWEptiT/0ZLZD
djB5731s2vBKNDKimIIR9frejeyqqa9fx2uvzY0q+ckdzg/ua5dSGhsPRb4rgmlIkTyRmOIQ8fyE
jyMpCOeEJVINkcQ6NxVvlp00J3ncB7vWwxnlcOowXN6dMDYa6zm8bhDBYNCSUAoEApx77mUcOfIL
4PK4vwiEw5exa5dkpBqJNMqQGSKXLlX3hplJv/Cy8DG6Bp2G3r6NKhAurEu7cGLOEmRSkqxZ8lii
RzR5/xf0FlA1s4o7f3Ins+bOkjy9c2Ke3vq99bw26zVXa2TUxlS3qE7zO6W0lLsV/yalpTzE0qXK
7zVFsTToMNJbJw2vNEjztxm4SPkz4bPCrGlYw1KWUru4lsZzGiUS2y3AW0AB0A344cKLLnR83hPS
KuNRhPocYF4GJUQP4taUsFtgyJtD8L/npye/J7pW77j3jpR18PWLv07IFzL8btyQkWrPkY69kSlU
zayifq9KRNJkPVEgEKCrq4u8tXmEZ4Zj5QdxkaQ77r0j43NsRP/LJLw2HqdQVTWd+vp1ir1Lk+tw
vYhceqHLSN6MHR0dLFz4YEIq2te/Po1f/OK2FM+qfJ2saO3YMwiuelFiM1RL5wMQoXJ1JXMu+L5q
yltNzV3U109VWbgvc+ONb1FXd2tiCL0LSTn4EDiJxOsRJxDZIcC6IZBfAgM7KQh3ck7FJN57dyyU
vAOzW+BvoqQgXAe8gSMpOslICf1rfA+7Yd6Z83j8ocdNf8eMmRez7YNtMHBYSmqnBGfSF5VgNv3C
i9Bbg0ZTYx0flwvpd07BqTmLly9qCoNqCs1eH4M3DebYjGNpT+HSGlNyGl48RFGkvHwOBw40qN5b
Ly0lYV3oyF8j+y+alnV5a2oKdvLYIulZYz8/NnXfx7KlXUl9VZU1yXMQQjIEW4ABkHcsj/nXzNc1
hmUYSQt8+J6HEQRBcx3kbcij+wYVp5QIo1aPovqCa02ngxtVrL2W3pgO2E23U7zPyLDECLgfEKCg
s4AfXv1D7vuP+7jt329j+aHljusO/R1eNB6TYbQMwyhy6YV9AGph77a2NqZN+0aESW8lrYcraT6+
h2UvPEbZ2Z9i3i3zoqHx+IUvp535z9go0eeqEVfIEKD1yEGWLTtflbFPuRhRSsELnzafx/50L+WT
ytlx1o7UwvEfAfOANiRmwify4JFKaFgg9VY5ug8OHKL30Er27Qb4LwiOhZdGSyyGY5EMNxWaVaFR
YPwH4y0XfqYQIWikAjEOfv3fvzVd+D511lS2ffovUBNKSe2UGllLmpBbjYv7AlORVwtivVyQrD1n
l2rOmZpcCgaDip/XIhQ50nskIylcVklOgsEghw83YSctJWFdVKBOjGRw/0WjZ6DNbpvMhps8xLh5
cDr1VTOqHp9SHk+qcQ1wNfTO6zVFqmEkLVB+P6rrYGyY7jO6VXtY+vb4CH4iGmaztZLC5oX0xnTD
KaKIhPc6EImI6xrgX6B3Zi8DCgYA8OSzTzqS3ptD9qXCmiXP8hpy6YUOQyu14Olpz3K05T8Rxbg0
wbOlz3SL8MSHT/DmrDcVhVRJSQmlp5cQEI5Lv9BJzZPqri6L+6XM2CdSW/uAQk+oQMKYegUIPBWK
CbYtxGoOIMZM+BXg/TD8qTqJ6EMgHL6UEyeWAKXAaiiskK6vRDqgQapz2xr5TwThuECxv5ijw44y
+cLJVM1MTcOMPmZSNFAms9gf3EL4xnB0LvRTgYqprX2ARx75D5UPJSLa8Dpe6EdTO3fCyokQ+hzQ
SUfHJ5bTF7VQt6iO12a9xi5R2bO45DFvMxVp9yWDeIM13Z43M+l3RuEUSYjivuUBpBB0Mfv3f8yC
BYv4xS9uT0kTNJuOE019SxkI2qllLqa3qo6JxDS8ZEgy7wtI/e5So4SC8L+6aSnx62LV9lW07Wqj
J9yjmP5kdP9F07JGhSUDRslzr8SGm6bUV83vlFPKw0AriecDxIxhUTKGtSIPZlOmE9ZBUoSNUyC8
JCBcLqTIxsGbyjh64GFEcXbCzeWzMT4d3Mqe6Sup31bgRLqd6v4WYvs7HA7TXWx/jrPxHTg95mxN
hTVShuFV5CJdDkH2FpRPKmfH2B3K3uFphxAHbITCWsm4GRdb5Aggni2qemtTago0KOhpBE58S/FP
4fBsGhq2pBYjKo0p3ljRihadI0KRkmfJRyzqUwIDS6T7xfe0+CNwEAiDcExA+JpA8NogB6oO0Dyn
mUdbH6Vs9EgqKy+ipuYu2traUkgE5s27k/POuzLivVxPb8HQhLnX8yJzyk9DwxaVD6RCy5PJOBGK
8oHVwAaCwV+60g/MSQraTKQYe70g1omCZKc9iKlzFgDmImm7K6Gwkt7SAMteeDwlcm42QqSpPBrY
U27Uvdmhkm5o2Aw8gtTvLrGnG7xEfv5PNUmHZMjrYt//7aP9w3ZqKmos7z9RFKPRM+FMQbO5qhxd
zUSEW/U7C0H4osCUlink7c6zFXkwQ8aQsA4UImxcC+GZYQa/OZjK1ZUJ76ZEnIgoXqk8zqToupWo
an9vySDDyvMZ3d8vvvqiZOhbmONsi+qA82RT8cjm9iiynM+2vZQzuhxAPLtTID+gyujEOCTjpKgB
RoUl2uGnkPL5nwJeh/BI9QMq4fDT6ICev9YPITVPqxRBqKqaltgTqqhBirrFPhZTrAxEixjYTaoU
FCkqAkH4ExTeDF0HYx+RI2XXAN8GRoF4mZiy+RkHPbM7afl4CsuWTWHs2Iuorz+f5ub10dSQ5csP
xuX3+qT6qvihaBqoPjgxx3AaoJGDITYXAqJ4uWsN++wYBm4KcqMw05hWC24bjVaEulavIDt91BLn
7AHgp8B0KJkGc+ulNNcb2umed4onDj0R/S6zKU+6ymMFkuxRgBvKv+zNtKLQxiKEpcALwNvALKA6
8vMdhg07m5KSElNjKi0tNb3/kpW+yRdOZsZ5M7hhxA2M8o+ieFMx+cvzKf7vYipXV6qz4aYx9VXr
Oyfum8ifX/ozZ1acackYjodRgzJhHcRnYMSfG5Pg2IxjVM+qjr6bh+95mN7e09AaaPw5YDVNsC+k
fmcCRvZ3fk++dP7qOJ2V5tgtmewm5Polo+mwZpFtqbBe0FvswpLRJQjC9wVBuDzu3/cJgnBMEIQt
giBUOje87EDUW3BWWN84KeyCASEpwhPvnbsm8u8/QkgMKR5QCYffAGLRoich/zf50UN6hP9zgJoC
IUUQ6upuY8KEh/D5XgbCkqGQPG5ZsBmKFhWkPLjPt5ZvfnMmA8qugbnLYFKvOq18ExrGahiK1iCK
7xBiPOHT5sPwUVHad2hG6rIcwYkqyZiSoWKgstsHDRMgtNhwVMXIwZA8F+moTzJjGNgR5E4aOHV1
t8atwdiLUWpMq/QMXvZYuuFBlFi9QuTl1QAvIqUUToOiGTBnRyxKHfkuOXJeu7jWUoRIS3kUhgsM
3TLUVeVf6YAtLTjdtEKbGCH0A3cDG4BVkZ93UVgYsuUxNUu9Hq/0rTiygk1bN/HepvcINAfoPtBN
4P0AzX9vTjHi0tFkNRl631laWupIdMeMQRldmwao++XvNRNdtxNV9XJNqNehZ7BWz6qW1tpUlM/0
Rih4pUBxjtMR1XHaAajW5kJKh7XnzM2GJtTxcNsATResRrr+DYm/DkEQpgI3AbcDh4FfOTO07EHU
W2DEOAn1wqmgsnfubOB8CB4OatLPRw+/DeWMDoym5uoamjc3M+eC77Pmjztob+8AXlIcgiCs5LTT
8pg8+UqOHCmgqOh2/P4v4es+kjpu2VhpRLNwnEbg5GSUFOeC0hN0zz4ppd1NR5k44wOBfF9+4uaP
H4uAZKiWLIO5/xvx5seTV/wNiCMDCNVJxtTuyKFXiFQ7th1YVgDLh8Mjo2HlTRDcis+32RTNqNbB
IEfOEuEeoYYVmBXkbhk4VgtijXgsMz3XTnsQOzo6mDp1LitWXER397vAX4CgFOEauk2zX1LDqw2W
lGK9CMf2zdtdU/7VDtjtf7mTgpcHmVZolaOq0vOmi2bYiNIXbyCoIRO9ePS+04nojhmDsm5RHeMb
x0sajAml0Wh03U6aYCYM474CIwZr1cwqfK2+mNP598AzkZ874Iff+aHiHLsV1XEz+uIm2VS2pcK6
aYCmE5Yo4wVBOAGMF0WxRRCEe4HhoiheIwjCJOANURRPd3qgduEWZXxKN/bX0aRBH/xaOUdOHYYF
J1WLof2/89Oxt8PQd0fpc6O9ey5FMkDmAjcjRYCkIi1BWMmAAf9KV9cvpdqyogYpwnWqhwG+Tnou
O5FKcxsCXoKSYyWcOnGKnpmphePnNJ7DhZ+rZu3ad+nuLqKg4ARz5kxnyZKfMfnCyYl0w3LR836g
APKP5zP/mvmsWr+KltktklEmF0R3IUXbpgKP++HygPTdydgNrKxJIvIIQOFCKFpDXvEBRg47k8An
YY4e+FUkp98HFmlG1ehxaYxEzoJbidHGA4iMHn0JTU2vGLq/UVgtIB0zZibNzRtQW4DxNPdWKbqt
wDYlc2St+o/7KR1Warh/k9NIkQkKkCnAtZ43vh/VoWA7nYeL4MQ/x9oSFFbAVa1SGwYduvGrvnKV
JRr8QCAgEYq8kkQosjCRUMTpYmYtanx4ninn3c/x7k80x5T8HE7SDFuBbpsHF+je0wUnKMOT15De
mgoEApRPLifw/YD6nCZR95tZB061jsi2Qn+nYeT542VdiBDBw0HIg5KyEgrFwoT9rbjWwpEzSWWt
OSWTlcadqHvJ62kdEyY8ZEuuiKJIRcUVtLauVh+zTpsLPXi5PUoyzOgtZpBuynir7IVBoAxJPZ5F
LLp1ChjkwLiyBinsTjKjE0hpD0mHz7p31nHORePp1PDOlQwtMSSoovS5CR4AkBT+F4AHgV9QXDyA
00/Pp7TUx/btv0QsviuBORERunYI+F7y4fuaL/HQ3O9jwqAJbN20FVEUWVS3SJPRLbn/T0r4Wq7l
Qrr/Gf97Bg/f8zChUIjlf1gOFyI1CZUNmQ+BPwB5ok6t3HNJRpcfQkvxdc9m/r+8xdKldxMMBlm4
8EHWrPnPJOPQnGBUYrfrONRJ4OML4dTvSTS4nPWkW20MK8Msa6BiY1TBOCuZGRg9OBQZruSC+qkQ
+HSAgBAgUyxMTrDMdXR0MO3SaUmsUgForIeG1yTDviggRZDfQve7rLJdGmUkc5ylMKWRcUAi+4k4
it7b2878a3+kymyaDDmqKu3/h2ztfyvo66x2Vhk/41lnzfTMkr/z2m9ea6opr5l1oLhn4pR7owyV
bjVh9jLMnFNqDHq+vT4qGit4a8Nbiim2ZtaaW8yfqboXxKIviWyYZpGYDqs8aLtkU+lgQTay9o0w
TXqV7dgsrEa6ngbGA39H8rGOEkWxXRCEOcAvRFH8jMn7XQDcBnweGA5cIYqiZqxXEITvRq45GziO
REl1myiKR1Q+70qkKxAIMGP2DLaN3haLwsRHcwTwh/384Js/iHpqnG5sq+0B6KCkZAbDhn2K/fs/
oTf/IqngfpxCmP09mHJgCsdPHtf1IBtd3Eafdd4t81j+yXLlSNb7wJ+L4fpO9S9aXgAHXgC+Tnxk
b8iQn1NSUkZvrz/hQC8pKXFsc4qiSDAYdN2T7lTUSd9jFIvKOemdd4o2XdFjqRNhTrfHzooHMSGy
1X6IzhmdKpFdH7xwI5Q9DzccMPzsRqNWmUaqhzeQ0mLDbrQ1E4ez5l4KR/aSBxqaO7VPjUQ37EYJ
7EbYjETTbl90O0+vfJoT3SdgABT5ivjOFd/h/p/fr0uaYsdBlq0we07ZbSZtKkPC4aiOW9EXGVoR
f5/vZW666W3LRp0MN84FI2vf7P4wo7eYQbY0R74RKRHsdGCuKIrtkd9/Him71iyKgf+L3FfXChQE
YToS398KYCLwDeBLwBMWvtsyZOGyvWK75G2Wa5UKgYvAN83HxGETaf1Hq6P57/GGsrYHIAB8g2Dw
lxKVeu+YVJbCeEyC4yePK+btJxvnRg9lo8+6buM69UjWOUDolE7ucR7z5m2N1gaNGvVVhgxZzLFj
99DS8mpK0aVaQ1grEAQhLQ37nCoENlrXIIoiIV/IVqGtK7TpSnnoBgrq0wmzxfTJdWqdeZ3axDLF
DXCqULq3KlEMCd+ViVogK0ghPEhuZwG2C+CVGA7dRoosDBFjsH0a2o+2Z4wMxo19KkNtbo3UaCSf
dcmwWz9l5Bzb9PYmOi/spPeGXnqv6yXw/QAr2ldoMt5lA1OeW2ve7Dllt9bKqC7iNMGJuu4l39x+
LbcdsimjcPpcMLL2rewPp9iOMw1LkS43IQhCGJ1IlyAIPwPmiaJ4dtzvbgJuF0VxlMo1jke6Ejw0
SbVKnIApo6aw6eVN2uF0g945La/A5MlXqngA/hWYAchEkxfD8N0SCYUK5LxmgGAwaNsvXyyCAAAg
AElEQVRTZ+RZS0pKdPOtedSHMFtEPDt1vQqNAjeccQOPP/R4VMDdfPPdrnuItOCGJ92pqJNWXcP4
8Q/x1lsro7nzZePK6L5BJS1KJyrrVj1YisdSRGq7oFPXZDZf3y7MeBATZImB52F5ORy5SiKSOcec
/MkGJHh4h4yRSHMcroWKT23r6ipiwIAThlPbrCBhP4wMSwy2U0lMQ3ehVtLUuBzap0a82OqeaymV
NK90BZ8aOSSxvidcqHkGOV5baDEKYzd64xbSEX0zc065VWulBqejOrE1HExIf+ZUAZyoYtQZ29i3
7w37Y174IGvWbE6pmfeibDey9kVRNL0/3KrLTXeky2p64WwgKIrim5F/3wj8CNgJ3CiK4lHLAzJm
dE0DXgOuFEXxZUEQzkCq6NgliuKPVa5x3OhSFS6RKdVSBsxsfr1DccaUr7NixUVJBkYA6UTfTmyA
d8GQ5VDzsTqJx29Po0z4AqFQIYdDG+m+rNO2UmDkWfUE9ag/jcJf5Fc03sbtHseF0y9k3cZ10YOk
/aMeAod2IPXmSb2h3bB/uuH04RQvyEOhAQR7tkNRByXDiqKKTVd3F8tfXw6fQTHqIjQKLBi5QFV5
cEvxUNwPTyG1XXAoZddp6CmDKetf53l4ZDQc/Qf4J8PX9yWQ2wgfCkzcMzGrmdLkA3bnzp8gnnm9
IUeR2QL4L32pmveb/TBoW0xROjmZ8aMDvPPOatcMr4VLFvKbZ35D4AJlYqB0K+VO71MjRlxJSYkK
SUBcKumozBumVh1dXiRN0Xov4xvHp9ROWYGVc8rpcgszY7VryNXU3MWyZVMQi/89Jf2ZRh9Dt5TR
vH1P2smmMgHZoH/sd4/RO69Xc+0jYml/uGGAZkt64f1EtFlBEM5FYmx4CRgDPOTM0NQhiuIW4F+A
5wRB6AIOAMeQqOvTAs3CaAHd1CszIV29cL1QdFwhBH0fUE7iAG+FEwMSe1jFoxECH19Ec/MGDhw5
S6J6T6K1t5LSo/asQDSl5VD7Ic1mq1fMvkIxjeT6susRBIEVh1ckhKkDl3wk0WmjlMZhLOyf/PdM
RoUFQSCvJ08nxdJ4IbDf72fp0rvZtm0lQyv30XlpK4Frj3Og6kA0zP/ks0/CZaj2QxFfgv/5/Yeq
FLluUfQqpRT5e/wIHyo/uxcakuoWCSfLEp3mn8U+gdGj5zLvu1cz78x5CXtiQfmCrDa4IEZ4sGDB
O+T1tDu27mXcdlsd77fuhateTGxBceWLvN+6l9tv/4XqtXbkgCwLy4aVadL8pzMd1ul9apQaX7Fn
Vnwq6VYUW6s42VdJC1b7GHm1/1HKewkBb0D4zTA7D++kfHK5I+mtZmnIM9VM2gnjpa7uVoYM/wnM
2ZmS/sw5YY5d0O7oOnXa4HJqDcoG/bK2ZfQOVjG4AAToEros7w9Zb2lq2sD+/atoatrA0qV3Z9VZ
Z9XoGoMU1QKJm/xFURT/Dakm6zInBqYFQRAmAkuRulx+Drg0Mqblbn933Bgc63Gg9xm9Q3HtxrUp
9UR5eX8CekkcoB9Cb0FDmUSzHqdEC40CvFgZYd8TNGu/wmeFqf/NigRl2+jmlZ81pYblu51SXVxj
4rji862VjLeCAQXsHrc75YBnHPD1nRJtfArUWX+Saxsqp1QyZfoUKj9bmZEmvPJ4Kj9byf6PPpLm
RwFWDydVBWlsmO7ibhiIcj+UVqDwTA4ceFGxQaERxeNQoJ2ODv3WCEpIXgutO1qZuGeiJxuS6u0N
RVmiUqfl+9DHpKZJtO39P5qaNvD447/k8Yce93ydlhXIB+z8a3/kuFL23yufhqr9iooSX9/P0y88
nfB5J2uevKSUuzEWo0acYo1G/LmT4TpNq2e82/2PrK6LhPcis72ORIqofw8C3w9YqjlL3hvth9tN
OcCyuZm03++n5FMCKJQ9QOo69UI5jxt9N2U9Qjxb1O1VOyA8wJH94dWInx6sUsZ3AUWR/58J/C7y
/0dQzudyGncCb4qiKEfV3hMEYT6wSRCEWlEUP1a78JZbbuG0005L+N3VV1/N1VdrFVAoo2pmlSm6
Wjk0bCZEbPRQLCkpYenSu1m6FMLhMKNGXUlr6z8B64D4tMMRENwDK7+L/8w/UzKsiODhkwQ+8cHJ
fyDRnYtSuo3Gd/bmD6W5+QUeXXEN//nHTzFs5BDdfPt4pFCRFyIp91uATVA8qJjTS05XpYGV5y+F
PlyubWkBBohQUi89j9zbCPWiyxTq2i7gOWg5tyUhvSVdNOQJ46mOjQeBmPc3ksYweEsZS7abP5wU
6deJ3DtMjBjmK5Hfi3Hfu60QeZEkU+QGg0GOHzoe+3wyROg8XMS0ad+wTTQSJTKxQFntFszWTqTI
kvj98Gf9/QDZewjpwWlaY1EUOSG2qxMKjQtz4pXDiX0QFSitrcqBYDBIx6Gg5t5IV1PSYDBIx+EO
x8Zixoirq7uV116by65dYiw1Xj53RKRejQbuE9+ixGl6drNnvN3r1GC3FiscDie+ly3EoogyBPOt
QBT3ximkNi9hUnp6Ku1Xr8luMxBFkd587chOSAxRc3uNJ1gsnZZlMhL0CDlLQ15bcbJFXvuiKDq6
P4zimWee4ZlnErn+jh8/7sp3qcFqTdcaJJG4GVgEjBFFsVUQhFnAMlEUlYiOjd7bSE3X80C3KIpX
x/1uKvAmUC6K4kGFaxyv6TJCEgGSgbF63Wraj7VzKnSKgacNpKyojOpLqg1tPCs5z1KB50okYsdb
kAwv+TR7mYKCn9Dc/AZf/ep32b2vFAZtgIFDowWgFK2Gmhb1mpKlo6DHb5nGWe+ZKtdU0vy3Zs15
Sckfj+vVFG8kxZoWb8Hn26xadJlS2/A6GaUhV6y1kI3KvUBvMZw8HU7MiRTsvm7q/rr5968jZaiq
0ZavvCmpN5pUK7dt20rOm3keu07tgnNRTqOKXO/rnu0KqUkmc9+tEBPoyZIt67YY6kfVV+FkAbwo
ihSMGkTv/wupfibvvwrpbjmJIAiO1jzJtWo79gyCK1+UIms272kV8prbcXKHat2mlbGYOa+SazQO
dq2nd/4pw3Wa2zZus32+asEqJb0TzaJ176Vz1iYbagf3H4zV2ujNrcGaM91G9R1+SstKTe1XL9ct
KUFzvZ+Cgl8X0Htpr+a7S9czu1FnraiHPQOcBnQgWQpdQCmMHzCed159B8DU/nBzfrKlpusmoAdJ
o/+xKIqy1nYZsNbszQRBKBYEYYogCP8U+dXYyL8rIn//pSAIT8Vd0gBcJQjCPEEQxkQo5JcCbysZ
XG5Bj64WpIW1rGUZLcEWOi/opHdeL53f6aSlukUzlB8fAtard1LyCkipG1uQmiS/jdTDujry84/8
8Idz+fnPH2F3W1OkruFkrK7hqnroCWrUfvmga4hlGmcj3tCevB7zaVnx3rvklKGqHfhP/4wmhXtK
WkyG01sU03TkqNN1wIlhcLQJQkvp7S01nbqgmwYzFQo2FKSkfbA7YsSGkiMMUq1c7eJadp29SyLN
VKQyF6LXh8OzWbNms+Exm01jdeJeZmGF2l9PlvRngwucpTUWBIGivIGa6S1FeQMTo+kO1TzJNOmc
+oO0B3Yn7i2hUbCdUmV0XcvrlK+huE+tjsVMjU5yjUZCKqlGXaNvj4/ZX55t+Xw1CquU9Hap7ONh
RZ4oUXL3ntMrzaeJKKIeVPdGIXAFlA0pM71fs8ngAu31zsvQPatb9d3NuGQmY8bMpKLiCkvlGmbh
Rp21oh4hAJOQDPurpZ/CZ4TouzWyP9xIg/QCPEEZLwjChUh+9eTBPCWK4nWCIPwGqBRF8atx19wI
zEOq5ToGvArcKYriAZXvcKU5cjySrfF5t8xj+aHlUj2MiYhJimdLTis7n4S0Mj2K+VR6zXCk8aQU
6Sk/ayKBS9pUGiULsH4IXH4sZljFR40KApqRMD1PmVOMRQn04Ta8dyneGhHXaci1vDdGWKBYXg4H
JHp/q40B9RpGXl92PQMKB0QjDB/va6en4/qIwZV8gEoNChmyJ/Zuk6nMu4F2PxxvjV5fXl7N/v2r
VOfCSZpjtymTRVFk7OfH2mYuyzZvrxK8/Ayazdh3w7wz50VbUDjJGppIkx6Qak6L1kTZE/35vbTu
2ZGWdZ0ggxX2qb/bT+uOVtOeeDtRHkVafZVzb8b5M1hxeAXh/eG0ZSRYXdN29oIVJkTVLAlZj9iK
bbbXdNO9exVa6z3vlTzNlis8egYcOYD0gQ6ghoKCdxk2bAyFhScdbWHh5vtK0CMsZAgl7w+32s0o
IVsiXQiCkCcIwlxBEBYKglArCMJVgiDkWbmXKIobRVH0iaKYl/TfdZG//yDe4Ir8rl4UxXNFUSwR
RXGkKIrfVzO40oXkRfPks09KkRKTEZMUz5Zc39EKPAnF/12s6zVTbtZ7aTTSU1JSol3XMEkE3wlY
+Sl89QX4/muARFO98iYIboGB2nnMep4ypxiL5CJc4QPBlvcuxVsjoFsQaqXuwqj3xkgxNqcKAMFW
Y0C9Iub7Ft+XEGH48bdvx9d9GakGl1QrV1U1PTGKKUfmrgG+HflZVAqURL9MjdQEnG0y6lbD0kAg
QE3NXYwZM5ORI6vZf+iAbS9yupUUJ1msssE7ef/P72fChxMkAqHk6M6eCdz3H/cBzpIipDZT9Uvp
uUebJOfJ0SZKB3yWkpISrdukwMq6Tsk2UNinJcNKqF1ca/pd2onyJFy7fjTDTxuOf5Mf/+/8DG8Y
nnCfdRvXSQpZGjMSrO5LO445K0QnqlkSET1COC6Yzp5J+WqXCUOyBWrr/cbhNzKsfJjmu6NQplUI
ICWOfZvu7u0cONCgSFClBUuETQk3sP6+EvQIC/tRrsWUYSW6my2wZHQJgvBpYBcSgcZVSKvl98AO
QRDOcm542Yt/+/m/SexvYNoY0Ewr+wEIp/LZ9sY23XC9Lr3mwLC2QBhUBqFWOLKa0zrPwXf8sUgN
T6mk8NvYvHf+5E4KXh6Ukl7Dbh8Fawdxx813qF6b/Ixb129lQfkC8o6Zp1SPn/cUQ1ApvSXycSvF
nh0dHaaUI820hUYfnJhjuzO9GQVJEATq6m5VaE8gRsdRV3erumCXo6URYxH0O8k7KXzdEORyRLm+
firNzRtoa1tDb+fwrFBE4o3F5PQWq/dTWt/LDiwzZdSmI/vC7/fz9itvs2DkgkS6/ZELUvoVOeUg
UqVJl/6KngNCDVbWtaYCJgCn4PBHhy07KOykg8Zf2/rXVjpaOujY28FH73wUvU9JSYlkjICp89UL
mT1mYEVR1jTUInrEmZVnMmnvJNuMgZmie/calNb7I/c9QmG40JDjFB4Afkqs9h5AiBBU3cLChQ8q
3sKsk8ut9yXrETcOv5G83jzD+1HtDFq9YbVyGqSY/pYaTsNqpOsRYA9QIYri50RR/CySitoU+Vu/
x4uvviix94CpiImiwAwhhWyfAp6D4IkAleMn0dbWZng8SrS2enUNnMwHfITDl3Hs2F0MHvyvMWX7
RJVqzZeRzXvPPcvpav+dFDl7ZLSUKheJpHW1P8W99z5h+NlkgTf/mvmqAkX4QGD2RRJDlpqguvMn
dyZGfWTa7h1IrbifQko5/DUMfnOwIcMwnvK9bNwwdozdYVg5UotCsRvy1xYz6oxtmjVqRmFGQVKO
oM5KGEfVzCpVymDZWIw31LQMRidz0N3IZ5drdGIpvNjeG8lwSlGMv0+ysdjautq0ZzUZCcp/F5LM
+h2IfxHZ0bqDC2ZfoHrfTETI4tf9zld3UnVxFWs2rGHixRMTvt9JSmtFmvQIrEasFdd1ZJxa69pO
LYoZB4UdB0MwGIyui1HnjYq+l2AwKBkjoHu+5nXlcfMdN3s++qoGs4qyEUOtkEJHas6yme7dLRjt
QRY7C0HipLtU8WNqdc9WItxuvi+/388j9z1CRVmFIX1X7Qxatux82o58HJM78frvs8Dv4NDhQ5bb
zWQaVtkLO4HzRVHcnvT7KcBmURTN5UekAemo6ZIRzZ0tbpVyW03WdKXk2qsw8ml1OzeSQ65Y1yDn
9u8BwjI7XhWEljBqVDVXXHEha9ZsJhQawOHQRnpmn5B6M5jI24f42gbiHkoer8SC19S0wfCzgCSE
zpt5HrvO2pVAVUujD16sYHz5WF599Q/MmjtLNVd4/QvruXfpvaxat4r2o+2c6DyB2CtKxebxdQUG
cotT8pJ/h+maMzXWtsW1iz1BrqBE06z+HgRoGEjeycmMHFlMdfUFmp3kncxBdyufPbFGR0YASqZC
1a6EekgzzGVO1Z4FAgFqax+goWEz3d3FFBR0UlU1na6uLlasuDBG1R0Hn+9lS4ySUbkl16Amy6wP
YNLeSSnPn878fSUY+X7AEHuinqxSrrUV8fnWqrKqaiFhXSe0y0B6D6NgeMdwWv/amjIuO7UoRtnt
7EDvvcw4fwYr2lcQblGv6RJ2CQx5ewjHZhzLyNpyAmZr5ERR5OY7btas1ZV1Dido9p1kFu1rUHt3
NAINkyC4FSnV/gpgtep9lOqerTIRuv2+9OrE5XHV1NxFff1UxTOIIWdCzcemzxIrSHdNl1Wj6wjw
dVEUtyT9fjrQIIriUIfG5xjSaXRBRAG5tFkqBP4C8C4pC0dNaBotSmQ31FTURDeWWUVNVo7f//T7
saZ2GpTrw/2VtLa+GBXSwWDQ0ubt6OhgxNh/ojMsRgvIJcMu1ktr+PDL+ca/nGVa6Zw3706WP/U+
DPpH3L3nQGgJPt+bnPvFu9l+9ruagmrJwiUxQdkShgrl+dcr0k4Qig4Qc9g5GN0gNdBabwC333U7
T698lhO9JyHko4hhfHfud7n33n81bDA6Rbji9L0govBWXEFrq9JhKZEk5JWu4MzKoYb3hryvnDBC
Ygr+TwmHLyWm4K8jL+9Wuru3ozYZ8U4PI0hQ/k0WUrtBY2wGZr9fqehbybBVK4BPpkkvKDjBnDnT
NR0QWkg4a5Jl94dQsL6A9j3t6mNJkuFVF1fx/GvPc6BKvUQ6HQQJeu/lR2U/4s2332Rn5U7Ev4iK
5+vgNwdLBleG1pZT0FOUk2VxXlcewY5gqrG5x8e43eO4cPqFrNu4znEyIS+T52QKSu+utOBTbH/n
DkTxqsinZgLJzjsZoiJRlhWClZSPuaQXGHESKDssIyisgbmPSjwGLpPkZIvR9Tvgc8APgXcivz4P
WAH8VRTFa50aoFNIt9EVNZxGhiXv4z6kpoFhYCAQHMTQgcPY/pe3GDFiRMK10f4pY3bAWxiKjtjp
5SELhOZ9LXBpWLUvk/+VEXR8sl/xec1Eo6bOmsqOsTtSGvxKvbS2AiIFQ0fQ+7WTppXOxI0cHz2T
Jizv9KJYH5iUh5Dms+riqthh/xSWGRFThKLevUwq/Xpwk6nPzHqLlzFmDUpVr1lEiBsVuoFAgBmz
Z7Bt9DbF9W1VgGseHJHDcu/eDbrRj/j31PFxB4EvB2wfNOqeRBGpdkA5zQ30GSWVEF3vJiO6TigP
dmDn+7UM2wkTHtKNXDmh9NTcXsOjGx6VKJqVoj2NAgtGLtBdM/FjcdpBYQWKY4iL5uX15lE+uJzB
JYM5GjjKkeNHCHWFKCwtZFjRMKpnVbNq/Spaqq2z7HoRRpnehN0CQ94agn+wn578HgrCBcy+YDYb
t25k97jdWRv5y2YkNFxPiHjfheQ1uCzlGqXMA68zR+o5CbQdlgAd5A8ZSU9JQGqP4+L+zRb2whqk
BLStSKbEKSRR+CHwE2eGlt2IsurtE+Ai4FrgeuBiH7RPhCMfc+zgcsXaJbkosWRDOXTpFyV2dHQw
Y/YMU/VC8d8l1zX4S/zKETWQ0qSKgqrPa3RjR3vDyGlnkXFKvbR2SRTKA79H92Wdpp8llR0sdUxi
ocKvZZsgMp/RGgkRy4yIoigS8oUSr9XpO+Nk0bFbTH0yjBbvBwIBbr75bsaOvSSFrMFIHU9CDvop
Yrndf4C8V/IIdYV0n0Wei+0V2yUnRlI/Ijv57Mo1OtLN5Rod3XSzpPcUyA84wsbW0LA5YggkQwB6
iU1CMowTOqT0E2zENLGBFXY2p2D3+2trH2DnzlsSa/oMFMBHb++AQlS3qI6CgwWqa0Y8WzS0ZozW
oqSDIEG1tvk5JM/3NdB7XS8tV7bw3lnvUVpcStv2NroPdBN4P0Dz35t5+J6H6c23x7LrRSSvGTVZ
LI4XOTbjGNWzqqO1ugUDCiSDqw+ywmUD4vtUrV//W8794t3knV6Eb+R9MHQODKxCoo4HrbpnrzNH
6tWJK5MKBaQI15AxMHwivUKIfF9+n9u/lowuURSPiaJYjaQ6fwP4JjBOFMUrRVE85uQAsxUJhpNM
FPHoaIk4ovMtoESzQLJ2cS1CcRBCom6R8LRLp7Ft/zZVg8mIoiaKIiXDijQXeMmwQbYXuBaZAePC
UPwcBaet11Q6V29Q9o5os4NFPhOK/Dm5OPMp4DXwhXyxw17AMm28IAgED59IvFYm5khpFoym0m9l
zo0YRXbepep7FGPrTYus4Utfqua8mefpGoXyPrq+7HoKfl0A5UhRlO9B9w3drGhfoWtEynMhThAl
yuSPkLhWnwGehHObzrXs4ZXZHOF54N+R0kSuAKYzePCd3HHH9YnTkzTnKe/JhqGf/D2JDohkTAde
UvyLUUKHZIOx87udUh92rS2YtGcyrTxY/X7Z2Hzs2fsQz/yRpCgU1iBRP0sw2/jbKkpKSnSpqc0q
J5kmSFB8L1uQggFyhgQkyLRFdYui16reI/Ic8k+vMIlaRSAQ4Lf/81tdgiA3Gn27gWxToK0iEAgw
a+4stp/9Lr3zTxH+fyFY0IMw938pGDqC4cMvTyCoUmojkWnHiFHEk8TFI9FhGamDnlsPNc1wQyvi
gi56wj3Kslkka/evYaNLEISHkv8D5iMRmV8EzI/7fQ5Ih2HpgM/F9WHZBqHBwJVIitklHDrUnsDC
Eq/IBK49DpPCmtGRISVD2HnWTijC1qErCIIuvWlhuFCTcl0PRrzKRUM7GTZySOpnZCPpd7D/yH5V
Bio9drDPjJ2MsFtI8JjKHdP5/+ydeXxU9bn/32cmyWSZCYSACCELUFlEoIsLm9Jb2VwCKu29tbVe
tbdIVdBb63IbUHsJrVu9IJuUSrFWa/0VBGIFAuLCJmq9NpQAYQuBJCgkQGYmZDKZOb8/zpyZc+Ys
c2YySbCX5/Xqy5KZOct3fb7P83k+n3zwur3Y2xTU8+3JTjW71Cx2sk7KCWAl8NssWNSbkUeu1iUX
aA+bW6zNdenvf5swTbimH3XYhb489SU//3mpltkvlAXYX+1i32XWaK5dLhepaakEJgc0GVIrEVpV
W0TrEd0D586fS+jAJQdHztn3IeTdDjnLwXE58EdgO2fPPs2kSXdRV1dn2JeafmrHQV9psQMQD5Oa
+p+G1P9WJAgM9QQdxKUB1NXOQ7z3V67Rgfta4N5ayVG4bYnkOIQPXgJ+f2aHO5JW1u54nZP2aG0l
yzT9koD+T/gaekG2tTDlOp0i/q+Iud1uRk0chdvutrT3d3VW2ci+Ktp+yTTD7ORlIoEbz/O9H32N
ioo1iI5GRowfodsupXNKL3jmSLO+VcnPOEpgqoJ4CqT/DiDif0XP4ZXQLaPbV26cWK7pEgThPYvX
FKOFjC8E6+yaLtkiNR8eYDqSFkME+w/vMGzYwjD2X1M8bMBeKBclulvcEmY9Vh2FBQy+VdaZ9tQK
WakVANTfMWqDIzaGVA1R6eposdKh5w+xg5WXr2L42OE0jm00rJkZfmQ4ewbukdohRvsbOSCiKJKX
dzP17mMaFrtI/dpchg17WVP3kUh9nhLnHwwGKbimwBTvzfI8KRAAlutPlBaTqa4KUjZm0namHtAh
zcjpLzmqFrHaidbddBT23ZiVSlmb6EIQVpNT8FPOXtug6cshVUM403ZGS1jwHkkpHjZjh7LZNvCT
n3yAw5GeMKGDYZ/Ic+YaVOyVRnMmXna2ZFu89zcjeOCATUIz+BZiVAAfbcmq67KydidqXUGQoOqX
AUFpTMVJROR2u7n6+qvZX78fxqNhQBt6aCi7t+zutDqmZLZjeBzuCFre+zuqVi/R9+pq5tJErb39
GKsfCtYW4MpwGdbpObs7CaQEsLfa6e7szrnmc+G6va5mjlTVrVlhhZ3zG5b86Rn9Wnt5L/km8Bm6
PmB7x8kFW9MliuK/WPzfBXfg6kqLZF70xe/gJhX2XxP5VmZHXgX7Sns44rjpL5to8J6RLtMXw+gy
VYQ1qszMCqSkvbVCVqLKmu9Ew0p8wPsQ3B6k8nQl2f27M/Kaq6mrq9PBSmdi75XJ8Kueorx8FX37
9sXZ3WkaMT3jPRNphzRU2amU36dQuK4wZsRXEAQcDh94doa0yAphuQteTIc1heDphcs1X/egE0+9
lCwsmJd3M9mX5JNd1J1+V/fj5PGTppHviCij9foTTf3OQZ2+CT0rg6FtSjM45uo/QLr1iGt7IrTt
ha8Z1vIY9JGqNhEQ0z6gcewp3b7cf9l+PA0e7bPJMNQq2hXB1BeyboL0adh73cb6T//A+m2vUPy9
oVRWvqoVTzexmAKs/wZZO7IsZUm6OqsS7/1jQqQzpYyLzbaR4uKxul9LtjB1R8MBuwLCo+qXt4uw
n7PHPY9dLhfjx46XDlzRa9QgODDoQIfXMXVUJic8DuNAYyQzq5yM9+oIwfqOsmT1o5X9rOFMg7Zd
WkH8WKRxbCM102qovbk2XNPoTHdS+W5lXCLkyTS9thk3ZVzMvnW5XCxY8CSXFuaa7iUp76fAKAyh
xRfSOIllCbEXfhWtqzJdcuZl714vsB2j0EZR0SSOHCmPGZXvW9aXE5+ckGilR09nb12FpGewBYkh
MTqadwj4AGZOn8myBcssPa8Z60x76Z2tRJUBY30rOfJxJXASOI50MPKCzZPCJ+/u5s777zSMruzc
tJPLr788Zuaj8t1K5s6f2y59LG2mQUR+IJtto6EWkpWsTsX7FQrWtDHgHCOl592KYokAACAASURB
VC8LvfNWDKnu1dH4yIXNaMI1/SZnuFqROEwNnpUXiyR4bbTFynRFRVzbE6GNNwtglMl9/KHHeXrB
05RtKeN4/XEC9xoU6SvfO8Z7ula68H7bq302H/AOuJpcZOdmJxzBVNKTy9p6/hu8SYkWWu2TeKPC
XU07bXR/t9vNf/3Xs7y07jkC/+EzvsCyPnDuSlK7baZnvxwcQYcKCdBexkMj+2fXS0o0m9eR7JiW
dNk6IJOj0WczQBsMO6rWMkpWVjlZ79XVzKVWLdn9GOu97S/ZCcyM2l+ShIBIthmiPlZimXkwofYw
uFa8dsFmui5aYuZyudi58y9kZZlXx/v9mQAxo/JpwTQEQaCk5Hn27fsZNP+rBGmqA+5ATRLwaujf
d8DGbRtjPqsoirhcLkrnlFI89k5STg3G/8UI1r+5l5KS5/VrUBRmpRDXSlRZ+Z3C9YXYgrZI0+0k
onuWT6Qm68cQvKmNqyZcZRpdmTt/rqXMR3Z2ti77TvSByyxooc00RA5cRnUzVrM6v/jFc5F6Kccc
LR56LLrZEg6E4G++6Mi3ef2Jbv3OvwIpmD4r6W50G/v8CIRD+j9Mdt1PPFkAo0zu4uOLGfCNAdLf
i6sJdDNnRSPdDwQhvdX0e86eTv1nO25jWMYwav9eq8v+JFusoJnL5WLhwqc4enQz371jIIEbzyct
Wmi1T+I9QHV1YbQeacbMh2aS+7VLWLJmGYHzBsXdIDFs+k7C9DL8M1uoL67XIAHktTtRxkMji8UY
9lW3RLJ5HVHHFE/G45EnHmHvwPhZhWOZKoMfhYaR937XdpfmMJCsrHIyMlQXao2ZniXyvmbPbbZ2
CocE0rula9slgZrGzjDdtoG4eAYSag+Da13odvHQ1QmWnZ1Nr152zDx9maLZqiOzbt0HBFPfgYx1
sEGQejIdNUnAnaF/p4NP8OkOyugNpPAbhRQNGcbixSM5dmyLinFu1KjbtDToSrM4+K04B/J3qj+r
pqBHQaTpapAyXHqQtssgmBU0PRSu27wubgdel7lMBxqkJESR32HXrtU88MBuioomkZc3TcVIpLfB
WYXDvf32zggdeGaZlOFSmrwR10LK8hTy3s4jZWm6lOEK1RtFX9iMJlz3sJ1OJKpl9KxBLzbbRsWX
gthsGxhS5GbIwSGWHahE4VNyIMGqo2FY4Fwv4pvok/5uw5zsogVoboKcgeA3h3k6cMR8NiPmvHhh
LslmLutqhruONrfbzT333UP3wu4sP7Uc/09b4N4GGBYwhHOxAbhJND3YGlP56zMeJqilGfdvLnRL
5MCQbHbMeOD1breblW+stOwox9vPqn0siiDINsbG3bffrdsmyTicJ2Mt6Wrm0njM6vtaXZt1186g
tHZefvhycjNz1e0ikhRW244w3bYRiIsQymwv0W0Pk2td6Hbx0NVJFotVT6ZotuLINDU1Uef+TKLX
fLAGfhqAZtSDUjn+RDh94gwej1pnS28DqZlWQ+P4WsSsJ5DIP6SLBYNT2L//Z1oadKVFDX4rC4CV
iRLeXOSF5zj6G5kI6LFkRzEfrtu0ju7buifkLGpp0P9Idf3lLPrjcnKHX0LhNwpVi6wy03D8+FpL
dTNWDoUROnCT+qjQRty7X29qdtfw0+8/is1/A9oDl5YmXNl3phFJk3oC4aDAj39wFzNmfIjLNRK7
fQR2+7VkZc1l/Phr2PLWFssOVDwOl97GVzKvhNI5pTEdDcPNNTrKaPTePiTywpvcEqwwBvvo1IlT
43KCEq2p7IioclfXYnWkyQQMv3/z9wRvDKpZMw2yyLZDNlK/MNbLkp0zcyp/KePc1NT0f47RzYol
cmCItZ4WTyi2dG9ZYN2qHuYv/vsX+LPM55xP9CXcz4a+wmHrQY9EHNVkriVdzVxqxay+b1NTk+W1
WSmF4lrpwv6SHfsqO1nbsxg3ahw3fPsGdbvEeYiJ9/0StUR9g+i+jbWXTJs47YIfJ1btYk1XJ5mW
VU8NNVNmPqzUVS2qXSQ5ArKZ4H3ZL8DaYmbP+Ea4hkgURR587EGLLFyyibh6FeKdUmuIq5/Rawap
bZdQVrYDvz+L1FQvxcVjmT//5wk7YSrM8PagdJgwYrF6BTWTkwHeXWYBcnV3aVh/nE6n4eKlrtMK
aUsoa6mCYDvaPry+Fdz9iBG3hlgxBcv1UbHGYHn5qnDNUjQr5YjxI+JiqqMKhh4eypa3tjBp0l0x
61es1vHI3zOru0kUe2/IdCgiUdQqx5xRHcVbwBVE5maC7JdG1p6ayo5iLgtfootrsZJpsx+dzaLy
RdCIfl2CDwnq/I8USOuNva2R/7j9Tl7d8CrNP2w2vG7e23mknBrMsWNbdC4KIFJQ8C+4+p7+yjG6
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
<div class="prompt input_prompt">In&nbsp;[21]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span></span><span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">stats</span><span class="p">[</span><span class="mi">2</span><span class="p">]</span><span class="o">.</span><span class="n">train_acc_history</span><span class="p">,</span> <span class="s1">&#39;-o&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">solver</span><span class="o">.</span><span class="n">train_acc_history</span><span class="p">,</span> <span class="s1">&#39;-o&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">stats</span><span class="p">[</span><span class="mi">2</span><span class="p">]</span><span class="o">.</span><span class="n">val_acc_history</span><span class="p">,</span> <span class="s1">&#39;-o&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">solver</span><span class="o">.</span><span class="n">val_acc_history</span><span class="p">,</span> <span class="s1">&#39;-o&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;iteration&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;loss&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">legend</span><span class="p">([</span><span class="s1">&#39;No BN train ACC&#39;</span><span class="p">,</span> <span class="s1">&#39;BatchNorm train ACC&#39;</span><span class="p">,</span> <span class="s1">&#39;No BN val ACC&#39;</span><span class="p">,</span> <span class="s1">&#39;BatchNorm val ACC&#39;</span><span class="p">],</span> <span class="n">loc</span><span class="o">=</span><span class="s1">&#39;upper right&#39;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[21]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>&lt;matplotlib.legend.Legend at 0x7fe52d04a6d0&gt;</pre>
</div>

</div>

<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAA1YAAAKvCAYAAABptl4OAAAABHNCSVQICAgIfAhkiAAAAAlwSFlz
AAAPYQAAD2EBqD+naQAAIABJREFUeJzs3XlY1WX+//Hn5yAqIO6JZC64jFrpzwFzyVRyGY1EHdwN
NXWyMsXMplIpBZeWUUlnMtMsNEFSc0GzHM20vpragKRN5liKTeaKCicXFLh/fxBnPLKvWr0e1/W5
Lj735/7c9/tzOFzXeXMvxzLGICIiIiIiIkVnu9UBiIiIiIiI/NopsRIRERERESkmJVYiIiIiIiLF
pMRKRERERESkmJRYiYiIiIiIFJMSKxERERERkWJSYiUiIiIiIlJMSqxERERERESKSYmViIiIiIhI
MSmxEhERERERKabbJrGyLOspy7KOWZZ1xbKsPZZl3ZdP/SqWZb1hWdZPv9zzrWVZPcsqXhERERER
kSzlbnUAAJZlDQLmAmOAfcBEYItlWX8wxpzLob4rsA04BQQBPwH1gYtlFrSIiIiIiMgvLGPMrY4B
y7L2AHuNMRN+ObeA/wILjDGv5VD/CWAS0MwYk16mwYqIiIiIiNzklk8F/GX0yQ/4JKvMZGZ724D2
udwWCHwBLLQs65RlWQcty5psWdYtfx4REREREfn9uR2mAtYEXIDTN5WfBprmck9DoAuwAngIaAIs
/KWdmaUTpoiIiIiISM5uh8QqNxaQ2zxFG5mJ15hfRrf2W5ZVB3iWXBIry7JqAD2AROBqiUcrIiIi
IiK/FhWBBsAWY0xSSTR4OyRW54B0wOum8lpkH8XKchK4ZpwXiB0CaluWVc4Yk5bDPT2AqOIGKyIi
IiIivxmPANEl0dAtT6yMMdcty4oDugKx4Ni8oiuwIJfbdgFDbiprCpzMJamCzJEqVqxYQfPmzYsb
tkieJk6cSERExK0OQ34H9F6TsqL3mpQVvdekLBw6dIjg4GD4JUcoCbc8sfrFPGDZLwlW1nbr7kAk
gGVZy4EfjTFTfqn/JjDOsqz5wD+APwCTgdfz6OMqQPPmzfH19S2NZxBxqFKlit5nUib0XpOyovea
lBW916SMldgSodsisTLGrLIsqyYQTuaUwASghzHm7C9V7gLSbqj/o2VZfwIigK+AE7/8nG1rdhER
ERERkdJ2WyRWAMaYhWTu7JfTtS45lO0F7i/tuERERERERPKj730SEREREREpJiVWIqVgyJCb91YR
KR16r0lZ0XtNyorea/JrZTnvWP7bZVmWLxAXFxenBZEiIiJSKD/88APnzp271WGISAHVrFmTevXq
5Xo9Pj4ePz8/AD9jTHxJ9HnbrLESERERuR398MMPNG/enMuXL9/qUESkgNzd3Tl06FCeyVVJU2Il
IiIikodz585x+fJlfRemyK9E1ndUnTt3TomViIiIyO1G34UpInnR5hUiIiIiIiLFpMRKRERERESk
mJRYiYiIiIiIFJMSKxERERERkWJSYiUiIiIiUgwNGjRg1KhRtzoMucWUWImIiIj8ji1btgybzYa7
uzsnT57Mdt3f35+WLVuWWH9hYWHYbDbH4eLiwp133klgYCB79+51qnv8+HFHvXXr1mVra/r06dhs
Ns6fP59nn1988QVhYWGkpKSU2HPcyGazYVlWqbT93HPPYbPZGDJkSJ717HY7YWFhtGrVCk9PT9zd
3WnRogWTJ0/O8fe6Y8cOgoKC8Pb2pkKFCnh5edG7d+8cX2cpGG23LiIiIiKkpqbyyiuvMH/+fKfy
0kgYLMti0aJFeHh4kJGRwX//+18WL15M586d2bdvX7ZEzrIswsPD+fOf/5ytvCDx7d69m/DwcEaO
HEnlypVL9FkADh8+jM1WOuMVMTEx+Pj4sHHjRi5duoSHh0e2OkePHqVbt278+OOPDBgwgMcffxxX
V1cOHjzI0qVLWbduHd9++62j/vTp0wkPD+cPf/gDTzzxBPXr1ycpKYnNmzfTv39/oqKiGDx4cKk8
z2+ZEisRERGREmaMKbURjNJqu1WrVixZsoTJkydTu3btEm//Zv369aN69eqO8z59+nDvvfeyevXq
bIlVq1atSEhIYP369fTt27fQfRljClX32rVrVKhQocD3uLq6Fjqmgvj00085ceIEn376Kd27d2ft
2rUMGzbMqU56ejpBQUGcPXuWnTt30r59e6frs2bN4tVXX3Wcr1mzhvDwcAYOHEhUVBQuLi6Oa5Mm
TWLr1q1cv369VJ7nt05TAUVERERKgN1uJyRkGj4+3ahbty8+Pt0ICZmG3W6/rduGzJGfKVOmkJaW
xiuvvJJv/fT0dGbMmEHjxo2pWLEiPj4+hIaGcu3atSLH4OXlBUC5ctn/7z948GCaNGlCeHh4odsN
CwvjueeeAzLXQmVNP/zhhx+AzGl8ISEhREdHc++991KxYkW2bNkCwJw5c+jQoQM1a9bE3d2d1q1b
88EHH2Tr4+Y1VlnTK3fv3s0zzzxDrVq1qFSpEkFBQSQlJRU49qioKO6++246depEt27diIqKylZn
zZo1HDhwgNDQ0GxJFUClSpWYMWOG4/zFF1+kRo0aLF261CmpytK9e3cCAgIKHKP8jxIrERERkWKy
2+20b9+PN95oT2LiVk6c2EBi4lbeeKM97dv3K1YCVJpt38jHx4fhw4ezZMkSTp06lWfd0aNHM23a
NFq3bs3rr7+Ov78/s2fPzncd0I2SkpJISkri7Nmz7N+/n8ceeww3NzcGDhyYra6LiwuhoaGOUavC
6NevnyOu+fPns2LFCt577z3uuOMOR51PPvmESZMmMXjwYObPn0+DBg0AWLBgAb6+vsyYMYOXX34Z
V1dXBg4cyEcffeTUR24jiOPHj+fgwYNMnz6dsWPHsnHjRsaNG1eguK9du8batWsZOnQoAEOGDGH7
9u2cOXPGqV5sbCyWZREcHJxvm9999x2HDx/mz3/+c45TCqV4NBVQREREpJimTp3DoUPPkJHR84ZS
i4yMnhw6ZAgNncv8+dNvu7az9zWV5cuX8+qrrxIREZFjnQMHDrB8+XLGjBnDokWLAHjiiSe44447
mDt3Ljt37qRz58559mOMoWnTpk5l1apVY/369TRv3jzHe4YOHcqMGTMIDw8v1HTAe++9F19fX2Ji
YujTpw/16tXLVuc///kPX3/9dbaYjhw54jQlcNy4cfzxj39k3rx5PPTQQ/n2fccdd/Dxxx87ztPT
0/n73/+O3W7H09Mzz3s3btxIcnIygwYNAqBv376MGTOGmJgYQkJCHPW+/fZbqlSpQp06dfKN59Ch
Q0DmayIlTyNWIiIiIsW0ceMuMjJ65HgtI6Mna9bsIj6eIh1r1uTddmzsrhJ7Dh8fH4YNG8bixYs5
ffp0jnU2b96MZVlMnDjRqXzSpEkYY/jwww/z7ceyLNatW8e2bdvYunUrkZGR/OEPfyAoKIg9e/bk
eI/NZnOMWm3YsKHwD5cHf3//bEkV4JRUXbx4kQsXLtCxY0fi4+PzbdOyLMaMGeNU1rFjR9LT0zl+
/Hi+90dHR9O6dWsaNmwIZE7pe/jhh7NNB0xJSck3SbuxLlDg+lI4GrESERERKQZjDNevewC5bShh
8dNP7vj5mTzq5No6kHfb16+7l+iGFqGhobz33nu88sorOY5aZW2B3rhxY6dyLy8vqlatWqCkATKT
jBs3r+jXrx9NmjRh/PjxfPnllzne88gjjzBz5kzCw8Pp06dPIZ4qb1lT/262adMmZs2aRUJCAqmp
qY7ygu4AWLduXafzatWqAXDhwoU870tOTmbz5s2MHz+e77//3lF+//33s3btWr777jvH61+5cmWO
HTtWoHiydkQsqemj4kyJlYiIiEgxWJaFq+slMpOgnJIbg7f3JTZtKkriY9Gr1yVOnsy9bVfXSyW6
S6CPjw/BwcEsXryY559/PnuPv+ywV9I7E3p4eNC2bVtiY2O5cuUKbm5u2erYbDamTp3KyJEjiY2N
LbG+c+rr888/p0+fPvj7+/Pmm2/i7e2Nq6sr77zzDitXrixQuzltDgH571K4atUqUlNTmTt3LnPm
zHG6ZlkWUVFRTJs2DYBmzZqRkJDAiRMn8p0O2KxZMwAOHjxYoPilcDQVUERERKSYAgM7YLNtyfGa
zfYxAwY8gK8vRTr698+77d69Hyjx5wkNDeX69etO23RnadCgARkZGRw5csSp/MyZM1y8eJH69esX
ud+0tDQAfv7551zrBAcH06hRI8LCwgq8jXpRksC1a9fi5ubGli1bePTRR+nRowddunQp1NbtRRUd
HU2LFi1YvXo1a9ascTq6du3qNB0wMDAQYwwrVqzIt90mTZrQtGlTNmzYwOXLl0vzEX6XlFiJiIiI
FNOsWc/SvPk8bLaPyBy5AjDYbB/RvHkEM2dOui3bzk3Dhg0JDg7mrbfeyrZDYEBAAMYYXn/9dafy
uXPnYlkWDz/8cJH6PH/+PLt378bb29tpx76bZa212r9/f4FHrbJ2wLt48WKB43FxccGyLEeyB5CY
mFji67tu9uOPP/LZZ58xaNAggoKCsh0jR47k+++/d0yX7N+/Py1atGDWrFk5rk+z2+2EhoY6zsPC
wjh37hyjR48mPT09W/2tW7cWaJ2cZKepgCIiIiLF5OnpyRdffEBo6FxiY+dx/bo7rq6X6d27AzNn
flCszQJKs+0sOY3CTJ06lffee4/Dhw877SLXsmVLRowYweLFi7lw4QKdO3dm7969LF++nKCgoHx3
BMzqb/Xq1VSqVAljDCdOnOCdd97h4sWLOY6S3Sw4OJiZM2eSkJBQoNEoPz8/jDFMmTKFwYMH4+rq
Su/evXOcApilV69ezJs3jx49ejB06FBOnz7NwoULadKkCQcOHCjQMxamPEvWaFRgYGCO1wMCAnBx
cSEqKor77ruPcuXKsXbtWrp3706nTp0YOHAgHTp0wNXVlX//+99ER0dTvXp1Zs6cCcDAgQM5ePAg
s2fPZv/+/QwZMoT69euTlJTExx9/zPbt24mOjs73+SQ7JVYiIiIiJcDT05P586czfz4luplEabcN
OU+Va9SoEcOGDWPZsmXZri9dupRGjRoRGRnJ+vXrqV27NlOnTuWll14qcH9jx451nHt4eNCyZUte
fvllgoKCstW9uf+stVajRo0q0GvRunVrZs6cyaJFi9iyZQsZGRkcO3aMevXq5dg+ZO4U+M477/DK
K68wceJEfHx8eO211zh27Fi2xCqnNnKLK794o6OjqVevHi1atMjxepUqVXjggQd4//33mTdvHjab
jUaNGpGQkEBERATr1q1jw4YNZGRk0LhxY8aMGcP48eOd2pgxYwZdu3ZlwYIFLFq0iPPnz1OtWjXa
tWtHbGxskUcdf++sspgnejuwLMsXiIuLi8PX1/dWhyMiIiK/EvHx8fj5+aHPECK/DgX5m82qA/gZ
Y/LfP78AtMZKRERERESkmJRYiYiIiIiIFJMSKxERERERkWJSYiUiIiIiIlJMSqxERERERESKSYmV
iIiIiIhIMSmxEhERERERKSYlViIiIiIiIsWkxEpERERERKSYlFiJiIiIiIgUkxIrERERERGRYlJi
JSIiIiK3lWXLlmGz2YiPj7/Vofxm7Ny5E5vNxmeffXarQ/nNUmIlIiIi8juWlcTceHh5edGlSxc+
/vjjIrf78ssvs2HDhiLfb1lWger5+/tjs9no06dPtmvHjx/HZrMxb968IsdRlt58802WLVtWau0X
9DUtrIyMDLy9vbHZbGzZsiXPugkJCQQHB1OvXj0qVqxIjRo16N69O5GRkWRkZDjVTU1NJSIignbt
2lG1alXc3Nxo2rQp48eP58iRI6XyLMVR7lYHICIiIiK3lmVZzJgxgwYNGmCM4fTp00RGRhIQEMCm
TZsICAgodJuzZ89mwIABOSY8JcmyLCzLYtOmTezfv58//vGPpdpfaVq4cCF33HEHI0aMKPG2O3fu
zJUrVyhfvnyJt719+3ZOnz6Nj48PUVFR9OjRI8d6b7/9Nk8++SS1a9dm2LBhNGnSBLvdzvbt2/nL
X/7CqVOneOGFFwBISkqiR48e7N+/n169evHII49QqVIlDh8+TExMDEuWLOHq1asl/izFocRKRERE
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
8/Nj27ZtREREcOedd+Lj40ObNm2YPXs2W7dupVOnTowZM4bmzZvz008/sWbNGnbt2uW03Xpusean
cuXKTJgwgbCwsGyJ1QsvvMDKlSvp2bMnISEhVK9encjISI4fP87atWsL9ZqVND8/PxYtWsSsWbNo
3LgxtWrV4sEHH8yzv169evHee+9RuXJl7r77br744gs++eQTatasWaoxR0VF0apVq1y3T+/duzfj
x48nISGBVq1a0b59e9544w2eeuopmjVrxrBhw2jSpAl2u50dO3YQGxvLrFmzHPcvX76cHj160K9f
Px5++GG6deuGh4cHR44cISYmhlOnTjmN0uVmv93OhO++4/PkZPCuBXv3QLv2+d5XFEqsREREREqA
p6cn81+dz3zml8hmEmXVNmSOJE2bNs1xXrFiRZo1a8aiRYt47LHHHOX+/v688847vPLKK0ycOBEf
Hx9ee+01jh07li2xmjdvHo8//jgvvvgiV65cYcSIEbRp04Y777yTvXv38uKLLxIdHU1KSgp16tQh
ICDA6Ytjc3vGnMpzKnv66aeZP39+tg0catWqxRdffMHzzz/PP/7xD65evUrLli3ZtGkTPXv2zLfd
glwrav2XXnqJH374gb/97W/Y7XY6d+7sSKxyu3/BggWUK1eO6Ohorl69ygMPPMC2bdvo0aNHjt9b
VdC48op3//79/Oc//+Gll17KtU5gYCAhISGsWLGCVq1aATBmzBjatGnD3Llzee+99zh79iyVKlXC
19eXZcuW8cgjjzjur1mzJrt372bhwoWOL2m+du0a9evXp2/fvoSEhOTad5bwY8eITUnB7doZ+PY1
6lpn+O/b8WCegeo18r2/sKzSyLZvR5Zl+QJxcXFxTjveiIiIiOQlPj4ePz8/9BlC5Nch62+23KK/
k2bbTrNr/yGixxw6eHWgTdc2fJvxI1yoCEfPAfgZY0pkXqrWWImIiIiIyG9OxcOz+Pv/68KBJ/bT
s3FPPD092ffJPkK6jsK7vGuJ96fESkREREREfnNi+0czrs04XF3+l0RlTavdFFW0rz/IixIrERER
ERH5zalSsUqZ9qfESkREREREpJiUWImIiIiIiBSTEisREREREZFiUmIlIiIiIiJSTEqsRERERERE
ikmJlYiIiIiISDEpsRIRERERESkmJVYiIiIiIiLFpMRKRERERESkmJRYiYiIiIgUQmRkJDabjR9+
+OFWhyKFZLfbmRYSwhO9epV420qsRERERH7Hli1bhs1mw93dnZMnT2a77u/vT8uWLUusv7CwMGw2
m+NwcXG2F3NNAAAgAElEQVThzjvvJDAwkL179zrVPX78uKPeunXrsrU1ffp0bDYb58+fL7H4CsKy
LCzLKtQ9zz33HDabjSFDhuRZz263ExYWRqtWrfD09MTd3Z0WLVowefLkHH8/O3bsICgoCG9vbypU
qICXlxe9e/fO8fX6vbPb7fRr3572b7zBmzm8lsWlxEpERESkhBljfnVtp6am8sorr2QrL2wCURCW
ZfHWW2+xYsUKli1bxvjx4/n666/p3LkzBw4cyLF+eHh4juWlEV9piImJwcfHh40bN3Lp0qUc6xw9
epT/9//+H7NmzeKee+7htddeY8GCBXTp0oWlS5fy4IMPOtWfPn06Xbp04ZtvvuGJJ57grbfe4rnn
nuPSpUv079+fmJiYsni0X405U6fyzKFD9MzIoDTeNeVKoU0RERGR3x273c6cqVPZtXEjHtevc8nV
lQ6BgTw7axaenp63bdtZWrVqxZIlS5g8eTK1a9cukTbz0q9fP6pXr+4479OnD/feey+rV6/ONkLW
qlUrEhISWL9+PX379i312Erap59+yokTJ/j000/p3r07a9euZdiwYU510tPTCQoK4uzZs+zcuZP2
7ds7XZ81axavvvqq43zNmjWEh4czcOBAoqKicHFxcVybNGkSW7du5fr166X7YL8yuzZuZHpGRqm1
rxErERERkWK6cYrR1sRENpw4wdbERNq/8Qb92rfHbrfflm1nsSyLKVOmkJaWluOo1c3S09OZMWMG
jRs3pmLFivj4+BAaGsq1a9eKHIOXlxcA5cpl/7//4MGDadKkSY6jVvlZs2YNNpuN//u//8t2bdGi
RdhsNg4dOgTAwYMHGTlyJI0aNcLNzQ1vb29Gjx5d7KmGUVFR3H333XTq1Ilu3boRFRWVY5wHDhwg
NDQ0W1IFUKlSJWbMmOE4f/HFF6lRowZLly51SqqydO/enYCAgGLF/VtijMHDbi+VkaosSqxERERE
iimnKUYW0DMjg4mHDjE3NPS2bPtGPj4+DB8+nCVLlnDq1Kk8644ePZpp06bRunVrXn/9dfz9/Zk9
e3a+64dulJSURFJSEmfPnmX//v089thjuLm5MXDgwGx1XVxcCA0NdYxaFUavXr2oVKkS77//frZr
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
7VhH++/a89qU1yhboAo3XjKQvjtyknNHxOuVK3NnsWJkTuTqURSFValHHoFff4X774f27aFQocTN
sY/kZHjjDejUKZQM/vOf8OijVqdLknQkM1hJSjeSU5J5ZeIrdBzVkQi46ew3GZW5Gp9sT+ZfJYrT
tmxZ8iZ6f9ykSaGYYswYuOQS+PbbcMDpIEhNDddePf54qE6/9daw47B06YMynSRJOoQMVpIOuyiK
6P9Lf5oPac6CjQu4umErlh93Bb227uDSvMcypEIFKid6f9yyZWGZ6MMPoWbN0Px33nmJnWMfw4aF
6vSpU+Gyy+Drr6FGjYM2nSRJOsQMVpIOq59X/0yzIc0YtnAYZ1RsTO3Te/H5pl1UTYFBtWpxQaL3
x23bBk8+GQ425c4dGiPuvBMyZ07sPL+ZOjVUpw8dCiefDKNHh4JBSZJ0dDFYSTos1m5fS/uR7Xl9
yuuUL1CZOy4bxOfbc5Jp216er1iR+4sXJ0umTImbMCUFevUK+/A2bAjb/1q3hjx5EjfHPhYsCNXp
H38MVavCV1/B5ZdbnS5J0tHKYCXpkEpOSealCS/xxOgnIBbjjnPeZOQxx/Pell3cX7wIHcuVo2CW
LImd9LvvQpCaPh1uuAG6dYOyZRM7x2/WrAnV6a+9BscdB2++CbfdZnW6JElHO/+ql3RIRFFEv1/6
0XxIcxZuXMh1DVqyutg1vLV5G+fkys6X1WtQ89hjEzvpvHnQsmU40HTiiTBuXNiPdxBs3QrPPht2
GGbObHW6JEkZjcFK0kH30+qfaDa4GcMXDadRxcs48cwP+HjDLsru3kvfGjVoXLAgsUTukdu4MXSZ
v/wyFC8OffrA9dcflH14yclhVapTJ9i82ep0SZIyKoOVpINmzfY1tPuuHW9OfZMKBSpzf+NBfLI9
F5M376Fr+fL8q2RJsiXyHNWePdCzJ3TsGBJPp07QtCnkyJG4OX7ze3V6mzawcGGoTu/Y0ep0SZIy
KoOVpITbvXc3L00M56gyxTJx7zlvMDpLTV7bvIPbixaiS7lyFM2WLXETRhH07w8tWsD8+aHl74kn
oEiRxM2xj32r0y+9NBRT1Kx5UKaSJElHCIOVpISJooiv535NiyEtWLxpMU0atmB9sevouWkLp+Y4
hkn161M/d+7ETjp9OjRvDiNGwLnnwmefQa1aiZ3jN1anS5Kkv5PAPTiSMrKfVv/EOb3O4cpPrqRs
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
rkJggg==
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[22]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Maybe we didn&#39;t run enough training?</span>
<span class="c1"># Try more epochs</span>
<span class="n">layers</span> <span class="o">=</span> <span class="p">[</span>
  <span class="p">[</span><span class="s1">&#39;conv&#39;</span><span class="p">,</span>  <span class="p">{</span><span class="s1">&#39;num_of_filters&#39;</span><span class="p">:</span><span class="n">f</span><span class="p">,</span> <span class="s1">&#39;filter_size&#39;</span><span class="p">:</span><span class="mi">3</span><span class="p">}],</span>
  <span class="p">[</span><span class="s1">&#39;relu&#39;</span><span class="p">],</span>
  <span class="p">[</span><span class="s1">&#39;pool&#39;</span><span class="p">],</span>
  <span class="p">[</span><span class="s1">&#39;spatial_batchnorm&#39;</span><span class="p">],</span> <span class="c1"># normalize before affine</span>
  <span class="p">[</span><span class="s1">&#39;affine&#39;</span><span class="p">,</span> <span class="p">(</span><span class="mi">500</span><span class="p">)],</span>
  <span class="p">[</span><span class="s1">&#39;relu&#39;</span><span class="p">],</span>
  <span class="p">[</span><span class="s1">&#39;batchnorm&#39;</span><span class="p">]</span> <span class="c1"># for last affine layer</span>
<span class="p">]</span>

<span class="n">model</span> <span class="o">=</span> <span class="n">convnetGenerator</span><span class="p">(</span><span class="n">layers</span><span class="o">=</span><span class="n">layers</span><span class="p">,</span> <span class="n">weight_scale</span><span class="o">=</span><span class="mf">0.001</span><span class="p">,</span> <span class="n">reg</span><span class="o">=</span><span class="mf">0.001</span><span class="p">)</span>

<span class="n">solver</span> <span class="o">=</span> <span class="n">Solver</span><span class="p">(</span><span class="n">model</span><span class="p">,</span> <span class="n">data</span><span class="p">,</span>
                <span class="n">num_epochs</span><span class="o">=</span><span class="mi">10</span><span class="p">,</span> <span class="n">batch_size</span><span class="o">=</span><span class="mi">50</span><span class="p">,</span>
                <span class="n">update_rule</span><span class="o">=</span><span class="s1">&#39;adam&#39;</span><span class="p">,</span>
                <span class="n">optim_config</span><span class="o">=</span><span class="p">{</span>
                  <span class="s1">&#39;learning_rate&#39;</span><span class="p">:</span> <span class="mf">1e-3</span><span class="p">,</span>
                <span class="p">},</span>
                <span class="n">verbose</span><span class="o">=</span><span class="bp">True</span><span class="p">,</span> <span class="n">print_every</span><span class="o">=</span><span class="mi">100</span><span class="p">)</span>
<span class="n">solver</span><span class="o">.</span><span class="n">train</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>(Iteration 1 / 9800) loss: 2.312011
(Epoch 0 / 10) train acc: 0.139000; val_acc: 0.141000
(Iteration 101 / 9800) loss: 1.800229
(Iteration 201 / 9800) loss: 1.651026
(Iteration 301 / 9800) loss: 1.893823
(Iteration 401 / 9800) loss: 1.465016
(Iteration 501 / 9800) loss: 1.716302
(Iteration 601 / 9800) loss: 1.418364
(Iteration 701 / 9800) loss: 1.624111
(Iteration 801 / 9800) loss: 1.590870
(Iteration 901 / 9800) loss: 1.660085
(Epoch 1 / 10) train acc: 0.578000; val_acc: 0.528000
(Iteration 1001 / 9800) loss: 1.756186
(Iteration 1101 / 9800) loss: 1.865406
(Iteration 1201 / 9800) loss: 1.547603
(Iteration 1301 / 9800) loss: 1.560186
(Iteration 1401 / 9800) loss: 1.582535
(Iteration 1501 / 9800) loss: 1.724063
(Iteration 1601 / 9800) loss: 1.365690
(Iteration 1701 / 9800) loss: 1.596534
(Iteration 1801 / 9800) loss: 1.445190
(Iteration 1901 / 9800) loss: 1.531936
(Epoch 2 / 10) train acc: 0.644000; val_acc: 0.605000
(Iteration 2001 / 9800) loss: 1.611134
(Iteration 2101 / 9800) loss: 1.374546
(Iteration 2201 / 9800) loss: 1.486211
(Iteration 2301 / 9800) loss: 1.184432
(Iteration 2401 / 9800) loss: 1.462766
(Iteration 2501 / 9800) loss: 1.394436
(Iteration 2601 / 9800) loss: 1.385071
(Iteration 2701 / 9800) loss: 1.508776
(Iteration 2801 / 9800) loss: 1.769226
(Iteration 2901 / 9800) loss: 1.571395
(Epoch 3 / 10) train acc: 0.683000; val_acc: 0.624000
(Iteration 3001 / 9800) loss: 1.558630
(Iteration 3101 / 9800) loss: 1.433534
(Iteration 3201 / 9800) loss: 1.381232
(Iteration 3301 / 9800) loss: 1.243681
(Iteration 3401 / 9800) loss: 1.483883
(Iteration 3501 / 9800) loss: 1.467480
(Iteration 3601 / 9800) loss: 1.242238
(Iteration 3701 / 9800) loss: 1.526186
(Iteration 3801 / 9800) loss: 1.397907
(Iteration 3901 / 9800) loss: 1.572212
(Epoch 4 / 10) train acc: 0.708000; val_acc: 0.620000
(Iteration 4001 / 9800) loss: 1.283835
(Iteration 4101 / 9800) loss: 1.384965
(Iteration 4201 / 9800) loss: 1.177130
(Iteration 4301 / 9800) loss: 1.633236
(Iteration 4401 / 9800) loss: 1.355671
(Iteration 4501 / 9800) loss: 1.250904
(Iteration 4601 / 9800) loss: 1.174688
(Iteration 4701 / 9800) loss: 1.523482
(Iteration 4801 / 9800) loss: 1.478957
(Epoch 5 / 10) train acc: 0.769000; val_acc: 0.648000
(Iteration 4901 / 9800) loss: 0.954473
(Iteration 5001 / 9800) loss: 1.268360
(Iteration 5101 / 9800) loss: 1.401886
(Iteration 5201 / 9800) loss: 1.410911
(Iteration 5301 / 9800) loss: 1.145333
(Iteration 5401 / 9800) loss: 1.247879
(Iteration 5501 / 9800) loss: 1.419671
(Iteration 5601 / 9800) loss: 0.891581
(Iteration 5701 / 9800) loss: 1.556425
(Iteration 5801 / 9800) loss: 1.352331
(Epoch 6 / 10) train acc: 0.758000; val_acc: 0.664000
(Iteration 5901 / 9800) loss: 1.160467
(Iteration 6001 / 9800) loss: 1.053299
(Iteration 6101 / 9800) loss: 1.297573
(Iteration 6201 / 9800) loss: 1.108562
(Iteration 6301 / 9800) loss: 0.976720
(Iteration 6401 / 9800) loss: 1.025000
(Iteration 6501 / 9800) loss: 0.972647
(Iteration 6601 / 9800) loss: 1.125813
(Iteration 6701 / 9800) loss: 0.997228
(Iteration 6801 / 9800) loss: 1.126960
(Epoch 7 / 10) train acc: 0.773000; val_acc: 0.648000
(Iteration 6901 / 9800) loss: 1.148099
(Iteration 7001 / 9800) loss: 1.062083
(Iteration 7101 / 9800) loss: 0.988627
(Iteration 7201 / 9800) loss: 0.785474
(Iteration 7301 / 9800) loss: 1.020244
(Iteration 7401 / 9800) loss: 0.918925
(Iteration 7501 / 9800) loss: 1.197352
(Iteration 7601 / 9800) loss: 0.964436
(Iteration 7701 / 9800) loss: 1.401961
(Iteration 7801 / 9800) loss: 1.145336
(Epoch 8 / 10) train acc: 0.762000; val_acc: 0.631000
(Iteration 7901 / 9800) loss: 1.210087
(Iteration 8001 / 9800) loss: 1.096513
(Iteration 8101 / 9800) loss: 1.077458
(Iteration 8201 / 9800) loss: 0.918693
(Iteration 8301 / 9800) loss: 1.164165
(Iteration 8401 / 9800) loss: 1.050552
(Iteration 8501 / 9800) loss: 0.906412
(Iteration 8601 / 9800) loss: 1.255938
(Iteration 8701 / 9800) loss: 0.979160
(Iteration 8801 / 9800) loss: 0.909903
(Epoch 9 / 10) train acc: 0.775000; val_acc: 0.654000
(Iteration 8901 / 9800) loss: 1.469478
(Iteration 9001 / 9800) loss: 1.028888
(Iteration 9101 / 9800) loss: 1.071493
(Iteration 9201 / 9800) loss: 1.057363
(Iteration 9301 / 9800) loss: 1.126383
(Iteration 9401 / 9800) loss: 1.048362
(Iteration 9501 / 9800) loss: 0.820006
(Iteration 9601 / 9800) loss: 0.932375
(Iteration 9701 / 9800) loss: 1.136240
(Epoch 10 / 10) train acc: 0.786000; val_acc: 0.680000
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[24]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span></span><span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">stats</span><span class="p">[</span><span class="mi">2</span><span class="p">]</span><span class="o">.</span><span class="n">train_acc_history</span><span class="p">,</span> <span class="s1">&#39;-o&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">solver</span><span class="o">.</span><span class="n">train_acc_history</span><span class="p">,</span> <span class="s1">&#39;-o&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">stats</span><span class="p">[</span><span class="mi">2</span><span class="p">]</span><span class="o">.</span><span class="n">val_acc_history</span><span class="p">,</span> <span class="s1">&#39;-o&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">solver</span><span class="o">.</span><span class="n">val_acc_history</span><span class="p">,</span> <span class="s1">&#39;-o&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;iteration&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;loss&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">legend</span><span class="p">([</span><span class="s1">&#39;No BN train ACC&#39;</span><span class="p">,</span> <span class="s1">&#39;BatchNorm train ACC&#39;</span><span class="p">,</span> <span class="s1">&#39;No BN val ACC&#39;</span><span class="p">,</span> <span class="s1">&#39;BatchNorm val ACC&#39;</span><span class="p">],</span> <span class="n">loc</span><span class="o">=</span><span class="s1">&#39;lower right&#39;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[24]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>&lt;matplotlib.legend.Legend at 0x7fe52ce46e90&gt;</pre>
</div>

</div>

<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAA1QAAAKvCAYAAABtQ44zAAAABHNCSVQICAgIfAhkiAAAAAlwSFlz
AAAPYQAAD2EBqD+naQAAIABJREFUeJzs3Xl4lNXd//H3PclknclCWEPYd1dIhApYQVHcINqqj2LV
ilCXigtWWxGsbUnE3WJ/0PYp1KVW+6itSpAKBRQrQUACLiGACEjYtyyThWQyc35/ZCEhk0BCkpkk
n9d15YqZ3HPzHbxJ7s+cc77HMsYgIiIiIiIiDWfzdwEiIiIiIiKtlQKViIiIiIhIIylQiYiIiIiI
NJIClYiIiIiISCMpUImIiIiIiDSSApWIiIiIiEgjKVCJiIiIiIg0kgKViIiIiIhIIylQiYiIiIiI
NJIClYiIiIiISCMFTKCyLOs+y7J2WpZVbFnW55ZlDT/F8Q9ZlrXFsqwiy7J2W5b1omVZoS1Vr4iI
iIiISEAEKsuybgJeAJ4EhgFfAksty+pYx/G3AHMqjh8M3AncBKS2SMEiIiIiIiKAZYzxdw1YlvU5
sNYY82DF1xaQDbxsjHnWx/F/AAYbYy6v9tjzwAhjzMUtVLaIiIiIiLRzfh+hsizLDiQBKyofM+Up
bzkwso6npQNJldMCLcvqC1wNfNi81YqIiIiIiJwQ7O8CgI5AEHDwpMcPAoN8PcEY81bFdMDPKkaz
goA/GWOeadZKRUREREREqgmEQFUXC/A5H9GyrLHA48A9wDqgP/CyZVn7jTEpdTwnDrgC2AUcb4Z6
RURERESkdQgDegNLjTFHz+REgRCojgAeoMtJj3em9qhVpd8BrxtjXqn4OtOyLAfwZ8BnoKI8TP39
DGsVEREREZG24yfAm2dyAr8HKmOM27KsDcA4YBFUNaUYB7xcx9MiAO9Jj3krnmoZ3502dgG88cYb
DBkypClKF6nT9OnTeemll/xdhrQDutakpehak5aia01aQlZWFrfeeitUZIQz4fdAVeFF4LWKYLUO
mE55aHoVwLKs14E9xpjHK45PA6ZblrUJWAsMoHzU6oM6whRUTPMbMmQIiYmJzfU6RACIjo7WdSYt
QteatBRda9JSdK1JCzvjpUABEaiMMW9XNJn4HeVT/zYBVxhjDlcckgCUVXvKbMpHpGYD3YHDlI9u
zWqxokVEREREpN0LiEAFYIyZD8yv43uXnvR1ZZia3QKliYiIiIiI+OT3fahERERERERaKwUqkWYw
adIkf5cg7YSuNWkputakpehak+bkcrl44JcPMOGWCU12TqvuHg5ti2VZicCGDRs2aKGjiIiIiEg7
43K5GDl+JFn9s/BGeOF/AUgyxmScyXk1QiUiIiIiIm3ezNkzy8NU/5N3XzozClQiIiIiItLmLVq+
CG+/pg1TEEBd/kRERERERBqj2F3MXtde9uTvqfGRnZ9d/jkvm8NFh8Fq+j9bgUpERERERAJWYWlh
raC0J38Pe1x7qsLS0eKjNZ7TIbwDCVEJJEQlMDx+OD8a/CPmvjaXI+ZIk4cqBSoREREREfELV4mr
1mjSyR85x3NqPKdjREd6RPUgISqBkQkjufGsG6vCU4+oHnSP6k6EPaLWn3Xo6kPM2zGvyaf9KVCJ
iIiIiEiTMsaQV5JXewpeXnbVyNKe/D3kl+TXeF6XyC5V4ejiXhdXBafKj+5R3QkLDmtUTalPpLJy
/EqyTEWXvyaiQCUiIiIi0ooZY7CsZlgcVM+fl3M8pzwc+ZiCVxmcCt2FVc+xsOjq6EqP6PKAdFmf
y2oEpR7RPYh3xhMSFNJsdTudTtYsW8OslFm8s+gd9rO/Sc6rfahEREREmkFL3+RK++JyuZg5eyZp
y9NwB7mxe+xMvGwiqU+k4nQ6G31eYwxHio74bOxQ/aO4rLjqOTbLRrwz/kRAciZUBafKj26ObtiD
7E3x0ptERkYGSUlJ0AT7UGmESkRERKSJNNdNrkh1NTaoTfaWN1kwMG/HPFaOX8maZWt8Xm9e4+VQ
4SGf65QqQ9Pe/L2UeEqqnhNsCybeGV819S6xW2LNkaWoHnRxdCHY1n5jRft95SIiIiJNqLE3uSIN
5XODWgu8/bxkmSxufvhmxk8ZX2sa3t78vbi97qqn2G32GuHoB91/UBWSKh/rHNmZIFuQH15l66FA
JSIiItIETnWTOytlFnOfmeu/AqVV83g97HXtZWfOTt5a8hbeG3w3VfD287Lkb0tY0WtFVSjqHdOb
i3pcVCM8JUQl0CmyEzbL1sKvpO1RoBIRkXZF61qkuaQtTysfmfLB28/LorRFzEWBSnwzxnCs+Bg7
cnawM3cnO3N2sjN3Z9XX3+d+Xz66ZIAy6t5LyYJuHbqx5/E92GwKSy1BgUpERNo8rWuRplbqKWVH
zg62Hd3GtqPb2HJ4C/tK9tV7k7v3+F6u/7/r6RHdo1Yr6HhnfEAt2JfmUeQuYlfurvKQVBGYqkJT
zk5cpa6qY6NCo+gT04e+sX1JHphMn9jy/+4T04crF13JbrPb9/VmINQTqjDVghSoRESkTdO6Fmks
Ywz7XPvYdnQbW49urQpPW49uZWfOTjzGA4AjxMHAuIHYPXZKTWm9N7muUhfLvltGdn42BaUFVd+2
sOji6FIraFVf+B/vjCc0OLSFXr00Rpm3jD35e9iZc2JkqXK0aUfODg4WHqw6NiQohF7Rvegb25dR
CaP4ybk/qQpQfWL7EBsWW+do+rWXXVvnBrW272wkX57cbK9RalOgEhGRNk3rWuRU8kvyy4PSka21
wlPlPjpBVhB9Y/syqOMgkgcmMzBuIIM6DmJg3EC6ObphWRYPbH+g3pvcO6+9k7m3nbjW8o7X3vS0
stvayp0r2ZO/h7ySvBrn6RzZuUZr6sr9e6o2PXV2J9we3rx/Ye2YMYbDRYdrTserNtK0O283Zd4y
oDwkxzvj6RPbhwFxAxjfb3yNwBTvjG/0+qUaG9T2O/FGke07G0O2DyFlfkoTvmo5Fe1DJSIibVqf
xD7sSt5V56hBxD8imPLSlFqdrTQa0LacPEVv65GtbDtW/rn6qEFXR1cGxZUHpcrPA+MG0je27ymn
5NUYDfVxk9uY0VBXiYu9rr1VG6X62kD1WPGxGs+JC487EbSctUe7EqISiAyJbFAd7UlBacGJkORj
pKn6ZrWxYbE1puL1ielT9XWv6F7N+jPE5XIxK2UWi5Yvwm1zY/faSb4smZRZKRp1Pw1NuQ+VApWI
iLRZxhi6XtCVQ8mH6jwm9J1Q+t3bj72uvXWOBtQ1DUujAYGloVP0qoemQXGDGBA3gKjQqDOqwR83
uUXuIp8jXdX3FjpSdKTGc2LDYuucWlj5385Q/9yUN3fjGLfHze683T4bP+zM2cnhosNVx4YFh9E7
pveJkaWKwFT5OSYsptnqbAg122k4BapGUKASEWlfXCUufrvqt7xwzwtwO3WOUPVe1JudGTurnuPz
xrRiNCA7L5uc4zk1TtExomOtKVjVp2F1d3bXaEATa8gUvRqh6aQpes0tkG5yj5cdZ2/+3lpBq/pH
9ZE6KG+K4CtoVf+IDo1uktfYlI1jjDEcLDxYczpezk525JZ/nZ2fjdeUT8u0WTYSohJOjCzF9K0K
TH1j+9LF0UVtxdsoBapGUKASEWkfjDH8K+tfPPjRgxwrPsbQrKGsta31va5lu41p8dMatIaqsLSw
agpW1c1pXnaNKVj1jQbUdWPqr9GAQNWYKXrVw9PpTNGTmkrKStjn2ufzDYXK6YYHCg5gOHHv6Ahx
1LyWfbypUF9zBahnquQOG0O+9T1VMr8kv+Z0vGojTbtyd1FcVlx1bMeIjj4DU5/YPvSM7klIUEiT
/11K4FOgagQFKhGRtm/7se3c/+/7+Wj7RyQPSmbulXOJC4pr8nUtp1LsLmafa5/PUYDK0YFDhTWn
IUaHRp9yClZUaJTfRjyaY7Sl+hS96iNNpzNFr/LjTKfoScO4PW72F+yv9w2Ffa59VSNAAOHB4XVe
0wlRCcx/dj5/PfLXmo1jKti22xgTPIbhtwyv0WK8+rqxCHtEjal4J0/N05sV4osCVSMoUImItF3H
y47zzGfPMOezOXR1dOXlq14medCJtsGBuHjb12jAyQGsvtGAuka6TjUa0BBNNQ3r5Cl6lSNNgTZF
T5pGmbeMgwUH631DYZ9rX1U3PF6j3mm5/A36PFB3YOoc2VnXhzSYAlUjKFCJiLRNS7cv5b4l97E7
bzePjHqEmT+cWe+apUBa13IqlaMBNbq7nbSma3/B/hqjARH2CJ9TsKq31o4Ljzvl30FDp2GVekrZ
mbPzxChTxRS9bUe3caDgQNVxmqInAB6vh0OFh8jOy+aqiVdx7LpjdR7bfXF3stdlt5p/t9I6NGWg
0j5UIiLSKu3J38P0pdN5d/O7XNL7EtImpTGk05BTPq813ZTZg+z0jO5Jz+iedR5T5i3jQMEBn1Ow
th/bzie7PmFv/t6q6XMAoUGh9U7BSohKIGV2Sr37d137wLUMvXnoKafoXdL7Ek3Rk1qCbEF0c3aj
m7MbUVYUx8yxOkeo7B57q/p3K+2PApWIiLQqbo+bP6z7A09+8iSR9kj+/uO/M+mcSe32hivYFlwV
gupSORrga1rh7rzdpGensyd/D26v+8ST/gnc5vt83n5ePv7bx+xJ3MPAuIF1bnQrcjomXjax3g2R
ky9P9vEskcChQCUiIq3G6t2ruffDe8k8nMl9w+/jd5f8LmD2gQlk1UcDhncf7vMYr/FyuPBw1QjX
He/dQZ6V5/NYLIjvEM/WaVsVnOSMpT6RysrxK8kyvhvHpMxP8XeJIvVSoBIRkYB3uPAwv1r+K17Z
9ArD44ezbuo6kuKT/F1Wm2KzbHRxdKGLowtJ8UnE2mLJM3l1TsMK8YQoTEmTcDqdrFm2prxxTNpJ
jWPm+69xjMjpUqASEZGA5TVeFmQs4LHlj2Ew/OmaPzE1cSpBtiB/l9bmaRqWtCSn08ncZ+Yyl7mt
qnGMCIC2fhYRkYC0cf9GRi0cxd2L7+bawdeyddpW7r7gboWpFpL6RCpDvh2CbbuNqs7tpnxfoCHb
h5AyS9OwpHkoTElro0AlIiIBJe94Hg/++0Eu+MsFFJQW8Okdn/LKta/QObKzv0trVyqnYU2Ln0bv
tN50X9yd3mm9mRY/rVk2QxYRaa005U9ERAKCMYZ/fPMPHl72MK4SF89c9gwP/uBB7U3kR5qGJSJy
agpUIiLid1uPbOW+JfexYucKrh9yPS9d8RI9onv4uyypRmFKRMQ3BSoREfGbIncRT/33KZ5d/Sw9
onuw5JYlXDXgKn+XJSIictoUqERExC8Wb1vM/f++n32ufcy4aAaPXfQY4fZwf5clIiLSIApUIiLS
or7P/Z6Hlj7E+1veZ3y/8Sy7dRkD4gb4uywREZFGUaASEZEWUeop5aU1L/G7T39HTFgMb9/wNjec
dYPW5oiISKumQCUiIs3uk12f8PMPf862o9t44AcP8JuxvyEqNMrfZYmIiJwxBSoREWk2BwsO8sh/
HuGNr95gVI9RbLhrA+d3Pd/fZYmIiDQZBSoREWlyHq+HP33xJ2aunEmwLZiFyQu5Y+gd2CztJy8i
Im2LApWIiDSp9XvXc++H97Jh/wZ+lvgz5oybQ1xEnL/LEhERaRYKVCIi0iRyinOYuXImf/riT5zX
5TzS70xnZI+R/i5LRESkWSlQiYjIGTHG8Lev/sYjyx7heNlxXrriJe4bcR/BNv2KERGRtk+/7URE
pNEyD2Xy8yU/59PvP+Xmc27mhfEvEO+M93dZIiIiLUaBSkREGqygtIDZq2bz4ucv0je2L/+57T9c
1vcyf5clIiLS4hSoRETktBljeH/L+zz40YMcLjrMk2Oe5NFRjxIaHOrv0kRERPxCgUpERE7Ljpwd
3P/v+1ny7RKuHnA1f7jqD/SN7evvskRERPxKgUpEROpVUlbCc+nPkfrfVDpFdOK9m97j2kHXYlmW
v0sTERHxOwUqERGp03+++w/3LbmPnbk7efjCh/n1mF8TGRLp77JEREQChgKViIjUss+1j4eXPsz/
Zf4fF/e6mPdueo+zO5/t77JEREQCjgKViIhUKfOWMW/dPJ74+AnC7eG8ft3r3HrerZreJyIiUgcF
KhERAWBN9hru/fBevjr4FfdecC8pl6YQGx7r77JEREQCmgKViEg7d7ToKI8tf4wFGxeQ1C2JtVPX
Mrz7cH+XJSIi0iooUImItFNe4+WVja/wq+W/Kp/qd/U87k66myBbkL9LExERaTUUqERE2qEvD3zJ
vR/ey5o9a7jtvNt47vLn6OLo4u+yREREWh0FKhGRdsRV4uLJT57k5bUvMzBuIB//9GPG9h7r77JE
RERaLQUqEZF2wBjDO5vfYfrS6eQez+WpcU/x0IUPERIU4u/SREREWjUFKhGRNm7b0W1MWzKN/+z4
D9cNvo7fX/F7esX08ndZIiIibYIClYhIG1XsLmbOZ3N4ZvUzxDvjSZuUxoSBE/xdloiISJuiQCUi
0gb9+9t/M+3f08jOy+ZXo3/FjB/OIMIe4e+yRERE2hwFKhGRVswYg2VZVV9n52Xz0NKH+FfWvxjX
ZxxLblnCoI6D/FihiIhI26ZAJSLSyrhcLmbOnkna8jTcQW7sHjvXjLuGLuO78Mz6Z3CGOnnr+re4
6eybaoQtERERaXoKVCIirYjL5WLk+JFk9c/Cm+wFCzAwb/s8uAfufe5e5lw9h+iwaH+XKiIi0i7Y
/F2AiIicvpmzZ5aHqf4VYQrKPw8A2ygb9rV2hSkREZEWpEAlItJKGGP457J/4u3n9fl9bz8vi5Yv
auGqRERE2jdN+RMRCVDGGDYf3swnuz7hk+8/4ZOdn3Dk+JETI1Mns8Btc9dqVCEiIiLNJ2BGqCzL
us+yrJ2WZRVblvW5ZVnD6zn2Y8uyvD4+0lqyZhGRpmSMIfNQJvPWzePGd26ky/NdOOeP5zB96XQO
FBzgngvuoUtIFzB1nQDsHrvClIiISAsKiBEqy7JuAl4A7gLWAdOBpZZlDTTGHPHxlB8BIdW+7gh8
Cbzd3LWKiDSVk0egVu1axeGiw9htdn6Q8APuTrqbsb3HMrLHyKo9pPKuzGPejnk+p/3ZvrORfHly
S78MERGRdi0gAhXlAerPxpjXASzLuge4BrgTePbkg40xudW/tizrFqAQeLf5SxURaZzGBKiTpT6R
ysrxK8kyWeWhqqLLn+07G0O2DyFlfkrLvigREZF2zu+ByrIsO5AEPFX5mDHGWJa1HBh5mqe5E3jL
GFPcDCWKiDRKUwSokzmdTtYsW8OslFksSluE2+bG7rWTfFkyKfNTcDqdzfyqREREpDq/ByrKp+sF
AQdPevwgMOhUT7YsawRwNjC56UsTETl9zRGgfHE6ncx9Zi5zmasGFCIiIn4WCIGqLhUTWU5pCvCN
MWbD6Zx0+vTpREfX3KNl0qRJTJo0qeEViki71lIBqj4KUyIiIvV76623eOutt2o8lpeX12Tnt4w5
nczSfCqm/BUB1xtjFlV7/FUg2hjzo3qeGw7sB2YZY/7fKf6cRGDDhg0bSExMbJLaRaR9qS9Ajeg+
grG9x5YHqISRRIZE+rtcERERqUNGRgZJSUkAScaYjDM5l99HqIwxbsuyNgDjgEUAVvlbruOAl0/x
9Jso7/b392YtUkTapVMFqLuS7lKAEhERaef8HqgqvAi8VhGsKtumRwCvAliW9Tqwxxjz+EnPmwK8
b4zJacFaRaSNUoASERGRhgqIQGWMeduyrI7A74AuwCbgCmPM4YpDEoCy6s+xLGsAMAq4vCVrFZG2
QwFKREREzlRABCoAY8x8YH4d37vUx2PfUt4dUETktChAiYiISFMLmEAlItLUFKBERESkuSlQiUib
oQAlIiIiLU2BSkQCQmM2qFWAEhEREX9ToBIRv3G5XMycPZO05Wm4g9zYPXYmXjaR1CdScTqdtY5X
gBIREZFAo0AlIn7hcrkYOX4kWf2z8CZ7wQIMzNsxj5XjV7Jm2RocDocClIiIiAQ0BSoR8YuZs2eW
h6n+3hMPWuDt52Wz2UziTxPJG5mnACUiIiIBTYFKRPwibXla+ciUD6afIfvNbB6Z9ogClIiIiDQZ
l8vFzDlzePfDD5vsnLYmO5OIyGnyer0UUlg+zc8XCzpGd2T2JbO5rO9lClMiIiJyxlwuFyMnTGBe
TAz7f/7zJjuvApWItJhjxcd4ee3LDP3zUA7nHgZTx4EG7B57g7v+iYiIiNRl5pw5ZF1zDd4RI6AJ
7zEUqESkWXmNl5U7V3LLP28h/oV4frHsFwyIG0DyZcnYdvj+EWT7zkby5cktXKmIiIi0RV5j+LKg
gL+vWIF3+PAmP7/WUIlIs9ibv5dXN73Kwo0L2Zm7k0Fxg0i5NIXbzruNLo4uuK6q6PJnsvD2O9Hl
z/adjSHbh5AyP8XfL0FERERaIWMM3xUXsyI3l5U5OazMzeVIaSkEBzfpyFQlBSoRaTJuj5sl3y5h
wcYFLPl2CaFBofzP2f/D6z96ndE9RteYwud0OlmzbA2zUmaxKG0Rbpsbu9dO8mXJpMxP8bkPlYiI
iIgv+0pKWFERnlbk5JBdUkIQMCIqiru7dWNcbCyTge+NafJQpUAlImfs26PfsnDjQl778jUOFBzg
gvgLmH/1fG4+52aiw6LrfJ7T6WTuM3OZy1yMMVozJSIiIqflmNvNJxXhaWVuLluKigA4PzKSGzp1
YlxsLD+MjiYq+ETcSR4zhnnr15evoWpCClQi0ijF7mL+mfVPFmQsYNX3q4gJi+HWc29lSuIUhnYd
2uDzKUyJiIhIXQo9Hv6bm1s1jW9jQQEG6B8ezriYGH7buzeXxMTQKSSkznOkzpjBygkTyAK80XW/
4dtQClQi0iAb929k4caFvPHVG+SV5DG291je+NEb/HjIjwm3h/u7PBEREWkDSr1ePs/PZ2VODity
c1mbn4/bGOJDQhgXG8v93btzaWwsPcPCTvucTqeTNYsXM+vpp3nnzTfZ30S1WsbU1be4bbEsKxHY
sGHDBhITE/1djkirknc8jze/fpMFGxeQsT+Dro6uTB46mTuH3Un/Dv39XZ6IiIi0ch5j2OhyVa2B
+iwvjyKvl9jgYC6JiWFcbCyXxsQwKCKiSWa1ZGRkkJSUBJBkjMk4k3NphEpEfDLG8Nnuz1iwcQHv
ZL5DqaeUqwdczZNjnuTqAVcTbNOPDxEREWkcYwxbioqq1kB9kptLTlkZETYbF1dM4bs0NpbzHQ6C
AnxZgO6IRKSGgwUHee3L11i4cSHbjm6jb2xfnrj4CX469KfEO+P9XZ6I+Ikax4jImfr++PHyAFUR
ovaXlmK3LEZGRfFgQgLjYmIYERVFiK11bZWrQCUieLweln63lAUZC0jblkaQFcT1Z13Pn675E2N6
j8Fmta4fbCLSNFwuFzPnzCFt1SrcoaHYS0qYOGYMqTNmaGsDETmlQ6WlfFzZiS8nh++OH8cCEh0O
buvShXGxsYyOjiYyKMjfpZ4RBSqRdmxnzk5e2fQKr2x6hT35ezivy3m8dMVL3HLuLXQI7+Dv8kTE
j1wuFyMnTCDrmmvwpqSU79tiDPPWr2flhAmsWbxYoUpEasgvK2NVtVbmXxcWAjAkIoKr4uK4NCaG
sTExxNrtfq60aSlQibQzJWUlvL/lfRZsXMDyHctxhji55dxbmJo4laRuSZrSIyIAzJwzpzxMVd+v
xbLwjhhBFjDr6aeZm5rqt/pExP+KPR7SKzvx5eTwhcuFB+gVGsq42Fh+1bMnl8bE0C001N+lNisF
KpF24ptD37AwYyF/++pvHC0+ykU9L+KVa1/hxrNuJDIk0t/liUiAKPV6+ba4mH+sXIl3zhyfx3iH
D+eDJ55gbgvXJiL+Veb18oXLxYqKUaj0vDxKjKGT3c6lMTFM6daNS2Nj6RsW1q7eoFWgEmnDXCUu
/i/z/1i4cSGf7/mcThGdmDx0MlMSpzC442B/lycifuQqK2NLURFZlR+FhWQVFfFdcTEeYyAoqHya
ny+WxffGMPDzzzkrMpIhkZEMiYhgSEQEgyMicAbr9kKkLfAawzeFhVVT+Fbl5uLyeIgKCmJMTAzP
9OvHpTExnBMZ2a4C1Mn0E0+kjTHGsHbvWhZkLOAf3/yDIncRV/S/gndvfJeJgyYSElT3DuIi0rYY
YzjsdtcITJUfe0pKqo7rERpavsahQ4eqcHSrMWQb4ztUGUOcx8PVcXFkFRXx94MHya52voSK81V9
VJyzk93erm+6RAKdMYbviotZkZvLypwcPs7N5bDbTZjNxuioKB7r2ZNxsbEkORwEt7JOfM1JgUqk
jThSdIQ3vnqDBRkLyDycSc/onvxy9C+5Y+gd9Izu6e/yRKQZeY3h++PHySoqOjHqVBGgjpWVARBs
WfQPD2dwRAS3delSY0TJ4WNE6bqxY5m3fn3NNVQVbOvX85Nx4/j9gAFVjxWcPOJVVMTSY8eYt3cv
nopjOgQH1whYlR89w8KwKWiJ+MW+kpLyNVAVIWp3SQlBwPCoKO7q1o1xsbGMjIoirJV34mtOClQi
rZjXeFmxYwULNi7g/S3vY4zhusHX8eIVLzKuzziCbPrhJ9KWVK5vOnm0aWtREcVeLwARNhuDK4LK
VXFxVaGlX3h4g/Z2SZ0xg5UTJpBF+Zqpyi5/tvXrGfLhh6QsXlzjeEdwMBdERXFBVFStmr8rLq4x
tTDD5eLNgwcpqqg53GZjUPURrYrQNaCBNYu0Vw3ZJ+6Y280n1TrxbSkqAuC8yEiu79SJS2NiuDgm
hihN3T1t+psSaYX25O/hlY2v8NdNf2VX7i7O6nQWT497mlvPu5VOkZ38XZ6InKF61zdVHBMXHMyQ
yEiGO53cXjniFBlJj9DQJhntcTqdrFm8mFlPP82iJ57AHRKCvbSU5DFjSGlAy/QQm618RCqyZvMb
rzFkl5TUCofLjh3jaMWoWhDQLzy81qiW1mmJnP4+cYUeD//NzWVlRYjaWFCAAfqHhzMuJobf9u7N
JTExdArRkoDGsowx/q6hRViWlQhs2LBhA4mJif4uR6TB3B43advSWLhxIR9t/4iw4DBuPvtmpiZO
5cKEC7VcwuTAAAAgAElEQVQuQaSVaej6ppNDRUvf/DTkHfAzdbi0tFaYzCoq0jotkQo19ok7aQR5
8Icf8uIbb7CmrIwVubmszc/HbQzdQkIYFxvLuJgYLo2NpWdYmL9fhl9lZGSQlJQEkGSMyTiTcylQ
iQS4rUe2snDjQl778jUOFR5iRPcRTB02lZvOuYmo0KhTn0BE/Kr6+qbKgFA5+nSs2khM//DwWmuL
6lrf1F75WqeVVVjI9mojd5XrtAafFEB7aZ2WtCEPPP4482JifK5xZO1ayMoidupULomJYVxsLJfG
xDAoIkJvNlTTlIFKP6VFAlCRu4h3N7/LgowF/Hf3f+kQ3oHbzruNKcOmcG6Xc/1dnkir1lwjLaez
vim82vqmK6t11OuvtUKnpb51Wtsr12lVBNaNBQW8deiQX9dpteSonrQfBWVlvP3xx3ifesr3ASNG
EP/BB+wePZogXX8tQoFKJEAYY8jYn8GCjAW8+c2b5JfkM67PON66/i2uG3wdYcHte2he5Eyc7lqD
0zpXI9c3DVY3u2YTYrNxVmQkZ0VGQqcT60j9sU6rKa81EYA9x4+zOj+f1Xl5rM7LY5PLhddmq3ef
OCssDL1F03IUqET8LKc4hze/fpMFGxew6cAm4p3xPDDiASYPm0zf2L7+Lk+k1aux1iAlpWqtwbz1
61k5YQJrfDRYMMZwyO2uMT3vdPdv8sf6JvHNZln0CgujV1gYV8bF1fier3Vap9pPq3IaYec61mk1
5loTqc5jDF8VFJSHp/x80vPy2F1xTfYPD2d0VBT3xMfzW2PYW88+cfaSEo2OtiAFKpFmcKppHsYY
Vn2/ioUbF/Lu5ndxe9xMHDSRlEtSuKL/FQTb9E9TpKnMnDOn/Aa3+loDy8I7YgRZwAMpKdz4y1/W
aoCQ42N90+ns3yStQ6eQEDqFhHBxTEyNx09nP63Yyv20ThrVevEU19qsp59mbmpqi71GCXyusjI+
rxx9ys/n8/x8Cjwe7JZFktPJjZ06MTo6mlHR0XSp9kbN16fYJy557NgWfBWiphQiTcTlcjFz9kzS
lqfhDnJj99iZeNlEUp9IrXpHcr9rP699+RoLNy5k+7HtDOgwgKmJU7n9/Nvp6ujq51cg0jb1GT2a
XZWjBSczBh59FJ5/vsb6puo3ylrfJOB7nVblRsqV67SsX/wC8/zzdV5rvZ94gp2ffdbClUugMMaw
u6Skaure6rw8vi4sxEv5NOFR0dHl4SkqigucTsLr2Ui3vi5/Qz78UKOhp0FNKUQCjMvlYuT4kWT1
z8Kb7AULMDBvxzxWjF/Bk/Oe5M1tb7J422LsQXZuPOtGFiYv5Ic9f6gheZFmYoxhc2EhOcHB9a41
iHM4WD9iBL3Cw7W+Sep0qnVamwsKmORwkFfPtXbQsnhq1y7OcTg4JzKS3lpT16aVeb1sKiggvdr6
p72lpQAMDA9ndHQ09yckMDoqqsEd+JpqnzhpGgpUIk1g5uyZ5WGqv/fEgxZ4+3nZ7N3MTQ/fROIt
ibx81cvccu4txITF1H0yEWm0XLebFbm5LD12jI+OHStfD1NQUD4SVceogdPtpk9ERMsXK21C9XVa
sWVl5NVzrXmPH+fZ7GzyPOWTByMqQtrZERGcExnJ2ZGRnBMZSUJoqN5sa4XyyspYUzF1b3VeHmvz
8ynyegmxLIY7nfykSxdGVYxANcU6S6fTydzUVOaijpL+pkAl0gTSlqeVj0z50h/iv4lnw10bWrYo
kXbAawwZLhcfHTvG0pwc1uTl4QEGR0RwfadOXBEby6Lx4/mz1hpIC5g4Zky961ruHj+e3190EXtL
SsgsKuKbwkIyCwv5prCQdw8fprBi6mBUUBBnVwtYlYGrS0iIbpoDhDGGncePk14tQH1TWIgBOtrt
jI6K4je9ezM6Opokp5PQZp42rOvCvxSoRM6QMQZ3kLt8mp8vFlh2S+8eiTSRg6WlLKsYgVqWk8MR
txtnUBCXxcYyf+BArujQgV5hJ7YZGP3443w6YQJZ4HOtQcrixf57MdKmpM6YwcpTXGuWZZEQFkZC
WBhXdOhQ9dzKDaArA1ZmURFfuFz87cABSirWu8cFB58IWdU+x9ntfnrF7Yfb62VjZfe9ihB1oGL6
3pCICEZHRzM9IYHR0dEMCA/X7/t2RoFK5Ax5jZeioiIw+A5VBuwe3y12ReTU3F4va/Lz+agiRG0s
KAAg0eHgrm7duKJDB0ZGRWGv4x1grTWQlnIm15rNsugTHk6f8HAmdOxY9XiZ18uO48drjGatys3l
f/fvp6wiaHUNCak1bfDsyEii1IWy0XLc7qq1T+l5eaxzuSj2egmz2RjudHJH166MjopiZHS0Aq2o
y5/Imdh8eDOTP5jMujfWYfWwMP1r/3uybbcxLX4ac5+Z64cKRVqnXcXFLM3J4aNjx1iRk4PL46GT
3c742Fiu7NCByzt0qNFCuCE0WiwtpTmvtVKvl2+Li2sErczCQrYXF1M5Ab1HaGitaYNDIiOJrKd7
XHtkjOG74uIam+duLioCoIvdzuhq3fcSnU51/Wwj1OVPxM/cHjfPpT/Hb1f9lr6xfVn+p+U8OPlB
ssjC2+9Elz/bdzaGbB9CyvwUf5csEtCKPB5WVWsmsbW4mCBgZHQ0v+rZkys7dGCYw9EkHdEUpqSl
NOe1FmKzVa2zqu64x8OWyvVZFZ//efgwzx8/Xl4T0CcsrCpoVY5mDQoPJ6ydBK0Sr5cMl6vG5rmH
3G4Azo6I4KKKnzujo6PpGxamnxlySgpUIg301cGvmPzBZDYd2MQvR/2SJ8c+SVhwGGuWrWFWyiwW
pS3CbXNj99pJviyZlPkpmlIkchJjDFlFReXNJI4dY1VuLiXG0DM0lCs6dOCpvn0ZFxtLtKYsiTRI
WFAQQ51Ohp70e6egrIyskxphvH7gQFUb78oNrE+eNjggPLzO6bStxVG3u7x5REWAWp+fT4kxhNts
/CAqip9168ao6GhGRkURq+l70gia8idymko9pTz136dI/W8qg+IG8cq1rzC8+3Cfx2pKkUhtlS3N
K0NUdkkJoZbF2JgYrujQgSs7dGBwA/diEZEzk+t2k1lUVGPa4DeFhVUjNnbLYlDl+qxq67T6hocT
1Ez/Vs/kd6gxhm3FxTU2z91aXAxAt5CQ8ul7UVGMjo5mqMPR6sOiNJ6m/Im0sIz9GUz+YDKZhzKZ
cdEMZl08i9Dg0DqP1w2hSM2W5h8dO8bn+fm1WppfHBNDRDuZZiQSiGKqrRGq7nBpKZnVpg1mFhay
9NgxcsrKAAiz2RhyciOMiAh6NnKzYpfLxcw5c0hbtQp3aCj2khImjhlD6owZ9c7yOO7x8IXLdaKB
RH4+R9xuLODcyEgujY3lid69GRUVRW9N35NmokAlUo+SshJmfzqbpz97mnM6n8P6n61nWLdh/i5L
JGA1tKW5iASmTiEhjA0JYWxsbNVjxhgOlJbWbIRRVMR7R45QULFZsSMoiLN8dByMr2cPLZfLxcgJ
E8i65hq8KSlV7ebnrV/PygkTWFOtQ+Kh0tIaez9tcLkoNYbIiul798bHMzo6mgujojRlWFqMrjSR
Oqzbu447P7iTbUe38eSYJ3nsosewB2lutUh1bq+X9Pz8qmYSJ7c0v7JDBy6sp6W5iLQelmXRLTSU
bqGhXF5tDy1jDLtLSmpMG9xUUMBbhw5RXLFZcUxwcK3W7udERtIpJISZc+aUh6nqGyJbFt4RI8gC
rnviCXrecw+r8/L4tmL6XkJoKKOjopjUuTOjoqM5PzKSYP2cET9RoBI5SbG7mCc/eZIX1rzAsK7D
2HDXBs7tcq6/yxIJGPW1NH84IeGMWpqLSOtjWRa9wsLoFRbG1XFxVY97jGFncXGNaYPp+fn89cAB
3BVr+DvZ7bj+8x+8zz7r89ze4cNZ+eijDL31VsbHxvLb3r0ZHR1NT410SwBRoBKpJj07nTs/uJOd
uTtJvTSVR0Y9QrBN/0ykfaurpfmoZmhpLiJtR5Bl0T8igv4REVxbbbNit9fL9uJiMgsL+bqggGfD
wsqn+fliWXSLiiIjKUnrnyRg6U5RBChyFzFzxUzmrp3LDxJ+wHs3vceQTkP8XVa7os6IgaN6S/OP
jh3j02otza9US3MROUN2m40hFZsM39C5M697vewyxneoMobQkhL9fpCApt+G0u6t2rWKKYumsNe1
l+cuf46HLnyIIJu6jrWExnZ1kqbnq6V5mM3GmOhonu7blyvU0lxEmsnEMWOYt359zTVUFWzr15M8
dmzLFyXSAApU0m4VlBbw2PLHmLd+Hhf1vIglP1nCwLiB/i6r3WhIVydpeqdqaX5lhw5cHB1NuFqa
i0gzS50xg5UTJpBF+Zqpyt8HtvXrGfLhh6QsXuzvEkXqpUAl7dKKHSuYmjaVQ4WHmHvlXKaNmIbN
UneglnSqrk6znn6auampfquvtWjIVEm1NBeRQOR0OlmzeDGznn6aRU88gTskBHtpKcljxpCiN9ek
FVCgknYlvySfR5c9yv9m/C9je49l+W3L6dehn7/Lane8xvCvTz7BW0dg8g4fzl8fewzPT39KZFAQ
EUFBRNhsRAQFEVnxOaLaZ1/HtOX2uac7VbKuluZJamkuIgHG6XQyNzWVuWhNrbQ+ClTSbizdvpSf
pf2MnOM5zL96PndfcLdGpVpAiddbtSfJxoICNrpcbCoooNCy6u3qVBISwn9zcykyhiKPhyKvlyKP
h9KKVrunYresEwHLVwA7KZid6phACW2nmir5j3fe4TO3m6U5OT5bmo/v0IHOamkuIgFMYUpaGwUq
afNyj+fy8NKHeWXTK1ze93L+MvEv9Irp5e+y2qS8sjI2FRSUhyeXi40FBWwuKqLMGCxgUEQEQx0O
kjt25EWvl4P1dHXq7vXypY8Fym6vl+KKcFXk9VJYLWxVfV3tscJq3yvyeKqOP+J2U1RSUuv5jQ1t
dYWuhoQ2X8ecPHpU31TJTGM495e/JOiOO9TSXEREpIUoUEmbtnjbYu5efDcFpQX8ZeJfmDJsit75
agLGGPaVltYITpsKCthx/DgAoZbFuQ4HP4iK4p74eIY6HJzncBBZrcHBnksuaVRXJ3tFyIhqxpbd
zR3aCj2eqk0tT+Xk0LZ72TK8zz3n++ARI+j8/vtsu+gitTQXERFpIfqNK23SseJjPPjRg7zx1Rtc
PeBq/jzhzyREJfi7rFbJYwzfFhWdmLJXEZ4Ou90AxAQHM8zh4LqOHRnqcDDM4WBwRMQpp8MFclen
lg5tJweyukJbYVkZ8yMicNczVdIeHk6UOvOJiIi0GAUqaXPey3qPez+8lxJPCa9d9xq3nXebRqVO
03GPh6+rrXfaVFDAlwUFFHm9APQIDWWYw8HPK0adhjmd9AwNbdTfb3vv6tTY0PaOx0NhPVMl7doA
U0REpEUpUEmbcbjwMNP+PY23M98meVAyf7zmj8Q74/1dVsDKcbtrjTplFRbiAWyU70c0zOHgxx07
MszpZKjDQZzd3qQ1qKtTw2kDTBERkcCiQCWtnjGGtzPfZtq/p+E1Xv7+478z6ZxJujmvYIwhu6Sk
xqjTRpeL70tKAAi32TgvMpKLoqOZ1r07wxwOzomMJKKFp43p/9fpCeSpkiIiIu2RApW0agcKDvDz
D3/Oe1ve4/oh1zPv6nl0cXTxd1l+U+b1sq24uEZ78k0FBRwtKwMgLjiYYU4nN3buzLCK9U4DwsPb
9J5NbU17nyopIiISaBSopFUyxvDm12/ywEcPEGQF8c6N73DDWTf4u6wWVVSx3ql6l72vCgs5XrHe
qXdYGMMcDh5ISGCYw8FQh4OERq53ksCiqZIiIiKBQ4FKWp19rn3cs/ge0ralMemcSbx81ct0jOjo
77Ka1VG3u0Zw2lhQwNaiIrxAEHBWZCRDHQ5urhh5Ot/hILaJ1ztJYFKYEhER8S8FKmk1jDG8uulV
pi+dTrg9nPdvep9rB1/r77J8auyogTGG748fr9EoYmNBAXsq1jtF2Gyc73BwSUwMDyckMLRivVOY
2mSLiIiI+IUClbQK2XnZ3LX4Lj7a/hG3n387L13xEh3CO/i7rBpcLhcz58whbdUq3KGh2EtKmDhm
DKkzZvhc1+L2etlSVFQjOG0qKCC3Yr1TJ7udYQ4HP+ncuarLXv/wcII0IiEiIiISMBSoJKAZY/hL
xl94ZNkjRIVGsXjSYq4ZeI2/y6rF5XIxcsIEsq65Bm9KSlXntXnr17NywgT+8/777LTZanTZ+6aw
kBJjAOhbsd7pkR49qjbH7RYSoulcIiIiIgEuYAKVZVn3AY8AXYEvgfuNMevrOT4aeAr4ERALfA88
ZIz5qAXKlRawK3cXUxdNZcXOFUwZNoXnxz9PTFiMv8vyaeacOeVhqvreQJaFd8QIMo0hfvp0uOMO
gi2LsyMiGOZ0clvXrlXrnaIbuLmriIiIiASGgLiLsyzrJuAF4C5gHTAdWGpZ1kBjzBEfx9uB5cAB
4MfAPqAXkNtiRUuz8Rovf1z/R361/FfERcSx9NaljO833t9l1Stt1arykSlfRoyg4/vvsywpibMi
IwlVi3IRERGRNiMgAhXlAerPxpjXASzLuge4BrgTeNbH8VOAGOBCY4yn4rHdLVGoNK/tx7YzddFU
Vn2/inuS7uGZy58hKjTK32XVyxhDSUhI+TQ/XyyL0PBwhjocmsInIiIi0sb4/a3yitGmJGBF5WPG
GEP5CNTIOp42EVgDzLcs64BlWV9bljXDsiy/vx5pHI/Xw+8//z3n/fE8duftZsXtK/jjhD8GfJgC
2OByccjlgor1ULUYg72kRGFKREREpA0KhADSkfKtdA6e9PhBytdT+dIXuJHy+q8CZgO/AB5vphql
GW09spWLX72Y6UunMzVxKl/d+xWX9rnU32WdkjGGP+3dy+iNG4kbNgzbet9L/mzr15M8dmzLFici
IiIiLSJQpvz5YgF1vOWPjfLAdVfFaNZGy7K6U97Uoo6FLOWmT59OdHR0jccmTZrEpEmTzrxiaRCP
18OLa17k15/8moSoBD6941N+2OuH/i7rtBR6PNyzbRtvHDzIz+Pj+e3zzzM2OZkswDt8eFWXP9v6
9Qz58ENSFi/2d8kiIiIi7dJbb73FW2+9VeOxvLy8Jju/ZeqaptRCKqb8FQHXG2MWVXv8VSDaGPMj
H8/5BCg1xoyv9tiVwIdAqDGmzMdzEoENGzZsIDExsclfhzTM5sObmfzBZNbvXc/DIx/md5f8jgh7
hL/LOi1bi4q4ITOTHcXF/GXQIG7p0gUob50+6+mnWbRqFe6QEOylpSSPGUPKY4/53IdKRERERPwj
IyODpKQkgCRjTMaZnMvvI1TGGLdlWRuAccAiAKt8sck44OU6nrYaOHlIaRCw31eYksDh9rh5Lv05
frvqt/SN7cvqO1czskddS+UCz7uHDnHn1q3Eh4SwLimJsyMjq77ndDqZm5rKXMqnA2rNlIiIiEjb
5/dAVeFF4LWKYFXZNj0CeBXAsqzXgT3GmMo1Un8EplmWNRf4f8BAYAbw+xauWxrgq4NfMfmDyWw6
sIlHRz3Kb8b+hrDgMH+XdVrcXi+/2rGDl/bs4X86dWLBoEE469k7SmFKREREpH0IiEBljHnbsqyO
wO+ALsAm4ApjzOGKQxKAsmrH77EsazzwEuWbAO+t+G9fLdbFz0o9pTz136dI/W8qg+IG8fmUzxne
fbi/yzpte0tKuCkzk7UuF3P79+f+7t0VmEREREQECJBABWCMmQ/Mr+N7tVq+GWPWAqOauy45Mxn7
M5j8wWQyD2Uy46IZzLp4FqHBof4u67StzMlh0ubN2C2LT4cOZeRJDU1EREREpH0LhLbp0gaVlJUw
c8VMRvxlBBYW63+2ntmXzm41YcprDE99/z2Xf/kl5zkcbLzgAoUpEREREaklYEaopO1Yt3cdkz+Y
zLdHv+XJMU/y2EWPYQ+y+7us05bjdnP7li0sPnqUWb168ZvevQnSFD8RERER8UGBSppMsbuYJz95
khfWvMCwrsPYcNcGzu1yrr/LapAMl4sbMjPJLSvjw3PP5eq4OH+XJCIiIiIBTIFKmkR6djp3fnAn
O3N3knppKo+MeoRgW+u5vIwxLNi/n/u//ZZzHQ5Wnn8+vcPD/V2WiIiIiAS41nPHKwGpyF3EzBUz
mbt2LiO6j2DT3ZsY0mmIv8tqkCKPh59v28ZrBw9yT3w8v+/fn1CblheKiIiIyKkpUEmjrdq1iimL
prDXtZfnLn+Ohy58iCBbkL/LapBvi4q4ITOTb4uLeX3wYG7r2tXfJYmIiIhIK6JAJQ1WUFrAY8sf
Y976eVzU8yKW/GQJA+MG+rusBvvX4cNM3rKFriEhrEtM5ByHw98liYiIiEgro0Al9TLG1NjEdsWO
FUxNm8qhwkPMvXIu00ZMw2a1rulxbq+XGTt28MKePVzfsSN/HTyYqGD9UxARERGRhtNdpNTicrmY
OXsmacvTcAe5sXvsXHHJFZSMKOHVLa8ytvdYlt+2nH4d+vm71AbbV1LCzZs3syY/nxf79eOhhIQa
gVFEREREpCEUqKQGl8vFyPEjyeqfhTfZCxZg4M/b/4w10+LFBS/y4JgHW92oFMAnOTncvHkzQZbF
J0OHMlob9YqIiIjIGWp9d8XSrGbOnlkepvpXhCko/zwArJEWu/69q9WFKa8xPLN7N+O+/JKzIyPJ
uOAChSkRERERaRKt685Yml3a8jS8/bw+v+ft52XR8kUtXNGZyXW7+dE33/DYjh081rMny84/ny4h
If4uS0RERETaCE35kyrGGNxB7hMjUyezwG1z12pUEag2uVxcn5nJsbIy0s45hwkdO/q7JBERERFp
YzRCJVUsy8LusYOp4wADdo+9VYSphfv3c2FGBjHBwWQkJSlMiYiIiEizUKCSGiZeNhHbDt+Xhe07
G8mXJ7dwRQ1T7PEwZcsWpm7dyu1du7J62DD6hIf7uywRERERaaMUqKSG1CdSGfLtEPiWEyNVBmzb
bQzZPoSUWSn+LK9e3xUXM2rjRt48dIhXBw/mfwcNIiwoyN9liYiIiEgbpjVUUoPT6WTNsjX0/J+e
eDZ4iHJEYffaSb4smZT5KTidTn+X6NMHR47w06wsOoWEsDYxkfMcDn+XJCIiIiLtgAKV1FIaVEru
hbm88cwb3HLuLQG9ZqrM62Xmzp08m53Njzp25JXBg4kO1mUtIiIiIi1Dd55Sy5o9awAY3XN0QIep
AyUl3Lx5M5/l5fF8v348nJAQ0PWKiIiISNujQCW1pGen083RjV7RvfxdSp0+zc3lps2bsYCPhw7l
hzEx/i5JRERERNohNaWQWlZnr2ZUj1EBOdpjjOH53bu5dNMmBkdEkJGUpDAlIiIiIn6jQCU1uD1u
1u1dx+geo/1dSi15ZWX8ODOTR3fs4JEePfjPeefRNTTU32WJiIiISDumKX9Sw6YDmzhedpxRPUb5
u5Qaviwo4IbMTA6XlvLBOeeQrI16RURERCQAaIRKalidvZqw4DCGdRvm71KqvLp/PxdmZOAICmLD
BRcoTImIiIhIwNAIldSQnp3O8PjhhASF+LsUjns83L99Owv272dK1678YcAAwrVRr4iIiIgEEAUq
qWKMYXX2am477zZ/l8KO4mJuyMwkq6iIvw4axORu3fxdkoiIiIhILQpUUmV33m72ufb5ff1U2pEj
3L5lC3HBwawZNoyhTqdf6xERERERqYvWUEmV9Ox0AL8FqjKvl8d37CD5m28YEx3NF0lJClMiIiIi
EtA0QiVV0rPTGRg3kI4RLd/04WBpKZM2b+bT3Fye6duXR3v0CMh9sEREREREqlOgkirpe9L9Mjr1
WW4u/7N5M15jWDF0KGO0Ua+IiIiItBKa8icAFJQW8OWBLxmV0HKByhjDi9nZjN20iQHh4Wy84AKF
KRERERFpVTRCJQCs27sOj/EwuufoFvnz8svKuHPLFv555AiP9ujBU336EGxTvhcRERGR1kWBSoDy
9VMxYTEM7ji42f+srwsKuD4zk4Olpbx39tlc16lTs/+ZIiIiIiLNQUMCAsDq7NWMTBiJzWreS+Jv
Bw7wg4wMwm02NiQlKUyJiIiISKumQCV4jZc12WsY3aP5pvsd93i4Z+tWbt+yhZs6d2ZNYiL9IyKa
7c8TEREREWkJmvInZB3OIq8kr9k6/O0qLuaGzEy+KSzkLwMHMqVbN7VEFxEREZE2QYFKWJ29miAr
iBHdRzT5uT88epTbsrKICQ4mPTGRRG3UKyIiIiJtiKb8CenZ6QztOpTIkMgmO6fHGGbt2MGEr7/m
ouhoNiQlKUyJiIiISJujESohPTudK/tf2WTnO1Rayi2bN/Nxbi5z+vThlz17YtMUPxERERFpgzRC
1c4dKjzEt8e+bbL1U+l5eSR+8QVfFxay/PzzeaxXL4UpEREREWmzFKjauTXZawDOuMOfMYa5e/Yw
ZtMmeoeFsfGCC7gkNrYpShQRERERCVia8tfOpWenkxCVQI/oHo0+h6usjKlbt/L24cM8nJDA0337
Yrcpq4uIiIhI26dA1c6tzl59RtP9MgsLuf6bb9hXWsq7Z5/N9dqoV0RERETaEQ0jtGMlZSV8se+L
Rk/3+/vBg4zYsIEQm40vkpIUpkRERESk3dEIVTu28cBGSjwl9Y5QGWNqbcJb4vUyfft2/rhvH7d3
6cIfBw4kIiioucsVEREREQk4ClTt2OrdqwkPDuf8LufXeNzlcvH8zJmsTksjorSUopAQRk+cyCOp
qRyz27kxM5MvCwr488CB/Kxbt1qBS0RERESkvVCgasfS96QzovsI7EH2qsdcLhfXjhiBc88evouK
wu1wYC8oIPKVV7ho926yf/ELou120hMTSdJGvSIiIiLSzilQtVPGGNKz07lz6J01Hk999FF2HD5M
9uOP473wQrAsMIbv167FvPsu/bZvZ92tt9LBbq/jzCIiIiIi7YeaUrRTu3J3caDgQK31U39ftIjs
X8Ld7mYAACAASURBVPwC78iR5WEKwLIwF16Idf31lMyapTAlIiIiIlJBgaqdWp29GoCRPUZWPWaM
4WhwcPnIlA/mwgs5GhyMMaZFahQRERERCXQKVO1UenY6QzoOoUN4hxqPex2OEyNTJ7MsvJGRLVCd
iIiIiEjroEDVTqVnp9ea7mdZFmFeL9Q1AmUMYT7aqIuIiIiItFcKVO1Qfkk+Xx/62uf+UzdPnAif
f+77iZ9/zqSJE5u5OhERERGR1kNd/tqhtXvW4jVeRvcYXet7z/3613x69dVkAVTr8md9/jmDlyzh
2SVLWrxeEREREZFApUDVDqVnp9MhvAMD4wbW+p7T6WTt66/T96GHOP7OO0THxGAvLSV5zBhSlizB
qb2nRERERESqKFC1Q6uzVzOqx6g610KVfvUVRx988P+zd+fRVV/3vfff+2gABEJiBjPHQ4wxNjNo
wINwmjxNm6ZxnjTcm/Supre9aZP4qdNbryYrqe3kprfNbeKbrJWsm/Z2NUmTuqs3zXg7ZLAsWTo/
JjMY22Acm+kABjPoCCEkNP2eP44QHCQwCKGj4f1aSwu090+/88Wka/Hp3t+9+bsZM/jtu+6yZ0qS
JEm6AnuoRpnOrk42Hd7U53a/C2p/+UviRIIHb73VMCVJkiRdhYFqlHn5xMs0tTX1eSDFBdVtbdzW
2Mi8sWMHsTJJkiRp+DFQjTLJQ0nyE/msvGVl3w80N/PMnDlUdXUNbmGSJEnSMGSgGmWiwxHLZy2n
qKCoz/mjmzfzyrx5VM2bN8iVSZIkScOPgWqUiVIR5XOuvN3v2VdfBeDBxYsHqyRJkiRp2DJQjSLH
zh5jX8O+q/dPtbay5MQJpts/JUmSJL0lA9UoEqUiACrmXeGEv44OqmfOpKqzcxCrkiRJkoYv76Ea
RaJUxPyS+dxSfEuf8/u3b+fAzJlU5fs/C0mSJOlauEI1ily40PdKqvfsIdHZyX3Llg1iVZIkSdLw
ZaAaJVo7Wtl2dNtVA9Uzra2seOMNSseP7xmL43gwypMkSZKGJQPVKLHt6Dbau9qpmNt3/1Tc1UX1
jBlUdXTQ1NTEI488zsKFDzF37ntZuPAhHnnkcZqamga5akmSJGloGzKBKoTwsRDC/hBCSwhhUwhh
1VWe/U8hhK4QQmf3r10hhHODWe9wE6UixheMZ8mMJX3O79mzh+OlpVRMnkxZ2cN87WtlHDjwc44c
+REHDvycr32tjLKyhw1VkiRJ0iWGRKAKIfwW8CXgcWAZ8ALw0xDC1Kv8WCMw85Kv+Te7zuEsmUqy
Zs4a8hN9HzhRvXs3Be3tVP90E3v2fJKurncBoXs20NX1LvbseZTPfOZLg1azJEmSNNQNiUAFPAp8
I47jb8dx/ArwUeAc8JGr/Ewcx/GJOI7f7P46MSiVDkNxHBOloitu9wOoPneOsoMH+eG/bqGr6519
PtPV9S5+/OPkzSpTkiRJGnZyHqhCCAXACuCZC2Nx5iSEXwBlV/nRCSGEAyGEQyGEH4YQ7rrJpQ5b
rze8zolzJ654IEVnHFMzdSoPtrXR3j6eiytTlwu0txd5UIUkSZLULeeBCpgK5AHHLxs/TmYrX1/2
klm9eg/wH8n8OaIQwuybVeRwljyUJBBYO2dtn/M7DxygYfx41s+aRUFBM3ClwBRTUNBMCFcKXJIk
SdLoMpRvcA1c4V/2cRxvAjb1PBjCRmAP8Ptk+rCu6NFHH6WkpCRrbMOGDWzYsOFG6x2yolTE4umL
KR1b2ud89csvMy4/nzWrV/Prv76Tr33tp909VNkSiX/nPe+pvNnlSpIkSQPm6aef5umnn84aa2xs
HLD3D4VAdRLoBGZcNj6d3qtWfYrjuCOEsAO47a2efeqpp1i+fPl1FzmcRYcjyudc5ULfs2dZd/Ik
he96F1/4wn+luvphXn45Bi4cTBGTSPw7ixY9xX/7b/88WGVLkiRJN6yvxZPt27ezYsWKAXl/zrf8
xXHcDmwD1l8YC5k9ZeuB6FreEUJIAHcDb9yMGoezdGual998+Yr9U21dXdRNmsT61lYAiouLiaJ/
Zty4zZSU/AqzZ/8GCxb8Ch//+GY2bvxniouLB7N8SZIkaUgbCitUAF8GvhVC2AZsIXPqXxHwTYAQ
wreBw3Ecf7r7+8+S2fL3GlAKPEbm2PT/PeiVD3GbDm8iJqZiXt8n/G09dozmMWOomnFxgfDIkWJa
Wp7ghz+Ed7wjtmdKkiRJuoIhEajiOP6n7junPkdm699O4J2XHIU+B+i45EcmAX9N5tCKBjIrXGXd
R67rElEqYlrRNG6ddGuf89W7d1PS2sqyVRfvUa6thfx8KC/HMCVJkiRdxZAIVABxHH8d+PoV5qou
+/6TwCcHo67hLplKUj63/IrBqLqpiQdee428d7+7Z6ymBlauhAkTBqlISZIkaZjKeQ+Vbp6Org42
H958xQt9z3V2EhUXU3XuHHQHrjjOrFA98MAgFipJkiQNUwaqEezF4y/S3N58xQMpolOnaMvPp2ra
tJ6xV1+FY8fg/vsHq0pJkiRp+DJQjWDJVJKCRAErbun7SMjqvXuZfvo0i1eu7BmrrYW8PKjoe1FL
kiRJ0iUMVCNYlIpYccsKxuaP7XO+urGRqhdfJFxyL1dtLaxYAZ6OLkmSJL01A9UIFqWiK/ZPNXZ0
sLWoiKqzZzNH+pHpn6qpcbufJEmSdK0MVCPUkTNHONh48Ir9U3UNDXQlElRNndoz9vrrcPSogUqS
JEm6VgaqESpKRQBXDFTV+/Yx79gx3nZZ/1QiAZWVg1KiJEmSNOwZqEaoKBXxtklvY+aEmX3OP9PQ
QNXOnYS1a3vGampg2TIoKRmkIiVJkqRhzkA1QkWHoyuuTp1oa2PX2LFUpdMwfjxw8f4pt/tJkiRJ
185ANQKdaz/H9je2Uz6n70BVk04DUDVlSs/YgQOQSnmhryRJknQ9DFQj0PNHn6ejq4OKeX2f8Fed
SvH2Q4eYfUn/VE0NhADr1g1SkZIkSdIIYKAagaJURHFhMYunLe5zvrqhgaodO7JOn6ithaVLobR0
sKqUJEmShj8D1QiUTCVZO2cteYm8XnOHW1t5NT+fquPHYdq0nnHvn5IkSZKun4FqhInj+KoX+lZ3
9089MHlyz9jBg5kvA5UkSZJ0fQxUI8yrp17ldMvpK98/dfw49772GlNXreoZq63N9E/dd99gVSlJ
kiSNDAaqESaZSpIICdbMWdNrLo5jqk+dyvRPXXL6RE0NLFkClyxaSZIkSboGBqoRJkpFLJm+hIlj
Jvaae72lhVQiwfr9+2Hhwp5x75+SJEmS+sdANcJEqStf6FudTpPX2cm6yZMze/zI3D21b5/3T0mS
JEn9YaAaQU63nGbPyT1XDlQnT7Jq714mrrm4HbC2NvOr/VOSJEnS9TNQjSAbUxsB+gxUcRxTffo0
Vdu3Z/VP1dbC4sUwdeqglSlJkiSNGAaqESRKRcycMJOFpQt7zb3U3MwJoGrv3swJFN1qatzuJ0mS
JPWXgWoESaaSlM8tJ3T3R12qOp2msKOD8tJSyMtc+Hv0KLz2mgdSSJIkSf1loBoh2jvb2XJkC+Vz
rtA/dfo05Xv2MG7t2p6xC/1TBipJkiSpfwxUI8QLx1+gpaOFinkVveY6urqoOX2a9Vu29Lp/atEi
mD59EAuVJEmSRhAD1QgRpSLG5I1h2cxlveZ2nD3LGaDqxRdh1aqece+fkiRJkm6MgWqESKaSrLxl
JWPyx/Saq06nGd/ezqriYhg3DoBjx2DvXg+kkCRJkm6EgWqEiFIRFXN7b/cDqG5o4L6XX6ag/GJ/
lf1TkiRJ0o0zUI0AqcYUh88c7vP+qfNdXdSl01Rt3Njr/qk77oCZMwezUkmSJGlkMVCNAMlUEoCy
uWW95jafOUNLHFO1YwdUXFzBqq11u58kSZJ0owxUI0CUirh98u1MH9/7uL7qhgYmnT/P0rFjYdIk
AN58E3bvdrufJEmSdKMMVCNAlIr63O4HmQMpHty9m0RlZc/Yc89lfjVQSZIkSTfGQDXMnW07y85j
O/sMVM2dnWw6c4aq556DSwJVTQ3cdhvMnj2IhUqSJEkjkIFqmNt6ZCudcWefJ/wlGxtpj2Oqtm/v
dSCFq1OSJEnSjTNQDXNRKqJkTAmLpi3qNfdMQwMzW1u5E2DuXABOnoSXXvJACkmSJGkgGKiGuWQq
SdncMhKh919ldTpN1Z49hEtWp+yfkiRJkgaOgWoY64q72Hh4I+VzevdPNbS3s72piapnnsnqn6qt
hYULexasJEmSJN0AA9Uw9srJV0i3pqmY17t/6rnGRrqA9c8/36t/yu1+kiRJ0sAwUA1jyUNJEiHB
6tmre81VNzSwsKWFBW1tsCjTX3X6NOza5XY/SZIkaaAYqIax6HDEvTPuZULhhF5z1ek0Va+8ktnu
l8j8NdfVQRwbqCRJkqSBYqAaxqJU1Odx6cfb2nipuZmqX/yiV//U/PmwYMEgFilJkiSNYAaqYepE
8wlePfVqnxf6PtvQAMCDmzZl9U/V1Lg6JUmSJA0kA9UwtfHwRoA+A1V1Os2ilhZmnTsHK1YAkE7D
zp0GKkmSJGkgGaiGqSgVMbt4NvNK5vWaq25ooOrVV2HNGigsBC72T3nCnyRJkjRwDFTDVJSKKJ9b
Tggha/xgayuvt7ay/mc/69U/NWdO5g4qSZIkSQPDQDUMtXW2sfXo1iv2TwXg/rq6Pu+fuix/SZIk
SboBBqphaMcbO2jtaO3zhL/qdJpl588zubkZysoAaGyE7dvtn5IkSZIGmoFqGIpSEePyx7F05tKs
8TiOM/1Tv/wl3HsvTJwIQDIJXV0GKkmSJGmgGaiGoWQqyarZqyjIK8gaf7WlhSNtbX3eP3XLLXDb
bYNdqSRJkjSyGaiGmTiOSaaSfW/3a2ggH1j305/2ef+U/VOSJEnSwDJQDTMHGw9y7OyxK94/taa9
nQmtrT0rVE1NsG2b2/0kSZKkm8FANcwkDyUBWDtnbdZ4VxzzbEMDVa+9BrfeCrNmZZ5PQmen909J
kiRJN4OBapiJUhFvn/J2phZNzRp/sbmZUx0dVFVX9zoufcYMuOOOwa5UkiRJGvkMVMNMdDi6Yv/U
2BBY+5Of9DqQwv4pSZIk6eYwUA0jTeeb2HV8V5/9U880NFDR2cnY8+d7Vqiam2HrVrf7SZIkSTeL
gWoY2XxkM11xV69A1d7VRW1jI1X79sH06XD77QBEEXR0eCCFJEmSdLMYqIaRKBUxedxk3j717Vnj
25qaONvZSVVNTWa7X/f+vtpamDYNFi3KQbGSJEnSKGCgGkaSqSRlc8pIhOy/tup0muK8PFb+4AdZ
/VPePyVJkiTdXAaqYaKzq5NNhzf1ff9UQwP3xzH558719E+dOwdbtrjdT5IkSbqZDFTDxO4Tuzlz
/kyvE/5aOztJnjlD1f79MH48LF0KwKZN0N7ugRSSJEnSzWSgGiaSqSR5IY9Vs1dljW86c4bWri6q
amuhrAzy84HMdr8pU+Cuu3JQrCRJkjRKGKiGiSgVsWzWMooKirLGn0mnmZKfz5If/ajX/VP33QcJ
/4YlSZKkm8Z/bg8TUerKF/o+mEiQOH26p3+qpSWz5c/tfpIkSdLN1a9AFUL4TyGEd1/y/RdDCOkQ
QhRCmD9w5Qng+NnjvN7weq8DKZo6OtjS1ETVoUOZrX5r1gCweTO0tXkghSRJknSz9XeF6tNAC0AI
oQz4OPAYcBJ4amBK0wVRKgLoFajqGxvpiGPWP/ccLF+eOZSCzHa/SZNgyZJBL1WSJEkaVfL7+XNz
gde6f/9e4HtxHP91CCEJ1AxEYbooSkXMK5nHnIlzssar02lmFxZy+7/8C7z//T3jNTX2T0mSJEmD
ob//5D4LTOn+/a8Av+j+fSsw7kaLUrbocHTF+6eqCgsJhw719E+dP5/pn3K7nyRJknTz9TdQ/Rz4
3yGE/w3cAfxL9/hi4EB/XhhC+FgIYX8IoSWEsCmEsOqtfwpCCB8MIXSFEL7fn88d6lo7Wnn+6POU
z8kOVKfb29lx9ixVqVRmoCJzYMWWLdDa6oEUkiRJ0mDob6D6GLARmAY8HMfxqe7xFcDT1/uyEMJv
AV8CHgeWAS8APw0hTH2Ln5sP/A/guev9zOFi+xvbaets67VCVZNOEwMP1tfDnXfCtGmZ8RooKYF7
7hn8WiVJkqTRpl89VHEcp8kcRHH5+OP9rONR4BtxHH8bIITwUeDdwEeAL/b1AyGEBPAd4M+A+4CS
fn72kBalIooKirh35r1Z49UNDdw6dizzf/azXvdPrVsHeXmDXakkSZI0+vT32PR3hRAqL/n+YyGE
nSGEfwghTLrOdxWQWdl65sJYHMcxmb6ssqv86OPAm3Ec/931VT+8JFNJ1sxeQ34iO/tWp9OsLyqC
l17q6Z9qa4MocrufJEmSNFj6u+XvfwATAUIIS8hs1/tXYCHw5et811QgDzh+2fhxYGZfPxBCqAB+
B/jP1/lZw0ocx0Sp3gdSvHH+PHvOnaPq6NHMQPcK1datmUt9PZBCkiRJGhz9PTZ9IbC7+/cPA/83
juNPhxCWkwlWAyEAca/BECYAfw/8XhzHDQP0WUPSvoZ9vNn8JhVzK7LGn02nAXggmYRbboGFC4HM
dr/iYli6dNBLlSRJkkal/gaqNqCo+/cPAd/u/v1puleursNJoBOYcdn4dHqvWgHcCswHfhJCCN1j
CYAQQhvw9jiO91/pwx599FFKSrLbrTZs2MCGDRuus+ybL5lKArB2ztqs8eqGBu4eP54Z1dWZ1anu
/ww1NZndf/n9/VuVJEmSRpinn36ap5/OPjevsbFxwN7f33961wNf7r7IdzXwW93jdwCHr+dFcRy3
hxC2AeuBHwN0B6X1wFf7+JE9wJLLxr4ATAAeAVJX+7ynnnqK5cuXX0+JOROlIu6adheTxmW3pT2T
TvOekpLMHr/uINjenumf+rM/y0WlkiRJ0tDU1+LJ9u3bWbFixYC8v7+B6uPA14H3A38Qx/GR7vH/
B/j3frzvy8C3uoPVFjKn/hUB3wQIIXwbOBzH8afjOG7j4nZDuufTZM6y2NOPzx6yolTUa7vf/pYW
DrS2UnX+fCZFdfdPbdsGzc32T0mSJEmDqb/Hph8Cfq2P8Uf7+b5/6r5z6nNktv7tBN4Zx/GJ7kfm
AB39efdwlW5N89KbL/HJsk9mjVen0ySA+zduhIkTYUlmsa6mBiZMgGGy+CZJkiSNCP3utgkh5AHv
BRaROTxiD/CjOI47+/O+OI6/TmbVq6+5qrf42d/pz2cOZZsPbyYm7nXCX3VDAyuKiymtrYWKip4L
py58W1CQi2olSZKk0am/91DdRiZAfRt4H5mtf38PvBxCuHXgyhu9olTE1KKp3D759p6xOI6pTqep
KinJNEx1b/fr6ID6eu+fkiRJkgZbf++h+irwOjA3juPlcRwvA+YB++n7IAldp2QqSfncci4eZAiv
nDvHsbY2qhoa4MyZngt9t2+Hs2ftn5IkSZIGW38D1f3AY3Ecn74wEMfxKeBPu+d0Azq6Oth8ZDPl
cy7b7pdOUxACFZs3Q2EhrFoFZLb7FRXBypW5qFaSJEkavfobqM4DxX2MTyBzR5VuwEtvvsTZtrNU
zMs+4e+ZhgbWTpzI+Lq6TJgaOxbIHEhh/5QkSZI0+PobqP4v8NchhDXhorXA/6L7Lin1X5SKKEgU
sGLWxbPxO+OYmnSaqtJSqKvr6Z/q7Mz0T7ndT5IkSRp8/Q1Uj5DpodoItHZ/RcBrwB8NTGmjVzKV
ZPms5YwrGNcz9sLZszR0dFB17hy88UZP/9TOnZl2KgOVJEmSNPj6ew9VGviN7tP+FgEB2B3H8WsD
WdxoFaUifvPO38waq25oYFwiwdrnn4cQoDzTX1VTA+PG9bRTSZIkSRpE1xyoQghffotHHrhwIl0c
x598i2d1BUebjnIgfYCKudn9U9XpNOtKSiisq4O774ZJk4DMgRRlZTBmTC6qlSRJkka361mhWnaN
z8X9KUQZUSoCoGxuWc9Ye1cXz6XTfHbBgkzDVFXmnuPOzkw71SeNr5IkSVJOXHOgiuP4wZtZiDKi
VMSC0gXcUnxLz9jWpiaau7qoimPYuxcefxyAXbsgnbZ/SpIkScqV/h5KoZskSkW9tvs909BASV4e
y7Zvzwx0n/BXW5vZ6rd69WBXKUmSJAkMVENKS3sL29/YTvnc3hf63l9aSn5dHcyfD3PnAhf7p7qv
o5IkSZI0yAxUQ8jzR5+nvas9K1C1dHYSNTayftKkTP9U9+pUVxc895zb/SRJkqRcMlANIVEqYkLh
BJZMX3Jx7MwZ2uKYqjFjYPv2nvunXnoJTp82UEmSJEm5ZKAaQpKpJGvnrCUvkdczVt3QwLSCAhbv
2pU51q97haqmBgoLYe3aHBUrSZIkyUA1VMRxTJSKKJ/Tu3+qqrSUUFcHkyfDokVApn9qzZrMpb6S
JEmScsNANUT88vQvOdVyiop5F0/4O9PRwdYzZ6i60D9VUQGJhP1TkiRJ0hBhoBoikoeSBAJrZq/p
GXsunaYTqJowATZu7Omf2r0bTp6EBx7ITa2SJEmSMgxUQ0SUirh7+t2UjC3pGatOp5k7Zgy3vvIK
nDuXdf9UQUHmyHRJkiRJuWOgGiKiw70v9K1uaGD9pEmE+vrMZVMrVgCZQLV6NRQV5aJSSZIkSRcY
qIaAhpYGdp/YnXX/1Mm2Nl5obqaqtDTTP7VmDRQWEseZQGX/lCRJkpR7BqohYOPhjQBZgaomnQbg
wQuBqrt/6pVX4M03DVSSJEnSUGCgGgKiVMT08dN526S39YxVp9PcMW4ccw4ehBMnegJVbS3k50N5
+ZXeJkmSJGmwGKiGgCiV6Z8KIfSMPdPQkDkuva4OEomeG3xramDlSpgwIUfFSpIkSephoMqx9s52
Nh/ZnLXd73BrK6+2tFzsn1q6FCZOtH9KkiRJGmIMVDm26/guzrWfywpUz3b3Tz1QWppZoeo+Lv3V
V+HYMe+fkiRJkoYKA1WORamIwrxCVsxa0TNWnU5z7/jxTDt5Evbty+qfysuDioorvU2SJEnSYDJQ
5VgylWTlLSsZkz8GgDiOqb7QP1Vfn3nokgt9ly+H4uJcVStJkiTpUgaqHItSEeVzLm7329fayqHz
5y/2T912G8ycSRxnDqRwu58kSZI0dBiocijVmCJ1JkXFvIt7+KobGsgD7rusf+r11+HoUQ+kkCRJ
koYSA1UORakIgLI5ZT1jzzQ0sLK4mInNzfDCC1n9U4lET76SJEmSNAQYqHIoSkXcOulWZkyYAXT3
T6XTmf6pjRshjnsSVE0NLFsGJSU5LFiSJElSFgNVDkWHo6ztfi83N3OivZ31Fy70nT4dbr/d+6ck
SZKkIcpAlSPNbc3seGNH1oEU1ek0hSFQPnFi5kCKykoIgf37IZXyQApJkiRpqDFQ5cjWo1vpjDuz
LvStbmigvKSEcR0dsHlzVv9UCD3fSpIkSRoiDFQ5EqUiJo6ZyOLpiwHojGNq0unMcenbtsH581n3
T917L5SW5rJiSZIkSZczUOVIMpWkbE4ZiZD5K9jR1ERjZ2fmQIq6Ohg/HpYuBbx/SpIkSRqqDFQ5
0BV3sTG1MWu73zPpNOMTCVYVF2f6p8rKID+fgwfh4EEPpJAkSZKGIgNVDuw9uZeG1oZe/VPrSksp
BEgms/qnwP4pSZIkaSgyUOVAlIpIhARrZq8BoK2ri7rGRtaXlsLu3dDQkHX/1D33wJQpOSxYkiRJ
Up8MVDmQTCW5Z8Y9FI8pBmDzmTO0dHVd7J/Kz4c1mbDl/VOSJEnS0GWgyoEoFfW6f2pSfj73TpiQ
6Z9avhzGjyeVgn37PJBCkiRJGqoMVIPs5LmT7D21l4p5FT1j1Q0NPFBaSl4ImRWqy/qn7rsvF5VK
kiRJeisGqkG2MbURoOdAiubOTjaeOZO5f+rQIUilsu6fWrwYpk7NWbmSJEmSrsJANciiVMSsCbOY
XzIfgGRjI+1xfLF/CqAis3rl/VOSJEnS0GagGmTR4YiKeRWEEIDMdr+ZhYUsKirK9E/deSdMm8bR
o/Daax5IIUmSJA1lBqpB1NbZxpYjW3odSFFVWpoJWPZPSZIkScOKgWoQ7Ty2k9aO1p7+qXR7O9ua
mjLb/U6fhpdf7glUNTWwaBHMmJHDgiVJkiRdlYFqEEWpiLH5Y1k2axkAzzU20gWZAymSycxDlxxI
4XY/SZIkaWgzUA2iZCrJqltWUZhXCGT6pxaMHcvCceMy/VOzZ8OCBRw7Bnv3GqgkSZKkoc5ANUji
OM5c6Dv3Yv/UM939U0Cmf6qyEkLo6Z8yUEmSJElDm4FqkBxqPMTRpqNUzM0ciX68rY2Xmpsz/VMt
LfD881kHUtxxB8yalcuKJUmSJL0VA9UgSaYyPVJlc8sAqEmnge7+qS1boL09q3/K+6ckSZKkoc9A
NUiiVMQdU+5gatFUINM/taioiFljxmT6p0pK4O67efNN2L3b7X6SJEnScGCgGiSX909VX94/VV4O
eXk891xmyEAlSZIkDX0GqkHQdL6JF46/0NM/dai1lddaWjL9U52dEEVZ90/ddlvmwD9JkiRJQ5uB
ahBsObKFrrirZ4Xq2XSaANxfWgq7dkFTk/dPSZIkScOQgWoQRKmI0rGl3Dn1TgCeaWhg6YQJTCko
yGz3KyyEVas4eRJeeslAJUmSJA0XBqpBEB3O9E8lQoI4jqluaLjYP1VfD6tWwdix9k9JkiRJw4yB
6ibrirvYmNpI+ZzMdr9ftrRwpK2N9ZMmQRxnVqguuX9q4UKYNy+XFUuSJEm6Vgaqm2z3id00nm/s
6Z+qbmggPwQqS0pg3z44dsz+KUmSJGmYMlDdZFEqIi/ksXr2aiBzXPrq4mKK8/Mzq1MhQHk5p09n
zqfwQl9JkiRp+DBQ3WTJVJKlM5cyvnA8XXHMs+l05rh0yPRP3X03TJpEXV1mB6ArVJIkSdLwl7RA
vQAAIABJREFUYaC6yS690PfF5mZOtrdnX+h7yf1T8+fDggW5qVOSJEnS9TNQ3URvNr/Ja6df67nQ
t7qhgTEhUDZxIrz5Jrz6qv1TkiRJ0jBmoLqJolQEcPFAinSaipISxublZbb7AaxbRzoNO3caqCRJ
kqThxkB1E0WpiDkT5zC3ZC4dXV3UptOZ49IhE6jmz4c5c3r6pzyQQpIkSRpehkygCiF8LISwP4TQ
EkLYFEJYdZVnfzOEsDWE0BBCOBtC2BFC+NBg1nstolTUs91v29mzNHV29tk/VVsLc+Zk7qCSJEmS
NHwMiUAVQvgt4EvA48Ay4AXgpyGEqVf4kVPAfwPWAkuAvwP+LoTwjkEo95qc7zjP80efz7p/qjgv
j5XFxXD2LOzY0at/KoRcVixJkiTpeg2JQAU8CnwjjuNvx3H8CvBR4Bzwkb4ejuP4uTiOfxTH8d44
jvfHcfxVYBdQOXglX932N7ZzvvN8Vv/UfSUl5CcSsGkTdHbCunU0NsL27W73kyRJkoajnAeqEEIB
sAJ45sJYHMcx8Aug7BrfsR64A6i9GTX2R5SKKCoo4t4Z99La2Ul9Y2P2/VNTpsCiRSST0NXlgRSS
JEnScJSf6wKAqUAecPyy8ePA26/0QyGEicARYAzQAfxhHMfVN6vI65VMJVk9ezUFeQUkGxpo7erK
7p+qqIAQqK2FWbPgtttyW68kSZKk6zcUAtWVBCC+ynwTcC8wAVgPPBVC2BfH8XNXe+mjjz5KSUlJ
1tiGDRvYsGHDDZZ7URzHRKmI3132u0Bmu9+U/HzumTAB2tszW/6efBLIXOj7wAP2T0mSJEk3w9NP
P83TTz+dNdbY2Dhg7x8Kgeok0AnMuGx8Or1XrXp0bwvc1/3trhDCXcCngKsGqqeeeorly5f3v9pr
sD+9n+PNx7MOpHhw0iQSIWQOozh3DioraWqCbdvgI312ikmSJEm6UX0tnmzfvp0VK1YMyPtz3kMV
x3E7sI3MKhMAIYTQ/X10Ha9KkNn+l3PJQ0kAyuaWcbajg81NTRe3+9XXw7hxsHw5yWTmbAoPpJAk
SZKGp6GwQgXwZeBbIYRtwBYyp/4VAd8ECCF8Gzgcx/Gnu7//U+B54HUyIerdwIfInA6Yc1EqYtHU
RUweN5l/P3WKjji+eCBFXR2sWQOFhdTWwowZcMcdua1XkiRJUv8MiUAVx/E/dd859TkyW/92Au+M
4/hE9yNzyBw8ccF44Gvd4y3AK8B/jOP4e4NX9ZVFh6Os49JvKSzkjnHjII4zK1R/8AeA909JkiRJ
w92QCFQAcRx/Hfj6FeaqLvv+s8BnB6Ou63Xm/BlePP4if7TmjwB4pqGBqkmTCCHAK6/AyZNQWUlz
M2zdCh/+cI4LliRJktRvOe+hGmk2Hd5ETEz53HJOt7ez4+zZ7P6pRALKyogi6Ojw/ilJkiRpODNQ
DbAoFTFl3BTumHIHtek0MWT3Ty1dCsXF1NbCtGmwaFFOy5UkSZJ0AwxUAyxKZfqnQghUp9PcOnYs
88eOzUzW1cG6dUDm/in7pyRJkqThzUA1gDq7Otl0eFPW/VM9q1NHjsD+/VBZyblzsGWL2/0kSZKk
4c5ANYBeevMlmtqaKJ9bzrHz59l97lx2/xRAZSWbNkF7u/dPSZIkScOdgWoARamI/EQ+q25ZRXU6
DcCDF1ao6uvhtttg5kxqamDKFLjrrtzVKkmSJOnGGagGUDKVZPms5YwrGEd1QwOLi4qYUViYmbyk
f6q2Fu67L3PgnyRJkqThy3/SD6AoFVE+5+KFvj39U42NsGsXVFbS0gKbNrndT5IkSRoJDFQD5I2m
N9if3k/53HL2t7Swv7WV9RcCVRRBHMO6dWzeDG1tHkghSZIkjQQGqgESpSIAKuZV8Gw6TQK4v6Qk
M1lfD9Onw223UVsLkybBkiW5q1WSJEnSwDBQDZAoFTG/ZD63FN9CdUMDy4uLKS0oyExe6J8KgZoa
+6ckSZKkkcJ/1g+Q6HDmQt84jjP9UxeOSz9/PnPpVGUl589n+qfc7idJkiSNDAaqAdDS3sK2o9uo
mFvBK+fO8UZb28UDKZ5/PhOq1q1jyxZobTVQSZIkSSOFgWoAbHtjG+1d7ZTPLac6naYgBCov7Z+a
MAHuvZeaGigpgXvvzWm5kiRJkgaIgWoARKmI8QXjWTJjCdUNDaydOJHxeXmZybo6KCuD/HxqazOt
VBemJEmSJA1vBqoBkEwlWTtnLYmQx7OX9k91dUEyCZWVtLVlTk/3/ilJkiRp5DBQ3aA4jjMX+s4t
54WzZ2no6LjYP/Xyy5BOw7p1bN0KLS32T0mSJEkjiYHqBr12+jVOnjvZ0z81LpFgzcSJmcn6esjP
hzVrqK2F4mJYujS39UqSJEkaOAaqGxSlIgKBtXPWUt3QQGVJCWMuXDJVVwcrVkBRETU1mf6p/Pyc
litJkiRpABmoblAylWTx9MWML5zIc42NF/unILNCtW4d7e2Z/im3+0mSJEkji4HqBkWpiPI55Wxt
auJsZ+fF/qmDByGVgspKtm2D5mYDlSRJkjTSGKhuQLo1zcsnXqZiXgXVDQ2U5OWxfMKEzGR9febX
igpqajJXUS1fnrNSJUmSJN0EBqobsDG1EaDnQIr7S0vJv7R/atEimDqV2lqoqICCghwWK0mSJGnA
GahuQJSKmFY0jVsmLiBqbLy43Q96+qc6OjK/dbufJEmSNPIYqG5AdDhz/9SmpibOx/HFAylOncrc
QVVZyfbtcPasF/pKkiRJI5GBqp86ujrYfHgzFXMreKahgWkFBSwePz4zmUxmfl23jtpaKCqClStz
V6skSZKkm8NA1U+7ju+iub25p3/qwdJSEiFkJuvrYfZsmD+fmhr7pyRJkqSRykDVT1EqojCvkNun
38vWM2ey+6fq6mDdOjq7gv1TkiRJ0ghmoOqnZCrJilkr2Np8nk5g/YX+qXPnYNs2qKxk5044c8ZA
JUmSJI1UBqp+ilKZAymqGxqYO2YMt44bl5nYsgXa22HdOmpqYNw4WLUqp6VKkiRJukkMVP1w+Mxh
DjUe6umfqiotJVzaP1VSAosXU1sLZWUwZkxu65UkSZJ0cxio+iFKRQDcOWsNO8+e7d0/VVFBJ3nU
1bndT5IkSRrJDFT9EKUi3jbpbexuyxzd9+CF/qmODogiqKxk1y5Ip71/SpIkSRrJDFT90NM/lU5z
+7hxzB07NjOxa1fmFt/u+6fGjIHVq3NbqyRJkqSbx0B1nc61n2PHsR1UzK2guqGB9Zdu96uvh8JC
WLmS2lpYuxYuZC1JkiRJI4+B6jptPbKVjq4Obp25lr0tLVRd2O4Hmf6p1avpKhzLc8+53U+SJEka
6QxU1ylKRUwcM5E38mYA8MCFQBXHmRWqykpeeglOn/ZACkmSJGmkM1Bdp+hwxNo5a6lpbOSe8eOZ
VliYmXj9dTh2rOf+qcLCzJY/SZIkSSOXgeo6dMVdRKmIsjnlPNPQkH1cen09hADl5dTWwpo1mUt9
JUmSJI1cBqrr8OqpVzndcpqFs8o5dP587/6pJUvomljKc8+53U+SJEkaDQxU1yFKRSRCgsZxt5IA
7rs0UNXXw7p17N4NJ096IIUkSZI0GhiorkPyUJIl05ew8Wwrq4qLKcnPz0wcPw6vvgqVldTWQkEB
lJXltlZJkiRJN5+B6jpEhyPK5pZTfXn/VDKZ+bU7UK1aBUVFualRkiRJ0uAxUF2jU+dO8crJV5g/
6z7ebG/v3T+1YAHx7DnU1rrdT5IkSRotDFTXaOPhjQC0TlhEYQiUl5RcnOzun3rlFXjzTQ+kkCRJ
kkYLA9U1ilIRMyfMZOf5BGUTJ1KUl5eZOHsWduyAykpqaiAvD8rLc1qqJEmSpEFioLpGUSqibG4F
Nel0dv/Upk3Q2Qnr1vX0T02YkLs6JUmSJA0eA9U1aO9sZ8uRLcyf/RCNnZ29+6emTCF++53U1rrd
T5IkSRpNDFTXYOexnbR0tNA+8W7GJxKsnjjx4mR9PVRW8uovA8eOeSCFJEmSNJoYqK5BlIoYkzeG
VzvHs660lMJE93+29vbMlr/u49Lz8qCiIre1SpIkSRo8BqprkEwlWTF7LckzTdnb/bZvh3Pnevqn
li+H4uLc1SlJkiRpcBmo3kIcxyRTSRbMfRfnurqyD6Sor4dx44iXLqOmxu1+kiRJ0mhjoHoLqTMp
jjYdpat0KaX5+Sy99Ai/ujpYu5bXU4UcPeqBFJIkSdJoY6B6C1EqAuBgmMwDpaXkhZCZiOOeAylq
ayGRgMrKHBYqSZIkadAZqN5C8lCSW6cs5vmzLay/tH/qlVfg1ClYt46aGli2DEpKclamJEmSpBww
UL2F6HDE2xb8Ou1x3Lt/KpEgXrPW+6ckSZKkUcpAdRVn287ywrEXyJu8ihkFBSwqKro4WVcHy5ax
/2QxqZSBSpIkSRqNDFRXseXIFjrjTo4kplM1aRLhQv8UZPVPhQDr1uWuTkmSJEm5YaC6iigVMbFo
Fi+3dmTfP3XkCOzf33P/1L33wqW7ASVJkiSNDgaqq4hSEbe97WG6oHf/FEBlpfdPSZIkSaOYgeoK
uuIuNh7eyJgpa5k/ZgwLx469OFlXB7ffzsHWGRw8aP+UJEmSNFoZqK5gz4k9pFvTHCu4hfVX6Z8C
+6ckSZKk0cpAdQVRKiJROIX97SF7u186Dbt29dw/dc89MGVKzsqUJEmSlEMGqitIppLMn/8eAB68
9ECKjRshjntWqNzuJ0mSJI1eBqoriFIRRdMqubOoiFvGjLk4UVcHM2aQGnMb+/YZqCRJkqTRzEDV
hxPNJ/jl6V9ycsy87OPSIdM/tW4dtc9leqruuy8HBUqSJEkaEoZMoAohfCyEsD+E0BJC2BRCWHWV
Z/9zCOG5EMLp7q+fX+356xWlIhgzneNd+dn9U+fPw5YtPdv9Fi+GadMG6lMlSZIkDTdDIlCFEH4L
+BLwOLAMeAH4aQhh6hV+5H7gH4AHgLVACvhZCGHWQNQTpSJKZ1YRgAcuXaF6/vlMqOo+kMLtfpIk
SdLoNiQCFfAo8I04jr8dx/ErwEeBc8BH+no4juMPx3H8v+I43hXH8avAfybzZ1k/EMVEhyNKZt7P
0gkTmFJQcHGirg4mTODo1Ht47TUv9JUkSZJGu5wHqhBCAbACeObCWBzHMfALoOwaXzMeKABO32g9
5zvOs+XIVhrHvq3v/qnycmqT+YD9U5IkSdJol/NABUwF8oDjl40fB2Ze4zv+EjhCJoTdkB3HdtBW
OJU0hdn9U11dkExCZSU1NbBoEcyYcaOfJkmSJGk4GwqB6koCEL/lQyH8KfAB4L1xHLfd6IdGqYiC
yWvIA9aVlFycePnlzKW+69Z5/5QkSZIkAPJzXQBwEugELl/vmU7vVassIYT/CjwGrI/j+OVr+bBH
H32UkkuDErBhwwY2bNgAZAJVyawHuX3iRIrzL/nPU1cHBQUcm7eavXvhiSeu5dMkSZIk5dLTTz/N
008/nTXW2Ng4YO/PeaCK47g9hLCNzIESPwYIIYTu7796pZ8LIfwJ8GngV+I43nGtn/fUU0+xfPny
K9VCfSqiefnv990/tWIFtVuLAFeoJEmSpOHg0sWTC7Zv386KFSsG5P1DZcvfl4HfDyH8dgjhTuB/
AUXANwFCCN8OIfz5hYdDCI8BnydzCuChEMKM7q/xN1LEgfQBjsfjaAmFrL+0fyqOMytU3fdP3XEH
zBqQA9olSZIkDWc5X6ECiOP4n7rvnPocma1/O4F3xnF8ovuROUDHJT/yB2RO9fveZa96svsd/RKl
IihdxpgQKJs48eLEwYNw+HDm/qk/dXVKkiRJUsaQCFQAcRx/Hfj6FeaqLvt+4c2oIZlKMmH6fawu
KWFsXt7Fifp6AE7cUcGePfCZz9yMT5ckSZI03AyVLX9DQjK1ifPFd2Yflw6Z7X533UXtS1MAV6gk
SZIkZQyZFapcO3P+DC+2tBKHwr4PpOi+f+rWW2H27JyUKEmSJGmIcYWq2+bDm4lLllGUCKwsLr44
ceoU7N7dc//UAw/krERJkiRJQ4yBqluUisifspr7SydRkLjkP0syCcDpuyp56SW3+0mSJEm6yEDV
rf7wZrom3sVDffVPzZlDzf75gIFKkiRJ0kUGKqCzq5NkYwNdoeCK/VO1zwUWLoR583JToyRJkqSh
x0AFvHziZVrG38nEBNwzYcLFiXPn4Pnne/qnXJ2SJEmSdCkDFd0X+k5aTtWkSSRCuDixZQt0dNC4
pJJduzyQQpIkSVI2AxVQm9pMmHgX75g8NXuirg5KSqg5eTdx7AqVJEmSpGwGKqCm4TRxyOu7f6qi
gprnEsybBwsW5KQ8SZIkSUPUqA9Ux84e41jBLCYlOnl7UdHFiY4OiCLvn5IkSZJ0RaM+UEWpCEqX
8WBpKeHS/qldu+DsWZqWrmPnTrf7SZIkSept1Aeq6tRWmHA7vzbtluyJujoYM4bnzq0kjl2hkiRJ
ktTbqA9Uvzj1JoQEVZdf6FtfD6tX82w0hjlzYOHC3NQnSZIkaega1YGqtaOVX8bFTAnnmT927MWJ
OM6sUFVW9tw/deluQEmSJEmCUR6oth3dRlfJUtZNnJA98frrcPw4zcvXsX272/0kSZIk9W1UB6qf
HtoC4xfw8Ky3ZU/U1UEIJLvK6OryQApJkiRJfRvVgerfTh0D4B2Tp2RP1NfDPffwzLZSZs2C227L
QXGSJEmShrxRG6jiOOaltkKmxWeZUViYPdndP1VTk9nuZ/+UJEmSpL6M2kD1esPrtE64k7IJY7Mn
jh+HX/6SlpXr2LbN7X6SJEmSriw/1wXkyo8ObIZxs/l/b1mQPVFfD8Cm/Eo6Ow1UkiRJkq5s1K5Q
/eR4CuIu3j19dvZEfT0sXMjPXp7NjBnw9rfnpj5JkiRJQ9+oDVQ72/KY2tXApIKC7Anvn5IkSZJ0
jUZloGpoaaBx7EJWFV2247GpCXbs4PzqdWzd6v1TkiRJkq5uVPZQfe/AFhgzlffPuuy49E2boKuL
beMq6eiwf0qSJEnS1Y3KFaofHDsAXR18YM6i7Im6OpgyhX/ddyfTpsGiRX3+uCRJkiQBozRQPd/S
xeSO40zIv2yBrr4+c/9UbbB/SpIkSdJbGnWBqr2zgxMFs1l22fVTtLXBpk20rVnHli1u95MkSZL0
1kZdoKo+9ioUTOQ3ZszLntixA1paeKG4kvZ2A5UkSZKktzbqAtXPT6Sg8zwfXrA8e6KuDsaN41/e
WM6UKbB4cW7qkyRJkjR8jLpT/l5saWfi+UOUjhmfPVFfD2vX8mx9AffdB4lRFzUlSdKVHDp0iJMn
T+a6DEnXaOrUqcybN++tHxwAoy5QncybRGVhR/ZgVxfU19P++x9j05fgi1/MTW2SJGnoOXToEIsW
LeLcuXO5LkXSNSoqKmLPnj2DEqpGXaAiMYZ3T5uRPbZ3L5w6xe7JlbS1eaGvJEm66OTJk5w7d47v
fOc7LPJOFWnI27NnDx/60Ic4efKkgeqm6DzHf1y4Knusrg7y8vjX02uZNAmWLMlNaZIkaehatGgR
y5cvf+sHJY0qo65TaGxLirkTb8kerK+HpUv52cZi+6ckSZIkXbNRFx0W5p3vPVhXR0f5OjZt8rh0
SZIkSddu1AWq1Dd+yiOf/jRNTU2ZgcOH4cABXp2+jtZWA5UkSZKkazfqAtXZ/++/8rXSUsp+7dcy
oaq+HoB/b6qgpATuvTfHBUqSJEkaNkZdoCIEulavZs+v/iqf+Yu/yASqO+7gX7fNYN06yMvLdYGS
JEkaThYsWMBHPvKRXJehHBl9gapb1+rV/OjZZ6Gujs7ySqLI7X6SJGn0+da3vkUikaCoqIg33nij
1/wDDzzAPffcM2Cf9+STT5JIJHq+8vLyuOWWW/j1X/91Nm/enPXswYMHe577wQ9+0OtdTzzxBIlE
gtOnT1/1Mzdu3MiTTz7JmTNnBuzPcalEIkEI4aa8+7HHHiORSLBhw4arPtfU1MSTTz7J0qVLKS4u
pqioiCVLlvCpT32qz7/Xmpoa3ve+9zFr1izGjBnDjBkzeM973tPnf2dd3agNVITAqdZW4l272HfL
OlpavH9KkiSNXufPn+cv/uIveo3fjKAQQuAb3/gG3/nOd/jWt77FJz7xCV566SXuv/9+du3a1efz
n/vc5/ocv5b6oijic5/7HOl0ekDqv9zevXv567/+65vy7n/8x39k4cKF/OQnP6G5ubnPZ/bt28e9
997LF77wBRYvXswXv/hFvvrVr1JVVcXf/u3f8uCDD2Y9/8QTT1BVVcXu3bv56Ec/yje+8Q0ee+wx
mpubef/7388//uM/3pQ/y0g1+u6huiCO4dQJAvCL1kqKi2Hp0lwXJUmSRoI4jm/aisXNevfSpUv5
m7/5Gz71qU8xc+bMAX//5R5++GEmT57c8/1v/MZvcPfdd/N//s//6bUitnTpUnbu3MkPf/hD3vve
9173Z8VxfF3PtrW1MWbMmGv+mYKCguuu6Vo8++yzHDlyhGeffZZ3vOMdfP/73+fDH/5w1jOdnZ28
733v48SJE9TW1lJWVpY1/4UvfIG//Mu/7Pn+e9/7Hp/73Of4wAc+wHe/+13yLul3+eM//mN+/vOf
097eflP+PCPV6F2h2rSRFa3NxDNn8oNdt1JZCfmjN15KkqQb1NTUxCOPPM7ChQ8xd+57WbjwIR55
5PGLJwsP0XdDZqXn05/+NB0dHX2uUl2us7OTz3/+89x2222MHTuWhQsX8pnPfIa2trZ+1zBjxgwA
8vv4B9kHP/hBbr/99j5Xqd7Kk08+yWOPPQZkep0ubDM8dOgQkNmu98gjj/AP//AP3H333YwdO5af
/vSnAPzVX/0VFRUVTJ06laKiIlauXMk///M/9/qMy3uoLmyjjKKIT37yk0yfPp0JEybwvve9j1On
Tl1z7d/97ne56667uO+++3jooYf47ne/2+uZ733ve+zatYvPfOYzvcIUwIQJE/j85z/f8/1nP/tZ
pkyZwt/+7d9mhakL3vGOd/Crv/qr11yjRmOgimPYGMG3v8wTZ5uJyyuJNga3+0mSpH5ramqirOxh
vva1Mg4c+DlHjvyIAwd+zte+VkZZ2cM3FHxu5rsvtXDhQn77t3+bv/mbv+HYsWNXffZ3f/d3efzx
x1m5ciX/83/+Tx544AH+/M///C37fC516tQpTp06xYkTJ9ixYwe/93u/x7hx4/jABz7Q69m8vDw+
85nP9KxSXY+HH364p66vfOUrfOc73+Hv//7vmTZtWs8zzzzzDH/8x3/MBz/4Qb7yla+wYMECAL76
1a+yfPlyPv/5z/Pf//t/p6CggA984AP827/9W9ZnXGnF8BOf+AQvvvgiTzzxBH/4h3/IT37yEz7+
8Y9fU91tbW18//vf5z/8h/8AwIYNG6iurubNN9/Meu7HP/4xIQQ+9KEPveU7X3vtNfbu3ctv/uZv
Mn78+GuqQ9cgjuNR8QUsB2LeNjVm/fh47PuJ2/MS8f5HvxJDHG/aFEuSJPWybdu2GIi3bdt2xWc+
8Yk/ixOJf4sz/5/b7K9E4l/jRx55vN+ffzPfHcdx/M1vfjNOJBLxtm3b4n379sUFBQXxH/3RH/XM
P/DAA/GSJUt6vn/hhRfiEEL8X/7Lf8l6z5/8yZ/EiUQirqmpuernPfHEE3EIodfX5MmT45/97GdZ
zx44cCAOIcRf+tKX4s7OzviOO+6Ily1blvWuRCIRnzp16qqf+Vd/9VdxIpGIDx482GsuhBDn5+fH
r7zySq+51tbWrO87OjriJUuWxA899FDW+IIFC+Lf+Z3f6fn+m9/8ZhxCiN/5zndmPffJT34yLigo
iM+cOXPVeuM4jr/3ve/FiUQifv311+M4juOmpqZ43Lhx8Ve+8pWs55YvXx5PmjTpLd8Xx3H84x//
OA4h9HrHSHMt/zd74RlgeXyDOWP0rVA9dJL/v707j8uyyv8//jq3oiLgnkjmgktqpeOAa6bi0mAk
6pBroWaWlblW06KW4pY5KelvMkfTQRM010SzHM20xrVAym85jpnYpKXlguSCC+f3B3CPt4DCDQri
+/l4XI+4znWucz7XzU3en/uc61wOv3N0/64mxS+n8tnFB/D2hoCAgg5MREREblVr1mwlNTU4y2Op
qZ1Yvnwr8fG4tS1ffu22Y2O35tt1+Pv707dvX+bMmcPRo0ezrLNu3TqMMYwcOdKl/IUXXsBay0cf
fXTdfowxrFq1io0bN7JhwwaioqK4++67CQsLY8eOHVme43A4nKNUq1evzv3FXUNQUBD16tXLVH7l
fVSnTp3i5MmTtG7dmvj4+Ou2aYxh0KBBLmWtW7fm8uXLHDp06Lrnx8TE0KRJE2rVqgWkTd17+OGH
M037O336ND4+PtdtL6MukOP6kjO33V1Dfp/70aNLD6bWLg/Tp7P8P41o1Qpu0L2EIiIiUsRZa7l4
0QvIbqEIw5EjpQkMtNeok23rwLXbvnixdL4uVDFmzBjef/99pkyZQmRkZKbjGUuZ16lTx6Xc19eX
cuXK5ShZgLTk4spFKR555BHq1q3L0KFD+fLLL7M857HHHmPixImMHz+erl275uKqri1jit/V1q5d
y6RJk0hISCAlJcVZ7nDkbEyiWrVqLvvly5cH4OTJk9c8LykpiXXr1jF06FAOHDjgLL///vtZuXIl
33//vfP1L1OmDAcPHsxRPGXKlAHIt2mikua2S6jWRq8lICAAHn6Y1BYt+XxbcUaNKuioRERE5FZl
jMHD4wxpyU9WSY3Fz+8Ma9e6k/AYOnc+w88/Z9+2h8eZfF31z9/fn/DwcObMmcPLL7+cucf0FfPy
e6VBLy8vmjdvTmxsLOfOncPT0zNTHYfDwejRoxkwYACxsbH51ndWfX3xxRd07dqVoKAg3n33Xfz8
/PDw8GD+/PksXrw4R+1mtegDXH/VwaVLl5KSksK0adN46623XI4ZY4iOjmbs2LEA1K/PWn2+AAAg
AElEQVRfn4SEBA4fPkzVqlWv2W79+vUB2LNnT47il5y5/ab8AVy+DFu3cqRWa37/Xc+fEhERkbwJ
DW2Fw7E+y2MOxyf06PEAAQG4tXXvfu22u3R5IN+vZ8yYMVy8eNFlue0MNWvWJDU1lf3797uUHzt2
jFOnTlGjRg23+7106RIAv//+e7Z1wsPDqV27NhERETleDt2d5G/lypV4enqyfv16Hn/8cYKDg2nf
vn2ulmB3V0xMDA0bNmTZsmUsX77cZevQoYPLtL/Q0FCstSxatOi67datW5d69eqxevVqzp49eyMv
4bZyeyZU334LSUn8iwcoXRqaNCnogERERORWNmnSizRoMB2H42PSRqoALA7HxzRoEMnEiS8Uyraz
U6tWLcLDw/n73/+eacW/kJAQrLW8/fbbLuXTpk3DGMPDDz/sVp8nTpxg27Zt+Pn5uazAd7WMe6l2
796d41GqjBXtcvNg32LFimGMcSZ5AImJifl+/9bVfvrpJz7//HN69epFWFhYpm3AgAEcOHDAOS2y
e/fuNGzYkEmTJmV5/1lycjJjxoxx7kdERPDbb78xcOBALl++nKn+hg0bcnQfnPzPbTflD4AvvgAP
D5YmNuP++3X/lIiIiOSNj48P27evYMyYacTGTufixdJ4eJylS5dWTJy4Ik+LANzItjNkNeoyevRo
3n//ffbt28d9993nLG/UqBH9+/dnzpw5nDx5krZt27Jz504WLlxIWFgYbdu2zVF/y5Ytw9vbG2st
hw8fZv78+Zw6dSrLUbGrhYeHM3HiRBISEnI0+hQYGIi1llGjRtG7d288PDzo0qVLllP9MnTu3Jnp
06cTHBzMo48+ytGjR5k1axZ169blm2++ydE15qY8Q8boU2hoaJbHQ0JCKFasGNHR0TRt2pTixYuz
cuVKHnzwQdq0aUPPnj1p1aoVHh4efPvtt8TExFChQgUmTpwIQM+ePdmzZw+TJ09m9+7d9OnThxo1
anD8+HE++eQTNm3aRExMzHWvT/7n9kyo/vUvbEAgn24vTfpz3kRERETyxMfHhxkzxjFjBvm6SMSN
bhuynhJXu3Zt+vbty4IFCzIdnzdvHrVr1yYqKooPP/yQKlWqMHr0aF5//fUc9zd48GDnvpeXF40a
NeKNN94gLCwsU92r+8+4l+qJJ57I0WvRpEkTJk6cyOzZs1m/fj2pqakcPHiQ6tWrZ9k+pK38N3/+
fKZMmcLIkSPx9/dn6tSpHDx4MFNClVUb2cV1vXhjYmKoXr06DRs2zPJ42bJleeCBB/jggw+YPn06
DoeD2rVrk5CQQGRkJKtWrWL16tWkpqZSp04dBg0axNChQ13amDBhAh06dGDmzJnMnj2bEydOUL58
eVq0aEFsbKzbo4y3K3Mz5oEWBsaYACAu7quvCOjalV/aP4rf+1P54gt4IP+nHouIiEgRER8fT2Bg
IHFxcWkLW4lIoZaTv9mMOkCgtfb66+Bfw+13D9XPP8Phw+wo/gClSkHTpgUdkIiIiIiI3Kpuv4Rq
924Alh1pxf33wxXPaxMREREREcmV2y+hSkjA3nMP63ZWJAf3TIqIiIiIiGTr9kuo4uM53qA1p07p
+VMiIiIiIpI3t19ClZjIV6UeoGRJaNasoIMREREREZFb2e2XUAErf21NixZQqlRBRyIiIiIiIrey
2y6hsr6+rPiqhqb7iYiIiIhInt12CVVy7cacOIEWpBARERERkTy77RKqfaX/SIkS0KJFQUciIiIi
IiK3utsuofo8qTHNm4OnZ0FHIiIiIiIit7rbLqH64quRlDo3jOTk5IIORUREREREbnG3XUK1yv7M
iPh3eKRlSyVVIiIiIoXQggULcDgcxMfHF3QoRcaWLVtwOBx8/vnnBR1KkXPbJVQGCElNZeTevUwb
M6agwxEREREpUBnJy5Wbr68v7du355NPPnG73TfeeIPVq1e7fb4xJkf1goKCcDgcdO3aNdOxQ4cO
4XA4mD59uttx3EzvvvsuCxYsuGHt5/Q1za3U1FT8/PxwOBysX7/+mnUTEhIIDw+nevXqlCpViooV
K/Lggw8SFRVFamqqS92UlBQiIyNp0aIF5cqVw9PTk3r16jF06FD2799/Q67FHcULOoCC0ik1lemx
sTBjRkGHIiIiIlKgjDFMmDCBmjVrYq3l6NGjREVFERISwtq1awkJCcl1m5MnT6ZHjx5ZJjr5yRiD
MYa1a9eye/du/vjHP97Q/m6kWbNmcccdd9C/f/98b7tt27acO3eOEiVK5HvbmzZt4ujRo/j7+xMd
HU1wcHCW9d577z2effZZqlSpQt++falbty7Jycls2rSJJ598kl9++YVXXnkFgOPHjxMcHMzu3bvp
3Lkzjz32GN7e3uzbt48lS5Ywd+5czp8/n+/X4o5Ck1AZY54DXgSqAF8DQ621X2ZT9x5gPBAI1ABG
WGtn5qo/oPTFi1hrb1i2LiIiIrenG/n54ka13alTJwICApz7TzzxBL6+vixevNithOpmql69OsnJ
yURERPDhhx/esH5SUlIoUaJEofjsePbsWUqXLp2rc25EMgWwaNEiAgMD6d+/P6NGjeLcuXN4XrUC
3I4dO3j22Wdp1aoV69atc4l92LBhxMfH83//93/Osv79+/P111+zYsUKunXr5tLWhAkTGDVq1A25
FncUiil/xphewDRgLPBH0hKq9caYStmcUho4ALwM/OxOnxY44+FRKP4gRERE5NaXnJzMsJeG4R/g
T7Vm1fAP8GfYS/mzENaNbDs7GVOsihd3/f79rbfeolWrVlSqVInSpUvTpEkTVqxY4VLH4XBw9uxZ
oqKinNMIn3jiCefxI0eOMHDgQKpWrUqpUqWoVasWgwcP5tKlSy7tpKSk8Pzzz1O5cmW8vb0JCwvj
+PHjmWL18fFh5MiRxMbGkpCQcN1rO3jwID169KBixYp4eXnRsmVL1q1b51In456jDz74gDFjxlCt
WjW8vLxITk52XtfWrVsZNmwYlStXpnz58jzzzDNcunSJpKQk+vXrR8WKFalQoQIvv/zydWPy9/fn
22+/ZfPmzc7XrH379gDO/j7//HMGDx6Mr68v1apVA+DHH39k8ODB1K9fn9KlS1OpUiV69uzJoUOH
sryeK++hCgoKolGjRuzdu5d27drh5eXFXXfdxV//+tfrxpvh/PnzrFq1ij59+tCjRw/Onj2b5VTP
iIgIHA4HixYtyjIRDAgIoF+/fgDs2rWLdevW8eSTT2ZKpgA8PDxyFeONVlhGqEYCf7fWLgQwxjwD
PAw8AUy9urK19ivgq/S6b7rT4ccOBw906eJ2wCIiIiIZkpOTafmnluyts5fULqlpU2EsvPPDO2z6
0ya2/3M7Pj4+ha7tKyUlJXH8+HGstRw7doyZM2dy5swZ+vbt61Jv5syZdO3alfDwcC5cuMCSJUvo
2bMna9eu5aGHHgLSRiwGDhxI8+bNGTRoEAC1a9cG4Oeff6Zp06acPn2ap59+mnr16nH48GGWL1/O
2bNnKVOmDJA2EjdkyBAqVKjAuHHjSExMJDIykiFDhrB48eJM8Q8fPpzp06czbty4a45SHTt2jJYt
W3L+/HmGDx9OhQoVWLBgAaGhoaxcuTLTFMUJEyZQsmRJXnzxxUwjVEOHDsXPz4/x48ezY8cO5s6d
S7ly5di2bRs1atRg8uTJrFu3jrfeeouGDRsSHh6ebVwzZsxgyJAh+Pj4MGbMGKy1+Pr6Av+792nw
4MFUrlyZsWPHcubMGQC+/PJLduzYQZ8+fbjrrrtITExk1qxZtGvXju+++45SpUo5+7h6IMEYw4kT
J3jooYcICwujd+/eLF++nFdeeYVGjRplO3XvSqtXr+bMmTP06tULX19fgoKCiI6Opnfv3s46586d
Y9OmTbRp04a77rrrum3GxsZijLnm61WoWGsLdAM8gItAl6vKo4BVOTj/IDAsB/UCAPsV2FgctmZJ
L3v48GErIiIici1xcXEWsHFxcdnWGfqXodYR7rCMI9PmCHfYYS8Nc7v/G9m2tdZGRUVZY0ymzdPT
0y5cuDBT/fPnz7vsX7p0yTZs2NB27NjRpdzb29sOGDAg0/n9+vWzxYsXt/Hx8deNKTg42KX8+eef
tx4eHvb06dPOsqCgINuwYUNrrbXjx4+3DofD7t6921prbWJiojXG2GnTpjnrjxgxwjocDrtt2zZn
2e+//25r1apla9Wq5SzbvHmzNcbYOnXq2JSUlCzjCwkJcSm///77rcPhsEOGDHGWXb582VarVs22
a9cu2+vNcN9992VZL6O/tm3b2tTUVJdjV/8+rLV2586d1hhjFy1a5HI9DofDbtmyxVkWFBRkHQ6H
jY6OdpZduHDBVqlSxfbo0eO68VprbWhoqG3durVzf+7cubZEiRL2t99+c5Z988031hhjR44cmaM2
w8LCrMPhsElJSTmqf7Wc/M1m1AECbB7zmcIw5a8SUAw4elX5UdLup8pX3fCjL0M4dGEBb745J7+b
FxERkdvQmo1rSK2dmuWx1NqpLF+/nPif493alq9ffs22YzfG5jl+YwzvvvsuGzduZOPGjURHR9Ou
XTsGDhyYabSnZMmSzp9PnTrFyZMnad26dY6WOLfWsnr1arp06XLdxSOMMc7RrQytW7fm8uXLmaaz
ZRg+fDjlypUjIiIi23Y//vhjmjVrRsuWLZ1lXl5eDBo0iMTERL777juX+o8//niW9x4ZY1ymMQI0
b94cgAEDBjjLHA4HTZo04Ycffsg2ppwwxvDUU09lGmW68vdx6dIlTpw4Qa1atShfvnyOfideXl48
+uijzn0PDw+aN2+eo3hPnDjB+vXrXc5/5JFHAFi6dKmz7PTp0wA5HknNbf2CVlim/GUlfUA7f/1E
XeAg2IPMnbudgwfj6dOnD3369MnvrkREROQ2YK3lYrGLaZ9csmLgyPkjBP49MPs62TYOpHDNti86
8meRraZNm7osStG7d28CAgIYMmQInTt3dt5LtXbtWiZNmkRCQgIpKSnO+g7H9b+n//XXXzl9+jT3
3ntvjmLKuE8oQ/ny5QE4efJklvXLlCnDiBEjGDduHF9//TXlypXLVOfQoUO0aNEiU3mDBg2cx++5
5x5nec2aNbONr3r16i77ZcuWzTLusmXLZhtzbmQVy/nz55k8eTJRUVEcPnw4Y2YWxhiSkpKu2+bV
sULa67xnz57rnrtkyRIuXbpE48aNOXDgAJD299C8eXOio6N59tlnAZzTOHN6z9+V9TN+zovFixdn
miaak9cmpwpDQvUbcBnwvaq8MplHrfJBJGmz/6BCha6sXv2hFqYQERERtxlj8LjskZb8ZPWRwoJf
ST/WPr3WrfY7r+rMz/bnbNv2uHxjFtkyxhAUFMTMmTPZv38/DRo04IsvvqBr164EBQXx7rvv4ufn
h4eHB/Pnz8/yvqZM4drcfVderFixXLczfPhwIiMjiYiIIDIyMlf9ZeXq1epyEl9W5bm99pzGMmTI
EBYsWMDIkSNp0aIFZcuWxRhDr169Mj3XKaex5jTemJgYAO6//36X8oz3Y2JiIjVr1qROnToUL148
R0kaQP369QHYs2cPrVq1ytE515LV4El8fDyBgYF5bhsKQUJlrb1ojIkDOgCxACbtt9AByNVS6Lns
GQ+PM0qmREREJM9CO4byzg/vZDk1z3HAQY9OPQjwC8jizOvrHtz9mm13efDGLbKVsere77//DsDK
lSvx9PRk/fr1Lqv/zZs3L9O5WX3Gqly5MmXKlHFZHju/ZYxSRUREOFeNu1KNGjXYt29fpvK9e/c6
jxcUdz6Xrlixgscff5ypU/+3jltKSgqnTp3Kz9AySUxMZNu2bQwbNow2bdq4HEtNTSU8PJyYmBhG
jRqFp6cn7du357PPPuPw4cNUrVr1mm2HhobyxhtvsGjRonxJqG60wnAPFcB0YJAxpp8xpj4wm7Sl
0aMAjDELjTGTMyobYzyMMX8wxjQGSgBV0/dr57RDh+MTunR5IF8vQkRERG5Pk16bRIP9DXB87/jf
DQsWHN87aPB9AyaOmVgo276WS5cusX79ekqUKOGcDlesWDGMMS7LmycmJma5TLaXl1emD/XGGLp1
68aaNWtydH+Pu0aMGEHZsmUZP358piQlJCSEXbt2sXPnTmfZmTNnmDNnDv7+/i7T/W62rF6z6ylW
rFimkaiZM2dy+fLl/Awtk0WLFmGM4cUXXyQsLMxl6969O23btiU6OtpZf+zYsaSmptK3b1/nCoVX
iouLY+HChQC0aNGCTp068d5772X53rpw4QIvvfTSjbu4XCrwESoAa+3S9GdOjSdt6l8CEGyt/TW9
yl3AlQ8muBPYzf/+t/Ji+rYFaH+d3nA4PqZBg0gmTlxx7aoiIiIiOeDj48P2f25nzMQxxK6J5aLj
Ih6pHnTp2IWJsybm6eb6G9l2Bmst69atc47SHDt2jOjoaA4cOMCrr76Kt7c3AJ07d2b69OkEBwfz
6KOPcvToUWbNmkXdunX55ptvXNoMDAxk48aNREZGcuedd+Lv70+zZs2YPHkyGzZsoE2bNgwaNIgG
DRpw5MgRli9fztatW12WTc8u1uspU6YMw4cPJyIiIlNC9corr7B48WI6derEsGHDqFChAlFRURw6
dIiVK1fm6jXLb4GBgcyePZtJkyZRp04dKleuTLt27a7ZX+fOnXn//fcpU6YM99xzD9u3b+fTTz+l
UqXMj3PNz5ijo6Np3Lhxtsugd+nShaFDh5KQkEDjxo1p2bIl77zzDs899xz169enb9++1K1bl+Tk
ZDZv3kxsbCyTJk1ynr9w4UKCg4N55JFHePjhh+nYsSNeXl7s37+fJUuW8Msvv7iMyhWkQpFQAVhr
ZwGzsjnW/qr9Q7g5uubnN5gePR5i4sQVt8zKISIiIlL4+fj4MOPNGcxgRr4sEnGz2oa0kaOxY8c6
90uVKkX9+vWZPXs2Tz31lLM8KCiI+fPnM2XKFEaOHIm/vz9Tp07l4MGDmRKq6dOn8/TTT/Paa69x
7tw5+vfvT7NmzbjzzjvZuXMnr732GjExMZw+fZqqVasSEhLi8sDX7K4xq/KsykaMGMGMGTMyLT5Q
uXJltm/fzssvv8zf/vY3zp8/T6NGjVi7di2dOnW6brs5OeZu/ddff50ff/yRv/71ryQnJ9O2bVtn
QpXd+TNnzqR48eLExMRw/vx5HnjgATZu3EhwcHCWz53KaVzXinf37t385z//4fXXX8+2TmhoKMOG
DWPRokU0btwYgEGDBtGsWTOmTZvG+++/z6+//oq3tzcBAQEsWLCAxx57zHl+pUqV2LZtG7NmzXI+
XPnChQvUqFGDbt26MWzYsGz7vtnMjciuCyNjTAAQFxcX57KCjYiIiMi1ZNy8rs8QIreGnPzNXrEo
RaC1Nk/zTwvLPVQiIiIiIiK3HCVUIiIiIiIiblJCJSIiIiIi4iYlVCIiIiIiIm5SQiUiIiIiIuIm
JVQiIiIiIiJuUkIlIiIiIiLiJiVUIiIiIiIiblJCJSIiIiIi4iYlVCIiIiIiIm5SQiUiIiIiIuIm
JVQiIiIiIiJuUkIlIiIiIpILUVFROBwOfvzxx4IORQoBJVQiIiIit7EFCxbgcDgoXbo0P//8c6bj
QUFBNGrUKN/6i4iIwOFwOLdixYpx5513Ehoays6dO13qHjp0yFlv1apVmdoaN24cDoeDEydO5Ft8
OWGMwRiTq3NeeuklHA4Hffr0uWa95ORkIiIiaNy4MT4+PpQuXZqGDRvy6quvZvn72bx5M2FhYfj5
+VGyZEl8fX3p0qVLlq+X3BjFCzoAERERkaLGWpvrD9wF3XZKSgpTpkxhxowZLuU3oi9jDLNnz8bL
y4vU1FT++9//MmfOHNq2bcuuXbsyJXDGGMaPH8+f//znTOU36nXOb0uWLMHf3581a9Zw5swZvLy8
MtX54Ycf6NixIz/99BM9evTg6aefxsPDgz179jBv3jxWrVrFv//9b2f9cePGMX78eO6++26eeeYZ
atSowfHjx1m3bh3du3cnOjqa3r1738zLvC0poRIRERHJB8nJybw1ejRb16zB6+JFznh40Co0lBcn
TcLHx6fQtp2hcePGzJ07l1dffZUqVarkS5vX8sgjj1ChQgXnfteuXbnvvvtYtmxZpoSqcePGJCQk
8OGHH9KtW7cbHlt+++yzzzh8+DCfffYZDz74ICtXrqRv374udS5fvkxYWBi//vorW7ZsoWXLli7H
J02axJtvvuncX758OePHj6dnz55ER0dTrFgx57EXXniBDRs2cPHixRt7YQJoyp+IiIhIniUnJ/NI
y5a0fOcdNiQmsvrwYTYkJtLynXd4pGVLkpOTC2XbGYwxjBo1ikuXLjFlypTr1r98+TITJkygTp06
lCpVCn9/f8aMGcOFCxfcjsHX1xeA4sUzf9/fu3dv6taty/jx43Pd7vLly3E4HPzrX//KdGz27Nk4
HA727t0LwJ49exgwYAC1a9fG09MTPz8/Bg4cmOcphdHR0dxzzz20adOGjh07Eh0dnWWc33zzDWPG
jMmUTAF4e3szYcIE5/5rr71GxYoVmTdvnksyleHBBx8kJCQkT3FLziihEhEREcmjt0aP5vm9e+mU
mkrGBDQDdEpNZeTevUwbM6ZQtn0lf39/+vXrx9y5c/nll1+uWXfgwIGMHTuWJk2a8PbbbxMUFMTk
yZOve3/QlY4fP87x48f59ddf2b17N0899RSenp707NkzU91ixYoxZswY5yhVbnTu3Blvb28++OCD
TMeWLVvGvffeS4MGDQDYsGEDBw8e5IknnuBvf/sbffr0YcmSJTz88MO56vNKFy5cYOXKlTz66KMA
9OnTh02bNnHs2DGXerGxsRhjCA8Pv26b33//Pfv27ePPf/5zllMH5eZSQiUiIiKSR1vXrCE4NTXL
Y51SU9m6fDnEx7u1bV2+/Nptx8bm23WMHj2aixcvukwtu9o333zDwoULGTRoEEuWLOGZZ57hH//4
By+++CIffvghW7ZsuW4/1lrq1avHHXfcga+vL4GBgWzZsoUPP/zQmdxc7dFHH3VrlKpUqVKEhoay
fPlyrLXO8mPHjrFlyxaXJPC5555j8+bNjB49moEDBzJ9+nTmz5/Prl272Lp1a676zbBmzRqSkpLo
1asXAN26daN48eIsWbLEpd6///1vypYtS9WqVa/bZsaI2n333edWTJK/lFCJiIiI5IG1Fq+LF8lu
aQQDlD5yBBsYCLncbGAgXj//fO22L150SRTywt/fn759+zJnzhyOHj2aZZ1169ZhjGHkyJEu5S+8
8ALWWj766KPr9mOMYdWqVWzcuJENGzYQFRXF3XffTVhYGDt27MjyHIfD4RylWr16da6uq1evXhw7
dozNmzc7y5YuXYq11mVErGTJks6fU1JSOH78OM2bN8daS3x8fK76zBATE0OTJk2oVasWkDZ17+GH
H8407e/06dM5vh/u9OnTAPl2/5zkjRIqERERkTwwxnDGw4PsUhoLnPHzw8TFQS43ExfHGT+/a7ft
4ZGvK92NGTOGixcvZnsvVcZS5nXq1HEp9/X1pVy5chw6dChH/bRu3Zr27dvToUMH+vXrx8aNG/Hx
8WHo0KHZnvPYY4+5NUrVqVMnypQp4zLtb+nSpTRu3NjlOk6ePMnw4cOpUqUKnp6e3HHHHdSqVQtj
DElJSbnqEyApKYl169bRtm1bDhw44Nzuv/9+vvrqK77//ntn3TJlyuT4frgyZcoA5Mv9c5J3SqhE
RERE8qhVaCjrHVl/rPrE4eCBHj0gIMCtrVX37tduu0uXfL0Wf39/wsPDmTNnTpb3UmWMhuX3cuVe
Xl40b96c+Ph4zp07l2Udh8PB6NGjSUhIIDYXUx1LlChB165dWblyJampqRw+fJitW7dmuuerR48e
zJs3j8GDB7Nq1So2bNjA+vXrsdaSms20y2tZunQpKSkpTJs2jbp16zq3F154AcBllKp+/fokJSVx
+PDh67Zbv359IG0RDSl4SqhERERE8ujFSZOY3qABHzscztEkC3zscBDZoAEvTJxYKNvOTsYoVVb3
UtWsWZPU1FT279/vUn7s2DFOnTpFjRo13O730qVLAPz+++/Z1gkPD6d27dpERETkaqpj7969OX78
OJ9++inLli0D0hKoDKdOnWLTpk28+uqrvP7663Tt2pUOHTrg7+/v5tWkTfdr2LAhy5YtY/ny5S5b
hw4dXBKq0NBQrLUsWrTouu3WrVuXevXqsXr1as6ePet2fJI/lFCJiIiI5JGPjw8rtm9n55Ah/Klm
TbpWrcqfatZk55AhrNi+PU/3utzItrNTq1YtwsPD+fvf/55plCokJARrLW+//bZL+bRp0zDGuL0i
3okTJ9i2bRt+fn7ccccd2dbLuJdq9+7duRql6tixI+XLl2fJkiUsXbqUZs2auSR/GUuPXz0SFRkZ
6dZo3E8//cTnn39Or169CAsLy7QNGDCAAwcO8OWXXwLQvXt3GjZsyKRJk7K8jyw5OZkxV6zoGBER
wW+//cbAgQO5fPlypvobNmzI0f1sknd6sK+IiIhIPvDx8WHcjBkwYwbW2nydEncj2wayHOkZPXo0
77//Pvv27XNZTa5Ro0b079+fOXPmcPLkSdq2bcvOnTtZuHAhYWFhtG3bNkf9LVu2DG9vb6y1HD58
mPnz53Pq1KlrrjCYITw8nIkTJ5KQkJDj16J48eKEhYWxZMkSzp49y1tvveVy3MfHhzZt2jB16lQu
XLhA1apV+ec//8nBgwfdWvQjY/QpNDQ0y+MhISEUK1aM6OhomjZtSvHixVm5ciUPPvggbdq0oWfP
nrRq1QoPDw++/fZbYmJiqFChAhPTRyR79uzJnj17mDx5Mrt376ZPnz7UqFGD48eP88knn7Bp0yZi
YmJyHbfknhIqERERkXyW3wnPjW47qzZr165N3759WbBgQabj8+bNo3bt2kRFRePNpDgAABqWSURB
VPHhhx9SpUoVRo8ezeuvv57j/gYPHuzc9/LyolGjRrzxxhuEhYVlqnt1/xn3Uj3xxBO5ej169erF
vHnzcDgcLtP9MixevJihQ4cya9YsrLUEBwfzySefcOedd+b6dY+JiaF69eo0bNgwy+Nly5blgQce
4IMPPmD69Ok4HA5q165NQkICkZGRrFq1itWrV5OamkqdOnUYNGhQpgU7JkyYQIcOHZg5cyazZ8/m
xIkTlC9fnhYtWhAbG5un52dJzpn8WmazsDPGBABxcXFxBAQEFHQ4IiIicouIj48nMDAQfYYQuTXk
5G82ow4QaK11b038dLqHSkRERERExE1KqERERERERNykhEpERERERMRNSqhERERERETcpIRKRERE
RETETUqoRERERERE3KSESkRERERExE1KqERERERERNykhEpERERERMRNSqhERERERETcpIRKRERE
RETETUqoRERERKRQWbBgAQ6Hg/j4+IIO5ZYWFBRE+/btCzqMIk8JlYiIiMhtLCN5uXLz9fWlffv2
fPLJJ263+8Ybb7B69Wq3zzfG5KheUFAQDoeDrl27Zjp26NAhHA4H06dPdzuOW1lOX8MMqamp+Pn5
4XA4WL9+/TXrJiQkEB4eTvXq1SlVqhQVK1bkwQcfJCoqitTUVJe6KSkpREZG0qJFC8qVK4enpyf1
6tVj6NCh7N+/P9fXVdgUL+gARERERKRgGWOYMGECNWvWxFrL0aNHiYqKIiQkhLVr1xISEpLrNidP
nkyPHj2yTHTykzEGYwxr165l9+7d/PGPf7yh/RVlmzZt4ujRo/j7+xMdHU1wcHCW9d577z2effZZ
qlSpQt++falbty7Jycls2rSJJ598kl9++YVXXnkFgOPHjxMcHMzu3bvp3Lkzjz32GN7e3uzbt48l
S5Ywd+5czp8/fzMvM98poRIRERHJZ9baXI8OFHTbnTp1IiAgwLn/xBNP4Ovry+LFi91KqG6m6tWr
k5ycTEREBB9++OEN6yclJYUSJUrcsN9tQVu0aBGBgYH079+fUaNGce7cOTw9PV3q7Nixg2effZZW
rVqxbt06Spcu7Tw2bNgw4uPj+b//+z9nWf/+/fn6669ZsWIF3bp1c2lrwoQJjBo16sZe1E2gKX8i
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
sPsD0NAYE35FmUn/rz+wL/3nuKtPNMb0AoYCtQFv0v7dS8pl//WBr9OTqQxbSZvlUQ/ISKi+ta4r
Pf1M2oiaiIgUYUqoRESksPMm7Z6oGfwvkcrw4xU/n7nygDGmBbCItCmE/yQtkeoDPJ/L/g1ZLFyR
7sryqxfBsGhqvYhIkaeESkRECpMLwNULOcQD91prD+ayrfuBRGvtlIwCY0zNHPR3te+AfsYYT2vt
ufSyB4DLwH9yGZOIiBQx+uZMREQKk0SgjTHmTmNMxfSyN4GWxpj/Z4z5gzGmjjGmqzHm6kUhrrYf
qG6M6WWMqWWMGQZ0y6I///R2KxpjSmTRTjRwHlhgjLnXGNMOmAksvM69VyIichtQQiUiIgXtymlz
rwM1gQPAMQBr7R6gLVAX+Jy0EatxwOFs2iD9vDVAJGmr8e0GWgDjr6q2grQV/D5L76/31e2lj0oF
AxWAXcBSYANp92aJiMhtzrjePysiIiIiIiI5pREqERERERERNymhEhERERERcZMSKhERERERETcp
oRIREREREXGTEioRERERERE3KaESERERERFxkxIqERERERERNymhEhERERERcZMSKhERERERETcp
oRIREREREXGTEioRERERERE3/X/7fQ0RX+5w4gAAAABJRU5ErkJggg==
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[25]:</div>
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
<pre>Validation set accuracy:  0.68
Test set accuracy:  0.665
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[26]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Remove max pool layer</span>
<span class="c1"># Try more epochs</span>
<span class="n">layers</span> <span class="o">=</span> <span class="p">[</span>
  <span class="p">[</span><span class="s1">&#39;conv&#39;</span><span class="p">,</span>  <span class="p">{</span><span class="s1">&#39;num_of_filters&#39;</span><span class="p">:</span><span class="n">f</span><span class="p">,</span> <span class="s1">&#39;filter_size&#39;</span><span class="p">:</span><span class="mi">3</span><span class="p">}],</span>
  <span class="p">[</span><span class="s1">&#39;relu&#39;</span><span class="p">],</span>
  <span class="p">[</span><span class="s1">&#39;spatial_batchnorm&#39;</span><span class="p">],</span> <span class="c1"># normalize before affine</span>
  <span class="p">[</span><span class="s1">&#39;affine&#39;</span><span class="p">,</span> <span class="p">(</span><span class="mi">500</span><span class="p">)],</span>
  <span class="p">[</span><span class="s1">&#39;relu&#39;</span><span class="p">],</span>
  <span class="p">[</span><span class="s1">&#39;batchnorm&#39;</span><span class="p">]</span> <span class="c1"># for last affine layer</span>
<span class="p">]</span>

<span class="n">model</span> <span class="o">=</span> <span class="n">convnetGenerator</span><span class="p">(</span><span class="n">layers</span><span class="o">=</span><span class="n">layers</span><span class="p">,</span> <span class="n">weight_scale</span><span class="o">=</span><span class="mf">0.001</span><span class="p">,</span> <span class="n">reg</span><span class="o">=</span><span class="mf">0.001</span><span class="p">)</span>

<span class="n">solver</span> <span class="o">=</span> <span class="n">Solver</span><span class="p">(</span><span class="n">model</span><span class="p">,</span> <span class="n">data</span><span class="p">,</span>
                <span class="n">num_epochs</span><span class="o">=</span><span class="mi">10</span><span class="p">,</span> <span class="n">batch_size</span><span class="o">=</span><span class="mi">50</span><span class="p">,</span>
                <span class="n">update_rule</span><span class="o">=</span><span class="s1">&#39;adam&#39;</span><span class="p">,</span>
                <span class="n">optim_config</span><span class="o">=</span><span class="p">{</span>
                  <span class="s1">&#39;learning_rate&#39;</span><span class="p">:</span> <span class="mf">1e-3</span><span class="p">,</span>
                <span class="p">},</span>
                <span class="n">verbose</span><span class="o">=</span><span class="bp">True</span><span class="p">,</span> <span class="n">print_every</span><span class="o">=</span><span class="mi">100</span><span class="p">)</span>
<span class="n">solver</span><span class="o">.</span><span class="n">train</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>(Iteration 1 / 9800) loss: 2.324754
(Epoch 0 / 10) train acc: 0.095000; val_acc: 0.123000
(Iteration 101 / 9800) loss: 1.896241
(Iteration 201 / 9800) loss: 1.805495
(Iteration 301 / 9800) loss: 2.008959
(Iteration 401 / 9800) loss: 1.973951
(Iteration 501 / 9800) loss: 1.878531
(Iteration 601 / 9800) loss: 2.170256
(Iteration 701 / 9800) loss: 1.937537
(Iteration 801 / 9800) loss: 2.089812
(Iteration 901 / 9800) loss: 1.766083
(Epoch 1 / 10) train acc: 0.505000; val_acc: 0.488000
(Iteration 1001 / 9800) loss: 1.767214
(Iteration 1101 / 9800) loss: 2.115131
(Iteration 1201 / 9800) loss: 2.088252
(Iteration 1301 / 9800) loss: 1.764972
(Iteration 1401 / 9800) loss: 1.684328
(Iteration 1501 / 9800) loss: 1.849211
(Iteration 1601 / 9800) loss: 1.987896
(Iteration 1701 / 9800) loss: 1.848357
(Iteration 1801 / 9800) loss: 1.791609
(Iteration 1901 / 9800) loss: 1.953224
(Epoch 2 / 10) train acc: 0.500000; val_acc: 0.521000
(Iteration 2001 / 9800) loss: 1.636806
(Iteration 2101 / 9800) loss: 1.675737
(Iteration 2201 / 9800) loss: 1.876629
(Iteration 2301 / 9800) loss: 1.797997
(Iteration 2401 / 9800) loss: 1.711645
(Iteration 2501 / 9800) loss: 1.825393
(Iteration 2601 / 9800) loss: 1.990960
(Iteration 2701 / 9800) loss: 1.666032
(Iteration 2801 / 9800) loss: 1.715085
(Iteration 2901 / 9800) loss: 1.442548
(Epoch 3 / 10) train acc: 0.554000; val_acc: 0.526000
(Iteration 3001 / 9800) loss: 1.674004
(Iteration 3101 / 9800) loss: 1.797069
(Iteration 3201 / 9800) loss: 1.785476
(Iteration 3301 / 9800) loss: 1.701619
(Iteration 3401 / 9800) loss: 1.394719
(Iteration 3501 / 9800) loss: 1.652609
(Iteration 3601 / 9800) loss: 1.669696
(Iteration 3701 / 9800) loss: 1.238229
(Iteration 3801 / 9800) loss: 1.357781
(Iteration 3901 / 9800) loss: 1.622159
(Epoch 4 / 10) train acc: 0.601000; val_acc: 0.552000
(Iteration 4001 / 9800) loss: 1.701807
(Iteration 4101 / 9800) loss: 1.292943
(Iteration 4201 / 9800) loss: 1.388350
(Iteration 4301 / 9800) loss: 1.441849
(Iteration 4401 / 9800) loss: 1.221635
(Iteration 4501 / 9800) loss: 1.574081
(Iteration 4601 / 9800) loss: 1.314446
(Iteration 4701 / 9800) loss: 1.440264
(Iteration 4801 / 9800) loss: 1.329411
(Epoch 5 / 10) train acc: 0.659000; val_acc: 0.607000
(Iteration 4901 / 9800) loss: 1.475479
(Iteration 5001 / 9800) loss: 1.391802
(Iteration 5101 / 9800) loss: 1.221501
(Iteration 5201 / 9800) loss: 1.256809
(Iteration 5301 / 9800) loss: 1.382730
(Iteration 5401 / 9800) loss: 1.371024
(Iteration 5501 / 9800) loss: 1.710086
(Iteration 5601 / 9800) loss: 1.131282
(Iteration 5701 / 9800) loss: 1.577423
(Iteration 5801 / 9800) loss: 1.497820
(Epoch 6 / 10) train acc: 0.710000; val_acc: 0.594000
(Iteration 5901 / 9800) loss: 1.534810
(Iteration 6001 / 9800) loss: 1.306800
(Iteration 6101 / 9800) loss: 1.248945
(Iteration 6201 / 9800) loss: 1.344940
(Iteration 6301 / 9800) loss: 1.697938
(Iteration 6401 / 9800) loss: 1.240161
(Iteration 6501 / 9800) loss: 1.334998
(Iteration 6601 / 9800) loss: 1.067959
(Iteration 6701 / 9800) loss: 1.041611
(Iteration 6801 / 9800) loss: 1.486041
(Epoch 7 / 10) train acc: 0.722000; val_acc: 0.620000
(Iteration 6901 / 9800) loss: 1.136422
(Iteration 7001 / 9800) loss: 1.130785
(Iteration 7101 / 9800) loss: 1.198386
(Iteration 7201 / 9800) loss: 1.403366
(Iteration 7301 / 9800) loss: 1.137794
(Iteration 7401 / 9800) loss: 1.069853
(Iteration 7501 / 9800) loss: 1.220662
(Iteration 7601 / 9800) loss: 1.098863
(Iteration 7701 / 9800) loss: 1.360739
(Iteration 7801 / 9800) loss: 1.190277
(Epoch 8 / 10) train acc: 0.764000; val_acc: 0.630000
(Iteration 7901 / 9800) loss: 1.096901
(Iteration 8001 / 9800) loss: 1.450723
(Iteration 8101 / 9800) loss: 1.169444
(Iteration 8201 / 9800) loss: 1.306434
(Iteration 8301 / 9800) loss: 1.085921
(Iteration 8401 / 9800) loss: 1.113912
(Iteration 8501 / 9800) loss: 1.243758
(Iteration 8601 / 9800) loss: 1.303660
(Iteration 8701 / 9800) loss: 0.966121
(Iteration 8801 / 9800) loss: 1.269276
(Epoch 9 / 10) train acc: 0.763000; val_acc: 0.605000
(Iteration 8901 / 9800) loss: 0.956320
(Iteration 9001 / 9800) loss: 1.402196
(Iteration 9101 / 9800) loss: 0.896963
(Iteration 9201 / 9800) loss: 0.923713
(Iteration 9301 / 9800) loss: 0.928696
(Iteration 9401 / 9800) loss: 1.179554
(Iteration 9501 / 9800) loss: 1.292880
(Iteration 9601 / 9800) loss: 1.021084
(Iteration 9701 / 9800) loss: 1.149757
(Epoch 10 / 10) train acc: 0.791000; val_acc: 0.604000
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[27]:</div>
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
<pre>Validation set accuracy:  0.509
Test set accuracy:  0.52
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[28]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span></span><span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">stats</span><span class="p">[</span><span class="mi">2</span><span class="p">]</span><span class="o">.</span><span class="n">train_acc_history</span><span class="p">,</span> <span class="s1">&#39;-o&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">solver</span><span class="o">.</span><span class="n">train_acc_history</span><span class="p">,</span> <span class="s1">&#39;-o&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">stats</span><span class="p">[</span><span class="mi">2</span><span class="p">]</span><span class="o">.</span><span class="n">val_acc_history</span><span class="p">,</span> <span class="s1">&#39;-o&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">solver</span><span class="o">.</span><span class="n">val_acc_history</span><span class="p">,</span> <span class="s1">&#39;-o&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;iteration&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;loss&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">legend</span><span class="p">([</span><span class="s1">&#39;No BN train ACC&#39;</span><span class="p">,</span> <span class="s1">&#39;BatchNorm train ACC&#39;</span><span class="p">,</span> <span class="s1">&#39;No BN val ACC&#39;</span><span class="p">,</span> <span class="s1">&#39;BatchNorm val ACC&#39;</span><span class="p">],</span> <span class="n">loc</span><span class="o">=</span><span class="s1">&#39;lower right&#39;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[28]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>&lt;matplotlib.legend.Legend at 0x7fe52cd37690&gt;</pre>
</div>

</div>

<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
NRUVFZSVlTFjxoyDPr/77rv53ve+1/b+4Ycf5o477uC6667jwQcfJCUlpe2zb3zjGzz77LM0Nzd3
yc/TW/W5Gaq9+/ezpKbmz/1TQ4fy3xtziQ/ayFz7pyRJUgfV1tZy4423MWbMPEaOvIoxY+Zx4423
UVtb262vDYmZnltuuYX9+/e3O0t1qJaWFu68807OOussMjIyGDNmDLfeeitNTU0drmHIkMQqodTU
w/97/2c/+1nOPvvsdmepjuX222/n5ptvBhK9Th8uM3znnXeAxHK9G2+8kd/+9rdMmDCBjIwMnnnm
GQB+8IMfMGvWLAYNGkRmZiYXX3wx//M//3PYPQ7tofpwGeWSJUv4+te/zuDBg8nOzubqq69m9+7d
x137gw8+yLnnnsvs2bOZN28eDz744GHHPPzww6xfv55bb731sDAFkJ2dzZ133tn2/jvf+Q4DBw7k
l7/85UFh6kPz58/n4x//+HHXqD4YqFbV1tIchlzW2j8Vn1nEsg9igP1TkiSpY2pra5kx4xp+8pMZ
vPXWs2zb9hhvvfUsP/nJDGbMuOakgk9XXvtAY8aM4Ytf/CK/+MUv+OCDD4567F/91V9x2223cfHF
F/N//+//Ze7cufzTP/3TMft8DrR79252795NRUUFa9as4W/+5m/o378/11133WHHpqSkcOutt7bN
Up2Ia665pq2uH/3oRzzwwAP85je/obCwsO2Y559/nm984xt89rOf5Uc/+hGjR48G4Mc//jGTJk3i
zjvv5P/8n/9DWloa1113HX/84x8PuseRZgxvuOEGNmzYwHe/+12+8pWv8Pjjj/O1r33tuOpuamri
kUce4XOf+xwACxYs4IUXXmDnzp0HHbdo0SKCIODzn//8Ma/5xhtv8Prrr/OpT32KrKys46pDx9bn
lvwtq61lzNChnBkEsGIF73z1+zTWlzG8/xhG5o1MdnmSJKkH+va3f8CmTV8nHv/oAaMB8fhH2bQp
5NZb7+FHP/put7v24ff6Nvfffz/f+973uPfee9s9Zv369dx///186Utf4mc/+xkAX/7ylyksLOSe
e+6hrKyMOXOO3kYRhiHnnHPOQWP5+fn84Q9/YPz48e2e87nPfY4777yTO+6444SW/U2YMIFJkybx
0EMPceWVV3L66acfdszmzZt55ZVXDqvpT3/600FL/772ta9x0UUX8cMf/pCPfexjx7x3YWEhTz/9
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
ZdZGVnHdKN7Y2Fhq1KhBo0aNMj1eunRpHnjgAT766COmT5+Ow+GgTp067Nmzh6ioKFauXMmqVatI
SUmhbt26DBkyhOHDh7u0MXHiRDp27MjMmTOZPXs2p06domzZsrRs2ZLVq1e7PcpYVJlbMQ+0IDDG
BABxvPce3HUXju3bSVmwgTL9/8WpV45ryp+IiIhkKj4+nsDAQOLi4ggICMjvcETkBrLzN5teBwi0
1t54HfzrKHL3UKVLadkS7BHa19b9UyIiIiIi4p4im1BhDPh60q5Wm/yOREREREREblNFN6GyFs7/
TlCtoPyOREREREREblNFN6HasQPPahe4t+K9N64rIiIiIiKSiaKXUFmLY/sOmDubjr1b4OHI/AnW
IiIiIiIiN1LkEqoqY8fSYOF/MQ+foNPdHfI7HBERERERuY0VuYRqjYcH/yUcW/ICbWu2ze9wRERE
RETkNlbkHuybVKcJSY4tlHD4EFBFz5IQERERERH3FbmE6kDJ+zCVv+SBGq3xdBS5yxcRERERkTxU
5Kb8bU5shKPWP2hfu11+hyIiIiIiIre5IpdQbd09At+/JdG0fNP8DkVERERERG5zRS6hWnn5VxZ+
BX/uNYqkpKT8DkdERERErjF//nwcDgfx8fH5HUqhsWXLFhwOB19++WV+h1LoFLmEygBdLTz3738z
bezY/A5HREREJF+lJy9Xb5UqVaJDhw589tlnbrf7+uuvs2rVKrfPN8Zkq15QUBAOh4Pu3btnOHbk
yBEcDgfTp093O45b6d1332X+/Pk3rf3svqY5lZKSQpUqVXA4HKxfv/66dffs2UN4eDg1atSgRIkS
lC9fns6dOxMdHU1KSopL3eTkZKKiomjZsiVlypTB29ub+vXrM3z4cA4ePHhTrsUdRXZVhi4pKUxf
vRpmzMjvUERERETylTGGiRMnUqtWLay1HD9+nOjoaEJCQli7di0hISE5bnPKlCn06tUr00QnLxlj
MMawdu1adu/ezX333XdT+7uZZs2axR133MHAgQPzvO127dpx/vx5ihUrludtb9q0iePHj+Pv709M
TAzBwcGZ1vvggw945plnqFy5Mv3796devXokJSWxadMmnnjiCX7++WdefvllAE6ePElwcDC7d++m
a9euPProo/j6+nLgwAEWL17MnDlzuHDhQp5fizsKTEJljHkWeAGoDOwFhltrv8qi7t3ABCAQqAmM
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
to1Zs2Y5H6588eJFatasSY8ePYiIiMiy71vN3IzsuiAyxgQAcQwBqqYOkw+rOowZb87I79BERESk
AEu/eT0uLs5lFTwRKZiy8zd71aIUgdbaXM0/LTAjVLeSc87xrJsz51hERERERIqGgrIoxS1T5csq
DKs6jO1/237bPCxMREREREQKpiI3QrU2Zq2G60VEREREJE8UuREqERERERGRvKKESkRERERExE1K
qERERERERNykhEpERERERMRNSqhERERERETcpIRKRERERETETUqoRERERERE3KSESkRERERExE1K
qERERERERNykhEpEREREJAeio6NxOBz88MMP+R2KFABKqERERESKsPnz5+NwOChZsiQ//fRThuNB
QUE0btw4z/qLjIzE4XA4Nw8PD6pWrUpoaCg7d+50qXvkyBFnvZUrV2Zoa/z48TgcDk6dOpVn8WWH
MQZjTI7OefHFF3E4HPTr1++69ZKSkoiMjKRJkyb4+flRsmRJGjVqxCuvvJLp72fz5s2EhYVRpUoV
ihcvTqVKlejWrVumr5fcHJ75HYCIiIhIYWOtzfEH7vxuOzk5mTfeeIMZM2a4lN+MvowxzJ49Gx8f
H1JSUvjvf//L+++/T7t27di1a1eGBM4Yw4QJE/jTn/6Uofxmvc55bfHixfj7+7NmzRrOnj2Lj49P
hjrff/89nTp14scff6RXr1489dRTeHl5sW/fPubOncvKlSv597//7aw/fvx4JkyYwF133cXTTz9N
zZo1OXnyJOvWraNnz57ExMTQt2/fW3mZRZISKhEREZE8kJSUxFtjxrB1zRp8Ll3irJcXrUNDeWHy
ZPz8/Aps2+maNGnCnDlzeOWVV6hcuXKetHk9Dz/8MOXKlXPud+/enXvvvZelS5dmSKiaNGnCnj17
+Pjjj+nRo8dNjy2vffHFFxw9epQvvviCzp07s2LFCvr37+9S58qVK4SFhfHLL7+wZcsWWrVq5XJ8
8uTJvPnmm879ZcuWMWHCBHr37k1MTAweHh7OY88//zwbNmzg0qVLN/fCBNCUPxEREZFcS0pK4uFW
rWj1zjtsSEhg1dGjbEhIoNU77/Bwq1YkJSUVyLbTGWMYPXo0ly9f5o033rhh/StXrjBx4kTq1q1L
iRIl8Pf3Z+zYsVy8eNHtGCpVqgSAp2fG7/v79u1LvXr1mDBhQo7bXbZsGQ6Hg3/84x8Zjs2ePRuH
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
gu4PQCNjTPhVZSbtv/7AgbSf46490RjTBxgO1AF8Sf13LzGH/TcA9qYlU+m2kjrLoz6QnlB9Y11X
evqJ1BE1EREpxJRQiYhIQedL6j1RM/hfIpXuh6t+Pnv1AWNMS2AhqVMI/0ZqItUPeC6H/RsyWbgi
zdXl1y6CYdHUehGRQk8JlYiIFCQXgWsXcogH7rHWHs5hW/cDCdbaN9ILjDG1stHftb4FBhhjvK21
59PKHgCuAP/JYUwiIlLI6JszEREpSBKAtsaYqsaY8mllbwKtjDH/zxjzB2NMXWNMd2PMtYtCXOsg
UMMY08cYU9sYEwH0yKQ//7R2yxtjimXSTgxwAZhvjLnHGNMemAksuMG9VyIiUgQooRIRkfx29bS5
14BawCHgBIC1dh/QDqgHfEnqiNV44GgWbZB23hogitTV+HYDLYEJ11RbTuoKfl+k9df32vbSRqWC
gXLALmAJsIHUe7NERKSIM673z4qIiIiIiEh2aYRKRERERETETUqoRERERERE3KSESkRERERExE1K
qERERERERNykhEpERERERMRNSqhERERERETcpIRKRERERETETUqoRERERERE3KSESkRERERExE1K
qERERERERNykhEpERERERMRN/x9pKyCFyJfehgAAAABJRU5ErkJggg==
"
>
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
