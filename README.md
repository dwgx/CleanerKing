# CleanerKing

Java Windows cleanup CLI with modular local maintenance tools.

CleanerKing is the "computer accelerant" idea turned into a Java command-line utility: collect a few annoying Windows cleanup and inspection tasks, put them behind one local tool, and keep the workflow direct enough to run from a terminal.

## Current Scope

- Windows-focused local cleanup and maintenance helper.
- Java/Maven project.
- Main entry: `src/main/java/org/CleanerKing/Client.java`.
- Intended for personal/local machines after reviewing what each action touches.

## What It Can Be Used For

- Cleaning temporary or unwanted local files.
- Running small Windows maintenance helpers from one CLI.
- Testing local system utility ideas before they become a more polished desktop tool.

## Safety Notes

This is still an experimental cleanup tool. Do not run it blindly on an important machine.

- Review the code path for the command you want to use.
- Prefer a disposable VM or secondary Windows profile for first tests.
- Keep backups for directories you care about.
- Do not add personal paths, tokens, or machine-specific secrets to the repository.

## Build And Run

Requirements:

- JDK compatible with the Maven project.
- Maven.

```bash
mvn clean package
```

Then run the built artifact or launch the main class from your IDE.

## Project Status

Personal experimental utility. The useful direction is clear, but every cleanup action should stay explicit, reviewable, and reversible where possible.

## License

MIT.
