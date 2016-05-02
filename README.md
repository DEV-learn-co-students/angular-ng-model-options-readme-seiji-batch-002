# ngModelOptions

## Overview

We've seen how to use `ng-model` to update our controller's value when a user types in a field, but we're used to controllers updating immediately. `ngModelOptions` allows us to control *exactly* when these updates occur.

## Objectives

- Describe ngModelOptions
- Use ngModelOptions on an input
- Debounce Model updates
- Control when $digest cycles occur

## ngModelOptions

So far, we've been updating our model values immediately. However, in some circumstances, we might want to wait until the user has actually finished typing. You'll notice this is used quite a lot in popular applications. Facebook waits for you to have finished typing for a little bit before making a search query. This reduces server load and stops them firing off hundreds of pointless requests as the user types.

We apply `ng-model-options` to our inputs, passing in a configuration option.

```html
<input ng-model="ctrl.search" ng-model-options="{}" />
```

This configuration option can take the following options:

### updateOn

We can choose `ng-model` to only update on a certain type of event, such as `blur`. We can also use the event `default` to allow it to update on all events. You can use as many events as you want, as long as they are separated by a space.

```html
<input ng-model="ctrl.search" ng-model-options="{updateOn: 'blur'}" />
```

This will only update `ctrl.search` when the user exits the input.

### debounce

We can also "debounce" updates. This means that we can set a timer for the update after the user has stopped typing.

If we set it to 200ms, it will wait for no button presses on the input for 200ms before updating the value. You'll notice that Google has a similar feature - it doesn't search until you have finished typing.

```html
<input ng-model="ctrl.search" ng-model-options="{debounce: 1000}" />
```

This will only update `ctrl.search` after the user has stopped typing for a full second.

We can also pass through an object of different event types to debounce. For instance, if we wanted it to update immediately after the user exits the input, but a second after the user stops typing, we'd use:

```html
<input ng-model="ctrl.search" ng-model-options="{ updateOn: 'default blur', debounce: {'default': 1000, 'blur': 0} }" />
```

<p data-visibility='hidden'>View <a href='https://learn.co/lessons/angular-ng-model-options-readme'>Angular Ng Model Options </a> on Learn.co and start learning to code for free.</p>

<p class='util--hide'>View <a href='https://learn.co/lessons/angular-ng-model-options-readme'>Angular Ng Model Options </a> on Learn.co and start learning to code for free.</p>
