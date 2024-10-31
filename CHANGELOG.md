# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/), and this project adheres to [Semantic Versioning](https://semver.org/).

## [0.1.9] - 2024-10-31

### Added

- **Config.java**:
  - Added hot-swap profanity filtering modes (`off`, `regex`, `api`).
  - Implemented the ability to change profanity filtering mode during server runtime using the command `/chatit mode (off|regex|api)`.

- **ChatITCommand.java**:
  - Added custom private messages to replace `/w`, `/tell`, `/msg` commands.
  - Updated the logic for sending and formatting private messages.

### Changed

- **ProfanityChecker.java**:
  - Updated profanity checking logic to accommodate new filtering modes.

## [0.1.8] - 2024-10-30

### Changed

- **ChatEventHandler.java**:
  - Change message color from white to yellow.

## [0.1.7] - 2024-10-23

### Changed

- **ProfanityChecker.java**:
  - Set HTTP version to HTTP/1.1 for HttpClient.

## [0.1.6] - 2024-10-21

### Fixed

- **Global Chat Issue**:
  - Resolved bugs affecting the functionality of the global chat.

## [0.1.5] - 2024-10-21

### Fixed

- **Local Chat Issue**:
  - Resolved bugs affecting the functionality of the local chat.

## [0.1.4] - 2024-10-21

### Added

- **Console Error Logging**:
  - Implemented comprehensive error logging to the console.
  - Facilitates easier debugging and monitoring by providing detailed error messages during runtime.

- **Configurable Message Text**:
  - Introduced the ability to customize message texts via configuration.
  - Users can now modify the default messages to better fit their server's communication style.

### Fixed

- **Tick Timeout Error**:
  - Resolved the tick timeout issue that caused the server to lag or crash under high load.
  - Enhanced the stability and performance of the mod by ensuring smoother execution of tick cycles.

### Changed

- **Renamed Command Class**:
  - Renamed the command class from `ChatitCommand.java` to `ChatITCommand.java`.
  - Improves consistency and readability within the codebase, aligning with naming conventions.

### Summary of Changes

- **Enhanced Debugging**: With the addition of console error logs, developers can now trace and fix issues more efficiently.
- **Increased Configurability**: Allowing message texts to be configured provides greater flexibility for server administrators.
- **Improved Stability**: Fixing the tick timeout error ensures that the mod runs more reliably, even under heavy usage.
- **Codebase Refinement**: Renaming the command class contributes to a more organized and maintainable code structure.

## [0.1.3] - 2024-10-21

### Added

- **Configurable Profanity Threshold**:
  - The threshold value for determining profanity (`0.5`) is now sourced from the configuration (`profanity_threshold`) with a default value of `0.5`.
  - Allows customization of the profanity filter sensitivity.

- **Configurable Regular Expression for Profanity Detection**:
  - The `PROFANITY_REGEX` pattern is now sourced from the configuration (`profanity_regex`).
  - The default value is set to the provided regular expression.
  - Enables customization or expansion of profanity filtering rules.

### Changed

- **Updated `ProfanityChecker` and `ChatEventHandler`**:
  - Modified to utilize the new configuration settings.
  - Enhanced the flexibility and configurability of the mod.

## [0.1.2] - 2024-10-21

### Changed

- **Mod Name**:
  - Renamed the mod from `Chatit` to `ChatIT` for consistency and improved branding.

## [0.1.1] - 2024-10-21

### Changed

- **Fixed Player Level Retrieval Method**:
  - Wrapped `receiver.level()` and `sender.level()` in a `try-with-resources` block to ensure proper resource management and eliminate errors.

- **Prefix Formatting**:
  - Removed bold formatting (`ChatFormatting.BOLD`) from the prefixes `[G]`, `[L]`, and `[ERROR]`. Now, the letters `G`, `L`, and `ERROR` are displayed without bold styling while retaining their color highlights.

- **Clean Code**:
  - Removed all comments from the code to enhance readability and maintainability.

## [0.1.0] - 2024-10-21

### Added

- **Local and Global Chat**:
  - Messages starting with `!` are broadcasted globally to all players.
  - Messages without `!` are sent locally to players within a 50-block radius.

- **Message Prefixes**:
  - `[G]` for global messages, where `G` is lime-colored.
  - `[L]` for local messages, where `L` is yellow-colored.
  - `[ERROR]` for error messages, where `ERROR` is red-colored.

- **Profanity Filtering**:
  - Integrated with an external API to check messages for profanity.
  - Asynchronous message checking to prevent blocking the main server thread.
  - Added a `regex` setting to use regular expressions when the API is unavailable.

- **Adult Parameter for Players**:
  - `/chatit adult` command to toggle the `adult` parameter for players.
  - Player settings are saved to `config/chatit_player_settings.json`.
  - Default `adult` value for new players is set in the configuration (`default_adult`).

- **Message Filtering Based on `adult` Parameter**:
  - If the sender's `adult` is off and the message contains profanity, the message is blocked and only sent to the sender with the `[ERROR]` prefix.
  - Players with `adult` off do not see profanity messages from other players.
  - Players with `adult` on can send and receive profanity messages.

- **Configuration File**:
  - Created `config/chatit.toml` with the following settings:
    - `host_api`: URL of the API for profanity checking.
    - `default_adult`: Default `adult` value for new players (true/false).
    - `regex`: Use regular expressions when the API is unavailable (true/false).

- **Asynchronous Processing**:
  - Interactions with the API are handled asynchronously using `CompletableFuture`.
  - Prevents blocking the main server thread during message checks.

- **Error Handling**:
  - When the API is unavailable and `regex=true`, regular expressions are used for profanity detection.
  - On encountering errors, an error message is sent only to the sender.

- **Message Formatting**:
  - Prefixes `[G]`, `[L]`, `[ERROR]` are displayed with proper formatting.
  - Letters `G`, `L`, and the word `ERROR` are colored appropriately.

### Changed

- **Code Optimization**:
  - Moved message handling to an asynchronous thread to improve performance.
  - Enhanced code structure for better readability and maintainability.

- **Bug Fixes**:
  - Removed warnings and errors related to deprecated methods.
  - Fixed issues with multithreading and accessing game objects.
