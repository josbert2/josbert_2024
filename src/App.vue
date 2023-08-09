<!--<script setup>
    import anime from 'animejs/lib/anime.es.js';
    /* Ontersection observer */

    !function(t,e){"use strict";function n(t){this.time=t.time,this.target=t.target,this.rootBounds=t.rootBounds,this.boundingClientRect=t.boundingClientRect,this.intersectionRect=t.intersectionRect||a(),this.isIntersecting=!!t.intersectionRect;var e=this.boundingClientRect,n=e.width*e.height,i=this.intersectionRect,o=i.width*i.height;n?this.intersectionRatio=o/n:this.intersectionRatio=this.isIntersecting?1:0}function i(t,e){var n=e||{};if("function"!=typeof t)throw new Error("callback must be a function");if(n.root&&1!=n.root.nodeType)throw new Error("root must be an Element");this._checkForIntersections=r(this._checkForIntersections.bind(this),this.THROTTLE_TIMEOUT),this._callback=t,this._observationTargets=[],this._queuedEntries=[],this._rootMarginValues=this._parseRootMargin(n.rootMargin),this.thresholds=this._initThresholds(n.threshold),this.root=n.root||null,this.rootMargin=this._rootMarginValues.map(function(t){return t.value+t.unit}).join(" ")}function o(){return t.performance&&performance.now&&performance.now()}function r(t,e){var n=null;return function(){n||(n=setTimeout(function(){t(),n=null},e))}}function s(t,e,n,i){"function"==typeof t.addEventListener?t.addEventListener(e,n,i||!1):"function"==typeof t.attachEvent&&t.attachEvent("on"+e,n)}function h(t,e,n,i){"function"==typeof t.removeEventListener?t.removeEventListener(e,n,i||!1):"function"==typeof t.detatchEvent&&t.detatchEvent("on"+e,n)}function c(t,e){var n=Math.max(t.top,e.top),i=Math.min(t.bottom,e.bottom),o=Math.max(t.left,e.left),r=Math.min(t.right,e.right),s=r-o,h=i-n;return s>=0&&h>=0&&{top:n,bottom:i,left:o,right:r,width:s,height:h}}function u(t){var e;try{e=t.getBoundingClientRect()}catch(n){}return e?(e.width&&e.height||(e={top:e.top,right:e.right,bottom:e.bottom,left:e.left,width:e.right-e.left,height:e.bottom-e.top}),e):a()}function a(){return{top:0,bottom:0,left:0,right:0,width:0,height:0}}function l(t,e){for(var n=e;n;){if(n==t)return!0;n=p(n)}return!1}function p(t){var e=t.parentNode;return e&&11==e.nodeType&&e.host?e.host:e}if("IntersectionObserver"in t&&"IntersectionObserverEntry"in t&&"intersectionRatio"in t.IntersectionObserverEntry.prototype)return void("isIntersecting"in t.IntersectionObserverEntry.prototype||Object.defineProperty(t.IntersectionObserverEntry.prototype,"isIntersecting",{get:function(){return this.intersectionRatio>0}}));var f=[];i.prototype.THROTTLE_TIMEOUT=100,i.prototype.POLL_INTERVAL=null,i.prototype.observe=function(t){var e=this._observationTargets.some(function(e){return e.element==t});if(!e){if(!t||1!=t.nodeType)throw new Error("target must be an Element");this._registerInstance(),this._observationTargets.push({element:t,entry:null}),this._monitorIntersections(),this._checkForIntersections()}},i.prototype.unobserve=function(t){this._observationTargets=this._observationTargets.filter(function(e){return e.element!=t}),this._observationTargets.length||(this._unmonitorIntersections(),this._unregisterInstance())},i.prototype.disconnect=function(){this._observationTargets=[],this._unmonitorIntersections(),this._unregisterInstance()},i.prototype.takeRecords=function(){var t=this._queuedEntries.slice();return this._queuedEntries=[],t},i.prototype._initThresholds=function(t){var e=t||[0];return Array.isArray(e)||(e=[e]),e.sort().filter(function(t,e,n){if("number"!=typeof t||isNaN(t)||0>t||t>1)throw new Error("threshold must be a number between 0 and 1 inclusively");return t!==n[e-1]})},i.prototype._parseRootMargin=function(t){var e=t||"0px",n=e.split(/\s+/).map(function(t){var e=/^(-?\d*\.?\d+)(px|%)$/.exec(t);if(!e)throw new Error("rootMargin must be specified in pixels or percent");return{value:parseFloat(e[1]),unit:e[2]}});return n[1]=n[1]||n[0],n[2]=n[2]||n[0],n[3]=n[3]||n[1],n},i.prototype._monitorIntersections=function(){this._monitoringIntersections||(this._monitoringIntersections=!0,this.POLL_INTERVAL?this._monitoringInterval=setInterval(this._checkForIntersections,this.POLL_INTERVAL):(s(t,"resize",this._checkForIntersections,!0),s(e,"scroll",this._checkForIntersections,!0),"MutationObserver"in t&&(this._domObserver=new MutationObserver(this._checkForIntersections),this._domObserver.observe(e,{attributes:!0,childList:!0,characterData:!0,subtree:!0}))))},i.prototype._unmonitorIntersections=function(){this._monitoringIntersections&&(this._monitoringIntersections=!1,clearInterval(this._monitoringInterval),this._monitoringInterval=null,h(t,"resize",this._checkForIntersections,!0),h(e,"scroll",this._checkForIntersections,!0),this._domObserver&&(this._domObserver.disconnect(),this._domObserver=null))},i.prototype._checkForIntersections=function(){var t=this._rootIsInDom(),e=t?this._getRootRect():a();this._observationTargets.forEach(function(i){var r=i.element,s=u(r),h=this._rootContainsTarget(r),c=i.entry,a=t&&h&&this._computeTargetAndRootIntersection(r,e),l=i.entry=new n({time:o(),target:r,boundingClientRect:s,rootBounds:e,intersectionRect:a});c?t&&h?this._hasCrossedThreshold(c,l)&&this._queuedEntries.push(l):c&&c.isIntersecting&&this._queuedEntries.push(l):this._queuedEntries.push(l)},this),this._queuedEntries.length&&this._callback(this.takeRecords(),this)},i.prototype._computeTargetAndRootIntersection=function(n,i){if("none"!=t.getComputedStyle(n).display){for(var o=u(n),r=o,s=p(n),h=!1;!h;){var a=null,l=1==s.nodeType?t.getComputedStyle(s):{};if("none"==l.display)return;if(s==this.root||s==e?(h=!0,a=i):s!=e.body&&s!=e.documentElement&&"visible"!=l.overflow&&(a=u(s)),a&&(r=c(a,r),!r))break;s=p(s)}return r}},i.prototype._getRootRect=function(){var t;if(this.root)t=u(this.root);else{var n=e.documentElement,i=e.body;t={top:0,left:0,right:n.clientWidth||i.clientWidth,width:n.clientWidth||i.clientWidth,bottom:n.clientHeight||i.clientHeight,height:n.clientHeight||i.clientHeight}}return this._expandRectByRootMargin(t)},i.prototype._expandRectByRootMargin=function(t){var e=this._rootMarginValues.map(function(e,n){return"px"==e.unit?e.value:e.value*(n%2?t.width:t.height)/100}),n={top:t.top-e[0],right:t.right+e[1],bottom:t.bottom+e[2],left:t.left-e[3]};return n.width=n.right-n.left,n.height=n.bottom-n.top,n},i.prototype._hasCrossedThreshold=function(t,e){var n=t&&t.isIntersecting?t.intersectionRatio||0:-1,i=e.isIntersecting?e.intersectionRatio||0:-1;if(n!==i)for(var o=0;o<this.thresholds.length;o++){var r=this.thresholds[o];if(r==n||r==i||n>r!=i>r)return!0}},i.prototype._rootIsInDom=function(){return!this.root||l(e,this.root)},i.prototype._rootContainsTarget=function(t){return l(this.root||e,t)},i.prototype._registerInstance=function(){f.indexOf(this)<0&&f.push(this)},i.prototype._unregisterInstance=function(){var t=f.indexOf(this);-1!=t&&f.splice(t,1)},t.IntersectionObserver=i,t.IntersectionObserverEntry=n}(window,document);
    
    function isElementInViewport(el, inCB, outCB, rootMargin) {
      var margin = rootMargin || '-10%';
      function handleIntersect(entries, observer) {
        var entry = entries[0];
        if (entry.isIntersecting) {
          if (inCB && typeof inCB === 'function') inCB(el, entry);
        } else {
          if (outCB && typeof outCB === 'function') outCB(el, entry);
        }
      }
      var observer = new IntersectionObserver(handleIntersect, {rootMargin: margin});
      observer.observe(el);
    }

    var sphereAnimation = (function() {

      var sphereEl = document.querySelector('.sphere-animation');
      var spherePathEls = sphereEl.querySelectorAll('.sphere path');
      var pathLength = spherePathEls.length;
      var introPlayed = false;
      var aimations = [];

      var breathAnimation = anime({
        begin: function() {
          for (var i = 0; i < pathLength; i++) {
            aimations.push(anime({
              targets: spherePathEls[i],
              stroke: {value: ['rgba(255,75,75,1)', 'rgba(80,80,80,.35)'], duration: 500},
              translateX: [2, -4],
              translateY: [2, -4],
              easing: 'easeOutQuad',
              autoplay: false
            }));
          }
        },
        update: function(ins) {
          aimations.forEach(function(animation, i) {
            var percent = (1 - Math.sin((i * .35) + (.0022 * ins.currentTime))) / 2;
            animation.seek(animation.duration * percent);
          });
        },
        duration: Infinity,
        autoplay: false
      });

      var introAnimation = anime.timeline({
        autoplay: false
      })
      .add({
        targets: sphereEl,
        opacity: [.001, 1],
        translateY: [60, 0],
        duration: 2000,
        easing: 'easeOutSine',
      }, 0)
      .add({
        targets: spherePathEls,
        strokeDashoffset: {
          value: [anime.setDashoffset, 0],
          duration: 3900,
          easing: 'easeInOutCirc',
          delay: anime.stagger(190, {direction: 'reverse'})
        },
        duration: 2000,
        delay: anime.stagger(60, {direction: 'reverse'}),
        easing: 'linear'
      }, 0);

      var shadowAnimation = anime({
          targets: '#sphereGradient',
          x1: '25%',
          x2: '25%',
          y1: '0%',
          y2: '75%',
          duration: 30000,
          easing: 'easeOutQuint',
          autoplay: false
        }, 0);

      function play() {
        if (!introPlayed) {
          introAnimation.play();
          introPlayed = true;
        }
        breathAnimation.play();
        shadowAnimation.play();
      }

      function pause() {
        breathAnimation.pause();
        shadowAnimation.pause();
      }

    isElementInViewport(sphereEl, play, pause);

    })();
</script>-->


<template>
  asd
  <div class="feature-animation square-animation">
    <div class="relative w-96 h-96">
      <div class="sphere-animation"  ref="sphereElement"
        
      
      style="opacity: 1;transform: translateY(0px);" >
        <svg class="sphere" viewBox="0 0 440 440">
          <defs>
            <linearGradient id="sphereGradient" x1="0%" x2="0%" y1="0%" y2="0%">
              <stop stop-color="#373734" offset="0%"/>
              <stop stop-color="#242423" offset="50%"/>
              <stop stop-color="#0D0D0C" offset="100%"/>
            </linearGradient>
          </defs>
          <path d="M361.604 361.238c-24.407 24.408-51.119 37.27-59.662 28.727-8.542-8.543 4.319-35.255 28.726-59.663 24.408-24.407 51.12-37.269 59.663-28.726 8.542 8.543-4.319 35.255-28.727 59.662z"/>
          <path d="M360.72 360.354c-35.879 35.88-75.254 54.677-87.946 41.985-12.692-12.692 6.105-52.067 41.985-87.947 35.879-35.879 75.254-54.676 87.946-41.984 12.692 12.692-6.105 52.067-41.984 87.946z"/>
          <path d="M357.185 356.819c-44.91 44.91-94.376 68.258-110.485 52.149-16.11-16.11 7.238-65.575 52.149-110.485 44.91-44.91 94.376-68.259 110.485-52.15 16.11 16.11-7.239 65.576-52.149 110.486z"/>
          <path d="M350.998 350.632c-53.21 53.209-111.579 81.107-130.373 62.313-18.794-18.793 9.105-77.163 62.314-130.372 53.209-53.21 111.579-81.108 130.373-62.314 18.794 18.794-9.105 77.164-62.314 130.373z"/>
          <path d="M343.043 342.677c-59.8 59.799-125.292 91.26-146.283 70.268-20.99-20.99 10.47-86.483 70.269-146.282 59.799-59.8 125.292-91.26 146.283-70.269 20.99 20.99-10.47 86.484-70.27 146.283z"/>
          <path d="M334.646 334.28c-65.169 65.169-136.697 99.3-159.762 76.235-23.065-23.066 11.066-94.593 76.235-159.762s136.697-99.3 159.762-76.235c23.065 23.065-11.066 94.593-76.235 159.762z"/>
          <path d="M324.923 324.557c-69.806 69.806-146.38 106.411-171.031 81.76-24.652-24.652 11.953-101.226 81.759-171.032 69.806-69.806 146.38-106.411 171.031-81.76 24.652 24.653-11.953 101.226-81.759 171.032z"/>
          <path d="M312.99 312.625c-73.222 73.223-153.555 111.609-179.428 85.736-25.872-25.872 12.514-106.205 85.737-179.428s153.556-111.609 179.429-85.737c25.872 25.873-12.514 106.205-85.737 179.429z"/>
          <path d="M300.175 299.808c-75.909 75.909-159.11 115.778-185.837 89.052-26.726-26.727 13.143-109.929 89.051-185.837 75.908-75.908 159.11-115.778 185.837-89.051 26.726 26.726-13.143 109.928-89.051 185.836z"/>
          <path d="M284.707 284.34c-77.617 77.617-162.303 118.773-189.152 91.924-26.848-26.848 14.308-111.534 91.924-189.15C265.096 109.496 349.782 68.34 376.63 95.188c26.849 26.849-14.307 111.535-91.923 189.151z"/>
          <path d="M269.239 267.989c-78.105 78.104-163.187 119.656-190.035 92.807-26.849-26.848 14.703-111.93 92.807-190.035 78.105-78.104 163.187-119.656 190.035-92.807 26.849 26.848-14.703 111.93-92.807 190.035z"/>
          <path d="M252.887 252.52C175.27 330.138 90.584 371.294 63.736 344.446 36.887 317.596 78.043 232.91 155.66 155.293 233.276 77.677 317.962 36.521 344.81 63.37c26.85 26.848-14.307 111.534-91.923 189.15z"/>
          <path d="M236.977 236.61C161.069 312.52 77.867 352.389 51.14 325.663c-26.726-26.727 13.143-109.928 89.052-185.837 75.908-75.908 159.11-115.777 185.836-89.05 26.727 26.726-13.143 109.928-89.051 185.836z"/>
          <path d="M221.067 220.7C147.844 293.925 67.51 332.31 41.639 306.439c-25.873-25.873 12.513-106.206 85.736-179.429C200.6 53.786 280.931 15.4 306.804 41.272c25.872 25.873-12.514 106.206-85.737 179.429z"/>
          <path d="M205.157 204.79c-69.806 69.807-146.38 106.412-171.031 81.76-24.652-24.652 11.953-101.225 81.759-171.031 69.806-69.807 146.38-106.411 171.031-81.76 24.652 24.652-11.953 101.226-81.759 171.032z"/>
          <path d="M189.247 188.881c-65.169 65.169-136.696 99.3-159.762 76.235-23.065-23.065 11.066-94.593 76.235-159.762s136.697-99.3 159.762-76.235c23.065 23.065-11.066 94.593-76.235 159.762z"/>
          <path d="M173.337 172.971c-59.799 59.8-125.292 91.26-146.282 70.269-20.991-20.99 10.47-86.484 70.268-146.283 59.8-59.799 125.292-91.26 146.283-70.269 20.99 20.991-10.47 86.484-70.269 146.283z"/>
          <path d="M157.427 157.061c-53.209 53.21-111.578 81.108-130.372 62.314-18.794-18.794 9.104-77.164 62.313-130.373 53.21-53.209 111.58-81.108 130.373-62.314 18.794 18.794-9.105 77.164-62.314 130.373z"/>
          <path d="M141.517 141.151c-44.91 44.91-94.376 68.259-110.485 52.15-16.11-16.11 7.239-65.576 52.15-110.486 44.91-44.91 94.375-68.258 110.485-52.15 16.109 16.11-7.24 65.576-52.15 110.486z"/>
          <path d="M125.608 125.241c-35.88 35.88-75.255 54.677-87.947 41.985-12.692-12.692 6.105-52.067 41.985-87.947C115.525 43.4 154.9 24.603 167.592 37.295c12.692 12.692-6.105 52.067-41.984 87.946z"/>
          <path d="M109.698 109.332c-24.408 24.407-51.12 37.268-59.663 28.726-8.542-8.543 4.319-35.255 28.727-59.662 24.407-24.408 51.12-37.27 59.662-28.727 8.543 8.543-4.319 35.255-28.726 59.663z"/>
        </svg>
      </div>
    </div>
  </div>
</template>

<script>
import anime from 'animejs/lib/anime.es.js';

export default {
  mounted() {
    this.initializeAnimation();
  },
  methods: {
    fitElementToParent(el, padding) {
      var timeout = null;
      const resize = () => {
        if (timeout) clearTimeout(timeout);
        anime.set(el, { scale: 1 });
        const pad = padding || 0;
        const parentEl = el.parentNode;
        const elOffsetWidth = el.offsetWidth - pad;
        const parentOffsetWidth = parentEl.offsetWidth;
        const ratio = parentOffsetWidth / elOffsetWidth;
        timeout = setTimeout(anime.set(el, { scale: ratio }), 10);
      };
      resize();
      window.addEventListener('resize', resize);
    },
    initializeAnimation() {
      const sphereEl = this.$refs.sphereElement; // Accessing the element using the reference
      const spherePathEls = sphereEl.querySelectorAll('.sphere path');
      const pathLength = spherePathEls.length;
      const aimations = [];

      this.fitElementToParent(sphereEl);

      const breathAnimation = anime({
        begin: function() {
          for (let i = 0; i < pathLength; i++) {
            aimations.push(anime({
              targets: spherePathEls[i],
              stroke: { value: ['rgba(255,75,75,1)', 'rgba(80,80,80,.35)'], duration: 500 },
              translateX: [2, -4],
              translateY: [2, -4],
              easing: 'easeOutQuad',
              autoplay: false
            }));
          }
        },
        update: (ins) => {
          aimations.forEach((animation, i) => {
            const percent = (1 - Math.sin((i * 0.35) + (0.0022 * ins.currentTime))) / 2;
            animation.seek(animation.duration * percent);
          });
        },
        duration: Infinity,
        autoplay: false
      });

      const introAnimation = anime.timeline({
        autoplay: false
      })
        .add({
          targets: spherePathEls,
          strokeDashoffset: {
            value: [anime.setDashoffset, 0],
            duration: 3900,
            easing: 'easeInOutCirc',
            delay: anime.stagger(190, { direction: 'reverse' })
          },
          duration: 2000,
          delay: anime.stagger(60, { direction: 'reverse' }),
          easing: 'linear'
        }, 0);

      const shadowAnimation = anime({
        targets: '#sphereGradient',
        x1: '25%',
        x2: '25%',
        y1: '0%',
        y2: '75%',
        duration: 30000,
        easing: 'easeOutQuint',
        autoplay: false
      }, 0);

      function init() {
        introAnimation.play();
        breathAnimation.play();
        shadowAnimation.play();
      }

      init();
    },
  },
};
</script>



<style>
.feature-animation {
  grid-column: 1/13;
  position: relative;
  width: 100%;
  margin-left: auto;
  margin-right: auto;
  margin-bottom: 48px;
  padding-bottom: 50%;
}

.square-animation {
  margin-top: -20px;
  margin-bottom: 20px;
  padding-bottom: 100%;
}

@media (min-width: 740px) {
  .feature-animation {
    padding-bottom: 50%;
    margin-bottom: 96px;
  }
  .square-animation {
    margin-top: -70px;
    margin-bottom: 20px;
    padding-bottom: 100%;
  }
}

@media (min-width: 1024px) {
  .feature-animation {
    grid-column: 2/12;
  }
  .large-grid .feature-animation {
    grid-column: 1/13;
  }
}

.feature-icons-container {
  display: flex;
  flex-wrap: wrap;
}

.feature-icon img {
  width: 48px;
  height: 48px;
  transition: transform .65s ease;
}
canvas {
  width: 100%;
  height: 100%;
  display: block;
}
.sphere-animation {
    position: absolute;
    opacity: .001;
    top: 0%;
    left: 0;
    width: 100%;
    height: 100%;
}

.sphere path {
  fill: url(#sphereGradient);
  stroke-width: 1px;
  stroke: rgba(80,80,80,.35);
  backface-visibility: hidden;
}

@media (min-width: 500px) {
  .sphere path {
    stroke-width: .4px;
  }
}
</style>