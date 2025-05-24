# Review previous lesson

## React.Memo

- là một higher-order component (HOC) trong React, dùng để ghi nhớ (memoize) một component — nghĩa là React sẽ tránh re-render lại component đó nếu props không thay đổi.

```jsx
const MyComponent = React.memo(function MyComponent(props) {
  return <div>{props.value}</div>;
});
```

**_Why use need React.memo?_**

- Mỗi khi component cha re-render, tất cả component con cũng mặc định re-render, dù props không đổi.
- Dùng React.memo, bạn:

  - Tránh render lại không cần thiết
  - Tối ưu hiệu năng, nhất là với component con:
    - nặng (nhiều tính toán)
    - hoặc hiển thị danh sách lớn, hoặc
    - nằm trong danh sách được map/render nhiều lần

```jsx
const Child = React.memo(({ value }) => {
  console.log("Child render");
  return <div>Value: {value}</div>;
});

function Parent() {
  const [count, setCount] = useState(0);

  return (
    <>
      <button onClick={() => setCount(count + 1)}>Increase</button>
      <Child value="static" />
    </>
  );
}
```

Khi nhấn nút, Parent render lại, nhưng Child không re-render, vì value không đổi.

**_Summary_**

`React.memo` giúp tiết kiệm render nếu props không đổi.

## useRef

- useRef is a React hook that allows you to store a "reference" value without causing the component to re-render when the value changes.
- It is commonly used to directly access DOM elements or to persist a value across renders.

```jsx
const myRef = useRef(initialValue);
```

`myRef.current` holds the current value of the ref.

_**When use useRef**_

- Want to update and store a value without causing a re-render.
- Store DOM information to access the DOM element directly.

_**Example access the DOM element**_

```jsx
import { useRef } from "react";

function FocusInput() {
  const inputRef = useRef();

  const handleFocus = () => {
    inputRef.current.focus();
  };

  return (
    <>
      <input ref={inputRef} />
      <button onClick={handleFocus}>Focus Input</button>
    </>
  );
}
```

_**Example store value without rerender**_

```jsx
function RenderCounter() {
  const renderCount = useRef(1);

  useEffect(() => {
    renderCount.current++;
  }, []);

  return <p>Render count: {renderCount.current}</p>;
}
```

## useCallBack

useCallback is a React hook that helps memoize a callback function. It returns a version of the function that only changes when one or more specified dependencies change.

```jsx
const memoizedCallback = useCallback(() => {
  ///logic
}, [dependencies]);
```

**_Why use callback_**

Khi một component React re-render, tất cả hàm bên trong nó (được định nghĩa lại trong hàm component) cũng được tạo lại mới, dẫn đến:

- Component con nhận prop là hàm mới sẽ bị re-render lại, dù không cần thiết.
- Khi hàm callback được truyền làm dependency cho các hook như useEffect, useMemo, việc hàm đó thay đổi liên tục sẽ gây gọi lại không cần thiết.

useCallback giúp tránh tái tạo hàm không cần thiết, tối ưu hiệu năng và giúp React dễ dàng kiểm soát các lần render.

```jsx
import React, { useState, useCallback } from "react";

const Child = React.memo(({ onClick }) => {
  console.log("Child rendered");
  return <button onClick={onClick}>Click me</button>;
});

export default function Parent() {
  const [count, setCount] = useState(0);

  const handleClick = () => {
    console.log("Button clicked");
  };

  return (
    <div>
      <h1>Count: {count}</h1>
      <button onClick={() => setCount(count + 1)}>Increase Count</button>
      <Child onClick={handleClick} />
    </div>
  );
}
```

**_When use useCallBack_**

- Khi truyền callback xuống các component con đã được React.memo, để tránh render lại không cần thiết của component con.
- Khi callback là dependency của các hook khác như useEffect hoặc useMemo để tránh gọi lại nhiều lần.
- Khi hàm callback có logic phức tạp hoặc liên quan đến tính toán, cần ghi nhớ để tăng hiệu suất.?

```jsx
export default function Parent() {
  const [count, setCount] = useState(0);

  const handleClick = useCallback(() => {
    console.log("Button clicked");
  }[]);

  return (
    <div>
      <h1>Count: {count}</h1>
      <button onClick={() => setCount(count + 1)}>Increase Count</button>
      <Child onClick={handleClick} />
    </div>
  );
}
```

**_Summary_**

- useCallback giúp React "ghi nhớ" hàm, tránh tạo lại hàm mới mỗi lần render.
- Dùng để tối ưu hiệu năng, đặc biệt khi truyền callback xuống component con hoặc làm dependency trong các hook khác.

## useMemo

- `useMemo` là một hook trong React dùng để ghi nhớ (memoize) kết quả của một phép tính tốn kém, chỉ tính lại khi dependency thay đổi.

```jsx
const memoizedValue = useMemo(() => {
  return computeExpensiveValue(a, b);
}, [a, b]);
```

- `computeExpensiveValue` chỉ được gọi lại khi a hoặc b thay đổi.
- Nếu dependency không đổi → kết quả cũ được reuse → tối ưu hiệu năng.

_**When use useMemo**_

- Tính toán nặng lặp lại nhiều lần

  - Ví dụ: sort, filter, map dữ liệu lớn.

- Tránh tạo object/array mới mỗi render

  - Dùng làm props cho component con đã React.memo.

- Khi performance là vấn đề thực sự

  - Tránh dùng để "tối ưu sớm" gây phức tạp không cần thiết.

```jsx
import React, { useState, useMemo } from "react";

function App() {
  const [count, setCount] = useState(0);
  const [other, setOther] = useState(false);

  const expensiveValue = useMemo(() => {
    console.log("♻️ Tính toán lại...");
    let total = 0;
    for (let i = 0; i < 1_000_000_000; i++) {
      total += i;
    }
    return total + count;
  }, [count]);

  return (
    <div>
      <p>Expensive result: {expensiveValue}</p>
      <button onClick={() => setCount(count + 1)}>Tăng count</button>
      <button onClick={() => setOther(!other)}>Toggle other</button>
    </div>
  );
}
```

## Form

### Controlled Component

- Là các component mà giá trị của input được điều khiển hoàn toàn bởi React thông qua state.

- Đặc điểm:

  - Giá trị nhập vào được lưu trong useState
  - Bắt buộc xử lý onChange để cập nhật state
  - Dễ kiểm soát, dễ xác thực dữ liệu, dễ reset form

_**Example**_

```jsx
import { useState } from "react";

function ControlledInput() {
  const [name, setName] = useState("");

  return <input value={name} onChange={(e) => setName(e.target.value)} />;
}
```

### Uncontrolled Component

- Là các component mà giá trị của input được lưu trữ trực tiếp trong DOM, không thông qua state.

- Đặc điểm:

  - Dùng ref để lấy giá trị khi cần thiết
  - Không cần state để lưu trữ giá trị
  - Nhanh chóng cho form đơn giản, nhưng khó kiểm soát khi form phức tạp

_**Example**_

```jsx
import { useRef } from "react";

function UncontrolledInput() {
  const inputRef = useRef();

  const handleSubmit = () => {
    alert(inputRef.current.value);
  };

  return (
    <>
      <input ref={inputRef} />
      <button onClick={handleSubmit}>Submit</button>
    </>
  );
}
```

### Compartition

| Tiêu chí        | Controlled Component              | Uncontrolled Component         |
| --------------- | --------------------------------- | ------------------------------ |
| Quản lý dữ liệu | Qua `state`                       | Qua DOM (`ref`)                |
| Tính linh hoạt  | Cao (validation, auto format,...) | Thấp hơn                       |
| Tính hiệu năng  | Chậm hơn chút (nhiều re-render)   | Nhanh hơn cho form đơn giản    |
| Sử dụng khi nào | Form phức tạp, cần validation     | Form đơn giản, hoặc quick task |

## Exercise

### Exercise 1: Basic React.memo

- Task:

  - Create two components: Counter (parent) and Child (child).
  - Child accepts a title prop and logs to the console on render.
  - When the count changes but title doesn’t, Child should not re-render.

### Exercise 2: Optimize Callback with useCallback

- Task:

  - Create a List component that receives an onAddItem function from the parent.
  - Use useCallback in the parent to prevent passing a new function reference on each render.

### Exercise 3: Memoize Expensive Computation with useMemo

- Task:

  - Create two states: number and text
  - Compute isEven(number) with a simulated heavy function (slow loop)
  - Use useMemo to only recompute when number changes
