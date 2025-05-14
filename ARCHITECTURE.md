# Todo List App Architecture

This document outlines the architecture and data flow of our Todo List application.

## Application Structure

The application follows a simple MVC-like pattern:
- HTML (View): Defines the UI structure
- CSS (View): Styles the UI components
- JavaScript (Controller): Handles user interactions and updates the model
- LocalStorage (Model): Stores task data persistently

## Data Flow Diagram

The following Mermaid.js diagram illustrates the data flow in our Todo List application:

```mermaid
flowchart TD
    User([User]) -->|Interacts with| UI[Todo List UI]
    
    %% User Actions
    UI -->|Add Task| AddTask[Add Task Function]
    UI -->|Toggle Task| ToggleTask[Toggle Task Function]
    UI -->|Delete Task| DeleteTask[Delete Task Function]
    UI -->|Filter Tasks| FilterTasks[Filter Tasks Function]
    UI -->|Clear Completed| ClearCompleted[Clear Completed Function]
    
    %% Data Processing
    AddTask -->|Update Model| TaskArray[(Task Array)]
    ToggleTask -->|Update Model| TaskArray
    DeleteTask -->|Update Model| TaskArray
    ClearCompleted -->|Update Model| TaskArray
    
    %% Storage
    TaskArray -->|Save| LocalStorage[(LocalStorage)]
    LocalStorage -->|Load| TaskArray
    
    %% Rendering
    TaskArray -->|Filtered by| FilterTasks
    FilterTasks -->|Render| UI
    
    %% Data Structure
    subgraph "Task Object Structure"
        TaskObj["{<br/>id: number,<br/>text: string,<br/>completed: boolean<br/>}"]
    end
    
    %% Styling
    classDef action fill:#90ee90,stroke:#333,stroke-width:1px
    classDef storage fill:#f9d6a0,stroke:#333,stroke-width:1px
    classDef interface fill:#a2d2ff,stroke:#333,stroke-width:1px
    classDef data fill:#ffc0cb,stroke:#333,stroke-width:1px
    
    class AddTask,ToggleTask,DeleteTask,FilterTasks,ClearCompleted action
    class LocalStorage,TaskArray storage
    class UI interface
    class TaskObj data
```

## Component Interactions

1. **User Input**: User interacts with the UI by adding, completing, or deleting tasks
2. **Event Handling**: JavaScript event listeners capture these interactions
3. **Data Manipulation**: Functions process the interactions and update the task array
4. **Persistence**: Changes are saved to localStorage
5. **Rendering**: The UI is updated to reflect the current state of tasks

## Filter Functionality

The application supports three view filters:
- **All**: Shows all tasks
- **Active**: Shows only uncompleted tasks
- **Completed**: Shows only completed tasks

Filtering is performed in-memory and does not affect the stored tasks.
