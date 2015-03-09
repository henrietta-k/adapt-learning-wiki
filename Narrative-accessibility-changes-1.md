``` javascript
From 3f541c22dcaf4f459f2c15a0dcf78eb3e432fcf2 Mon Sep 17 00:00:00 2001
From: Dan Gray <dan@sinensis.co.uk>
Date: Fri, 13 Feb 2015 16:56:39 +0000
Subject: [PATCH] Apply new globals and focus for a11y

---
 js/adapt-contrib-narrative.js | 10 ++++++++--
 templates/narrative.hbs       | 22 +++++++++++-----------
 2 files changed, 19 insertions(+), 13 deletions(-)

diff --git a/js/adapt-contrib-narrative.js b/js/adapt-contrib-narrative.js
index beae881..b2d786a 100644
--- a/js/adapt-contrib-narrative.js
+++ b/js/adapt-contrib-narrative.js
@@ -3,6 +3,7 @@
  * License - http://github.com/adaptlearning/adapt_framework/blob/master/LICENSE
  * Maintainers - Brian Quinn <brian@learningpool.com>, Daryl Hedley <darylhedley@hotmail.com>
  */
+
 define(function(require) {
 
     var ComponentView = require('coreViews/componentView');
@@ -173,12 +174,16 @@ define(function(require) {
                 // Set the visited attribute for large screen devices
                 var currentItem = this.getCurrentItem(stage);
                 currentItem.visited = true;
+                this.$('.narrative-content-item').eq(stage).a11y_focus();
+            } else {
+                this.$('.narrative-popup-open').a11y_focus();
             }
 
             this.$('.narrative-progress').removeClass('selected').eq(stage).addClass('selected');
             this.$('.narrative-slider-graphic').children('.controls').attr('tabindex', -1);
             this.$('.narrative-slider-graphic').eq(stage).children('.controls').attr('tabindex', 0);
             this.$('.narrative-content-item').addClass('narrative-hidden').eq(stage).removeClass('narrative-hidden');
+            
 
             this.evaluateNavigation();
             this.evaluateCompletion();
@@ -281,7 +286,7 @@ define(function(require) {
             currentItem.visited = true;
 
             Adapt.trigger('notify:popup', popupObject);
-            Adapt.trigger('popup:opened');
+            Adapt.trigger('popup:opened', this.$el);
         },
 
         onNavigationClicked: function(event) {
@@ -333,11 +338,12 @@ define(function(require) {
             var previousX = this.model.get('_currentX');
             var deltaX = currentX - previousX;
 
+            Adapt.trigger('popup:closed');
+
             this.moveElement(this.$('.narrative-slider'), deltaX);
             this.moveElement(this.$('.narrative-strapline-header-inner'), deltaX);
 
             this.model.set('_currentX', currentX);
-            Adapt.trigger('popup:closed');
         }
 
     });
diff --git a/templates/narrative.hbs b/templates/narrative.hbs
index 7d4f401..eeff1b3 100755
--- a/templates/narrative.hbs
+++ b/templates/narrative.hbs
@@ -1,5 +1,5 @@
 {{! Maintainers - Brian Quinn}}
-<div class="narrative-inner component-inner" role="region" aria-label="{{_accessibility._ariaRegions.narrative}}">
+<div class="narrative-inner component-inner" role="region" aria-label="{{_globals._components._narrative.ariaRegion}}">
     {{> component this}}
     <div class="narrative-widget component-widget">
         
@@ -8,24 +8,24 @@
                 <div class="narrative-strapline-header-inner clearfix">
                     {{#each _items}}
                     <div class="narrative-strapline-title">
-                        <h5 class="narrative-strapline-title-inner">
-                           {{{strapline}}} 
-                        </h5>
+                        <div class=”narrative-strapline-title-inner accessible-text-block h5” role=”heading” aria-level=”5” tabindex=”0”>
+                            {{{strapline}}} 
+                        </div>
                     </div>
                     {{/each}}
                 </div>
             </div>
-            <a href="#" class="narrative-popup-open" tabindex="-1">
+            <a href="#" class="narrative-popup-open" tabindex="0">
                 <div class="icon icon-plus"></div>
             </a>
         </div>
         
         <div class="narrative-slide-container">
   
-            <a href="#" class="narrative-controls narrative-control-left" role="button" aria-label="{{_accessibility._ariaLabels.previous}}">
+            <a href="#" class="narrative-controls narrative-control-left" role="button" aria-label="{{_globals._accessibility._ariaLabels.previous}}">
                 <div class="icon icon-controls-left"></div>
             </a>
-            <a href="#" class="narrative-controls narrative-control-right" role="button" aria-label="{{_accessibility._ariaLabels.next}}">
+            <a href="#" class="narrative-controls narrative-control-right" role="button" aria-label="{{_globals._accessibility._ariaLabels.next}}">
                 <div class="icon icon-controls-right"></div>
             </a>
             
@@ -48,13 +48,13 @@
                 {{#each _items}}
                 <div class="narrative-content-item">
                     <div class="narrative-content-title">
-                        <h5 class="narrative-content-title-inner">
-                           {{{title}}} 
-                        </h5>
+                        <div class="narrative-content-title-inner accessible-text-block h5" role="heading" aria-level="5" tabindex="0">
+                            {{{title}}} 
+                        </div>
                     </div>
                     <div class="narrative-content-body">
                         <div class="narrative-content-body-inner">
-                            {{{body}}}
+                            {{{a11y_text body}}}
                         </div> 
                     </div>
                 </div>
-- 
2.2.1

From 587ca2d672aad2f996367933fe083f71985a13e2 Mon Sep 17 00:00:00 2001
From: Dan Gray <dan@sinensis.co.uk>
Date: Mon, 16 Feb 2015 11:37:59 +0000
Subject: [PATCH] Tidy code

Removed incorrect quote characters
---
 js/adapt-contrib-narrative.js | 2 --
 templates/narrative.hbs       | 2 +-
 2 files changed, 1 insertion(+), 3 deletions(-)

diff --git a/js/adapt-contrib-narrative.js b/js/adapt-contrib-narrative.js
index b2d786a..177787f 100644
--- a/js/adapt-contrib-narrative.js
+++ b/js/adapt-contrib-narrative.js
@@ -3,7 +3,6 @@
  * License - http://github.com/adaptlearning/adapt_framework/blob/master/LICENSE
  * Maintainers - Brian Quinn <brian@learningpool.com>, Daryl Hedley <darylhedley@hotmail.com>
  */
-
 define(function(require) {
 
     var ComponentView = require('coreViews/componentView');
@@ -183,7 +182,6 @@ define(function(require) {
             this.$('.narrative-slider-graphic').children('.controls').attr('tabindex', -1);
             this.$('.narrative-slider-graphic').eq(stage).children('.controls').attr('tabindex', 0);
             this.$('.narrative-content-item').addClass('narrative-hidden').eq(stage).removeClass('narrative-hidden');
-            
 
             this.evaluateNavigation();
             this.evaluateCompletion();
diff --git a/templates/narrative.hbs b/templates/narrative.hbs
index eeff1b3..baca4a9 100755
--- a/templates/narrative.hbs
+++ b/templates/narrative.hbs
@@ -8,7 +8,7 @@
                 <div class="narrative-strapline-header-inner clearfix">
                     {{#each _items}}
                     <div class="narrative-strapline-title">
-                        <div class=”narrative-strapline-title-inner accessible-text-block h5” role=”heading” aria-level=”5” tabindex=”0”>
+                        <div class="narrative-strapline-title-inner accessible-text-block h5" role="heading" aria-level="5" tabindex="0">
                             {{{strapline}}} 
                         </div>
                     </div>
-- 
2.2.1
```