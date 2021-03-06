# Stimulus Sortable

[![](https://img.shields.io/npm/dt/stimulus-sortable.svg)](https://www.npmjs.com/package/stimulus-sortable)
[![](https://img.shields.io/npm/v/stimulus-sortable.svg)](https://www.npmjs.com/package/stimulus-sortable)
[![](https://github.com/stimulus-components/stimulus-sortable/workflows/Lint/badge.svg)](https://github.com/stimulus-components/stimulus-sortable)
[![](https://img.shields.io/github/license/stimulus-components/stimulus-sortable.svg)](https://github.com/stimulus-components/stimulus-sortable)
[![Netlify Status](https://api.netlify.com/api/v1/badges/a8341029-7f19-443d-88aa-02c6325b389e/deploy-status)](https://stimulus-sortable.netlify.com)

## Getting started

A Stimulus controller to reorder lists with drag-and-drop.

This controller is using [SortableJS](https://github.com/SortableJS/sortablejs) behind the scene.

## Installation

```bash
$ yarn add stimulus-sortable
```

And use it in your JS file:
```js
import { Application } from "stimulus"
import Sortable from "stimulus-sortable"

const application = Application.start()
application.register("sortable", Sortable)
```

## Usage

In your model:
```ruby
class Todo < ApplicationRecord
  acts_as_list # Or with a custom position system.
end
```

In your controller:
```ruby
class TodosController < ApplicationController
  def update
    # Do what you want with todo_params.
  end

  private

  def todo_params
    params.permit(:position)
  end
end
```

In your views:
### Basic usage
```html
<ul
  data-controller="sortable"
  data-sortable-animation="150"
>
  <li>Pet the cat</li>
  <li>Get the groceries</li>
</ul>
```

### With custom handler
```html
<ul
  data-controller="sortable"
  data-sortable-handle=".handle"
>
  <li>
    <svg class="handle"></svg>
    Pet the cat
  </li>

  <li>
    <svg class="handle"></svg>
    Get the groceries
  </li>
</ul>
```

### With AJAX call

If you're using [Rails UJS](https://github.com/rails/rails/tree/master/actionview/app/assets/javascripts) in your application, you can add an url as data-attribute on every items to perform an AJAX call to update the new position.

```html
<ul
  data-controller="sortable"
  data-sortable-resource-name="todo"
>
  <%= @todos.each do |todo| %>
    <!-- <li data-sortable-update-url="/todos/1">Pet the cat</li> -->
    <li data-sortable-update-url="<%= todo_path(todo) %>"><%= todo.description %></li>
  <% end %>
</ul>
```

By default, `position` will be used as param in a PATCH request.

If you use `data-sortable-resource-name`, the name will be used. For instance, `todo[position]`.

## Configuration

| Attribute | Default | Description | Optional |
| --------- | ------- | ----------- | -------- |
| `data-sortable-resource-name` | `undefined` | Name of the resource to use as AJAX param. | ✅ |
| `data-sortable-animation` | `150` | Animation speed moving items when sorting in milliseconds. `0` to disable. | ✅ |
| `data-sortable-handle` | `undefined` | Drag handle selector within list items. | ✅ |

## Extending Controller

You can use inheritance to extend the functionality of any Stimulus components.

```js
import Sortable from "stimulus-sortable"

export default class extends Sortable {
  connect() {
    super.connect()
    console.log("Do what you want here.")
  }
}
```

These controllers will automatically have access to targets defined in the parent class.

If you override the connect, disconnect or any other methods from the parent, you'll want to call `super.method()` to make sure the parent functionality is executed.

## Development

### Project setup
```bash
$ yarn install
$ yarn dev
```

### Linter
[Prettier](https://prettier.io/) and [ESLint](https://eslint.org/) are responsible to lint and format this component:
```bash
$ yarn lint
$ yarn format
```

## Contributing

Do not hesitate to contribute to the project by adapting or adding features ! Bug reports or pull requests are welcome.

## License

This project is released under the [MIT](http://opensource.org/licenses/MIT) license.
