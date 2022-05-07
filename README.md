# joi-ko v1.0.0

[![NPM Version][npm-image]][npm-url]
[![NPM Downloads][downloads-image]][downloads-url]


## Description

- [danieluhm2004님의 joi-ko.js gist](https://gist.github.com/danieluhm2004/e8106b950a9773490d0cf2a251dd400d) 의 번역문을 기준으로 '(은)는' 삭제 수정 및 패키지화
- joi 응답메세지를 한국어로 출력합니다. 나머지 사용법은 동일합니다.
- 추가 번역이 필요한 부분은 PR 부탁드립니다.

## Installation

```console
$ npm install joi-ko --save
```


## Usage

```js
const Joi = require('joi-ko');

const schema = Joi.object({
    username: Joi.string()
        .alphanum()
        .min(3)
        .max(30)
        .required(),

    password: Joi.string()
        .pattern(new RegExp('^[a-zA-Z0-9]{3,30}$')),

    repeat_password: Joi.ref('password'),

    access_token: [
        Joi.string(),
        Joi.number()
    ],

    birth_year: Joi.number()
        .integer()
        .min(1900)
        .max(2013),

    email: Joi.string()
        .email({ minDomainSegments: 2, tlds: { allow: ['com', 'net'] } })
})
    .with('username', 'birth_year')
    .xor('password', 'access_token')
    .with('password', 'repeat_password');


schema.validate({ username: 'abc', birth_year: 1994 });
// -> { value: { username: 'abc', birth_year: 1994 } }

schema.validate({});
// -> { value: {}, error: '"username" is required' }

// Also -

try {
    const value = await schema.validateAsync({ username: 'abc', birth_year: 1994 });
}
catch (err) { }
```

## License

[MIT](LICENSE)

[npm-image]: https://img.shields.io/npm/v/joi-ko.svg
[npm-url]: https://npmjs.org/package/joi-ko
[downloads-image]: https://img.shields.io/npm/dm/joi-ko.svg
[downloads-url]: https://npmjs.org/package/joi-ko
