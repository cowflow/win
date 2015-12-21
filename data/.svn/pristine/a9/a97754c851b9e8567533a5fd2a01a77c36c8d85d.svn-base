/*!
 * jQuery UI Touch Punch 0.2.3
 *
 * Copyright 2011–2014, Dave Furfero
 * Dual licensed under the MIT or GPL Version 2 licenses.
 *
 * Depends:
 *  jquery.ui.widget.js
 *  jquery.ui.mouse.js
 */
;!function(h){function g(m,f,p){if(!(m.originalEvent.touches.length>1)){p!==!1&&m.preventDefault();var o=m.originalEvent.changedTouches[0],n=document.createEvent("MouseEvents");n.initMouseEvent(f,!0,!0,window,1,o.screenX,o.screenY,o.clientX,o.clientY,!1,!1,!1,!1,0,null),m.target.dispatchEvent(n)}}if(h.support.touch="ontouchend" in document,h.support.touch){var l,k=h.ui.mouse.prototype,j=k._mouseInit,i=k._mouseDestroy;k._touchStart=function(b){var c=this;!l&&c._mouseCapture(b.originalEvent.changedTouches[0])&&(l=!0,c._touchMoved=!1,g(b,"mouseover",!1),g(b,"mousemove",!1),g(b,"mousedown",!1))},k._touchMove=function(b){l&&(this._touchMoved=!0,g(b,"mousemove"))},k._touchEnd=function(b){l&&(g(b,"mouseup"),g(b,"mouseout"),this._touchMoved||g(b,"click"),l=!1)},k._mouseInit=function(){var a=this;a.element.bind({touchstart:h.proxy(a,"_touchStart"),touchmove:h.proxy(a,"_touchMove"),touchend:h.proxy(a,"_touchEnd")}),j.call(a)},k._mouseDestroy=function(){var a=this;a.element.unbind({touchstart:h.proxy(a,"_touchStart"),touchmove:h.proxy(a,"_touchMove"),touchend:h.proxy(a,"_touchEnd")}),i.call(a)}}}(jQuery);