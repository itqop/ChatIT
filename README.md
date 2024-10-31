# ChatIT

![ChatIT Banner](assets/banner.png)

**ChatIT** is a customizable Minecraft server mod designed to enhance in-game communication by providing robust chat management features. It offers local and global chat capabilities, profanity filtering through an external API or configurable regex patterns, and player-specific settings to control adult content visibility.

## Table of Contents

- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
  - [Commands](#commands)
- [Configuration](#configuration)
- [Contributing](#contributing)
- [Changelog](CHANGELOG.md)
- [License](#license)
- [Acknowledgments](#acknowledgments)

## Features

- **Local and Global Chat**:
  - Messages prefixed with `!` are broadcasted globally to all players.
  - Messages without `!` are sent locally to players within a 50-block radius.

- **Profanity Filtering**:
  - Integrates with an external API to detect and filter profanity in chat messages.
  - Configurable fallback using regex patterns when the API is unavailable.
  - Adjustable profanity threshold to control sensitivity.

- **Player-Specific Settings**:
  - Command to toggle `adult` content filtering for individual players.
  - Settings are persisted across sessions, ensuring consistent behavior.

- **Customizable Configuration**:
  - Comprehensive `chatit.toml` configuration file to tailor the mod's behavior.
  - Options to set API endpoints, default settings, regex patterns, and thresholds.

- **Asynchronous Processing**:
  - Ensures that chat processing does not block the main server thread, maintaining optimal performance.

- **Hot-Swap Profanity Filtering Modes**:
  - Switch between `off`, `regex`, and `api` profanity filtering modes dynamically during server runtime.
  - Modes can be changed via configuration file or using the `/chatit mode` command.

- **Custom Private Messages**:
  - Replaces default `/w`, `/msg`, `/tell` commands with custom implementations.
  - Enhanced formatting and additional features for private messaging.


## Installation

### Prerequisites

- **Minecraft Server Version**: Ensure you have the compatible version of your Minecraft server installed.
- **Forge**: Install the Minecraft Forge server mod loader compatible with your server version.
- **Java**: Java 17 or higher is recommended.

### Steps

1. **Download ChatIT**:
   - Obtain the latest version of the ChatIT mod from the [Releases](https://github.com/itqop/ChatIT/releases) page.

2. **Install Minecraft Forge Server**:
   - Download and install Minecraft Forge from the [official website](https://files.minecraftforge.net/).
   - Ensure the Forge version matches the one required by ChatIT.

3. **Add ChatIT to Mods Folder**:
   - Locate your Minecraft server installation directory.
   - If the `mods` folder does not exist, create it.
   - Place the downloaded `ChatIT.jar` file into the `mods` folder.

4. **Start the Server**:
   - Launch your Minecraft server. ChatIT should be loaded alongside other server-side mods.

## Usage

### Commands

#### `/chatit adult`

- **Description**: Toggles the `adult` content setting for the player.
- **Usage**: `/chatit adult`
- **Permissions**: Typically restricted to operators or players with specific permissions.
- **Effects**:
  - **Enabled (`adult=true`)**: The player can send and receive messages containing profanity.
  - **Disabled (`adult=false`)**: The player cannot send or receive messages containing profanity.

#### `/chatit mode <mode>`

- **Description**: Changes the profanity filtering mode.
- **Usage**: `/chatit mode (off|regex|api)`
- **Permissions**: Restricted to operators or users with specific permissions.
- **Effects**:
  - **off**: Disables profanity filtering.
  - **regex**: Uses regex patterns for profanity detection.
  - **api**: Uses external API for profanity detection.

#### Custom Private Messages

- **Description**: Replaces the default `/w`, `/msg`, `/tell` commands with enhanced custom private messaging.
- **Usage**: `/w <player> <message>`, `/msg <player> <message>`, `/tell <player> <message>`
- **Features**:
  - Improved message formatting with color coding.
  - Additional validations and restrictions.

### Chat Functionality

- **Global Chat**:
  - **Prefix**: `[G]`
  - **Description**: Messages starting with `!` are sent to all players on the server.
  - **Example**: `!Hello everyone!`

- **Local Chat**:
  - **Prefix**: `[L]`
  - **Description**: Messages without `!` are sent to players within a 50-block radius.
  - **Example**: `Hello nearby players!`

- **Error Messages**:
  - **Prefix**: `[ERROR]`
  - **Description**: Displays error messages, such as when a player attempts to send profanity without the required permissions.
  - **Example**: `[ERROR] You cannot send messages with profanity.`

## Configuration

All configurations are managed through the `config/chatit.toml` file. Below are the available settings:

```toml
# ChatIT Configuration File

# URL of the profanity checking API
host_api = "http://your-api-url.com"

# Default 'adult' value for new players (true/false)
default_adult = false

# Use regex for profanity filtering when API is unavailable (true/false)
regex = true

# Profanity threshold (0.0 - 1.0)
profanity_threshold = 0.5

# Regular expression for profanity detection
profanity_regex = "(?iu)\\b(?:(?:(?:у|[нз]а|(?:хитро|не)?вз?[ыьъ]|с[ьъ]|(?:и|ра)[зс]ъ?|(?:.\\B)+?[оаеи-])-?)?(?:[её](?:б(?!о[рй]|рач)|п[уа](?:ц|тс))|и[пб][ае][тцд][ьъ]).*?|(?:(?:н[иеа]|(?:ра|и)[зс]|[зд]?[ао](?:т|дн[оа])?|с(?:м[еи])?|а[пб]ч|в[ъы]?|пр[еи])-?)?ху(?:[яйиеёю]|л+и(?!ган)).*?|бл(?:[эя]|еа?)(?:[дт][ьъ]?)?|\\S*?(?:п(?:[иеё]зд|ид[аое]?р|ед(?:р(?!о)|[аое]р|ик)|охую)|бля(?:[дбц]|тс)|[ое]ху[яйиеё]|хуйн).*?|(?:о[тб]?|про|на|вы)?м(?:анд(?:[ауеыи](?:л(?:и[сзщ])?[ауеиы])?|ой|[ао]в.*?|юк(?:ов|[ауи])?|е[нт]ь|ища)|уд(?:[яаиое].+?|е?н(?:[ьюия]|ей))|[ао]л[ао]ф[ьъ](?:[яиюе]|[еёо]й))|елд[ауые].*?|ля[тд]ь|(?:[нз]а|по)х)\\b)"

# Profanity filtering mode: off, regex, api
profanity_mode = "api"

# Message displayed when profanity is detected and blocked.
message_adult = "Вы пытаетесь использовать ненормативную лексику в своем сообщении."

# Message displayed when no players are nearby to receive the local message.
message_local = "Вас никто не услышал, поставьте ! перед сообщением."
```

## API Requirements

The external API used for profanity checking must adhere to the following specifications:

- **Request**: Accepts a JSON object with a `text` field containing the message to be analyzed.

  ```json
  {
    "text": "your message here"
  }
  ```
  
- **Response**: Returns a JSON object with a `toxicity_score` field containing the floating-point number between 0.0 and 1.0 representing the profanity score of the provided text.
