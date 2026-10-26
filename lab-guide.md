# Lab Guide: Modernizing a legacy Java Swing Application to React and Springboot with IBM Bob

## Prerequisites

Before starting this lab, ensure you have the following installed and available:

- **IBM Bob** with the **Java Premium Package** add-on enabled
- **Java 17** installed on your system (Oracle JDK or compatible distribution)

> **Note:** Certain steps and outputs in this guide may look different from what you see in IBM Bob. LLM responses are not deterministic, so Bob's exact wording, tool call sequences, and summaries may vary between runs.

## 1. Running the Legacy Swing Application

### Step 1: Clone the Github Repo
Run this command in terminal.
```bash
git clone https://github.com/SuyashGupte/patient-management-system
```

### Step 2: Run the application with Gradle

Open a terminal in the `patient-management-system` project and run following commands:
```bash
bobide .
```

```bash
./gradlew run
```

![Screenshot](images/1.png)

### Step 3: Log in

The **Welcome** screen opens. Enter your username as `Admin` and password as `Password`, then click **LOGIN**.

![Screenshot](images/2.png)

### Step 4: Browse the patient list

![Screenshot](images/3.png)

### Step 5: Open a patient record

Select a patient, for example **Daniel Radcliffe**. The detail screen shows the patient photo, personal details, appointment, billing and insurance, medical condition, comments and medical images. Use the back arrow to return to the list, or the save icon to save changes.

![Screenshot](images/4.png)

## 2. Java Upgrade

### Step 6: Start the Java Modernization workflow

In the IBM Bob panel toolbar, the first icon (play) opens **Bob workflows**.

![Screenshot](images/5.png)

Expand **Java Modernization** and review its options:

- **Java Upgrade** upgrades the project to a newer Java version.
- **Liberty Modernization** moves the application to WebSphere Liberty. It requires an AMA zip file.
- **UI Modernization** transforms JSP, JSF or Struts applications into a Java backend and a React frontend.

Click **Start** next to **Java Modernization**.

![Screenshot](images/6.png)

### Step 7: Analyze the project

The workflow opens at **Analyze Project (1/3)**. Select the project, for example `/Users/<user>/Documents/work/patient-management-system`. Leave **Custom project path** and **Custom build command** off, then click **Continue**.

![Screenshot](images/7.png)

Bob then asks for approval to run two tools. Click **Approve once** for each, or **Approve execute tools for task** to approve all tool calls for the task:

- **Query vulnerabilities** checks the detected dependencies, for example `org.junit.jupiter:junit-jupiter-engine` version `5.3.1`.
- **Building Java project** runs `./gradlew build` on the project path.

![Screenshot](images/8.png)

![Screenshot](images/9.png)

Bob reports **"2 errors found during initial build."** and asks **"Do you want me to fix the project?"**

- **Yes** lets Bob fix the errors.
- **No, proceed with workflow** continues without fixing them. Select this option.

![Screenshot](images/10.png)

### Step 8: Select the Modernization Type

In the **Flow Selection** screen under **Modernization Type**, select **Java Upgrade** ("Upgrade your Java application to a newer version"). Leave **Enable Git Flow** disabled and click **Continue**. Note that Liberty Modernization and UI Modernization are automatically disabled if Bob detects no supported application server or UI components.

![Screenshot](images/11.png)

### Step 9: Configure the Java Upgrade

Bob checks whether the required tools (such as SDKMAN!) are installed. When Bob requests approval to execute `source ~/.sdkman/bin/sdkman-init.sh && sdk version`, click **Approve once** (or **Approve for task**).

![Screenshot](images/12.png)

Bob then presents the **Java Upgrade Configuration** screen. Choose the target **Java Distribution** as **Oracle JDK** and **Java Version** as **Java 17**. Review the migration summary, key technical challenges, complexity rating, and vulnerability assessment, then click **Continue**.

![Screenshot](images/13.png)

### Step 10: Run the upgrade recipe and fix build issues

Bob runs the OpenRewrite migration recipe and verifies the result. Click **Approve once** for each of these prompts:

- **Run recipe: UpgradeToJava17** (`org.openrewrite.java.migrate.UpgradeToJava17`)
- **Building Java project** (`./gradlew build`), to detect any remaining build or migration issues
- **Execute subtask: Fixing issues in patient-management-system**. The build finishes with 0 errors and 2 warnings, and Bob starts a subtask to address them.

![Screenshot](images/14.png)

![Screenshot](images/15.png)

![Screenshot](images/16.png)

### Step 11: Query vulnerabilities for dependencies

After the build fix subtask, Bob transitions to the **Java Vulnerability Remediation** workflow. It extracts the project dependencies (40 dependencies found, 23 unique) and checks them for known CVEs. When prompted to approve the **Query vulnerabilities** tool , click **Approve once** or **Approve execute tools for task**.

![Screenshot](images/17.png)

### Step 12: Confirm vulnerability remediation

Bob completes the vulnerability scan and finds 18 vulnerabilities across the dependencies. Under **Vulnerabilities fixing**, Bob asks how to proceed:

- **Yes, resolve all** (resolves all detected vulnerabilities)
- **Yes, select subset** (lets you choose which vulnerabilities to remediate)
- **No** (skips remediation)

Click **Yes, resolve all**.

![Screenshot](images/18.png)

### Step 13: Approve the fix and validation subtasks

Bob plans the safe dependency upgrades, then runs the **Fix Vulnerabilities**, **Validate Fixes** and **Final step** subtasks, followed by a final `./gradlew build`. Click **Approve once** (or the matching **Approve ... for task** option) each time Bob asks for approval, including:

- **Execute subtask** prompts for each of the three subtasks
- The **Fix Vulnerabilities** todo plan
- **Complete subtask** prompts at the end of **Validate Fixes** and **Final step**
- **Building Java project** (`./gradlew build`) for the final validation


![Screenshot](images/21.png)

### Step 14: Review the cleared vulnerabilities

The **Fix Vulnerabilities** subtask completes with **All tasks completed! (6/6)**. Bob lists every cleared advisory under **Vulnerabilities cleared**, 

Bob then asks for approval to **Complete subtask** with the full remediation summary. Click **Approve once**.

![Screenshot](images/23.png)

### Step 15: Review the Java Modernization summary

When the workflow finishes, Bob displays a **Modernization Visualization** diagram of all steps performed, followed by the **Summary**:

> *Project's Java version was **upgraded from 1.8 to 17**. Used Oracle Java distribution. Build **completed successfully** with no errors or warnings.*

![Screenshot](images/28.png)

Bob closes with:

> *"Java Modernization workflow has been finished. If there are any problems or questions, please ask me here in the chat."*

A **New task** button appears in the bottom-right corner.

![Screenshot](images/29.png)

## 3. Swing to React

### Step 16: Enter the UI modernization prompt

Start a new task. In the Agent mode chat input, type the following prompt and press **Send**:

```
Convert this java swing based application to react based web app using vite. Use material UI for the design.
Use springboot for backend.
Create a separate backend and frontend folder for the modernized code. Do not modify exsiting code.
Ensure all the functionality is maintained and verify database connections are working.
```

![Screenshot](images/30.png)

### Step 17: Approve the skill and the todo plan

Bob detects the UI modernization request and asks for approval to **Use Skill java-ui-modernization**. Click **Approve once** (or **Approve skill tools for task**) to let Bob load its specialized UI modernization instructions.

![Screenshot](images/31.png)

Bob explores the application structure, then presents its planned **Update Todo List**:

Click **Approve once** (or **Approve todo tools for task**) to begin the conversion.

![Screenshot](images/32.png)

### Step 18: Approve the scaffolding and build prompts

While Bob builds the backend and frontend, it asks for approval to run several commands. Click **Approve once** (or **Approve for task**) for each subtask.

![Screenshot](images/34.png)

### Step 19: UI modernization complete — review what was created

All todos complete. Bob displays a full summary under **What was created**:

![Screenshot](images/38.png)

### Step 20: Run the backend and the frontend

In a terminal, start the Spring Boot backend. This command will change based on your system. If you are not sure ask Bob "How to run this application?":

```bash
cd backend
JAVA_HOME=~/.sdkman/candidates/java/<java-17-version> ./gradlew bootRun
```


The backend REST API is now live at **http://localhost:8080**.

![Screenshot](images/40.png)

In a second terminal, start the frontend dev server:

```bash
cd frontend
npm install && npm run dev
```

![Screenshot](images/39.png)

### Step 21: Verify the modernized React application

Open the frontend URL printed by Vite (**http://localhost:5173** by default, or **http://localhost:5174** if 5173 is already in use) in a browser.

**Login page (`/login`).** The new React login page replaces the original Java Swing welcome dialog with clean Material UI card. Enter your username as `Admin` and password as `Password`.

![Screenshot](images/41.png)

![Screenshot](images/42.png)

![Screenshot](images/43.png)

## 4. Java Unit Tests
### Step 22: Open the `backend` folder in a new Bob window.
In a terminal with current directory as `backend`. Run the following command
```bash 
bobide .
```

### Step 23: Start the workflow, add JaCoCo and generate the test strategy

Click the **play (▶)** icon in the IBM Bob toolbar to reopen the **Bob workflows** panel. Three workflows are listed:

- **Java Modernization** — Java Upgrade, Liberty Modernization, UI Modernization
- **Java Unit Testing** — run, update, and create unit tests to increase code coverage
- **Java Vulnerability Remediation** — scan and fix CVEs in dependencies

Click **Start** next to **Java Unit Testing**.

![Screenshot](images/42.png)

The workflow starts with installing JaCoCo library for code coverage reporting. Click **Approve once** (or **Approve all subtask tools for this task**) for each of these prompts:

- **Execute subtask: Add JaCoCo library (java-modernization)**, with a three-item todo plan: analyze the project's build files, install JaCoCo library, verify successful installation

![Screenshot](images/47.png)

Bob then generates Unit Test Strategy. Approve **Execute subtask: Generate Unit Test Strategy (java-modernization)**. Its plan is to analyze the project, gather key information about unit testing the codebase, and create the unit testing strategy file.

![Screenshot](images/48.png)

### Step 24: Configure unit test generation options and continue

The workflow reaches step **3/8 — Select Action**. Both the **Add JaCoCo library** and **Generate Unit Test Strategy** subtasks are now marked complete. Bob presents the **Select Tasks** configuration panel:

| Option | State |
|---|---|
| Re-generate Unit Test Strategy | Off |
| Generate Unit Tests | **On** |
| Candidate Selection Strategy | **All classes** |
| Run Code Coverage | **On** |
| Enable Git Flow | Off |

Review the settings, then click **Continue**.

![Screenshot](images/49.png)

### Step 25: Confirm the plan and approve the write-unit-test skill

Bob gathers unit test candidates using the **All classes** strategy and displays a **Confirmation** dialog:

Click **Proceed with test generation**.

![Screenshot](images/50.png)

Bob runs the batches in parallel. Click **Approve once** (or **Approve skill tools for task**).

![Screenshot](images/51.png)

### Step 26: Java Unit Testing workflow complete — review the summary

The **Java Unit Testing** workflow finishes with **All tasks completed!**. Bob displays a **Modernization Visualization** diagram of all subtasks, then the **Summary**.

![Screenshot](images/54.png)

## 5. Java Vulnerability Remediation

### Step 27: Scan the modernized backend for vulnerabilities

Open the **Bob workflows** panel and click **Start** next to **Java Vulnerability Remediation** 

![Screenshot](images/52.png)

The workflow starts with detecting vulnerabilities. This vulnerabilities list might change in future.

![Screenshot](images/53.png)

The workflow finishes with **All tasks completed!**. You might see some vulnerabilities listed here. Just approve the subtasks let Bob fix those vulnerabilities.

![Screenshot](images/55.png)
