# Package manager

The language is integrated with JetPM, a package manager with support for vital features:

* workspaces;
* specifying a dependency through a directory path;
* registry namespaces.

## Build process

The package manifest represents a JetWork project, and locates its sources; therefore, the package manager is able to build a project through a simple command such as `jetpm build`, resulting into a bytecode artifact.

Here is an example package manifest:

**package.json**

```json
{
    "id": "org.q.f",
    "version": "0.1.0",
    "compilerOptions": {
        "includeSources": ["src"]
    }
}
```

## Registry namespaces

Registry namespaces are required to distinguish platforms on which the JetWork program executes. Platforms may have incompatible implementations, such as regular expressions, or lacking implementations of certain functions, therefore sharing packages between platforms is not allowed in JetPM.

The package manifest's top-level `registryNamespace` option is required and indicates the registry namespace to which the package belongs as well as the namespace on which dependencies are found in the package registry.

Here is an example of a potential package manifest that uses `http://www.airsdk.dev/2008` as its registry namespace:

**package.json**

```json
{
    "id": "org.q.f",
    "version": "0.1.0",
    "registryNamespace": "http://www.airsdk.dev/2008",
    "dependencies": {
        "goog.firebase": "1.0.0"
    }
}
```

Note that registry namespaces are defined internally in the registry and may not be arbitrary. Registry namespaces are available as platforms are supported.

## Conditional configuration

The package manager supports configuration constants that allow for conditional configuration within a manifest through the top-level `conditional` property. The matching options are combined and overriden properly in top-down sequence, including the program sources and the package dependencies.

The conditions in `conditional` support a minimal conditional language:

* `constant` — If constant is present
* `constant=value` — If constant is equals `"value"`
* `!expression` — If condition is false
* `(expression)` — Parenthesized condition
* `primaryExpression && primaryExpression` — If conditions are true
* `primaryExpression || primaryExpression` — If one condition is true
* The root condition is in one of the forms:
  * `always`
  * `if (condition)`
  * `else if (condition)`
  * `else`

Here is an example package manifest using the `conditional` setting:

**package.json**

```json
{
    "conditional": [
        ["always", {
            "compilerOptions": {
                "includeSources": ["src/base"]
            }
        }],
        ["if (air::target=ios)", {
            "compilerOptions": {
                "includeSources": ["src/platform/ios"]
            }
        }],
        ["else", {
            "compilerOptions": {
                "includeSources": ["src/platform/unsupported"]
            }
        }],
        ["always", {
            "compilerOptions": {
                "includeSources": ["src/facade"]
            }
        }]
    ]
}
```

Here are example JetPM commands passing configuration constants:

```plain
jetpm build --define someConstant
jetpm build --define air::target=ios
```

## Build script

The package manifest allows build scripts to be specified, as well as their dependencies.

Build scripts are executed in the Node.js® platform; therefore they implicitly use the `http://www.nodejs.org/2009` registry namespace.

Build scripts can be specified both inside the top-level and inside conditional configurations.

Here is an example manifest demonstrating build scripts:

**package.json**

```json
{
    "buildScript": {
        "compilerOptions": {
            "includeSources": ["build.jw"]
        }
    }
}
```

## Workspaces

A workspace project contains a `workspace.json` file, which follows the format:

**workspace.json**

```json
{
    "members": [
        "packages/com.c.s.p1",
        "packages/com.c.s.p2"
    ]
}
```

A member package may depend in another member package by using a `file:` URL:

**package.json**

```json
{
    "dependencies": {
        "com.c.s.p1": "file:../com.c.s.p1"
    }
}
```