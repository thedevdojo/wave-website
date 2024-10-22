---
title: Using Filament With Volt
description: Learn how to use FilamentPHP with any Volt page
prevTitle: 'About Guides'
prevURL: '/docs/guides/about'
nextTitle: ''
nextURL: null
---

# Using Filament with Volt

Using Filament with Wave and Volt can make your life a lot easier. In this guide we will use the example from the <a href="{ url('/docs/your-functionality' )}">Your Functionality</a> section and show you how to implement the same functionality using the <a href="https://filamentphp.com/docs/tables/installation" target="_blank">Table Builder</a> and the <a href="https://filamentphp.com/docs/forms/installation" target="_blank">Form Builder</a>.

- [Using Filament with Volt](#using-filament-with-volt)
  - [Using the Table Builder](#using-the-table-builder)
  - [Using the Form Builder](#using-the-form-builder)
  - [Combining the Table and Form Builder](#combining-the-table-and-form-builder)


We will assume that you've already added the **database migration** and the **model** for the `projects` table in <a href="{ url('/docs/your-functionality' )}">this section</a>. Be sure to finish that section before continuing with this guide.

## Using the Table Builder

Looking at the **volt project page** that we created inside the theme page directory at `pages/projects/index.blade.php` we can utilize the Table builder to easily display our projects in a nice table view:

**resources/themes/{theme}/pages/projects/index.blade.php**

```php
<?php
    use App\Models\Project;
    use Filament\Forms\Concerns\InteractsWithForms;
    use Filament\Forms\Contracts\HasForms;
    use Filament\Tables;
    use Filament\Tables\Columns\TextColumn;
    use Filament\Tables\Table;
    use Livewire\Volt\Component;
    use function Laravel\Folio\{middleware, name};

	middleware('auth');
    name('projects');

    new class extends Component implements HasForms, Tables\Contracts\HasTable
	{
        use InteractsWithForms, Tables\Concerns\InteractsWithTable;

        public ?array $data = [];

        public function table(Table $table): Table
        {
            return $table
                ->query(Project::query()->where('user_id', auth()->id()))
                ->columns([
                    TextColumn::make('name')
                        ->searchable()
                        ->sortable(),
                    TextColumn::make('description')
                        ->limit(50)
                        ->searchable(),
                    TextColumn::make('start_date')
                        ->date()
                        ->sortable(),
                    TextColumn::make('end_date')
                        ->date()
                        ->sortable(),
                    TextColumn::make('created_at')
                        ->dateTime()
                        ->sortable()
                        ->toggleable(isToggledHiddenByDefault: true),
                ])
                ->defaultSort('created_at', 'desc');
        }
    }
?>

<x-layouts.app>
    @volt('projects')
        <x-app.container>
            <div class="flex items-center mb-5 justify-between">
                <x-app.heading
                        title="Projects"
                        description="Check out your projects below"
                        :border="false"
                    />
                <x-button tag="a" href="/projects/create">New Project</x-button>
            </div>
            <div class="overflow-x-auto rounded-lg border">
                {{ $this->table }}
            </div>
        </x-app.container>
    @endvolt
</x-layouts.app>
```

This code will generate a table that is sortable and searchable. See screenshot below of what this code will create.

<img src="https://cdn.devdojo.com/images/october2024/projects-table.png" class="w-full" alt="filament table">

Next, let's see what it would take to implement the project creation in the `projects/create.blade.php` file:

## Using the Form Builder

We can easily utilize the Filament Form builder to simplify the creation of our projects. Here's what the code looks like for our `projects/create.blade.php` file:

**resources/themes/{theme}/pages/projects/create.blade.php**

```php
<?php
    use Filament\Forms\Components\TextInput;
    use Filament\Forms\Components\Textarea;
    use Filament\Forms\Components\DatePicker;
    use Filament\Forms\Concerns\InteractsWithForms;
    use Filament\Forms\Contracts\HasForms;
    use Filament\Forms\Form;
    use Filament\Notifications\Notification;
    use Livewire\Volt\Component;
    use function Laravel\Folio\{middleware, name};
    use App\Models\Project;

    middleware('auth');
    name('projects.create');

    new class extends Component implements HasForms
    {
        use InteractsWithForms;

        public ?array $data = [];

        public function mount(): void
        {
            $this->form->fill();
        }

        public function form(Form $form): Form
        {
            return $form
                ->schema([
                    TextInput::make('name')
                        ->required()
                        ->maxLength(255),
                    Textarea::make('description')
                        ->maxLength(1000),
                    DatePicker::make('start_date'),
                    DatePicker::make('end_date')
                        ->after('start_date'),
                ])
                ->statePath('data');
        }

        public function create(): void
        {
            $data = $this->form->getState();
            
            auth()->user()->projects()->create($data);
            
            $this->form->fill();

            Notification::make()
                ->success()
                ->title('Project created successfully')
                ->send();

            $this->redirect('/projects');
        }
    }
?>

<x-layouts.app>
    @volt('projects.create')
        <x-app.container class="max-w-xl">
            <div class="flex items-center mb-5 justify-between">
                <x-app.heading
                    title="Create Project"
                    description="Fill out the form below to create a new project"
                    :border="false"
                />
            </div>

            <form wire:submit="create" class="space-y-6">
                {{ $this->form }}
                <div class="flex justify-end gap-x-3">
                    <x-button tag="a" href="/projects" color="secondary">Cancel</x-button>
                    <x-button type="submit" class="bg-primary-600 hover:bg-primary-500 text-white">
                        Create Project
                    </x-button>
                </div>
            </form>
        </x-app.container>
    @endvolt
</x-layouts.app>
```

Navigating to `app_url.test/projects/create` will allow us to create a new project with validation.

<img src="https://cdn.devdojo.com/images/october2024/projects-form.png" class="w-full rounded" alt="create project with filament form builder">

Utilizing the FilamentPHP form and table builder we can simplify the process even more by combining the table and form builder into a single Volt Page. Let's take a look at that below.

## Combining the Table and Form Builder

We can simplify the process of viewing, creating, editing, and deleting our projects by creating a single Volt Page that will handle all these operations for us. We can combine the **table** and **form** builder, like so:

**resources/themes/{theme}/pages/projects/index.blade.php**

```php
<?php
    use Filament\Forms\Components\TextInput;
    use Filament\Forms\Components\TextArea;
    use Filament\Forms\Components\DatePicker;
    use Livewire\Volt\Component;
    use function Laravel\Folio\{middleware, name};
    use Filament\Forms\Concerns\InteractsWithForms;
    use Filament\Forms\Contracts\HasForms;
    use Filament\Forms\Form;
    use Filament\Notifications\Notification;
    use Filament\Tables;
    use Filament\Tables\Table;
    use Filament\Tables\Actions\Action;
    use App\Models\Project;
    use Filament\Tables\Columns\TextColumn;
    use Filament\Tables\Actions\DeleteAction;
    use Filament\Tables\Actions\EditAction;
    use Filament\Tables\Actions\CreateAction;
    use Filament\Tables\Actions\ViewAction;

	middleware('auth');
    name('projects');

    new class extends Component implements HasForms, Tables\Contracts\HasTable
	{
        use InteractsWithForms, Tables\Concerns\InteractsWithTable;

        public ?array $data = [];

        public function table(Table $table): Table
        {
            return $table
                ->query(Project::query()->where('user_id', auth()->id()))
                ->columns([
                    TextColumn::make('name')
                        ->searchable()
                        ->sortable(),
                    TextColumn::make('description')
                        ->limit(50)
                        ->searchable(),
                    TextColumn::make('start_date')
                        ->date()
                        ->sortable(),
                    TextColumn::make('end_date')
                        ->date()
                        ->sortable(),
                    TextColumn::make('created_at')
                        ->dateTime()
                        ->sortable()
                        ->toggleable(isToggledHiddenByDefault: true),
                ])
                ->defaultSort('created_at', 'desc')
                ->actions([
                    ViewAction::make()
                        ->slideOver()
                        ->modalWidth('md')
                        ->form([
                            TextInput::make('name')
                                ->disabled(),
                            Textarea::make('description')
                                ->disabled(),
                            DatePicker::make('start_date')
                                ->disabled(),
                            DatePicker::make('end_date')
                                ->disabled(),
                        ]),
                    EditAction::make()
                        ->slideOver()
                        ->modalWidth('md')
                        ->form([
                            TextInput::make('name')
                                ->required()
                                ->maxLength(255),
                            Textarea::make('description')
                                ->maxLength(1000),
                            DatePicker::make('start_date'),
                            DatePicker::make('end_date')
                                ->after('start_date'),
                        ]),
                    DeleteAction::make()
                        ->after(function () {
                            Notification::make()
                                ->success()
                                ->title('Project deleted')
                                ->send();
                        })
                    ->mutateFormDataUsing(function (array $data): array {
                        $data['user_id'] = auth()->id();
                        return $data;
                    })
                    ->after(function () {
                        Notification::make()
                            ->success()
                            ->title('Project created')
                            ->send();
                    }),
                ])
                ->filters([
                    // Add any filters you want here
                ])
                ->bulkActions([
                    Tables\Actions\BulkActionGroup::make([
                        Tables\Actions\DeleteBulkAction::make(),
                    ]),
                ]);
        }

        public function form(Form $form): Form
        {
            return $form
                ->schema([
                    TextInput::make('name')
                        ->required()
                        ->maxLength(255),
                    Textarea::make('description')
                        ->maxLength(1000),
                    DatePicker::make('start_date'),
                    DatePicker::make('end_date')
                        ->after('start_date'),
                ])
                ->statePath('data');
        }

        public function create(): void
        {
            $data = $this->form->getState();
            
            $project = auth()->user()->projects()->create($data);
            
            $this->form->fill();

            Notification::make()
                ->success()
                ->title('Project created successfully')
                ->send();
        }
    }
?>

<x-layouts.app>
    @volt('projects')
        <x-app.container class="max-w-5xl">
        
            <div class="flex items-center mb-5 justify-between">
                <x-app.heading
                        title="Projects"
                        description="Check out your projects below"
                        :border="false"
                    />
                <x-modal id="create-project" width="md" :slide-over="true">
                    <x-slot name="trigger">
                        <x-button>New Project</x-button>
                    </x-slot>
                    <x-slot name="header">
                        <h2 class="text-lg font-medium">Create Project</h2>
                    </x-slot>

                    <form wire:submit="create" class="space-y-6">
                        {{ $this->form }}

                        <div class="mt-6 flex justify-end">
                            <x-button type="submit">
                                Create Project
                            </x-button>
                        </div>
                    </form>
                </x-modal>
            </div>
            <div class="overflow-x-auto rounded-lg border">
                {{ $this->table }}
            </div>
        </x-app.container>
    @endvolt
</x-layouts.app>
```

Now, when we visit `app_url.test/projects` we can view, create, edit, and delete projects from a single page. Here is how our new `/projects` page will look.

<img src="https://cdn.devdojo.com/images/october2024/projects-table-form.png" class="w-full rounded" alt="Projects View and Create">

As you can see, when you click on the `edit` button next to a project a slide-over will open allowing you to edit the details for this project.

<img src="https://cdn.devdojo.com/images/october2024/projects-edit.png" class="w-full rounded" alt="Projects Edit">

You can also click the **New Project** button and you'll see a slide-over open allowing you to create a new project.

<img src="https://cdn.devdojo.com/images/october2024/projects-create.png" class="w-full rounded" alt="Projects Create">

Combining the Table and the Form builder in the same page will make it easer to add functionality to our application.

