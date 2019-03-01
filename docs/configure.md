# Configure :hatched_chick:
├── [Pages](#pages)
├── [Cases](#cases)
└── [Responsive Cases](#responsive-cases)

## Pages

Each test component should be described. One component — one page.

First of all, let's create a Page.
It's easier to follow the following file structure:

```
your-project
├── uibook
│   ├── button.uibook.js
│   ├── field.uibook.js
│   └── uibook-controller.js
├── src
│   ├── button.js
│   └── field.js
├── webpack.config.js
└── package.json
```

:triangular_flag_on_post: Tip: run `$ npx uibook-plugin structure` 
to create example Uibook files. // TODO

1. Create a new js file in `uibook/` folder naming it 
as a test component
2. Open this file, import `UibookCase` and your Component
3. Then return an object like in an example below

_button.uibook.js_
```js
import UibookCase from 'uibook-plugin/components/case'
import Button from '../src/button'

export default {
  component: Button,
  name: 'Button',
  cases: [...]
}
```

where:
- `component` — pass the Test Component here
- `name` — a name of the Page
- `cases` — an array of Cases

## Cases

Кейс — это один набор параметров, передаваемых в компонент.

Each case is a function returning `UibookCase` with the following parameters:

_button.uibook.js_
```js
export default {
  component: Button,
  name: 'Button',
  cases: [
    () => <UibookCase props={{ href: '#' }}>Button</UibookCase>,
    () => <UibookCase props={{ isSmall: true, href: '#' }}>
      Small Button
    </UibookCase>
  ]
}
```

where:
- `example` _(optional)_ — code example or your comments, it will be rendered
before Test Component. Если не указать, то сгенерируется автоматически
- `props` — set of necessary props
– `text` — string child of the Component

## Responsive Cases

Mobile Cases will be rendered in an iframe to emulate
media queries.

You can add Mobile case by wrapping a Case with the object

Невероятная важная фича: мобильные кейсы с настоящими media-запросами. Реализовано с помощью iframe. Достаточно обернуть функцию в объект, опционально задав высоту или ширину. Если задать только ширину, то высота определяется автоматически.

_button.uibook.js_
```js
  cases: [
    () => <UibookCase props={{ … }}>Button</UibookCase>,
    {
      width: 320,
      body: () => <UibookCase props={{ … }}>Mobile Button</UibookCase>
    }
  ]
```

## Events testing

You can pass fake events to your components as props:

_button.uibook.js_
```js
  cases: [
    () => <UibookCase props={{
      onClick: UibookCase.event('onClick')
    }}>Clickable Button</UibookCase>,
  ]
```

This will render a small popup with arguments when triggered.

---

[← Back to the installation guide](install.md)
**[Next: Controller →](controller.md)**