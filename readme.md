# Passport.js authentication for Onscribe

[Passport](http://passportjs.org/) strategy for authenticating with [Onscribe](https://onscri.be/) using the OAuth 2.0 API.

This module lets you authenticate using Onscribe in your Node.js applications.

By plugging into Passport, Onscribe authentication can be easily and unobtrusively integrated into any application or framework that supports [Connect](http://www.senchalabs.org/connect/)-style middleware, including [Express](http://expressjs.com/).

## Install
```
npm install passport-onscribe
```

## Usage

#### Configure Strategy

The Onscribe authentication strategy authenticates users using a Onscribe account and OAuth 2.0 tokens.  The strategy requires a `verify` callback, which accepts these credentials and calls `done` providing a user, as well as `options` specifying a client ID, client secret, and callback URL.
```
passport.use(new OnscribeOAuth2Strategy({
	clientID: CLIENT_ID,
	clientSecret: CLIENT_SECRET,
	callbackURL: "https://www.example.net/auth/onscribe/callback"
	},
	function(accessToken, refreshToken, profile, done) {
	User.findOrCreate({ providerId: profile.id }, function (err, user) {
		return done(err, user);
	});
	}
));
```

#### Authenticate Requests

Use `passport.authenticate()`, specifying the `'onscribe'` strategy, to authenticate requests.

For example, as route middleware in an [Express](http://expressjs.com/) application:

```
app.get('/auth/onscribe',
	passport.authenticate('onscribe'));

app.get('/auth/onscribe/callback',
	passport.authenticate('onscribe', { failureRedirect: '/login' }),
	function(req, res) {
	// Successful authentication, redirect home.
	res.redirect('/');
	});
```

## Credits

Initiated by [Makis Tracend](http://github.com/tracend)

Part of [Onscribe](http://onscri.be/) by [K&D Interactive](http://kdi.co/)

Released under the [MIT license](http://makesites.org/licenses/MIT)

