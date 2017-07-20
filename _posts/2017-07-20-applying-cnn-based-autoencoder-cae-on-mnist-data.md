---
layout: post
title: "Applying CNN Based AutoEncoder (CAE) on MNIST Data"
description: ""
category: 
tags: 
 - Deep Learning
 - PCA
 - Neural Network
---
{% include JB/setup %}
<html>
<head><meta charset="utf-8" />
<title>AutoEncoder</title>

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
<h1 id="Autoencoder">Autoencoder<a class="anchor-link" href="#Autoencoder">&#182;</a></h1><p><a href="https://en.wikipedia.org/wiki/Principal_component_analysis">Principal Component Analysis (PCA)</a> are often used to extract orthognal, independent variables for a given coveraiance matrix. It is effectively Singlar Value Deposition (SVD) in linear algebra and it is so powerful and elegant that usually deemed as the <a href="http://www.maths.adelaide.edu.au/anthony.roberts/larxxia.php">crown drews of linear algebra</a>. However, the obvious limition of SVD is the linear transformation assumption. With nonlinear transforms for generalization purpose, Hinton and  Salakhutdinov extended the method in <a href="http://science.sciencemag.org/content/313/5786/504">data dimensionaility reduction using neural networks</a>. It shown better results than pure PCA method.</p>
<p>In this project, I will use <a href="http://yann.lecun.com/exdb/mnist/">MNIST hand-writing digits dataset</a> and Tensorflow to train an autoencoder (encoder and decoder). Because the flow tries to first compress input data into a smaller dimension, then to regenerate an output that closely matches input. It does not need supervised data (label, bounding box etc.). Autoencoder belongs to the category of unsupervised learning.
The final output dimensionality is the same as the input, but the internal dimension can be much smaller. This dimensionality reduction can be deemed as a generalized PCA, it can be very useful to provide insight to data and for efficient storing/comparing/retrieving data. In a sense, I feel that word embedding (covered by one of my other blogs) is a special kind of autoencoder.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[1]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Step 1: Prepare environments</span>
<span class="kn">import</span> <span class="nn">sys</span>
<span class="kn">import</span> <span class="nn">time</span>
<span class="kn">import</span> <span class="nn">numpy</span> <span class="kn">as</span> <span class="nn">np</span>
<span class="kn">import</span> <span class="nn">tensorflow</span> <span class="kn">as</span> <span class="nn">tf</span>
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="kn">as</span> <span class="nn">plt</span>
<span class="kn">import</span> <span class="nn">math</span>
<span class="kn">import</span> <span class="nn">os</span>
<span class="n">os</span><span class="o">.</span><span class="n">environ</span><span class="p">[</span><span class="s2">&quot;CUDA_DEVICE_ORDER&quot;</span><span class="p">]</span><span class="o">=</span><span class="s2">&quot;PCI_BUS_ID&quot;</span>
<span class="n">os</span><span class="o">.</span><span class="n">environ</span><span class="p">[</span><span class="s2">&quot;CUDA_VISIBLE-DEVICES&quot;</span><span class="p">]</span><span class="o">=</span><span class="s2">&quot;&quot;</span>    <span class="c1"># Change to &#39;0&#39; to use tf.device(&quot;/gpu:0&quot;)</span>

<span class="kn">from</span> <span class="nn">tensorflow.examples.tutorials.mnist</span> <span class="kn">import</span> <span class="n">input_data</span>
<span class="o">%</span><span class="k">matplotlib</span> inline

<span class="o">%</span><span class="k">load_ext</span> autoreload
<span class="o">%</span><span class="k">autoreload</span> 2

<span class="n">MNIST</span> <span class="o">=</span> <span class="n">input_data</span><span class="o">.</span><span class="n">read_data_sets</span><span class="p">(</span><span class="s2">&quot;MNIST_data&quot;</span><span class="p">,</span> <span class="n">one_hot</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>Extracting MNIST_data/train-images-idx3-ubyte.gz
Extracting MNIST_data/train-labels-idx1-ubyte.gz
Extracting MNIST_data/t10k-images-idx3-ubyte.gz
Extracting MNIST_data/t10k-labels-idx1-ubyte.gz
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[2]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Define functions for weights and bias initialization</span>
<span class="k">def</span> <span class="nf">weight_variable</span><span class="p">(</span><span class="n">shape</span><span class="p">):</span>
  <span class="n">initial</span> <span class="o">=</span> <span class="n">tf</span><span class="o">.</span><span class="n">truncated_normal</span><span class="p">(</span><span class="n">shape</span><span class="p">,</span> <span class="n">stddev</span><span class="o">=</span><span class="mi">1</span><span class="o">/</span><span class="n">math</span><span class="o">.</span><span class="n">sqrt</span><span class="p">(</span><span class="n">shape</span><span class="p">[</span><span class="mi">2</span><span class="p">]))</span>
  <span class="k">return</span> <span class="n">tf</span><span class="o">.</span><span class="n">Variable</span><span class="p">(</span><span class="n">initial</span><span class="p">)</span>

<span class="k">def</span> <span class="nf">bias_variable</span><span class="p">(</span><span class="n">shape</span><span class="p">):</span>
  <span class="n">initial</span> <span class="o">=</span> <span class="n">tf</span><span class="o">.</span><span class="n">zeros</span><span class="p">(</span><span class="n">shape</span><span class="p">)</span>
  <span class="k">return</span> <span class="n">tf</span><span class="o">.</span><span class="n">Variable</span><span class="p">(</span><span class="n">initial</span><span class="p">)</span>

<span class="c1"># Define CNN and max_pool operations</span>
<span class="k">def</span> <span class="nf">conv2d</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">W</span><span class="p">):</span>
  <span class="k">return</span> <span class="n">tf</span><span class="o">.</span><span class="n">nn</span><span class="o">.</span><span class="n">conv2d</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">W</span><span class="p">,</span> <span class="n">strides</span><span class="o">=</span><span class="p">[</span><span class="mi">1</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">1</span><span class="p">],</span> <span class="n">padding</span><span class="o">=</span><span class="s1">&#39;SAME&#39;</span><span class="p">)</span>

<span class="k">def</span> <span class="nf">max_pool_2x2</span><span class="p">(</span><span class="n">x</span><span class="p">):</span>
  <span class="k">return</span> <span class="n">tf</span><span class="o">.</span><span class="n">nn</span><span class="o">.</span><span class="n">max_pool</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">ksize</span><span class="o">=</span><span class="p">[</span><span class="mi">1</span><span class="p">,</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">1</span><span class="p">],</span>
                        <span class="n">strides</span><span class="o">=</span><span class="p">[</span><span class="mi">1</span><span class="p">,</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">1</span><span class="p">],</span> <span class="n">padding</span><span class="o">=</span><span class="s1">&#39;SAME&#39;</span><span class="p">)</span>
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
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># In this CNN Based AutoEncoder, I will compress 784-dimension images to 128 (4 x 4 x 8) dimensions</span>
<span class="c1"># The latent code can be used for many purpose</span>
<span class="k">class</span> <span class="nc">AutoEncoder</span><span class="p">(</span><span class="nb">object</span><span class="p">):</span>
    
    <span class="sd">&quot;&quot;&quot;</span>
<span class="sd">    AutoEncoder class for MNIST</span>
<span class="sd">    &quot;&quot;&quot;</span>
    
    <span class="k">def</span> <span class="nf">__init__</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">MNIST</span><span class="p">):</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">MNIST</span> <span class="o">=</span> <span class="n">MNIST</span>
        <span class="c1"># Input, output placeholders</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">x_input</span> <span class="o">=</span> <span class="n">tf</span><span class="o">.</span><span class="n">placeholder</span><span class="p">(</span><span class="n">tf</span><span class="o">.</span><span class="n">float32</span><span class="p">,</span> <span class="n">shape</span><span class="o">=</span><span class="p">[</span><span class="bp">None</span><span class="p">,</span> <span class="mi">784</span><span class="p">])</span>
        <span class="c1">#y_ = tf.placeholder(tf.float32, shape=[None, 10])</span>
        <span class="c1">#self.mean_img = np.mean(self.MNIST.train.images, axis=0)</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">mean_img</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">zeros</span><span class="p">((</span><span class="mi">784</span><span class="p">))</span>
        <span class="c1"># Shapes: bookkeeping dimensions</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">shapes</span> <span class="o">=</span> <span class="p">[]</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">global_step</span> <span class="o">=</span> <span class="n">tf</span><span class="o">.</span><span class="n">Variable</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span> <span class="n">dtype</span><span class="o">=</span><span class="n">tf</span><span class="o">.</span><span class="n">int32</span><span class="p">,</span> <span class="n">trainable</span><span class="o">=</span><span class="bp">False</span><span class="p">,</span> <span class="n">name</span><span class="o">=</span><span class="s1">&#39;global_step&#39;</span><span class="p">)</span>

    <span class="k">def</span> <span class="nf">__build_graph</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>
        <span class="c1"># First cnn layer</span>
        <span class="n">W_conv1</span> <span class="o">=</span> <span class="n">weight_variable</span><span class="p">([</span><span class="mi">3</span><span class="p">,</span> <span class="mi">3</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">32</span><span class="p">])</span>
        <span class="n">b_conv1</span> <span class="o">=</span> <span class="n">bias_variable</span><span class="p">([</span><span class="mi">32</span><span class="p">])</span>

        <span class="bp">self</span><span class="o">.</span><span class="n">x_image</span> <span class="o">=</span> <span class="n">tf</span><span class="o">.</span><span class="n">reshape</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">x_input</span><span class="p">,</span> <span class="p">[</span><span class="o">-</span><span class="mi">1</span><span class="p">,</span><span class="mi">28</span><span class="p">,</span><span class="mi">28</span><span class="p">,</span><span class="mi">1</span><span class="p">])</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">shapes</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">x_image</span><span class="o">.</span><span class="n">get_shape</span><span class="p">()</span><span class="o">.</span><span class="n">as_list</span><span class="p">())</span>
        <span class="c1"># shape[0]</span>
        <span class="k">print</span><span class="p">(</span><span class="s2">&quot;x_image shape: </span><span class="si">%s</span><span class="s2">&quot;</span> <span class="o">%</span> <span class="bp">self</span><span class="o">.</span><span class="n">shapes</span><span class="p">[</span><span class="o">-</span><span class="mi">1</span><span class="p">])</span>

        <span class="n">h_conv1</span> <span class="o">=</span> <span class="n">tf</span><span class="o">.</span><span class="n">nn</span><span class="o">.</span><span class="n">relu</span><span class="p">(</span><span class="n">tf</span><span class="o">.</span><span class="n">nn</span><span class="o">.</span><span class="n">conv2d</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">x_image</span><span class="p">,</span> <span class="n">W_conv1</span><span class="p">,</span> <span class="n">strides</span><span class="o">=</span><span class="p">[</span><span class="mi">1</span><span class="p">,</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">1</span><span class="p">],</span> <span class="n">padding</span><span class="o">=</span><span class="s1">&#39;SAME&#39;</span><span class="p">)</span> <span class="o">+</span> <span class="n">b_conv1</span><span class="p">)</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">shapes</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">h_conv1</span><span class="o">.</span><span class="n">get_shape</span><span class="p">()</span><span class="o">.</span><span class="n">as_list</span><span class="p">())</span>
        <span class="c1">#h_pool1 = max_pool_2x2(h_conv1)</span>
        <span class="c1"># shape[1]</span>
        <span class="k">print</span><span class="p">(</span><span class="s2">&quot;h_conv1 dimension: </span><span class="si">%s</span><span class="s2">&quot;</span> <span class="o">%</span> <span class="bp">self</span><span class="o">.</span><span class="n">shapes</span><span class="p">[</span><span class="o">-</span><span class="mi">1</span><span class="p">])</span>

        <span class="c1"># 2nd CNN layer</span>
        <span class="c1"># 64 features with 5x5 filter</span>
        <span class="n">W_conv2</span> <span class="o">=</span> <span class="n">weight_variable</span><span class="p">([</span><span class="mi">3</span><span class="p">,</span> <span class="mi">3</span><span class="p">,</span> <span class="mi">32</span><span class="p">,</span> <span class="mi">16</span><span class="p">])</span>
        <span class="n">b_conv2</span> <span class="o">=</span> <span class="n">bias_variable</span><span class="p">([</span><span class="mi">16</span><span class="p">])</span>

        <span class="n">h_conv2</span> <span class="o">=</span> <span class="n">tf</span><span class="o">.</span><span class="n">nn</span><span class="o">.</span><span class="n">relu</span><span class="p">(</span><span class="n">tf</span><span class="o">.</span><span class="n">nn</span><span class="o">.</span><span class="n">conv2d</span><span class="p">(</span><span class="n">h_conv1</span><span class="p">,</span> <span class="n">W_conv2</span><span class="p">,</span> <span class="n">strides</span><span class="o">=</span><span class="p">[</span><span class="mi">1</span><span class="p">,</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">1</span><span class="p">],</span> <span class="n">padding</span><span class="o">=</span><span class="s1">&#39;SAME&#39;</span><span class="p">)</span> <span class="o">+</span> <span class="n">b_conv2</span><span class="p">)</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">shapes</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">h_conv2</span><span class="o">.</span><span class="n">get_shape</span><span class="p">()</span><span class="o">.</span><span class="n">as_list</span><span class="p">())</span>
        <span class="c1"># shape[2]</span>
        <span class="k">print</span><span class="p">(</span><span class="s2">&quot;h_conv2 dimension: </span><span class="si">%s</span><span class="s2">&quot;</span> <span class="o">%</span> <span class="bp">self</span><span class="o">.</span><span class="n">shapes</span><span class="p">[</span><span class="o">-</span><span class="mi">1</span><span class="p">])</span>
        <span class="c1">#h_pool2 = max_pool_2x2(h_conv2)</span>

        <span class="c1"># 3rd CNN layer</span>
        <span class="c1"># 32 features with 5x5 filter</span>
        <span class="n">W_conv3</span> <span class="o">=</span> <span class="n">weight_variable</span><span class="p">([</span><span class="mi">3</span><span class="p">,</span> <span class="mi">3</span><span class="p">,</span> <span class="mi">16</span><span class="p">,</span> <span class="mi">8</span><span class="p">])</span>
        <span class="n">b_conv3</span> <span class="o">=</span> <span class="n">bias_variable</span><span class="p">([</span><span class="mi">8</span><span class="p">])</span>

        <span class="bp">self</span><span class="o">.</span><span class="n">laten_code</span> <span class="o">=</span> <span class="n">tf</span><span class="o">.</span><span class="n">nn</span><span class="o">.</span><span class="n">relu</span><span class="p">(</span><span class="n">tf</span><span class="o">.</span><span class="n">nn</span><span class="o">.</span><span class="n">conv2d</span><span class="p">(</span><span class="n">h_conv2</span><span class="p">,</span> <span class="n">W_conv3</span><span class="p">,</span> <span class="n">strides</span><span class="o">=</span><span class="p">[</span><span class="mi">1</span><span class="p">,</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">1</span><span class="p">],</span> <span class="n">padding</span><span class="o">=</span><span class="s1">&#39;SAME&#39;</span><span class="p">)</span> <span class="o">+</span> <span class="n">b_conv3</span><span class="p">)</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">shapes</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">laten_code</span><span class="o">.</span><span class="n">get_shape</span><span class="p">()</span><span class="o">.</span><span class="n">as_list</span><span class="p">())</span>
        <span class="c1"># shape[3]</span>
        <span class="k">print</span><span class="p">(</span><span class="s2">&quot;h_conv3 dimension: </span><span class="si">%s</span><span class="s2">&quot;</span> <span class="o">%</span> <span class="bp">self</span><span class="o">.</span><span class="n">shapes</span><span class="p">[</span><span class="o">-</span><span class="mi">1</span><span class="p">])</span>

        <span class="c1">#h_pool3 = max_pool_2x2(laten_code)</span>


        <span class="c1"># 3rd Deconv layer</span>
        <span class="n">W_dconv3</span> <span class="o">=</span> <span class="n">W_conv3</span>
        <span class="n">b_dconv3</span> <span class="o">=</span> <span class="n">bias_variable</span><span class="p">([</span><span class="mi">16</span><span class="p">])</span>
        <span class="n">h_dconv3</span> <span class="o">=</span> <span class="n">tf</span><span class="o">.</span><span class="n">nn</span><span class="o">.</span><span class="n">relu</span><span class="p">(</span><span class="n">tf</span><span class="o">.</span><span class="n">nn</span><span class="o">.</span><span class="n">conv2d_transpose</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">laten_code</span><span class="p">,</span> <span class="n">W_dconv3</span><span class="p">,</span> 
                                                <span class="n">tf</span><span class="o">.</span><span class="n">stack</span><span class="p">([</span><span class="n">tf</span><span class="o">.</span><span class="n">shape</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">x_input</span><span class="p">)[</span><span class="mi">0</span><span class="p">],</span> <span class="bp">self</span><span class="o">.</span><span class="n">shapes</span><span class="p">[</span><span class="mi">2</span><span class="p">][</span><span class="mi">1</span><span class="p">],</span> 
                                                          <span class="bp">self</span><span class="o">.</span><span class="n">shapes</span><span class="p">[</span><span class="mi">2</span><span class="p">][</span><span class="mi">2</span><span class="p">],</span> <span class="bp">self</span><span class="o">.</span><span class="n">shapes</span><span class="p">[</span><span class="mi">2</span><span class="p">][</span><span class="mi">3</span><span class="p">]]),</span>
                                                <span class="n">strides</span><span class="o">=</span><span class="p">[</span><span class="mi">1</span><span class="p">,</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">1</span><span class="p">],</span> <span class="n">padding</span><span class="o">=</span><span class="s1">&#39;SAME&#39;</span> <span class="p">)</span> <span class="o">+</span> <span class="n">b_dconv3</span><span class="p">)</span>
        <span class="k">print</span><span class="p">(</span><span class="s2">&quot;h_dconv3 dimension: </span><span class="si">%s</span><span class="s2">&quot;</span> <span class="o">%</span> <span class="n">h_dconv3</span><span class="o">.</span><span class="n">get_shape</span><span class="p">()</span><span class="o">.</span><span class="n">as_list</span><span class="p">())</span>

        <span class="c1"># 2nd Deconv layer</span>
        <span class="n">W_dconv2</span> <span class="o">=</span> <span class="n">W_conv2</span>
        <span class="n">b_dconv2</span> <span class="o">=</span> <span class="n">bias_variable</span><span class="p">([</span><span class="mi">32</span><span class="p">])</span>
        <span class="n">h_dconv2</span> <span class="o">=</span> <span class="n">tf</span><span class="o">.</span><span class="n">nn</span><span class="o">.</span><span class="n">relu</span><span class="p">(</span><span class="n">tf</span><span class="o">.</span><span class="n">nn</span><span class="o">.</span><span class="n">conv2d_transpose</span><span class="p">(</span><span class="n">h_dconv3</span><span class="p">,</span> <span class="n">W_dconv2</span><span class="p">,</span>
                                                <span class="n">tf</span><span class="o">.</span><span class="n">stack</span><span class="p">([</span><span class="n">tf</span><span class="o">.</span><span class="n">shape</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">x_input</span><span class="p">)[</span><span class="mi">0</span><span class="p">],</span> <span class="bp">self</span><span class="o">.</span><span class="n">shapes</span><span class="p">[</span><span class="mi">1</span><span class="p">][</span><span class="mi">1</span><span class="p">],</span> 
                                                          <span class="bp">self</span><span class="o">.</span><span class="n">shapes</span><span class="p">[</span><span class="mi">1</span><span class="p">][</span><span class="mi">2</span><span class="p">],</span> <span class="bp">self</span><span class="o">.</span><span class="n">shapes</span><span class="p">[</span><span class="mi">1</span><span class="p">][</span><span class="mi">3</span><span class="p">]]),</span>
                                                <span class="n">strides</span><span class="o">=</span><span class="p">[</span><span class="mi">1</span><span class="p">,</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">1</span><span class="p">],</span> <span class="n">padding</span><span class="o">=</span><span class="s1">&#39;SAME&#39;</span> <span class="p">)</span> <span class="o">+</span> <span class="n">b_dconv2</span><span class="p">)</span>

        <span class="k">print</span><span class="p">(</span><span class="s2">&quot;h_dconv2 dimension: </span><span class="si">%s</span><span class="s2">&quot;</span> <span class="o">%</span> <span class="n">h_dconv2</span><span class="o">.</span><span class="n">get_shape</span><span class="p">())</span>

        <span class="c1"># 1st Deconv layer to reconstruct the image</span>
        <span class="n">W_dconv1</span> <span class="o">=</span> <span class="n">W_conv1</span>
        <span class="n">b_dconv1</span> <span class="o">=</span> <span class="n">bias_variable</span><span class="p">([</span><span class="mi">1</span><span class="p">])</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">reconstructed_img</span> <span class="o">=</span> <span class="n">tf</span><span class="o">.</span><span class="n">nn</span><span class="o">.</span><span class="n">relu</span><span class="p">(</span><span class="n">tf</span><span class="o">.</span><span class="n">nn</span><span class="o">.</span><span class="n">conv2d_transpose</span><span class="p">(</span><span class="n">h_dconv2</span><span class="p">,</span> <span class="n">W_dconv1</span><span class="p">,</span>
                                                <span class="n">tf</span><span class="o">.</span><span class="n">stack</span><span class="p">([</span><span class="n">tf</span><span class="o">.</span><span class="n">shape</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">x_input</span><span class="p">)[</span><span class="mi">0</span><span class="p">],</span> <span class="bp">self</span><span class="o">.</span><span class="n">shapes</span><span class="p">[</span><span class="mi">0</span><span class="p">][</span><span class="mi">1</span><span class="p">],</span> 
                                                          <span class="bp">self</span><span class="o">.</span><span class="n">shapes</span><span class="p">[</span><span class="mi">0</span><span class="p">][</span><span class="mi">2</span><span class="p">],</span> <span class="bp">self</span><span class="o">.</span><span class="n">shapes</span><span class="p">[</span><span class="mi">0</span><span class="p">][</span><span class="mi">3</span><span class="p">]]),</span>
                                                <span class="n">strides</span><span class="o">=</span><span class="p">[</span><span class="mi">1</span><span class="p">,</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">1</span><span class="p">],</span> <span class="n">padding</span><span class="o">=</span><span class="s1">&#39;SAME&#39;</span> <span class="p">)</span> <span class="o">+</span> <span class="n">b_dconv1</span><span class="p">)</span>
        <span class="k">print</span><span class="p">(</span><span class="s2">&quot;reconstructed_img dimension: </span><span class="si">%s</span><span class="s2">&quot;</span> <span class="o">%</span> <span class="bp">self</span><span class="o">.</span><span class="n">reconstructed_img</span><span class="o">.</span><span class="n">get_shape</span><span class="p">())</span>


        <span class="c1"># Define the cost function</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">cost</span> <span class="o">=</span> <span class="n">tf</span><span class="o">.</span><span class="n">reduce_sum</span><span class="p">(</span><span class="n">tf</span><span class="o">.</span><span class="n">square</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">reconstructed_img</span> <span class="o">-</span> <span class="bp">self</span><span class="o">.</span><span class="n">x_image</span><span class="p">))</span>
    
        <span class="c1">#return {&#39;input&#39;: x_input, &#39;laten_code&#39;: laten_code, &#39;reconstructed_img&#39;: reconstructed_img, &#39;cost&#39;: cost}</span>
        
    <span class="k">def</span> <span class="nf">train</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">n_epochs</span><span class="o">=</span><span class="mi">10</span><span class="p">,</span> <span class="n">learning_rate</span><span class="o">=</span><span class="mf">0.01</span><span class="p">,</span> <span class="n">batch_size</span><span class="o">=</span><span class="mi">100</span><span class="p">):</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">__build_graph</span><span class="p">()</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">optimizer</span> <span class="o">=</span> <span class="n">tf</span><span class="o">.</span><span class="n">train</span><span class="o">.</span><span class="n">AdamOptimizer</span><span class="p">(</span><span class="n">learning_rate</span><span class="p">)</span><span class="o">.</span><span class="n">minimize</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">cost</span><span class="p">)</span>
        <span class="k">with</span> <span class="n">tf</span><span class="o">.</span><span class="n">Session</span><span class="p">(</span><span class="n">config</span><span class="o">=</span><span class="n">tf</span><span class="o">.</span><span class="n">ConfigProto</span><span class="p">(</span><span class="n">log_device_placement</span><span class="o">=</span><span class="bp">True</span><span class="p">))</span> <span class="k">as</span> <span class="n">sess</span><span class="p">:</span>
            <span class="n">saver</span> <span class="o">=</span> <span class="n">tf</span><span class="o">.</span><span class="n">train</span><span class="o">.</span><span class="n">Saver</span><span class="p">()</span>
            <span class="n">writer</span> <span class="o">=</span> <span class="n">tf</span><span class="o">.</span><span class="n">summary</span><span class="o">.</span><span class="n">FileWriter</span><span class="p">(</span><span class="s1">&#39;./graphs&#39;</span><span class="p">,</span> <span class="n">sess</span><span class="o">.</span><span class="n">graph</span><span class="p">)</span>
            
            <span class="c1"># Initialize variables</span>
            <span class="n">sess</span><span class="o">.</span><span class="n">run</span><span class="p">(</span><span class="n">tf</span><span class="o">.</span><span class="n">global_variables_initializer</span><span class="p">())</span>
            <span class="c1"># Training</span>
            <span class="k">for</span> <span class="n">epoch_i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">n_epochs</span><span class="p">):</span>
                <span class="k">for</span> <span class="n">batch_i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">MNIST</span><span class="o">.</span><span class="n">train</span><span class="o">.</span><span class="n">num_examples</span> <span class="o">//</span> <span class="n">batch_size</span><span class="p">):</span>
                    <span class="n">batch_xs</span><span class="p">,</span> <span class="n">_</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">MNIST</span><span class="o">.</span><span class="n">train</span><span class="o">.</span><span class="n">next_batch</span><span class="p">(</span><span class="n">batch_size</span><span class="p">)</span>
                    <span class="n">train_imgs</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">array</span><span class="p">([</span><span class="n">img</span> <span class="o">-</span> <span class="bp">self</span><span class="o">.</span><span class="n">mean_img</span> <span class="k">for</span> <span class="n">img</span> <span class="ow">in</span> <span class="n">batch_xs</span><span class="p">])</span>
                    <span class="n">sess</span><span class="o">.</span><span class="n">run</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">optimizer</span><span class="p">,</span> <span class="n">feed_dict</span><span class="o">=</span><span class="p">{</span><span class="bp">self</span><span class="o">.</span><span class="n">x_input</span><span class="p">:</span> <span class="n">train_imgs</span><span class="p">})</span>
                <span class="k">print</span><span class="p">(</span><span class="n">epoch_i</span><span class="p">,</span> <span class="n">sess</span><span class="o">.</span><span class="n">run</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">cost</span><span class="p">,</span> <span class="n">feed_dict</span><span class="o">=</span><span class="p">{</span><span class="bp">self</span><span class="o">.</span><span class="n">x_input</span><span class="p">:</span> <span class="n">train_imgs</span><span class="p">}))</span>
                <span class="n">saver</span><span class="o">.</span><span class="n">save</span><span class="p">(</span><span class="n">sess</span><span class="p">,</span> <span class="s1">&#39;checkpoints/checkpoint&#39;</span><span class="p">,</span> <span class="n">global_step</span><span class="o">=</span><span class="bp">self</span><span class="o">.</span><span class="n">global_step</span><span class="p">)</span>
            <span class="n">writer</span><span class="o">.</span><span class="n">close</span><span class="p">()</span>

                
    <span class="k">def</span> <span class="nf">test</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>
        <span class="c1"># Plot example reconstructions</span>
        <span class="n">n_examples</span> <span class="o">=</span> <span class="mi">10</span>
        <span class="n">imgs</span><span class="p">,</span> <span class="n">raw_labels</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">MNIST</span><span class="o">.</span><span class="n">test</span><span class="o">.</span><span class="n">next_batch</span><span class="p">(</span><span class="n">n_examples</span><span class="p">)</span>
        <span class="n">labels</span> <span class="o">=</span> <span class="p">[</span><span class="n">np</span><span class="o">.</span><span class="n">nonzero</span><span class="p">(</span><span class="n">label</span><span class="p">)[</span><span class="mi">0</span><span class="p">][</span><span class="mi">0</span><span class="p">]</span> <span class="k">for</span> <span class="n">label</span> <span class="ow">in</span> <span class="n">raw_labels</span><span class="p">]</span>
        <span class="n">test_imgs</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">array</span><span class="p">([</span><span class="n">img</span> <span class="o">-</span> <span class="bp">self</span><span class="o">.</span><span class="n">mean_img</span> <span class="k">for</span> <span class="n">img</span> <span class="ow">in</span> <span class="n">imgs</span><span class="p">])</span>
        <span class="k">with</span> <span class="n">tf</span><span class="o">.</span><span class="n">Session</span><span class="p">()</span> <span class="k">as</span> <span class="n">sess</span><span class="p">:</span>
            <span class="n">saver</span> <span class="o">=</span> <span class="n">tf</span><span class="o">.</span><span class="n">train</span><span class="o">.</span><span class="n">Saver</span><span class="p">()</span>
            <span class="n">sess</span><span class="o">.</span><span class="n">run</span><span class="p">(</span><span class="n">tf</span><span class="o">.</span><span class="n">global_variables_initializer</span><span class="p">())</span>
            <span class="c1"># Check whether we have check points from training</span>
            <span class="n">ckpt</span> <span class="o">=</span> <span class="n">tf</span><span class="o">.</span><span class="n">train</span><span class="o">.</span><span class="n">get_checkpoint_state</span><span class="p">(</span><span class="n">os</span><span class="o">.</span><span class="n">path</span><span class="o">.</span><span class="n">dirname</span><span class="p">(</span><span class="s1">&#39;checkpoints/checkpoint&#39;</span><span class="p">))</span>
            <span class="k">if</span> <span class="n">ckpt</span> <span class="ow">and</span> <span class="n">ckpt</span><span class="o">.</span><span class="n">model_checkpoint_path</span><span class="p">:</span>
                <span class="k">pass</span>
            <span class="k">else</span><span class="p">:</span>
                <span class="n">train</span><span class="p">()</span>
            <span class="n">initial_step</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">global_step</span><span class="o">.</span><span class="n">eval</span><span class="p">()</span>
            <span class="n">saver</span><span class="o">.</span><span class="n">restore</span><span class="p">(</span><span class="n">sess</span><span class="p">,</span> <span class="n">ckpt</span><span class="o">.</span><span class="n">model_checkpoint_path</span><span class="p">)</span>
            <span class="n">restored_imgs</span> <span class="o">=</span> <span class="n">sess</span><span class="o">.</span><span class="n">run</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">reconstructed_img</span><span class="p">,</span> <span class="n">feed_dict</span><span class="o">=</span><span class="p">{</span><span class="bp">self</span><span class="o">.</span><span class="n">x_input</span><span class="p">:</span> <span class="n">test_imgs</span><span class="p">})</span>
            
        <span class="n">fig</span><span class="p">,</span> <span class="n">axs</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="mi">2</span><span class="p">,</span> <span class="n">n_examples</span><span class="p">,</span> <span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">10</span><span class="p">,</span> <span class="mi">2</span><span class="p">))</span>
        <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">n_examples</span><span class="p">):</span>
            <span class="n">axs</span><span class="p">[</span><span class="mi">0</span><span class="p">][</span><span class="n">i</span><span class="p">]</span><span class="o">.</span><span class="n">set_title</span><span class="p">(</span><span class="n">labels</span><span class="p">[</span><span class="n">i</span><span class="p">])</span>
            <span class="n">axs</span><span class="p">[</span><span class="mi">0</span><span class="p">][</span><span class="n">i</span><span class="p">]</span><span class="o">.</span><span class="n">imshow</span><span class="p">(</span>
                <span class="n">np</span><span class="o">.</span><span class="n">reshape</span><span class="p">(</span><span class="n">imgs</span><span class="p">[</span><span class="n">i</span><span class="p">,</span> <span class="p">:],</span> <span class="p">(</span><span class="mi">28</span><span class="p">,</span> <span class="mi">28</span><span class="p">)),</span> <span class="n">cmap</span><span class="o">=</span><span class="n">plt</span><span class="o">.</span><span class="n">get_cmap</span><span class="p">(</span><span class="s1">&#39;gray&#39;</span><span class="p">))</span>
            <span class="n">axs</span><span class="p">[</span><span class="mi">0</span><span class="p">][</span><span class="n">i</span><span class="p">]</span><span class="o">.</span><span class="n">set_axis_off</span><span class="p">()</span>
            <span class="n">axs</span><span class="p">[</span><span class="mi">1</span><span class="p">][</span><span class="n">i</span><span class="p">]</span><span class="o">.</span><span class="n">imshow</span><span class="p">(</span>
                <span class="n">np</span><span class="o">.</span><span class="n">reshape</span><span class="p">(</span>
                    <span class="n">np</span><span class="o">.</span><span class="n">reshape</span><span class="p">(</span><span class="n">restored_imgs</span><span class="p">[</span><span class="n">i</span><span class="p">,</span> <span class="o">...</span><span class="p">],</span> <span class="p">(</span><span class="mi">784</span><span class="p">,))</span> <span class="o">+</span> <span class="bp">self</span><span class="o">.</span><span class="n">mean_img</span><span class="p">,</span>
                    <span class="p">(</span><span class="mi">28</span><span class="p">,</span> <span class="mi">28</span><span class="p">)),</span> <span class="n">cmap</span><span class="o">=</span><span class="n">plt</span><span class="o">.</span><span class="n">get_cmap</span><span class="p">(</span><span class="s1">&#39;gray&#39;</span><span class="p">))</span>
            <span class="n">axs</span><span class="p">[</span><span class="mi">1</span><span class="p">][</span><span class="n">i</span><span class="p">]</span><span class="o">.</span><span class="n">set_axis_off</span><span class="p">()</span>
        <span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
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
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Create CAE and train it with MNIST data</span>
<span class="n">cae</span> <span class="o">=</span> <span class="n">AutoEncoder</span><span class="p">(</span><span class="n">MNIST</span><span class="o">=</span><span class="n">MNIST</span><span class="p">)</span>
<span class="n">cae</span><span class="o">.</span><span class="n">train</span><span class="p">(</span><span class="n">n_epochs</span><span class="o">=</span><span class="mi">20</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>x_image shape: [None, 28, 28, 1]
h_conv1 dimension: [None, 14, 14, 32]
h_conv2 dimension: [None, 7, 7, 16]
h_conv3 dimension: [None, 4, 4, 8]
h_dconv3 dimension: [None, None, None, 16]
h_dconv2 dimension: (?, ?, ?, 32)
reconstructed_img dimension: (?, ?, ?, ?)
(0, 5696.1021)
(1, 4914.9907)
(2, 4715.1685)
(3, 4630.8564)
(4, 4587.5801)
(5, 4545.1592)
(6, 4513.7646)
(7, 4248.1909)
(8, 4197.1558)
(9, 3786.3115)
(10, 3818.7854)
(11, 3735.7927)
(12, 3750.4924)
(13, 3894.1965)
(14, 3990.6133)
(15, 973.03845)
(16, 932.56592)
(17, 832.84894)
(18, 726.32324)
(19, 710.25317)
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
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Plot randomly selected MNIST test images and reconstructed images</span>
<span class="n">cae</span><span class="o">.</span><span class="n">test</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>INFO:tensorflow:Restoring parameters from checkpoints/checkpoint-0
</pre>
</div>
</div>

<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
su8AAAAASUVORK5CYII=
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
