## Testing your application

### Used libraries

RSK comes with the following libraries for testing purposes:

- [Mocha](https://mochajs.org/) - Node.js and browser test runner
- [Chai](http://chaijs.com/) - Assertion library
- [Enzyme](https://github.com/airbnb/enzyme) - Testing utilities for React

You may also want to take a look at the following related packages:

- [jsdom](https://github.com/tmpvar/jsdom)
- [react-addons-test-utils](https://www.npmjs.com/package/react-addons-test-utils)

### Running tests

To test your application simply run the
[`npm test`](https://github.com/kriasoft/react-starter-kit/blob/b22b1810461cec9c53eedffe632a3ce70a6b29a3/package.json#L154)
command which will:
- recursively find all files ending with `.test.js` in your `src/` directory
- mocha execute found files

```bash
npm test
```

### Conventions

- test filenames MUST end with `test.js` or `npm test` will not be able to detect them
- test filenames SHOULD be named after the related component (e.g. create `Login.test.js` for
`Login.js` component)

### Basic example

To help you on your way RSK comes with the following
[basic test case](https://github.com/kriasoft/react-starter-kit/blob/master/src/components/App/App.test.js)
you can use as a starting point:

```js
import React from 'react';
import { expect } from 'chai';
import { shallow } from 'enzyme';
import App from './App';

describe('App', () => {

  it('renders children correctly', () => {
    const wrapper = shallow(
      <App context={{ insertCss: () => {} }}>
        <div className="child" />
      </App>
    );

    expect(wrapper.contains(<div className="child" />)).to.be.true;
  });

});
```

### React-intl example

React-intl users MUST render/wrap components inside an IntlProvider like the example below:

The example below example is a drop-in test for the RSK `Header` component:

```js
import React from 'react';
import Header from './Header';
import IntlProvider from 'react-intl';
import Navigation from '../../components/Navigation';

describe('A test suite for <Header />', () => {

  it('should contain a <Navigation/> component', () => {
    it('rendering', () => {
      const wrapper = renderIntoDocument(<IntlProvider locale="en"><Header /></IntlProvider>);
      expect(wrapper.find(Navigation)).to.have.length(1);
    });
  });

});
```

Please note that  NOT using IntlProvider will produce the following error: 

> Invariant Violation: [React Intl] Could not find required `intl` object. <IntlProvider>
> needs to exist in the component ancestry.

### Linting

Running RSK eslint will also scan your test files:

```bash
npm run eslint
```

