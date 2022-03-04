# Testing Library (/w React)

### Required modules

- msw (for mocking http request/response)
- testing-library/react

# 필요성

> 주관적인 의견이 포함되어있습니다.

- storybook 도 훌륭한 ui 테스팅 라이브러리이지만 항상 모든 인터렉션을 검증하기엔 적합하지 않다.
- storybook 에선 prop 변화에 따른 컴포넌트 렌더링을 보여주기 힘들다.
- 개발 당시 의도한 인터렉션을 모두 명시하고 실행 가능한 코드로 작성한다는 것에 의미가 있다고 생각한다.

# Usage

## render

```
function render(
    ui: React.ReactElement<any>,
    options?: {
        ...
    }
): RenderResult
```

인자로 넘겨준 ReactElement를 document.body 에 append 한다.
제공되는 옵션은 다음과 같다.

### container

첫번째 인자로 넘겨준 ReactElement를 append 할 container.
default: document.body

### baseElement

```
baseElement = container ? container : document.body
```

### hydrate

hydrate = true 인 경우 ReactDom.hydrate로 render 한다.

### wrapper

```
const AllTheProviders = ({children}) => {
  return (
    <ThemeProvider theme="light">
      <TranslationProvider messages={defaultStrings}>
        {children}
      </TranslationProvider>
    </ThemeProvider>
  )
}

const customRender = (ui, options) =>
  render(ui, {wrapper: AllTheProviders, ...options})
```

Provider 컴포넌트가 있을 경우 편리함.

### queries

bind할 query들. default query를 오버라이드할 custom query

## RenderResult

### ...queries

```
const {getByLabelText, queryAllByTestId, ... ,} = render(<Component />)
```

보통 이렇게도 query들을 구조분해로 꺼내쓰지만

```
import { render, screen } from "@testing-library/react";

render(<Component />);

screen.getByLabelText("...");
```

처럼 screen 객체에서 바로 접근하기도 한다.

이 방식이 하나하나 꺼내쓰는 방법보다 훨씬 편한듯.
