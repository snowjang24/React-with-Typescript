# Basic 05ae09835b4e44228b65f3e9bdfef365

## Basic

Created: Sep 26, 2020 1:41 PM

## 0. [Setup](https://react-typescript-cheatsheet.netlify.app/docs/basic/setup)

### [전제조건](https://react-typescript-cheatsheet.netlify.app/docs/basic/setup#prerequisites)

1. good understanding of [React](https://reactjs.org/)
2. familiarity with [TypeScript Types](https://www.typescriptlang.org/docs/handbook/basic-types.html) \([2ality's guide](http://2ality.com/2018/04/type-notation-typescript.html) is helpful. If you’re an absolute beginner in TypeScript, check out [chibicode’s tutorial](https://ts.chibicode.com/todo/).\)
3. having read [the TypeScript section in the official React docs](https://reactjs.org/docs/static-type-checking.html#typescript).
4. having read [the React section of the new TypeScript playground](http://www.typescriptlang.org/play/index.html?jsx=2&esModuleInterop=true&e=181#example/typescript-with-react) \(optional: also step through the 40+ examples under [the playground's](http://www.typescriptlang.org/play/index.html) Examples section\)

This guide will always assume you are starting with the latest TypeScript version. Notes for older versions will be in expandable `<details>` tags.

### [React + TypeScript Starter Kits](https://react-typescript-cheatsheet.netlify.app/docs/basic/setup/#react--typescript-starter-kits)

1. [Create React App v2.1+ with TypeScript](https://facebook.github.io/create-react-app/docs/adding-typescript): `npx create-react-app my-app --template typescript`
2. We used to recommend `create-react-app-typescript` but it is now [deprecated](https://www.reddit.com/r/reactjs/comments/a5919a/createreactapptypescript_has_been_archived_rip/). [see migration instructions](https://vincenttunru.com/migrate-create-react-app-typescript-to-create-react-app/)
3. [Basarat's guide](https://github.com/basarat/typescript-react/tree/master/01%20bootstrap) for **manual setup** of React + TypeScript + Webpack + Babel
4. In particular, make sure that you have `@types/react` and `@types/react-dom` installed \([Read more about the DefinitelyTyped project if you are unfamiliar](https://definitelytyped.org/)\)
5. There are also many React + TypeScript boilerplates, please see [our Resources list below](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet#recommended-react--typescript-codebases-to-learn-from).

### [Import React](https://react-typescript-cheatsheet.netlify.app/docs/basic/setup/#import-react)

```jsx
import * as React from "react";
import * as ReactDOM from "react-dom";
```

In [TypeScript 2.7+](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-7.html), you can run TypeScript with `-allowSyntheticDefaultImports` \(or add `"allowSyntheticDefaultImports": true` to tsconfig\) to import like in regular jsx:

```jsx
import React from "react";
import ReactDOM from "react-dom";
```

Why `allowSyntheticDefaultImports` over `esModuleInterop`? [Daniel Rosenwasser](https://twitter.com/drosenwasser/status/1003097042653073408) has said that it's better for webpack/parcel. For more discussion check out [https://github.com/wmonk/create-react-app-typescript/issues/214](https://github.com/wmonk/create-react-app-typescript/issues/214)You should also check [the new TypeScript docs for official descriptions between each compiler flag](https://www.typescriptlang.org/v2/en/tsconfig#allowSyntheticDefaultImports)!

## 1. Getting Started

### 1.1 [Function Components](https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-started/function_components)

#### 1.1.1 Normal Function Component

함수형 컴포넌트는 `type`혹은 `interface`를 이용하여 해당 컴포넌트의 타입을 선언하고 인자\(`props`\)의 타입으로 할당하면 됩니다.

```jsx
type AppProps = {
  message: string;
}; 
/* could also use interface */
// interface AppProps {
//   message: string;
// }
const App = ({ message }: AppProps) => <div>{message}</div>;
```

#### 1.1.2 FC / FunctionComponent / VoidFunctionComponent

`React.FunctionComponent` 혹은 축약형인 `React.FC`를 활용하여 컴포넌트를 작성할 수 있습니다.

```jsx
const App: React.FunctionComponent<{ message: string }> = ({ message }) => (
  <div>{message}</div>
);
```

```jsx
const Title: React.FunctionComponent<{ title: string }> = ({
  children,
  title,
}) => <div title={title}>{children}</div>;
```

`React.FunctionComponent`를 사용하지 않고 아래와 같이 작성하면 `children`은 명시되지 않은 타입이기 때문에 에러를 띄웁니다.

```jsx
interface TitleProps {
  title: string;
}
const Title = ({ children, title }: TitleProps) => (
  <div title={title}>{children}</div>
);
```

만약 `React.FC`를 사용하지 않고 위와 같이 작성하고 싶으면 아래와 같이 React에서 제공하는 `React.ReactNode` 타입을 사용하면 됩니다.

```jsx
interface TitleProps {
  children: React.ReactNode;
  title: string;
}
const Title = ({ children, title }: TitleProps) => (
  <div title={title}>{children}</div>
);
```

#### 1.1.3 사소한 함정들\(Minor Pitfalls\)

아래와 같은 패턴을 사용하면 에러가 발생합니다.

```jsx
const MyConditionalComponent = ({ shouldRender = false }) =>
  shouldRender ? <div /> : false; // don't do this in JS either
const el = <MyConditionalComponent />; // throws an error
```

### 1.2 [Hooks](https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-started/hooks)

#### 1.2.1 [useState](https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-started/hooks#usestate)

#### 1.2.2 [useReducer](https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-started/hooks#usereducer)

#### 1.2.3 [useEffect](https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-started/hooks#useeffect)

#### 1.2.4 [useRef](https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-started/hooks#useref)

#### 1.2.5 [useImperativeHandle](https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-started/hooks#useimperativehandle)

#### 1.2.6 [Custom Hooks](https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-started/hooks#custom-hooks)

### 1.3 [Class Components](https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-started/class_components)

### 1.4 [Typing defaultProps](https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-started/default_props)

### 1.5 [Types or Interfaces?](https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-started/types_or_interfaces)

### 1.6 [Basic Prop Types Examples](https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-started/basic_type_example)

### 1.7 [Useful React Prop Type Examples](https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-started/react_prop_type_example)

### 1.8 [getDerivedStateFromProps](https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-started/get_derived_props_from_state)

### 1.9 [Forms and Events](https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-started/forms_and_events)

### 1.10 [Context](https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-started/context)

### 1.11 [forwardRef/createRef](https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-started/forward_and_create_ref)

### 1.12 [Portals](https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-started/portals)

### 1.13 [Error Boundaries](https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-started/error_boundaries)

### 1.14 [Concurrent React/React Suspense](https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-started/concurrent)

## 2. Troubleshooting

## 3. Handbook

## Recommendations

## Editor Tooling and Integration

## Linting

## Examples

