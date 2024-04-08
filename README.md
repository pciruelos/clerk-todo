# To Do App for Clerk.io

## About This App

This is a Vue 3 based To-Do application designed specifically for Clerk.io.

## Installation

To get started with the To Do App, you'll need to first clone the project to your local machine and then install its dependencies. Here's how:

1. **Clone the project**:

   ```bash
   git clone https://github.com/pciruelos/clerk-todo.git
   ```

2. **Navigate to the project directory**:

   ```bash
   cd clerk-todo
   ```

3. **Install dependencies**:

   ```bash
   npm install
   ```

## Running the App

Depending on your development stage or purpose, you can run the app in development mode or prepare it for production.

### For Development

To compile and hot-reload for development, use:

   ```bash
    npm run serve
   ```

This command starts a local server. Open http://localhost:8080 to view the app in the browser.

### For Production

To compile and minify the app for production, use:


   ```bash
    npm run build
   ```

This command prepares your app for deployment by optimizing and minifying the files into the `dist` directory.

How to Use the App
------------------

Using the To Do App is intuitive and user-friendly, ensuring your tasks stay updated and saved, even if you decide to close the browser. Here's how:

-   Access the App: Start by navigating to the application using the link from the development server, typically found at http://localhost:8080.
-   To add new tasks, use the navbar. Here, you can enter task details and select a priority level (High, Medium, Low), then click the "Save" button. The priority affects the task's border color, making important tasks stand out visually.
-   Within the main interface, tasks can be directly managed:
*Edit task details or change their priority.
*Mark tasks as complete to track your progress.
*Delete tasks that are no longer needed.
*Add subtasks for detailed organization, allowing you to manage complex projects with ease.
-   Data Persistence: All your tasks and their states are securely saved in localStorage. This means you can close your browser or turn off your device, and when you return, your tasks will be just as you left them.

Highlights of the App
---------------------

-   Vue 3's Composition API and Reactivity System: Prioritizing simplicity and readability. By doing so, it demonstrates that for many applications, a lightweight, direct approach without external state management solutions like Vuex can be incredibly effective. 

-   Efficient State Management: This highlights how well-designed reactivity can eliminate the need for Vuex, EventBus, or prop-drilling through router views for component communication, showcasing a streamlined and efficient approach to managing app state.
-   Component Design: Emphasizes modular and reusable components, showcasing best practices in Vue.js development.

-   Effective data flow between components is achieved through the use of props (for passing down read-only data) and emits (for communication back to parent components), exemplifying best practices in Vue component architecture.
-   Reusability is demonstrated with the TaskForm component, which is used both for adding new tasks and editing existing ones, showcasing the efficiency of Vue components.
-   Tasks are dynamically styled based on their priority, improving the user interface and overall user experience by providing immediate visual cues for task prioritization.
-   The app supports advanced task management through the creation of subtasks, allowing for granular control and organization of tasks.
------------

Improvements
------------------
#### Form Validation

-   Enhance Data Integrity: Implement stronger form validation to ensure task inputs meet our standards, potentially using Vuelidate for concise, declarative validation rules.

#### Type Safety

-   Adopt TypeScript: Transitioning to TypeScript can safeguard against type-related bugs, making our app more robust and easier to maintain by enforcing type safety.

#### Method Refactoring and Abstraction

-   Refactor for Reusability and Maintainability: Abstract common functionalities into reusable services, particularly for task operations such as create, update, and delete. This approach minimizes direct array manipulations and event emissions, centralizing logic for easier testing and scalability. Adopting patterns like the Repository pattern for daata handling can further modularize the code, making it cleaner and more adaptable to changes.