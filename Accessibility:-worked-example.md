Converting a component for accessibility can seem like a daunting task. This page documents the steps one of the core devs went through when upgrading the Narrative component for accessibility. It is not intended to be a definitive walkthrough, but rather contains a few useful pointers for any devs embarking on this task.

_**Please note:** the Narrative component was by far the most complex component to convert, and so it is unlikely that you will experience all of the issues documented here._

The following is feedback given by [@oliverfoster](https://github.com/oliverfoster) regarding the first iteration of changes, which can be viewed as [a git patch file here](https://github.com/adaptlearning/adapt_framework/wiki/Accessibility:-worked-example-(patch-1)).

## Desktop tab order:

The main issue on a desktop is in getting the focus to the content title before the left and right controls. To do this it is necessary to redo the DOM order. 

1. `.narrative-content`
2. `.narrative-strapline`
3. `.narrative-slide-contrainer`

Then add a ```<div class="clearfix"></div>``` div to the end of the `.component-widget` element to make sure that the `component-widget` height accommodates the content.

So that it looks like this:
```
{{! Maintainers - Brian Quinn}}
<div class="narrative-inner component-inner" role="region" aria-label="{{_globals._components._narrative.ariaRegion}}">
    {{> component this}}
    <div class="narrative-widget component-widget">

        <div class="narrative-content">
        </div>
        
        <div class="narrative-strapline">
         </div>
        
        <div class="narrative-slide-container">
        </div>

        <div class="clearfix"></div>
     
    </div>    
</div>
```

To maintain the visual appearance it is necessary to change the LESS so that the `.narrative-content` element appears to the right of the `.narrative-slide-container` element:

```
    .narrative-content {
        float: right; /*CHANGED*/
        .dir-rtl & {
            float: left; /*CHANGED*/
        }
        width: 36%;
        background: @inverted-background-color;
        color: @inverted-foreground-color;
    }
```
### Focus plan

```
onNavigationClicked: function(event) {
            event.preventDefault();

            if (!this.model.get('_active')) return;

            var stage = this.model.get('_stage');
            var numberOfItems = this.model.get('_itemCount');

            if ($(event.currentTarget).hasClass('narrative-control-right')) {
                stage++;
                /*if (stage === numberOfItems - 1) {
                    this.$('.narrative-control-left').focus();
                }*/
            } else if ($(event.currentTarget).hasClass('narrative-control-left')) {
                stage--;
                /*if (stage === 0) {
                    this.$('.narrative-control-right').focus();
                }*/
            }
            stage = (stage + numberOfItems) % numberOfItems;
            this.setStage(stage);
        },
```

Both focus sections can be removed as the focus is set during the `setStage` function. Shifting the focus twice in quick succession confuses the screen-reader, making it irritable and potentially forcing it to behave irrationally. 

### Mobile view, strap line

The original implementation of the strapline doesn't facilitate the dotted selection outline, nor tab indexing and so it needs a slightly bigger change.

```
<div class="narrative-strapline">
            <div class="narrative-strapline-header">
                <div class="narrative-strapline-header-inner clearfix">
                    <div></div>
                    {{#each _items}}
                    <a href="#" role="button" class="narrative-strapline-title" aria-label="{{{strapline}}}">
                        <div class="narrative-strapline-title-inner accessible-text-block h5">
                            {{{strapline}}} 
                        </div>
                        <div class="icon icon-plus"></div>
                        <div class="focus-rect"></div>
                    </a>
                    {{/each}}
                </div>
            </div>
        </div>
```

Move the plus icon into each item. 
Remove the tab index from the title and add an aria-label to the link instead (as the link is natively in the tab order and the aria-label will be read instead of the title).
To each item, add an extra div in which to create a focus outline. (This is necessary as all of the strapline containers have `overflow:hidden` and outlines are always `overflow`).

The styling for this change is something like:

```
 .narrative-strapline {
        height: auto;
        position: relative;
    }

    .narrative-strapline-header {
        overflow: hidden;
        position: relative;
    }

    .narrative-strapline-header-inner {
        position:relative;
    }

    .narrative-strapline-title {
        position: relative;
        float: left;
        text-decoration: none;
        background-color: @button-color;
        color: @button-text-color;
        .dir-rtl & {
            float: right;
        }
        .icon {
            display: block;
            position: absolute;
            top: 0;
            right: 0;
            padding: 10px;
            color:@button-text-color;
        }
        &:hover {
            background-color:@button-hover-color;
            color:@button-text-hover-color;
            .icon {
                color:@button-text-hover-color;
            }
        }
        &:focus .focus-rect {
              position: absolute;
              outline: @focus-outline;
              right: extract(@focus-outline, 1);
              bottom: extract(@focus-outline, 1);
              top: extract(@focus-outline, 1);
              left: extract(@focus-outline, 1);
        }
    }

    .narrative-strapline-title-inner {
        height: (@item-padding-top + @item-padding-bottom + @icon-size);
        line-height: (@item-padding-top + @item-padding-bottom + @icon-size);
        padding-left: (@icon-size/2);
        padding-right: (@item-padding-left + @item-padding-right + @icon-size);
        .dir-rtl & {
            padding-right: (@icon-size/2);
            padding-left: (@item-padding-left + @item-padding-right + @icon-size);
        }
        text-overflow: ellipsis;
        white-space: nowrap;
        overflow: hidden;
    }
```

Remove the old styling for these elements:
```
.narrative-strapline {
        background-color: @inverted-background-color;
        color: @inverted-foreground-color;
        height: auto;
        position: relative;
    }

    .narrative-strapline-header {
        overflow: hidden;
        position: relative;
    }

    .narrative-strapline-title {
        float: left;
        .dir-rtl & {
            float: right;
        }
    }

    .narrative-strapline-title-inner {
        height: (@item-padding-top + @item-padding-bottom + @icon-size);
        line-height: (@item-padding-top + @item-padding-bottom + @icon-size);
        padding-left: (@icon-size/2);
        padding-right: (@item-padding-left + @item-padding-right + @icon-size);
        .dir-rtl & {
	        padding-right: (@icon-size/2);
	        padding-left: (@item-padding-left + @item-padding-right + @icon-size);
        }
        text-overflow: ellipsis;
        white-space: nowrap;
        overflow: hidden;
    }
```


The JavaScript also needs to be updated to allow correct focusing in mobile view as well as appropriate ordering of animations, content taborder disabling and focus attachment.

```
        moveSliderToIndex: function(itemIndex, animate, callback) {
            var extraMargin = parseInt(this.$('.narrative-slider-graphic').css('margin-right'));
            var movementSize = this.$('.narrative-slide-container').width() + extraMargin;
            var marginDir = {};
            if (animate) {
                marginDir['margin-' + this.model.get('_marginDir')] = -(movementSize * itemIndex);
                this.$('.narrative-slider').velocity("stop", true).velocity(marginDir);
                this.$('.narrative-strapline-header-inner').velocity("stop", true).velocity(marginDir, {complete:callback});
            } else {
                marginDir['margin-' + this.model.get('_marginDir')] = -(movementSize * itemIndex);
                this.$('.narrative-slider').css(marginDir);
                this.$('.narrative-strapline-header-inner').css(marginDir);
                callback();
            }
        },

        setStage: function(stage, initial) {
            this.model.set('_stage', stage);

            this.$('.narrative-progress').removeClass('selected').eq(stage).addClass('selected');
            this.$('.narrative-slider-graphic').children('.controls').a11y_cntrl_enabled(false);
            this.$('.narrative-slider-graphic').eq(stage).children('.controls').a11y_cntrl_enabled(true);
            this.$('.narrative-content-item').addClass('narrative-hidden').a11y_on(false).eq(stage).removeClass('narrative-hidden').a11y_on(true);
            this.$('.narrative-strapline-title').a11y_cntrl_enabled(false).eq(stage).a11y_cntrl_enabled(true);      

            this.evaluateNavigation();
            this.evaluateCompletion();

            this.moveSliderToIndex(stage, !initial, _.bind(function() {
                if (this.model.get('_isDesktop')) {
                    // Set the visited attribute for large screen devices
                    var currentItem = this.getCurrentItem(stage);
                    currentItem.visited = true;
                    this.$('.narrative-content-item').eq(stage).a11y_focus();
                } else {
                    this.$('.narrative-strapline-title').a11y_focus();
                }     
            }, this));
        },
```

The the click event then needs to be reattached to the new strapline title item to show the popup.
```
        events: {
            'touchstart .narrative-slider': 'onTouchNavigationStarted',
            'click .narrative-strapline-title': 'openPopup', /*CHANGED*/
            'click .notify-popup-icon-close': 'closePopup',
            'click .narrative-controls': 'onNavigationClicked'
        },
```

And finally the popup needs fixing:
```
        openPopup: function(event) {
            event.preventDefault();

            var currentItem = this.getCurrentItem(this.model.get('_stage'));
            var popupObject = {
                title: currentItem.title,
                body: currentItem.body
            };

            // Set the visited attribute for small and medium screen devices
            currentItem.visited = true;

            Adapt.trigger('notify:popup', popupObject);
            //Adapt.trigger('popup:opened', this.$el); < UNNECESSARY AS THE notify:popup MANAGES THE POPUP DOM ELEMENT
        },
```
You can view the resulting amends as [a git patch file here](https://github.com/adaptlearning/adapt_framework/wiki/Accessibility:-worked-example-(patch-2)).