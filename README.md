# angular-19-work-flow
This is the project where we can explore angular 19 feature and we can apply in our project.


Angular 19 introduces a significant shift in workflow and best practices, focusing on a standalone-first, signal-based, and simplified developer experience. Here's a breakdown of the new flow you need to be familiar with.

### 1\. New Control Flow Syntax: `@if`, `@for`, and `@switch`

This is one of the most visible changes and a cornerstone of the new Angular workflow. The new syntax is more intuitive, built-in, and doesn't require importing common modules like `CommonModule` for standalone components.

#### `@if`

The `@if` block replaces the `*ngIf` structural directive. It has a more readable syntax and natively supports `else if` and `else` conditions.

**Old Way (Angular 16 and below):**

```html
<div *ngIf="userIsLoggedIn; else loggedOut">
  Welcome, {{ user.name }}
</div>
<ng-template #loggedOut>
  Please log in.
</ng-template>
```

**New Way (Angular 19):**

```html
@if (userIsLoggedIn) {
  <div>Welcome, {{ user.name }}</div>
} @else {
  <div>Please log in.</div>
}
```

#### `@for`

The `@for` block replaces the `*ngFor` structural directive. It is designed to be more performant by requiring a `track` expression, which helps Angular optimize rendering by efficiently identifying and re-rendering only the items that have changed. It also has a built-in `@empty` block.

**Old Way (Angular 16 and below):**

```html
<div *ngFor="let user of users; trackBy: trackByUserId">
  {{ user.name }}
</div>
<div *ngIf="users.length === 0">
  No users found.
</div>
```

## Handling Empty Collections Gracefully
### The @empty block is a new addition that allows developers to provide fallback content when a collection/list is empty to enhance the user experience.

```html
<section>
   @for (user of userList; track user) {
      <user-card [data]="user" />
   } @empty {
      <p>No item available</p>
   }
</section>
```

**New Way (Angular 19):**

```html
@for (user of users; track user.id) {
  <div>{{ user.name }}</div>
} @empty {
  <div>No users found.</div>
}
```

### 2\. Service Injection: The `inject()` Function

The `inject()` function is now the recommended way to get services. It provides a more modern, flexible, and concise approach to dependency injection, especially in the context of standalone components and signals. It can be used outside of constructors, for instance, inside class fields and functions.

#### Old Way (Constructor Injection):

```typescript
import { Component } from '@angular/core';
import { UserService } from './user.service';

@Component({
  selector: 'app-user-profile',
  template: '...',
})
export class UserProfileComponent {
  constructor(private userService: UserService) {}
  
  // Use userService in methods
  saveUser() {
    this.userService.save();
  }
}
```

#### New Way (`inject()` function):

```typescript
import { Component, inject } from '@angular/core';
import { UserService } from './user.service';

@Component({
  selector: 'app-user-profile',
  standalone: true,
  template: '...',
})
export class UserProfileComponent {
  private userService = inject(UserService);

  // Use userService in methods
  saveUser() {
    this.userService.save();
  }
}
```
Here are **all** the Angular 19 topics you should know (excluding SSR, Angular Material updates, and anything related to testing):

1. **Standalone components, directives, and pipes now default to `standalone: true`** (no need to declare them in NgModule) ([Medium](https://medium.com/%40rajat29gupta/highlight-key-new-features-in-angular-19-de77981756c7?utm_source=chatgpt.com))
2. **Strict standalone enforcement**: new compiler flag `strictStandalone` to enforce standalone-first architecture ([Medium](https://medium.com/%40rajat29gupta/highlight-key-new-features-in-angular-19-de77981756c7?utm_source=chatgpt.com))
3. **Enhanced reactivity primitives**: stable introduction of signal APIs like `linkedSignal` and `resource()` ([Angular Blog](https://blog.angular.dev/meet-angular-v19-7b29dfd05b84?utm_source=chatgpt.com))
4. **Resource API**: declarative async data fetching with built‑in caching and loading/error states ([Medium](https://medium.com/%40rajat29gupta/highlight-key-new-features-in-angular-19-de77981756c7?utm_source=chatgpt.com))
5. **Local template variables**: new `@let` syntax for async values or DOM references in templates ([Medium](https://medium.com/%40rajat29gupta/highlight-key-new-features-in-angular-19-de77981756c7?utm_source=chatgpt.com))
6. **AutoCSP (developer preview)**: automatic Content Security Policy generation with inline script hashes ([Medium](https://medium.com/%40rajat29gupta/highlight-key-new-features-in-angular-19-de77981756c7?utm_source=chatgpt.com))
7. **Hot Module Replacement (HMR) for styles and templates**: live updates of CSS and templates without full reloads ([angularminds.com](https://www.angularminds.com/blog/angular-19-features?utm_source=chatgpt.com))
8. **Support for TypeScript 5.6**: updated compatibility; older TS 5.4 is no longer supported ([Bacancy](https://www.bacancytechnology.com/blog/whats-new-in-angular-19?utm_source=chatgpt.com))
9. **Command‑line environment variable support**: use `-define "apiKey=$API_KEY"` in builds ([Medium](https://medium.com/%40rajat29gupta/highlight-key-new-features-in-angular-19-de77981756c7?utm_source=chatgpt.com))
10. **Unused import warnings in standalone components**: CLI warns you when imports in standalone components aren’t used ([Medium](https://medium.com/%40rajat29gupta/highlight-key-new-features-in-angular-19-de77981756c7?utm_source=chatgpt.com))
11. **Angular Language Service + Schematics integration**: editor assistance and automatic migrations for modern APIs ([angularminds.com](https://www.angularminds.com/blog/angular-19-features?utm_source=chatgpt.com))
12. **Two‑dimensional drag‑and‑drop in CDK**: support for grid-style or mixed-axis dragging UI ([Medium](https://medium.com/%40rajat29gupta/highlight-key-new-features-in-angular-19-de77981756c7?utm_source=chatgpt.com))
13. *(Note: SSR topics such as incremental hydration, route-level render modes, event replay, zoneless SSR – are all excluded as per your request)*

---

Yes, there **are** more upgrades in Angular 19 beyond SSR and tests. The list above covers the rest of the new features and developer-preview enhancements you’ll want to be familiar with. Let me know if you want detailed examples or migration guidance on any specific topic!

Here are **all Angular 19 topics** (with **SSR and Angular Material updates skipped**), so you can get fully familiar with the version:

1. **Standalone components, directives, and pipes are now default**
2. **Signals API enhancements**
3. **Linked signals** (experimental)
4. **Resource API** (experimental async logic handling)
5. **After-render effect API** (`afterRenderEffect()`)
6. **Effect API changes** (root/component effects, signal writes allowed)
7. **Template variable syntax stabilized** (`@let` syntax)
8. **Hot Module Replacement (HMR) for styles and templates**
9. **Zoneless change detection (experimental)**
10. **Dependency Injection type inference improvements**
11. **Improved testing support** (esbuild builder, Jest/Web Test Runner support)

Let me know if you want a brief explanation of any item.

https://angular.dev/guide/signals

# Angular 19 Enhanced Reactivity Primitives: Detailed Information with Examples

## 1. **Signal API - Core Foundation**

Signals are the foundational reactive primitive in Angular 19. They provide a way to manage state that automatically notifies consumers when values change.

### Basic Signal Example:

```tsx
import { signal } from '@angular/core';

// Create a signal
const count = signal(0);

// Read the value
console.log(count()); // 0

// Update the value
count.set(5);
count.update(current => current + 1);

```

## 2. **linkedSignal() - Enhanced Signal Management**

The linkedSignal function creates a writable signal that automatically updates its value based on changes in a source signal. This solves the limitation of computed signals being read-only.

### Key Features:

- Creates writable signals that depend on other signals
- Automatically synchronizes with source signals
- Supports independent updates
- Simplifies reset patterns

### Basic linkedSignal Example:

```tsx
import { signal, linkedSignal } from '@angular/core';

const sourceSignal = signal(0);
const updatedSignal = linkedSignal({
  source: sourceSignal,
  computation: () => sourceSignal() * 5,
});

// updatedSignal will always be 5x the sourceSignal value
console.log(updatedSignal()); // 0
sourceSignal.set(10);
console.log(updatedSignal()); // 50

// Can also be updated independently
updatedSignal.set(100);

```

### Advanced linkedSignal Example:

```tsx
import { signal, linkedSignal } from '@angular/core';

// User selection scenario
const availableOptions = signal(['option1', 'option2', 'option3']);
const selectedOption = linkedSignal({
  source: availableOptions,
  computation: (options) => {
    // Keep previous selection if it still exists, otherwise select first
    const current = selectedOption?.();
    return options.includes(current) ? current : options[0];
  }
});

// Initial state
console.log(selectedOption()); // 'option1'

// User selects option2
selectedOption.set('option2');
console.log(selectedOption()); // 'option2'

// Options change but option2 still exists
availableOptions.set(['option2', 'option4', 'option5']);
console.log(selectedOption()); // 'option2' (retained)

// Options change and option2 no longer exists
availableOptions.set(['option6', 'option7']);
console.log(selectedOption()); // 'option6' (reset to first)

```

## 3. **Resource API - Streamlined Asynchronous Data Loading**

The Resource API offers a reactive approach to loading resources, particularly for read operations like HTTP GET requests. It manages loading states automatically and provides built-in error handling.

### Key Features:

- Automatic status tracking (Idle, Loading, Resolved, Error, etc.)
- Built-in error handling
- Local data updates without refetching
- Automatic request cancellation
- Dependency tracking

### Basic Resource Example:

```tsx
import { resource } from '@angular/core';

const productResource = resource({
  loader: async () => {
    const response = await fetch('https://api.example.com/products');
    if (!response.ok) {
      throw new Error('Failed to fetch products');
    }
    return response.json();
  }
});

// Access different states
console.log(productResource.status()); // 2 (Loading)
console.log(productResource.isLoading()); // true
console.log(productResource.value()); // undefined initially
console.log(productResource.error()); // null if no error

```

### Advanced Resource Example with Dependencies:

```tsx
import { resource, signal } from '@angular/core';

const userId = signal(1);
const userResource = resource({
  request: () => ({ userId: userId() }),
  loader: async ({ request }) => {
    const response = await fetch(`/api/users/${request.userId}`);
    return response.json();
  }
});

// Resource automatically reloads when userId changes
userId.set(2); // Triggers new API call

// Status values:
// 0: Idle
// 1: Error
// 2: Loading
// 3: Reloading
// 4: Resolved
// 5: Local

```

### Resource with Local Updates:

```tsx
import { resource } from '@angular/core';

const todosResource = resource({
  loader: async () => {
    const response = await fetch('/api/todos');
    return response.json();
  }
});

// Update locally without refetching
todosResource.update(currentTodos => [
  ...currentTodos,
  { id: Date.now(), text: 'New todo', completed: false }
]);

// Force reload from server
todosResource.reload();

```

## 4. **Practical Component Example**

Here's how these primitives work together in a real component:

```tsx
import { Component, signal, linkedSignal, resource } from '@angular/core';

@Component({
  selector: 'app-user-dashboard',
  template: `
    <div>
      <h2>User Dashboard</h2>

      <!-- User selection -->
      <select [value]="selectedUserId()" (change)="selectUser($event)">
        <option *ngFor="let user of users.value()" [value]="user.id">
          {{user.name}}
        </option>
      </select>

      <!-- Loading state -->
      <div *ngIf="userDetails.isLoading()">Loading user details...</div>

      <!-- Error state -->
      <div *ngIf="userDetails.error()" class="error">
        Error: {{userDetails.error()?.message}}
      </div>

      <!-- Success state -->
      <div *ngIf="userDetails.value()">
        <h3>{{userDetails.value().name}}</h3>
        <p>Email: {{userDetails.value().email}}</p>
        <p>Posts: {{filteredPosts().length}}</p>
      </div>
    </div>
  `
})
export class UserDashboardComponent {
  // Basic signal for user selection
  selectedUserId = signal(1);

  // Resource for loading all users
  users = resource({
    loader: async () => {
      const response = await fetch('/api/users');
      return response.json();
    }
  });

  // Resource that depends on selectedUserId
  userDetails = resource({
    request: () => ({ userId: this.selectedUserId() }),
    loader: async ({ request }) => {
      const response = await fetch(`/api/users/${request.userId}`);
      return response.json();
    }
  });

  // All posts resource
  allPosts = resource({
    loader: async () => {
      const response = await fetch('/api/posts');
      return response.json();
    }
  });

  // Linked signal that filters posts based on selected user
  filteredPosts = linkedSignal({
    source: this.selectedUserId,
    computation: () => {
      const posts = this.allPosts.value() || [];
      return posts.filter(post => post.userId === this.selectedUserId());
    }
  });

  selectUser(event: Event) {
    const target = event.target as HTMLSelectElement;
    this.selectedUserId.set(parseInt(target.value));
  }
}

```

## Benefits of These Primitives:

1. **Simplified State Management**: No more complex RxJS operators for basic reactivity
2. **Automatic Dependency Tracking**: Changes propagate automatically
3. **Built-in Loading States**: No manual loading state management
4. **Error Handling**: Automatic error capture and propagation
5. **Performance**: Fine-grained reactivity with minimal re-renders
6. **Type Safety**: Full TypeScript support with proper inference
7. **Testability**: Easier to test reactive state changes

These primitives represent a significant shift towards a more reactive, signal-based architecture in Angular, making state management and asynchronous operations much more straightforward and maintainable.

https://claude.ai/public/artifacts/f850c355-0856-44d5-8483-730cd6ad1304

// ==================================================
// 1. Basic resource() Function Usage
// ==================================================

import { Component, signal, resource } from '@angular/core';
import { HttpClient } from '@angular/common/http';

interface User {
id: number;
name: string;
email: string;
}

@Component({
selector: 'app-user-profile',
template: `
<div>
<h2>User Profile</h2>

```
  <!-- Show loading state -->
  @if (userResource.isLoading()) {
    <p>Loading user data...</p>
  }

  <!-- Show error state -->
  @if (userResource.error()) {
    <p class="error">Error: {{ userResource.error()?.message }}</p>
  }

  <!-- Show data -->
  @if (userResource.value()) {
    <div class="user-card">
      <h3>{{ userResource.value()?.name }}</h3>
      <p>Email: {{ userResource.value()?.email }}</p>
      <p>ID: {{ userResource.value()?.id }}</p>
    </div>
  }

  <button (click)="loadUser(2)">Load User 2</button>
  <button (click)="loadUser(3)">Load User 3</button>
</div>

```

`
})
export class UserProfileComponent {
private http = inject(HttpClient);

// Signal to track which user ID to load
userId = signal(1);

// Create a resource that depends on userId signal
userResource = resource({
request: () => ({ id: this.userId() }),
loader: async ({ request }) => {
// Simulate API call with Promise
const response = await fetch(`/api/users/${request.id}`);
return response.json() as Promise<User>;
}
});

loadUser(id: number) {
this.userId.set(id); // This will trigger the resource to reload
}
}

// ==================================================
// 2. Resource API Interface Usage
// ==================================================

import { Resource, ResourceStatus } from '@angular/core';

@Component({
selector: 'app-data-manager',
template: `
<div>
<h2>Data Manager</h2>

```
  <!-- Generic resource display -->
  <div class="resource-info">
    <p>Status: {{ getStatusText(dataResource.status()) }}</p>
    <p>Is Loading: {{ dataResource.isLoading() }}</p>
    <p>Has Error: {{ !!dataResource.error() }}</p>
  </div>

  @if (dataResource.value()) {
    <pre>{{ dataResource.value() | json }}</pre>
  }

  <button (click)="refreshData()">Refresh Data</button>
</div>

```

`
})
export class DataManagerComponent {
private http = inject(HttpClient);

// Using Resource API interface for type safety
dataResource: Resource<any> = resource({
loader: async () => {
// Simulate async operation
await new Promise(resolve => setTimeout(resolve, 1000));
return {
timestamp: new Date().toISOString(),
data: 'Sample data loaded!'
};
}
});

// Helper method to work with Resource API
getStatusText(status: ResourceStatus): string {
switch (status) {
case ResourceStatus.Idle: return 'Idle';
case ResourceStatus.Loading: return 'Loading';
case ResourceStatus.Resolved: return 'Resolved';
case ResourceStatus.Error: return 'Error';
case ResourceStatus.Reloading: return 'Reloading';
default: return 'Unknown';
}
}

refreshData() {
this.dataResource.reload();
}
}

// ==================================================
// 3. Advanced resource() with Dependencies
// ==================================================

@Component({
selector: 'app-posts-list',
template: `
<div>
<h2>Posts by Category</h2>

```tsx
  <select (change)="onCategoryChange($event)">
    <option value="">All Categories</option>
    <option value="tech">Technology</option>
    <option value="news">News</option>
    <option value="sports">Sports</option>
  </select>

  @if (postsResource.isLoading()) {
    <div class="loading">Loading posts...</div>
  }

  @if (postsResource.error()) {
    <div class="error">
      Failed to load posts: {{ postsResource.error()?.message }}
      <button (click)="postsResource.reload()">Retry</button>
    </div>
  }

  @if (postsResource.value()) {
    <div class="posts-grid">
      @for (post of postsResource.value(); track post.id) {
        <div class="post-card">
          <h3>{{ post.title }}</h3>
          <p>{{ post.excerpt }}</p>
          <small>Category: {{ post.category }}</small>
        </div>
      }
    </div>
  }
</div>

```

`
})
export class PostsListComponent {
private http = inject(HttpClient);

// Signals for filtering
selectedCategory = signal<string>('');
searchTerm = signal<string>('');

// Resource with multiple dependencies
postsResource = resource({
request: () => ({
category: this.selectedCategory(),
search: this.searchTerm()
}),
loader: async ({ request, abortSignal }) => {
// Build query parameters
const params = new URLSearchParams();
if (request.category) params.set('category', request.category);
if (request.search) params.set('search', request.search);

```
  // Use abort signal for cancellation
  const response = await fetch(`/api/posts?${params}`, {
    signal: abortSignal
  });

  if (!response.ok) {
    throw new Error(`Failed to fetch posts: ${response.statusText}`);
  }

  return response.json();
}

```

});

onCategoryChange(event: Event) {
const target = event.target as HTMLSelectElement;
this.selectedCategory.set(target.value);
}
}

// ==================================================
// 4. Using rxResource() with Observables
// ==================================================

import { rxResource } from '@angular/core';
import { switchMap, catchError } from 'rxjs/operators';
import { of } from 'rxjs';

@Component({
selector: 'app-reactive-data',
template: `
<div>
<h2>Reactive Data with rxResource</h2>

```
  <input
    #searchInput
    (input)="searchQuery.set(searchInput.value)"
    placeholder="Search..."
  />

  @if (searchResource.isLoading()) {
    <div>Searching...</div>
  }

  @if (searchResource.value()) {
    <div class="results">
      @for (item of searchResource.value(); track item.id) {
        <div class="result-item">{{ item.title }}</div>
      }
    </div>
  }
</div>

```

`
})
export class ReactiveDataComponent {
private http = inject(HttpClient);

searchQuery = signal('');

// Using rxResource with Observable
searchResource = rxResource({
request: () => ({ query: this.searchQuery() }),
loader: ({ request }) => {
if (!request.query) {
return of([]);
}

```
  return this.http.get<any[]>(`/api/search?q=${request.query}`).pipe(
    catchError(error => {
      console.error('Search error:', error);
      return of([]);
    })
  );
}

```

});
}

// ==================================================
// 5. Resource API Type Guards and Utilities
// ==================================================

import { ResourceRef } from '@angular/core';

// Utility functions for working with Resource API
export class ResourceUtils {

// Type guard to check if resource has data
static hasData<T>(resource: Resource<T>): resource is Resource<T> & { value(): T } {
return resource.status() === ResourceStatus.Resolved && resource.value() !== undefined;
}

// Type guard to check if resource is in error state
static hasError<T>(resource: Resource<T>): resource is Resource<T> & { error(): Error } {
return resource.status() === ResourceStatus.Error && resource.error() !== undefined;
}

// Generic resource state handler
static handleResourceState<T>(
resource: Resource<T>,
handlers: {
loading?: () => void;
error?: (error: Error) => void;
success?: (data: T) => void;
}
) {
if (resource.isLoading() && handlers.loading) {
handlers.loading();
} else if (this.hasError(resource) && handlers.error) {
handlers.error(resource.error());
} else if (this.hasData(resource) && handlers.success) {
handlers.success(resource.value());
}
}
}

// ==================================================
// 6. Custom Resource Hook Pattern
// ==================================================

// Custom composable for user data
export function useUserData(userId: Signal<number>) {
const http = inject(HttpClient);

return resource({
request: () => ({ id: userId() }),
loader: async ({ request }) => {
const response = await fetch(`/api/users/${request.id}`);
if (!response.ok) {
throw new Error(`User not found: ${response.status}`);
}
return response.json() as Promise<User>;
}
});
}

// Usage in component
@Component({
selector: 'app-user-details',
template:     `<div>       @if (userResource.isLoading()) {         <p>Loading user...</p>       }       @if (userResource.error()) {         <p>Error: {{ userResource.error()?.message }}</p>       }       @if (userResource.value()) {         <h2>{{ userResource.value()?.name }}</h2>       }     </div>`  
})
export class UserDetailsComponent {
userId = signal(1);
userResource = useUserData(this.userId);
}



The `@defer` block is a powerful new built-in primitive for **lazy-loading** components, directives, and pipes in your template. It's designed to improve application performance by delaying the loading of non-critical parts of your application until they are actually needed, reducing the initial bundle size and improving the initial load time.

It's a more declarative and streamlined way to achieve lazy-loading compared to traditional router-based lazy-loading or dynamic imports.

### The Core Concept of `@defer`

The `@defer` block works by telling Angular to only download the code for the deferred content (e.g., a component) when a specific condition, known as a **trigger**, is met. This content is then rendered and hydrated, becoming a part of the application.

### The Basic Structure

The `@defer` block can contain three main parts:

  * **`@placeholder` (Optional):** Content to be displayed while the deferred code is being loaded, *before* the trigger is met. This is useful for preventing layout shifts.
  * **`@loading` (Optional):** Content to be displayed while the deferred code is *actually being downloaded*. This is great for showing a spinner or a loading message.
  * **`@error` (Optional):** Content to be displayed if the lazy-loading fails.

### `@defer` Triggers

You can configure exactly when the deferred content should load by using a `trigger` on the `@defer` block. Here are the most common ones:

  * **`on viewport`:** The content loads when it enters the user's viewport. This is one of the most common and useful triggers for content "below the fold."
  * **`on idle`:** The content loads when the browser becomes idle (using the `requestIdleCallback` API). This is a great way to load non-critical content without blocking the main thread.
  * **`on interaction`:** The content loads when the user interacts with a specific element within the placeholder. You can also specify a target element using a template reference variable, e.g., `on interaction(myButton)`.
  * **`on hover`:** The content loads when the user hovers over the deferred block.
  * **`on immediate`:** The content loads as soon as the browser can. This is an alternative to `on idle` that is more aggressive.
  * **`on timer(...)`:** The content loads after a specified duration (e.g., `on timer(5s)`).
  * **`when <expression>`:** The content loads when a boolean expression becomes `true`. This is useful for custom triggers.

### Example: Lazy-Loading a Comment Section

Let's imagine we have a news article page. The comments section is a good candidate for lazy-loading because it's not critical for the initial page load.

#### Step 1: Create the Lazy-Loaded Component

First, create a new standalone component for the comments. This component is just a regular component.

```bash
ng generate component comments --standalone
```

**`comments.component.ts`**

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-comments',
  standalone: true,
  template: `
    <h3>Comments Section</h3>
    <p>This component was lazy-loaded!</p>
    <ul>
      <li>This is the first comment.</li>
      <li>Another insightful comment here.</li>
      <li>One more comment for good measure.</li>
    </ul>
  `,
})
export class CommentsComponent {}
```

#### Step 2: Use `@defer` in the Parent Component

Now, in your main article component, you'll use the `@defer` block to load the `CommentsComponent`.

**`article.component.ts`**

```typescript
import { Component } from '@angular/core';
import { CommonModule } from '@angular/common';
import { CommentsComponent } from './comments.component';

@Component({
  selector: 'app-article',
  standalone: true,
  // Note: We do NOT import CommentsComponent in the imports array here,
  // because it will be lazy-loaded by @defer.
  template: `
    <article>
      <h1>Angular's New `@defer` Block</h1>
      <p>This is the main article content. The comments section below will be lazy-loaded.</p>
    </article>

    <div class="comments-section-container">
      @defer (on viewport) {
        <app-comments />
      } @placeholder {
        <p>Comments section will load when you scroll down...</p>
      } @loading {
        <p>Loading comments...</p>
      } @error {
        <p>Failed to load comments. Please try again later.</p>
      }
    </div>
  `,
})
export class ArticleComponent {}
```

### Breakdown of the Example

  * **`@defer (on viewport)`:** This is the trigger. The content inside the `@defer` block will only be loaded when the user scrolls the "comments-section-container" div into view.
  * **`<app-comments />`:** This is the component that will be lazy-loaded. Angular automatically handles the dynamic import behind the scenes.
  * **`@placeholder`:** When the page first loads, the user sees "Comments section will load when you scroll down..." This ensures a seamless user experience and prevents layout shifts.
  * **`@loading`:** After the user scrolls and the trigger fires, this content briefly appears while the browser downloads the `comments.component.ts` code.
  * **`@error`:** If the download fails for any reason (e.g., network issue), this block will be displayed.

### Other Useful Triggers

Here's how you could use other triggers in the same scenario:

**On Interaction:**

```html
@defer (on interaction) {
  <app-comments />
} @placeholder {
  <p>Click here to load comments.</p>
}
```

In this case, the comments would load only when the user clicks on the placeholder.

**On Timer:**

```html
@defer (on timer(3s)) {
  <app-comments />
} @placeholder {
  <p>Comments are loading in 3 seconds...</p>
}
```

This would automatically start loading the comments after 3 seconds, regardless of user interaction.
