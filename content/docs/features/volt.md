---
title: Vole Pages
description: Learn how to use volt pages in your themes
prevTitle: 'Themes'
prevURL: '/docs/features/themes'
nextTitle: null
nextURL: null
---

# Volt Pages

When you create/install a new theme, the `pages` directory. Let's discuss more about how this works below:

- [Volt Pages](#volt-pages)
    - [Pages Directory and Folio](#pages-directory-and-folio)
    - [Single File Volt Pages](#single-file-volt-pages)


### Pages Directory and Folio

We are utilizing <a href="https://laravel.com/docs/folio" target="_blank">Laravel Folio</a> to make it easy to create new routes and pages in your app. When you add a new file to the `pages` directory. For example, if we add a file called `about.blade.php` our application will now have a new route at `/about` which is mapped to that file. Here is a list of how files can map to URL's.

| **File**                         | **Route**                   |
|----------------------------------|-----------------------------|
| `pages/index.blade.php`          | `/` (Homepage)              |
| `pages/about.blade.php`          | `/about`                    |
| `pages/about/index.blade.php`    | `/about`                    |
| `pages/blog/index.blade.php`     | `/blog`                     |
| `pages/blog/show.blade.php`      | `/blog/show`                |
| `pages/blog/[post].blade.php`    | `/blog/{post}` (Dynamic)    |
| `pages/contact.blade.php`        | `/contact`                  |
| `pages/services/web.blade.php`   | `/services/web`             |
| `pages/[category]/index.blade.php`| `/{category}` (Dynamic)    |
| `pages/[category]/[id].blade.php`| `/{category}/{id}` (Dynamic)|

You will want to learn more about how Folio works by checking out the official <a href="https://laravel.com/docs/folio" target="_blank">documentation here</a>.

### Single File Volt Pages

We are utilizing Laravel Livewire in every theme. This means that you can add Volt functionality to any page you create inside the `resources/themes/{theme}/pages` directory.

Here's a simple version `todos` Volt single-file component:

```php
<?php

    use function Laravel\Folio\{middleware, name};
    use Livewire\Volt\Component;
    use Livewire\Attributes\Rule;
    use Livewire\Attributes\Computed;
    name('todos');

    new class extends Component
    {
        public $todos;

        #[Rule('required')] 
        public $todo;
        
        public function mount()
        {
            $this->todos = [
                ['todo' => 'Install Wave Application', 'completed' => true,],
                ['todo' => 'Read the documentation', 'completed' => false,],            
                ['todo' => 'Learn how to use folio and volt', 'completed' => false,],
                ['todo' => 'Add the todos single-file volt component', 'completed' => false,],
                ['todo' => 'See how simple Wave will make your life', 'completed' => false,]
            ];
        }

        public function add()
        {
            $this->validate();
            
            $this->todos[] = [
                'todo' => $this->todo,
                'completed' => false,
            ];
            
            $this->reset('todo');
        }

        #[Computed]
        public function remaining()
        {
            return collect($this->todos)->where('completed', false)->count();
        }
    }
?>

<x-layouts.marketing>
    @volt('todos')
        <div class="flex justify-center items-center px-16 py-20 w-full h-full text-gray-300 bg-gray-100">
            <div class="p-10 bg-white rounded">
                <h2 class="text-base font-semibold leading-7 text-gray-900">My Todo</h2>
                <p class="mt-1 text-sm leading-6 text-gray-500">You have {{ $this->remaining }} things on your todo list.</p>

                <div class="mt-4 space-y-3">
                    @foreach($todos as $todo)
                    <div class="flex relative items-start">
                        <div class="flex items-center h-6">
                            <input id="todo-{{ $loop->index }}" wire:model.live="todos.{{ $loop->index }}.completed" type="checkbox" value="1" class="w-4 h-4 text-indigo-600 rounded border-gray-300 focus:ring-indigo-600">
                        </div>
                        <div class="ml-3 text-sm leading-6">
                            <label for="todo-{{ $loop->index }}" class="font-medium text-gray-900">{{ $todo['todo'] }}</label>
                        </div>
                    </div>
                    @endforeach
                </div>

                <form wire:submit="add" class="mt-6">
                    <input type="text" wire:model="todo" placeholder="My new todo..." class="block py-1.5 w-full text-gray-900 rounded-md border-0 ring-1 ring-inset ring-gray-300 shadow-sm placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6">
                </form>
            </div>
        </div>
    @endvolt
</x-layouts.marketing>
```

If you add this file to `resources/themes/anchor/todos.blade.php` you'll be able to visit the todos page at your app URL `/todos`, and see a page that looks like this:

<img src="https://cdn.devdojo.com/images/august2024/todos-component.png" class="w-full" alt="Single-file Todos Component" />

Be sure to learn more about Volt page by visiting the <a href="https://livewire.laravel.com/docs/volt" target="_blank">full documentation here</a>.

