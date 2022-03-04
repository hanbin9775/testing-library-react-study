# Testing Library (/w React)

### Required modules

- msw (for mocking http request/response)
- testing-library/react

# 필요성

- storybook 도 훌륭한 ui 테스팅 라이브러리이지만 항상 모든 인터렉션을 검증하기엔 적합하지 않다.
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

render 함수의 가장 중요한 특징 중 하나는
