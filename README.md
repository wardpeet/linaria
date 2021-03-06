<p align="center">
  <img alt="Linaria" src="website/assets/linaria-logo@2x.png" width="496">
</p>

<p align="center">
Zero-runtime CSS in JS library.
</p>

---

[![Build Status][build-badge]][build]
[![Code Coverage][coverage-badge]][coverage]
[![Version][version-badge]][package]
[![MIT License][license-badge]][license]

[![All Contributors][all-contributors-badge]](#contributors)
[![PRs Welcome][prs-welcome-badge]][prs-welcome]
[![Chat][chat-badge]][chat]
[![Code of Conduct][coc-badge]][coc]

[![tweet][tweet-badge]][tweet]

## Features

- Write CSS in JS, but with **zero runtime**, CSS is extracted to CSS files during build
- Familiar **CSS syntax** with Sass like nesting
- Use **dynamic prop based styles** with the React bindings, uses CSS variables behind the scenes
- Easily find where the style was defined with **CSS sourcemaps**
- **Lint your CSS** in JS with [stylelint](https://github.com/stylelint/stylelint)
- Use **JavaScript for logic**, no CSS preprocessor needed

**[Why use Linaria](/docs/BENEFITS.md)**

## Installation

```sh
npm install linaria
```

or

```sh
yarn add linaria
```

## Setup

Linaria currently supports webpack and Rollup to extract the CSS at build time. See [Bundlers integration](/docs/BUNDLERS_INTEGRATION.md) to configure your bundler.

Optionally, add the `linaria/babel` preset to your Babel configuration at the end of the presets list to avoid errors when importing the components in your server code or tests:

```json
{
  "presets": [
    "@babel/preset-env",
    "@babel/preset-react",
    "linaria/babel"
  ]
}
```

See [Configuration](/docs/CONFIGURATION.md) to customize how Linaria processes your files.

## Syntax

Linaria can be used with any framework, with additional helpers for React. The basic syntax looks like this:

```js
import { css } from 'linaria';
import { modularScale, hiDPI } from 'polished';
import fonts from './fonts';

// Write your styles in `css` tag
const header = css`
  text-transform: uppercase;
  font-family: ${fonts.heading};
  font-size: ${modularScale(2)};

  ${hiDPI(1.5)} {
    font-size: ${modularScale(2.5)};
  }
`;

// Then use it as a class name
<h1 class={header}>Hello world</h1>;
```

You can use imported variables and functions for logic inside the CSS code. They will be evaluated at build time.

If you're using [React](https://reactjs.org/), you can use the `styled` helper, which makes it easy to write React components with dynamic styles with a styled-component like syntax:

```js
import { styled } from 'linaria/react';
import { families, sizes } from './fonts';

// Write your styles in `styled` tag
const Title = styled.h1`
  font-family: ${families.serif};
`;

const Container = styled.div`
  font-size: ${sizes.medium}px;
  color: ${props => props.color};
  border: 1px solid red;

  &:hover {
    border-color: blue;
  }

  ${Title} {
    margin-bottom: 24px;
  }
`;

// Then use the resulting component
<Container color="#333">
  <Title>Hello world</Title>
</Container>;
```

Dynamic styles will be applied using CSS custom properties (aka CSS variables) and don't require any runtime.

## Documentation

- [API and usage](/docs/API.md)
  - [Client APIs](/docs/API.md#client-apis)
  - [Server APIs](/docs/API.md#server-apis)
- [Configuration](/docs/CONFIGURATION.md)
- [Dynamic styles with `css` tag](/docs/DYNAMIC_STYLES.md)
- [Theming](/docs/THEMING.md)
- [Critical CSS extraction](/docs/CRITICAL_CSS.md)
- [Bundlers integration](/docs/BUNDLERS_INTEGRATION.md)
  - [Webpack](/docs/BUNDLERS_INTEGRATION.md#webpack)
  - [Rollup](/docs/BUNDLERS_INTEGRATION.md#rollup)
- [CLI](/docs/CLI.md)
- [Linting](/docs/LINTING.md)
- [How it works](/docs/HOW_IT_WORKS.md)
- [Example](/website)

## Trade-offs

- No IE11 support when using dynamic styles in components with `styled`, since it uses CSS custom properties
- Dynamic styles are not supported with `css` tag. See [Dynamic styles with `css` tag](/docs/DYNAMIC_STYLES.md) for alternative approaches.
- Modules used in the CSS rules cannot have side-effects.
  For example:

  ```js
  import { css } from 'linaria';
  import colors from './colors';

  const title = css`
    color: ${colors.text};
  `;
  ```

  Here, there should be no side-effects in the `colors.js` file, or any file it imports. We recommend to move helpers and shared configuration to files without any side-effects.

## Editor Plugins

### VSCode

- Syntax Highlighting - [language-babel](https://marketplace.visualstudio.com/items?itemName=mgmcdermott.vscode-language-babel)
- Autocompletion - [vscode-styled-components](https://marketplace.visualstudio.com/items?itemName=jpoissonnier.vscode-styled-components)
- Linting - [stylelint](https://marketplace.visualstudio.com/items?itemName=shinnn.stylelint)

### Atom

- Syntax Highlighting and Autocompletion - [language-babel](https://atom.io/packages/language-babel)

## Recommended Libraries

- [linaria-jest](https://github.com/thymikee/linaria-jest) – Jest testing utilities for Linaria.
- [gatsby-plugin-linaria](https://github.com/silvenon/gatsby-plugin-linaria) – Gatsby plugin that sets up Babel and webpack configuration for Linaria.
- [polished.js](https://polished.js.org/) - A lightweight toolset for writing styles in JavaScript.

## Inspiration

- [glam](https://github.com/threepointone/glam)
- [styled-components](https://github.com/styled-components/styled-components)
- [css-literal-loader](https://github.com/4Catalyzer/css-literal-loader)

## Acknowledgements

This project wouldn't have been possible without the following libraries or the people behind them.

- [babel](https://babeljs.io/)
- [stylis.js](https://github.com/thysultan/stylis.js)

Special thanks to [@kentcdodds](https://github.com/kentcdodds) for his babel plugin and [@threepointone](https://github.com/threepointone) for his suggestions and encouragement.

## Contributors

Thanks goes to these wonderful people ([emoji key](https://github.com/kentcdodds/all-contributors#emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
| [<img src="https://avatars2.githubusercontent.com/u/17573635?v=4" width="100px;"/><br /><sub>Paweł Trysła</sub>](https://twitter.com/_zamotany)<br />[💻](https://github.com/satya164/linara/commits?author=zamotany "Code") [📖](https://github.com/satya164/linara/commits?author=zamotany "Documentation") [🤔](#ideas-zamotany "Ideas, Planning, & Feedback") |      [<img src="https://avatars2.githubusercontent.com/u/1174278?v=4" width="100px;"/><br /><sub>Satyajit Sahoo</sub>](https://medium.com/@satya164)<br />[💻](https://github.com/satya164/linara/commits?author=satya164 "Code") [🤔](#ideas-satya164 "Ideas, Planning, & Feedback")       | [<img src="https://avatars2.githubusercontent.com/u/5106466?v=4" width="100px;"/><br /><sub>Michał Pierzchała</sub>](https://github.com/thymikee)<br />[💻](https://github.com/satya164/linara/commits?author=thymikee "Code") [📖](https://github.com/satya164/linara/commits?author=thymikee "Documentation") [🤔](#ideas-thymikee "Ideas, Planning, & Feedback") |                                             [<img src="https://avatars1.githubusercontent.com/u/1909761?v=4" width="100px;"/><br /><sub>Lucas</sub>](https://lcs.sh)<br />[📖](https://github.com/satya164/linara/commits?author=AgtLucas "Documentation")                                              | [<img src="https://avatars0.githubusercontent.com/u/680439?v=4" width="100px;"/><br /><sub>Alexey Pronevich</sub>](https://github.com/pronevich)<br />[📖](https://github.com/satya164/linara/commits?author=pronevich "Documentation") | [<img src="https://avatars3.githubusercontent.com/u/18573330?v=4" width="100px;"/><br /><sub>Wojtek Szafraniec</sub>](https://github.com/wojteg1337)<br />[💻](https://github.com/satya164/linara/commits?author=wojteg1337 "Code") | [<img src="https://avatars1.githubusercontent.com/u/1854763?v=4" width="100px;"/><br /><sub>Tushar Sonawane</sub>](https://twitter.com/tushkiz)<br />[📖](https://github.com/satya164/linara/commits?author=Tushkiz "Documentation") [💡](#example-Tushkiz "Examples") |
| :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|                                                                 [<img src="https://avatars2.githubusercontent.com/u/774577?v=4" width="100px;"/><br /><sub>Ferran Negre</sub>](http://twitter.com/ferrannp)<br />[📖](https://github.com/satya164/linara/commits?author=ferrannp "Documentation")                                                                 | [<img src="https://avatars3.githubusercontent.com/u/8135252?v=4" width="100px;"/><br /><sub>Jakub Beneš</sub>](https://jukben.cz)<br />[💻](https://github.com/satya164/linara/commits?author=jukben "Code") [📖](https://github.com/satya164/linara/commits?author=jukben "Documentation") |                                  [<img src="https://avatars2.githubusercontent.com/u/13413409?v=4" width="100px;"/><br /><sub>Oscar Busk</sub>](https://github.com/oBusk)<br />[🐛](https://github.com/satya164/linara/issues?q=author%3AoBusk "Bug reports") [💻](https://github.com/satya164/linara/commits?author=oBusk "Code")                                  | [<img src="https://avatars3.githubusercontent.com/u/18584155?v=4" width="100px;"/><br /><sub>Dawid</sub>](https://github.com/Trancever)<br />[💻](https://github.com/satya164/linara/commits?author=Trancever "Code") [📖](https://github.com/satya164/linara/commits?author=Trancever "Documentation") |
<!-- ALL-CONTRIBUTORS-LIST:END -->

This project follows the [all-contributors](https://github.com/kentcdodds/all-contributors) specification. Contributions of any kind welcome!

<!-- badges -->
[build-badge]: https://img.shields.io/circleci/project/github/callstack/linaria/master.svg?style=flat-square
[build]: https://circleci.com/gh/callstack/linaria
[coverage-badge]: https://img.shields.io/codecov/c/github/callstack/linaria.svg?style=flat-square
[coverage]: https://codecov.io/github/callstack/linaria
[version-badge]: https://img.shields.io/npm/v/linaria.svg?style=flat-square
[package]: https://www.npmjs.com/package/linaria
[license-badge]: https://img.shields.io/npm/l/linaria.svg?style=flat-square
[license]: https://opensource.org/licenses/MIT
[prs-welcome-badge]: https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square
[prs-welcome]: http://makeapullrequest.com
[coc-badge]: https://img.shields.io/badge/code%20of-conduct-ff69b4.svg?style=flat-square
[coc]: https://github.com/callstack/linaria/blob/master/CODE_OF_CONDUCT.md
[all-contributors-badge]: https://img.shields.io/badge/all_contributors-11-orange.svg?style=flat-square
[chat-badge]: https://img.shields.io/discord/426714625279524876.svg?style=flat-square&colorB=758ED3
[chat]: https://discord.gg/zwR2Cdh
[tweet-badge]: https://img.shields.io/badge/tweet-%23linaria-blue.svg?style=flat-square&colorB=1DA1F2&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAUCAYAAACXtf2DAAAAAXNSR0IArs4c6QAAAaRJREFUOBGtlM8rBGEYx3cWtRHJRaKcuMtBSitxkCQ3LtzkP9iUUu5ODspRHLhRLtq0FxeicEBC2cOivcge%2FMgan3fNM8bbzL4zm6c%2BPT%2Fe7%2FO8887svrFYBWbbtgWzsAt3sAcpqJFxxF1QV8oJFqFPFst5dLWQAT87oTgPB7DtziFRT1EA4yZolsFkhwjGYFRO8Op0KD8HVe7unoB6PRTBZG8IctAmG1xrHcfkQ2B55sfI%2ByGMXSBqV71xZ8CWdxBxN6ThFuECDEAL%2Bc9HIzDYumVZ966GZnX0SzCZvEqTbkaGywkyFE6hKAsBPhFQ18uPUqh2ggJ%2BUor%2F4M%2F%2FzOC8g6YzR1i%2F8g4vvSI%2ByD7FFNjexQrjHd8%2BnjABI3AU4Wl16TuF1qANGll81jsi5qu%2Bw6XIsCn4ijhU5FmCJpkV6BGNw410hfSf6JKBQ%2FUFxHGYBnWnmOwDwYQ%2BwzdHqO75HtiAMJfaC7ph32FSRJCENUhDHsLaJkL%2FX4wMF4%2BwA5bgAcrZE4sr0Cu9Jq9fxyrvBHWbNkMD5CEHWTjjT2m6r5D92jfmbbKJEWuMMAAAAABJRU5ErkJggg%3D%3D
[tweet]: https://twitter.com/intent/tweet?text=Check%20out%20linaria!%20https://github.com/callstack/linaria%20%F0%9F%91%8D
