---
title: Protractor Locators
tags: Protractor
categories:
  - Protractor
date: 2016-09-13 15:31:04
---
The `$('#some-id')` is not a jQuery selector, but a shorthanded version of `element(by.css('#some-id'))`. In this fashion, we’d be able to select elements by id, class and attributes:

    $('#some-id')                // element(by.id())
    $('.some-class')             // element(by.className())
    $('tag-name')                // element(by.tagName())
    $('[ng-message=required]')   // remember to leave out the double quotes around the value of attribute
    $('#parent #child')          // select one child inside parent
    $('ul li')                   // select all children inside parent
    $('ul li').first()           // select first of children
    $('ul li').last()            // select last of children
    $('ul li').get(index)        // select index-th of children

Then we get the more interesting ones:

    element(by.model('data'));
    element(by.repeater('cat in pets'));
    element(by.options('c for c in colors'))
    element(by.binding('value'));           // only look through the elements with ng-binding attribute
    element(by.buttonText('Save'));         // the whole of button text
    element(by.partialButtonText('Save'));  // part of button text
    element(by.cssContainingText('.pet', 'Dog')) // for selecting this: <li class="pet">Dog</li>
    element(by.deepCss('span'))             // for selecting all level of spans <span><span>x</span></span>

You can find information about locators [here][2].

[1]: http://luxiyalu.com/protractor-locators-selectors/
[2]: https://github.com/angular/protractor/blob/master/docs/locators.md
