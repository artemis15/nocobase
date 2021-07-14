---
title: Upload - 上传
nav:
  title: 组件
  path: /client
group:
  order: 1
  title: Schemas
  path: /client/schemas
---

# Upload - 上传

## Node Tree

<pre lang="tsx">
<Upload/>
</pre>

## Designable Bar

- Upload.DesignableBar

## Examples

### 上传

```tsx
import React from 'react';
import { Button } from 'antd'
import { UploadOutlined, InboxOutlined } from '@ant-design/icons'
import Upload from './';
import { SchemaRenderer, registerComponents } from '../';

const NormalUpload = (props) => {
  return (
    <Upload
      {...props}
      action="https://www.mocky.io/v2/5cc8019d300000980a055e76"
      headers={{
        authorization: 'authorization-text',
      }}
    >
      <Button icon={<UploadOutlined />}>上传文件</Button>
    </Upload>
  )
}

registerComponents({
  NormalUpload,
});

const schema = {
  type: 'object',
  properties: {
    input: {
      type: 'string',
      title: `编辑模式`,
      'x-decorator': 'FormItem',
      'x-component': 'NormalUpload',
      'x-reactions': {
        target: 'read',
        fulfill: {
          state: {
            value: '{{$self.value}}',
          },
        },
      },
    },
    read: {
      type: 'string',
      title: `阅读模式`,
      'x-read-pretty': true,
      'x-decorator': 'FormItem',
      'x-component': 'NormalUpload',
    },
  }
};

export default () => {
  return (
    <SchemaRenderer schema={schema} />
  );
};
```