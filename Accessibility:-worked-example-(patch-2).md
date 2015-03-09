``` javascript
From 41f59a51f311d66570bbcd626486c945c8375120 Mon Sep 17 00:00:00 2001
From: Dan Gray <dan@sinensis.co.uk>
Date: Wed, 4 Mar 2015 16:18:14 +0000
Subject: [PATCH] Focus, mobile view and tab changes

---
 js/adapt-contrib-narrative.js | 44 ++++++++++++++------------------
 less/narrative.less           | 37 ++++++++++++++++++++++++---
 templates/narrative.hbs       | 58 ++++++++++++++++++++++---------------------
 3 files changed, 82 insertions(+), 57 deletions(-)

diff --git a/js/adapt-contrib-narrative.js b/js/adapt-contrib-narrative.js
index 177787f..97560ff 100644
--- a/js/adapt-contrib-narrative.js
+++ b/js/adapt-contrib-narrative.js
@@ -12,7 +12,7 @@ define(function(require) {
 
         events: {
             'touchstart .narrative-slider': 'onTouchNavigationStarted',
-            'click .narrative-popup-open': 'openPopup',
+            'click .narrative-strapline-title': 'openPopup',
             'click .notify-popup-icon-close': 'closePopup',
             'click .narrative-controls': 'onNavigationClicked'
         },
@@ -140,18 +140,19 @@ define(function(require) {
             return model;
         },
 
-        moveSliderToIndex: function(itemIndex, animate) {
+        moveSliderToIndex: function(itemIndex, animate, callback) {
             var extraMargin = parseInt(this.$('.narrative-slider-graphic').css('margin-right'));
             var movementSize = this.$('.narrative-slide-container').width() + extraMargin;
             var marginDir = {};
             if (animate) {
                 marginDir['margin-' + this.model.get('_marginDir')] = -(movementSize * itemIndex);
-                this.$('.narrative-slider').stop().animate(marginDir);
-                this.$('.narrative-strapline-header-inner').stop(true, true).animate(marginDir);
+                this.$('.narrative-slider').velocity("stop", true).velocity(marginDir);
+                this.$('.narrative-strapline-header-inner').velocity("stop", true).velocity(marginDir, {complete:callback});
             } else {
                 marginDir['margin-' + this.model.get('_marginDir')] = -(movementSize * itemIndex);
                 this.$('.narrative-slider').css(marginDir);
                 this.$('.narrative-strapline-header-inner').css(marginDir);
+                callback();
             }
         },
 
@@ -169,27 +170,27 @@ define(function(require) {
         setStage: function(stage, initial) {
             this.model.set('_stage', stage);
 
-            if (this.model.get('_isDesktop')) {
-                // Set the visited attribute for large screen devices
-                var currentItem = this.getCurrentItem(stage);
-                currentItem.visited = true;
-                this.$('.narrative-content-item').eq(stage).a11y_focus();
-            } else {
-                this.$('.narrative-popup-open').a11y_focus();
-            }
-
             this.$('.narrative-progress').removeClass('selected').eq(stage).addClass('selected');
-            this.$('.narrative-slider-graphic').children('.controls').attr('tabindex', -1);
-            this.$('.narrative-slider-graphic').eq(stage).children('.controls').attr('tabindex', 0);
-            this.$('.narrative-content-item').addClass('narrative-hidden').eq(stage).removeClass('narrative-hidden');
+            this.$('.narrative-slider-graphic').children('.controls').a11y_cntrl_enabled(false);
+            this.$('.narrative-slider-graphic').eq(stage).children('.controls').a11y_cntrl_enabled(true);
+            this.$('.narrative-content-item').addClass('narrative-hidden').a11y_on(false).eq(stage).removeClass('narrative-hidden').a11y_on(true);
+            this.$('.narrative-strapline-title').a11y_cntrl_enabled(false).eq(stage).a11y_cntrl_enabled(true);
 
             this.evaluateNavigation();
             this.evaluateCompletion();
 
-            this.moveSliderToIndex(stage, !initial);
+            this.moveSliderToIndex(stage, !initial, _.bind(function() {
+                if (this.model.get('_isDesktop')) {
+                    // Set the visited attribute for large screen devices
+                    var currentItem = this.getCurrentItem(stage);
+                    currentItem.visited = true;
+                    this.$('.narrative-content-item').eq(stage).a11y_focus();
+                } else {
+                    this.$('.narrative-popup-open').a11y_focus();
+                }
+            }, this));
         },
 
-
         constrainStage: function(stage) {
             if (stage > this.model.get('_items').length - 1) {
                 stage = this.model.get('_items').length - 1;
@@ -284,7 +285,6 @@ define(function(require) {
             currentItem.visited = true;
 
             Adapt.trigger('notify:popup', popupObject);
-            Adapt.trigger('popup:opened', this.$el);
         },
 
         onNavigationClicked: function(event) {
@@ -297,14 +297,8 @@ define(function(require) {
 
             if ($(event.currentTarget).hasClass('narrative-control-right')) {
                 stage++;
-                if (stage === numberOfItems - 1) {
-                    this.$('.narrative-control-left').focus();
-                }
             } else if ($(event.currentTarget).hasClass('narrative-control-left')) {
                 stage--;
-                if (stage === 0) {
-                    this.$('.narrative-control-right').focus();
-                }
             }
             stage = (stage + numberOfItems) % numberOfItems;
             this.setStage(stage);
diff --git a/less/narrative.less b/less/narrative.less
index cff6589..3ef300f 100755
--- a/less/narrative.less
+++ b/less/narrative.less
@@ -23,9 +23,9 @@
     }
 
     .narrative-content {
-        float: left;
+        float: right;
         .dir-rtl & {
-            float: right;
+            float: left;
         }
         width: 36%;
         background: @inverted-background-color;
@@ -124,8 +124,6 @@
     }
 
     .narrative-strapline {
-        background-color: @inverted-background-color;
-        color: @inverted-foreground-color;
         height: auto;
         position: relative;
     }
@@ -135,11 +133,42 @@
         position: relative;
     }
 
+    .narrative-strapline-header-inner {
+        position:relative;
+    }
     .narrative-strapline-title {
+        position: relative;
         float: left;
+        text-decoration: none;
+        background-color: @button-color;
+        color: @button-text-color;
         .dir-rtl & {
             float: right;
         }
+        .icon {
+            display: block;
+            position: absolute;
+            top: 0;
+            right: 0;
+            padding: 10px;
+            color: @button-text-color;
+        }
+        &:hover {
+            background-color: @button-hover-color;
+            color: @button-text-hover-color;
+            .icon {
+                color: @button-text-hover-color;
+            }
+
+        }
+        &:focus .focus-rect {
+            position: absolute;
+            outline: @focus-outline;
+            right: extract(@focus-outline, 1);
+            bottom: extract(@focus-outline, 1);
+            top: extract(@focus-outline, 1);
+            left: extract(@focus-outline, 1);
+        }
     }
 
     .narrative-strapline-title-inner {
diff --git a/templates/narrative.hbs b/templates/narrative.hbs
index baca4a9..6f8a3e8 100755
--- a/templates/narrative.hbs
+++ b/templates/narrative.hbs
@@ -2,33 +2,52 @@
 <div class="narrative-inner component-inner" role="region" aria-label="{{_globals._components._narrative.ariaRegion}}">
     {{> component this}}
     <div class="narrative-widget component-widget">
-        
+
+        <div class="narrative-content">
+            <div class="narrative-content-inner">
+                {{#each _items}}
+                <div class="narrative-content-item">
+                    <div class="narrative-content-title">
+                        <div class="narrative-content-title-inner accessible-text-block h5" role="heading" aria-level="5" tabindex="0">
+                            {{{title}}} 
+                        </div>
+                    </div>
+                    <div class="narrative-content-body">
+                        <div class="narrative-content-body-inner">
+                            {{{a11y_text body}}}
+                        </div> 
+                    </div>
+                </div>
+                {{/each}}
+            </div>
+        </div>
+
         <div class="narrative-strapline">
             <div class="narrative-strapline-header">
                 <div class="narrative-strapline-header-inner clearfix">
+                    <div></div>
                     {{#each _items}}
-                    <div class="narrative-strapline-title">
-                        <div class="narrative-strapline-title-inner accessible-text-block h5" role="heading" aria-level="5" tabindex="0">
+                    <a href="#" role="button" class="narrative-strapline-title" aria-label="{{{strapline}}}">
+                        <div class="narrative-strapline-title-inner accessible-text-block h5">
                             {{{strapline}}} 
                         </div>
-                    </div>
+                        <div class="icon icon-plus"></div>
+                        <div class="focus-rect"></div>
+                    </a>
                     {{/each}}
                 </div>
             </div>
-            <a href="#" class="narrative-popup-open" tabindex="0">
-                <div class="icon icon-plus"></div>
-            </a>
         </div>
-        
+
         <div class="narrative-slide-container">
-  
+
             <a href="#" class="narrative-controls narrative-control-left" role="button" aria-label="{{_globals._accessibility._ariaLabels.previous}}">
                 <div class="icon icon-controls-left"></div>
             </a>
             <a href="#" class="narrative-controls narrative-control-right" role="button" aria-label="{{_globals._accessibility._ariaLabels.next}}">
                 <div class="icon icon-controls-right"></div>
             </a>
-            
+
             <div class="narrative-slider clearfix">
                 {{#each _items}}
                 <div class="narrative-slider-graphic {{#if visited}}visited{{/if}}">
@@ -43,24 +62,7 @@
             </div>
         </div>
 
-        <div class="narrative-content">
-            <div class="narrative-content-inner">
-                {{#each _items}}
-                <div class="narrative-content-item">
-                    <div class="narrative-content-title">
-                        <div class="narrative-content-title-inner accessible-text-block h5" role="heading" aria-level="5" tabindex="0">
-                            {{{title}}} 
-                        </div>
-                    </div>
-                    <div class="narrative-content-body">
-                        <div class="narrative-content-body-inner">
-                            {{{a11y_text body}}}
-                        </div> 
-                    </div>
-                </div>
-                {{/each}}
-            </div>
-        </div>
+        <div class="clearfix"></div>
 
     </div>    
 </div>
\ No newline at end of file
-- 
2.2.1

```