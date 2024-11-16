
# @precooked/react-sortable

![Precooked Logo](https://precookedcode.com/assets/logos/logo-horizontal-dark.svg)

A React library for creating sortable lists with drag-and-drop support. This library provides components for handling sortable containers, sortable elements, and drag handles.

---

## Installation

Install the package using npm or yarn:

```bash
npm install @precooked/react-sortable
# or
yarn add @precooked/react-sortable
```

---

## Features

- Simple and intuitive API for sortable lists.
- Supports both drag handles and full-element dragging.
- Fully customizable.

---

## Components

### `SortableContainer`
The main container for managing sortable items.

#### Props:
| Prop              | Type               | Description                                            | Default   |
|-------------------|--------------------|--------------------------------------------------------|-----------|
| `items`           | `any[]`           | Array of items to be rendered and sorted.              | `[]`      |
| `onSortEnd`       | `(newOrder: any[]) => void` | Callback called when the list order changes.          | `null`    |
| `renderItem`      | `(item: any, index: number) => React.ReactNode` | Function to render each item.                        | `null`    |
| `useDragHandle`   | `boolean`         | Enables sorting using a drag handle (`SortableHandle`). | `false`   |

---

### `SortableElement`
Wraps each individual item in the sortable list.

#### Props:
| Prop              | Type               | Description                                            | Default   |
|-------------------|--------------------|--------------------------------------------------------|-----------|
| `index`           | `number`          | Index of the item in the list.                         | `null`    |
| `useDragHandle`   | `boolean`         | Whether to use a drag handle for this element.         | `false`   |
| `onDragStart`     | `(event: React.DragEvent) => void` | Callback when dragging starts.                      | `null`    |
| `onDragOver`      | `() => void`      | Callback when an item is dragged over this element.    | `null`    |
| `onDrop`          | `() => void`      | Callback when an item is dropped on this element.      | `null`    |

---

### `SortableHandle`
Optional drag handle for items in the list. Use it when `useDragHandle` is set to `true` in the `SortableContainer`.

#### Props:
| Prop              | Type               | Description                                            | Default   |
|-------------------|--------------------|--------------------------------------------------------|-----------|
| `children`        | `React.ReactNode` | The content inside the handle (e.g., an icon).         | `null`    |

---

## Usage Examples

### Example 1: Full-Element Dragging (Without `useDragHandle`)

```tsx
import React, { useState } from 'react';
import { SortableContainer, SortableElement } from '@precooked/react-sortable';

const Example = () => {
    const [items, setItems] = useState(['Item 1', 'Item 2', 'Item 3']);

    const handleSortEnd = (newOrder) => {
        setItems(newOrder);
    };

    const renderItem = (item, index) => (
        <div style={{ padding: 10, border: '1px solid #ccc' }}>{item}</div>
    );

    return (
        <SortableContainer
            items={items}
            onSortEnd={handleSortEnd}
            renderItem={renderItem}
        />
    );
};

export default Example;
```

---

### Example 2: Using a Drag Handle (`useDragHandle`)

```tsx
import React, { useState } from 'react';
import { SortableContainer, SortableElement, SortableHandle } from '@precooked/react-sortable';
import { Icon } from '@precooked/react-icon'; // Optional: Replace with your drag handle icon.

const Example = () => {
    const [items, setItems] = useState(['Item 1', 'Item 2', 'Item 3']);

    const handleSortEnd = (newOrder) => {
        setItems(newOrder);
    };

    const renderItem = (item, index) => (
        <div style={{ display: 'flex', alignItems: 'center', padding: 10, border: '1px solid #ccc' }}>
            <SortableHandle>
                <Icon name="drag" />
            </SortableHandle>
            <span>{item}</span>
        </div>
    );

    return (
        <SortableContainer
            items={items}
            onSortEnd={handleSortEnd}
            renderItem={renderItem}
            useDragHandle={true}
        />
    );
};

export default Example;
```

---

### Example 3: Custom Drag Handle Content

You can customize the content inside the `SortableHandle`:

```tsx
<SortableHandle>
    <span style={{ padding: '0 10px', cursor: 'grab' }}>☰</span>
</SortableHandle>
```

---

## License

This project is licensed under the MIT License. See the LICENSE file for details.
