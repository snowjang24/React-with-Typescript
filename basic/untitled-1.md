# 1. Getting Started

## **1. Getting Started**

### **1.1** [**Function Components**](https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-started/function_components)\*\*\*\*

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

