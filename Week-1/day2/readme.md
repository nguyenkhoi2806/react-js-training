# Props, State in react

## State

### What is state

- State là một đối tượng đặc biệt trong React, dùng để lưu trữ dữ liệu nội bộ của component.
- Khi state thay đổi, React sẽ tự động re-render lại component để cập nhật giao diện.

### Tại sao cần state?

- HTML/JS thông thường không "nhớ" được dữ liệu sau mỗi lần thay đổi.
- React cho phép ghi nhớ và cập nhật lại UI khi dữ liệu thay đổi — nhờ vào state.

### Ví dụ

- Số lần người dùng click nút
- Tình trạng mở/tắt menu
- Danh sách sản phẩm đã thêm vào giỏ hàng

### Cách sử dụng state

### Function component

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```

**\*Explain**

- `useState(0)` tạo ra một state tên count với giá trị khởi đầu là 0
- `setCount` là hàm dùng để thay đổi giá trị count
- Khi gọi `setCount(...)`, React sẽ `re-render` lại UI để hiển thị giá trị mới

### Class component

```jsx
import React from "react";

class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0,
    };
  }

  handleClick = () => {
    this.setState({
      count: this.state.count + 1,
    });
  };

  render() {
    return (
      <div>
        <p>You clicked {this.state.count} times</p>
        <button onClick={this.handleClick}>Click me</button>
      </div>
    );
  }
}

export default Counter;
```

**\*Explain**

- `constructor` Dùng để khởi tạo state, gọi `super(props)` để kế thừa từ `React.Component`
- `this.state` Dữ liệu nội bộ của component
- `this.setState(...)` Cập nhật `state` và tự động `re-render` giao diện
- `render()` Trả về JSX để hiển thị trên giao diện

## Props

### What is Props

- Props là viết tắt của "properties"
- Dùng để truyền dữ liệu từ component cha → component con
- Trong React, props là "đầu vào" của component, giúp component linh hoạt & tái sử dụng được.

### Example

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}!</h1>;
}

function App() {
  return <Welcome name="William" />;
}
```

**\*Explains**

- Welcome là component con
- name="William" là props được truyền từ App vào Welcome
- Trong Welcome, ta truy cập props.name để sử dụng dữ liệu đó

### Tái sử dụng component với propsi
