---
layout: post
title: "Word Embedding Implemented in Python"
description: ""
category: 
tags: []
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
.highlight .n { color: #040404} 
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
<span class="kn">import</span> <span class="nn">random</span>
<span class="kn">from</span> <span class="nn">random</span> <span class="kn">import</span> <span class="n">randrange</span>
<span class="kn">import</span> <span class="nn">zipfile</span>
<span class="kn">import</span> <span class="nn">collections</span>
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
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Because we are not using any flow, we need to define all building blocks in Python</span>

<span class="c1"># </span>
<span class="k">def</span> <span class="nf">normalize_vecs</span><span class="p">(</span><span class="n">x</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot; Row normalization function &quot;&quot;&quot;</span>
    <span class="c1"># Implement a function that normalizes each row of a matrix to have unit length</span>
    
    <span class="c1">### YOUR CODE HERE</span>
    <span class="n">xl_vec</span> <span class="o">=</span>  <span class="n">np</span><span class="o">.</span><span class="n">sqrt</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">(</span><span class="n">x</span><span class="o">**</span><span class="mi">2</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">,</span> <span class="n">keepdims</span><span class="o">=</span><span class="bp">True</span><span class="p">))</span>
    <span class="n">x</span> <span class="o">=</span> <span class="n">x</span><span class="o">/</span><span class="n">xl_vec</span>
    <span class="c1">### END YOUR CODE</span>
    
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
<span class="sd">    Calculate probability for given vector</span>
<span class="sd">    &quot;&quot;&quot;</span>
    <span class="n">x</span> <span class="o">-=</span> <span class="n">np</span><span class="o">.</span><span class="n">max</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="n">x</span><span class="o">.</span><span class="n">ndim</span><span class="o">-</span><span class="mi">1</span><span class="p">,</span> <span class="n">keepdims</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span>
    <span class="n">exp_x</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">exp</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>
    <span class="n">p</span> <span class="o">=</span> <span class="n">exp_x</span> <span class="o">/</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">(</span><span class="n">exp_x</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="n">x</span><span class="o">.</span><span class="n">ndim</span><span class="o">-</span><span class="mi">1</span><span class="p">,</span> <span class="n">keepdims</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span>
    
    <span class="k">return</span> <span class="n">p</span>

<span class="c1"># Softmax cost layer</span>
<span class="k">def</span> <span class="nf">softmax_cost</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">w</span><span class="p">,</span> <span class="n">target_idx</span><span class="p">,</span> <span class="n">dataset</span><span class="o">=</span><span class="bp">None</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;</span>
<span class="sd">    Calculate softmax cost and gradient</span>
<span class="sd">    No bias in this implmentation</span>
<span class="sd">    </span>
<span class="sd">    Inputs</span>
<span class="sd">        - x            # vector from previous layer, such as hidden layer</span>
<span class="sd">        - w            # weight for last layer, so called &quot;output vectors&quot;</span>
<span class="sd">        - target_idx   # Target word index, ground truth</span>
<span class="sd">        - dataset      # Dummy input, to be compatiable with negative_sampling_cost</span>
<span class="sd">    </span>
<span class="sd">    Outputs</span>
<span class="sd">        - cost         # Softmax + cross-entropy cost for current predication</span>
<span class="sd">        - dw           # Gradient with regarding to weights</span>
<span class="sd">        - dx           # Gradient with regarding to input vector</span>
<span class="sd">    &quot;&quot;&quot;</span>
    <span class="n">V</span><span class="p">,</span> <span class="n">D</span> <span class="o">=</span> <span class="n">w</span><span class="o">.</span><span class="n">shape</span>   <span class="c1"># V: vocabulary size, D: Vector dimension</span>
    <span class="n">x</span> <span class="o">=</span> <span class="n">x</span><span class="o">.</span><span class="n">reshape</span><span class="p">((</span><span class="mi">1</span><span class="p">,</span> <span class="n">D</span><span class="p">))</span>
    <span class="c1"># x.shape is (1, D)</span>
    <span class="n">prob</span> <span class="o">=</span> <span class="n">softmax</span><span class="p">(</span><span class="n">x</span><span class="o">.</span><span class="n">dot</span><span class="p">(</span><span class="n">w</span><span class="o">.</span><span class="n">T</span><span class="p">))</span>    <span class="c1"># (1, V)</span>
    <span class="n">cost</span> <span class="o">=</span> <span class="o">-</span><span class="n">np</span><span class="o">.</span><span class="n">log</span><span class="p">(</span><span class="n">prob</span><span class="p">[</span><span class="mi">0</span><span class="p">,</span> <span class="n">target_idx</span><span class="p">])</span>  <span class="c1"># Cross-entropy loss, true distribution is one hot</span>
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
<span class="k">def</span> <span class="nf">negative_sampling_cost</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">w</span><span class="p">,</span> <span class="n">target_idx</span><span class="p">,</span> <span class="n">dataset</span><span class="p">,</span> <span class="n">sample_size</span><span class="o">=</span><span class="mi">10</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;</span>
<span class="sd">    Purpose is to replace softmax cost layer because of the huge computation cost</span>
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
    <span class="n">labels</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">array</span><span class="p">([</span><span class="mi">1</span><span class="p">]</span> <span class="o">+</span> <span class="p">[</span><span class="o">-</span><span class="mi">1</span> <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">sample_size</span><span class="p">)])</span>   <span class="c1"># (sample_size + 1,)</span>
    <span class="n">vecs</span> <span class="o">=</span> <span class="n">w</span><span class="p">[</span><span class="n">indices</span><span class="p">]</span>                                           <span class="c1"># (sample_size+1, D)</span>
    <span class="n">z</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">dot</span><span class="p">(</span><span class="n">vecs</span><span class="p">,</span> <span class="n">x</span><span class="o">.</span><span class="n">T</span><span class="p">)</span>    <span class="c1"># (sample_size + 1, D) doct (D, 1) ==&gt; (sample_size + 1)</span>
    <span class="n">z</span> <span class="o">=</span> <span class="n">z</span> <span class="o">*</span> <span class="n">labels</span>
    <span class="n">scores</span><span class="p">,</span> <span class="n">_</span> <span class="o">=</span> <span class="n">logistic</span><span class="p">(</span><span class="n">z</span><span class="p">)</span> <span class="c1"># (sample_size + 1)</span>
    <span class="n">cost</span> <span class="o">=</span> <span class="o">-</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">log</span><span class="p">(</span><span class="n">scores</span><span class="p">))</span>   <span class="c1"># A scaler </span>
    <span class="c1"># Calculate gradients</span>
    <span class="n">dz</span> <span class="o">=</span> <span class="n">labels</span> <span class="o">*</span> <span class="p">(</span><span class="n">scores</span> <span class="o">-</span><span class="mi">1</span><span class="p">)</span>   <span class="c1"># (sample_size + 1)</span>
    <span class="n">dz</span> <span class="o">=</span> <span class="n">dz</span><span class="o">.</span><span class="n">reshape</span><span class="p">((</span><span class="mi">1</span><span class="p">,</span> <span class="n">sample_size</span> <span class="o">+</span> <span class="mi">1</span><span class="p">))</span>
    <span class="n">dx</span> <span class="o">=</span> <span class="n">dz</span><span class="o">.</span><span class="n">dot</span><span class="p">(</span><span class="n">vecs</span><span class="p">)</span>    <span class="c1"># (sample_size + 1) dot (sample_size + 1, D) ==&gt; (1, D)</span>
    <span class="n">dvecs</span> <span class="o">=</span> <span class="n">dz</span><span class="o">.</span><span class="n">T</span><span class="o">.</span><span class="n">dot</span><span class="p">(</span><span class="n">x</span><span class="o">.</span><span class="n">reshape</span><span class="p">((</span><span class="mi">1</span><span class="p">,</span> <span class="n">D</span><span class="p">)))</span>  <span class="c1"># (sample_size + 1, 1) dot (1, D) ==&gt; (sample_size + 1, D)</span>
    
    <span class="c1"># Copy gradient for sample vectors to complete dW array</span>
    <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">sample_size</span> <span class="o">+</span> <span class="mi">1</span><span class="p">):</span>
        <span class="n">dw</span><span class="p">[</span><span class="n">indices</span><span class="p">[</span><span class="n">i</span><span class="p">]]</span> <span class="o">+=</span> <span class="n">dvecs</span><span class="p">[</span><span class="n">i</span><span class="p">,:]</span>
    
    <span class="k">return</span> <span class="n">cost</span><span class="p">,</span> <span class="n">dw</span><span class="p">,</span> <span class="n">dx</span><span class="o">.</span><span class="n">flatten</span><span class="p">()</span>


<span class="c1"># skipgram function</span>
<span class="k">def</span> <span class="nf">skipgram</span><span class="p">(</span><span class="n">center_word</span><span class="p">,</span> <span class="n">context_size</span><span class="p">,</span> 
             <span class="n">context_words</span><span class="p">,</span> <span class="n">input_vectors</span><span class="p">,</span> <span class="n">output_vectors</span><span class="p">,</span> 
             <span class="n">dataset</span><span class="p">,</span> <span class="n">cost_func</span><span class="o">=</span><span class="n">negative_sampling_cost</span><span class="p">):</span>
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
        <span class="n">c_cost</span><span class="p">,</span> <span class="n">c_dw</span><span class="p">,</span> <span class="n">c_dx</span> <span class="o">=</span> <span class="n">cost_func</span><span class="p">(</span><span class="n">center_word_vec</span><span class="p">,</span> <span class="n">output_vectors</span><span class="p">,</span> <span class="n">target_word_idx</span><span class="p">,</span> <span class="n">dataset</span><span class="p">)</span>
        <span class="n">cost</span> <span class="o">+=</span> <span class="n">c_cost</span>
        <span class="n">grad_in</span><span class="p">[</span><span class="n">center_word</span><span class="p">,</span> <span class="p">:]</span> <span class="o">+=</span> <span class="n">c_dx</span>
        <span class="n">grad_out</span> <span class="o">+=</span> <span class="n">c_dw</span>
        
    <span class="k">return</span> <span class="n">cost</span><span class="p">,</span> <span class="n">grad_in</span><span class="p">,</span> <span class="n">grad_out</span>
        
<span class="c1"># continuous bag of words</span>
<span class="k">def</span> <span class="nf">cbow</span><span class="p">(</span><span class="n">center_word</span><span class="p">,</span> <span class="n">context_size</span><span class="p">,</span> 
             <span class="n">context_words</span><span class="p">,</span> <span class="n">input_vectors</span><span class="p">,</span> <span class="n">output_vectors</span><span class="p">,</span> 
             <span class="n">dataset</span><span class="p">,</span> <span class="n">cost_func</span><span class="o">=</span><span class="n">negative_sampling_cost</span><span class="p">):</span>
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
    <span class="n">cost</span><span class="p">,</span> <span class="n">grad_out</span><span class="p">,</span> <span class="n">grad_cbow_vec</span> <span class="o">=</span> <span class="n">cost_func</span><span class="p">(</span><span class="n">cbow_vec</span><span class="p">,</span> <span class="n">output_vectors</span><span class="p">,</span> <span class="n">target_word_idx</span><span class="p">,</span> <span class="n">dataset</span><span class="p">)</span>

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
    <span class="k">return</span> <span class="n">random</span><span class="o">.</span><span class="n">randint</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span> <span class="mi">4</span><span class="p">),</span> <span class="p">[</span><span class="n">random</span><span class="o">.</span><span class="n">randint</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span> <span class="mi">4</span><span class="p">)</span> <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">xrange</span><span class="p">(</span><span class="mi">2</span> <span class="o">*</span> <span class="n">context_size</span><span class="p">)]</span>

<span class="k">def</span> <span class="nf">word2vec_sgd_wrapper</span><span class="p">(</span><span class="n">model</span><span class="p">,</span> <span class="n">word_vectors</span><span class="p">,</span> <span class="n">dataset</span><span class="p">,</span> <span class="n">context_size</span><span class="p">,</span> <span class="n">word2vec_cost_func</span><span class="o">=</span><span class="n">negative_sampling_cost</span><span class="p">):</span>
    <span class="n">batchsize</span> <span class="o">=</span> <span class="mi">50</span>
    <span class="n">cost</span> <span class="o">=</span> <span class="mf">0.0</span>
    <span class="n">grad</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">zeros</span><span class="p">(</span><span class="n">word_vectors</span><span class="o">.</span><span class="n">shape</span><span class="p">)</span>
    <span class="n">N</span> <span class="o">=</span> <span class="n">word_vectors</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span>
    <span class="n">input_vectors</span> <span class="o">=</span> <span class="n">word_vectors</span><span class="p">[:</span><span class="n">N</span><span class="o">/</span><span class="mi">2</span><span class="p">,</span> <span class="p">:]</span>
    <span class="n">output_vectors</span> <span class="o">=</span> <span class="n">word_vectors</span><span class="p">[</span><span class="n">N</span><span class="o">/</span><span class="mi">2</span><span class="p">:,:]</span>
    <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">xrange</span><span class="p">(</span><span class="n">batchsize</span><span class="p">):</span>
        <span class="n">c_size</span> <span class="o">=</span> <span class="n">random</span><span class="o">.</span><span class="n">randint</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span> <span class="n">context_size</span><span class="p">)</span>
        <span class="n">centerword</span><span class="p">,</span> <span class="n">context</span> <span class="o">=</span> <span class="n">getRandomContext</span><span class="p">(</span><span class="n">c_size</span><span class="p">,</span> <span class="n">dataset</span><span class="p">)</span>
        
        <span class="n">c</span><span class="p">,</span> <span class="n">gin</span><span class="p">,</span> <span class="n">gout</span> <span class="o">=</span> <span class="n">model</span><span class="p">(</span><span class="n">centerword</span><span class="p">,</span> <span class="n">c_size</span><span class="p">,</span> <span class="n">context</span><span class="p">,</span> <span class="n">input_vectors</span><span class="p">,</span> <span class="n">output_vectors</span><span class="p">,</span> <span class="n">dataset</span><span class="p">,</span> <span class="n">word2vec_cost_func</span><span class="p">)</span>
        <span class="n">cost</span> <span class="o">+=</span> <span class="n">c</span><span class="o">/</span> <span class="n">batchsize</span>
        <span class="n">grad</span><span class="p">[:</span><span class="n">N</span><span class="o">/</span><span class="mi">2</span><span class="p">,</span> <span class="p">:]</span> <span class="o">+=</span> <span class="n">gin</span> <span class="o">/</span> <span class="n">batchsize</span>
        <span class="n">grad</span><span class="p">[</span><span class="n">N</span><span class="o">/</span><span class="mi">2</span><span class="p">:,</span> <span class="p">:]</span> <span class="o">+=</span> <span class="n">gout</span> <span class="o">/</span><span class="n">batchsize</span>
        
    <span class="k">return</span> <span class="n">cost</span><span class="p">,</span> <span class="n">grad</span>

<span class="n">dataset</span> <span class="o">=</span> <span class="p">[</span><span class="s1">&#39;a&#39;</span><span class="p">,</span> <span class="s1">&#39;b&#39;</span><span class="p">,</span> <span class="s1">&#39;c&#39;</span><span class="p">,</span> <span class="s1">&#39;d&#39;</span><span class="p">,</span> <span class="s1">&#39;e&#39;</span><span class="p">]</span>



<span class="n">random</span><span class="o">.</span><span class="n">seed</span><span class="p">(</span><span class="mi">31415</span><span class="p">)</span>
<span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">seed</span><span class="p">(</span><span class="mi">9265</span><span class="p">)</span>
<span class="n">dummy_vectors</span> <span class="o">=</span> <span class="n">normalize_vecs</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">randn</span><span class="p">(</span><span class="mi">10</span><span class="p">,</span> <span class="mi">3</span><span class="p">))</span>
<span class="n">dummy_tokens</span> <span class="o">=</span> <span class="nb">dict</span><span class="p">([(</span><span class="s2">&quot;a&quot;</span><span class="p">,</span> <span class="mi">0</span><span class="p">),</span> <span class="p">(</span><span class="s2">&quot;b&quot;</span><span class="p">,</span> <span class="mi">1</span><span class="p">),</span> <span class="p">(</span><span class="s2">&quot;c&quot;</span><span class="p">,</span> <span class="mi">2</span><span class="p">),</span> <span class="p">(</span><span class="s2">&quot;d&quot;</span><span class="p">,</span> <span class="mi">3</span><span class="p">),</span> <span class="p">(</span><span class="s2">&quot;e&quot;</span><span class="p">,</span> <span class="mi">4</span><span class="p">)])</span>

<span class="n">gradcheck_naive</span><span class="p">(</span><span class="k">lambda</span> <span class="n">vec</span><span class="p">:</span> <span class="n">word2vec_sgd_wrapper</span><span class="p">(</span><span class="n">skipgram</span><span class="p">,</span> <span class="n">vec</span><span class="p">,</span> <span class="n">dataset</span><span class="p">,</span> <span class="mi">5</span><span class="p">),</span> <span class="n">dummy_vectors</span><span class="p">)</span>
<span class="n">gradcheck_naive</span><span class="p">(</span><span class="k">lambda</span> <span class="n">vec</span><span class="p">:</span> <span class="n">word2vec_sgd_wrapper</span><span class="p">(</span><span class="n">skipgram</span><span class="p">,</span> <span class="n">vec</span><span class="p">,</span> <span class="n">dataset</span><span class="p">,</span> <span class="mi">5</span><span class="p">,</span> <span class="n">softmax_cost</span><span class="p">),</span> <span class="n">dummy_vectors</span><span class="p">)</span>
<span class="n">gradcheck_naive</span><span class="p">(</span><span class="k">lambda</span> <span class="n">vec</span><span class="p">:</span> <span class="n">word2vec_sgd_wrapper</span><span class="p">(</span><span class="n">cbow</span><span class="p">,</span> <span class="n">vec</span><span class="p">,</span> <span class="n">dataset</span><span class="p">,</span> <span class="mi">5</span><span class="p">),</span> <span class="n">dummy_vectors</span><span class="p">)</span>
<span class="n">gradcheck_naive</span><span class="p">(</span><span class="k">lambda</span> <span class="n">vec</span><span class="p">:</span> <span class="n">word2vec_sgd_wrapper</span><span class="p">(</span><span class="n">cbow</span><span class="p">,</span> <span class="n">vec</span><span class="p">,</span> <span class="n">dataset</span><span class="p">,</span> <span class="mi">5</span><span class="p">,</span> <span class="n">softmax_cost</span><span class="p">),</span> <span class="n">dummy_vectors</span><span class="p">)</span>
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
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Download text8 dataset, a text-only version of Wikipedia, trimmed to the first 10^8 bytes</span>

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
<div class=" highlight hl-ipython2"><pre><span></span><span class="c1"># Read data into a list of string</span>
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
<div class=" highlight hl-ipython2"><pre><span></span><span class="k">def</span> <span class="nf">build_dataset</span><span class="p">(</span><span class="n">words_list</span><span class="p">,</span> <span class="n">vocabulary_size</span><span class="p">):</span>
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

<span class="n">vocabulary_size</span> <span class="o">=</span> <span class="mi">50000</span>
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
<pre>Most common words: [[&#39;UNK&#39;, 418391], (&#39;the&#39;, 1061396), (&#39;of&#39;, 593677), (&#39;and&#39;, 416629), (&#39;one&#39;, 411764)]
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
<div class=" highlight hl-ipython2"><pre><span></span><span class="k">def</span> <span class="nf">sgd</span><span class="p">(</span><span class="n">f</span><span class="p">,</span> <span class="n">x0</span><span class="p">,</span> <span class="n">step</span><span class="p">,</span> <span class="n">iterations</span><span class="p">,</span> <span class="n">PRINT_EVERY</span><span class="o">=</span><span class="mi">500</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot; </span>
<span class="sd">    Stochastic Gradient Descent                    </span>
<span class="sd">    </span>
<span class="sd">     Inputs:                                                         </span>
<span class="sd">     - f: the function to optimize, it should take a single        </span>
<span class="sd">         argument and yield two outputs, a cost and the gradient  </span>
<span class="sd">         with respect to the arguments                            </span>
<span class="sd">     - x0: the initial point to start SGD from                     </span>
<span class="sd">     - step: the step size for SGD                                 </span>
<span class="sd">     - iterations: total iterations to run SGD for                 </span>
<span class="sd"> </span>

<span class="sd">     Output:                                                         </span>
<span class="sd">     - x: the parameter value after SGD finishes  </span>
<span class="sd">     - cost_history: the history of cost function value</span>
<span class="sd">    &quot;&quot;&quot;</span>
    
    <span class="c1"># Anneal learning rate every several iterations</span>
    <span class="n">ANNEAL_EVERY</span> <span class="o">=</span> <span class="mi">10000</span>
    
    <span class="n">start_iter</span> <span class="o">=</span> <span class="mi">0</span>
    
    <span class="n">x</span> <span class="o">=</span> <span class="n">x0</span>
    
    
    <span class="n">expcost</span> <span class="o">=</span> <span class="bp">None</span>
    <span class="n">cost_history</span>  <span class="o">=</span> <span class="p">[]</span>
    
    <span class="k">for</span> <span class="nb">iter</span> <span class="ow">in</span> <span class="nb">xrange</span><span class="p">(</span><span class="n">start_iter</span> <span class="o">+</span> <span class="mi">1</span><span class="p">,</span> <span class="n">iterations</span> <span class="o">+</span> <span class="mi">1</span><span class="p">):</span>
        <span class="n">cost</span> <span class="o">=</span> <span class="bp">None</span>
        <span class="n">cost</span><span class="p">,</span> <span class="n">grad</span> <span class="o">=</span> <span class="n">f</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>
        <span class="n">x</span> <span class="o">-=</span> <span class="n">step</span> <span class="o">*</span> <span class="n">grad</span>
        <span class="n">cost_history</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">cost</span><span class="p">)</span>
        
        <span class="k">if</span> <span class="nb">iter</span> <span class="o">%</span> <span class="n">PRINT_EVERY</span> <span class="o">==</span> <span class="mi">0</span><span class="p">:</span>
            <span class="k">if</span> <span class="ow">not</span> <span class="n">expcost</span><span class="p">:</span>
                <span class="n">expcost</span> <span class="o">=</span> <span class="n">cost</span>
            <span class="k">else</span><span class="p">:</span>
                <span class="n">expcost</span> <span class="o">=</span> <span class="o">.</span><span class="mi">95</span> <span class="o">*</span> <span class="n">expcost</span> <span class="o">+</span> <span class="o">.</span><span class="mo">05</span> <span class="o">*</span> <span class="n">cost</span>
            <span class="k">print</span> <span class="s2">&quot;</span><span class="se">\r</span><span class="s2">&gt;&gt;&gt; iter </span><span class="si">%d</span><span class="s2">: </span><span class="si">%f</span><span class="s2">&quot;</span> <span class="o">%</span> <span class="p">(</span><span class="nb">iter</span><span class="p">,</span> <span class="n">expcost</span><span class="p">)</span>
        
            
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
<div class=" highlight hl-ipython2"><pre><span></span><span class="n">embedding_size</span> <span class="o">=</span> <span class="mi">32</span>
<span class="n">word_vectors</span> <span class="o">=</span> <span class="n">normalize_vecs</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">randn</span><span class="p">(</span><span class="mi">2</span> <span class="o">*</span> <span class="n">vocabulary_size</span><span class="p">,</span> <span class="n">embedding_size</span><span class="p">))</span>
<span class="n">context_window_size</span> <span class="o">=</span> <span class="mi">2</span>

<span class="n">trained_word_vector</span><span class="p">,</span> <span class="n">cost_history</span> <span class="o">=</span> <span class="n">sgd</span><span class="p">(</span><span class="k">lambda</span> <span class="n">vec</span><span class="p">:</span> <span class="n">word2vec_sgd_wrapper</span><span class="p">(</span><span class="n">skipgram</span><span class="p">,</span> <span class="n">vec</span><span class="p">,</span> <span class="n">dataset</span><span class="p">,</span> <span class="mi">5</span><span class="p">),</span>
                         <span class="n">word_vectors</span><span class="p">,</span> <span class="mf">0.1</span><span class="p">,</span> <span class="mi">20000</span><span class="p">)</span>

<span class="c1">#print len(dataset)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>&gt;&gt;&gt; iter 500: 38.116903
&gt;&gt;&gt; iter 1000: 37.195350
&gt;&gt;&gt; iter 1500: 35.440778
&gt;&gt;&gt; iter 2000: 33.706059
&gt;&gt;&gt; iter 2500: 32.041080
&gt;&gt;&gt; iter 3000: 30.452728
&gt;&gt;&gt; iter 3500: 28.941955
&gt;&gt;&gt; iter 4000: 27.503316
&gt;&gt;&gt; iter 4500: 26.143659
&gt;&gt;&gt; iter 5000: 24.842278
&gt;&gt;&gt; iter 5500: 23.605699
&gt;&gt;&gt; iter 6000: 22.430370
&gt;&gt;&gt; iter 6500: 21.313718
&gt;&gt;&gt; iter 7000: 20.251640
&gt;&gt;&gt; iter 7500: 19.242406
&gt;&gt;&gt; iter 8000: 18.289291
&gt;&gt;&gt; iter 8500: 17.384212
&gt;&gt;&gt; iter 9000: 16.518030
&gt;&gt;&gt; iter 9500: 15.702365
&gt;&gt;&gt; iter 10000: 14.919712
&gt;&gt;&gt; iter 10500: 14.175952
&gt;&gt;&gt; iter 11000: 13.469200
&gt;&gt;&gt; iter 11500: 12.798035
&gt;&gt;&gt; iter 12000: 12.160320
&gt;&gt;&gt; iter 12500: 11.554405
&gt;&gt;&gt; iter 13000: 10.978509
&gt;&gt;&gt; iter 13500: 10.431386
&gt;&gt;&gt; iter 14000: 9.911849
&gt;&gt;&gt; iter 14500: 9.417995
&gt;&gt;&gt; iter 15000: 8.948789
&gt;&gt;&gt; iter 15500: 8.503029
&gt;&gt;&gt; iter 16000: 8.079481
&gt;&gt;&gt; iter 16500: 7.677241
&gt;&gt;&gt; iter 17000: 7.295171
&gt;&gt;&gt; iter 17500: 6.932300
&gt;&gt;&gt; iter 18000: 6.587423
&gt;&gt;&gt; iter 18500: 6.259686
&gt;&gt;&gt; iter 19000: 5.948062
&gt;&gt;&gt; iter 19500: 5.652199
&gt;&gt;&gt; iter 20000: 5.370939


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
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;iteration&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;cost&#39;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[10]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>&lt;matplotlib.text.Text at 0x7f7241490e90&gt;</pre>
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
<div class=" highlight hl-ipython2"><pre><span></span><span class="n">final_embeddings</span> <span class="o">=</span> <span class="n">trained_word_vector</span><span class="p">[:</span><span class="n">vocabulary_size</span><span class="p">,</span> <span class="p">:]</span> <span class="o">+</span> <span class="n">trained_word_vector</span><span class="p">[</span><span class="n">vocabulary_size</span><span class="p">:,</span> <span class="p">:]</span>
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
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAABbIAAAWhCAYAAABAp2a4AAAABHNCSVQICAgIfAhkiAAAAAlwSFlz
AAAPYQAAD2EBqD+naQAAIABJREFUeJzs3Xl8TXf+x/H3uUmQhBCE2oosRFRI6JTaScXSBV2soUWr
xtZoKdVapxh7LR3V0mZpqWrVDJFoLJFapiRp7LJo6cwP7dSaCY0k5/dHuCN2JclRr+fjcR+9Z/ue
7zl1PeSdz/0cwzRNAQAAAAAAAABgVbaingAAAAAAAAAAADdDkA0AAAAAAAAAsDSCbAAAAAAAAACA
pRFkAwAAAAAAAAAsjSAbAAAAAAAAAGBpBNkAAAAAAAAAAEsjyAYAAAAAAAAAWBpBNgAAAAAAAADA
0giyAQAAAAAAAACWRpANAAAAAAAAALC0Ag2yDcN41TCMZMMwzlx6bTMMo/0V24sbhrHQMIz/GIZx
zjCMlYZhVCjIOQEAAAAAAAAA7i8FXZH9k6Q3JTW89NooabVhGHUubZ8rqZOkZyW1kFRZ0pcFPCcA
AAAAAAAAwH3EME2zcE9oGL9KekN5gfUvkrqbprnq0rbakg5Iamya5neFOjEAAAAAAAAAgCUVWo9s
wzBshmF0l+QiabvyKrQdJW24vI9pmockHZXUpLDmBQAAAAAAAACwNseCPoFhGI8oL7guIemcpC6m
aR40DCNAUpZpmmevOuSEpIduMl45ScGSfpR0oUAmDQAAAAAAAAC4WyUk1ZAUY5rmr3czUIEH2ZIO
SqovqYzyemGHG4bR4ib7G5Ju1u8kWNKn9256AAAAAAAAAIAC1EvSZ3czQIEH2aZpZks6fGkx0TCM
P0kaLmmFpGKGYbhdVZVdQXlV2TfyoyRFRkaqTp06N9kNQFEIDQ3VnDlzinoaAG6AzyhgXXw+AWvj
MwpYF59PwLoOHDig3r17S5cy3btRGBXZV7NJKi4pQVK2pLaSLj/ssZakh5XXiuRGLkhSnTp1FBgY
WLAzBXDHSpcuzWcTsDA+o4B18fkErI3PKGBdfD6B+8Jdt4gu0CDbMIx3Ja2T9JOkUsorIW8pqZ1p
mmcNw1giabZhGKeU1z97nqStpml+V5DzAgAAAAAAAADcPwq6IruipHBJlSSdkbRbeSH2xkvbQyXl
SFqpvCrtaEmDC3hOAAAAAAAAAID7SIEG2aZpDrjF9t8kDb30AgAAAAAAAADgGraingCAP5YePXoU
9RQA3ASfUcC6+HwC1sZnFLAuPp/Ag8EwTbOo53BHDMMIlJSQkJBAI38AAAAAAAAAsKjExEQ1bNhQ
khqappl4N2NRkQ0AAAAAAAAAsDSCbAAAAAAAAACApRFkAwAAAAAAAAAsjSAbAAAAAAAAAGBpBNkA
AAAAAAAAAEsjyAYAAAAAAAAAWBpBNgAAAAAAAADA0giyAQAAAAAAAACWRpANAAAAAAAAALA0gmwA
AAAAAAAAgKURZAMAAAAAAAAALI0gGwAAAAAAAABgaQTZAAAAAAAAAABLI8gGAAAAAAAAAFgaQTYA
AAAAAAAAwNIIsgEAAAAAAAAAlkaQDQAAAAAAAACwNIJsAAAAAAAAAIClEWQDAAAAAAAAACyNIBsA
AAAAAAAAYGkE2QAAAAAAAAAASyPIBgAAAAAAAABYGkE2AAAAAAAAAMDSCLIBAAAAAAAAAJZGkA0A
AAAAAAAAsDSCbAAAAAAAAACApRFkAwAAAAAAAAAsjSAbAAAAAAAAAGBpBNkAAAAAAAAAAEsjyAYA
AAAAAAAAWBpBNgAAAAAAAADA0giyAQAAAAAAAACWRpANAAAAAAAAALA0gmwAAAAAAAAAgKURZAMA
AAAAAAAALI0gGwAAAAAAAABgaQTZAAAAAAAAAABLI8gGAAAAAAAAAFgaQTYAAAAAAAAAwNIIsgEA
AAAAAAAAlkaQDQAAAAAAAACwNIJsAAAAAAAAAIClEWQDAAAAAAAAACyNIBsAAAAAAAAAYGkE2QAA
AAAAAAAASyPIBgAAAAAAAABYGkE2AAAAAAAAAMDSCLIBAAAAAAAAAJZGkA0AAAAAAAAAsDSCbAAA
AAAAAACApRFkAwAAAAAAAAAsjSAbAAAAAAAAAGBpBNkAAAAAAAAAAEsjyAYAAAAAAAAAWBpBNgAA
AAAAAADA0giyAQAAAAAAAACWRpANAAAAAAAAALA0gmwAAAAAAAAAgKURZAMAAAAAAAAALI0gGwAA
AAAAAABgaQTZAAAAAAAAAABLI8gGAAAAAAAAAFgaQTYAAAAAAAAAwNIIsgEAAAAAAAAAlkaQDQAA
AAAAAACwNIJsAAAAAAAAAIClEWQDAAAAAAAAACyNIBsAAAAAAAAAYGkE2QAAAAAAAAAASyPIBgAA
AAAAAABYGkE2AAAAAAAAAMDSCLIBAAAAAAAAAJZGkA0AAAAAAAAAsDSCbAAAAAAAAACApRFkAwAA
AAAAAAAsjSAbAAAAAAAAAGBpBNkAAAAAAAAAAEsjyAYAAAAAAAAAWBpBNgAAAAAAAADA0giyAQAA
AAAAAACWRpANAAAAAAAAALA0gmwAAAAAAAAAgKURZAMAAAAAAAAALI0gGwAAAAAAAABgaQTZAAAA
AAAAAABLI8gGAAAAAAAAAFgaQTYAAAAAAAAAwNIIsgEAAAAAAAAAlkaQDQAAAAAAAACwNIJsAAAA
AAAAAIClEWQDAAAAAAAAACyNIBsAAAAAAAAAYGkE2QAAAAAAAAAASyPIBgAAAAAAAABYGkE2AAAA
AAAAAMDSCLIBAAAAAAAAAJZGkA0AAAAAAAAAsDSCbAAAAAAAAACApRFkAwAAAAAAAAAsjSAbAAAA
AAAAAGBpBNkAAAAAAAAAAEsjyAYAAAAAAAAAWBpBNgAAAAAAAADA0giyAQAAAAAAAACWRpANAAAA
AAAAALA0gmwAAAAAAAAAgKURZAMAAAAAAAAALI0gGwAAAMADoWbNmpo3b95N97HZbPr73/8uSTpy
5IhsNpt2795dGNMDAADATTgW9QQAAAAAwIoefvhhHT9+XOXLly/qqQAAADzwqMgGAAAAUGQuXrxY
1FO4IcMwVKFCBdls/NgEAABQ1PgXGQAAAIBC07p1aw0dOlShoaHy8PBQ+/btdebMGQ0YMEAVKlRQ
6dKlFRQUlK+dx8SJExUQEKDFixfr4Ycflqurq7p166azZ8/mG3fEiBH5ztWlSxf169cv37qzZ8+q
Z8+eKlmypKpWrar333//hnO9XmuR/fv366mnnlLp0qXl5uamli1b6ocffrjb2wIAAIBbIMgGAAAA
UKjCw8NVvHhxbdu2TYsWLdLzzz+vX3/9VTExMUpMTFRgYKCCgoJ0+vRp+zFpaWn64osvtHbtWsXE
xCgpKUmDBw++43PPnDlTAQEB+v777zV69GgNHz5cGzZsuOH+hmHY3//f//2fWrRoIWdnZ23evFmJ
iYnq16+fsrOz73geAAAAuDP0yAYAAABQqLy9vTVt2jRJ0tatW7Vz5079/PPPcnJykiRNnz5dq1at
0sqVKzVgwABJ0m+//abw8HBVqlRJkjR//nx16tRJs2bNUoUKFW773E2bNtXIkSMlSUOGDNHWrVs1
Z84ctW3b9rr7m6Zpf79gwQKVKVNGy5Ytk4ODg/1aAAAAUPCoyAYAAABQqBo1amR/n5ycrHPnzqls
2bIqVaqU/fXjjz8qPT3dvt/DDz9sD7ElqUmTJsrNzdWhQ4fu6NxNmjS5ZvnAgQO3dWxycrKaN29u
D7EBAABQeKjIBgAAAFCoXF1d7e8zMjJUuXJlxcXF5at+lqQyZcrccIzLLT8u/9dms11z/O0+SPLK
9iE34+zsfFv7AQAA4N6jIhsAAABAkQkMDNTx48fl4OAgT0/PfK+yZcva9zt69KiOHz9uX962bZsc
HBxUq1YtSZKHh4eOHTtm356bm6u9e/dec74dO3Zcs+zr63tbc/X391d8fLxycnLu6BoBAABw9wiy
AQAAABSZoKAgNWnSRJ07d9Y333yjI0eOaNu2bXr77beVmJho36948eLq27evdu/erfj4eA0fPlzd
unWz98du06aN1q5dq6ioKB06dEiDBg3K97DIy7Zu3aqZM2cqNTVVCxcu1MqVK/Xaa6/d1lyHDBmi
s2fPqlu3bkpISFBaWpoiIyOVmpp6b24GAAAAbojWIgAAAAAKzfXaeERFRWns2LHq16+ffvnlFz30
0ENq0aKFKlasaN/Hx8dHXbt2VceOHXXq1Ck99dRTWrhwoX17v379tHv3bvXt21eOjo4KDQ1VmzZt
rjn366+/rl27dmnChAkqXbq05syZo6CgoBvO78rlsmXLauPGjRo5cqRatWolBwcHNWjQQM2aNbvr
+wIAAICbM67uI2d1hmEESkpISEhQYGBgUU8HAAAAQAGbOHGiVq9ena9CGwAAANaXmJiohg0bSlJD
0zTv6h9zVGQDAAAAwG1ISUlRenq6vL295ePjU9TTAQAAeKDQIxsAAAAAbuLkyZNq376TateurY4d
O6pWrVpq376TTp06VdRTAwAAeGAQZAMAAACwtPHjxxdpW5GePUMUG7tDUqSko5IiFRu7Qz169C6y
OQEAADxoCLIBAAAA4AZSUlIUExOlnJx5knpJqiapl3Jy3lNMTJRSU1ML9PxhYWFyd3cv0HMAAADc
DwiyAQAAAOAG0tPTL71rcdWWlpKktLS0Aj2/aZoyDKNAzwEAAHA/IMgGAAAAgBvw8vK69G7Lpf+2
ljRM0suSpD59+mjJkiXKzMxUv3795ObmJh8fH0VHR0uSPvnkk2sqqlevXi2b7X8/iu3evVtt2rSR
m5ubSpcurUcffVSJiYmKi4tTv379dObMGdlsNjk4OGjSpEkFe8EAAAAWRZANAAAAADdQq1YtBQd3
lIPDMOX1yP5N0hIZxhY1b95SoaGhevXVV/X888+radOmSkpKUrt27dSnTx9duHBBhmFct6L6ynW9
evVStWrVlJCQoMTERI0ePVpOTk5q2rSp5s6dKzc3N504cULHjh3TG2+8UWjXDgAAYCUE2QAAAABw
E8uWRSooqLGkEEnbJWWqXbvWWr16lUaPHq0SJUrIw8ND/fv3l5eXl8aNG6dff/1Vu3fvvq3xjx49
qqCgIPn4+MjLy0vPPvus6tWrJ0dHR5UuXVqGYcjDw0MVKlSQi4tLQV4qAACAZRFkAwAAAMBNuLu7
Kzp6rVJSUuTv76/evXsrOnqt3N3dZbPZVK5cOdWrV8++f8WKFWWapn7++efbGn/EiBHq37+/nnji
Cf31r3/V4cOHC+pSAAAA7lsE2QAAAABwG3x8fFS2bFl5eHjkW28YhpycnK7ZPzc3VzabTaZp5lt/
8eLFfMvjx4/X/v379eSTT2rjxo3y8/PT6tWr7/0FAAAA3McIsgEAAIB7KCwsTGXLli3qacAiPDw8
dO7cOZ0/f96+Likp6Zr9vL29NXz4cMXExKhr1676+OOPJUnFihVTTk5Ooc0XAADAqgiyAQAAgHuo
e/fuSklJKeppwCIee+wxOTs7a8yYMTp8+LA+++wzhYWF2bdfuHBBQ4cOVVxcnI4ePaqtW7dq586d
8vPzkyTVqFFDGRkZ2rhxo3799dd8gTgAAMCDhCAbAAAAuEeys7NVvHhxlS9fvqinggJiGMYdrXN3
d9enn36qdevWqV69evr88881ceJE+34ODg769ddf1bdvX9WuXVvdu3dXp06dNGHCBElSkyZN9Oqr
r6pbt26qUKGCZsyYUTAXBgAAYHHG1f3arM4wjEBJCQkJCQoMDCzq6QAAAOA+t3LlSk2aNElpaWly
cXFRYGCgVq9eLWdnZ3300UeaPXu2fvjhB9WsWVNDhw7VoEGDJElHjhxRzZo1tXz5cr3//vv67rvv
tGjRIpmmqddee02nTp2yn2P16tWaNGmS9u/frypVqqhPnz4aO3asHBwcJEkTJkzQxx9/rBMnTqh8
+fJ67rnnNHfu3CK5HwAAAMC9kpiYqIYNG0pSQ9M0E+9mLMd7MyUAAADg/nP8+HH17NlTM2fOVOfO
nXXu3DnFx8fLNE19+umnmjBhghYuXKgGDRooKSlJL7/8skqWLKmQkBD7GGPGjNGsWbMUEBCgEiVK
KDo6Ol+F7rfffqu+fftqwYIFat68udLS0vTKK6/IMAy98847WrlypebOnasVK1bIz89Px48fV3Jy
clHcDgAAAMCyCLIBAADwwDp27JhycnLUpUsXVatWTZJUt25dSXlV0rNmzdIzzzwjSapevbr27dun
RYsW5QuyQ0ND1blz5xueY+LEiRozZox69+5tH2fSpEkaNWqU3nnnHf3000+qVKmS2rZtKwcHB1Wt
WlWNGjUqqEvGfSIlJUXp6eny9vaWj49PUU8HAACgyNEjGwAAAA+s+vXrq23btnrkkUf0wgsv6KOP
PtLp06eVmZmp9PR09e/fX6VKlbK/3n33Xf3www/5xrj0VckbSk5O1qRJk/KN8/LLL+vEiRO6cOGC
nn/+eWVmZqpmzZp65ZVX9PXXXysnJ6cgLxsWdvLkSbVv30m1a9dWx44dVatWLbVv3ylfqxoAAIAH
EUE2AAAAHlg2m03r169XdHS06tatq/nz58vX11d79+6VJH300UdKTk62v/bu3avt27fnG8PV1fWm
58jIyNDEiROvGSclJUUlSpRQ1apVlZKSovfff18uLi4aPHiwWrZsSZj9gOrZM0SxsTskRUo6KilS
sbE71KNH7yKeGQAAQNGitQgAAAAeeE2aNFGTJk30zjvvqHr16tq6dauqVq2q9PR0de/e/YbHXdkL
+0YCAwN16NAheXp63nCf4sWL68knn9STTz6pP//5z/L19dWePXvUoEGD33U9uD+lpKQoJiZKeSF2
r0treyknx1RMTIhSU1NpMwIAAB5YBNkAAAB4YH333XfasGGD2rVrpwoVKmjHjh36z3/+Iz8/P40f
P17Dhw+Xm5ub2rdvr99++027du3S6dOn9dprr0mSTNO85TnGjRunp556StWqVdNzzz0nm81mr8qe
PHmywsLClJOTo8cee0wuLi6KiIiQi4uLqlevXtCXD4tJT0+/9K7FVVtaSpLS0tIIsgEAwAOLIBsA
AAAPLDc3N23ZskXvvfeezp49q+rVq2v27NkKDg6WlNc2ZPr06Ro1apRcXV1Vr149e4gt3V5Fdrt2
7bRmzRpNmjRJ06dPl5OTk3x9fTVgwABJUpkyZTRt2jS9/vrrysnJUb169bRmzRq5u7sXzEXDsry8
vC6926L/VWRLUpwkydvbu7CnBAAAYBnG7VSRWIlhGIGSEhISEhQYGFjU0wEAAACAe6Z9+06Kjd2h
nJz3lFeJHScHh+EKCmqs6Oi1RT09AACAO5KYmHj54egNTdNMvJuxeNgjAAAAUIRSUlK0bt06paam
FvVUbmrbtm3y9/dXsWLF1LVr16Kezh/WsmWRCgpqLClE0sOSQhQU1FjLlkUW8cwAAACKFq1FAAAA
gCJw8uRJ9ewZcunhfnmCgztq2bJIS7YVGTFihAIDAxUTEyNXV1fFxcWpdevWOn36tNzc3Ip6en8Y
7u7uio5eq9TUVKWlpcnb25u+2AAAAKIiGwAAACgSPXuGKDZ2h6RISUclRSo2dod69OhdxDO7vvT0
dLVu3VqVKlWSm5ubTNOUYRi39cBL3DkfHx916NCBEBsAAOASgmwAAACgkKWkpCgmJko5OfOU91C/
apJ6KSfnPcXERBVJm5GsrCwNGzZMFStWlLOzs5o3b65du3bpyJEjstlsOnnypF566SU5ODgoLCxM
bdq0kZRXQezg4KB+/fpJkkzT1NSpU+Xp6SkXFxcFBAToyy+/tJ8nLi5ONptNGzdu1KOPPipXV1c1
bdrU8q1VAAAAULQIsgEAAIBClp6efuldi6u2tJQkpaWlFep8JGnkyJFatWqVIiIilJSUJG9vbwUH
B8vNzU3Hjh1TqVKlNG/ePB07dkwvvPCCPZxOTU3VsWPH9N5770mSpkyZosjISC1evFj79+9XaGio
QkJCFB8fn+98b7/9tubMmaOEhAQ5Ojrag3AAAADgeuiRDQAAABQyLy+vS++2KK8i+7I4SZK3t3eh
ziczM1OLFi1SeHi42rVrJ0n68MMP9c0332jp0qV6/fXXZRiG3NzcVKFCBUlS2bJlJUkeHh72HtlZ
WVmaOnWqNmzYoMcee0ySVKNGDcXHx+uDDz5Q8+bNJUmGYWjKlClq1qyZJGn06NF68sknlZWVpWLF
ihXqtQMAAOD+QEU2AABAAQoLC7Pkg/tQtGrVqqXg4I5ycBimvB7ZP0mKlIPDcAUHdyz0vsjp6enK
zs7W448/bl/n6OioP/3pTzpw4MBtj5OWlqbMzEw98cQTKlWqlP0VERGhw4cP59u3Xr169veVKlWS
JP388893eSUAAAD4o6IiGwAAoIAZhmF/P3HiRH399ddKSkoqwhnBCpYti1SPHr0VExNiXxcU1FHL
lkUW+lwuP7Dxyj+rl9dfve5mMjIyJElRUVGqXLlyvm3FixfPt+zk5GR/f/kcubm5tz9pAAAAPFAI
sgEAAArZnQSDN5OTkyMHB4d7MhYKn7u7u6Kj1yo1NVVpaWny9vYu9Ersy7y9veXk5KRvv/1W3bt3
lyRlZ2dr165dGjFixHWPudwCJCcnx77Oz89PxYsX15EjR+xtQwAAAIB7gdYiAAAAt2CapqZPny4f
Hx+VKFFCNWrU0NSpUxUXFyebzaazZ8/a901OTpbNZtPRo0evGScsLEwTJ0607+Pg4KDw8HAdOXJE
NptNu3fvtu975swZ2Ww2bdmyRZLs54qOjlajRo1UokQJbd26VZK0evVqNWzYUM7OzvL29takSZOo
bL2P+Pj4qEOHDkUWYkuSi4uLBg0apJEjRyomJkb79+/XgAEDdP78efXv3/+6x1SvXl2GYegf//iH
/vOf/+i///2vSpYsqTfeeEOhoaEKDw/X4cOHlZSUpAULFigiIsJ+7OUK8Ctdbx0AAABwGRXZAAAA
tzB69GgtWbJEc+fOVdOmTXXs2DEdPHhQ0vWrq29Ucd2tWzft3btXMTEx2rBhg0zTVOnSpXX8+PHb
rtIeM2aMZs6cKU9PT7m7u+vbb79V3759tWDBAjVv3lxpaWl65ZVXZBiG3nnnnd9/0XjgTJs2TaZp
qk+fPjp37pwaNWqkmJgY+4Mcr/4zWrlyZU2cOFGjR49Wv3791KdPHy1dulSTJ09WxYoVNW3aNB0+
fFhlypRRYGCg3nrrLfuxd/K5AQAAACSCbAAAgJvKyMjQvHnz9P7776t3796SpJo1a+rxxx9XXFzc
HY1VokQJlSxZUo6OjvLw8Mi37XarUSdPnqy2bdvalydOnKgxY8bY51a9enVNmjRJo0aNIsjGHSle
vLjmzp2ruXPnXnf7yZMnr1k3duxYjR079pr1Q4YM0ZAhQ647TsuWLfO1I5Gk+vXrX7MOAAAAuBJB
NgAAwE0cOHBAWVlZatOmTVFPRYZhqGHDhvnWJScna9u2bfrLX/5iX5eTk6OsrCxduHBBJUqUKOxp
AreUkpKi9PT0Iu0LDgAAgPsLQTYAAMBNODs733CbzZb3uJErq6kvXrx4x+e4k3FcXV3zLWdkZGjS
pEnq2rXrNfsSYsNqTp48qZ49QxQTE2VfFxzcUcuWRcrd3b0IZwYAAACr42GPAAAAN3H5AY8bNmy4
ZpuHh4dM09SxY8fs65KSkm46XrFixa5poXC5zcjV49xOz+DAwEAdOnRInp6e17wAq+nZM0SxsTsk
RUo6KilSsbE71KNH7yKeGQAAAKyOimwAAICbKF68uN58802NGjVKTk5Oatq0qX755Rft27dPffr0
UbVq1TRhwgT95S9/0aFDhzR79uybjlejRg398MMPSk5OVtWqVVWqVCmVKFFCjRs31l//+lfVqFFD
J06cuG5/6+v10R43bpyeeuopVatWTc8995xsNpuSk5O1d+9eTZ48+Z7dB+BupaSkXKrEjpTU69La
XsrJMRUTE6LU1NR72makdevWCggIuOVnEgAAAPcHKrIBAABuYdy4cXr99dc1fvx4+fn5qXv37vrl
l1/k6OioZcuW6eDBg6pfv75mzJihd99996ZjPfvss2rfvr1at26tChUqaPny5ZKkpUuXKisrS40a
NdKIESOuO871KrTbtWunNWvW6JtvvtGf/vQnNWnSRHPnzlWNGjXuybUD90JYWNgV/d1bXLW1pSQp
LS2tUOcEAACA+4txvcoeKzMMI1BSQkJCggIDA4t6OgAAAABu4ZNPPtFrr72mM2fOKH9Fti4thygl
JeW2KrKzs7Pl6HjrL5ZSkQ0AAFD0EhMTLxc0NDRNM/FuxqIiGwAA4D6WkpKidevWKTU1taingj+w
1q1ba/jw4XrzzTdVrlw5VapUSRMnTrRvnzNnjvz9/VWyZEk9/PDDGjx4sDIzMyVJcXFx6tevn86d
O3dp796SnpX0kySbbLZBCg7uaA+x3d3dFR4eLkk6cuSIbDabVqxYoVatWsnFxUWfffbZpYdG9lS1
atXk6uoqf39/+7cbAAAA8MdEkA0AAHAfOnnypNq376TatWurY8eOqlWrltq376RTp04V9dTwBxUe
Hq6SJUvqu+++0/Tp0zVp0iT7Q1AdHBw0f/587du3T+Hh4dq0aZNGjRolSXr88cc1d+5cubm5KSUl
Ra1atZX0laSHJZmqX7+2li2LvOm5x4wZo9DQUB04cEDBwcG6cOGCGjVqpKioKO3bt08DBw5Unz59
tHPnzoK9CQAAACgyBNkAAAAWc/HixVvu07NniGJjdyivLcNRSZGKjd2hHj16F/T08IDy9/fXO++8
Iy8vL4WEhKhRo0b2IHvYsGFq2bKlqlevrlatWmny5MlasWKFJMnJyUmlS5eWYRjy8fHRpk2xSklJ
UVRUlAzD0IQJ4+Tu7n7Tc4eGhuqZZ55R9erVVbFiRVWuXFkjRoxQvXr1VKNGDQ0ePFjBwcH64osv
Cvw+AAAAoGgQZAMAANyhNWvW5AvekpOTZbPZNHbsWPu6AQMGqG/fvrfVAqF169YaOnSoQkND5eHh
ofbt29+CU/0fAAAgAElEQVT0/CkpKYqJiVJOzjzl9RquJqmXcnLeU0xMFG1GUCD8/f3zLVeqVEk/
//yzJCk2NlZBQUGqWrWq3NzcFBISol9//VXnz5+/7lg+Pj7q0KHDbZ/7fw+KzJObm6vJkyfL399f
5cqVU6lSpbR+/XodPXr0Dq8KAAAA9wuCbAAAgDvUokULZWRkKCkpSVJeD2APDw9t3rzZvs+WLVvU
qlWr226BEB4eruLFi2vbtm1atGjRTc+fnp5+eSZXbWkpSUpLS7ubywOuy8nJKd+yYRjKzc3VkSNH
9NRTT6lBgwb66quvlJiYqIULF0q69bcLDMPQ1Q+fv94xrq6u+ZanT5+u+fPna8yYMdq8ebOSk5PV
rl07ZWVl/Z5LAwAAwH3g1o/7BgAAQD5ubm7y9/fX5s2bFRAQoM2bN2vEiBGaMGGCMjMzdfr0aaWl
pally5b2FgiXDR48WNHR0friiy/06KOP2td7e3tr2rRpt3V+Ly+vS++2KK8i+7I4+1hAYUlISFBu
bq5mzpxpX3f1tw6KFSumnJyca4718PDQsWPH7Mupqan2h0ReZhjGNcdt27ZNzzzzjHr06CFJMk1T
qamp8vPzu6trAQAAgHVRkQ0AAPA7tGrVyl6BHR8fr65du8rX11dbt25VXFycqlSpIk9Pz9tugdCo
UaPbPnetWrUUHNxRDg7DlNcj+ydJkXJwGK7g4I7y8fG5Z9cJ3Iq3t7eys7M1b948/fDDD4qIiNAH
H3yQb58aNWooIyNDGzduzNdypE2bNlqwYIG+//577dq1S4MGDVKxYsXyHXt1xbaU15rkm2++0fbt
23XgwAENHDhQx48fL7iLBAAAQJEjyAYAAPgdWrZsqfj4eCUnJ6tYsWLy8fFRy5YttWnTJsXFxalV
q1aSbr8FwtWtE25l2bJIBQU1lhQi6WFJIQoKaqxlyyLvyfUBV7peVfRl/v7+mj17tqZPn6569epp
2bJl13y7oEmTJnr11VfVrVs3VahQQTNmzJAkzZo1S9WqVVOLFi3Uu3dvjRw5Ui4uLrc899tvv63A
wEC1b99ebdq0UaVKldSlS5fbnjMAAADuP8b1KhyszDCMQEkJCQkJCgwMLOrpAACAB9Tp06dVvnx5
hYSEKCsrS59++qm+/vprTZ8+XadOndLrr7+uAQMG6Omnn1bFihX14YcfSsqrLq1Tp478/Pz01Vdf
Scp72GNAQIBmz559x/NITU1VWlqavL29qcQGAAAAYCmJiYmXH9zd0DTNxLsZi4psAACA36FMmTKq
V6+eIiMj7dXXLVu2VEJCglJSUuzrCroFgo+Pjzp06ECIjQdeSkqK1q1bp9TU1KKeCgAAAAoAQTYA
AMDv1KpVK+Xm5tpDa3d3d/n5+alSpUr2By7SAgEoWCdPnlT79p1Uu3ZtdezYUbVq1VL79p106tSp
op4aAAAA7iFaiwAAAAC4b7Vv30mxsTuUkzNPUgtJW+TgMExBQY0VHb22qKcHAADwQKO1CAAAwH2O
NgjA3UtJSVFMTNSlELuXpGqSeikn5z3FxETx+XqAtG7dWiNGjCjqaQAAgAJEkA0AAHBJdnZ2gZ+D
NgjAvZOenn7pXYurtrSUJKWlpRXqfAAAAFBwCLIBAMB9yzRNTZ06VZ6ennJxcVFAQIC+/PJLSdIn
n3wid3f3fPuvXr1aNtv//vkzceJEBQQEaMmSJfL09FSJEiUkSVlZWRo2bJgqVqwoZ2dnNW/eXLt2
7bIfFxcXJ5vNpqioKNWvX1/Ozs5q0qSJ9u3bl+983377rVq0aCEXFxdVr15dw4cPV7duPRUbu0NS
pKSjkiIVG7tDPXr0LpB7hGu99NJL6tq16w23T5w4kRZ29wkvL69L77ZctSVOkuy96nH/KoxfMAIA
gPsDQTYAALhvTZkyRZGRkVq8eLH279+v0NBQhYSEKD4+XoZhXPchilevS0tL01dffaVVq1bp+++/
lySNHDlSq1atUkREhJKSkuTt7a3g4GCdPn0637GjRo3SnDlztGvXLnl4eOjpp59WTk6OpLxK0Q4d
Ouj555/X3r179fnnn2vDhg2KjY2hDYLFjRw5Uhs2bCjqaeA21KpVS8HBHeXgMEx5vxz6SVKkHByG
Kzi4o3x8fIp4hvePjIwM9erVSyVLllSVKlU0d+7cfO06srKy9MYbb6hq1aoqWbKkmjRpori4OPvx
YWFhcnd31/r16+Xn56dSpUqpQ4cOOnHiRL7zfPTRR/Lz85Ozs7P8/Pz0t7/9zb7tyJEjstlsWrFi
hVq1aiUXFxd99tlnOnnypHr27Klq1arJ1dVV/v7+Wr58eeHcGAAAYBkE2QAA4L6UlZWlqVOnaunS
pQoKClKNGjXUp08f9erVS4sWLbrtcS5evKiIiAjVr19fjzzyiDIzM7Vo0SLNnDlT7dq1k6+vrz78
8EM5OztryZIl+Y6dMGGC2rRpo7p16yosLEzHjx/XqlWrJEnTpk1T7969NXToUHl6eqpx48Z68cUX
Lx3Z+KpZ0AbBSlxcXK6p5od1LVsWqaCgxpJCJD0sKURBQY21bFlkEc/s/hIaGqrt27drzZo1+uab
bxQfH6/ExP89j6lPnz6aNWuWpkyZoj179uj5559Xhw4drmjvIp07d06dOnXSp59+qvj4eB09elRv
vPGGffunn36qCRMmaOrUqTp48KCmTJmicePGKSIiIt9cxowZo9DQUB04cEDBwcG6cOGCGjVqpKio
KO3bt08DBw5Unz59tHPnzoK/MQAAwDIIsgEAwH0pLS1NmZmZeuKJJ1SqVCn7KyIiQocPH77tcapX
r66yZcval9PT05Wdna3HH3/cvs7R0VF/+tOfdODAAfs6wzDUuPH/Aml3d3fVrl3bvk9ycrI++eST
fHMbP378pb2/umoWtEG4kdatW2vYsGEKDQ1V2bJl9dBDD2nJkiXKzMxUv3795ObmJh8fH0VHR0uS
cnNzNWDAAHu7GV9fX82bN++m59i5c6cqVKigGTNmSMr7BUVAQIB9+0svvaQuXbpo1qxZqly5ssqX
L68hQ4bYq+8l6fjx4+rUqZNcXFzk5eWlZcuWqWbNmrc8N+6eu7u7oqPXKiUlRVFRUUpJSVF09Fp+
GXEHMjIyFB4erlmzZqlVq1by8/PTxx9/bP8z/tNPP2nlypWy2Wxq0KCBatasqREjRqhp06b6+OOP
7ePk5ubqn//8pwICAtSgQQMNGTIk37cbJkyYoFmzZumZZ55R9erV1blzZ7322mvX/PIxNDTUvk/F
ihVVuXJljRgxQvXq1VONGjU0ePBgBQcH64svviicGwQAACzBsagnAAB/NDabTV9//bWefvrpop4K
8IeWkZEhSYqKilLlypXzbStevLg2btwo0zTzrb948eI147i6uuZbvnzM1S1ITNO8bquSq13eJyMj
QwMHDtTw4cPzzePFF/tr69apys2tpLxK7Dg5OAxXUBBtEG4kPDxco0aN0s6dO/X555/r1Vdf1Vdf
faWuXbtq7Nixmj17tkJCQvTTTz/J0dFR1apV08qVK1WuXDlt27ZNr7zyiipXrqznnnvumrE3btyo
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
bdv0yCOP5NvesGFDRUdH68yZMzp79qySkpI0evToe3wHcKWtW7eqadOmGjhwoOrXry9PT0+lp6df
s1/58uW1ceNGpaenq1u3bvn+XNwpX19fZWdn52tdk5aWptOnT//uMYHCNmfOHPn6+iorK0vz589X
s2bN5OvrqxIlSkiSZs2aJUlatWqVfH191aVLF6Wlpck0Tfu3E27ExcVFktS/f391795d//d//yd/
f3+1bt1av/32mz744AOVKlVKdevWlWmaWrNmjf2hvYMGDdLhw4d1+vRptWrVSs2aNVOlSpXUpUsX
nTlzRqmpqSpVqpTi4+O1YMEClStXTr/99tt1P/cAAOD+xsMeAVhOVlaWpk6dqg0bNuixxx6TJNWo
UUPx8fH64IMP1Lx5c0VERCggIEBjxozRvHnztHTpUnuVoyQNGzbM/r569eqaPHmyBg0apAULFtjX
Z2dna9GiRapRo4Yk2b9i/vPPP8vZ2Vm+vr5q3bq1Nm3alO9r502bNtXIkSMl5QVoW7du1Zw5c/JV
hF+2fPlye6XQZUuWLJG7u7s2b96soKCge3PTABS6W1XbpqSkKD09Xd7e3lRdFyIfHx9FRERo/fr1
qlmzpiIiIrRz5055enpes+/lMLt169bq3r27li9fbn+I3Z2oXbu22rZtq5dffll/+9vf5OjoqDfe
eEMuLi639YBQwApcXV01Y8YMrV+/Xt999508PDw0YcIEDRw4UFJekYBhGIqKirK3+zlz5ozc3d2V
m5urvn37SpJCQ0PtY/r6+uZruSPl/YLv22+/1eHDh/Xdd9+pcePGWr9+/XUf2itJ7du319GjR7V2
7VrFxsZq5cqVOn/+vD7++GP9+c9/VlJSkj777LNr/k728PC4tzcIAAAUOYJsAJaTlpamzMxMPfHE
E/l+KLl48aL9h6GaNWtqxowZGjhwoLp3765u3brlGyM2NlbTpk3TwYMHdfbsWWVnZ+u3337T+fPn
5ezsLCmvOuhyiC3l9VitUaOGffvldVdXGTVp0uSa5ffee++617J79257pdCVLlcKEWQD968bBZQn
T55Uz54hiomJsq8LDu6oZcsi6Zn8O1zvPt9onWEYevXVV/X999+re/fuMgxDPXr00ODBg7Vu3brr
jl+xYkV7mN27d2999tlnv2ueERER6t+/v1q2bKmHHnpIU6dO1b59++zVrIDVff/999qzZ4+KFy+u
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
7949peZ1fkZ/foC0WbNmTJo0iVatWiGEoE6dOo98gFMaVCqVHIVQxpWX7PGy4Flrz8uRXHnktSZJ
kiRJUklQlbf6nSqVyg2IjY2Nxc3NrbS7I0lSBZaUlISjoyPaGdn8/f5dkpKS5B9lz8nb25vGjRsz
d+7cUutDcQSfZQaeJEmSJP/fIEmSJEmSVNiJEyd47bXXAF4TQpz4t/aPoy6eLkmSJFU8+TUedXRG
kvdHaDqwCh2dUfj6yhqPxWHv3r2lFsTOzMzEz68Djo6O+Pv7U69ePfz8OvDnn38+9b60M/DSgFXs
3n2UXr36FHe3pZdUUlIS27dvJzk5ubS7IknSIzzJSC5JkiRJkiTp2clAtiRJ0mOsWbMKH5/mwLuA
DfAuPj7NZY3HCqC4gs/5tdRzcsLIy8CrRV4t9VCioiJl4FF6LsX5wKUkyUD7o6WmpqJWqzl9+nRp
d+WFa9OmDR999FFpd+OFqVOnzt9f7X9oTQwAdevWfaH9kSRJkiRJqmhkIFuSJOkx8ms8JiUlERkZ
SVJSEjt2bJPlIsq54gw+yww8qSSV9Wz/8hJoL22lXTv8ZQ6mv0hyJJckSZIkSVLJkoFsSZKkJ+Dg
4ED79u3lH6EVRHEGn2UGnlRSykO2f1kPtJek2rVrExYW9kRtS3tOGiHECw+mDxgwgJiYGEJDQ1Gr
1ajVavT09AqVkzp16hRqtVqZXFGtVrNo0SL8/f3RaDTUqVOH77//XmubX3/9lXfeeQdzc3MsLS3p
3LkzqampL+zYHkeO5JIkSZIkSSo5MpAtSZIkvXSKM/gsM/CkklLWs/3LQ6D9SQwYMICuXbs+1z6i
oqJ4/fXXlcDqW2+9xYULF4psGxMTg1qtZufOnbi5uaHRaPDx8eHq1ats374dZ2dnKleuTEBAAPfu
3VO2y8rKYuTIkVSrVg1DQ0Nef/11jh8/rqy/fv06AQEBWFlZodFocHR0JDw8HAB7e3sAGjdujFqt
xtvb+7mO90mEhobi4eHBkCFDyMjI4PfffycoKIjly5drtVu+fDmtW7emdu3ayrIpU6bw9ttvc/r0
aQICAujZsyfnzp0DIDs7G19fXypXrsyhQ4c4dOgQJiYm+Pn5kZ2dXeLH9W/kSK7is2HDBlxcXNBo
NFhaWtKuXTvu3r0LwJIlS3B2dsbQ0BBnZ2cWLlyote2ECRNwdHTEyMiIOnXqMGXKFHJyckrjMCRJ
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
qVPZvft/CYqbNGkCwLVr12jevDkAVgBTcfcAACAASURBVFZWOnVreno6OTk5vPbaazp5UB4+fIiL
iwsAJ0+efKo6UpIkSaqZZEO2JElSBaoOyZxqIrVaXSJR48OHD3Wma9WqpTOtUqnIz8+v8LJJ5WPj
xvUMGfIuUVFDlXne3v46cdElqboyNDRU/r59+zZNmzYlNjb2mRLM3r59mxkzZjBw4MASywobsYsf
q3C7vn37Mnfu3BLHK2wIgrLryCc1ON++fZtRo0YRHBxc4hiWlpbo6elx/PhxfvrpJ6KjowkLC2P6
9OkcO3YMY2PjMvctlVQRCVvPnz9Pbm4ur776qjJPT08PV1dXUlNTSzRkp6amlrgX3dzcql1Ddlm0
Wq3SUCm/W1Vftra2dOnSBdCtpwqTchb9Llda/QcQGRlJ06ZNdZbVqVNHWedp6khJkiSpZpIN2ZIk
SRVIN5lTYJElMplTWczNzbly5Yoy/ccff3Dx4sWn3r527doAOknTpOqlInsiSlJlcnFx4erVq2g0
GiwtLZ9pu59//pmWLVs+8/G2bduGlZUVavWfS3fj5OTEf/7zH+W9V9oxzpw5g7W19WP3oVar6dmz
Jz179mTatGmYmJiwb98++vfv/6fKJJWvwga8wsbBovOLzytrfk2QnZ1NQMDQRyPgCvj4FDwYLSvX
hlR5ateuXS7fyRwcHKhTpw4ZGRl069at1HXKo46UJEmSqi9Zs0uSJFWgykjm9CLq2bMn69atIy4u
jlOnTvH++++jp/f0z16trKxQqVTs2LGD33//nTt37lRgaaXnYWtri5+fn3wvSDWWt7c3bm5u9O/f
nx9//JGMjAzi4+MJDQ0lOTlZWa94z8Bp06YRERHBjBkzOHv2LOfOnWPz5s18+umnZR5v7NixZGdn
884773Ds2DEuXLhAVFQUw4cPL3GMx/Hw8KB79+68+eabxMTEcOnSJfbs2aP0vp08eTIJCQmMGzeO
lJQU0tPT+eGHH5Rkj7t27WLp0qWkpKSQmZnJ2rVrEUJgb2//LJdOqkA2NjbUqlWLuLg4ZV5ubi7H
jh2jTZs2JdZ3cHDg8OHDOvMSEhIqvJzlISBgKDExhyn4npUJrCcm5jBDhrxbxSWTCrVo0YLExEQy
MjLIysoiPz+/1PrqSXWYkZEREydOJCQkhIiICC5cuMDx48dZtmwZ69atA8qnjpQkSZKqL9mQLUmS
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
oZYIqXPnzhQUFJToyC7eWDI2NmblypV06NCBli1bsn//fnbu3CmNFJe3sbV582b++usvsrOziY+P
Z+zYseWu36ugxpV5dqpzVu/iv4VHFZ9XrlyhXr16fP3111y+fJmYmBgCAgKAQh/Eb775hrZt22Jt
bS3Z9Lz//vvS8cOGDePSpUt4eXmRnZ3N1q1bsbOzY+zYsTx48EBNvSfz4qlsr8PiSswiipSYdnZ2
5VLrloaTkxN//fUXKpVKUmCGhW2je3cXYDyFSWm3Y2CgJ019NTQ05NChQ/Tu3ZshQ4YQHx/P0qVL
0dfXf6yfc1HH5/Tp03nzzTfp06cPLi4uKJVKfv31V6nj2dbWlm+//ZZvv/2WVq1aSWrTx/H111/T
sWNH+vbtS48ePejYseNjlbZeXl7cu3ePtm3b4uPjo5YHIjg4+LHxQWHn59SpUxkyZAgdOnTAwMCA
TZs2Sdt79OjB9OnTmTp1Km3btiUrK4sRI0aoxVD8fmFqakpwcDBbt27F3t6eBQsWsHDhQrX9GzRo
wKxZs/j000+pV6+elIjxUcoT//Pw6GBzdHQ0mzdvVhtsrmqF+7Vr17hx4wY///wz/fr1Y926dVy9
ehUhhGRnUpxWrVoxc+bMp74WVUFAQADvvvsuXl5etG7dmrS0NPbu3YuRkVG5vyNFPHjwQPpbJiQk
cPbsWfr27UuzZs0YMmQIFy9epG7dupVUMxmZV5MuXbqQkJBATk4Op06domPHjuTn59OnTx8peXJx
f34jIyO1WRpF/Pnnn5iamlb4oKTM87Nx4zq6dWsHDKew3TScbt3ayZYhMi8WIUS1+gBOgIiJiREy
MjKvB4MHDxbDhw+v6jBeOOfPnxeAgHUCRLFPqABEUlJSVYco84J5Fb4Dbm5uwtDQUEyaNEmcP39e
bNiwQejr64uVK1cKIYSwsLAQixcvFkIIERcXJ5RKpVi8eLFIS0sTa9euFY0aNRJKpVLcvn1brdyh
Q4cKLS0t0bt370qvk0xJMjMzhbt7r3++r4Ufd/deIjMz84Wc7+OPPxaNGjUSe/bsEWfOnBEjRowQ
tWrVErdu3RKXL18WKpVKhISEiGvXromsrCwhROF30dfXV62cHj16CEDExcUJIYRwdXUVjo6OYu/e
vSI9PV1ERUWJzz//XGzfvl3s2rVL+Pj4CEdHR7UyoqOjxdy5c8WJEyfExYsXxZYtW4S2trYIDw8v
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
WcLv//3336NXr17Q0tKCoaEhPD098ddff/Hb4+LiIBKJEB0djZ49e0JNTQ27du3CsmXLkJycDJFI
BLFYjB9//BG+vr5YsGABTp8+jWvXrsHHxwdisRgeHu4YOrQ/KtOJjAXghf79uyMoKAAhISE4fvw4
gMr0KZcuXcKHH36IlJQUpKen49///jcKCgqgoaGBoKAgBAQEYOfOncjOzsbly5fxr3/9C5GRkXx9
q6f+qI/8/HwEBQVBoVBgz549+Ne//oWPPvoIQOVomSlTpsDb2xsHDx5ETk4OLl68KKg7wzDM64z1
yGYYhmEaVG2TK6WmssmVmJYpNzcXZmZmuHLlCrp37/7C/X18fFBYWIgDBw40Qe0aX2NO9NrSZGdn
o7y8XJCrX0tLCzY2Ns1YqzfPqVOn+J+zs7MF22p7aFBQUMD/PGjQoBr7bN68GZs3bwZQ2YvSz8+v
IavLvMFedWJSpm7eeecdlJSUvNSxNe8ZXZGXl44TJ/6LS5cuISEhATNnzkTHjh3h6+uLx48fY+XK
lbCxscGdO3cwf/58+Pj44KeffhKUu3jxYqxbtw7m5uZQU1NDYGAgYmJi8PPPP4OIoK2tjbFjx6Kk
pAQjRoyApqYmAgMDUVRUBDU1NURHH0N6ejpWrlyJM2fO4NdfL2DatGlwcHDA8OHDAVQGjE+cOIFP
PvkEffr0gbq6Ovr06YMpU6YAAFasWIG2bdsiJCQE2dnZ0NHRgb29PT755BO+ni/zP5jjOHh7e+PB
gwfo3bs3JBIJAgICBJ+N4eHhWLlyJYKCgnDz5k3o6ekJ6s4wDPM64172KWBz4TjOHkBiYmJijYkS
GIZhmOalUCieBIWqT66EJ8teUCgUrBcU88rMzMwQEBCAuXPnvnJZubm5MDc3x+XLl1tkINvZ2fmV
8zcrlUqIxeIa65ctW4bDhw8jKSkJQP2D+tW9aru8yrnrKjk5Gfb29sjLy4OxsTG/3t7eHk5OTixH
dgvXmKkHmDfby05MyjSu2u8ZnQFkALjJ3zMuXrwYR48erTG/CwAkJCSgT58+uH//PqRSKeLi4uDs
7IwjR45g2LBh/H5P/79jGIZhmlZSUhJ69OgBAD2I6JU+jFlqEYZhGKbB1GVyJYZpChUVFXUeslvb
fvv370f37t0hlUrRpk0bDB06FAsXLkRERAQOHz7MD08+c+YMAGDRokWwsbGBTCaDhYUFlixZIuhZ
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
Ubt2bTIyMjh37px1/IszrOfPn8/o0aP54IMPaNGiBdu2beOFF17AycmJyMhIvvnmG/z9/Vm9ejXe
3t6UL1+eqlWr4ubmxrx584iJiQGgsLCQxMREJk2adM+vl4iIiNx/FMiW/2/v7oPtrus7gb8/xPBQ
h0RTidAMxYUkFMRgYISgo4IgoVAL2oEWaCoLrNrVwrDiajuOZKRBcCVFYq0PSBaLZNa2o6IFEh60
WQTMSnjoWDQPUGUXsBuehcJq+O4f51y8XMJDkpt7fsl9vWbunHvP7/v7nc+9M58597zP73x+AABA
x91///1Zv3593v3ud2f33XdPkrz+9a9Pklx44YX52Mc+luOPPz5Jcv755+e73/1uLrrooixatChf
+9rX8uCDD2blypWZPHlykl+fVb0h8+fPz4UXXphjjz02SbLHHnvkRz/6Ub7whS9k3rx52WWXXZIk
U6ZMydSpU5/d79RTT83ixYufDbKvvPLKPP3008/WNeSwww7L7Nmzs3DhwtH40wAA44TRIgAAAB23
//775/DDD89+++2XE044IZdcckkeeeSRPP7447nvvvvy5je/+Tnr3/KWt+Suu+5Kktxxxx2ZPXv2
syH2i3nyySezdu3anHbaadl5552f/VqwYEHuueeeF933lFNOyerVq7NixYokyWWXXZYTTjghO+20
0yb+1gAAv+aMbAAAgI7bbrvtsmzZstx8881ZtmxZFi1alI9//ONZtmxZkjzv4ovDL8i4MUHyL37x
iyS9GdkHHXTQc7ZNmDDhRffdZZdd8q53vSuLFy/O6173ulx99dVZvnz5y35sAIAX44xsAACArcQh
hxySc845J7fddlsmTpyY66+/PtOmTcuNN974nHU33XRT9tlnnyTJrFmzcvvtt+eRRx55yeNPnTo1
06ZNy9q1a7Pnnns+52uPPfZIkmy//fZJkvXr1z9v/9NPPz1LlizJl770pUyfPj1z5szZ3F8ZACCJ
M7IBAAA6b8WKFbn++utz5JFHZurUqbnllluybt267Lvvvjn77LMzf/787LnnDrmTfgAAEQNJREFU
nnnjG9+YSy+9NHfccUeuuOKKJMmJJ56Y8847L8cdd1zOO++87Lbbbrntttsybdq0HHzwwc97rPnz
5+fMM8/MpEmTctRRR+Xpp5/OD3/4wzz88MM566yzMnXq1Oy000655pprMm3atOy4446ZNGlSkmTu
3LmZPHlyFixYkHPPPXdM/0YAwLbNGdkAAAAdN2nSpCxfvjzHHHNM9t5773ziE5/IwoULM3fu3Jxx
xhn58Ic/nLPPPjuzZs3KsmXL8u1vfzt77bVXkmTixIm59tprM3Xq1BxzzDGZNWtWLrjgghccFXLa
aaflkksuyeLFizNr1qwceuihueyyy569QOSECROyaNGifPGLX8y0adNy3HHHPbtvVeWUU07J+vXr
M2/evC3/hwEAxo1qrQ26ho1SVQckufXWW2/NAQccMOhyAAAAGOb000/PunXr8s1vfnOD2w877LDM
nj07CxcuHOPKAICxtnLlyhx44IFJcmBrbeXmHMtoEQAAADbbY489ljvvvDNXXHFFvvOd7wy6HABg
GyPIBgAAYLO9853vzJ133pmTTjop73jHOwZdDgCwjTEjGwAAgE320EMP5aijjsmKFSvy1FNP5dJL
L81RRx2Thx9+eNClAQDbEEE2AAAAm+ykk+bluutuSXJ5kp8luTzXXXdLTjzxjze4vqrGsjwAYBth
tAgAAACbZNWqVVm69Kr0QuyT+/eenPXrW5YunZfVq1dnxowZz9nnhhtuGOsyAYBtgCAbAACATbJ2
7dr+d28bseXtSZLvfe97WbNmTaZPn/68QBsAYGMYLQIAAMAm2WuvvfrfLR+x5Z+SJO973/ty9NFH
Z+bMmeZmAwCbRZANAADAJpk5c2bmzj06Eyackd54kXuTXJ6qP0uyQ17u3GwAgJciyAYAAGCTLVly
eY44Yk6SeUl+O8m8tPZYkovTm5u9e3pzsz+bpUuvyurVqwdYLQCwtRJkAwAAsMle/epX55pr/jGr
Vq3KVVddlS9/+ctJnknyuyNW9uZmr1mzZqxLBAC2AS72CAAAwGabMWNGZsyYkVWrVvXvWZ7eGdlD
enOzp0+fPtalAQDbAGdkAwAAMGpeaG72hAlnZu7cozNjxowBVwgAbI0E2QAAAIyqDc3NPuKIOVmy
5PIBVwYAbK2MFgEAAGBUDc3NXr16ddasWZPp06c7ExsA2CyCbAAAALaIobnZAACby2gRAAAAAAA6
TZANAAAAAECnCbIBAAAAAOg0QTYAAAAAAJ0myAYAAAAAoNME2QAAAAAAdJogGwAAAACAThNkAwAA
AADQaYJsAAAAAAA6TZANAAAAAECnCbIBAAAAAOg0QTYAAAAAAJ0myAYAAAAAoNME2QAAAAAAdJog
GwAAAACAThNkAwAAAADQaYJsAAAAAAA6TZANAAAAAECnCbIBAAAAAOg0QTYAAAAAAJ0myAYAAAAA
oNME2QAAAAAAdJogGwAAAACAThNkAwAAAADQaYJsAAAAAAA6TZANAAAAAECnCbIBAAAAAOg0QTYA
AAAAAJ0myAYAAAAAoNME2QAAAAAAdJogGwAAAACAThNkAwAAAADQaYJsAAAAAAA6TZANAAAAAECn
CbIBAAAAAOg0QTYAAAAAAJ0myAYAAAAAoNME2QAAAAAAdJogGwAAAACAThNkAwAAAADQaYJsAAAA
AAA6TZANAAAAAECnCbIBAAAAAOg0QTYAAAAAAJ0myAYAAAAAoNME2QAAAAAAdJogGwAAAACAThNk
AwAAAADQaYJsAAAAAAA6TZANAAAAAECnCbIBAAAAAOg0QTYAAAAAAJ0myAYAAAAAoNME2QAAAAAA
dJogGwAAAACAThNkAwAAAADQaYJsAAAAAAA6TZANAAAAAECnCbIBAAAAAOg0QTYAAAAAAJ0myAYA
AAAAoNME2QAAAAAAdJogGwAAAACAThNkAwAAAADQaYJsAAAAAAA6TZANAAAAAECnCbIBAAAAAOg0
QTYAAAAAAJ0myAYAAAAAoNME2QAAAAAAdJogGwAAAACAThNkAwAAAADQaYJsAAAAAAA6TZANAAAA
AECnCbIBAAAAAOg0QTYAAAAAAJ0myAYAAAAAoNME2QAAAAAAdJogGwAAAACAThNkAwAAAADQaYJs
AAAAAAA6TZANAAAAAECnCbIBAAAAAOg0QTYAAAAAAJ0myAYAAAAAoNME2QAAAAAAdJogGwAAAACA
ThNkAwAAAADQaYJsAAAAAAA6TZANAAAAAECnCbIBAAAAAOg0QTYAAAAAAJ0myAYAAAAAoNME2QAA
AAAAdJogGwAAAACAThNkAwAAAADQaYJsAAAAAAA6TZANAAAAAECnCbIBAAAAAOg0QTYAAAAAAJ0m
yAYAAAAAoNME2QAAAAAAdJogGwAAAACAThNkAwAAAADQaYJsAAAAAAA6TZANAAAAAECnCbIBAAAA
AOg0QTYAAAAAAJ0myAYAAAAAoNME2QAAAAAAdJogGwAAAACAThNkA6NqyZIlgy4BeBF6FLpLf0K3
6VHoLv0J48MWDbKr6ltV9dOq+vequq+qvlpVu41YM6uqlvfX/LSqPrIlawK2LP9AQLfpUegu/Qnd
pkehu/QnjA9b+ozsG5Icn2Rmkvck2SvJ3w1trKqdkyxNck+SA5J8JMn8qjp9C9cFAAAAAMBW4hVb
8uCttc8O+/Heqjo/yTeqakJrbX2SP04yMclprbVfJbmrqmYn+S9JLtmStQEAAAAAsHUYsxnZVTUl
yclJvt8PsZNkTpLl/RB7yNIke1fV5LGqDQAAAACA7tqiZ2QnSf8s7A8l+Y0kNyf5vWGbd01y94hd
fj5s26MbOOSOSXLXXXeNbqHAqHj00UezcuXKQZcBvAA9Ct2lP6Hb9Ch0l/6E7hqW4e64uceq1trG
7VD1qSQffZElLck+rbVV/fVTkkxJskeSc5I81lr7vf62pUnubq396bDj75vkn4cfY8Tjn5TkaxtV
NAAAAAAAg3Jya+2KzTnApgTZv5nkN19i2d0jxoUM7Tstyb1JDmmt/aCqLkuyc2vtPcPWHJrk+iRT
WmvPOyO7//hzk/xrkqc2qngAAAAAAMbKjklel2Rpa+3BzTnQRo8W6T/gpj7ohP7tDv3bm5P85bCL
PybJkUl+sqEQe9jjb1Z6DwAAAADAmLhpNA6y0Wdkv+wDV70pyUFJbkzycJLpST6ZZJck+7XWfllV
k5L8OMm1SS5I8oYkX0lyZmvtK1ukMAAAAAAAtipbMsjeL8lnk8xK8sok9ye5OsmC1tr9w9a9Icnn
krwpybokF7fWPrNFigIAAAAAYKuzxYJsAAAAAAAYDdsNugAAAAAAAHgxgmwAAAAAADptqwqyq+pb
VfXTqvr3qrqvqr5aVbuNWDOrqpb31/y0qj4yqHphvKiqParqkqq6u6qerKrVVTW/qiaOWKc/YUCq
6i+q6vtV9URVPfQCa3avqn/sr3mgqj5dVVvV/wqwtaqqD1bVPf3nyFv6F04HxlhVvbWqrqyq/1NV
z1TV729gzSf7r0efrKprq2r6IGqF8aaq/ryqVlTVY1X186r6RlXNHLFmh6r666paV1WPV9XfV9XU
QdUM40VVfaCq7qiqR/tfN1XVUcO2j0pvbm0vTm9IcnySmUnek2SvJH83tLGqdk6yNMk9SQ5I8pEk
86vq9LEvFcaV30lSSf5Tkn2TnJXkA0kWDC3QnzBwE5N8PcnfbGhjP7C+KskrksxJ8t4kpyT55BjV
B+NWVf1hkguTnJNkdpI7kiytqtcMtDAYn16Z5PYkH0zyvAtKVdVHk3woyfuTHJTkifT6dfuxLBLG
qbcmWZTk4CRHpPf/7bKq2mnYmouSHJPkD5K8LclvJfmHMa4TxqN7k3w0yYH9rxuSfKuq9ulvH5Xe
3Kov9lhV70ryjSQ7tNbWV9WfJjk3ya6ttV/113wqybGttX0HWCqMO1V1dpIPtNam93/Wn9ABVfXe
JH/VWpsy4v7fTXJlkt1aa+v6970/yflJdhnqW2D0VdUtSX7QWjuz/3Ol92Lg4tbapwdaHIxjVfVM
kuNaa1cOu+++JP+ttfZX/Z8nJfl5kve21r4+mEphfOq/4ftvSd7WWrux34//N8kftda+0V+zd5K7
ksxpra0YXLUw/lTVg0nOTi+wHpXe3NrOyH5WVU1JcnKS77fW1vfvnpNk+YgX20uT7F1Vk8e6Rhjn
XpVk+PgC/QndNifJPw+F2H1Lk0xO8vrBlATbvv4YrgOTXD90X+udaXJdkkMGVRfwfFX1H5Lsmuf2
62NJfhD9CoPwqvQ+OTH0uvPA9D5dOLxHf5LkZ9GjMGaqaruq+qMkv5Hk5oxib251QXZVnV9Vv0iy
LsnuSY4btnnX9N4NH+7nw7YBY6A/J/BDSb4w7G79Cd2mR2EwXpNkQjbcf3oPumXX9EIz/QoD1v/0
0kVJbmyt/Uv/7l2T/L/+G0zD6VEYA1W1X1U9nuTpJJ9P8u7W2o8zir058CC7qj7Vv4jGC32tHzG8
/9NJ3pjknUnWJ/nbl3qI/u3WO0MFBmQT+jNVNS3J1Un+R2vt0pd6iP6t/oRNsCk9uon0KIy9it6D
rYV+hbH3+fSuz3Tiy1irR2Fs/DjJ/unNsf+bJF+tqt95kfUb3Zuv2PTaRs1nkix+iTV3D33TWnso
vY+NrKmqHye5t6oObq39IMkDSV47Yt+hK2COfNcceGkb1Z9V9VvpDfS/sbX2/hHr9CeMvo3q0Zfw
QJI3jbhvqGf1KGw569I7OWNDz5F6D7rlgfRedL82z+3PqUluG0hFMA5V1eeSHJ3kra21+4ZteiDJ
9lU1acSZn55TYQz0R8kOvf5cWVUHJTkzydczSr058CC7tfZgkgc3cfcJ/dsd+rc3J/nLqpowbG72
kUl+0lp7dDPKhHFpY/qzfyb2DUn+V5JTN7BEf8Io28zn0JFuTvIXVfWaYXOyj0zyaJJ/eeHdgM3R
WvtlVd2a5PD0Lrg69HHpw5NcPMjagOdqrd1TVQ+k1593Js9e7PHgJH89yNpgvOiH2McmeXtr7Wcj
Nt+a5Ffp9ejQBeVmJvnt9P7XBcbWdulltqPWmwMPsl+uqnpTkoOS3Jjk4STTk3wyyer8+pe+Iskn
klxaVRckeUOSM9JL/4EtpKp2S/K9JP+a5L8mmdp7DZ601obeXdOfMEBVtXuSKUn2SDKhqvbvb1rT
WnsiybL0Auu/raqPJtktyblJPtda++UgaoZxZGGSy/qB9ookZ6V3cZz/PsiiYDyqqlem91pzaATe
nv3nzIdaa/emN5P341W1Jr3/fc9N8r+TfGsA5cK4UlWfT2+UyO8neaKqhj7N9Ghr7anW2mNV9ZUk
C6vq4SSPp/em8PdbaysGUzWMD1W1IL0xs/cm2TnJyUnenuTI0ezN6l0Uvfuqar8kn00yK8krk9yf
3h9oQWvt/mHr3pDkc+l9PHpdkotba58Z+4ph/Kiq9yYZOQ+7krTW2oRh6/QnDEhVLU7yJxvYdFhr
bXl/ze7pzTI7NMkT6YVof95ae2aMyoRxq6r+c3pvBr82ye1J/qy19sPBVgXjT1W9Pcl38/yZnZe1
1k7tr5mf5H1JXpXkfyb5YGttzVjWCeNRVT2TDc/T/Y+tta/21+yQ3vi9E9M7E/Sa9Hr038asUBiH
quqSJO9I74SoR9P75NL5rbUb+ttHpTe3miAbAAAAAIDxabtBFwAAAAAAAC9GkA0AAAAAQKcJsgEA
AAAA6DRBNgAAAAAAnSbIBgAAAACg0wTZAAAAAAB0miAbAAAAAIBOE2QDAAAAANBpgmwAAAAAADpN
kA0AAAAAQKcJsgEAAAAA6LT/D8JMk9GiCu/cAAAAAElFTkSuQmCC
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[14]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span></span><span class="n">visualizeWords</span> <span class="o">=</span> <span class="p">[</span><span class="s2">&quot;the&quot;</span><span class="p">,</span> <span class="s2">&quot;a&quot;</span><span class="p">,</span> <span class="s2">&quot;an&quot;</span><span class="p">,</span> <span class="s2">&quot;one&quot;</span><span class="p">,</span> <span class="s2">&quot;first&quot;</span><span class="p">,</span> <span class="s2">&quot;two&quot;</span><span class="p">,</span> <span class="s2">&quot;three&quot;</span><span class="p">,</span>
	<span class="s2">&quot;good&quot;</span><span class="p">,</span> <span class="s2">&quot;great&quot;</span><span class="p">,</span> <span class="s2">&quot;cool&quot;</span><span class="p">,</span> <span class="s2">&quot;brilliant&quot;</span><span class="p">,</span> <span class="s2">&quot;wonderful&quot;</span><span class="p">,</span> <span class="s2">&quot;well&quot;</span><span class="p">,</span> <span class="s2">&quot;amazing&quot;</span><span class="p">,</span>
	<span class="s2">&quot;worth&quot;</span><span class="p">,</span> <span class="s2">&quot;sweet&quot;</span><span class="p">,</span> <span class="s2">&quot;enjoyable&quot;</span><span class="p">,</span> <span class="s2">&quot;boring&quot;</span><span class="p">,</span> <span class="s2">&quot;bad&quot;</span><span class="p">,</span> <span class="s2">&quot;waste&quot;</span><span class="p">,</span> <span class="s2">&quot;dumb&quot;</span><span class="p">,</span> 
	<span class="s2">&quot;annoying&quot;</span><span class="p">]</span>
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
RU5ErkJggg==
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
