# ngModelOptions

## Overview

We've seen how to use `ng-model` to update our controller's value when a user types in a field, but we're used to controller updating immediately. `ngModelOptions` allows us to control *exactly* when these updates occur.

## Objectives

- Describe ngModelOptions
- Use ngModelOptions on an input
- Debounce Model updates
- Control when $digest cycles occur

## ngModelOptions

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

This will only update `ctrl.search` when the user exists the input.

### debounce

We can also "debounce" updates. This means that we can set a timer for the update after the user has stopped typing.

If we set it to 200ms, it will wait for no button presses on the input for 200ms before updating the value. You'll notice that Google has a similar feature - it doesn't search until you have finished typing.

```html
<input ng-model="ctrl.search" ng-model-options="{debounce: 1000}" />
```

This will only update `ctrl.search` after the user has stopped typing for a full second.

We can also pass through an object of different event types to debounce. For instance, if we wanted it to update immediately after the user exists the input, but a second after the user stops typing, we'd use:

```html
<input ng-model="ctrl.search" ng-model-options="{debounce: {'default': 1000, 'blur': 0}" />
```