# Lecture 23

### Software testing

**Definition**
- Check a specific part of code(or project) for the expected result.

**Purposes**
- Quality control
- Analysis
- Work with different circumstances
- Compliance with requirements
- Versioning

### Software quality
- Perfomance
- Compatibility
- Convenience of use
- Reliability
- Security
- Accompanyability
- Portability
- Modifiability
- Functional suitability

### Testing types
- By test object
  - Functional
  - Perfomance (load, stress, stability)
  - Usability (UX)
  - Interface (UI)
  - Localization
  - Security
- According to the available information about the object
  - Black box
  - White box
  - Grey box
- According to the automation process
  - Automated
  - Manual
  - Semi-automated
- According to the isolation of object
  - Module
  - Integration
  - System
- By time
  - Alpha
  - Beta
  - Gamma

### Code coverage
- https://github.com/dwyl/hapi-auth-jwt2

### TDD, Test-driven development
> Test -> Code -> Refactor

### KISS
> Keep it simple, stupid

### YAGNI
> You aren't gonna need it

### Fixtures
Test data for unit-testing:
- data in database
- data in specific files (e.g. json or xml)

### 💩
- https://github.com/AceLewis/my_first_calculator.py/blob/master/my_first_calculator.py
- https://github.com/asweigart/my_first_tic_tac_toe/blob/master/tictactoe.py

### Testing Node.js app
- Test runner
- Assertion library

**Test runners:**
- Mocha
- Jest
- Jasmine
- Karma
- Ava

**Assertion libs:**
- Chai
- Expect
- Supertest

### Mocha & Chai
```js
const chai = require('chai');
const chaiHttp = require('chai-http');
const fs = require('fs');
const app = require('../../app');

chai.should();
chai.use(chaiHttp);


describe('Accounts', () => {
  it('Should login user and return his auth data', (done) => {
    chai.request(app)
      .post('/api/accounts/sign-in')
      .send({
        email: 'antonboksha@gmail.com',
        password: 'testpass',
      })
      .end((err, res) => {
        res.should.have.status(200);
        res.body.should.have.property('user').that.have.keys(['fullName', 'email', 'photo']);
        res.body.should.have.property('token');
        done();
      });
  });

  it('Should upload user photo and return url', (done) => {
    chai.request(app)
      .put('/api/accounts/photo')
      .attach('photo', fs.readFileSync('cage.jpg'), 'cage.jpg')
      .end((err, res) => {
        res.should.have.status(200);
        done();
      });
  });
});

```

```json
"test": "mocha ./src/tests/*.test.js --timeout 10000 --exit",
"coverage": "nyc npm run test",
"coverage-report": "nyc report --reporter=html"
```