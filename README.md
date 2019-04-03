<img align="right" src="assets/hook-and-loop.gif">

# React Conditions & Loops

## Get Started with Velcro by installing React Loops!

```sh
yarn add react-loops
```

## For Loops

Use the props `of` to provide the list and `as` to provide an element for
each item in the list. The `of` prop accepts Arrays, Array-likes,
and Iterables.

```js
<ul>
  <For of={myList} as={item =>
    <li>{item}</li>
  }/>
</ul>
```

Or provide a "render prop" function as a child.

```js
<ul>
  <For of={myList}>
    {item =>
      <li>{item}</li>
    }
  </For>
</ul>
```

Access additional information about each iteration by destructuring the
second argument:

- `index`: A number from 0 to the length of the list
- `length`: The length of the list
- `key`: The key for this item in the list. Same as `index` for Arrays
         but string properties for `in` Objects
- `isFirst`: True for the first iteration
- `isLast`: True for the last iteration

```js
<ul>
  <For of={myList} as={(item, { isLast }) =>
    <li><If case={isLast}>and </If>{item}</li>
  }/>
</ul>
```

### For in Loops

Use the prop `in` to provide an Object instead of an Array or Iterable.

```js
<ul>
  <For in={myObj} as={(item, {key}) =>
    <li>{key}: {item}</li>
  }/>
</ul>
```

### React Keys

Provide `key` on each child to ensure correct behavior if the list may be
reordered over time. If you don't provide `key`, the `key` of each
iteration will be used by default.

```js
<ul>
  <For of={myList} as={item =>
    <li key={item.id}>{item.label}</li>
  }/>
</ul>
```


## If conditions

Use the `case` prop with `<If>` and `<ElseIf>` elements to conditionally
include certain elements. When an `<If>` case is _truthy_ it does not
render any `<ElseIf>` or `<Else>` children. However when it is _falsey_ it
_only_ renders `<ElseIf>` and `<Else>` children.

```js
<If case={someCondition}>
  This will only be shown if someCondition is truthy.
  <ElseIf case={otherCondition}>
    This will only be shown if someCondition is falsey
    and otherCondition is truthy.
    <Else>
      This will only be shown if both someCondition and
      otherCondition are both falsey.
    </Else>
  </ElseIf>
  <Else>
    This will be shown if someCondition is falsey.
    <If case={finalCondition}>
      This will be shown if someCondition is falsey
      and finalCondition is truthy.
    </If>
  </Else>
</If>
```

Alternatively, you can provide `then` and `else` props.

```js
<If case={someCondition} then={
  "This will only be shown if someCondition is truthy."
} else={
  "This will be shown if someCondition is falsey."
}/>
```

## Choose conditions

Inspired by XSL this component renders the first `<When>` component
of which the `test` prop has a _truthy_ value. If no `<When>` component
has a _truthy_ value the `<Otherwise>` component is rendered instead.

```js
<Choose>
  <When test={someCondition}>
  This will only be shown if someCondition is truthy.
  </When>
  <When case={otherCondition}>
    This will only be shown if someCondition is falsey
    and otherCondition is truthy.
  </When>
  <Otherwise>
    This will be shown if someCondition and otherCondition are falsey.
  </Otherwise>
</Choose>
```


## History

Forked manuelbieh/react-loops which added `Choose/When/Otherwise` to leebyron/react-loops.  Lee dropped `<If />` in v1.2.0.  I liked the `<If />`, but may change the API to `<If></If>` & `Switch/Case/Default` which is more famaliar to JS-land.  Changed the project name not to confuse others, & myself ;).
