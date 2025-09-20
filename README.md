<img align="center" src="https://i.imgur.com/ZgHWFhw.png" alt="gabriellugo" />

# OWASP PASSWORD STRENGHT TEST

<a href="https://github.com/GabrielLugooo/Owasp-Pass-Test/tree/main" target="_blank" rel="noreferrer noopener"> <img align="center" src="https://img.shields.io/badge/English%20OWASP-000000" alt="English OWASP" /></a>
<a href="https://github.com/GabrielLugooo/Owasp-Pass-Test/blob/main/README%20Spanish.md" target="_blank" rel="noreferrer noopener"> <img align="center" src="https://img.shields.io/badge/Spanish%20OWASP-green" alt="Spanish OWASP" /></a>

### Objective

OWASP Password Strenght Test is a password-strength tester based off of the <a href="https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html#Implement_Proper_Password_Strength_Controls" target="_blank" rel="noreferrer noopener">OWASP Guidelines for enforcing secure passwords</a>. It is lightweight, extensible, has no dependencies, and can be used on the server (nodejs) or in-browser.

OWASP Password Strenght Test is not an OWASP project, it is merely based off of OWASP research.

### Skills Learned

- Understanding of OWASP guidelines for authentication and enforcement of passwords.
- Proficiency in analyzing and interpreting node.js, Jason and Yaml.
- Ability to generate and recognize signatures and patterns in Authentication, digital identtity, identtity proofing and session management.
- Enhanced knowledge of network protocols and security vulnerabilities.
- Development of critical thinking and problem-solving skills in cybersecurity.

### Tools Used

![Static Badge](https://img.shields.io/badge/OWASP-000000?logo=owasp&logoSize=auto)
![Static Badge](https://img.shields.io/badge/HTML-000000?logo=html5&logoSize=auto)
![Static Badge](https://img.shields.io/badge/Javascript-000000?logo=javascript&logoSize=auto)
![Static Badge](https://img.shields.io/badge/Node.JS-000000?logo=nodedotjs&logoSize=auto)
![Static Badge](https://img.shields.io/badge/Json-000000?logo=json&logoSize=auto)
![Static Badge](https://img.shields.io/badge/YAML-000000?logo=yaml&logoSize=auto)
![Static Badge](https://img.shields.io/badge/Travis-000000?logo=travis&logoSize=auto)

- OWASP guidelines
- HTML5 & Javascript
- Node.js
- Jason
- YAML
- Travis

### Installing

- #### Server-side (node.js)
  From the command line:

```sh
npm install owasp-password-strength-test
```

- #### In-browser
  Within your document:

```html
<script src="owasp-password-strength-test.js"></script>
```

### Features

This module is built upon the following beliefs:

1. <a href="https://xkcd.com/936/" target="_blank" rel="noreferrer noopener">Passphrases are better than passwords</a>

2. Passwords should be subject to stricter complexity requirements than passphrases.

Thus, the module:

- **provides for "required" and "optional" tests**.
  In order to be considered "strong", a password must pass _all_ required tests, as well as a
  configurable number of optional tests. This makes it possible to always enforce certain rules (like minimum password length), while giving users
  flexibility to honor only some of a pool of lower-priority rules.

- **encourages the use of passphrases over passwords**.
  Passphrases (by default) are not subject to the same complexity requirements as a password.
  (Whereby, by default, a "passphrase" can be defined as "a password whose length is greater than or equal to 20 characters.")

- **can be arbitrarily extended**
  As-needed with additional required and optional tests.

### Usage

After you've included it into your project, using the module is straightforward:

- #### Server-side

```javascript
// require the module
var owasp = require("owasp-password-strength-test");

// invoke test() to test the strength of a password
var result = owasp.test("correct horse battery staple");
```

- #### In Browser

```javascript
// in the browser, including the script will make a
// `window.owaspPasswordStrengthTest` object available.
var result = owaspPasswordStrengthTest.test("correct horse battery staple");
```

The returned value will take this shape when the password is valid:

```javascript
{
  errors              : [],
  failedTests         : [],
  requiredTestErrors  : [],
  optionalTestErrors  : [],
  passedTests         : [ 0, 1, 2, 3, 4, 5, 6 ],
  isPassphrase        : false,
  strong              : true,
  optionalTestsPassed : 4
}
```

and will take this shape when the password is invalid:

```javascript
{
  errors: [
      'The password must be at least 10 characters long.',
      'The password must contain at least one uppercase letter.',
      'The password must contain at least one number.',
      'The password must contain at least one special character.'
    ],
    failedTests         : [ 0, 4, 5, 6 ],
    passedTests         : [ 1, 2, 3 ],
    requiredTestErrors  : [
      'The password must be at least 10 characters long.',
    ],
    optionalTestErrors  : [
      'The password must contain at least one uppercase letter.',
      'The password must contain at least one number.',
      'The password must contain at least one special character.'
    ],
    isPassphrase        : false,
    strong              : false,
    optionalTestsPassed : 1
}
```

Whereby:

- `errors` is an `array` of `string`s of error messages associated with the failed tests.

- `failedTests` enumerates which tests have failed, beginning from 0 with the first required test

- `passedTests` enumerates which tests have succeeded, beginning from 0 with the first required test

- `requiredTestErrors` is an array containing the error messages of required tests that have failed.

- `optionalTestErrors` is an array containing the error messages of optional tests that have failed.

- `isPassphrase` is a `boolean` indicating whether or not the password was considered to be a passphrase.

- `strong` is a `boolean` indicating whether or not the user's password satisfied the strength requirements.

- `optionalTestsPassed` is a `number` indicating how many of the optional tests were passed.
  In order for the password to be considered "strong", it (by default) must either be a passphrase,
  or must pass a number of optional tests that is equal to or greater than `configs.minOptionalTestsToPass`.

### Configuring

The module may be configured as follows:

```javascript
var owasp = require("owasp-password-strength-test");

// Pass a hash of settings to the `config` method. The settings shown here are
// the defaults.
owasp.config({
  allowPassphrases: true,
  maxLength: 128,
  minLength: 10,
  minPhraseLength: 20,
  minOptionalTestsToPass: 4,
});
```

Whereby:

- `allowPassphrases` is a `boolean` that toggles the "passphrase" mechanism on and off.
  If set to `false`, the strength-checker will abandon the notion of "passphrases", and will subject all passwords to the same complexity requirements.

- `maxLength` is a constraint on a password's maximum length.

- `minLength` is a constraint on a password's minimum length.

- `minPhraseLength` is the minimum length a password needs to achieve in order to be considered a "passphrase" (and thus exempted from the optional complexity tests by default).

- `minOptionalTestsToPass` is the minimum number of optional tests that a password must pass in order to be considered "strong".
  By default (per the OWASP guidelines), four optional complexity tests are made, and a password must pass at least three of them in order to be considered "strong".

### Extending

If you would like to filter passwords through additional tests beyond the default, you may simply push new tests onto the appropriate arrays within the module's `test` object:

```javascript
var owasp = require("owasp-password-strength-test");

// push "required" tests onto `tests.required` array, and push "optional" tests
// onto the `tests.optional` array.
owasp.tests.required.push(function (password) {
  if (password === "one two three four five") {
    return "That's the kind of thing an idiot would have on his luggage!";
  }
});
```

Test functions must resemble the following:

```javascript
// accept the password as the single argument
function(password) {

  // the "if" conditional should evaluate to `true` if the password is bad
  if (thePasswordIsBad) {

    // On password failure, a string should be returned. It will be pushed
    // onto an array of errors associated with the password.
    return "This is the failure message associated with the test";
  }

  // if the password is OK, nothing should be returned
}
```

### Testing

To run the module's test suite, `cd` into its directory and run `npm test`.
You may first need to run `npm install` to install the required development dependencies. (These dependencies are **not** required in a production environment, and facilitate only unit testing.)

### Limitations

OWASP Password Strenght Test is a copycat of <a href="https://github.com/nowsecure/owasp-password-strength-test" target="_blank" rel="noreferrer noopener">NOWSECURE</a> and it's just for educational purpose under the MIT License.

---

<h3 align="left">Connect with me</h3>

<p align="left">
<a href="https://www.youtube.com/@gabriellugooo" target="_blank" rel="noreferrer noopener"> <img align="center" src="https://img.icons8.com/?size=50&id=55200&format=png" alt="@gabriellugooo" height="40" width="40" /></a>
<a href="http://www.tiktok.com/@gabriellugooo" target="_blank" rel="noreferrer noopener"> <img align="center" src="https://img.icons8.com/?size=50&id=118638&format=png" alt="@gabriellugooo" height="40" width="40" /></a>
<a href="https://instagram.com/lugooogabriel" target="_blank" rel="noreferrer noopener"> <img align="center" src="https://img.icons8.com/?size=50&id=32309&format=png" alt="lugooogabriel" height="40" width="40" /></a>
<a href="https://twitter.com/gabriellugo__" target="_blank" rel="noreferrer noopener"> <img align="center" src="https://img.icons8.com/?size=50&id=phOKFKYpe00C&format=png" alt="gabriellugo__" height="40" width="40" /></a>
<a href="https://www.linkedin.com/in/hernando-gabriel-lugo" target="_blank" rel="noreferrer noopener"> <img align="center" src="https://img.icons8.com/?size=50&id=8808&format=png" alt="hernando-gabriel-lugo" height="40" width="40" /></a>
<a href="https://github.com/GabrielLugooo" target="_blank" rel="noreferrer noopener"> <img align="center" src="https://img.icons8.com/?size=80&id=AngkmzgE6d3E&format=png" alt="gabriellugooo" height="34" width="34" /></a>
<a href="mailto:lugohernandogabriel@gmail.com"> <img align="center" src="https://img.icons8.com/?size=50&id=38036&format=png" alt="lugohernandogabriel@gmail.com" height="40" width="40" /></a>
<a href="https://linktr.ee/gabriellugooo" target="_blank" rel="noreferrer noopener"> <img align="center" src="https://simpleicons.org/icons/linktree.svg" alt="gabriellugooo" height="40" width="40" /></a>
</p>

<p align="left">
<a href="https://github.com/GabrielLugooo/GabrielLugooo/blob/main/README.md" target="_blank" rel="noreferrer noopener"> <img align="center" src="https://img.shields.io/badge/English%20Version-000000" alt="English Version" /></a>
<a href="https://github.com/GabrielLugooo/GabrielLugooo/blob/main/Readme%20Spanish.md" target="_blank" rel="noreferrer noopener"> <img align="center" src="https://img.shields.io/badge/Spanish%20Version-Green" alt="Spanish Version" /></a>
</p>

<a href="https://linktr.ee/gabriellugooo" target="_blank" rel="noreferrer noopener"> <img align="center" src="https://img.shields.io/badge/Credits-Gabriel%20Lugo-green" alt="Credits" /></a>
<img align="center" src="https://komarev.com/ghpvc/?username=GabrielLugoo&label=Profile%20views&color=green&base=2000" alt="GabrielLugooo" />
<a href="" target="_blank" rel="noreferrer noopener"> <img align="center" src="https://img.shields.io/badge/License-MIT-green" alt="MIT License" /></a>
