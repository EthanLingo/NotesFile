
# VScode自带变量

#内容/自动办公 #内容/vscode 

Variables Reference

Visual Studio Code supports variable substitution in [Debugging](https://code.visualstudio.com/docs/editor/debugging) and [Task](https://code.visualstudio.com/docs/editor/tasks) configuration files as well as some select settings. Variable substitution is supported inside key and value strings in launch.json and tasks.json files using ${variableName} syntax.

Predefined variables[#](https://code.visualstudio.com/docs/editor/variables-reference#_predefined-variables)

The following predefined variables are supported:

-   ${workspaceFolder} - the path of the folder opened in VS Code
-   ${workspaceFolderBasename} - the name of the folder opened in VS Code without any slashes (/)
-   ${file} - the current opened file
-   ${relativeFile} - the current opened file relative to workspaceFolder
-   ${relativeFileDirname} - the current opened file's dirname relative to workspaceFolder
-   ${fileBasename} - the current opened file's basename
-   ${fileBasenameNoExtension} - the current opened file's basename with no file extension
-   ${fileDirname} - the current opened file's dirname
-   ${fileExtname} - the current opened file's extension
-   ${cwd} - the task runner's current working directory on startup
-   ${lineNumber} - the current selected line number in the active file
-   ${selectedText} - the current selected text in the active file
-   ${execPath} - the path to the running VS Code executable
-   ${defaultBuildTask} - the name of the default build task

Predefined variables examples[#](https://code.visualstudio.com/docs/editor/variables-reference#_predefined-variables-examples)

Supposing that you have the following requirements:

1.  A file located at /home/your-username/your-project/folder/file.ext opened in your editor;
2.  The directory /home/your-username/your-project opened as your root workspace.

So you will have the following values for each variable:

-   ${workspaceFolder} - /home/your-username/your-project
-   ${workspaceFolderBasename} - your-project
-   ${file} - /home/your-username/your-project/folder/file.ext
-   ${relativeFile} - folder/file.ext
-   ${relativeFileDirname} - folder
-   ${fileBasename} - file.ext
-   ${fileBasenameNoExtension} - file
-   ${fileDirname} - /home/your-username/your-project/folder
-   ${fileExtname} - .ext
-   ${lineNumber} - line number of the cursor
-   ${selectedText} - text selected in your code editor
-   ${execPath} - location of Code.exe

Tip: Use IntelliSense inside string values for tasks.json and launch.json to get a full list of predefined variables.

Variables scoped per workspace folder[#](https://code.visualstudio.com/docs/editor/variables-reference#_variables-scoped-per-workspace-folder)

By appending the root folder's name to a variable (separated by a colon), it is possible to reach into sibling root folders of a workspace. Without the root folder name, the variable is scoped to the same folder where it is used.

For example, in a multi root workspace with folders Server and Client, a ${workspaceFolder:Client} refers to the path of the Client root.

Environment variables[#](https://code.visualstudio.com/docs/editor/variables-reference#_environment-variables)

You can also reference environment variables through the ${env:Name} syntax (for example, ${env:USERNAME}).

{  
  "type": "node",  
  "request": "launch",  
  "name": "Launch Program",  
  "program": "${workspaceFolder}/app.js",  
  "cwd": "${workspaceFolder}",  
  "args": ["${env:USERNAME}"]  
}

Configuration variables[#](https://code.visualstudio.com/docs/editor/variables-reference#_configuration-variables)

You can reference VS Code settings ("configurations") through ${config:Name} syntax (for example, ${config:editor.fontSize}).

Command variables[#](https://code.visualstudio.com/docs/editor/variables-reference#_command-variables)

If the predefined variables from above are not sufficient, you can use any VS Code command as a variable through the ${command:commandID} syntax.

A command variable is replaced with the (string) result from the command evaluation. The implementation of a command can range from a simple calculation with no UI, to some sophisticated functionality based on the UI features available via VS Code's extension API.

An example of this functionality is in VS Code's Node.js debugger extension, which provides an interactive command extension.pickNodeProcess for selecting a single process from the list of all running Node.js processes. The command returns the process ID of the selected process. This makes it possible to use the extension.pickNodeProcess command in an Attach by Process ID launch configuration in the following way:

{  
  "configurations": [  
    {  
      "type": "node",  
      "request": "attach",  
      "name": "Attach by Process ID",  
      "processId": "${command:extension.pickNodeProcess}"  
    }  
  ]  
}

Input variables[#](https://code.visualstudio.com/docs/editor/variables-reference#_input-variables)

Command variables are already powerful but they lack a mechanism to configure the command being run for a specific use case. For example, it is not possible to pass a prompt message or a default value to a generic "user input prompt".

This limitation is solved with input variables which have the syntax: ${input:variableID}. The variableID refers to entries in the inputs section of launch.json and tasks.json, where additional configuration attributes are specified.

The following example shows the overall structure of a task.json that makes use of input variables:

{  
  "version": "2.0.0",  
  "tasks": [  
    {  
      "label": "task name",  
      "command": "${input:variableID}"  
      // ...  
    }  
  ],  
  "inputs": [  
    {  
      "id": "variableID",  
      "type": "type of input variable"  
      // type specific configuration attributes  
    }  
  ]  
}

Currently VS Code supports three types of input variables:

-   promptString: Shows an input box to get a string from the user.
-   pickString: Shows a Quick Pick dropdown to let the user select from several options.
-   command: Runs an arbitrary command.

Each type requires additional configuration attributes:

promptString:

-   description: Shown in the quick input, provides context for the input.
-   default: Default value that will be used if the user doesn't enter something else.
-   password: Set to true to input with a password prompt that will not show the typed value.

pickString:

-   description: Shown in the quick pick, provides context for the input.
-   options: An array of options for the user to pick from.
-   default: Default value that will be used if the user doesn't enter something else. It must be one of the option values.

command:

-   command: Command being run on variable interpolation.
-   args: Optional option bag passed to the command's implementation.

Below is an example of a tasks.json that illustrates the use of inputs using Angular CLI:

{  
  "version": "2.0.0",  
  "tasks": [  
    {  
      "label": "ng g",  
      "type": "shell",  
      "command": "ng",  
      "args": ["g", "${input:componentType}", "${input:componentName}"]  
    }  
  ],  
  "inputs": [  
    {  
      "type": "pickString",  
      "id": "componentType",  
      "description": "What type of component do you want to create?",  
      "options": [  
        "component",  
        "directive",  
        "pipe",  
        "service",  
        "class",  
        "guard",  
        "interface",  
        "enum",  
        "enum"  
      ],  
      "default": "component"  
    },  
    {  
      "type": "promptString",  
      "id": "componentName",  
      "description": "Name your component.",  
      "default": "my-new-component"  
    }  
  ]  
}

Running the example:

![Inputs Example](data:image/png;base64,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)

The following example shows how to use a user input variable of type command in a debug configuration that lets the user pick a test case from a list of all test cases found in a specific folder. It is assumed that some extension provides an extension.mochaSupport.testPicker command that locates all test cases in a configurable location and shows a picker UI to pick one of them. The arguments for a command input are defined by the command itself.

{  
  "configurations": [  
    {  
      "type": "node",  
      "request": "launch",  
      "name": "Run specific test",  
      "program": "${workspaceFolder}/${input:pickTest}"  
    }  
  ],  
  "inputs": [  
    {  
      "id": "pickTest",  
      "type": "command",  
      "command": "extension.mochaSupport.testPicker",  
      "args": {  
        "testFolder": "/out/tests"  
      }  
    }  
  ]  
}

Command inputs can also be used with tasks. In this example, the built-in Terminate Task command is used. It can accept an argument to terminate all tasks.

{  
  "version": "2.0.0",  
  "tasks": [  
    {  
      "label": "Terminate All Tasks",  
      "command": "echo ${input:terminate}",  
      "type": "shell",  
      "problemMatcher": []  
    }  
  ],  
  "inputs": [  
    {  
      "id": "terminate",  
      "type": "command",  
      "command": "workbench.action.tasks.terminate",  
      "args": "terminateAll"  
    }  
  ]  
}

Common questions[#](https://code.visualstudio.com/docs/editor/variables-reference#_common-questions)

Details of variable substitution in a debug configuration or task[#](https://code.visualstudio.com/docs/editor/variables-reference#_details-of-variable-substitution-in-a-debug-configuration-or-task)

Variable substitution in debug configurations or tasks is a two pass process:

-   In the first pass, all variables are evaluated to string results. If a variable occurs more than once, it is only evaluated once.
-   In the second pass, all variables are substituted with the results from the first pass.

A consequence of this is that the evaluation of a variable (for example, a command-based variable implemented in an extension) has no access to other substituted variables in the debug configuration or task. It only sees the original variables. This means that variables cannot depend on each other (which ensures isolation and makes substitution robust against evaluation order).

Is variable substitution supported in User and Workspace settings?[#](https://code.visualstudio.com/docs/editor/variables-reference#_is-variable-substitution-supported-in-user-and-workspace-settings)

The predefined variables are supported in a select number of setting keys in settings.json files such as the terminal cwd, env, shell and shellArgs values. Some [settings](https://code.visualstudio.com/docs/getstarted/settings) like window.title have their own variables:

  "window.title": "${dirty}${activeEditorShort}${separator}${rootName}${separator}${appName}"

Refer to the comments in the Settings editor (⌘,) to learn about setting specific variables.

Why isn't ${workspaceRoot} documented?[#](https://code.visualstudio.com/docs/editor/variables-reference#_why-isnt-workspaceroot-documented)

The variable ${workspaceRoot} was deprecated in favor of ${workspaceFolder} to better align with [Multi-root Workspace](https://code.visualstudio.com/docs/editor/multi-root-workspaces) support.

How can I know a variable's actual value?[#](https://code.visualstudio.com/docs/editor/variables-reference#_how-can-i-know-a-variables-actual-value)

One easy way to check a variable's runtime value is to create a VS Code [task](https://code.visualstudio.com/docs/editor/tasks) to output the variable value to the console. For example, to see the resolved value for ${workspaceFolder}, you can create and run (Terminal > Run Task) the following simple 'echo' task in tasks.json:

{  
  "version": "2.0.0",  
  "tasks": [  
    {  
      "label": "echo",  
      "type": "shell",  
      "command": "echo ${workspaceFolder}"  
    }  
  ]  
}