# LifeOS Database Schema

This document outlines the database schema for the LifeOS personal management system.

---

## Table: `goals`

**Purpose**: This table stores high-level goals and ambitions. It is the core of the "Direction To Destination" module.

| Column Name      | Data Type                                                    | Constraints                               | Description                                                    |
| ---------------- | ------------------------------------------------------------ | ----------------------------------------- | ------------------------------------------------------------   |
| `goal_id`        | `INT UNSIGNED`                                               | `AUTO_INCREMENT`, `PRIMARY KEY`           | The unique identifier for each goal.                           |
| `parent_goal_id` | `INT UNSIGNED`                                               | `NULL`                                    | An optional link to a parent goal's `goal_id`.                 |
| `title`          | `VARCHAR(255)`                                               | `NOT NULL`                                | The short, inspiring name of the goal.                         |
| `description`    | `TEXT`                                                       | `NULL`                                    | A detailed explanation of the goal's purpose and "why".        |
| `status`         | `ENUM('Not Started', 'In Progress', 'Completed', 'On Hold')` | `NOT NULL`, `DEFAULT 'Not Started'`       | The current operational state of the goal.                     |
| `inspiration_date` | `DATETIME`                                                 | `NULL`                                    | The user-defined date and time of the goal's inspiration.      |
| `target_date`    | `DATE`                                                       | `NULL`                                    | The optional deadline for achieving the goal.                  |
| `creation_date`  | `TIMESTAMP`                                                  | `NOT NULL`, `DEFAULT CURRENT_TIMESTAMP`   | The automatic system timestamp of when the record was created. |

### Relationships

* **`parent_goal_id`**: This column can optionally reference the `goal_id` of another row in this **same table**. This creates a self-referencing, hierarchical relationship, allowing for goals and sub-goals.