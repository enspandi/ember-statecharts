# Working with statecharts

## `xstate`
Everything that `ember-statecharts` is doing is powered by the wonderful [`xstate`-library](https://xstate.js.org/). The [`xstate`-guides](https://xstate.js.org/docs/) provide extensive documentation about how to write statechart-configurations - please make use of this invaluable resource.

## Authoring `statechart`-configurations

To implement a statechart via `ember-statecharts` all you have to do is to pass a valid `xstate`-statechart configuration to the `statechart`-computed macro exported from `ember-statecharts/computed`.

Here's an example that reflects the [nested statechart](https://xstate.js.org/docs/#hierarchical-nested-state-machines)-example from the [`xstate`-guides](https://xstate.js.org/docs/):

```js
import Component from '@ember/component';
import { statechart } from 'ember-statecharts/computed';

export default Component.extend({
  statechart: statechart({
    id: 'light',
    initial: 'green',
    states: {
      green: {
        on: {
          TIMER: 'yellow'
        }
      },
      yellow: {
        on: {
          TIMER: 'red'
        }
      },
      red: {
        on: {
          TIMER: 'green'
        },
        initial: 'walk',
        states: {
          walk: {
            on: {
              PED_TIMER: 'wait'
            }
          },
          wait: {
            on: {
              PED_TIMER: 'stop'
            }
          },
          stop: {}
        }
      }
    }
  }),
});

```

To get a detailed overview about the configuration options available via `xstate` please have a look at the [xstate documentation](https://xstate.js.org/docs).

## Sending events

## Matching state

## Visualizing statecharts

## ES6 classes and decorators - Ember Octane

## Caution: Actors and `invoke` 

All of `xstate`'s features are supported but not all of them are useful in the context of an `Ember.js`-application. For example due to the programming model that the framework provides direct communication between statecharts should be used with care - there's most likely a cleaner way to do what you are trying to do while staying on the path that `Ember.js` recommends.

If you don't have a `Ember.Service`-layer available to allow your various objects to access global state in a clean way it might make sense to allow interaction between statecharts directly via [Actor](https://xstate.js.org/docs/guides/actors.html#actor-api)s or [Invoking Services](https://xstate.js.org/docs/guides/communication.html#the-invoke-property) - in `Ember.js` we have other means of communicationa available to us though. We encourage to our users the usage of `Ember.Service` and `data-down-actions-up` over using `xstate`'s `Actors` and `invoke`.

## Further reading

`xstate` comes with a comprehensive [documentation page](https://xstate.js.org/docs/) - it goes into great detail what things you can do in `statechecart`-configurations.

Writing statecharts configurations is very easy once you are used to the syntax but feel free to consult the [`xstate`-guides](https://xstate.js.org/docs/) as often as necessary to get the hang of it.