# @ngx-prism/core

[![npm version](https://badge.fury.io/js/%40ngx-prism%2Fcore.svg)](https://badge.fury.io/js/%40ngx-prism%2Fcore)
[![GitHub version](https://badge.fury.io/gh/ngx-prism%2Fcore.svg)](https://badge.fury.io/gh/ngx-prism%2Fcore)
[![Build Status](https://travis-ci.org/ngx-prism/core.svg?branch=master)](https://travis-ci.org/ngx-prism/core)
[![Known Vulnerabilities](https://snyk.io/test/github/ngx-prism/core/badge.svg)](https://snyk.io/test/github/ngx-prism/core)

[![GitHub issues](https://img.shields.io/github/issues/ngx-prism/core.svg)](https://github.com/ngx-prism/core/issues)
[![GitHub forks](https://img.shields.io/github/forks/ngx-prism/core.svg)](https://github.com/ngx-prism/core/network)
[![GitHub stars](https://img.shields.io/github/stars/ngx-prism/core.svg)](https://github.com/ngx-prism/core/stargazers)
[![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/ngx-prism/core/master/LICENSE)

Simple Angular 2+ Prism highlighter module. It uses `highElement()` prismjs method to highlight code.

Here is [@ngx-prism/rxjs](https://github.com/ngx-prism/rxjs) with rxjs.

----

* [Demonstration](#demonstration)
* [Installation](#installation)
* [Usage](#usage)
* [Attributes](#attributes)
* [Lifecycle Hooks](#lifecycle-hooks)
* [Scripts](#scripts)
* [Git](#git)
  * [Commit](#commit)
  * [Versioning](#versioning)
* [License](#license)
* [Donate](#donate)

----


## Demonstration

Get simple example demonstration usage from github [repository](https://github.com/ngx-prism/demo) by opening your command line and do the following:

```bash
git clone https://github.com/ngx-prism/demo.git
cd demo
npm install && npm start
```

Open http://localhost:4200/ in your browser.

## Installation

To install, run:

```bash
npm install @ngx-prism/core --save
```

## Usage

It is designed to use `ng-content` and property `code` separately. You should **NOT** use both the same time.

1. Import `PrismModule` into your module.

```typescript
// example.module.ts
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';

import { PrismModule } from '@ngx-prism/core';
import { ExampleComponent } from './example.component';

@NgModule({
  declarations: [ ExampleComponent ],
  imports: [ CommonModule, PrismModule ],
  exports: [ ExampleComponent ]
})
export class ExampleModule { }
```

2. Use prism component in your example component.

```typescript
// example.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'example-component',
  template: `
    <prism-highlight [language]="language">
      {{content}}
    </prism-highlight>
  `
})
export class ExampleComponent {
  language = 'html';
  content = '<p>test</p>';
  constructor() { }
}
```

Use `PrismComponent` by providing `code` and `interpolation` property in `ExampleComponent`.

```typescript
// example.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'example-component',
  template: `
    <prism-highlight
      [language] = "language"
      [hooks] = "hooks"
      [code] = "content"
      [interpolation] = "interpolate"
    ></prism-highlight>`
})
export class ExampleComponent {
  content = '<p>test {{language}}</p>';
  hooks = {
    'before-sanity-check': (env) => { console.log(`before-sanity-check`, env); },
    'before-highlight': (env) => { console.log(`before-highlight`, env); },
    'after-highlight': (env) => { console.log(`after-highlight`, env); },
    'complete': (env) => { console.log(`complete`, env); },
    'before-insert': (env) => { console.log(`before-insert`, env); }
  };
  interpolate = {
    language: 'language interpolated'
  };
  language = 'html';
  constructor() { }
}
```

* It is possible to import themes files in `@angular/cli` like below.

```css
@import '~@ngx-prism/core/dist/themes/prism-coy.css';
@import '~@ngx-prism/core/dist/themes/prism-dark.css';
@import '~@ngx-prism/core/dist/themes/prism-funky.css';
@import '~@ngx-prism/core/dist/themes/prism-okaidia.css';
@import '~@ngx-prism/core/dist/themes/prism-solarizedlight.css';
@import '~@ngx-prism/core/dist/themes/prism-tomorrow.css';
@import '~@ngx-prism/core/dist/themes/prism-twilight.css';
@import '~@ngx-prism/core/dist/themes/prism.css';
```

### Attributes

| name | Type | Description |
|----------|----------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| async | boolean | Works only with `ng-content`. *"Whether to use Web Workers to improve performance and avoid blocking the UI when highlighting very large chunks of code."* - prismjs |
| callback | (element: Element) => void \| undefined = undefined | *"An optional callback to be invoked after the highlighting is done. Mostly useful when async is true, since in that case, the highlighting is done asynchronously."* - prismjs  |
| code | string | *"A string with the code to be highlighted."* - prismjs |
| **hooks** | Object | Callback with specific execute time and name: `before-sanity-check`, `before-highlight`, `after-highlight`, `complete`, `before-insert`. |
| **interpolation** | Object \| undefined | Data property values to inject.  |
| language | string | *"Valid language identifier, for example 'javascript', 'css'."* - prismjs |


### Lifecycle Hooks

[Angular Lifecycle Hooks](https://angular.io/guide/lifecycle-hooks)

**ngAfterViewChecked()**: Performs `highlightElement(element, async, callback)` prismjs method when property `change` value is set to `true`.

**ngOnChanges()**: Detect input property `code` or `language` changes by comparing `currentValue` to `previousValue`. If yes, set component property `change` to `true`.    

## Scripts

Clone repository:

```bash
git clone https://github.com/ngx-prism/core.git
```

Go to just created folder:

```bash
cd core
```

To build a clean package, means before that script removes node_modules, dist folder and install dependencies:

```bash
npm run start:clean
```

To build a package:

```bash
npm start
```

To run karma tests:

```bash
npm test
```

## GIT

### Commit

- [AngularJS Git Commit Message Conventions](https://gist.github.com/stephenparish/9941e89d80e2bc58a153)   
- [Karma Git Commit Msg](http://karma-runner.github.io/0.10/dev/git-commit-msg.html)

### Versioning

[Semantic Versioning 2.0.0](http://semver.org/)

**Given a version number MAJOR.MINOR.PATCH, increment the:**  
MAJOR version when you make incompatible API changes,  
MINOR version when you add functionality in a backwards-compatible manner, and  
PATCH version when you make backwards-compatible bug fixes.

Additional labels for pre-release and build metadata are available as extensions to the MAJOR.MINOR.PATCH format.   

**FAQ**
How should I deal with revisions in the 0.y.z initial development phase?
>The simplest thing to do is start your initial development release at 0.1.0 and then increment the minor version for each subsequent release.

How do I know when to release 1.0.0?

>If your software is being used in production, it should probably already be 1.0.0. If you have a stable API on which users have come to depend, you should be 1.0.0. If you’re worrying a lot about backwards compatibility, you should probably already be 1.0.0.

## License

MIT © ngx-prism

## Donate

[Click to donate](https://donorbox.org/help-creating-open-source-software)
