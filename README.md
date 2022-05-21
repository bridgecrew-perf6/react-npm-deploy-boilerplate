# 💻 리액트 디자인 시스템 NPM 배포 보일러 플레이트
- UI Kits, Design System 구축해서 NPM으로 오픈소스 배포에 최적화
- 웹팩 개발 서버, 불 필요한 웹팩, 로더 모두 제거 후 경량화
- TypeScript + Storybook 지원

<br />

### 의존성 설치
```
yarn
또는
```

<br />

### development
- src폴더에서 컴포넌트 작업 후 `src/index.tsx`에서 export

```js
// src/components/Button/Button.tsx
import React from 'react';
import styled from 'styled-components';

interface Props {
  children: React.ReactNode;
  size?: 'medium' | 'large';
}

const Button = ({ children, size = 'medium' }: Props) => {
  return <StyledButton size={size}>{children}</StyledButton>;
};

// styled 코드

export default Button
```
```js
// src/index.tsx
export { default as Button } from './components/Button/Button';
```

<br />

### build
- 컴포넌트 작업 후 build
- build 파일들은 `dist` 폴더에 생성
```
yarn build
```

<br />

### deploy
- 주의 1. deploy하기 전에 package.json version 업데이트 해줘야 함
- 주의 2. deploy하기 전에 꼭 build 진행해야 됌 dist 폴더가 npm에 올라감
```
npm publish
``` 

<br />

### download
```
yarn add (본인 배포 저장소)
```
```jsx
import { Button } from 'react-npm-deploy-boilerplate';

function App() {
  return (
    <div>
      <Button>하이</Button>
      <Button size="large">바이</Button>
    </div>
  )
}

export default App;
```

<br />

### storybook
- storybook을 통해서 ui 테스트 가능
- Example 코드는 src/stories 에서 확인 가능
```
스토리북 실행
yarn storybook
```
```jsx
// src/stories/components/Button.stories.tsx
import React from 'react';
import { Story } from '@storybook/react/types-6-0';
import Button from 'src/components/Button/Button';

export default {
  title: 'components/Button',
  argTypes: {
    size: {
      options: ['medium', 'large'],
      control: { type: 'select' },
    },
  },
};

interface Props {
  size: 'medium' | 'large';
  select: any[];
}

const Template: Story<Props> = ({ size }: Props) => {
  return (
    <div>
      <Button size={size}>안녕</Button>
    </div>
  );
};

export const Default = Template.bind({});

Default.args = {
  size: 'medium',
};

```

<br />

