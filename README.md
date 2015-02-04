Ember-cli-sentry
================

An ember-cli addon adding [Sentry](https://www.getsentry.com) support.

## Install

From any ember-cli application, run `ember install:addon ember-cli-sentry`.

## Usage

ember-cli-sentry expects to find a `sentry` key in _ENV_.

```javascript
var ENV = {
  /* rest of the conf */
  sentry: {
    dsn: 'https://dsn_key@app.getsentry.com/app_id',
    version: '1.1.16',
    whitelistUrls: [ 'localhost:4200', 'site.local' ]
  }
}
```

## Trapping exceptions

ember-cli-sentry will trap exceptions within `Ember.run` loop and unhandled RSVP failures.

Since one will most likely implement his own ApplicationRoute error, I didn't bother adding a mixin for it.

Here is a way to trap routing errors:

```javascript
// routes/application.js

export default Ember.Route.extend({
  actions: {
    error: function(err){
      Raven.captureException(err);
      /* more error handling: redirect to a catchall route, etc */
    }
  }
});
```

## Licence

MIT