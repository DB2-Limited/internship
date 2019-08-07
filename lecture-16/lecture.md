# Lecture 16

- https://nodejs.org/api/crypto.html#crypto_crypto_pbkdf2sync_password_salt_iterations_keylen_digest
- https://mongoosejs.com/docs/api.html#document_Document-invalidate
- https://mongoosejs.com/docs/guide.html#virtuals

```js
const userSchema = new mongoose.Schema({
  fullName: {
    type: String,
    required: true
  },
  email: {
    type: String,
    unique: '{VALUE} is already exist!',
    required: true,
    validate: {
      validator: function checkEmail(value) {
        const re = /^(\S+)@([a-z0-9-]+)(\.)([a-z]{2,4})(\.?)([a-z]{0,4})+$/;
        return re.test(value);
      },
      message: props => `${ props.value } is not a valid email.`
    },
  },
  photo: {
    type: String,
    default: config.get('aws').defaultUserPhoto
  },
  passwordHash: {
    type: String
  },
  salt: {
    type: String
  }
});
```

```js
userSchema.virtual('password')
  .set(function (password) {
    if (!password) {
      this.invalidate('password', 'Password can\'t be empty!');
    }

    if (password !== undefined) {
      if (password.length < 6) {
        this.invalidate('password', 'Password can\'t be less than 6 symbols!');
      }
    }

    this._plainPassword = password;

    if (password) {
      this.salt = crypto.randomBytes(config.get('crypto').hash.length).toString('base64');
      this.passwordHash = crypto.pbkdf2Sync(
        password,
        this.salt,
        config.get('crypto').hash.iterations,
        config.get('crypto').hash.length,
        'sha1'
      ).toString('base64');
    } else {
      this.salt = undefined;
      this.passwordHash = undefined;
    }
  })
  .get(function () {
    return this._plainPassword;
  });
```

```js
userSchema.methods.checkPassword = function (password) {
  if (!password) return false;
  if (!this.passwordHash) return false;

  return crypto.pbkdf2Sync(
    password,
    this.salt,
    config.get('crypto').hash.iterations,
    config.get('crypto').hash.length,
    'sha1').toString('base64') === this.passwordHash;
};
```

```js
userSchema.methods.getAuthData = function () {
  const payload = {
    id: this._id,
    email: this.email
  };
  return {
    token: jwt.encode(payload, config.get('jwtSecret')),
    user: {
      fullName: this.fullName,
      photo: this.photo
    }
  };
};
```

- http://www.passportjs.org/
- https://github.com/rkusa/koa-passport
- https://www.npmjs.com/package/passport-local
- https://www.npmjs.com/package/passport-jwt


```js
const passport = require('koa-passport');

passport.use(require('./jwtStrategy'));
passport.use(require('./localStrategy'));

module.exports = passport;
```

```js
const JwtStrategy = require('passport-jwt').Strategy;
const ExtractJwt = require('passport-jwt').ExtractJwt;
const config = require('config');

const User = require('../../accounts/models/user');


let opts = {
  jwtFromRequest: ExtractJwt.fromAuthHeaderWithScheme('JWT'),
  secretOrKey: config.get('jwtSecret'),
};

module.exports = new JwtStrategy(opts, function (jwt_payload, done) {
  User.findById(jwt_payload.id, function (err, user) {
    if (err) {
      return done(err, false);
    }
    if (user) {
      return done(null, user);
    } else {
      return done(null, false);
    }
  });
});
```

```js
let LocalStrategy = require('passport-local');
let User = require('../../accounts/models/user');

let opts = {
  usernameField: 'email',
  passwordField: 'password',
  passReqToCallback: true,
  session: false
};

module.exports = new LocalStrategy(opts, (req, email, password, done) => {
  User.findOne({ email: email }, (err, user) => {
    if (err) {
      return done(err);
    }
    if (!user) {
      return done('User doesn\'t exist!', false);
    }
    if (!user.checkPassword(password)) {
      return done('Incorrect password!', false);
    }
    return done(null, user);
  });
});
```

```js
const passport = require('../libs/passport');

module.exports = passport.initialize();
```

```js
exports.auth = async (ctx, next) => {
  await passport.authenticate('local', (err, user) => {
    if (user) {
      ctx.body = user.getAuthData();
    } else {
      ctx.status = 400;
      if (err) {
        ctx.body = { error: err };
      }
    }
  })(ctx, next);
};

exports.signUp = async ctx => {
  const body = ctx.request.body;
  let user = new User({
    fullName: body.fullName,
    email: body.email,
    password: body.password,
    role: 'Admin'
  });
  await user.save();
  ctx.body = user.getAuthData();
};
```