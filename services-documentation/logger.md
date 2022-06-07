# Logger

We created a simple Logger to help us with logging in the sdk. If you want you can use it and it works either as a static class or instantiate it. If you create an instance you can set the logging level and the name will be shown in the log.

### Relevant types

```typescript
export enum LoggingLevel {
    DEBUG = "debug",
    INFO = "info",
    WARN = "warn",
    ERROR = "error",
}
```

### Static methods

```typescript
// Sends a message to standard output with tag debug
static debug(message: any, name = ""): void;

// Sends a message to standard output with tag info
static info(message: any, name = ""): void;

// Sends a message to standard output with tag log
static log(message: any, name = ""): void;

// Sends a message to standard error output with tag warn
static warn(message: any, name = ""): void;

// Sends a message to standard error output with tag error
static error(message: any, name = ""): void;
```

### Constructor and class methods

```typescript
// In the constructor we can pass a name that will always be added in the log
// and a logging level to choose which level of logs you want to be logged.
// If you choose logging level WARN only logger.warn and logger.error will be logged
constructor(name = "", loggingLevel: LoggingLevel = LoggingLevel.INFO);

// Sends a message to standard output with tag debug if logging level DEBUG or greater
debug(message: any): void;

// Sends a message to standard output with tag info if logging level INFO or greater
info(message: any): void;

// Sends a message to standard output with tag log if logging level INFO or greater
log(message: any): void

// Sends a message to standard error output with tag warn if logging level WARN or greater
warn(message: any): void;

// Sends a message to standard error output with tag error if logging level ERROR
error(message: any): void;
```

