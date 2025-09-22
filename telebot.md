

<!-- Source: https://help.telebotcreator.com/getting-started.md -->

# Getting Started

### 2. **Getting Started with Telebot Creator**

This section provides a step-by-step guide to help new users set up their accounts, create bots, and navigate the platform’s dashboard effectively.

***

**2.1 Account Setup**

To start using Telebot Creator, follow these steps:

1. **Visit the Website**:
   * Go to the official Telebot Creator website: [telebotcreator.com](http://telebotcreator.com/).
2. **Register an Account**:
   * Click the **"Register"** button on the homepage.
   * Fill in the required details, including:
     * Email address.
     * Password (choose a strong password for security).
   * Complete the CAPTCHA verification and submit the form.
   * Verify your email if required.
3. **Log In to Your Account**:
   * Once registered, log in using your email and password.
   * You’ll be redirected to the **Dashboard**, where you can start creating bots.

***

**2.2 Creating a Bot**

Creating a bot in Telebot Creator is straightforward:

1. **Obtain a Telegram Bot API Token**:
   * Open Telegram and message @BotFather.
   * Use the `/newbot` command to create a new bot.
   * Follow the prompts to:
     * Name your bot.
     * Choose a unique username (must end with “bot,” e.g., MySampleBot).
   * Copy the **API token** provided by BotFather. This token is required to link your bot to Telebot Creator.
2. **Add Your Bot to Telebot Creator**:
   * On the Telebot Creator dashboard, click the **"Add New Bot"** button.
   * Paste the Telegram Bot API token into the input field.
   * Click **"Create Bot"** to register your bot on the platform.
3. **Explore Your New Bot**:
   * After creation, your bot will appear on the dashboard with its unique **Bot ID** and basic status information.
   * You’re now ready to configure commands and start your bot!

***

**2.3 Dashboard Overview**

The dashboard is your control center for managing bots. Here’s a breakdown of its menus:

1. **Main Menu (Home Icon)**:
   * **Bot Status**:
     * "Working": Indicates the bot is active and running.
     * "Stopped": The bot is inactive. Use this status when making changes.
     * "Cloned Bot": The bot was cloned and requires token configuration in the **Settings** menu.
     * "Transferred Bot": The bot was transferred from another account. You can set the token in **Settings** and activate it.
2. **Commands (Tool Icon)**:
   * Add, edit, or remove commands for your bot.
   * Each command corresponds to specific user actions (e.g., `/start`, `/help`).
3. **Errors (Bug Icon)**:
   * Review errors or issues with your bot.
   * Provides debugging tools to resolve problems.
4. **Settings (Gear Icon)**:
   * Update your bot’s API token.
   * Configure settings for cloned or transferred bots.
   * Manage advanced bot options.
5. **Back Button**:
   * Navigate back to the previous menu or page.

***

#### **Next Steps**

Once you’ve set up your account, added your bot, and explored the dashboard, the next step is to **start writing commands** and customizing your bot.

***


<!-- Source: https://help.telebotcreator.com/command-in-tpy.md -->

# Command in TPY

#### **3. Commands in TPY**

Commands are the backbone of every bot built on Telebot Creator. They define how a bot responds to specific inputs from users, such as messages or commands like `/start` or `/help`. This section explains what commands are, how to write them using **TPY (Telebot Python)**, and advanced techniques for chaining commands, handling user interactions, and adding interactivity.

***

**3.1 What Are Commands?**

* A **command** is a predefined trigger in your bot that responds to specific user messages. For example:
  * `/start`: Greets the user and provides an introduction.
  * `/help`: Displays a list of available commands and their usage.
* Commands can perform actions like:
  * Sending messages or media.
  * Handling user inputs dynamically.
  * Running scheduled tasks or interacting with APIs.

***

**3.2 Writing Commands in TPY**

TPY (Telebot Python) is a customized, lightweight version of Python designed for Telebot Creator. It simplifies the process of writing commands while providing powerful tools for bot development.

**Example of a Basic Command**

Here’s how you create a `/start` command that sends a welcome message:

```python
bot.sendMessage("Welcome to my bot! Use /help to see available commands.")
```

***

**3.3 Using Variables and Parameters**

Variables in TPY allow you to customize responses and interact dynamically with users.

**Accessing User Information**

You can use variables like `message.from_user.first_name` to personalize your messages. For example:

```python
first_name = message.from_user.first_name
bot.sendMessage(f"Hello {first_name}, welcome to my bot!")
```

**Handling Command Parameters**

Commands can accept parameters passed by users. For example, in `/start 12345`, the parameter `12345` can be accessed as `params`:

```python
refer_id = params
bot.sendMessage(f"You were referred by ID: {refer_id}.")
```

***

**3.4 Handling User Interactions**

TPY provides several methods to manage and guide user interactions effectively.

**1. `handleNextCommand`**

This method waits for the user’s next input and routes it to a specific command.

**Example**:

```python
bot.sendMessage("Please enter your email:")
handleNextCommand("process_email")
```

In the `process_email` command:

```python
email = msg
bot.sendMessage(f"Thank you! We received your email: {email}.")
```

**2. `runCommand`**

This method allows you to trigger another command immediately.

**Example**:

```python
bot.sendMessage("Redirecting you to the /help command...")
bot.runCommand("help")
```

**3. `runCommandAfter`**

This schedules a command to execute after a specified delay (in seconds).

**Example**:

```python
bot.sendMessage("You will receive a message in 5 seconds.")
bot.runCommandAfter(5, "delayed_message")
```

In the `delayed_message` command:

```python
bot.sendMessage("This is the delayed message!")
```

***

**3.5 Advanced Command Techniques**

**Wildcard Master Command (`*`)**

The wildcard (`*`) command captures any input that doesn’t match a predefined command. This is useful for creating fallback responses.

**Example**:

```python
bot.sendMessage("Sorry, I didn’t understand that. Type /help for a list of commands.")
```

**At Handler Command (`@`)**

The at handler (`@`) command executes before any other command. Use it for preprocessing messages or logging user activity.

**Example**:

```python
bot.sendMessage("Processing your request...")
# Continue to other commands
```

***

**3.6 Examples of Common Commands**

**1. Greet Users**

```python
bot.sendMessage("Welcome! Use /help to get started.")
```

**2. Display Help Menu**

```python
bot.sendMessage("""
Here are the available commands:
/start - Start the bot
/help - Show this help menu
/points - Check your current points
""")
```

**3. Check User Points**

```python
points = left_points
bot.sendMessage(f"You have {points} points remaining in your account.")
```

**4. Collect User Input**

```python
bot.sendMessage("What’s your favorite color?")
bot.handleNextCommand("save_color")
```

In the `save_color` command:

```python
color = msg
User.saveData("favorite_color", color)
bot.sendMessage(f"Got it! Your favorite color is {color}.")
```

***

**3.7 Chaining Commands**

Commands can be chained together to create complex workflows. For example, a multi-step form:

1.  Ask for the user’s name:

    ```python
    bot.sendMessage("What’s your name?")
    handleNextCommand("get_name")
    ```
2.  Process the name and ask for the email:

    ```python
    name = msg
    User.saveData("name", name)
    bot.sendMessage(f"Hi {name}! Now, what’s your email?")
    handleNextCommand("get_email")
    ```
3.  Process the email and confirm:

    ```python
    email = msg
    User.saveData("email", email)
    bot.sendMessage("Thank you! Your details have been saved.")
    ```

***

#### **Summary**

Commands in TPY are the heart of every bot on Telebot Creator. By mastering command creation, parameter handling, and advanced techniques like chaining and scheduling, you can build bots that are interactive, intelligent, and highly functional.


<!-- Source: https://help.telebotcreator.com/tpy-language-reference.md -->

# TPY Language Reference

### **4. TPY Language Reference**

TPY (Telebot Python) is the main programming language used in Telebot Creator (TBC). It is a simplified version of Python specifically designed for building Telegram bots. TPY offers a safe, efficient, and powerful environment for creating bots with built-in functions, global variables, and libraries.

#### **4.1 Overview of TPY**

* **Purpose**: TPY makes it easy to create bots by providing essential tools and structures to interact with users, manage data, and connect with external services.
* **Environment**: TPY runs in a secure, controlled environment to ensure your bots operate safely and efficiently.
* **Key Features**:
  * **Built-in Libraries**: Pre-made modules for blockchain, payments, randomness, and more.
  * **Pre-defined Globals**: Ready-to-use variables and functions for handling user interactions and bot tasks.
  * **Command Chaining and Scheduling**: Run commands in a sequence or at specific times.
  * **Telegram Update Handling**: Simplified system for processing both standard and special update types.

#### **4.1.1 Security and Restrictions**

TPY operates in a sandboxed environment for security reasons. Important security restrictions include:

* **No `eval()` or `exec()`**: These functions, which can execute arbitrary code at runtime, are deliberately unavailable to prevent security vulnerabilities.
* **No Access to System Modules**: Modules like `os`, `sys`, `subprocess`, etc., that could interact with the host system are restricted.
* **Limited File Access**: Files can only be accessed through provided APIs, not direct filesystem access.
* **Isolated Execution**: Each bot runs in its own isolated environment to prevent interference between bots.

These restrictions are not limitations but security features designed to:

1. Protect the TBC platform infrastructure
2. Prevent malicious code execution
3. Ensure one bot cannot access data from other bots
4. Provide a stable, reliable environment for all bots

You'll find that all legitimate bot functionality is available through safe, controlled APIs and the extensive library of available functions and globals.

#### **4.2 Allowed Built-ins**

TPY includes a limited set of Python's built-in functions to keep things simple and secure.

* **Data Types**: `str`, `int`, `float`, `bool`, `dict`, `list`, `set`
* **Utilities**: `len()`, `all()`, `any()`, `sum()`, `min()`, `max()`, `round()`, `sorted()`, `reversed()`, `enumerate()`
* **Type Checks**: `isinstance()`
* **Exceptions**: `ValueError`, `TypeError`, `IndexError`, `KeyError`, `NameError`, `ZeroDivisionError`
* **Math and Iteration**: `range()`, `abs()`, `zip()`, `ord()`
* **Other**: `map()`, `slice()`

| Built-in         | Description                                                              |
| ---------------- | ------------------------------------------------------------------------ |
| **`abs`**        | Returns the absolute value of a number.                                  |
| **`all`**        | Returns `True` if all elements in an iterable are true.                  |
| **`any`**        | Returns `True` if any element in an iterable is true.                    |
| **`bin`**        | Converts an integer to a binary string.                                  |
| **`bool`**       | Converts a value to a Boolean (`True` or `False`).                       |
| **`callable`**   | Checks if an object is callable (e.g., a function).                      |
| **`chr`**        | Converts an integer to a character.                                      |
| **`divmod`**     | Returns a tuple of the quotient and remainder when dividing two numbers. |
| **`enumerate`**  | Returns an enumerator object with index-value pairs for an iterable.     |
| **`filter`**     | Filters elements in an iterable based on a function.                     |
| **`float`**      | Converts a value to a floating-point number.                             |
| **`format`**     | Formats a value using a specified format string.                         |
| **`getattr`**    | Returns the value of an attribute for an object.                         |
| **`hasattr`**    | Checks if an object has a specific attribute.                            |
| **`hash`**       | Returns the hash value of an object.                                     |
| **`hex`**        | Converts an integer to a hexadecimal string.                             |
| **`id`**         | Returns the unique identifier of an object.                              |
| **`int`**        | Converts a value to an integer.                                          |
| **`isinstance`** | Checks if an object is an instance of a specific class or type.          |
| **`issubclass`** | Checks if a class is a subclass of another class.                        |
| **`iter`**       | Returns an iterator for an iterable object.                              |
| **`len`**        | Returns the length of an iterable object.                                |
| **`list`**       | Creates a list from an iterable.                                         |
| **`map`**        | Applies a function to every item in an iterable.                         |
| **`max`**        | Returns the largest item in an iterable.                                 |
| **`min`**        | Returns the smallest item in an iterable.                                |
| **`next`**       | Retrieves the next item from an iterator.                                |
| **`oct`**        | Converts an integer to an octal string.                                  |
| **`ord`**        | Returns the Unicode code point of a character.                           |
| **`pow`**        | Returns the result of raising a number to a power.                       |
| **`range`**      | Generates a sequence of numbers.                                         |
| **`reversed`**   | Returns a reversed iterator for a sequence.                              |
| **`round`**      | Rounds a number to a specified number of decimal places.                 |
| **`set`**        | Creates a set from an iterable.                                          |
| **`slice`**      | Creates a slice object for use in slicing operations.                    |
| **`sorted`**     | Returns a sorted list from an iterable.                                  |
| **`str`**        | Converts a value to a string.                                            |
| **`sum`**        | Returns the sum of an iterable of numbers.                               |
| **`tuple`**      | Creates a tuple from an iterable.                                        |
| **`type`**       | Returns the type of an object.                                           |
| **`zip`**        | Combines multiple iterables into a single iterable of tuples.            |

#### **4.3 Allowed Globals**

TPY provides global objects and functions to help you build your bot without needing to define everything from scratch.

| **Global**               | **Description**                                                                             |
| ------------------------ | ------------------------------------------------------------------------------------------- |
| **`msg`**                | Contains the raw text content of an incoming message.                                       |
| **`message`**            | Represents the full Telegram update, including sender, chat, and message details.           |
| **`bot`**                | Low-level bot object for interacting with the Telegram Bot API.                             |
| **`Bot`**                | High-level bot object with additional methods like broadcasting, saving data, etc.          |
| **`base64`**             | Provides utilities for encoding and decoding base64 data.                                   |
| **`binascii`**           | Contains functions to convert binary data to ASCII and vice versa.                          |
| **`hashlib`**            | Provides secure hash functions like SHA256 and MD5.                                         |
| **`User`**               | A class for managing user-specific data (e.g., `User.saveData`, `User.getData`).            |
| **`time`**               | Provides utilities for working with time, including delays and timestamps.                  |
| **`bot_token`**          | The current bot's Telegram Bot API token.                                                   |
| **`HTTP`**               | A custom HTTP client for making API requests to external services.                          |
| **`regex` / `re`**       | Allows pattern matching and regular expressions.                                            |
| **`update_type`**        | Indicates the type of the current update (e.g., "message", "callback\_query").              |
| **`CSV`**                | A library for managing CSV files in the bot.                                                |
| **`bunchify`**           | Converts a dictionary into an object, allowing access via attributes.                       |
| **`bot_id`**             | The unique identifier of the bot being used.                                                |
| **`params`**             | Stores additional parameters passed to a command (e.g., `/start referral_id`).              |
| **`u`**                  | Represents the ID of the current user interacting with the bot.                             |
| **`options`**            | Contains data passed to commands, such as webhook responses or additional input parameters. |
| **`left_points`**        | Tracks the remaining points available for the bot in the current month.                     |
| **`isNumeric`**          | A helper function to check if a value is numeric.                                           |
| **`MembershipCheck`**    | Verifies user membership in a group or channel.                                             |
| **`encodejson`**         | Encodes a dictionary into a JSON string.                                                    |
| **`bf_json`**            | Converts JSON strings into Python dictionaries and vice versa.                              |
| **`ReturnCommand`**      | Returns the output of a command to the bot.                                                 |
| **`parse_qs`**           | Parses query strings into key-value pairs.                                                  |
| **`rawurlencode`**       | Encodes URLs to ensure safe transmission of data.                                           |
| **`decodeURIComponent`** | Decodes URI components into readable strings.                                               |
| **`encodeURIComponent`** | Encodes URI components for safe transmission.                                               |
| **`web3_`**              | Provides tools for interacting with Ethereum-compatible blockchains.                        |
| **`md5`**                | Generates MD5 hashes for data.                                                              |
| **`libs`**               | Accesses libraries like `libs.CSV`, `libs.Coinbase`, `libs.Polygon`, etc.                   |
| **`jsondumps`**          | Serializes Python objects into JSON strings.                                                |

#### **4.4 TPY Classes**

TPY includes several classes that help manage different aspects of your bot. Below are the main classes with their methods and explanations.

**4.4.1 Bot Class (High-level)**

The `Bot` class offers advanced methods to manage bots, handle broadcasts, manage data, and more.

| **Method**             | **Arguments**                                                                                                                                                                      | **Description**                                                                                                           |
| ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| `Transfer`             | `email` (Required), `bot_id` (Required), `bot_token` (Optional, default=None), `run_now` (Optional, default=False)                                                                 | Moves a bot to another account and optionally starts it.                                                                  |
| `broadcast`            | `code` (Optional), `command` (Optional), `callback_url` (Optional), `bot_id` (Optional), `api_key` (Optional), `function` (Optional), `warnings` (Optional), `**kwargs` (Required) | Starts a broadcast or executes code for multiple users.                                                                   |
| `clearBroadcast`       | `broadcast_id` (Optional)                                                                                                                                                          | Clears broadcast records, optionally for a specific broadcast.                                                            |
| `deleteData`           | `name` (Optional)                                                                                                                                                                  | Removes a stored global data entry by name.                                                                               |
| `genCaptcha`           | `mode` (Required), `captcha` (Optional)                                                                                                                                            | Creates a captcha (manual or automatic) and returns its info.                                                             |
| `genId`                | None                                                                                                                                                                               | Generates a unique numeric identifier.                                                                                    |
| `genRandomErrorId`     | None                                                                                                                                                                               | Creates a random error ID for logging or tracking.                                                                        |
| `genRandomId`          | None                                                                                                                                                                               | Generates a random ID, often for new bots or references.                                                                  |
| `getAllBroadcasts`     | None                                                                                                                                                                               | Retrieves a list of all broadcasts associated with the bot.                                                               |
| `getBroadcastStatus`   | `broadcast_id` (Required)                                                                                                                                                          | Gets the current status of a specific broadcast.                                                                          |
| `getData`              | `name` (Optional)                                                                                                                                                                  | Retrieves a stored global data value by name.                                                                             |
| `getIpnUrl`            | `command` (Required), `user_id` (Optional), `url` (Optional)                                                                                                                       | Provides an IPN URL for a command, useful for payments or callbacks.                                                      |
| `getIpnUrlForCoinbase` | `command` (Required)                                                                                                                                                               | Generates a Coinbase-specific IPN URL for a command.                                                                      |
| `handleNextCommand`    | `command` (Required), `options` (Optional), `cancel_at_command`(Optional)                                                                                                          | Sets up a future command to run after the user's next response.                                                           |
| `info`                 | `bot_id` (Optional), `api_key` (Optional)                                                                                                                                          | Provides detailed information about the bot's setup and status.                                                           |
| `runCommand`           | `command` (Required), `options` (Optional)                                                                                                                                         | Executes another command within the same bot, optionally with options.                                                    |
| `runCommandAfter`      | `timeout` (Required), `command` (Required), `options` (Optional), `id`(Optional)                                                                                                   | Schedules a command to run after a certain delay.                                                                         |
| `saveData`             | `name` (Required), `data` (Required)                                                                                                                                               | Stores global data under a specific name.                                                                                 |
| `start`                | `bot_id` (Required), `api_key` (Required)                                                                                                                                          | Starts a bot if conditions like sufficient points are met.                                                                |
| `status`               | `bot_id` (Required), `api_key` (Required)                                                                                                                                          | Checks or updates the bot's current status.                                                                               |
| `stop`                 | `bot_id` (Required), `api_key` (Required)                                                                                                                                          | Stops a running bot.                                                                                                      |
| `stopBroadcast`        | `broadcast_id` (Required)                                                                                                                                                          | Stops an ongoing broadcast.                                                                                               |
| `getDataFile`          | `name` (Required), `output_format` (Optional, default="txt")                                                                                                                       | Retrieves global data as a file that can be sent to users.                                                                |
| `getAllData`           | `name` (Required), `output_format` (Optional, default="json")                                                                                                                      | Retrieves all global data entries matching a name pattern as a file. Note: Only works with data saved after 4.7.0 update. |
| `getBotUsersFile`      | `output_format` (Optional, default="json"), `include_creation_date` (Optional, default=False), `include_last_active_date` (Optional, default=False)                                | Retrieves information about all bot users as a file (CSV or JSON).                                                        |

**Example Usage:**

```python
# Transfer a bot to another account and start it
bot.Transfer(email="user@example.com", bot_id="12345", run_now=True)

# Start a broadcast
bot.broadcast(command="send_newsletter", function="broadcast_news")

# Generate a unique ID
unique_id = bot.genId()
```

**4.4.2 Bot Class (Low-level)**

The low-level `bot` class provides methods for more specific actions like managing stickers, handling queries, and interacting with chats. While **camelCase** is the preferred naming convention for methods, **snake\_case** is also supported.

| **Method**                          | **Arguments**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | **Description**                                                                                                                            |
| ----------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| `addStickerToSet`                   | `user_id` (Required), `name` (Required), `emojis` (Required), `png_sticker` (Optional), `tgs_sticker` (Optional), `webm_sticker` (Optional), `mask_position` (Optional), `sticker`(Optional)                                                                                                                                                                                                                                                                                                                                                                                       | Adds a new sticker to an existing sticker set.                                                                                             |
| `answerCallbackQuery`               | `callback_query_id` (Required), `text` (Optional), `show_alert`(Optional), `url` (Optional), `cache_time` (Optional)                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Replies to a callback query from an inline keyboard.                                                                                       |
| `answerInlineQuery`                 | `inline_query_id` (Required), `results` (Required), `cache_time`(Optional), `is_personal` (Optional), `next_offset` (Optional), `switch_pm_text` (Optional), `switch_pm_parameter` (Optional), `button` (Optional)                                                                                                                                                                                                                                                                                                                                                                 | Sends results for an inline query.                                                                                                         |
| `answerPreCheckoutQuery`            | `pre_checkout_query_id` (Required), `ok` (Required), `error_message` (Optional)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Responds to a pre-checkout query during payment.                                                                                           |
| `answerShippingQuery`               | `shipping_query_id` (Required), `ok` (Required), `shipping_options` (Optional), `error_message` (Optional)                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | Replies to a shipping query with options or an error.                                                                                      |
| `answerWebAppQuery`                 | `web_app_query_id` (Required), `result` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | Provides a result to a Web App query.                                                                                                      |
| `approveChatJoinRequest`            | `chat_id` (Required), `user_id` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | Approves a user's request to join a chat.                                                                                                  |
| `banChatMember`                     | `chat_id` (Required), `user_id` (Required), `until_date`(Optional), `revoke_messages` (Optional)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | Bans a user from a chat.                                                                                                                   |
| `banChatSenderChat`                 | `chat_id` (Required), `sender_chat_id` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Bans a channel or chat sender from a group or channel.                                                                                     |
| `close`                             | None                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Closes the bot's session if needed.                                                                                                        |
| `closeForumTopic`                   | `chat_id` (Required), `message_thread_id` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Closes a forum topic in a chat.                                                                                                            |
| `closeGeneralForumTopic`            | `chat_id` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Closes the general forum topic in a chat.                                                                                                  |
| `copyMessage`                       | `chat_id` (Required), `from_chat_id` (Required), `message_id`(Required), `caption` (Optional), `parse_mode` (Optional), `caption_entities` (Optional), `disable_notification`(Optional), `protect_content` (Optional), `reply_to_message_id` (Optional), `allow_sending_without_reply` (Optional), `reply_markup`(Optional), `timeout` (Optional), `message_thread_id` (Optional), `reply_parameters` (Optional), `show_caption_above_media`(Optional), `allow_paid_broadcast` (Optional)                                                                                          | Copies a single message to another chat without sending a link.                                                                            |
| `copyMessages`                      | `chat_id` (Required), `from_chat_id` (Required), `message_ids`(Required), `disable_notification` (Optional), `message_thread_id` (Optional), `protect_content` (Optional), `remove_caption` (Optional)                                                                                                                                                                                                                                                                                                                                                                             | Copies multiple messages to another chat.                                                                                                  |
| `createChatInviteLink`              | `chat_id` (Required), `name` (Optional), `expire_date` (Optional), `member_limit` (Optional), `creates_join_request` (Optional)                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Creates a new chat invite link with optional limits.                                                                                       |
| `createChatSubscriptionInviteLink`  | `chat_id` (Required), `subscription_period` (Required), `subscription_price` (Required), `name` (Optional)                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | Creates a subscription-based chat invite link.                                                                                             |
| `createForumTopic`                  | `chat_id` (Required), `name` (Required), `icon_color` (Optional), `icon_custom_emoji_id` (Optional)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | Creates a forum topic in a chat.                                                                                                           |
| `createInvoiceLink`                 | `title` (Required), `description` (Required), `invoice_payload`(Required), `provider_token` (Required), `currency` (Required), `prices` (Required), `max_tip_amount` (Optional), `suggested_tip_amounts` (Optional), `provider_data`(Optional), `photo_url` (Optional), `photo_size` (Optional), `photo_width` (Optional), `photo_height` (Optional), `need_name`(Optional), `need_phone_number` (Optional), `need_email`(Optional), `need_shipping_address` (Optional), `send_phone_number_to_provider` (Optional), `send_email_to_provider` (Optional), `is_flexible` (Optional) | Generates a link for an invoice, allowing external payment.                                                                                |
| `createNewStickerSet`               | `user_id` (Required), `name` (Required), `title` (Required), `emojis`(Optional), `png_sticker` (Optional), `tgs_sticker` (Optional), `webm_sticker` (Optional), `contains_masks` (Optional), `sticker_type` (Optional), `mask_position` (Optional), `needs_repainting` (Optional), `stickers` (Optional), `sticker_format` (Optional)                                                                                                                                                                                                                                              | <p>This method wouldn't work on TBC for now we expect it to work in next updates.<br>Creates a new sticker set under a user's account.</p> |
| `declineChatJoinRequest`            | `chat_id` (Required), `user_id` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | Declines a pending join request to a chat.                                                                                                 |
| `deleteChatPhoto`                   | `chat_id` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Deletes a chat's profile photo.                                                                                                            |
| `deleteChatStickerSet`              | `chat_id` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Removes a sticker set from a chat.                                                                                                         |
| `deleteForumTopic`                  | `chat_id` (Required), `message_thread_id` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Deletes an entire forum topic.                                                                                                             |
| `deleteMessage`                     | `chat_id` (Required), `message_id` (Required), `timeout`(Optional)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | Removes a single message from a chat.                                                                                                      |
| `deleteMessages`                    | `chat_id` (Required), `message_ids` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Removes multiple messages from a chat.                                                                                                     |
| `deleteMyCommands`                  | `scope` (Optional), `language_code` (Optional)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Deletes the bot's current list of commands.                                                                                                |
| `deleteStickerFromSet`              | `sticker` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Removes a sticker from a sticker set.                                                                                                      |
| `deleteStickerSet`                  | `name` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Deletes an entire sticker set.                                                                                                             |
| `downloadFile`                      | `file_path` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | Downloads a file from Telegram servers.                                                                                                    |
| `editChatInviteLink`                | `chat_id` (Required), `invite_link` (Optional), `name` (Optional), `expire_date` (Optional), `member_limit` (Optional), `creates_join_request` (Optional)                                                                                                                                                                                                                                                                                                                                                                                                                          | Modifies an existing chat invite link's parameters.                                                                                        |
| `editChatSubscriptionInviteLink`    | `chat_id` (Required), `invite_link` (Required), `name` (Optional)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Updates a subscription invite link's properties.                                                                                           |
| `editForumTopic`                    | `chat_id` (Required), `message_thread_id` (Required), `name`(Optional), `icon_custom_emoji_id` (Optional)                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | Edits forum topic details like name or icon.                                                                                               |
| `editGeneralForumTopic`             | `chat_id` (Required), `name` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | Edits the general forum topic's name in a chat.                                                                                            |
| `editMessageCaption`                | `caption` (Required), `optional parameters`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | Changes the caption of a sent message.                                                                                                     |
| `editMessageLiveLocation`           | `latitude` (Required), `longitude` (Required), `optional parameters`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Updates the coordinates of a live location message.                                                                                        |
| `editMessageMedia`                  | `media` (Required), `optional parameters`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | Replaces the media of an existing message.                                                                                                 |
| `editMessageReplyMarkup`            | `optional parameters`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | Updates the inline keyboard markup of a message.                                                                                           |
| `editMessageText`                   | `text` (Required), `optional parameters`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | Modifies the text content of a sent message.                                                                                               |
| `exportChatInviteLink`              | `chat_id` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Generates a new primary invite link for a chat.                                                                                            |
| `forwardMessage`                    | `chat_id` (Required), `from_chat_id` (Required), `message_id`(Required), `optional parameters`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Forwards a single message from one chat to another.                                                                                        |
| `forwardMessages`                   | `chat_id` (Required), `from_chat_id` (Required), `message_ids`(Required), `optional parameters`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Forwards multiple messages to another chat.                                                                                                |
| `getBusinessConnection`             | `business_connection_id` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | Retrieves information about a specific business connection.                                                                                |
| `getChat`                           | `chat_id` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Fetches details about a chat.                                                                                                              |
| `getChatAdministrators`             | `chat_id` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Lists chat administrators.                                                                                                                 |
| `getChatMember`                     | `chat_id` (Required), `user_id` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | Retrieves information about a specific chat member.                                                                                        |
| `getChatMemberCount`                | `chat_id` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Gets the number of members in a chat.                                                                                                      |
| `getChatMembersCount`               | `chat_id` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Provides the chat member count (legacy method).                                                                                            |
| `getChatMenuButton`                 | `chat_id` (Optional)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Retrieves the current menu button in a chat.                                                                                               |
| `getCustomEmojiStickers`            | `custom_emoji_ids` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | Fetches stickers for given custom emoji IDs.                                                                                               |
| `getFile`                           | `file_id` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Obtains file information for a given file ID.                                                                                              |
| `getFileUrl`                        | `file_id` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Generates a direct download URL for a file.                                                                                                |
| `getForumTopicIconStickers`         | None                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Retrieves stickers suitable for forum topic icons.                                                                                         |
| `getGameHighScores`                 | `user_id` (Required), `optional parameters`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | Gets high scores of users in a game.                                                                                                       |
| `getMyCommands`                     | `scope` (Optional), `language_code` (Optional)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Retrieves the bot's currently set commands.                                                                                                |
| `getMyDefaultAdministratorRights`   | `for_channels` (Optional)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | Obtains the bot's default admin rights.                                                                                                    |
| `getMyDescription`                  | `language_code` (Optional)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | Gets the bot's description text.                                                                                                           |
| `getMyName`                         | `language_code` (Optional)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | Retrieves the bot's configured name.                                                                                                       |
| `getMyShortDescription`             | `language_code` (Optional)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | Gets the bot's short description.                                                                                                          |
| `getStarTransactions`               | `offset` (Optional), `limit` (Optional)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | Retrieves recorded star transactions (platform-specific).                                                                                  |
| `getStickerSet`                     | `name` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Fetches the details of a sticker set.                                                                                                      |
| `getUserChatBoosts`                 | `chat_id` (Required), `user_id` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | Gets chat boost information for a user.                                                                                                    |
| `getUserProfilePhotos`              | `user_id` (Required), `offset` (Optional), `limit` (Optional)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | Retrieves a user's profile photos.                                                                                                         |
| `hideGeneralForumTopic`             | `chat_id` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Hides the general forum topic from view.                                                                                                   |
| `kickChatMember`                    | `chat_id` (Required), `user_id` (Required), `optional parameters`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Kicks a member from a chat, optionally until a future time.                                                                                |
| `leaveChat`                         | `chat_id` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | The bot leaves the specified chat.                                                                                                         |
| `pinChatMessage`                    | `chat_id` (Required), `message_id` (Required), `optional parameters`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Pins a message in the chat.                                                                                                                |
| `promoteChatMember`                 | `chat_id` (Required), `user_id` (Required), `optional parameters`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Promotes a user to an admin or adjusts their admin privileges.                                                                             |
| `refundStarPayment`                 | `user_id` (Required), `telegram_payment_charge_id` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | Issues a refund for a star payment (platform-specific).                                                                                    |
| `reopenForumTopic`                  | `chat_id` (Required), `message_thread_id` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Reopens a previously closed forum topic.                                                                                                   |
| `reopenGeneralForumTopic`           | `chat_id` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Reopens the general forum topic in a chat.                                                                                                 |
| `replaceStickerInSet`               | `user_id` (Required), `name` (Required), `old_sticker` (Required), `sticker` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | Replaces an existing sticker in a set with another.                                                                                        |
| `replyPhoto`                        | `chat_id` (Required), `photo` (Required), `optional parameters`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Sends a photo in reply to a message.                                                                                                       |
| `replyText`                         | `chat_id` (Required), `text` (Required), `optional parameters`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Sends a text message in reply to another message.                                                                                          |
| `replyTo`                           | `message` (Required), `text` (Required), `kwargs` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | Quickly replies to a given message with text and options.                                                                                  |
| `restrictChatMember`                | `chat_id` (Required), `user_id` (Required), `optional parameters`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Restricts what a user can do in a chat.                                                                                                    |
| `revokeChatInviteLink`              | `chat_id` (Required), `invite_link` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Revokes an existing chat invite link.                                                                                                      |
| `sendAnimation`                     | `animation` (Required), `optional parameters`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | Sends an animation (like a GIF) to a chat.                                                                                                 |
| `sendAudio`                         | `audio` (Required), `optional parameters`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | Sends an audio file (music, podcast) to a chat.                                                                                            |
| `sendChatAction`                    | `action` (Required), `optional parameters`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | Shows a chat action (e.g., typing) to the user.                                                                                            |
| `sendContact`                       | `phone_number` (Required), `first_name` (Required), `optional parameters`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | Shares a contact's information with a chat.                                                                                                |
| `sendDice`                          | `optional parameters`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | Sends a dice emoji message that shows a random value.                                                                                      |
| `sendDocument`                      | `document` (Required), `optional parameters`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | Sends a document or file to a chat.                                                                                                        |
| `sendGame`                          | `game_short_name` (Required), `optional parameters`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | Shares a game link in a chat.                                                                                                              |
| `sendInvoice`                       | `title` (Required), `description` (Required), `invoice_payload`(Required), `provider_token` (Required), `currency` (Required), `prices` (Required), `optional parameters`                                                                                                                                                                                                                                                                                                                                                                                                          | Sends an invoice for payment to a user.                                                                                                    |
| `sendLocation`                      | `latitude` (Required), `longitude` (Required), `optional parameters`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Shares a geographic location in a chat.                                                                                                    |
| `sendMediaGroup`                    | `media` (Required), `optional parameters`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | Sends multiple media items as an album.                                                                                                    |
| `sendMessage`                       | `text` (Required), `optional parameters`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | Sends a text message to a chat.                                                                                                            |
| `sendPaidMedia`                     | `star_count` (Required), `media` (Required), `optional parameters`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | Sends media that requires a star payment (platform-specific).                                                                              |
| `sendPhoto`                         | `photo` (Required), `optional parameters`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | Sends a photo to a chat.                                                                                                                   |
| `sendPoll`                          | `question` (Required), `options` (Required), `optional parameters`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | Creates and sends a poll to the chat.                                                                                                      |
| `sendSticker`                       | `sticker` (Required), `optional parameters`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | Sends a sticker to a chat.                                                                                                                 |
| `sendVenue`                         | `latitude` (Required), `longitude` (Required), `title` (Required), `address` (Required), `optional parameters`                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Shares a venue's location and details.                                                                                                     |
| `sendVideo`                         | `video` (Required), `optional parameters`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | Sends a video file to a chat.                                                                                                              |
| `sendVideoNote`                     | `data` (Required), `optional parameters`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | Sends a video note (circular video) to a chat.                                                                                             |
| `setChatAdministratorCustomTitle`   | `chat_id` (Required), `user_id` (Required), `custom_title`(Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Sets a custom admin title for a chat member.                                                                                               |
| `setChatDescription`                | `chat_id` (Required), `description` (Optional)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Updates the chat's description text.                                                                                                       |
| `setChatMenuButton`                 | `chat_id` (Optional), `menu_button` (Optional)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Sets the menu button for a chat or globally.                                                                                               |
| `setChatPermissions`                | `chat_id` (Required), `permissions` (Required), `use_independent_chat_permissions` (Optional)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | Configures chat-wide permissions for all members.                                                                                          |
| `setChatPhoto`                      | `chat_id` (Required), `photo` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | Updates the chat's profile photo.                                                                                                          |
| `setChatStickerSet`                 | `chat_id` (Required), `sticker_set_name` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | Assigns a sticker set to a chat.                                                                                                           |
| `setChatTitle`                      | `chat_id` (Required), `title` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | Changes the chat's title.                                                                                                                  |
| `setCustomEmojiStickerSetThumbnail` | `name` (Required), `custom_emoji_id` (Optional)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Sets a custom emoji as a sticker set's thumbnail.                                                                                          |
| `setGameScore`                      | `user_id` (Required), `score` (Required), `optional parameters`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Updates the score of a user in a game.                                                                                                     |
| `setMessageReaction`                | `chat_id` (Required), `message_id` (Required), `reaction`(Optional), `is_big` (Optional)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | Adds or updates a reaction (emoji) to a message.                                                                                           |
| `setMyCommands`                     | `commands` (Required), `scope` (Optional), `language_code`(Optional)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Sets the bot's list of commands.                                                                                                           |
| `setMyDefaultAdministratorRights`   | `rights` (Optional), `for_channels` (Optional)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Defines the bot's default admin rights.                                                                                                    |
| `setMyDescription`                  | `description` (Optional), `language_code` (Optional)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Updates the bot's description.                                                                                                             |
| `setMyName`                         | `name` (Optional), `language_code` (Optional)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | Sets the bot's name.                                                                                                                       |
| `setMyShortDescription`             | `short_description` (Optional), `language_code` (Optional)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | Sets a short description for the bot.                                                                                                      |
| `setStickerEmojiList`               | `sticker` (Required), `emoji_list` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | Assigns an emoji list to a sticker.                                                                                                        |
| `setStickerKeywords`                | `sticker` (Required), `keywords` (Optional)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | Adds keywords to a sticker for better searchability.                                                                                       |
| `setStickerMaskPosition`            | `sticker` (Required), `mask_position` (Optional)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | Defines a mask position for a sticker.                                                                                                     |
| `setStickerPositionInSet`           | `sticker` (Required), `position` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | Changes a sticker's position in its set.                                                                                                   |
| `setStickerSetThumb`                | `name` (Required), `user_id` (Required), `thumb` (Optional)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | Sets the thumbnail for a sticker set.                                                                                                      |
| `setStickerSetThumbnail`            | `name` (Required), `user_id` (Required), `thumbnail` (Optional), `format` (Optional)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Sets or changes the thumbnail for a sticker set with extra options.                                                                        |
| `setStickerSetTitle`                | `name` (Required), `title` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | Changes the title of a sticker set.                                                                                                        |
| `stopMessageLiveLocation`           | `optional parameters`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | Stops an ongoing live location update.                                                                                                     |
| `stopPoll`                          | `chat_id` (Required), `message_id` (Required), `optional parameters`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Ends a currently active poll in a chat.                                                                                                    |
| `unbanChatMember`                   | `chat_id` (Required), `user_id` (Required), `only_if_banned`(Optional)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | Unbans a previously banned user.                                                                                                           |
| `unbanChatSenderChat`               | `chat_id` (Required), `sender_chat_id` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Unbans a previously banned channel sender.                                                                                                 |
| `unhideGeneralForumTopic`           | `chat_id` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Makes the general forum topic visible again.                                                                                               |
| `unpinAllChatMessages`              | `chat_id` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Unpins all pinned messages in a chat.                                                                                                      |
| `unpinAllForumTopicMessages`        | `chat_id` (Required), `message_thread_id` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Unpins all messages in a forum topic.                                                                                                      |
| `unpinAllGeneralForumTopicMessages` | `chat_id` (Required)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Unpins all messages in the general forum topic.                                                                                            |
| `unpinChatMessage`                  | `chat_id` (Required), `message_id` (Optional), `business_connection_id` (Optional)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | Unpins a specific message in the chat.                                                                                                     |
| `uploadStickerFile`                 | `user_id` (Required), `png_sticker` (Optional), `sticker`(Optional), `sticker_format` (Optional)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | Uploads a file for sticker creation.                                                                                                       |

**Note:** While **camelCase** is the preferred method naming convention in TPY, **snake\_case** method names (e.g., `send_message`) are also supported for flexibility.

**Example Usage:**

```python
# Approve a user's join request
bot.approve_chat_join_request(chat_id=123456789, user_id=789012345)

# Send a welcome photo
bot.sendPhoto(chat_id=123456789, photo="https://ibb.co/kyjq5Tm", caption="Welcome to the group!")
```

#### **4.5 Libraries (libs)**

TPY offers various libraries to extend your bot's functionality. These libraries provide pre-built modules for tasks like payments, blockchain transactions, data handling, and more.

**1. Payment Libraries**

*   **libs.Coinbase**

    * `setKeys(api_key, secret)`: Sets Coinbase API keys.
    * `post(api_key=None, secret=None)`: Initializes a Coinbase client.

    **Example:**

    ```python
    libs.Coinbase.setKeys("your_api_key", "your_secret_key")
    client = libs.Coinbase.post()
    ```
*   **libs.Paytm**

    * `setKeys(key, mid, token)`: Sets Paytm credentials.
    * `send(amount, number, description=None)`: Transfers funds via Paytm.

    **Example:**

    ```python
    libs.Paytm.setKeys("merchant_key", "merchant_id", "auth_token")
    libs.Paytm.send(100, "9876543210", "Payment for services")
    ```

**2. Blockchain Libraries**

*   **libs.Polygon**

    * `setKeys(private_key)`: Sets your private key for Polygon transactions.
    * `send(value, to, contract, private_key=None)`: Sends tokens via a contract.
    * `sendPolygon(value, to, private_key=None)`: Sends MATIC tokens.

    **Example:**

    ```python
    libs.Polygon.setKeys("your_private_key")
    libs.Polygon.sendPolygon(2.0, "recipient_wallet_address")
    ```
*   **libs.web3lib**

    * `setKeys(private_key)`: Sets your private key for web3 transactions.
    * `sendETHER(value, to, contract, rpc_url, gasPrice=None, private_key=None)`: Sends Ether or tokens.
    * `sendPolygon(value, to, private_key=None)`: Sends MATIC tokens.

    **Example:**

    ```python
    libs.web3lib.setKeys("your_private_key")
    libs.web3lib.sendETHER(1, "recipient_wallet_address", "contract_address", "https://rpc_url")
    ```

**3. Utility Libraries**

*   **libs.Random**

    * `randomInt(min, max)`: Returns a random integer.
    * `randomStr(length, char_set=None)`: Generates a random string.
    * `randomFloat(min, max)`: Returns a random float.
    * `randomAscii(length)`: Returns a random ASCII string.

    **Example:**

    ```python
    random_number = libs.Random.randomInt(1, 100)
    bot.sendMessage(f"Your random number is: {random_number}")

    random_string = libs.Random.randomStr(8)
    bot.sendMessage(f"Your random string is: {random_string}")
    ```
*   **libs.CSV**

    * `create_csv(headers)`: Creates a CSV file.
    * `add_row(row)`: Adds a row to the CSV.
    * `edit_row(row_index, row)`: Edits an existing row.
    * `get()`: Retrieves information about the CSV file.
    * `delete()`: Deletes the CSV file.

    **Example:**

    ```python
    csv = libs.CSV.CSVHandler("data.csv")
    csv.create_csv(["Name", "Points", "Date"])
    csv.add_row({"Name": "Alice", "Points": 100, "Date": "2025-01-01"})
    ```

#### **4.6 Examples**

Here are some examples of how to use TPY to create and manage your bots effectively.

**1. Sending a Welcome Message**

```python
bot.sendMessage("Welcome to the bot!")
```

**2. Get User Points**

```python
points = left_points
bot.sendMessage(f"You have {points} points remaining.")
```

**3. Scheduling a Reminder**

in the /set\_reminder command:

```python
bot.sendMessage("Reminder set for 5 seconds later.")
bot.runCommandAfter(5, "send_reminder")
```

In the send\_reminder command:

```python
bot.sendMessage("This is your reminder!")
```

#### **4.7 Handling Telegram Updates**

TPY provides a structured system for handling different types of Telegram updates. Understanding how to process these updates is essential for creating responsive and versatile bots.

**4.7.1 Update Types in Telegram**

Telegram sends various types of updates to your bot when events occur. These updates fall into two categories:

1. **Normal Updates**: The most common update types that are directly handled by standard command names
2. **Special Updates**: Less common update types that require special handler commands

**Normal Updates include:**

* `message` - Regular text or media messages sent by users
* `callback_query` - Responses from inline keyboard buttons

**Special Updates include:**

```
edited_message, channel_post, edited_channel_post, business_connection, business_message,
edited_business_message, deleted_business_messages, message_reaction, message_reaction_count,
inline_query, chosen_inline_result, shipping_query, pre_checkout_query, purchased_paid_media,
poll, poll_answer, my_chat_member, chat_member, chat_join_request, chat_boost, removed_chat_boost
```

**4.7.2 Handling Normal Updates**

Normal updates (`message` and `callback_query`) can be handled directly using standard command names:

```python
# /start command handles message updates with text "/start"
# Command name in TBC: /start
bot.sendMessage("Welcome to my bot!")

# /joined command handles new chat join events
# Command name in TBC: /joined
bot.sendMessage("Welcome to the group!")

# command for handling callback queries named "show_profile"
# Command name in TBC: show_profile (callback data name)
bot.answerCallbackQuery(callback_query_id=message.id, text="Loading profile...")
```

**4.7.3 Handling Special Updates**

Special updates require specific handler commands using the pattern: `/handler_<update_type>`

For example:

```python
# Command name in TBC: /handler_edited_message
# This processes edited_message updates
edited_text = message.text
bot.sendMessage(f"You edited your message to: {edited_text}")
```

```python
# Command name in TBC: /handler_inline_query
# This processes inline_query updates
query = message.query
results = [...]  # Define your inline results
bot.answerInlineQuery(inline_query_id=message.id, results=results)
```

```python
# Command name in TBC: /handler_chat_join_request
# Handles chat join requests
user_id = message.from_user.id
bot.approveChatJoinRequest(chat_id=message.chat.id, user_id=user_id)
```

**4.7.4 Handling All Special Updates**

If you want a single command to handle all special update types, you can create a command named `/handler_special_updates`:

```python
# Command name in TBC: /handler_special_updates
# This processes all special update types
update_type = update_type  # The global variable that contains the current update type

if update_type == "edited_message":
    # Handle edited messages
    bot.sendMessage("You edited a message")
    
elif update_type == "inline_query":
    # Handle inline queries
    query = message.query
    results = [...]  # Define your inline results
    bot.answerInlineQuery(inline_query_id=message.id, results=results)
    
elif update_type == "chat_join_request":
    # Handle join requests
    bot.approveChatJoinRequest(chat_id=message.chat.id, user_id=message.from_user.id)
    
# Add handlers for other special update types as needed
```

**4.7.5 Accessing Update Type Information**

In any command, you can access the current update type using the global variable `update_type`. This is especially useful in the `/handler_special_updates` command:

```python
# Check what kind of update we're processing
current_update = update_type
bot.sendMessage(f"Processing update type: {current_update}")
```

This system gives you flexible control over how your bot handles different Telegram events, allowing for more interactive and responsive bot experiences.

#### **Summary**

TPY is a simple yet powerful language designed for building Telegram bots with Telebot Creator. By using its built-in functions, global variables, and libraries, you can create interactive and feature-rich bots tailored to your needs.

***

**4.4.3 User Class**

The `User` class provides methods for managing user-specific data.

| **Method**         | **Arguments**                                                                   | **Description**                                                     |
| ------------------ | ------------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `saveData`         | `name` (Required), `data` (Required), `user` (Optional)                         | Saves user-specific data under a given name.                        |
| `getData`          | `name` (Required), `user` (Optional)                                            | Retrieves user-specific data by name.                               |
| `deleteData`       | `name` (Required), `user` (Optional)                                            | Removes user-specific data by name.                                 |
| `getDataFile`      | `name` (Required), `user` (Optional), `output_format` (Optional, default="txt") | Retrieves user data as a file that can be sent to users.            |
| `getAllData`       | `name` (Required), `output_format` (Optional, default="json")                   | Gets all data entries that match a specific name pattern as a file. |
| `getAllDataOfUser` | `user` (Required), `output_format` (Optional, default="json")                   | Retrieves all data associated with a specific user as a file.       |

**Example Usage:**

```python
# Save user data
User.saveData("profile", {"name": "Alice", "age": 30})

# Get user data
profile = User.getData("profile")
bot.sendMessage(f"User profile: {profile}")

# Get user data as a file
profile_file = User.getDataFile("profile")
bot.sendDocument(profile_file)

# Get all data for a specific user
all_user_data = User.getAllDataOfUser("12345678")
bot.sendDocument(all_user_data)
```

***


<!-- Source: https://help.telebotcreator.com/tbc-libraries-libs.md -->

# TBC Libraries (Libs)

Libraries, often called **libs**, in Telebot Creator (TBC) enhance the basic TPY functionalities by offering pre-built modules for specific tasks. These libraries make it easier and faster to add advanced features to your Telegram bots, such as handling payments, managing blockchain transactions, working with data, generating random values, and more.\
\
**DEPRECATION NOTICE:**

The following libraries are deprecated and removed:

`libs.Polygon, libs.ARB, libs.TTcoin, libs.Tomochain.`

Please migrate to libs.web3lib (sendETHER) which now supports all EVM chains, proxy support, and enhanced functionality.

> **New in 4.9.0**:
>
> * Added native `time.sleep()` function with a maximum limit of 10 seconds
> * Direct HTTP module usage is now recommended over `libs.customHTTP()`
> * Code execution timeout increased from 60 to 120 seconds
> * Do not use `import` statements in your code
> * For handling inline queries and other update types, use the `/handler_<update_type>` command format
>
> **New in 5.0.0**:
>
> * Commands can now run up to 160 seconds (increased from 120 seconds)
> * New stats tracking capabilities in Account and Bot classes
> * Data transfer functionality between bots
> * OpenRouter API support in openai\_lib with extended timeouts

#### **5.1 Overview of Libraries**

TBC libraries are grouped based on their functionalities to help you develop bots efficiently:

* **Payment Integrations**: Automate payments using popular services.
* **Blockchain Transactions**: Manage cryptocurrency transfers and transactions.
* **Data Handling**: Work with data easily using CSV files.
* **Randomization**: Generate random numbers or strings for games and giveaways.
* **Resource Management**: Track points, credits, or other resources for users or globally.

**7. libs.Paytm**

Integrates with the Paytm payment gateway for fund transfers and automated payments.

* **Functions**:
  * `setKeys(key, mid, token)`: Sets your Paytm merchant credentials.
  * `send(amount, number, description=None, key=None, mid=None, token=None)`: Sends a payment to a phone number.
*   **Example**:

    ```python
    libs.Paytm.setKeys("merchant_key", "merchant_id", "auth_token")
    libs.Paytm.send(100, "9876543210", "Payment for services")
    ```

**8. libs.Webhook**

The `libs.Webhook` library in Telebot Creator allows you to create and manage webhooks for seamless external integrations. Webhooks enable bots to respond to real-time updates from external systems, such as payment notifications or user actions.

***

**Functions**

1. **`getUrlFor(command, user_id=None, chat_id=None, bot_id=None, api_key=None, **options)`**
   * **Description**: Generates a webhook URL for invoking a specific command, optionally tied to a specific user, chat, or another bot.
   *   **Function Syntax**:

       ```python
       libs.Webhook.getUrlFor(
           command: str,
           user_id: Optional[str] = None,
           chat_id: Optional[str] = None,
           bot_id: Optional[str] = None,
           api_key: Optional[str] = None,
           **options: Any
       )
       ```
   * **Parameters**:
     * **`command`** (_str_): The command to be triggered by the webhook.
     * **`user_id`** (_Optional\[str]_): The user ID associated with the webhook.
     * **`chat_id`** (_Optional\[str]_): The chat ID associated with the webhook.
     * **`bot_id`** (_Optional\[str]_): The ID of the bot for which the webhook is being generated. If provided, **`api_key`** is required.
     * **`api_key`** (_Optional\[str]_): The API key of the bot owner. Used for validation when `bot_id` is specified.
     * **`**options`**: Additional options to customize the webhook behavior.
   * **In webhook commands**, the incoming response data is stored in `options`, not `message`. The `options` dictionary includes two keys:
     * **`data`**: The raw incoming data.
     * **`json`**: A parsed JSON object from the webhook payload.
   *   **Examples**:

       **Basic Webhook URL**:

       ```python
       webhook_url = libs.Webhook.getUrlFor("process_payment", user_id=12345)
       bot.sendMessage(f"Webhook URL: {webhook_url}")
       ```

       **Webhook for Another Bot**:

       ```python
       webhook_url = libs.Webhook.getUrlFor(
           "process_payment",
           user_id=12345,
           bot_id="another_bot_id",
           api_key="another_bot_api_key"
       )
       bot.sendMessage(f"Webhook URL for another bot: {webhook_url}")
       ```

       **Webhook with Additional Options**:

       ```python
       webhook_url = libs.Webhook.getUrlFor(
           "notify_event",
           chat_id=67890,
           options={"options": "example", "redirect_to": "https://example.com/callback"}
       )
       bot.sendMessage(f"Custom Webhook URL: {webhook_url}")
       ```

***

**Use Cases**

* **Payment Confirmation**: Generate webhook URLs for real-time payment updates from external systems.
* **Bot-to-Bot Communication**: Use `bot_id` and `api_key` to enable bots to trigger commands in each other.
* **Dynamic Event Handling**: Pass additional options to customize webhook behavior based on the event.

**9. libs.DateAndTime**

Works with dates and times.

* **Functions**:
  * `utcnow()`: Gets the current UTC date and time.
  * `date_now()`: Gets the current UTC date.
  * `time()`: Gets the current UNIX timestamp.
  * `now(timezone_str)`: Gets the current date and time in a specific timezone.
*   **Example**:

    ```python
    current_time = libs.DateAndTime.utcnow()
    bot.sendMessage(f"The current UTC time is: {current_time}")
    ```

**10. libs.Oxapay**

Integrates the Oxapay payment system for merchants.

* **Functions**:
  * `post(merchant_api_key)`: Initializes the Oxapay client with your API key.
*   **Example**:

    ```python
    client = libs.Oxapay.post("your_merchant_api_key")
    bot.sendMessage("Oxapay client initialized!")
    ```

**11. libs.customHTTP**

Performs HTTP requests with limitations on data size and timeouts, we use it as HTTP class but if you want you can use this lib, this lib provides 30 seconds timeout and it can receive contene upto 20 mb.

> **Note**: As of version 4.9.0, it's recommended to use the standard HTTP module instead of libs.customHTTP() for better performance and reliability.

* **Class**:
  * `CustomHTTP()`: Creates an HTTP client.
* **Methods**:
  * `get(url, **kwargs)`: Performs a GET request.
  * `post(url, **kwargs)`: Performs a POST request.
  * `put(url, **kwargs)`: Performs a PUT request.
  * `head(url, **kwargs)`: Performs a HEAD request.
  * `options(url, **kwargs)`: Performs an OPTIONS request.
  * `patch(url, **kwargs)`: Performs a PATCH request.
  * `close()`: Closes the HTTP session.
*   **Example**:

    ```python
    http_client = libs.customHTTP()
    response = http_client.get("https://api.example.com/data")
    bot.sendMessage(f"Response: {response}")
    # not close the connect for future requests
    ```

**12. TonLib**

> **New in 4.9.0**

Provides comprehensive integration with The Open Network (TON) blockchain. With TonLib, you can create wallets, check balances, send TON, work with jettons (TON's tokens), and integrate TON Connect for user wallet connections.

* **Wallet Management**:
  * `generateWallet()`: Creates a new TON wallet and returns its address and mnemonic phrase.
  * `setKeys(mnemonics)`: Stores a mnemonic phrase for later use.
  * `getWalletAddress(mnemonics=None)`: Retrieves the wallet address from stored keys or specified mnemonics.
* **TON Operations**:
  * `getBalance(address, api_key=None, endpoint=None)`: Checks the TON balance of an address.
  * `sendTON(to_address, amount, comment=None, mnemonics=None, api_key=None, endpoint=None, is_testnet=False)`: Sends TON to another address.
  * `checkTONTransaction(address, api_key=None, endpoint=None, limit=10)`: Gets recent transactions for an address.
* **TON Connect Integration**:
  * `create_ton_connect_session(user_id, expiry_seconds=86400)`: Creates a session for wallet connection.
  * `verify_ton_connect_session(session_id)`: Checks if a wallet has connected to the session.
  * `request_ton_transaction(to_address, amount, comment=None, callback_url="", return_url=None)`: Requests a TON transfer from a connected wallet.
* **Jetton Operations**:
  * `get_jetton_metadata(jetton_master_address, api_key=None, endpoint=None)`: Retrieves information about a Jetton (token).
  * `get_jetton_balance(owner_address, jetton_master_address, api_key=None, endpoint=None)`: Checks a Jetton balance.
  * `request_jetton_transfer(to_address, jetton_master_address, amount, comment=None, callback_url="", return_url=None)`: Requests a Jetton transfer.
*   **Example**:

    ```python
    # Generate a wallet
    wallet = TonLib.generateWallet()
    address = wallet["address"]

    # Check balance
    balance = TonLib.getBalance(address)
    bot.sendMessage(f"Balance: {balance} TON")

    # Send TON
    TonLib.sendTON(
        to_address="EQD...",
        amount=0.1,
        comment="Test payment"
    )
    ```

For detailed documentation, see [TON Library Documentation](ton-library-documentation).

**13. libs.web3lib**

**Overview:**\
This library is designed to interact with all supported EVM chains. It offers functions to send native coins and tokens (ERC‑20) using advanced features such as automatic gas estimation, retry logic, and optional proxy support. This library is published on Telebot Creator in TPY language.

**Supported Networks (31 Total):**

* **Ethereum** (chainId: 1)
* **BSC** (chainId: 56)
* **Polygon** (chainId: 137)
* **Avalanche** (chainId: 43114)
* **Fantom** (chainId: 250)
* **Arbitrum** (chainId: 42161)
* **Optimism** (chainId: 10)
* **Harmony** (chainId: 1666600000)
* **Cronos** (chainId: 25)
* **Moonriver** (chainId: 1285)
* **Moonbeam** (chainId: 1284)
* **Celo** (chainId: 42220)
* **Heco** (chainId: 128)
* **Okexchain** (chainId: 66)
* **Xdai** (chainId: 100)
* **KCC** (chainId: 321)
* **Metis** (chainId: 1088)
* **Aurora** (chainId: 1313161554)
* **Base** (chainId: 8453)
* **ZKSync** (chainId: 324)
* **Scroll** (chainId: 534352)
* **Linea** (chainId: 59144)
* **Boba** (chainId: 288)
* **Kava** (chainId: 2222)
* **Fuse** (chainId: 122)
* **Evmos** (chainId: 9001)
* **Canto** (chainId: 7700)
* **Astar** (chainId: 592)
* **Telos** (chainId: 40)
* **Rootstock** (chainId: 30)
* **TTcoin** (chainId: 22023)

**Key Functions:**

* **get\_default\_rpc(network: str) -> str**\
  Returns the default RPC URL for the given network.
* **get\_supported\_networks() -> Dict\[str, Dict\[str, Any]]**\
  Provides a list of all supported networks with their chain IDs and RPC endpoints.
* **setKeys(private\_Key: str) -> str**\
  Stores the sender's private key (linked to your current bot ID) in the MongoDB collection.
* **sendNativeCoin(...) -> str**\
  Sends native coins (like ETH) on the selected EVM chain. Features include automatic gas estimation, retry logic, and optional proxy support.
* **sendETHER(...) -> str**\
  When provided with a token contract address, this function sends tokens via the contract's transfer method. It supports the same features as sendNativeCoin.

Additionally, the following aliases are available for token transfers:\
`send_ether`, `sendether`, and `sendEther` (all reference the same function).\
For more details please read [https://help.telebotcreator.com/crypto-libraries-documentation](https://help.telebotcreator.com/crypto-libraries-documentation).

***

## **Usage Examples**

In TPY language on Telebot Creator, you define your function alias like this:

```tpy
sendETHER = libs.web3lib.sendETHER
```

Below are several examples demonstrating how to use these functions:

#### **Example 1: Sending a Native Coin Transfer (ETH)**

```tpy
dummy_private_key = "0xYOUR_PRIVATE_KEY_HERE"
test_rpc = "https://rpc.ankr.com/eth"  # Use explicit RPC URL or specify network below
test_recipient = "0xRecipientAddressHere"

# Native transfer example (contract_address omitted)
tx_hash = libs.web3lib.sendNativeCoin(
    value = 0.5,                     # Amount in Ether
    to = test_recipient,
    rpc_url = test_rpc,
    private_key = dummy_private_key,
    network = "ethereum",            # If rpc_url is empty, default Ethereum RPC is used
    retry = True,                    # Retry once on recoverable errors
    estimate_gas = True
)

bot.sendMessage("Native Transfer TX Hash: " + tx_hash)
```

#### **Example 2: Sending an ERC‑20 Token Transfer**

```tpy
dummy_private_key = "0xYOUR_PRIVATE_KEY_HERE"
dummy_contract = "0xTokenContractAddressHere"
test_recipient = "0xRecipientAddressHere"
test_rpc = "https://rpc.ankr.com/eth"

# Token transfer example (using token transfer branch)
tx_hash = libs.web3lib.sendETHER(
    value = 1,                       # Token amount (assumes 18 decimals)
    to = test_recipient,
    rpc_url = test_rpc,
    private_key = dummy_private_key,
    contract_address = dummy_contract,  # Token contract address provided triggers token transfer logic
    network = "ethereum",
    retry = True,
    estimate_gas = True
)

bot.sendMessage("Token Transfer TX Hash: " + tx_hash)
```

#### **Example 3: Using Network Parameter Only (No Explicit RPC URL)**

```tpy
dummy_private_key = "0xYOUR_PRIVATE_KEY_HERE"
dummy_contract = "0xTokenContractAddressHere"
test_recipient = "0xRecipientAddressHere"

# Use network parameter to automatically use the default RPC for Polygon
tx_hash = libs.web3lib.sendETHER(
    value = 0.25,
    to = test_recipient,
    network = "polygon",
    private_key = dummy_private_key,
    contract_address = dummy_contract,
    retry = False,
    estimate_gas = True
)

bot.sendMessage("Token Transfer on Polygon TX Hash: " + tx_hash)
```

***

**Summary:**

* This library supports 31 EVM networks with default RPC endpoints.
* It offers robust functionality with automatic gas estimation, retry logic, and proxy support.
* Aliases like `send_ether`, `sendether`, and `sendEther` are provided for convenience.
* It is published on Telebot Creator and written in TPY language.

#### **5.3 Example Use Cases for Libraries**

Here are some real-world scenarios where these libraries can be applied:

**Payment Automation**

Automate payments for subscriptions or services using payment libraries.

*   **Example**:

    ```python
    libs.Paytm.setKeys("merchant_key", "merchant_id", "auth_token")
    libs.Paytm.send(500, "1234567890", "Subscription payment")
    ```

**User Data Tracking**

Manage user data for referral systems or leaderboards with the CSV library.

*   **Example**:

    ```python
    csv = libs.CSV.CSVHandler("referrals.csv")
    csv.add_row({"User": "Bob", "Referrals": 5})
    ```

**Crypto Payment Bots**

Handle cryptocurrency transactions for services or rewards using blockchain libraries.

*   **Example**:

    ```python
    libs.Polygon.setKeys("your_private_key")
    libs.Polygon.sendPolygon(2.0, "recipient_wallet_address")
    ```

**Random Giveaways**

Use the Random library to create giveaways or dynamic responses.

*   **Example**:

    ```python
    random_number = libs.Random.randomInt(1, 100)
    bot.sendMessage(f"Your random number is: {random_number}")
    ```

**Webhook Integrations**

Connect your bot with external services using the Webhook library.

*   **Example**:

    ```python
    webhook_url = libs.Webhook.getUrlFor("process_payment", user_id=12345)
    bot.sendMessage(f"Webhook URL: {webhook_url}")
    ```

**14. libs.openai\_lib**

Provides a client for interacting with OpenAI's API and OpenRouter API, enabling AI-powered features in your bot.

* **Classes**:
  * `OpenAIClient`: Core client for interacting with OpenAI API or OpenRouter API.
  * `AIAssistant`: Higher-level class for working with OpenAI Assistants or direct chat completions.
* **Error Classes**:
  * `OpenAIError`: Base exception class for OpenAI errors.
  * `OpenAITimeoutError`: Error for request timeouts.
  * `OpenAIAPIError`: Error for API-specific issues.
* **Key Methods in OpenAIClient**:
  * `create_chat_completion`: Generates text completions using OpenAI or OpenRouter models.
  * `create_assistant`: Creates a new OpenAI Assistant (OpenAI API only).
  * `create_thread`: Creates a new conversation thread (OpenAI API only).
  * `create_message`: Adds a message to a conversation thread (OpenAI API only).
  * `create_run`: Runs an assistant on a thread to generate a response (OpenAI API only).
* **Key Methods in AIAssistant**:
  * `start_conversation`: Starts a new conversation thread.
  * `send_message`: Sends a message and returns the assistant's response.
  * `get_conversation_history`: Retrieves the history of messages in a thread.
* **New in 5.0.0**:
  * Extended timeout support up to 160 seconds
  * OpenRouter API integration with access to various models like Llama
  * Enhanced error handling and retries
*   **Example - Chat Completion with OpenAI**:

    ```python
    client = libs.openai_lib.OpenAIClient(api_key="YOUR_API_KEY", timeout=120)
    response = client.create_chat_completion(
        model="gpt-4o",
        messages=[
            {"role": "system", "content": "You are a helpful assistant."},
            {"role": "user", "content": "Tell me about Telegram bots."}
        ]
    )
    bot.sendMessage(response["choices"][0]["message"]["content"])
    ```
*   **Example - Using OpenAI Assistant**:

    ```python
    client = libs.openai_lib.OpenAIClient(api_key="YOUR_API_KEY", timeout=120)
    assistant = libs.openai_lib.AIAssistant(
        openai_client=client,
        create_new=True,
        name="Customer Support Bot",
        instructions="You are a helpful customer support assistant.",
        model="gpt-4o"
    )

    thread_id = assistant.start_conversation()
    response = assistant.send_message("How do I reset my password?")
    bot.sendMessage(response["content"])
    ```
*   **Example - Using OpenRouter API**:

    ```python
    # Initialize with OpenRouter API key and extended timeout
    client = libs.openai_lib.OpenAIClient(
        api_key="YOUR_OPENROUTER_API_KEY",
        timeout=120,
        base_url="https://openrouter.ai/api/v1"
    )

    # Use with a specific model via AIAssistant
    assistant = libs.openai_lib.AIAssistant(
        openai_client=client,
        model="meta-llama/llama-3.3-8b-instruct:free",
        system_message="You're a helpful assistant."
    )

    # Send message and get response
    response = assistant.send_message("Tell me about Telegram bots")
    response_text = str(response.get("content")[0]['text']['value'])
    bot.sendMessage(response_text)
    ```

**15. libs.gemini\_lib**

Provides a client for interacting with Google's Gemini AI models, offering an OpenAI-compatible interface.

* **Classes**:
  * `GeminiClient`: Core client for interacting with Gemini API.
  * `GeminiAIAssistant`: Higher-level class for working with Gemini in an assistant-like way.
* **Error Classes**:
  * `GeminiError`: Base exception class for Gemini errors.
  * `GeminiTimeoutError`: Error for request timeouts.
  * `GeminiAPIError`: Error for API-specific issues.
* **Key Methods in GeminiClient**:
  * `create_chat_completion`: Generates text completions using Gemini models.
  * `create_assistant`: Creates a new assistant-like interface.
  * `create_thread`: Creates a new conversation thread.
  * `create_message`: Adds a message to a conversation thread.
  * `create_run`: Runs an assistant on a thread to generate a response.
* **Key Methods in GeminiAIAssistant**:
  * `start_conversation`: Starts a new conversation thread.
  * `send_message`: Sends a message and returns the assistant's response.
  * `get_conversation_history`: Retrieves the history of messages in a thread.
*   **Example - Chat Completion**:

    ```python
    client = libs.gemini_lib.GeminiClient(api_key="YOUR_API_KEY")
    response = client.create_chat_completion(
        model="gemini-2.0-flash",
        messages=[
            {"role": "user", "content": "What are the best practices for Telegram bot development?"}
        ]
    )
    bot.sendMessage(response["choices"][0]["message"]["content"])
    ```
*   **Example - Using Assistant**:

    ```python
    client = libs.gemini_lib.GeminiClient(api_key="YOUR_API_KEY")
    assistant = libs.gemini_lib.GeminiAIAssistant(
        gemini_client=client,
        create_new=True,
        name="Product Advisor",
        instructions="You are a helpful product recommendation assistant.",
        model="gemini-2.0-flash"
    )

    thread_id = assistant.start_conversation()
    response = assistant.send_message("I need a new laptop for video editing.")
    bot.sendMessage(response["content"])
    ```

#### **5.4 Summary of Libraries**

| **Library**          | **Purpose**                                                       | **Key Functions**                                                                                                                                          |
| -------------------- | ----------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **libs.Resources**   | Managing user and global resources                                | `value`, `add`, `cut`, `set`, `reset`, `getAllData`, `clearAllData`, `fetchAllResourcesOfUser`, `removeDataOfUser`, `removeAllDataOfUser`, `removeAllData` |
| **libs.Coinbase**    | Coinbase payment integration                                      | `setKeys`, `post`                                                                                                                                          |
| **libs.Crypto**      | Cryptocurrency conversions and pricing                            | `convert`, `get_price`                                                                                                                                     |
| **libs.Random**      | Generating random numbers and strings                             | `randomInt`, `randomStr`, `randomFloat`, `randomAscii`                                                                                                     |
| **libs.Paytm**       | Paytm payment integration                                         | `setKeys`, `send`                                                                                                                                          |
| **libs.CSV**         | Data management with CSV files                                    | `create_csv`, `add_row`, `edit_row`, `get`, `delete`                                                                                                       |
| **libs.Webhook**     | Creating and managing webhooks                                    | `genRandomId`, `getUrlFor`                                                                                                                                 |
| **libs.DateAndTime** | Working with dates and times                                      | `utcnow`, `date_now`, `time`, `now`                                                                                                                        |
| **libs.Oxapay**      | Oxapay payment integration                                        | `post`                                                                                                                                                     |
| **libs.customHTTP**  | Performing HTTP requests with constraints                         | `get`, `post`, `put`, `delete`, `head`, `options`, `patch`, `close`                                                                                        |
| **libs.web3lib**     | Ethereum-compatible blockchain transactions (Supports EVM chains) | `setKeys`, `sendETHER`, `sendNativeCoin`                                                                                                                   |
| **libs.openai\_lib** | OpenAI API integration for AI capabilities                        | `OpenAIClient`, `AIAssistant`, create\_chat\_completion                                                                                                    |
| **libs.gemini\_lib** | Google Gemini API integration for AI capabilities                 | `GeminiClient`, `GeminiAIAssistant`, create\_chat\_completion                                                                                              |

#### **5.6 Real-World Applications of Libraries**

Here are some practical examples of how you can use these libraries in your bots:

**Crypto Payment Bots**

Handle cryptocurrency payments for services or rewards.

*   **Example**:

    ```python
    dummy_private_key = "0xYOUR_PRIVATE_KEY_HERE"
    dummy_contract = "0xTokenContractAddressHere"
    test_recipient = "0xRecipientAddressHere"

    # Use network parameter to automatically use the default RPC for Polygon
    tx_hash = libs.web3lib.sendETHER(
        value = 0.25,
        to = test_recipient,
        network = "polygon",
        private_key = dummy_private_key,
        contract_address = dummy_contract,
        retry = False,
        estimate_gas = True
    )

    bot.sendMessage("Token Transfer on Polygon TX Hash: " + tx_hash)
    ```

**Referral and Loyalty Systems**

Manage user points or rewards for referrals and other actions.

*   **Example**:

    ```python
    points = libs.Resources.userRes("points", user)
    points.add(10)
    current_points = points.value()
    bot.sendMessage(f"You now have {current_points} points!")
    ```

**Data-Driven Decisions**

Log and analyze user data or create leaderboards using CSV files.

*   **Example**:

    ```python
    csv = libs.CSV.CSVHandler("leaderboard.csv")
    csv.add_row({"User": "Charlie", "Score": 250})
    ```

**Automated Payments**

Use Paytm or Coinbase libraries to automate payment transfers.

*   **Example**:

    ```python
    libs.Paytm.setKeys("merchant_key", "merchant_id", "auth_token")
    libs.Paytm.send(100, "9876543210", "Payment for services")
    ```

**Random Giveaways**

Create random giveaways or generate unique codes.

*   **Example**:

    ```python
    random_number = libs.Random.randomInt(1, 100)
    bot.sendMessage(f"Your random number is: {random_number}")
    ```

**OpenAI Integration**

Use the OpenAI library to add AI capabilities to your bot.

*   **Example - Chat Completion**:

    ```python
    client = libs.openai_lib.OpenAIClient(api_key="YOUR_API_KEY")
    response = client.create_chat_completion(
        model="gpt-4o",
        messages=[
            {"role": "system", "content": "You are a helpful assistant."},
            {"role": "user", "content": "Tell me about Telegram bots."}
        ]
    )
    bot.sendMessage(response["choices"][0]["message"]["content"])
    ```

**Gemini Integration**

Use the Gemini library to add AI capabilities to your bot.

*   **Example - Chat Completion**:

    ```python
    client = libs.gemini_lib.GeminiClient(api_key="YOUR_API_KEY")
    response = client.create_chat_completion(
        model="gemini-2.0-flash",
        messages=[
            {"role": "user", "content": "What are the best practices for Telegram bot development?"}
        ]
    )
    bot.sendMessage(response["choices"][0]["message"]["content"])
    ```

***

By using these libraries, you can significantly extend the capabilities of your Telegram bots, making them more interactive, efficient, and feature-rich. Whether you need to handle payments, manage data, or integrate with blockchain technologies, TBC's libraries provide the tools you need to build powerful bots with ease.

**4. libs.Resources**

The `libs.Resources` library in Telebot Creator provides a simple and efficient way to track and manage numeric values in your bot. These can represent points, credits, scores, or any other numerical resource.

### Resource Classes

#### userRes

Create and manage resources for specific users.

```python
res = libs.Resources.userRes(name, user=None)
```

**Parameters:**

* `name` (Required): The name of the resource.
* `user` (Optional): User ID to associate with this resource. Defaults to the current user.

#### globalRes

Create and manage global resources that apply across all users.

```python
res = libs.Resources.globalRes(name)
```

**Parameters:**

* `name` (Required): The name of the resource.

#### anotherRes

Create and manage resources for a specific user (even if not the current user).

```python
res = libs.Resources.anotherRes(name, user)
```

**Parameters:**

* `name` (Required): The name of the resource.
* `user` (Required): User ID to associate with this resource.

#### adminRes

Create and manage resources with administrative privileges.

```python
res = libs.Resources.adminRes(name, user=None)
```

**Parameters:**

* `name` (Required): The name of the resource.
* `user` (Optional): User ID to scope the admin operations.

#### accountRes

Create and manage account-level resources that persist across all bots.

```python
res = libs.Resources.accountRes(name)
```

**Parameters:**

* `name` (Required): The name of the resource.

### Resource Methods

All resource classes support the following methods:

#### value()

Gets the current value of the resource.

```python
current_value = res.value()
```

**Returns:** The current numeric value of the resource.

#### add(value)

Adds the specified amount to the resource.

```python
new_value = res.add(amount)
```

**Parameters:**

* `value` (Required): The amount to add.

**Returns:** The new value after addition.

#### cut(value)

Subtracts the specified amount from the resource.

```python
new_value = res.cut(amount)
```

**Parameters:**

* `value` (Required): The amount to subtract.

**Returns:** The new value after subtraction.

#### set(value)

Sets the resource to a specific value.

```python
new_value = res.set(amount)
```

**Parameters:**

* `value` (Required): The value to set.

**Returns:** The new value.

#### reset()

Resets the resource value to zero.

```python
new_value = res.reset()
```

**Returns:** The new value (always 0).

### Examples

**User-specific resources:**

```python
# Create or access a user resource
points = libs.Resources.userRes("points")

# Add points for current user
points.add(100)

# Check current points
current = points.value()
bot.sendMessage(f"You have {current} points")

# Reset points
points.reset()
bot.sendMessage("Points reset to 0")
```

**Global resources:**

```python
# Create or access a global resource
jackpot = libs.Resources.globalRes("jackpot")

# Add to jackpot
jackpot.add(50)

# Check current jackpot
current = jackpot.value()
bot.sendMessage(f"Current jackpot: {current}")
```

**Managing another user's resources:**

```python
# Add points to a specific user
user_points = libs.Resources.anotherRes("points", "123456789")
user_points.add(25)
bot.sendMessage(f"Added 25 points to user. New total: {user_points.value()}")
```

**Administrative tasks:**

```python
# Get top scorers
admin = libs.Resources.adminRes("score")
top_scores = admin.getAllData(10)

result = "Top Scores:\n"
for entry in top_scores:
    result += f"{entry['user']}: {entry['value']}\n"
bot.sendMessage(result)
```

**Account-level resources:**

```python
# Create or access an account-level resource
subscription_points = libs.Resources.accountRes("subscription_points")

# Add points
subscription_points.add(100)

# Check current account points (accessible across all bots)
current = subscription_points.value()
bot.sendMessage(f"Account has {current} subscription points")
```


<!-- Source: https://help.telebotcreator.com/bot-features-and-functionalities.md -->

# Bot Features and Functionalities

#### **6. Bot Features and Functionalities**

This section dives into the various features and functionalities available in Telebot Creator, showing how to apply them effectively in real-world scenarios. From handling user interactions to automating tasks and broadcasting messages, these features enable you to build bots that are both powerful and versatile.

***

#### **6.1 Wildcard Master Command (`*`)**

The `*` command, also known as the **Wildcard Master Command**, is triggered when a bot receives a message that does not match any predefined command. This is useful for handling fallback responses or processing unexpected user inputs.

**Use Cases**:

* Providing default responses.
* Logging unknown commands for debugging.

**Example**:

```python
bot.sendMessage("Sorry, I didn’t understand that. Type /help for a list of commands.")
```

***

#### **6.2 At Handler Command (`@`)**

The `@` command runs **before any other command** is executed. It’s primarily used for preprocessing messages, logging user activity, or setting up global conditions.

**Use Cases**:

* Validating messages before they are processed by other commands.
* Logging user activities.

**Example**:

```python
bot.sendMessage("Processing your request...")
# Continue to the next relevant command
```

***

#### **6.3 Broadcasting Messages**

The broadcasting feature allows you to send a message or execute a command for multiple users simultaneously.

**Key Functions**:

* **`broadcast`**: Sends a message or runs a command for a group of users.
* **`clearBroadcast`**: Clears records of completed broadcasts.

**Example**:

```python
bot.broadcast("Hello, everyone! This is a broadcast message.")
```

**Advanced Example with Commands**:

```python
bot.broadcast(command="promo_offer")
```

***

#### **6.4 Captcha Generation and Validation**

Telebot Creator supports automatic and manual CAPTCHA generation to ensure security during user interactions.

**Key Functions**:

* **`genCaptcha`**: Generates a CAPTCHA.
* **`validateCaptcha`**: Validates user responses to the CAPTCHA.

**Example**:

```python
captcha = bot.genCaptcha(mode="auto")
bot.sendMessage(f"Please solve this CAPTCHA: {captcha['image_url']}")
```

***

#### **6.5 Error Handling and Debugging**

Telebot Creator includes robust error-handling tools to debug and track issues in your bot.

**Features**:

* **Error Logs**: Access error logs from the dashboard under the **Errors** menu.
* **Try-Catch Blocks**: Use exception handling in TPY to manage errors gracefully.

**Example**:

```python
try:
    bot.sendMessage("Sending a risky message.")
except Exception as e:
    bot.sendMessage(f"An error occurred: {str(e)}")
```

***

#### **6.6 Persistent Data Storage**

Use `saveData` and `getData` to store and retrieve global data for your bot.

**Use Cases**:

* Tracking user progress.
* Storing settings or configurations.

**Example**:

```python
Bot.saveData("welcome_message", "Hello, welcome to our bot!")
welcome_message = Bot.getData("welcome_message")
bot.sendMessage(welcome_message)
```

***

#### **6.7 Scheduled Commands**

Schedule commands to run after a specified delay using `runCommandAfter`.

**Use Cases**:

* Sending reminders.
* Automating periodic tasks.

**Example**:

```python
bot.sendMessage("A reminder will be sent in 10 seconds.")
Bot.runCommandAfter(10, "send_reminder")
```

In the `send_reminder` command:

```python
bot.sendMessage("This is your reminder!")
```

***

#### **6.8 Webhook Integration**

Webhooks allow your bot to receive real-time updates or trigger commands based on external events.

**Key Functions**:

* **`getUrlFor`**: Generates a webhook URL for a specific command.

**Example**:

```python
webhook_url = libs.Webhook.getUrlFor("update_user_status", user_id=12345)
bot.sendMessage(f"Webhook URL: {webhook_url}")
```

***

#### **6.9 CSV File Management**

Use the `libs.CSV` library to manage data in CSV files, such as tracking user activity or creating leaderboards.

**Example**:

```python
csv = libs.CSV.CSVHandler("leaderboard.csv")
csv.create_csv(["User", "Points"])
csv.add_row({"User": "Alice", "Points": 50})
```

***

#### **6.10 Real-Time User Points**

The `left_points` global variable tracks the remaining points for executing commands.

**Example**:

```python
points = left_points
bot.sendMessage(f"You have {points} points remaining.")
```

#### **6.11 Multi-Step User Interactions**

Telebot Creator enables seamless multi-step user interactions using commands like `handleNextCommand`. This feature allows you to guide users through a sequence of questions or tasks.

**Use Cases**:

* Collecting user information step-by-step.
* Creating interactive forms or surveys.

**Example: Collecting User Details**\
Step 1: Ask for the user's name.

```python
bot.sendMessage("What is your name?")
Bot.handleNextCommand("get_name")
```

Step 2: Process the name and ask for the email.

```python
name = msg
User.saveData("name", name)
bot.sendMessage(f"Thanks, {name}! Now, what is your email?")
Bot.handleNextCommand("get_email")
```

Step 3: Process the email and confirm.

```python
email = msg
User.saveData("email", email)
bot.sendMessage("Your details have been saved. Thank you!")
```

***

#### **6.12 Dynamic Message Replies**

Telebot Creator allows bots to provide dynamic responses using variables and user-specific data.

**Use Cases**:

* Greeting users by their name.
* Sending personalized notifications.

**Example**:

```python
first_name = message.from_user.first_name
bot.sendMessage(f"Hello {first_name}, welcome back!")
```

***

#### **6.13 Inline Keyboard and Buttons**

You can create interactive inline keyboards and buttons for your bot using TPY.

**Use Cases**:

* Providing quick action buttons.
* Navigating through menus.

**Example: Inline Keyboard**

```python
keyboard = [
    [{"text": "Option 1", "callback_data": "option1"}],
    [{"text": "Option 2", "callback_data": "option2"}],
]
bot.sendMessage("Choose an option:", reply_markup={"inline_keyboard": keyboard})
```

**Handling Button Clicks**:

```python
if callback_data == "option1":
    bot.sendMessage("You selected Option 1!")
elif callback_data == "option2":
    bot.sendMessage("You selected Option 2!")
```

***

#### **6.14 Using the Random Library**

The `libs.Random` library allows you to generate random outputs for lotteries, giveaways, or dynamic bot interactions.

**Use Cases**:

* Picking random winners.
* Generating unique codes.

**Example: Generating a Random Number**

```python
random_number = libs.Random.randomInt(1, 100)
bot.sendMessage(f"Your random number is: {random_number}")
```

**Example: Generating a Random String**

```python
random_string = libs.Random.randomStr(8)
bot.sendMessage(f"Your unique code is: {random_string}")
```

***

#### **6.15 User Resource Management**

Manage user-specific resources such as points, credits, balance or quotas using the `libs.Resources` library.

**Use Cases**:

* Awarding points for user actions.
* Tracking balances for memberships or services.

**Example**:

```python
points = libs.Resources.userRes("points", user)
points.add(10)
bot.sendMessage(f"You have earned 10 points! Total points: {points.value()}")
```

***

#### **6.16 Advanced Broadcasting Options**

Broadcasting messages to users can be fine-tuned with custom commands or targeting specific groups.

**Use Cases**:

* Sending promotions to active users.
* Notifying specific users about updates.

**Advanced Example: Custom Command Broadcast**

```python
bot.broadcast(command="special_offer")
```

**Targeted Broadcasts**:

```python
users = [12345, 67890]  # List of user IDs
for user in users:
    bot.sendMessage(f"Hello, user {user}! Check out our latest offer.")
```

***

#### **6.17 Debugging Features**

Debugging is essential for ensuring your bot functions as expected. Telebot Creator provides multiple tools for error handling and tracking.

**Tools Available**:

1. **Errors Menu**:
   * Access error logs directly from the dashboard.
2. **Try-Except Handling**:
   * Use Python-style error handling to catch and manage exceptions.

**Example**:

```python
try:
    bot.sendMessage("Sending a critical message.")
except Exception as e:
    bot.sendMessage(f"An error occurred: {str(e)}")
```

***

#### **6.18 Automation with Webhooks**

Webhooks enable your bot to react to external events in real-time, such as receiving payments or triggering commands based on third-party API updates.

**Use Cases**:

* Automating responses to external triggers.
* Integrating with payment gateways or external systems.

**Example: Generating a Webhook URL**

```python
webhook_url = libs.Webhook.getUrlFor("payment_received", user_id=12345)
bot.sendMessage(f"Your webhook URL is: {webhook_url}")
```

***

#### **6.19 Managing Scheduled Tasks**

With `runCommandAfter`, you can schedule tasks to execute at a later time.

**Use Cases**:

* Sending periodic reminders.
* Automating recurring updates.

**Example**:

```python
bot.sendMessage("A reminder will be sent in 30 seconds.")
Bot.runCommandAfter(30, "reminder_task")
```

In the `reminder_task` command:

```python
bot.sendMessage("This is your reminder!")
```

***

#### **6.20 Combining Features for Complex Bots**

By combining these features, you can create highly interactive and functional bots.

**Example: Multi-Feature Use Case**

* A bot that collects user information, awards points, and broadcasts updates:

```python
bot.sendMessage("Welcome! Let’s start by getting your name.")
Bot.handleNextCommand("get_name")
```

In the `get_name` command:

```python
name = msg
User.saveData("name", name)
bot.sendMessage(f"Thanks, {name}! You’ve earned 10 points.")
points = libs.Resources.userRes("points", user)
points.add(10)
Bot.runCommandAfter(5, "send_update")
```

In the `send_update` command:

```python
bot.broadcast("Thank you for joining! Check out our updates.")
```

#### **6.21 Example Scenarios for Real-World Use Cases**

**1. Referral System**

Track and reward users for referring others to your bot.

**Workflow**:

1.  **User Shares Referral Link**:

    * Generate a unique referral link using `params` in the `/start` command.

    ```python
    pythonCopyEditbot.sendMessage(f"Invite your friends using this link: t.me/{bot.username}?start={u}")
    ```
2.  **Track Referrals**:

    * When a new user joins using the link, log the referrer.

    ```python
    pythonCopyEditreferrer = params
    if referrer:
        referrer_points = libs.Resources.userRes("points", referrer)
        referrer_points.add(10)
        bot.sendMessage(f"User {referrer} has earned 10 points!")
    ```
3.  **Reward Top Referrers**:

    * Use `libs.Resources.userRes` to fetch the top contributors.

    ```python
    pythonCopyEdittop_referrers = libs.Resources.userRes("points").getAllData(5)
    bot.sendMessage(f"Top referrers: {top_referrers}")
    ```

***

**2. Event Reminder Bot**

Let users set reminders for specific dates and times.

**Workflow**:

1.  **Collect Event Details**:

    ```python
    bot.sendMessage("What is the event name?")
    Bot.handleNextCommand("get_event_name")
    ```
2.  **Ask for the Date and Time**:

    ```python
    event_name = msg
    User.saveData("event_name", event_name)
    bot.sendMessage("When is the event? (Format: YYYY-MM-DD HH:MM)")
    Bot.handleNextCommand("get_event_time")
    ```
3.  **Schedule the Reminder**:

    ```python
    event_time = msg  # Save and validate date-time
    Bot.runCommandAfter(seconds_until_event, "send_event_reminder")
    bot.sendMessage("Reminder scheduled!")
    ```
4.  **Send the Reminder**:

    ```python
    event_name = User.getData("event_name")
    bot.sendMessage(f"Reminder: The event '{event_name}' is happening now!")
    ```

***

#### **6.22 Integration Highlights**

**Fetching External Data with `libs.customHTTP`**

Integrate your bot with external APIs to provide dynamic content.

**Example: Fetching Weather Data**

```python
http_client = libs.customHTTP()
response = http_client.get("https://api.weatherapi.com/v1/current.json?key=API_KEY&q=London")
weather_data = response.json()
bot.sendMessage(f"Current temperature in London: {weather_data['current']['temp_c']}°C")
http_client.close()
```

***

#### **6.24 Feature Customization Options**

**Custom Inline Keyboards**

Create dynamic options for users.

```python
keyboard = [
    [{"text": "Buy Now", "url": "https://example.com"}],
    [{"text": "Contact Support", "callback_data": "contact_support"}],
]
bot.sendMessage("Choose an action:", reply_markup={"inline_keyboard": keyboard})
```

***

#### **6.25 Common Mistakes and Solutions**

| **Mistake**                            | **Solution**                                                           |
| -------------------------------------- | ---------------------------------------------------------------------- |
| Incorrectly scheduling commands.       | Ensure the time delay for `runCommandAfter` is accurate and positive.  |
| Resource mismanagement (e.g., points). | Use `libs.Resources` consistently to avoid overwriting or losing data. |
| Webhook not triggering.                | Verify the webhook URL and ensure the command exists in your bot.      |

***

#### **6.26 Debugging with Logs**

**Access Logs via the Dashboard**:

* Use the **Errors** menu to view logs for failed commands or system issues.

**Inline Logging**:

```python
try:
    bot.sendMessage("Processing your request...")
except Exception as e:
    bot.sendMessage(f"Error: {e}") # or use 
    Bot.saveData("last_error", str(e))
```


<!-- Source: https://help.telebotcreator.com/advanced-features.md -->

# Advanced Features

#### **7. Advanced Features**

Telebot Creator offers powerful advanced features that extend basic bot functionality. This section explores these capabilities, including custom data storage, scheduled tasks, integration with external systems, and managing user interactions, among others.

***

### **7.1 Scheduled Commands**

Telebot Creator allows you to schedule commands to run at specific intervals, creating chatbots that can perform time-based tasks.

#### **Bot.runCommandAfter**

The `Bot.runCommandAfter` function lets you schedule a command to run after a specific time delay.

***

**Function Syntax**:

```python
Bot.runCommandAfter(
    delay_seconds: float,
    command: str,
    user_id: Optional[str] = None,
    chat_id: Optional[str] = None,
    params: Optional[str] = None,
    bot_id: Optional[str] = None,
    api_key: Optional[str] = None
)
```

> **New in 4.9.0**:
>
> * Maximum timeout extended to 1 year (365 days)
> * Minimum timeout reduced to 0.1 seconds
> * Smart rate limiting: For ultra-fast commands (under 0.4 seconds), a limit of 5 executions within 5 seconds to prevent abuse
> * Increased maximum scheduled commands per user from 20 to 100

**Parameters**:

* **`delay_seconds`** (_float_): The delay in seconds before executing the command. Range: 0.1 to 31,536,000 (365 days).
* **`command`** (_str_): The command to execute after the delay.
* **`user_id`** (_Optional\[str]_): The user ID for which to execute the command.
* **`chat_id`** (_Optional\[str]_): The chat ID in which to execute the command.
* **`params`** (_Optional\[str]_): Parameters to pass to the command.
* **`bot_id`** (_Optional\[str]_): The bot ID for which to schedule the command.
* **`api_key`** (_Optional\[str]_): The API key for authentication with external bots.

**Examples**:

1.  **Basic Scheduling**:

    ```python
    Bot.runCommandAfter(300, "reminder")  # Run the reminder command after 5 minutes
    ```
2.  **User-Specific Scheduling**:

    ```python
    Bot.runCommandAfter(3600, "daily_check", user_id=12345)  # Run for specific user after 1 hour
    ```
3.  **With Parameters**:

    ```python
    Bot.runCommandAfter(60, "send_reminder", params="meeting")  # Pass parameters to the command
    ```
4.  **Long-term Scheduling**:

    ```python
    # Schedule a command to run in 30 days (new in 4.9.0)
    Bot.runCommandAfter(2592000, "monthly_report") 
    ```
5.  **Ultra-fast Task**:

    ```python
    # Quick follow-up message (subject to rate limiting in 4.9.0)
    Bot.runCommandAfter(0.2, "send_followup") 
    ```

***

#### **7.2 Command Chaining for Workflows**

Command chaining allows bots to create step-by-step workflows, guiding users through complex processes such as registration, surveys, or multi-step forms.

**Example: Multi-Step Registration**

1.  **Start the Workflow**:

    ```python
    bot.sendMessage("Welcome! Let's start with your name.")
    Bot.handleNextCommand("get_name")
    ```
2.  **Process Name**:

    ```python
    name = msg
    User.saveData("name", name)
    bot.sendMessage(f"Thanks, {name}! What is your email?")
    Bot.handleNextCommand("get_email")
    ```
3.  **Complete Registration**:

    ```python
    email = msg
    User.saveData("email", email)
    bot.sendMessage("Your registration is complete!")
    ```

***

#### **7.3 Custom API Integrations**

With `libs.customHTTP`, bots can interact with external APIs, enabling dynamic data fetching or triggering external processes.

**Example: Weather Bot**:

```python
http_client = libs.customHTTP()
response = http_client.get("https://api.weatherapi.com/v1/current.json?key=API_KEY&q=New York")
weather_data = response.json()
bot.sendMessage(f"The current temperature in New York is {weather_data['current']['temp_c']}°C.")
http_client.close()
```

***

#### **7.4 Webhook Management**

The `libs.Webhook` library facilitates real-time event handling, such as receiving external updates or triggering bot commands.

**Example: Webhook for Payment Confirmation**:

```python
webhook_url = libs.Webhook.getUrlFor("payment_received", user_id=12345)
bot.sendMessage(f"Webhook URL: {webhook_url}")
```

***

#### **7.5 Bot.Transfer Function**

The `Bot.Transfer` function allows you to transfer a bot from one Telebot Creator account to another. It ensures that the transferred bot retains its commands, configurations, and status while validating points and ownership.

**Function Syntax**

```python
Bot.Transfer(email: str, bot_id: str, bot_token: Optional[str] = None, run_now: Optional[bool] = False) -> dict
```

**Parameters**

* **`email`**: The email address of the new owner.
* **`bot_id`**: The unique ID of the bot to be transferred.
* **`bot_token`** (optional): The Telegram Bot API token. Required if `run_now` is `True`.
* **`run_now`** (optional): If `True`, starts the bot immediately under the new owner.

**Validation and Requirements**

* The transferring user must own the bot (`bot_id`) being transferred.
* The new owner's email must exist on Telebot Creator.
* The original account must have at least 200 points to initiate the transfer.

**Usage Example**

```python
try:
    result = Bot.Transfer(
        email="<newowner>@example.com",
        bot_id="123456",
        bot_token="YOUR_BOT_API_TOKEN",
        run_now=True
    )
    bot.sendMessage(f"Bot successfully transferred to {result['bot_id']}!")
except Exception as e:
    bot.sendMessage(f"Error during transfer: {e}")
```

***

#### **7.6 Bot.info() Function**

The `Bot.info()` function retrieves detailed information about a specific bot, including its status, owner details, points, and usage statistics.

**Function Syntax**

```python
Bot.info(bot_id: Optional[str] = None, api_key: Optional[str] = None) -> dict
```

**Parameters**

* **`bot_id`** (optional): The ID of the bot to retrieve information for. If not provided, retrieves info for the current bot.
* **`api_key`** (optional): The API key of the bot owner. Used for validation if `bot_id` is provided.

**Information Returned**

* **`token`**: The bot's API token.
* **`bot_id`**: The unique ID of the bot.
* **`owner_email`**: The email of the current bot owner.
* **`status`**: The bot's current status (e.g., "Working", "Stopped").
* **`username`**: The bot's Telegram username.
* **`first_name`**: The bot's first name.
* **`account_points`**: Remaining points in the owner's account.
* **`userstat`**: Number of users interacting with the bot.

**Usage Example**

```python
try:
    details = Bot.info()
    bot.sendMessage(f"Bot Name: {details.first_name}, Status: {details.status}")
except Exception as e:
    bot.sendMessage(f"Error fetching bot info: {e}")
```

**Validation**

* Returns structured and human-readable details about the bot.

***

#### **7.7 Multi-Bot Management**

For users managing multiple bots, Telebot Creator allows seamless integration between them.

**Example: Interaction Between Two Bots**

1.  Bot A triggers Bot B via a webhook:

    ```python
    webhook_url = libs.Webhook.getUrlFor("bot_b_command", user_id=12345)
    bot.sendMessage(f"Triggering Bot B: {webhook_url}")
    ```
2.  Bot B handles the webhook and sends a response:

    ```python
    bot.sendMessage("Response from Bot B!")
    ```

***

#### **7.8 Advanced Error Handling**

Implement advanced error-handling techniques to ensure smooth workflows.

**Example**:

```python
try:
    response = libs.customHTTP().get("https://invalid.url")
    response.raise_for_status()
except Exception as e:
    bot.sendMessage(f"Error occurred: {str(e)}")
```

#### **7.9 Bot.Transfer (Expanded Use Cases)**

**1. Bot Migration Between Users**

The `Bot.Transfer` function allows seamless migration of bots from one account to another, ensuring no loss of functionality or data.

**Real-World Scenario**:

* **Use Case**: A developer transfers a bot to a business partner who will manage the bot moving forward.
*   **Example**:

    ```python
    try:
        result = Bot.Transfer(
            email="partner@example.com",
            bot_id="123456",
            bot_token="API_TOKEN",
            run_now=True
        )
        bot.sendMessage(f"Bot successfully transferred! New Bot ID: {result['bot_id']}")
    except Exception as e:
        bot.sendMessage(f"Transfer failed: {e}")
    ```

**2. Batch Transfer**

Use the `Bot.Transfer` function for multiple bots by iterating through bot IDs.

```python
bots_to_transfer = ["123456", "654321"]
for bot_id in bots_to_transfer:
    try:
        Bot.Transfer(email="newowner@example.com", bot_id=bot_id, run_now=False)
        bot.sendMessage(f"Bot ID {bot_id} transferred successfully.")
    except Exception as e:
        bot.sendMessage(f"Failed to transfer Bot ID {bot_id}: {e}")
```

***

#### **7.10 Bot.info() (Expanded Details)**

The `Bot.info()` function is a powerful tool for retrieving comprehensive bot details. It provides insight into bot usage, configurations, and ownership.

**Advanced Usage Scenarios**

1.  **Bot Status Monitoring**:

    * Periodically fetch and log bot statuses for analytics or troubleshooting.

    ```python
    details = Bot.info(bot_id="123456", api_key="VALID_API_KEY")
    bot.sendMessage(f"Bot {details.first_name} is currently {details.status}.")
    ```
2.  **Ownership Verification**:

    * Verify bot ownership before performing sensitive operations.

    ```python
    details = Bot.info(bot_id="123456", api_key="VALID_API_KEY")
    if details.owner_email == "admin@example.com":
        bot.sendMessage("Ownership verified.")
    ```
3.  **Integration with Dashboards**:

    * Fetch bot stats for visual dashboards.

    ```python
    bot_stats = Bot.info(bot_id="123456", api_key="VALID_API_KEY")
    bot.sendMessage(f"Bot Username: {bot_stats.username}, Points Remaining: {bot_stats.account_points}")
    ```

***

#### **7.11 Advanced API Integrations**

**1. Fetch and Process Data**

Integrate third-party APIs dynamically using `libs.customHTTP`.

**Example**: Fetching cryptocurrency prices.

```python
http_client = libs.customHTTP()
response = http_client.get("https://api.coindesk.com/v1/bpi/currentprice/BTC.json")
price_data = response.json()
bot.sendMessage(f"Current Bitcoin Price: {price_data['bpi']['USD']['rate']}")
http_client.close()
```

**2. Post Data to External Systems**

Use POST requests to send data to external APIs.

```python
http_client = libs.customHTTP()
response = http_client.post("https://api.example.com/submit", json={"user": "123", "action": "register"})
if response.status_code == 200:
    bot.sendMessage("Data successfully submitted!")
http_client.close()
```

**3. Automate Tasks Using Webhooks**

Automatically trigger bot actions based on webhook updates.

```python
webhook_url = libs.Webhook.getUrlFor("update_action", user_id=12345)
bot.sendMessage(f"Webhook URL for updates: {webhook_url}")
```

***

#### **7.12 Multi-Bot Management (Expanded)**

**1. Orchestrating Bots**

Enable communication between bots for advanced workflows.

* **Scenario**: Bot A collects user data and triggers Bot B to send notifications.

**Example**:

1.  **Bot A** collects data and calls Bot B's webhook:

    ```python
    webhook_url = libs.Webhook.getUrlFor(
        "notify_points",
        user_id=12345, # Don't add user_id if you don't want user specific webhook url
        bot_id="another_bot_id",
        api_key="another_bot_api_key"
    )
    bot.sendMessage(f"Webhook URL for another bot: {webhook_url}")
    ```
2.  **Bot B** processes the webhook:

    ```python
    bot.sendMessage("Notification sent via Bot B!")
    ```

**2. Delegating Tasks**

Use a primary bot to assign tasks to secondary bots.

```python
bot_ids = ["bot_123", "bot_456"]
for bot_id in bot_ids:
    Bot.runCommand(bot_id, "execute_task")
```

***

#### **7.13 Enhanced Error Handling**

**Logging Errors for Debugging**

Save errors to a persistent log for later review.

```python
try:
    risky_task()
except Exception as e:
    error_message = f"An error occurred: {str(e)}"
    Bot.saveData("last_error", error_message)
    bot.sendMessage(error_message)
```

**Custom Error Handlers**

Define custom actions for specific errors.

```python
try:
    execute_critical_task()
except ValueError as ve:
    bot.sendMessage(f"Value Error: {ve}")
except Exception as e:
    bot.sendMessage(f"Unhandled Error: {e}")
```

***

#### **7.14 Combining Features for Real-World Applications**

**Use Case: Survey Bot with API Integration**

1.  **Step 1: Collect User Input**

    ```python
    bot.sendMessage("What is your name?")
    Bot.handleNextCommand("collect_name")
    ```
2.  **Step 2: Process and Store Data**

    ```python
    name = msg
    User.saveData("name", name)
    bot.sendMessage(f"Thank you, {name}. What's your email?")
    Bot.handleNextCommand("collect_email")
    ```
3.  **Step 3: Send Data to an API**

    ```python
    email = msg
    User.saveData("email", email)
    http_client = libs.customHTTP()
    response = http_client.post(
        "https://api.example.com/register",
        json={"name": User.getData("name"), "email": email}
    )
    if response.status_code == 200:
        bot.sendMessage("Registration successful!")
    http_client.close()
    ```

**Use Case: Reward Bot with Multi-Bot Management**

1.  Bot A verifies user actions and updates points.

    ```python
    User.saveData("points", User.getData("points") + 10)
    bot.sendMessage("You've earned 10 points!")
    ```
2.  Bot B notifies the user via a secondary bot:

    ```python
    webhook_url = libs.Webhook.getUrlFor("notify_points", user_id=12345)
    bot.sendMessage(f"Notification sent via webhook: {webhook_url}")
    ```

***

####


<!-- Source: https://help.telebotcreator.com/real-world-use-cases.md -->

# Real-World Use Cases

#### **8. Real-World Use Cases**

This section demonstrates how to apply Telebot Creator’s features and libraries in real-world scenarios. By combining workflows, advanced commands, and external integrations, you can create bots that solve practical problems and enhance user engagement.

***

### **8.1 Referral System**

#### **Overview**

A referral system tracks users who invite others to the bot and rewards them with points or other incentives. This use case involves:

1. Generating unique referral links.
2. Tracking referrals.
3. Rewarding users based on their referral count.
4. Displaying leaderboards for top referrers.

***

#### **Implementation**

**Step 1: Generate Unique Referral Links**

In the `/start` command, include the user’s ID as a parameter to generate a referral link:

```python
bot.sendMessage(f"Invite your friends using this link: t.me/{bot.username}?start={u}")
```

**Step 2: Track Referrals**

In the `/start` command, check if a referral ID is provided:

```python
referrer_id = params
if referrer_id:
    referrer_points = libs.Resources.userRes("points", referrer_id)
    referrer_points.add(10)
    bot.sendMessage(f"User {referrer_id} has earned 10 points for referring you!")
```

**Step 3: Reward Users**

Track and display referral rewards dynamically:

```python
user_points = libs.Resources.userRes("points", u)
bot.sendMessage(f"You have {user_points.value()} points!")
```

**Step 4: Create a Leaderboard**

Display the top referrers using `libs.Resources`:

```python
top_referrers = libs.Resources.userRes("points").getAllData(5)
leaderboard = "\n".join([f"{i+1}. User {entry['user']}: {entry['value']} points" for i, entry in enumerate(top_referrers)])
bot.sendMessage(f"Top Referrers:\n{leaderboard}")
```

***

### **8.2 Payment Automation Bot**

#### **Overview**

This bot automates payment handling using the `libs.Coinbase` library. It can:

1. Generate payment requests.
2. Confirm payment status.
3. Notify users of successful payments.

***

#### **Implementation**

**Step 1: Set Up Coinbase Client**

Configure the Coinbase client with your API keys:

```python
libs.Coinbase.setKeys("your_api_key", "your_api_secret")
client = libs.Coinbase.post()
```

**Step 2: Generate Payment Requests**

Request payment for specific amounts:

```python
payment_details = client.createCharge({
    "name": "Subscription Payment",
    "description": "Monthly subscription fee",
    "local_price": {"amount": "10.00", "currency": "USD"},
    "pricing_type": "fixed_price"
})
bot.sendMessage(f"Please make your payment here: {payment_details['hosted_url']}")
```

**Step 3: Verify Payment Status**

Check payment status using the charge ID:

```python
charge_id = "charge_id_from_payment"
status = client.retrieveCharge(charge_id)['status']
if status == "CONFIRMED":
    bot.sendMessage("Payment confirmed! Thank you!")
else:
    bot.sendMessage(f"Payment status: {status}")
```

***

### **8.3 Survey and Data Collection Bot**

#### **Overview**

This bot collects user input for surveys or forms and stores the data in a CSV file for easy analysis.

***

#### **Implementation**

**Step 1: Collect User Responses**

Ask users a series of questions:

```python
bot.sendMessage("What is your name?")
Bot.handleNextCommand("get_name")
```

Store the responses:

```python
name = msg
User.saveData("name", name)
bot.sendMessage("What is your email?")
Bot.handleNextCommand("get_email")
```

**Step 2: Save Data to CSV**

Save the collected data into a CSV file using `libs.CSV`:

```python
csv_handler = libs.CSV.CSVHandler("survey_data.csv")
csv_handler.create_csv(["Name", "Email"])
csv_handler.add_row({"Name": User.getData("name"), "Email": User.getData("email")})
bot.sendMessage("Your responses have been saved. Thank you!")
```

***

### **8.4 Crypto Airdrop Bot**

#### **Overview**

This bot automates cryptocurrency distributions using the `libs.Polygon` library.

***

#### **Implementation**

**Step 1: Configure Polygon Keys**

Set the private key for transactions:

```python
libs.Polygon.setKeys("your_private_key")
```

**Step 2: Automate Token Transfers**

Send tokens to multiple recipients:

```python
recipients = [
    {"address": "0xRecipient1", "amount": 10},
    {"address": "0xRecipient2", "amount": 15}
]

for recipient in recipients:
    libs.Polygon.send(
        value=recipient["amount"],
        to=recipient["address"],
        contract="contract_address"
    )
    bot.sendMessage(f"Sent {recipient['amount']} tokens to {recipient['address']}")
```

***

### **8.5 Real-Time Notification Bot**

#### **Overview**

This bot uses `libs.Webhook` to send real-time updates based on external events, such as sales or user actions.

***

#### **Implementation**

**Step 1: Generate Webhook URL**

Generate a webhook URL for notifications:

```python
webhook_url = libs.Webhook.getUrlFor("send_notification", user_id=12345)
bot.sendMessage(f"Webhook URL: {webhook_url}")
```

**Step 2: Process Webhook Events**

Handle incoming webhook events in a command:

```python
bot.sendMessage("You have a new sale! Congratulations!")
```

***

### **8.6 Event Management Bot**

#### **Overview**

This bot manages events, allowing users to RSVP, receive reminders, and track attendance.

***

#### **Implementation**

**Step 1: RSVP System**

Allow users to RSVP to an event:

```python
bot.sendMessage("Would you like to attend the event? Reply with 'Yes' or 'No'.")
Bot.handleNextCommand("process_rsvp")
```

Store responses:

```python
response = msg
if response.lower() == "yes":
    User.saveData("RSVP", "Yes")
    bot.sendMessage("Thank you for RSVPing!")
else:
    bot.sendMessage("Maybe next time!")
```

**Step 2: Event Reminders**

Send reminders using `runCommandAfter`:

```python
Bot.runCommandAfter(3600, "send_event_reminder")
```

In the reminder command:

```python
bot.sendMessage("Reminder: The event starts in 1 hour!")
```

***

### **8.7 Tips and Best Practices**

1. **Optimize Point Usage**:
   * Combine commands where possible.
   * Use wildcards (`*`) for unstructured messages to reduce redundant commands.
2. **Handle Large User Bases**:
   * Use in-built broadcasting strategies.
   * Target active users only.
3. **Secure Data**:
   * Encrypt sensitive user data.
   * Use HTTPS webhooks for secure communication.


<!-- Source: https://help.telebotcreator.com/tips-best-practices-and-troubleshooting.md -->

# Tips, Best Practices, and Troubleshooting

#### **9. Tips, Best Practices, and Troubleshooting**

This section provides essential guidance for optimizing bot performance, managing resources effectively, ensuring security, and troubleshooting common issues in Telebot Creator. By following these practices, you can create highly reliable, efficient, and secure bots.

***

### **9.1 Tips for Optimizing Your Bot**

#### **Efficient Point Usage**

1.  **Combine Actions into a Single Command**:

    * Reduce redundant commands by combining related actions.

    ```python
    bot.sendMessage("Welcome!")
    bot.sendMessage("Use /help for instructions.")
    ```

    **Combine into one:**

    ```python
    bot.sendMessage("Welcome! Use /help for instructions.")
    ```
2. **Use Targeted Broadcasts**:
   * Use `Bot.broadcast()` to reach your audience efficiently instead of manual loops.
3.  **Schedule Tasks Appropriately**:

    * Use `runCommandAfter` for periodic tasks to avoid invoking commands unnecessarily.

    ```python
    Bot.runCommandAfter(3600, "send_reminder")  # Execute a reminder after 1 hour
    ```

    > **New in 4.9.0**: You can now schedule tasks up to 1 year (365 days) ahead, with a minimum interval of 0.1 seconds. Maximum scheduled tasks per user increased from 20 to 100.
4.  **Minimize Repeated API Calls**:

    * Cache data that doesn't change frequently (e.g., user statistics or configuration).

    > **New in 4.9.0**: Use standard `HTTP` module instead of `libs.customHTTP()` for better performance and reliability.

***

#### **Enhancing Performance**

1. **Handle Large User Bases**:
   * Use asynchronous operations and efficient workflows to manage broadcasts or commands.
   * Limit unnecessary broadcasts to inactive users.
2. **Optimize User Interactions**:
   * Use `handleNextCommand` to guide users through workflows instead of using multiple commands.
3. **Efficient Error Handling**:
   *   Log and analyze errors for better debugging:

       ```python
       try:
           bot.sendMessage("Attempting an action...")
       except Exception as e:
           Bot.saveData("last_error", str(e))
           bot.sendMessage(f"Error occurred: {e}")
       ```

***

#### **Code Execution Limits**

> **New in 4.9.0**:
>
> 1. Code execution timeout has been extended from 60 to 120 seconds.
> 2. A new `time.sleep()` function is available with a maximum limit of 10 seconds.
> 3. For ultra-fast commands (under 0.4 seconds), a rate limit of 5 executions within 5 seconds is enforced to prevent abuse.
> 4. Do not use `import x` statements in your code. Use the built-in libraries instead.
> 5. For handling inline queries and other update types, use the `/handler_<update_type>` command format.

***

#### **Improving Security**

1. **Secure Sensitive Data**:
   * Encrypt user data (e.g., emails or payment information) before saving it.
2. **Dynamic Webhook Generation**:
   *   Generate secure webhook URLs with `libs.Webhook.getUrlFor` and validate inputs:

       ```python
       webhook_url = libs.Webhook.getUrlFor("process_data", user_id=12345)
       ```
3. **Restrict API Access**:
   * Use API keys for authentication when interacting with external systems.
4. **Data Minimization**:
   * Store only the data you need to avoid unnecessary risk.

***

### **9.2 Best Practices**

#### **Developing Reliable Workflows**

1.  **Use Multi-Step Commands**:

    * Break complex processes into smaller steps using `handleNextCommand`.

    ```python
    bot.sendMessage("What's your name?")
    Bot.handleNextCommand("get_name")
    ```
2.  **Validate Inputs**:

    * Always validate user inputs to prevent errors or misuse.

    ```python
    if not params.isnumeric():
        bot.sendMessage("Invalid input. Please enter a valid number.")
    ```

***

#### **Optimizing Bot Features**

1. **Leverage Built-In Libraries**:
   * Use libraries like `libs.CSV` for data management or `libs.Random` for randomization.
2.  **Monitor Points Usage**:

    * Use `Bot.info()` to track points and optimize commands accordingly.

    ```python
    details = Bot.info(bot_id="123456")
    bot.sendMessage(f"Points left: {details.account_points}")
    ```
3.  **Use Test Runs for Broadcasts**:

    * Validate your broadcast before deploying to avoid errors or excessive point usage.

    ```python
    Bot.broadcast(
        function="send_message",
        text="Testing the broadcast system."
    )
    ```

***

### **9.3 Troubleshooting Common Issues**

#### **Command Errors**

* **Issue**: The bot doesn't respond to a command.
* **Causes**:
  * Command is misspelled or case-sensitive mismatch.
  * Missing parameters in the command.
* **Solution**:
  * Verify the command exists and is spelled correctly.
  * Ensure required parameters are passed.

***

#### **Broadcast Failures**

* **Issue**: Broadcast does not execute or returns an error.
* **Causes**:
  * Too many running broadcasts (limit: 2 per bot, 1000 globally).
  * Invalid or unsupported `function`.
* **Solution**:
  *   Check broadcast limits:

      ```python
      Bot.broadcast(
          function="send_message",
          text="Broadcast Test Message"
      )
      ```
  * Use only supported functions for broadcasting.

***

#### **Webhook Issues**

* **Issue**: Webhook does not trigger the intended command.
* **Causes**:
  * Incorrect webhook URL.
  * Command does not exist in the bot.
* **Solution**:
  *   Validate webhook URL generation:

      ```python
      webhook_url = libs.Webhook.getUrlFor("update_event", user_id=12345)
      bot.sendMessage(f"Webhook URL: {webhook_url}")
      ```
  * Ensure the command is properly defined in the bot.

***

#### **Payment Errors**

* **Issue**: Payments fail or do not register.
* **Causes**:
  * Incorrect API keys or misconfigured payment gateway.
  * Network issues between bot and payment service.
* **Solution**:
  *   Verify API keys and gateway settings:

      ```python
      libs.Coinbase.setKeys("API_KEY", "SECRET")
      client = libs.Coinbase.post()
      ```

***

#### **Bot Transfer Issues**

* **Issue**: Bot transfer fails.
* **Causes**:
  * Insufficient points (minimum 200 required).
  * Invalid `bot_id` or `api_key`.
* **Solution**:
  *   Check points using `Bot.info()`:

      ```python
      details = Bot.info(bot_id="123456")
      bot.sendMessage(f"Points available: {details.account_points}")
      ```

***

#### **General Debugging Tips**

1. **Log Errors**:
   *   Use `Bot.saveData()` to log errors for analysis:

       ```python
       try:
           risky_task()
       except Exception as e:
           Bot.saveData("last_error", str(e))
           bot.sendMessage(f"Error: {e}")
       ```
2. **Verify Configurations**:
   * Double-check settings for commands, libraries, and webhooks.

***

### **9.4 Advanced Tips**

#### **Monitor Bot Performance**

*   Use `Bot.info()` to retrieve metrics like status, user engagement, and remaining points:

    ```python
    details = Bot.info(bot_id="123456")
    bot.sendMessage(f"Bot Status: {details.status}, Points Left: {details.account_points}")
    ```

***

#### **Scale with Multi-Bot Management**

*   Enable communication between multiple bots using webhooks:

    ```python
    webhook_url = libs.Webhook.getUrlFor(
        command="notify_event",
        bot_id="another_bot_id",
        api_key="another_bot_api_key"
    )
    bot.sendMessage(f"Webhook for another bot: {webhook_url}")
    ```

***

#### **Secure API Keys and Tokens**

* Regularly rotate API keys and ensure they are not exposed in public logs or repositories

#### **9.5 Advanced Use Cases for Tips and Best Practices**

**1. Efficient Data Management with CSV**

Telebot Creator's `libs.CSV` library allows you to handle large datasets effectively. Use this for leaderboards, attendance tracking, or survey results.

**Example: Create and Update a Leaderboard**

```python
csv_handler = libs.CSV.CSVHandler("leaderboard.csv")
csv_handler.create_csv(["Name", "Points"])

# Add or update a user's points
csv_handler.add_row({"Name": "Alice", "Points": 100})
csv_handler.edit_row(0, {"Name": "Alice", "Points": 150})  # Update Alice's points

leaderboard = csv_handler.get()
bot.sendMessage(f"Leaderboard: {leaderboard}")
```

***

**2. Payment Handling with Coinbase**

Efficiently handle payments using `libs.Coinbase`. Automate user interactions based on payment status.

**Example: Automate Subscription Payments**

```python
libs.Coinbase.setKeys("API_KEY", "SECRET")
client = libs.Coinbase.post()

# Create a payment request
payment = client.createCharge({
    "name": "Subscription",
    "description": "Monthly Subscription",
    "local_price": {"amount": "10.00", "currency": "USD"},
    "pricing_type": "fixed_price"
})

bot.sendMessage(f"Pay here: {payment['hosted_url']}")

# Check payment status
charge_id = payment["id"]
status = client.retrieveCharge(charge_id)["status"]

if status == "CONFIRMED":
    bot.sendMessage("Thank you for your payment!")
else:
    bot.sendMessage(f"Payment is still pending. Status: {status}")
```

***

**3. Dynamic Webhook Management**

Using `libs.Webhook.getUrlFor`, you can dynamically create webhooks for real-time event handling.

**Example: Notify Users on External Events**

```python
webhook_url = libs.Webhook.getUrlFor(
    command="notify_user",
    user_id=12345
)
bot.sendMessage(f"Webhook URL: {webhook_url}")
```

**Handle Notifications in the `notify_user` Command**:

```python
bot.sendMessage("You've received a new notification!")
```

***

**4. Combining Multi-Step Interactions with Reminders**

Create workflows that interact with users and automate follow-ups.

**Example: Survey with Reminders**

1.  Collect user input:

    ```python
    bot.sendMessage("What's your favorite color?")
    Bot.handleNextCommand("save_color")
    ```
2.  Save the input and set a reminder:

    ```python
    color = msg
    User.saveData("favorite_color", color)
    bot.sendMessage(f"Got it! Your favorite color is {color}.")
    Bot.runCommandAfter(3600, "send_reminder")
    ```
3.  Send the reminder:

    ```python
    bot.sendMessage("Don't forget to tell your friends about our bot!")
    ```

***

#### **9.6 Advanced Debugging Techniques**

**1. Track Errors Over Time**

Store error logs with timestamps for later analysis:

```python
try:
    risky_action()
except Exception as e:
    bot.sendMessage(f"An error occurred: {e}")
```

Retrieve and review logs:

```python
logs = Bot.getData("error_log")
bot.sendMessage(f"Error Logs:\n{logs}")
```

***

**2. Use Test Runs for Broadcasts**

Before sending a broadcast to all users, validate it with a test run:

```python
Bot.broadcast(
    function="send_message",
    text="Testing broadcast system."
)
```

***

#### **9.7 Real-World Scenarios for Best Practices**

**Scenario 1: Handling a Viral Campaign**

When a bot receives an influx of users due to a campaign:

* Use caching for common responses to reduce API calls.
* Implement a queue system for processing tasks like rewards or verifications.

**Scenario 2: Managing High Broadcast Demand**

If multiple broadcasts are required:

* Use `Bot.broadcast()` with precise targeting to avoid exceeding limits.
*   Monitor broadcasts with:

    ```python
    status = self.db['broadstatus'].find({"status": "running"})
    bot.sendMessage(f"Current running broadcasts: {len(list(status))}")
    ```

**Scenario 3: Secure Payment Bot**

* Rotate API keys regularly.
*   Use `callback_url` to handle payment confirmations securely:

    ```python
    Bot.broadcast(
        function="send_message",
        text="Your subscription has been activated!",
        callback_url="https://example.com/payment-callback"
    )
    ```

***

#### **9.8 Frequently Asked Questions (FAQs)**

**1. Why isn't my command executing?**

* **Check**: Ensure the command exists and matches the trigger exactly.
* **Fix**: Verify case sensitivity and parameter requirements.

**2. What should I do if a webhook fails?**

* **Check**: Confirm the webhook URL and command are valid.
*   **Fix**: Regenerate the webhook with:

    ```python
    libs.Webhook.getUrlFor(command="my_command", user_id=12345)
    ```

**3. Why are broadcasts limited?**

* **Reason**: Each bot is limited to 2 broadcasts to ensure system stability.
* **Fix**: Wait for existing broadcasts to complete or optimize the broadcast content.

**4. How do I secure sensitive data?**

* **Best Practices**:
  * Encrypt data before storage.
  * Restrict access to commands handling sensitive data.


<!-- Source: https://help.telebotcreator.com/frequently-asked-questions-faqs.md -->

# Frequently Asked Questions (FAQs)

#### **10. Frequently Asked Questions (FAQs)**

This section addresses common questions and concerns about using Telebot Creator. Whether you're a beginner or an experienced user, these FAQs provide quick answers to help you use the platform effectively.

***

### **10.1 General Questions**

#### **1. What is Telebot Creator, and how does it work?**

Telebot Creator is a platform for building and hosting Telegram bots. It uses a custom programming language called TPY (Telebot Python) to simplify bot creation, allowing you to add commands, integrate libraries, and host bots without managing your own servers.

#### **2. How do I create my first bot?**

To create your first bot:

1. Get a Bot API token from @BotFather on Telegram.
2. Log in to Telebot Creator.
3. Click **"Add New Bot"** on the dashboard and paste the API token.
4. Start adding commands and customizing your bot.

#### **3. What are the limitations of the free plan?**

The free plan includes:

* 100,000 points per month for bot operations.
* Each command execution costs 1 point.
* A maximum of 2 simultaneous broadcasts per bot.

#### **4. How do I check my remaining points?**

Use the following code to display your remaining points:

```python
points = left_points
bot.sendMessage(f"You have {points} points remaining.")
```

#### **5. Will there be advertisements in my bot?**

Telebot Creator has a minimal advertising policy:

* Ads appear only 2-4 times per month as a single broadcast message.
* These are non-intrusive and won't spam your users.
* The platform prioritizes user experience by keeping advertisements to an absolute minimum.

#### **6. How can I get more points if I run out?**

You can obtain more points in several ways:

* Request additional points for free by asking admins in the TBC Help Group.
* In upcoming updates, a points faucet will allow you to obtain unlimited points.
* All additional points are provided completely free of charge.

#### **7. What is the upcoming Bot Store?**

The Bot Store is a new feature coming in the next update that will allow users to:

* Discover pre-made bots for various purposes.
* Share their own bot templates with the community.
* Deploy ready-to-use bots without having to code them from scratch.
* Access specialized bot templates for different industries and use cases.

***

### **10.2 Commands and Features**

#### **1. How do I create a command?**

Commands are added via the "Commands" menu in the bot dashboard. For example, to create a `/start` command:

1. Open the **Commands** menu.
2. Click **"Add Command"**.
3.  Define the command name (`/start`) and write its logic in TPY:

    ```python
    bot.sendMessage("Welcome to the bot!")
    ```

#### **2. What is the difference between `handleNextCommand` and `runCommand`?**

*   **`handleNextCommand`**: Waits for the user's next message and then routes it to a specific command.

    ```python
    bot.sendMessage("What's your name?")
    Bot.handleNextCommand("save_name")
    ```
*   **`runCommand`**: Executes another command immediately.

    ```python
    bot.sendMessage("Redirecting to the help menu...")
    Bot.runCommand("help")
    ```

#### **3. Can I execute a command for another bot?**

Yes, you can use the `bot_id` and `api_key` parameters with certain functions like `libs.Webhook.getUrlFor` to execute commands for another bot.

***

### **10.3 Libraries and Integrations**

#### **1. How do I integrate payments using Coinbase?**

Set up the Coinbase library:

```python
libs.Coinbase.setKeys("API_KEY", "SECRET")
client = libs.Coinbase.post()
```

Create a payment request:

```python
payment = client.createCharge({
    "name": "Subscription",
    "description": "Monthly fee",
    "local_price": {"amount": "10.00", "currency": "USD"},
    "pricing_type": "fixed_price"
})
bot.sendMessage(f"Pay here: {payment['hosted_url']}")
```

#### **2. Can I use multiple libraries in a single bot?**

Yes, multiple libraries can be combined seamlessly. For example, you can use `libs.CSV` for data storage and `libs.Webhook` for real-time updates in the same bot.

#### **3. How do I fetch external data using `libs.customHTTP`?**

Use the `get` method to fetch data:

```python
http_client = libs.customHTTP()
response = http_client.get("https://api.example.com/data")
bot.sendMessage(f"API Response: {response.json()}")
http_client.close()
```

***

### **10.4 Broadcasting**

#### **1. Why is my broadcast not working?**

Common reasons:

1. You've exceeded the maximum of 2 running broadcasts per bot.
2. The `function` or `command` used in the broadcast is invalid.

#### **2. What are the limits for broadcasting?**

* **User Limit**: 2 simultaneous broadcasts per bot.
* **Global Limit**: 1000 simultaneous broadcasts across all bots.

#### **3. How do I test a broadcast before sending it?**

Use the `broadcast` function with a test run:

```python
Bot.broadcast(
    function="send_message",
    text="Testing broadcast system."
)
```

***

### **10.5 Webhooks**

#### **1. What is a webhook, and how does it work in Telebot Creator?**

A webhook is a URL that allows your bot to receive real-time updates from external systems or trigger commands dynamically. Use `libs.Webhook.getUrlFor` to generate webhook URLs.

#### **2. How do I generate a webhook URL?**

```python
webhook_url = libs.Webhook.getUrlFor(
    command="process_data",
    user_id=12345
)
bot.sendMessage(f"Webhook URL: {webhook_url}")
```

#### **3. How do I secure my webhook endpoints?**

* Use dynamically generated webhook URLs.
* Validate requests by checking headers or access tokens.

***

### **10.6 Bot Transfer and Management**

#### **1. How do I transfer a bot to another account?**

Use the `Bot.Transfer` function:

```python
result = Bot.Transfer(
    email="newowner@example.com",
    bot_id="123456",
    bot_token="BOT_API_TOKEN",
    run_now=True
)
bot.sendMessage(f"Bot transferred successfully: {result['bot_id']}")
```

#### **2. What happens to my points after transferring a bot?**

Points remain with the original account. The new owner will need points in their account to run the transferred bot.

#### **3. Can I retrieve a transferred bot?**

No, once a bot is transferred, it cannot be retrieved unless the new owner transfers it back.

***

### **10.7 Payment and Points**

#### **1. How do I purchase more points?**

Points are completely free. You can request additional points by:

* Asking admins in the TBC Help Group.
* In future updates, using the points faucet to obtain unlimited points.

#### **2. How are points deducted for bot actions?**

Each command execution costs 1 point. Broadcasts and API integrations may consume additional points based on usage.

#### **3. What happens if I run out of points?**

Your bot will stop functioning until points are replenished. You can easily request more points from the TBC Help Group admins at any time, free of charge.

#### **4. How many points do new accounts receive?**

New accounts automatically receive 100,000 points upon creation, enough to execute 100,000 commands.

#### **5. Is there a limit to how many points I can request?**

No, you can request as many points as you need to run your bots. The platform is designed to be generous with points to ensure you can operate your bots without restrictions.

***

### **10.8 Troubleshooting**

#### **1. Why is my bot not responding?**

* **Cause**: Command not defined, or bot is not running or maybe the server is down.
* **Solution**: Check the command list in the dashboard and start the bot if it's stopped.

#### **2. What should I do if my webhook fails?**

* **Cause**: Invalid webhook URL or unreachable endpoint.
* **Solution**: Regenerate the webhook URL using `libs.Webhook.getUrlFor` and verify the endpoint.

#### **3. How do I debug errors in my bot's commands?**

Use try-except blocks to catch and log errors:

```python
try:
    bot.sendMessage("Testing risky operation...")
except Exception as e:
    bot.sendMessage(f"Error: {e}")
```

***


<!-- Source: https://help.telebotcreator.com/glossary-and-key-concepts.md -->

# Glossary and Key Concepts

#### **11. Glossary and Key Concepts**

This section provides definitions and explanations of key terms and concepts in Telebot Creator. Understanding these terms is crucial for effectively building and managing bots on the platform.

***

### **11.1 Introduction**

The Telebot Creator platform uses a variety of specialized terms and concepts to define its functionality. This glossary serves as a quick reference for users, ensuring they have a clear understanding of the platform's core elements and advanced features.

***

### **11.2 Key Terms**

#### **1. Bot API Token**

* **Definition**: A unique token provided by Telegram for authenticating and managing a bot. This token is required to link your bot with Telebot Creator.
* **Where to Get It**: Use @BotFather on Telegram to create a new bot and retrieve its token.

***

#### **2. TPY (Telebot Python)**

* **Definition**: A customized version of Python designed specifically for Telebot Creator. TPY simplifies bot development by offering built-in libraries, pre-defined variables, and a restricted, secure environment.
*   **Example**:

    ```python
    bot.sendMessage("Welcome to my bot!")
    ```

***

#### **3. Commands**

* **Definition**: Triggers in a bot that execute specific logic when a user sends a corresponding message. Commands typically start with a `/` (e.g., `/start`, `/help`).
*   **Example**:

    ```python
    def start_command():
        bot.sendMessage("Hello! This is the start command.")
    ```

***

#### **4. Points**

* **Definition**: The internal currency of Telebot Creator used to execute bot operations. Each command execution costs 1 point.
* **Monthly Allocation**: Users receive 100,000 points per month for free.
*   **Usage**:

    ```python
    points = left_points
    bot.sendMessage(f"You have {points} points remaining.")
    ```

***

#### **5. Broadcast**

* **Definition**: A feature that sends messages or executes commands across multiple users simultaneously.
*   **Example**:

    ```python
    Bot.broadcast(
        function="send_message",
        text="Hello, everyone!"
    )
    ```

***

#### **6. Webhook**

* **Definition**: A URL that allows bots to receive real-time updates from external systems or trigger commands dynamically.
*   **Example**:

    ```python
    webhook_url = libs.Webhook.getUrlFor(
        command="process_data",
        user_id=12345
    )
    bot.sendMessage(f"Webhook URL: {webhook_url}")
    ```

***

#### **7. Transfer**

* **Definition**: The process of transferring ownership of a bot from one Telebot Creator account to another.
*   **Example**:

    ```python
    result = Bot.Transfer(
        email="newowner@example.com",
        bot_id="123456",
        bot_token="API_TOKEN",
        run_now=True
    )
    bot.sendMessage(f"Bot successfully transferred to {result['bot_id']}.")
    ```

***

### **11.3 Libraries and Integrations**

#### **1. libs.CSV**

* **Definition**: A library for managing CSV files. Useful for storing and retrieving structured data like leaderboards or survey responses.
*   **Example**:

    ```python
    csv_handler = libs.CSV.CSVHandler("data.csv")
    csv_handler.create_csv(["Name", "Points"])
    csv_handler.add_row({"Name": "Alice", "Points": 100})
    ```

***

#### **2. libs.Coinbase**

* **Definition**: A library for handling cryptocurrency payments using Coinbase.
*   **Example**:

    ```python
    libs.Coinbase.setKeys("API_KEY", "SECRET")
    client = libs.Coinbase.post()
    payment = client.createCharge({
        "name": "Subscription",
        "description": "Monthly fee",
        "local_price": {"amount": "10.00", "currency": "USD"},
        "pricing_type": "fixed_price"
    })
    bot.sendMessage(f"Pay here: {payment['hosted_url']}")
    ```

***

#### **3. libs.Webhook**

* **Definition**: A library for generating and managing webhook URLs.
*   **Example**:

    ```python
    webhook_url = libs.Webhook.getUrlFor(
        command="update_status",
        user_id=67890
    )
    bot.sendMessage(f"Webhook URL: {webhook_url}")
    ```

***

#### **4. libs.Polygon**

* **Definition**: A library for managing cryptocurrency transactions on the Polygon network.
*   **Example**:

    ```python
    libs.Polygon.setKeys("PRIVATE_KEY")
    libs.Polygon.send(
        value=5,
        to="0xRecipientAddress",
        contract="TokenContractAddress"
    )
    ```

***

### **11.4 Advanced Concepts**

#### **1. Multi-Step Workflows**

* **Definition**: A sequence of commands executed step-by-step based on user input.
*   **Example**:

    ```python
    bot.sendMessage("What’s your name?")
    Bot.handleNextCommand("save_name")
    ```

***

#### **2. Callback URLs**

* **Definition**: URLs used in broadcasts and webhooks to receive execution feedback or trigger additional processes.
*   **Example**:

    ```python
    Bot.broadcast(
        function="send_message",
        text="Thank you for subscribing!",
        callback_url="https://example.com/callback"
    )
    ```

***

#### **3. Sandbox Environment**

* **Definition**: A secure environment where bot commands are executed to prevent unauthorized actions or access.

***

#### **4. Global Broadcast Limits**

* **Definition**: A system-wide limit of 1000 simultaneous broadcasts across all bots to ensure server stability.

***

### **11.5 Usage Examples**

#### **Broadcast Syntax**

```python
Bot.broadcast(
    function="send_message",
    text="Hello, everyone!"
)
```

#### **Webhook Generation**

```python
webhook_url = libs.Webhook.getUrlFor(
    command="process_data",
    user_id=12345
)
bot.sendMessage(f"Webhook URL: {webhook_url}")
```

#### **Dynamic Data Fetching**

```python
http_client = libs.customHTTP()
response = http_client.get("https://api.example.com/data")
bot.sendMessage(f"API Response: {response.json()}")
http_client.close()
```

***

####


<!-- Source: https://help.telebotcreator.com/broadcast-function-in-tbc.md -->

# Broadcast Function In TBC

#### **Broadcast Function Documentation**

The `broadcast` function in Telebot Creator allows you to send messages or execute commands for multiple users efficiently. It supports both direct messaging with pre-defined functions and executing custom code for dynamic broadcasts.

***

#### **Function Syntax**

```python
Bot.broadcast(
    code=None, 
    command=None, 
    callback_url=None, 
    bot_id=None, 
    api_key=None, 
    function=None, 
    warnings=None, 
    **kwargs
)
```

***

#### **Parameters**

1. **`code`** (_Optional_):
   * Custom TPY code to execute for the broadcast.
   * Example: A piece of code that sends personalized messages.
2. **`command`** (_Optional_):
   * The name of a pre-defined command in the bot to execute during the broadcast.
   * If `code` is not provided, `command` must be specified.
3. **`callback_url`** (_Optional_):
   * URL to be called after the broadcast task is executed for each user.
4. **`bot_id`** (_Optional_):
   * The ID of the bot for which the broadcast is being created.
   * **Requires** `api_key` for validation if specified.
5. **`api_key`** (_Optional_):
   * API key of the bot owner. Used to validate access when `bot_id` is provided.
6. **`function`** (_Optional_):
   * Pre-defined Telegram functions for broadcasting (e.g., `send_message`, `send_photo`).
   * Full list of allowed functions:
     * `send_message`, `send_photo`, `send_video`, `send_animation`
     * `send_audio`, `send_document`, `forward_message`
     * `send_sticker`, `send_poll`, `send_location`, etc.
7. **`warnings`** (_Optional_):
   * Whether to display warnings during test execution (`True` by default).
8. **`**kwargs`** (_Optional_):
   * Additional arguments for the selected `function`.

***

#### **Validation and Limitations**

* **Maximum Global Broadcasts**: 1000 simultaneous broadcasts across all bots.
* **User Broadcast Limit**: 2 running broadcasts per bot.
* **Command Validation**: The `command` provided must exist in the bot.
* **Function Restrictions**: Only allowed functions can be used for broadcasting.

If these limits are exceeded, the function returns an error message.

***

#### **Usage Examples**

**1. Broadcasting a Message**

Broadcast a message to all users using the `send_message` function:

```python
Bot.broadcast(
    function="send_message",
    text="Hello, everyone! Check out our new feature!"
)
```

**2. Broadcasting a Command**

Execute a pre-defined command across all users:

```python
Bot.broadcast(
    command="promo_offer"
)
```

**3. Broadcasting with Custom Code**

Use TPY code for a dynamic broadcast:

```python
Bot.broadcast(
    code="""
    first_name = message.from_user.first_name
    bot.sendMessage(f"Hello {first_name}, don’t miss our latest update!")
    """
)
```

**4. Broadcasting for Another Bot**

Broadcast messages for a different bot by providing `bot_id` and `api_key`:

```python
Bot.broadcast(
    bot_id="another_bot_id",
    api_key="another_bot_api_key",
    function="send_message",
    text="Greetings from Bot B!"
)
```

**5. Broadcasting with a Callback URL**

Trigger a callback URL after the broadcast execution:

```python
Bot.broadcast(
    function="send_message",
    text="Hello! Thank you for being with us.",
    callback_url="https://example.com/broadcast-callback"
)
```

***

#### **Error Handling**

**Common Errors**

1. **Exceeding Limits**:
   * Error: "You already have 2 running broadcasts."
   * Solution: Wait for an existing broadcast to complete or stop it manually.
2. **Invalid Command**:
   * Error: "Command doesn’t exist."
   * Solution: Ensure the `command` specified is defined in your bot.
3. **Invalid Function**:
   * Error: "Function `<name>` not allowed for broadcasting."
   * Solution: Use only allowed functions for the broadcast.
4. **API Key Validation**:
   * Error: "API key not valid."
   * Solution: Verify the `bot_id` and `api_key` combination.

***

#### **Best Practices**

1. **Efficient Broadcasting**:
   * Use pre-defined commands or reusable functions to minimize errors.
   * Avoid overloading the system with frequent or unnecessary broadcasts.
2. **Test Before Deployment**:
   * Use the test run feature built into the `broadcast` function to validate your setup before executing the full broadcast.
3. **Secure API Keys**:
   * Never expose `api_key` in public code or logs.
4. **Monitor Broadcast Status**:
   * Use the `broadstatus` collection to track running broadcasts and their success rate.

***

This documentation provides a comprehensive guide to using the `broadcast` function for efficient and scalable messaging in Telebot Creator.


<!-- Source: https://help.telebotcreator.com/coinbase-library-tbc.md -->

# Coinbase Library TBC

#### **12. Coinbase Library (libs.Coinbase)**

The `libs.Coinbase` library in Telebot Creator integrates seamlessly with the Coinbase API, enabling bots to handle cryptocurrency payments, create addresses, manage transactions, and automate deposit notifications through webhooks.

***

### **12.1 Overview**

The Coinbase integration allows you to:

1. Generate cryptocurrency deposit addresses.
2. Process payments and transactions.
3. Use webhooks to receive real-time updates for deposits.
4. Automate payment responses in your bot.

***

### **12.2 Setting Up Coinbase**

#### **Step 1: Create API Keys in Coinbase**

1. Log in to your Coinbase Commerce account.
2. Go to **Settings > API Keys**.
3. Click **Create an API Key**.
4. Copy the generated API key and save it securely. You’ll need it to configure `libs.Coinbase` in your bot.

***

#### **Step 2: Configure the Coinbase Library**

Set the API keys in your bot using the `libs.Coinbase.setKeys` function:

```python
libs.Coinbase.setKeys("YOUR_API_KEY", "YOUR_API_SECRET")
```

Create a client instance for making API calls:

```python
client = libs.Coinbase.post()
```

***

### **12.3 Creating Cryptocurrency Deposit Addresses**

Generate a unique cryptocurrency address for a user:

```python
address = client.createAddress("BTC")
bot.sendMessage(f"Your Bitcoin deposit address: {address['address']}")
```

**Example: Generating an Ethereum Address**

```python
eth_address = client.createAddress("ETH")
bot.sendMessage(f"Your Ethereum deposit address: {eth_address['address']}")
```

***

### **12.4 Creating a Webhook URL for Deposit Notifications**

#### **Step 1: Generate a Webhook URL**

Use `libs.Webhook.getUrlFor` to create a webhook URL for the `/get_coinbase_updates` command:

```python
webhook_url = libs.Webhook.getUrlFor(
    command="/get_coinbase_updates",
    user_id=12345
)
bot.sendMessage(f"Webhook URL: {webhook_url}")
```

#### **Step 2: Set IPN URL in Coinbase**

1. Log in to Coinbase Commerce.
2. Navigate to **Settings > Notifications**.
3. Paste the webhook URL you generated into the **Webhook URL** field.
4. Click **Save**.

***

### **12.5 Handling Deposit Notifications**

In the `/get_coinbase_updates` command, handle incoming webhook notifications:

```python
# Example command logic for handling Coinbase IPN responses
status = options.json.get("event", {}).get("type", "")
if status == "charge:confirmed":
    bot.sendMessage("Deposit confirmed!")
elif status == "charge:pending":
    bot.sendMessage("Deposit is pending. Waiting for confirmation.")
else:
    bot.sendMessage("Deposit failed or was canceled.")
```

***

### **12.6 Performing Transactions**

#### **Send Cryptocurrency**

Send cryptocurrency to a specific address using `libs.Coinbase`:

```python
transaction = client.sendTransaction({
    "to": "recipient_wallet_address",
    "currency": "BTC",
    "amount": "0.01"
})
bot.sendMessage(f"Transaction initiated! Transaction ID: {transaction['id']}")
```

***

### **12.7 Basic Coinbase Functions**

#### **1. Fetch Payment Status**

Retrieve the status of a payment:

```python
charge_id = "YOUR_CHARGE_ID"
status = client.retrieveCharge(charge_id)["status"]
bot.sendMessage(f"Payment status: {status}")
```

***

#### **2. Fetch Account Balances**

Retrieve your Coinbase wallet balances:

```python
balances = client.getBalance()
bot.sendMessage(f"Your balances: {balances}")
```

***

#### **3. Create a Charge**

Request a payment from a user:

```python
payment = client.createCharge({
    "name": "Subscription Payment",
    "description": "Monthly subscription fee",
    "local_price": {"amount": "10.00", "currency": "USD"},
    "pricing_type": "fixed_price"
})
bot.sendMessage(f"Please complete your payment here: {payment['hosted_url']}")
```

***

#### **4. Verify API Keys**

Check if your API keys are valid:

```python
try:
    client = libs.Coinbase.post()
    bot.sendMessage("API keys are valid!")
except Exception as e:
    bot.sendMessage(f"Invalid API keys: {e}")
```

***

#### **5. Handling Refunds**

Issue refunds directly from the bot:

```python
refund = client.refundCharge("CHARGE_ID")
bot.sendMessage(f"Refund issued: {refund}")
```

***

### **12.8 Summary**

The `libs.Coinbase` library provides all the tools you need to manage cryptocurrency transactions, automate deposit notifications, and handle payments efficiently. By combining this library with webhooks and commands, you can create powerful bots that support seamless crypto integration.


<!-- Source: https://help.telebotcreator.com/ton-library-documentation.md -->

# TON Library Documentation

## Introduction

The TON Library (TonLib) is a powerful addition to TeleBot Creator that enables seamless integration with The Open Network blockchain. With TonLib, you can create wallets, check balances, send TON, work with jettons (TON's tokens), and integrate TON Connect for user wallet connections.

> **Note:** This is a development version of the TON Library introduced in version 4.9.0. Most bugs have been fixed and the library is stable for production use.

## Getting Started

Unlike other libraries, TonLib doesn't require an import statement. It's globally available in your bot code.

```python
# ❌ Don't use imports
# import TonLib  # This will cause an error

# ✅ Instead, use the library directly
wallet = libs.TonLib.generateWallet()
```

## Core Functions

### Wallet Management

#### generateWallet()

Creates a new TON wallet and returns its address and mnemonic phrase.

```python
result = libs.TonLib.generateWallet()
address = result["address"]
mnemonics = result["mnemonics"]
```

#### setKeys(mnemonics)

Stores a mnemonic phrase for later use.

```python
libs.TonLib.setKeys("word1 word2 ... word24")
```

#### getWalletAddress(mnemonics=None)

Retrieves the wallet address from a mnemonic phrase or from stored keys.

```python
# Using stored keys
address = libs.TonLib.getWalletAddress()

# Or with specific mnemonics
address = libs.TonLib.getWalletAddress("word1 word2 ... word24")
```

### TON Operations

#### getBalance(address, api\_key=None, endpoint=None)

Checks the TON balance of an address.

```python
balance = libs.TonLib.getBalance("EQD...")
```

#### sendTON(to\_address, amount, comment=None, mnemonics=None, api\_key=None, endpoint=None, is\_testnet=False)

Sends TON to another address.

```python
result = libs.TonLib.sendTON(
    to_address="EQD...",
    amount=0.1,  # In TON
    comment="Payment for service"
)
```

#### checkTONTransaction(address, api\_key=None, endpoint=None, limit=10)

Gets the recent transactions for an address.

```python
transactions = libs.TonLib.checkTONTransaction("EQD...")
for tx in transactions:
    if tx["type"] == "incoming":
        from_address = tx["from"]
        amount = tx["amount"]
        # Process the incoming transaction...
```

### TON Connect Integration

#### create\_ton\_connect\_session(user\_id, expiry\_seconds=86400)

Creates a TON Connect session for wallet connection.

```python
session = libs.TonLib.create_ton_connect_session(user_id="12345")
connect_url = session["connect_url"]
# Send this URL to the user for connection
```

#### verify\_ton\_connect\_session(session\_id)

Checks if a wallet has connected to the session.

```python
status = libs.TonLib.verify_ton_connect_session(session_id)
if status["status"] == "connected":
    wallet_address = status["wallet_address"]
    # User wallet is connected
```

#### request\_ton\_transaction(to\_address, amount, comment=None, callback\_url="", return\_url=None)

Requests a TON transfer from a connected wallet.

```python
request = libs.TonLib.request_ton_transaction(
    to_address="EQD...",
    amount=1.5,
    comment="Donation",
    callback_url="https://your-app.com/callback"
)
# Send the request["connect_url"] to the user
```

### Jetton Operations

#### get\_jetton\_metadata(jetton\_master\_address, api\_key=None, endpoint=None)

Retrieves information about a Jetton (token).

```python
metadata = libs.TonLib.get_jetton_metadata("EQD...")
name = metadata["name"]
symbol = metadata["symbol"]
total_supply = metadata["total_supply"]
```

#### get\_jetton\_balance(owner\_address, jetton\_master\_address, api\_key=None, endpoint=None)

Checks the Jetton balance of an address.

```python
balance = libs.TonLib.get_jetton_balance(
    owner_address="EQD...",
    jetton_master_address="EQD..."
)
```

#### request\_jetton\_transfer(to\_address, jetton\_master\_address, amount, comment=None, callback\_url="", return\_url=None)

Requests a Jetton transfer from a connected wallet.

```python
request = libs.TonLib.request_jetton_transfer(
    to_address="EQD...",
    jetton_master_address="EQD...",
    amount=10,
    callback_url="https://your-app.com/callback"
)
```

## Examples

### Creating a Simple TON Wallet Bot

```python
def handle_start(message):
    # Generate a new wallet
    wallet = libs.TonLib.generateWallet()
    
    # Store the mnemonics
    libs.TonLib.setKeys(wallet["mnemonics"])
    
    # Send information to the user
    bot.send_message(
        chat_id=message.chat.id,
        text=f"Your new TON wallet address:\n`{wallet['address']}`\n\n"
             f"Seed phrase (keep it safe):\n`{wallet['mnemonics']}`",
        parse_mode="Markdown"
    )

def handle_balance(message):
    # Get wallet address
    address = libs.TonLib.getWalletAddress()
    
    # Get balance
    balance = libs.TonLib.getBalance(address)
    
    # Send balance to user
    bot.send_message(
        chat_id=message.chat.id,
        text=f"Your balance: {balance} TON"
    )
```

### TON Connect Integration Example

```python
# Step 1: Initialize wallet connection
def handle_connect_wallet(message):
    user_id = str(message.from_user.id)
    session = libs.TonLib.create_ton_connect_session(user_id)
    
    # Store session_id for later verification
    db.set_user_data(user_id, "ton_session_id", session["session_id"])
    
    # Send connection link to user
    bot.send_message(
        chat_id=message.chat.id,
        text=f"Connect your TON wallet by opening this link:\n{session['connect_url']}"
    )

# Step 2: Check wallet connection status
def handle_check_connection(message):
    user_id = str(message.from_user.id)
    session_id = db.get_user_data(user_id, "ton_session_id")
    
    if not session_id:
        return bot.send_message(message.chat.id, "You haven't started a connection yet")
    
    status = libs.TonLib.verify_ton_connect_session(session_id)
    
    if status["status"] == "connected":
        bot.send_message(
            chat_id=message.chat.id,
            text=f"Wallet connected: {status['wallet_address']}"
        )
    else:
        bot.send_message(
            chat_id=message.chat.id,
            text="Wallet not connected yet. Try again later."
        )
```

## Best Practices

1. **Security**: Never store sensitive mnemonic phrases in plain text. Consider encrypting them or using a secure key management solution.
2. **Error Handling**: Always wrap TON operations in try/except blocks to handle potential errors gracefully.
3. **Testnet First**: When developing, use the testnet (is\_testnet=True) before moving to mainnet.
4. **Rate Limiting**: Be mindful of API request limits when checking balances or transactions frequently.
5. **User Experience**: Provide clear instructions and feedback to users, especially for wallet connection steps.

## Limitations

* Maximum code execution time is 120 seconds
* `time.sleep()` function is limited to 10 seconds maximum

## Further Resources

* [The Open Network Documentation](https://ton.org/docs)
* [TON Connect Documentation](https://docs.ton.org/develop/dapps/ton-connect/overview)
* [TBC Libraries Documentation](tbc-libraries-libs)


<!-- Source: https://help.telebotcreator.com/version-4.7.0-update.md -->

# Version 4.7.0 Update

## New Features Overview

The version 4.7.0 update introduces several powerful features to enhance your bot development experience:

1. **New User and Bot Class Methods**: Additional methods for data file handling and user information.
2. **New AI Integration Libraries**: OpenAI and Gemini AI libraries for advanced AI capabilities.
3. **Enhanced Resource Management**: New functions in the Resources library.

## New User.x Class Methods

The following methods have been added to the `User.x` class for better data handling:

### getDataFile

Retrieves stored user data as a file, which can be sent to users directly.

```
User.getDataFile(name, user=None, output_format="txt")
```

**Parameters:**

* `name` (Required): The name of the data to retrieve.
* `user` (Optional): The user ID to get data for. Defaults to current user if not specified.
* `output_format` (Optional): Format of the output file (currently supports "txt").

**Example:**

```
file = User.getDataFile("profile")
bot.sendDocument(file)
```

### getAllData

Retrieves all data entries that match a specific name pattern and returns them as a JSON file.

```
User.getAllData(name, output_format="json")
```

**Parameters:**

* `name` (Required): The name pattern to search for.
* `output_format` (Optional): Format of the output file (currently supports "json").

**Example:**

```
data_file = User.getAllData("settings")
bot.sendDocument(data_file)
```

### getAllDataOfUser

Retrieves all data associated with a specific user.

```
User.getAllDataOfUser(user, output_format="json")
```

**Parameters:**

* `user` (Required): The user ID to get all data for.
* `output_format` (Optional): Format of the output file (currently supports "json").

**Example:**

```
user_data = User.getAllDataOfUser("12345678")
bot.sendDocument(user_data)
```

## New Bot.x Class Methods

The following methods have been added to the `Bot.x` class for better global data handling:

### getDataFile

Retrieves stored global data as a file.

```
Bot.getDataFile(name, output_format="txt")
```

**Parameters:**

* `name` (Required): The name of the global data to retrieve.
* `output_format` (Optional): Format of the output file (currently supports "txt").

**Example:**

```
config_file = Bot.getDataFile("config")
bot.sendDocument(config_file)
```

### getAllData

Retrieves all global data entries that match a specific name pattern.

**Note:** This method only works with data saved after the 4.7.0 update. It cannot access older data.

```
Bot.getAllData(name, output_format="json")
```

**Parameters:**

* `name` (Required): The name of the global data to retrieve.
* `output_format` (Optional): Format of the output file (currently supports "json").

**Example:**

```
all_configs = Bot.getAllData("config")
bot.sendDocument(all_configs)
```

### getBotUsersFile

Retrieves information about all users of the bot in either CSV or JSON format.

```
Bot.getBotUsersFile(output_format="json", include_creation_date=False, include_last_active_date=False)
```

**Parameters:**

* `output_format` (Optional): Format of the output file ("json" or "csv").
* `include_creation_date` (Optional): Whether to include user creation date in the output.
* `include_last_active_date` (Optional): Whether to include the user's last active date.

**Example:**

```
users_file = Bot.getBotUsersFile(output_format="csv", include_creation_date=True)
bot.sendDocument(users_file)
```

## New AI Libraries

### libs.openai\_lib

Integrates OpenAI's API for powerful AI capabilities. Supports chat completions and the OpenAI Assistants API.

#### Key Classes:

1. **OpenAIClient**: Core client for interacting with OpenAI API.
2. **AIAssistant**: High-level wrapper for working with OpenAI Assistants.

**Example - Chat Completion:**

```
client = libs.openai_lib.OpenAIClient(api_key="YOUR_API_KEY")
response = client.create_chat_completion(
    model="gpt-4o",
    messages=[
        {"role": "system", "content": "You are a helpful assistant."},
        {"role": "user", "content": "Tell me about Telegram bots."}
    ]
)
bot.sendMessage(response["choices"][0]["message"]["content"])
```

**Example - Assistant:**

```
client = libs.openai_lib.OpenAIClient(api_key="YOUR_API_KEY")
assistant = libs.openai_lib.AIAssistant(
    openai_client=client,
    create_new=True,
    name="Customer Support Bot",
    instructions="You are a helpful customer support assistant.",
    model="gpt-4o"
)

thread_id = assistant.start_conversation()
response = assistant.send_message("How do I reset my password?")
bot.sendMessage(response["content"])
```

### libs.gemini\_lib

Integrates Google's Gemini AI models using an OpenAI-compatible API interface.

#### Key Classes:

1. **GeminiClient**: Core client for interacting with Gemini API.
2. **GeminiAIAssistant**: High-level wrapper for working with Gemini in an assistant-like way.

**Example - Chat Completion:**

```
client = libs.gemini_lib.GeminiClient(api_key="YOUR_API_KEY")
response = client.create_chat_completion(
    model="gemini-2.0-flash",
    messages=[
        {"role": "user", "content": "What are the best practices for Telegram bot development?"}
    ]
)
bot.sendMessage(response["choices"][0]["message"]["content"])
```

**Example - Assistant:**

```
client = libs.gemini_lib.GeminiClient(api_key="YOUR_API_KEY")
assistant = libs.gemini_lib.GeminiAIAssistant(
    gemini_client=client,
    create_new=True,
    name="Product Advisor",
    instructions="You are a helpful product recommendation assistant.",
    model="gemini-2.0-flash"
)

thread_id = assistant.start_conversation()
response = assistant.send_message("I need a new laptop for video editing.")
bot.sendMessage(response["content"])
```

## Enhanced Resource Management

The 4.7.0 update adds significant improvements to the `libs.Resources` library with new administrative capabilities:

### New adminRes Class

A new `adminRes` class has been added to provide administrative control over resources:

```
admin = libs.Resources.adminRes(name, user=None)
```

**Parameters:**

* `name` (Required): The name of the resource to manage.
* `user` (Optional): User ID to scope the admin operations.

### New Administrative Methods

The following methods are available with the adminRes class:

#### clearAllData

Clears all resource data, optionally for a specific user.

```
admin.clearAllData(user=None)
```

**Example:**

```
admin = libs.Resources.adminRes("points")
admin.clearAllData("12345678")  # Clear for specific user
admin.clearAllData()  # Clear for all users
```

#### fetchAllResourcesOfUser

Retrieves all resources for a specific user as a file (JSON or CSV).

```
admin.fetchAllResourcesOfUser(user, output_format)
```

**Parameters:**

* `user` (Required): User ID to get resources for.
* `output_format` (Required): Format of the output file ("json" or "csv").

**Example:**

```
resources_file = admin.fetchAllResourcesOfUser("12345678", "json")
bot.sendDocument(resources_file)
```

#### removeDataOfUser

Removes specific resource data for a user.

```
admin.removeDataOfUser(user)
```

**Example:**

```
admin = libs.Resources.adminRes("points")
admin.removeDataOfUser("12345678")
```

#### removeAllDataOfUser

Removes all resource data for a user.

```
admin.removeAllDataOfUser(user)
```

**Example:**

```
admin = libs.Resources.adminRes("points")
admin.removeAllDataOfUser("12345678")
```

#### removeAllData

Removes all resource data for the bot.

```
admin.removeAllData()
```

**Example:**

```
admin = libs.Resources.adminRes("points")
admin.removeAllData()
```

## Summary

Version 4.7.0 dramatically expands the capabilities of Telebot Creator with:

1. **New Data Management Functions**: Added `getDataFile`, `getAllData`, and `getAllDataOfUser` to the User.x class and `getDataFile`, `getAllData`, and `getBotUsersFile` to the Bot.x class, making it easier to work with data and export it in different formats.
2. **Powerful AI Integration**: Introduced OpenAI and Gemini libraries for advanced AI capabilities, allowing bots to leverage state-of-the-art language models through simple interfaces.
3. **Enhanced Resource Management**: Added the new `adminRes` class to libs.Resources with administrative methods like `clearAllData`, `fetchAllResourcesOfUser`, `removeDataOfUser`, `removeAllDataOfUser`, and `removeAllData` for better control over resources.

These additions make it easier to build sophisticated bots with advanced data handling, resource management, and AI capabilities.

Remember that the new `Bot.getAllData()` method only works with data saved after this update, as it requires a specific data structure not present in older versions.


<!-- Source: https://help.telebotcreator.com/version-4.8.0-update.md -->

# Version 4.8.0 Update

## New Features Overview

The version 4.8.0 update introduces several powerful enhancements to improve your bot development experience:

1. **New Account Class**: Direct access to account-level operations through the globally accessible `Account` variable.
2. **Enhanced Resource Management**: New `accountRes` class for managing account-level resources.
3. **Improved Server Stability**: Enhanced server maintenance and durability.
4. **Command Aliases**: Support for command aliases in the upcoming UI update.
5. **Bot Recovery System**: Ability to recover deleted bots within 90 days.
6. **Coming Soon - Bot Store**: A marketplace for discovering, sharing, and deploying pre-made bots.
7. **Coming Soon - Points Faucet**: System to obtain unlimited points for running your bots.

## Advertising and Points System

### Points System Enhancements

Telebot Creator continues to offer one of the most generous free bot hosting solutions available:

* **Initial Allocation**: New accounts receive **100,000 points** upon creation.
* **Command Cost**: Each command execution costs just **1 point**.
* **Free Additional Points**: Users can request additional points at any time by contacting admins in the TBC Help Group.
* **Upcoming Points Faucet**: In the next update, a points faucet system will allow users to obtain unlimited points.

### Ad Policy Clarification

Telebot Creator maintains a minimal advertising approach to keep the platform free while ensuring a great user experience:

* **Low Frequency**: Advertisements appear only 2-4 times per month.
* **Non-Intrusive Format**: Ads are delivered as a single broadcast message, not as continuous spam.
* **User-Friendly**: This approach ensures that bot users enjoy an uninterrupted experience.

## New Account Class

The 4.8.0 update introduces the powerful `Account` class, giving developers direct access to account-level operations. This class allows for comprehensive management of bots, commands, statistics, and more from a centralized interface.

### Accessing the Account Class

The Account class is globally accessible in your bot code through the `Account` variable, similar to how you access the `Bot` and `User` classes:

```python
# The Account variable is directly available in your bot code
result = Account.get_bots_list()
if result["ok"]:
    for bot_info in result["result"]:
        Bot.sendMessage(f"Bot: {bot_info['name']}")
```

No initialization is needed as the variable is automatically created with the correct authentication and database connections.

### Account Data Management Methods

#### saveData

Stores data at the account level, accessible across all bots.

```python
Account.saveData(name, data)
```

**Parameters:**

* `name` (Required): Name identifier for the data.
* `data` (Required): The data to store (limited to 10MB).

**Example:**

```python
result = Account.saveData("global_settings", {"theme": "dark", "notifications": True})
Bot.sendMessage(f"Save result: {result['result']}")
```

**Example Output:**

```json
{
  "ok": "true",
  "result": "Added new data"
}
```

#### getData

Retrieves previously stored account data.

```python
Account.getData(name)
```

**Parameters:**

* `name` (Required): Name of the data to retrieve.

**Example:**

```python
settings = Account.getData("global_settings")
if settings:
    Bot.sendMessage(f"Theme: {settings['theme']}")
else:
    Bot.sendMessage("No settings found")
```

**Example Output:**

```json
{
  "theme": "dark",
  "notifications": true
}
```

#### deleteData

Deletes account data by name.

```python
Account.deleteData(name)
```

**Parameters:**

* `name` (Required): Name of the data to delete.

**Example:**

```python
result = Account.deleteData("temp_data")
Bot.sendMessage(f"Delete result: {result['result']}")
```

**Example Output:**

```json
{
  "ok": "true",
  "result": "deleted"
}
```

#### getDataFile

Returns account data as a file that can be sent to users.

```python
Account.getDataFile(name, output_format="txt")
```

**Parameters:**

* `name` (Required): Name of the data to retrieve.
* `output_format` (Optional): Format of the output file (currently supports "txt").

**Example:**

```python
try:
    file = Account.getDataFile("report_data")
    Bot.sendDocument(file)
except ValueError as e:
    Bot.sendMessage(f"Error: {str(e)}")
```

**Example Output:**

```
# Returns a file-like object that can be directly passed to Bot.sendDocument()
# The file contains the stored data in text format
```

#### getAllData

Retrieves all account data entries, optionally filtered by name pattern.

```python
Account.getAllData(name=None, output_format="json")
```

**Parameters:**

* `name` (Optional): Name pattern to filter data.
* `output_format` (Optional): Format of the output file (currently supports "json").

**Example:**

```python
data_file = Account.getAllData("config_")
Bot.sendDocument(data_file)
```

**Example Output:**

```
# Returns a file-like object containing JSON data in the format:
# [
#   {
#     "name": "config_user",
#     "data": {"setting1": "value1", "setting2": "value2"},
#     "time": "2023-05-15 14:30:22"
#   },
#   {
#     "name": "config_bot",
#     "data": {"timeout": 30, "retry": true},
#     "time": "2023-05-16 09:15:43"
#   }
# ]
```

#### deleteAllData

Deletes all account data, with optional exclusions and bot data inclusion.

```python
Account.deleteAllData(except_data=None, include_bot_data=False)
```

**Parameters:**

* `except_data` (Optional): List of data names to preserve.
* `include_bot_data` (Optional): Whether to also delete bot-level data.

**Example:**

```python
result = Account.deleteAllData(except_data=["important_settings"], include_bot_data=True)
Bot.sendMessage(f"Data cleared: {result['result']}")
```

**Example Output:**

```json
{
  "ok": "true",
  "result": "deleted"
}
```

#### info

Returns basic account information.

```python
Account.info()
```

**Example:**

```python
info = Account.info()
Bot.sendMessage(f"Account plan: {info.plan}, Points left: {info.points_left}")
```

**Example Output:**

```json
{
  "email": "user@example.com",
  "plan": "Premium",
  "points_resetAt": "2023-06-01 00:00:00",
  "points_left": 8500,
  "ep": 1000
}
```

### Bot Management Methods

#### start\_bot

Starts a bot by setting its webhook.

```python
Account.start_bot(botid)
```

**Parameters:**

* `botid` (Required): ID of the bot to start.

**Example:**

```python
result = Account.start_bot("1234567")
Bot.sendMessage(f"Start result: {result['result']}")
```

**Example Output:**

```json
{
  "ok": true,
  "result": "Bot started successfully"
}
```

#### stop\_bot

Stops a bot by removing its webhook.

```python
Account.stop_bot(botid)
```

**Parameters:**

* `botid` (Required): ID of the bot to stop.

**Example:**

```python
result = Account.stop_bot("1234567")
Bot.sendMessage(f"Stop result: {result['result']}")
```

**Example Output:**

```json
{
  "ok": true,
  "result": "Bot stopped successfully"
}
```

#### restart\_bot

Restarts a bot by stopping and then starting it.

```python
Account.restart_bot(botid)
```

**Parameters:**

* `botid` (Required): ID of the bot to restart.

**Example:**

```python
result = Account.restart_bot("1234567")
Bot.sendMessage(f"Restart result: {result['result']}")
```

**Example Output:**

```json
{
  "ok": true,
  "result": "Bot started successfully"
}
```

#### create\_bot

Creates a new bot with the given token.

```python
Account.create_bot(bot_token, bot_name=None, bot_username=None)
```

**Parameters:**

* `bot_token` (Required): Telegram bot token.
* `bot_name` (Optional): Name for the bot (retrieved from Telegram if not provided).
* `bot_username` (Optional): Username for the bot (retrieved from Telegram if not provided).

**Example:**

```python
result = Account.create_bot("123456789:ABCDEF-ghijklmnopqrstuvwxyz")
if result["ok"]:
    Bot.sendMessage(f"Created bot with ID: {result['botid']}")
else:
    Bot.sendMessage(f"Error: {result['result']}")
```

**Example Output:**

```json
{
  "ok": true,
  "result": "Bot created successfully",
  "botid": "7654321"
}
```

#### delete\_bot

Deletes a bot (temporarily or permanently).

```python
Account.delete_bot(botid, permanent=False)
```

**Parameters:**

* `botid` (Required): ID of the bot to delete.
* `permanent` (Optional): Whether to permanently delete or keep for recovery.

**Example:**

```python
result = Account.delete_bot("1234567")
Bot.sendMessage(f"Delete result: {result['result']}")
```

**Example Output:**

```json
{
  "ok": true,
  "result": "Bot deleted successfully"
}
```

#### recover\_bot

Recovers a previously deleted bot.

```python
Account.recover_bot(botid, new_token=None)
```

**Parameters:**

* `botid` (Required): ID of the bot to recover.
* `new_token` (Optional): New token if the original is no longer valid.

**Example:**

```python
result = Account.recover_bot("1234567")
Bot.sendMessage(f"Recovery result: {result['result']}")
```

**Example Output:**

```json
{
  "ok": true,
  "result": "Bot recovered successfully"
}
```

#### get\_deleted\_bots

Retrieves a list of deleted bots that can be recovered.

```python
Account.get_deleted_bots()
```

**Example:**

```python
bots = Account.get_deleted_bots()
if bots["ok"] and bots["result"]:
    for bot_info in bots["result"]:
        Bot.sendMessage(f"Bot {bot_info['name']} - Days remaining: {bot_info['days_remaining']}")
```

**Example Output:**

```json
{
  "ok": true,
  "result": [
    {
      "botid": "1234567",
      "name": "Customer Support Bot",
      "username": "customer_support_bot",
      "deleted_at": "2023-05-01T14:30:22Z",
      "commands_count": 15,
      "days_remaining": 60,
      "recoverable": true
    },
    {
      "botid": "7654321",
      "name": "Quiz Bot",
      "username": "quiz_master_bot",
      "deleted_at": "2023-04-15T09:12:45Z",
      "commands_count": 8,
      "days_remaining": 44,
      "recoverable": true
    }
  ]
}
```

#### get\_deleted\_bots\_stats

Provides statistics about deleted bots, including counts and expiration information.

```python
Account.get_deleted_bots_stats()
```

**Example:**

```python
stats = Account.get_deleted_bots_stats()
if stats["ok"]:
    result = stats["result"]
    Bot.sendMessage(f"Total deleted: {result['total']}, Recoverable: {result['recoverable']}")
```

**Example Output:**

```json
{
  "ok": true,
  "result": {
    "total": 5,
    "recoverable": 3,
    "expired": 2,
    "expiring_soon": [
      {
        "botid": "2345678",
        "name": "Test Bot",
        "days_remaining": 15
      }
    ]
  }
}
```

#### permanent\_delete\_bot

Permanently removes a deleted bot from the recovery system.

```python
Account.permanent_delete_bot(botid)
```

**Parameters:**

* `botid` (Required): ID of the deleted bot to permanently remove.

**Example:**

```python
result = Account.permanent_delete_bot("1234567")
Bot.sendMessage(f"Permanent deletion result: {result['result']}")
```

**Example Output:**

```json
{
  "ok": true,
  "result": "Bot permanently deleted"
}
```

#### clear\_expired\_bots

Admin-only method to clear expired bots (deleted over 90 days ago).

```python
Account.clear_expired_bots()
```

**Example:**

```python
result = Account.clear_expired_bots()
Bot.sendMessage(f"Cleared expired bots: {result['result']}")
```

**Example Output:**

```json
{
  "ok": true,
  "result": "Cleared 3 expired bots"
}
```

#### clone\_bot

Creates a clone of an existing bot.

```python
Account.clone_bot(botid, new_token=None)
```

**Parameters:**

* `botid` (Required): ID of the bot to clone.
* `new_token` (Optional): Token for the new bot.

**Example:**

```python
result = Account.clone_bot("1234567", "987654321:ABCDEF-ghijklmnopqrstuvwxyz")
if result["ok"]:
    Bot.sendMessage(f"Created clone with ID: {result['botid']}")
```

**Example Output:**

```json
{
  "ok": true,
  "result": "Bot cloned successfully",
  "botid": "8765432"
}
```

#### get\_bots\_list

Retrieves a list of all bots in the account.

```python
Account.get_bots_list()
```

**Example:**

```python
bots = Account.get_bots_list()
if bots["ok"] and bots["result"]:
    for bot_info in bots["result"]:
        Bot.sendMessage(f"Bot {bot_info['name']} - Status: {bot_info['status']}")
```

**Example Output:**

```json
{
  "ok": true,
  "result": [
    {
      "botid": "1234567",
      "name": "Support Bot",
      "username": "support_bot",
      "status": "working",
      "creation_date": "14:30:22 01:05:2023",
      "has_token": true
    },
    {
      "botid": "7654321",
      "name": "Quiz Bot",
      "username": "quiz_master_bot",
      "status": "stopped",
      "creation_date": "09:15:43 16:04:2023",
      "has_token": true
    }
  ]
}
```

#### get\_bot\_info

Retrieves detailed information about a specific bot.

```python
Account.get_bot_info(botid)
```

**Parameters:**

* `botid` (Required): ID of the bot to get information for.

**Example:**

```python
info = Account.get_bot_info("1234567")
if info["ok"]:
    bot_info = info["result"]
    Bot.sendMessage(f"Bot {bot_info['name']}: {bot_info['user_count']} users, {bot_info['command_count']} commands")
```

**Example Output:**

```json
{
  "ok": true,
  "result": {
    "botid": "1234567",
    "name": "Support Bot",
    "username": "support_bot",
    "status": "working",
    "creation_date": "14:30:22 01:05:2023",
    "has_token": true,
    "command_count": 12,
    "user_count": 278,
    "points_used": 5432
  }
}
```

#### get\_bot\_status

Checks the status of a bot.

```python
Account.get_bot_status(botid)
```

**Parameters:**

* `botid` (Required): ID of the bot to check.

**Example:**

```python
status = Account.get_bot_status("1234567")
if status["ok"]:
    Bot.sendMessage(f"Bot status: {status['result']['status']}")
```

**Example Output:**

```json
{
  "ok": true,
  "result": {
    "status": "online"
  }
}
```

#### get\_bot\_data

Retrieves stored global data for a specific bot.

```python
Account.get_bot_data(botid, name)
```

**Parameters:**

* `botid` (Required): ID of the bot to get data for.
* `name` (Required): Name of the data to retrieve.

**Example:**

```python
data = Account.get_bot_data("1234567", "bot_settings")
if data["ok"]:
    Bot.sendMessage(f"Bot settings: {data['result']}")
```

**Example Output:**

```json
{
  "ok": true,
  "result": {
    "welcome_msg": "Hello!",
    "timeout": 30,
    "language": "en"
  }
}
```

#### set\_bot\_data

Stores global data for a specific bot.

```python
Account.set_bot_data(botid, name, data)
```

**Parameters:**

* `botid` (Required): ID of the bot to store data for.
* `name` (Required): Name identifier for the data.
* `data` (Required): The data to store (limited to 10MB).

**Example:**

```python
result = Account.set_bot_data("1234567", "bot_settings", {"welcome_msg": "Hello!"})
Bot.sendMessage(f"Save result: {result['result']}")
```

**Example Output:**

```json
{
  "ok": true,
  "result": "Data saved successfully"
}
```

### Command Management Methods

#### create\_command

Creates a new command for a bot.

```python
Account.create_command(botid, command, code)
```

**Parameters:**

* `botid` (Required): ID of the bot to create the command for.
* `command` (Required): Name of the command.
* `code` (Required): Code for the command.

**Example:**

```python
result = Account.create_command("1234567", "/hello", "Bot.sendMessage('Hello, world!')")
Bot.sendMessage(f"Command creation result: {result['result']}")
```

**Example Output:**

```json
{
  "ok": true,
  "result": "Command created successfully"
}
```

#### delete\_command

Deletes a command from a bot.

```python
Account.delete_command(botid, command)
```

**Parameters:**

* `botid` (Required): ID of the bot to delete the command from.
* `command` (Required): Name of the command to delete.

**Example:**

```python
result = Account.delete_command("1234567", "/hello")
Bot.sendMessage(f"Command deletion result: {result['result']}")
```

**Example Output:**

```json
{
  "ok": true,
  "result": "Command deleted successfully"
}
```

#### edit\_command

Updates the code of an existing command.

```python
Account.edit_command(botid, command, code)
```

**Parameters:**

* `botid` (Required): ID of the bot to edit the command for.
* `command` (Required): Name of the command to edit.
* `code` (Required): New code for the command.

**Example:**

```python
result = Account.edit_command("1234567", "/hello", "Bot.sendMessage('Updated hello message!')")
Bot.sendMessage(f"Command update result: {result['result']}")
```

**Example Output:**

```json
{
  "ok": true,
  "result": "Command updated successfully"
}
```

#### get\_command\_list

Retrieves a list of all commands for a bot.

```python
Account.get_command_list(botid)
```

**Parameters:**

* `botid` (Required): ID of the bot to get commands for.

**Example:**

```python
commands = Account.get_command_list("1234567")
if commands["ok"] and commands["result"]:
    for cmd in commands["result"]:
        Bot.sendMessage(f"Command: {cmd['command']}, Has code: {cmd['has_code']}")
```

**Example Output:**

```json
{
  "ok": true,
  "result": [
    {
      "command": "/start",
      "code_length": 256,
      "has_code": true
    },
    {
      "command": "/help",
      "code_length": 128,
      "has_code": true
    },
    {
      "command": "/settings",
      "code_length": 512,
      "has_code": true
    }
  ]
}
```

#### get\_command\_info

Retrieves detailed information about a specific command.

```python
Account.get_command_info(botid, command)
```

**Parameters:**

* `botid` (Required): ID of the bot the command belongs to.
* `command` (Required): Name of the command to get information for.

**Example:**

```python
info = Account.get_command_info("1234567", "/hello")
if info["ok"]:
    cmd_info = info["result"]
    Bot.sendMessage(f"Command code: {cmd_info['code']}")
```

**Example Output:**

```json
{
  "ok": true,
  "result": {
    "command": "/hello",
    "code": "Bot.sendMessage('Hello, world!')",
    "code_length": 31,
    "stats": {
      "executions": 342,
      "last_executed": "2023-05-15T14:30:22Z"
    }
  }
}
```

#### get\_command\_usage

Retrieves usage statistics for a specific command.

```python
Account.get_command_usage(botid, command, period="all")
```

**Parameters:**

* `botid` (Required): ID of the bot the command belongs to.
* `command` (Required): Name of the command to get usage for.
* `period` (Optional): Time period for statistics ("hour", "day", "week", "month", "all").

**Example:**

```python
usage = Account.get_command_usage("1234567", "/hello", "week")
if usage["ok"]:
    Bot.sendMessage(f"Command usage: {usage['result']}")
```

**Example Output:**

```json
{
  "ok": true,
  "result": {
    "command": "/hello",
    "count": 123,
    "update_types": {
      "message": 85,
      "callback_query": 38
    },
    "execution_types": {
      "direct": 95,
      "celery": 28
    },
    "period": "week"
  }
}
```

### User Management Methods

#### blockUser

Blocks a user from using a specific bot.

```python
Account.blockUser(user_id)
```

**Parameters:**

* `user_id` (Required): ID of the user to block.

**Example:**

```python
result = Account.blockUser("123456789")
Bot.sendMessage(f"Block result: {result['result']}")
```

**Example Output:**

```json
{
  "ok": true,
  "result": "User blocked successfully"
}
```

#### unblockUser

Unblocks a previously blocked user.

```python
Account.unblockUser(user_id)
```

**Parameters:**

* `user_id` (Required): ID of the user to unblock.

**Example:**

```python
result = Account.unblockUser("123456789")
Bot.sendMessage(f"Unblock result: {result['result']}")
```

**Example Output:**

```json
{
  "ok": true,
  "result": "User unblocked successfully"
}
```

#### getBlockedUsers

Retrieves a list of blocked users for a specific bot.

```python
Account.getBlockedUsers(botid)
```

**Parameters:**

* `botid` (Required): ID of the bot to get blocked users for.

**Example:**

```python
users = Account.getBlockedUsers("1234567")
if users["ok"] and users["result"]:
    for user in users["result"]:
        Bot.sendMessage(f"Blocked user: {user['user_id']}, Date: {user['blocked_date']}")
```

**Example Output:**

```json
{
  "ok": true,
  "result": [
    {
      "user_id": "123456789",
      "blocked_date": "2023-05-10T14:30:22Z"
    },
    {
      "user_id": "987654321",
      "blocked_date": "2023-05-12T09:15:43Z"
    }
  ]
}
```

#### getBlockedUsersFile

Generates a file containing blocked users information.

```python
Account.getBlockedUsersFile(botid=None, output_format="csv")
```

**Parameters:**

* `botid` (Optional): ID of the bot to get blocked users for. If omitted, gets all blocked users.
* `output_format` (Optional): Format of the output file ("csv" or "json").

**Example:**

```python
file = Account.getBlockedUsersFile("1234567", "json")
Bot.sendDocument(file)
```

**Example Output:**

```
# Returns a file-like object that can be directly passed to Bot.sendDocument()
# For CSV format, the file contains columns: user_id, blocked_date
# For JSON format, the file contains an array of objects with user_id and blocked_date fields
```

### Statistics and Reporting Methods

#### get\_bot\_stats

Retrieves comprehensive statistics for a specific bot.

```python
Account.get_bot_stats(botid)
```

**Parameters:**

* `botid` (Required): ID of the bot to get statistics for.

**Example:**

```python
stats = Account.get_bot_stats("1234567")
if stats["ok"]:
    bot_stats = stats["result"]
    Bot.sendMessage(f"Bot {bot_stats['name']}: {bot_stats['users']['total']} users, {bot_stats['users']['active_30d']} active")
```

**Example Output:**

```json
{
  "ok": true,
  "result": {
    "botid": "1234567",
    "name": "Support Bot",
    "username": "support_bot",
    "status": "working",
    "users": {
      "total": 1250,
      "active_30d": 450,
      "new_7d": 75,
      "blocked": 12
    },
    "commands": {
      "total": 15,
      "usage": {
        "start": 523,
        "help": 186,
        "settings": 94
      }
    },
    "points_used": 8765,
    "all_time_users": 1584
  }
}
```

#### get\_bot\_usage

Retrieves detailed usage statistics for a specific bot.

```python
Account.get_bot_usage(botid, period="all")
```

**Parameters:**

* `botid` (Required): ID of the bot to get usage for.
* `period` (Optional): Time period for statistics ("day", "week", "month", "all").

**Example:**

```python
usage = Account.get_bot_usage("1234567", "month")
if usage["ok"]:
    Bot.sendMessage(f"Bot usage: {usage['result']}")
```

**Example Output:**

```json
{
  "ok": true,
  "result": {
    "commands": {
      "/start": {
        "count": 523,
        "update_types": {
          "message": 400,
          "callback_query": 123
        },
        "execution_types": {
          "direct": 450,
          "celery": 73
        }
      },
      "/help": {
        "count": 186,
        "update_types": {
          "message": 150,
          "callback_query": 36
        },
        "execution_types": {
          "direct": 160,
          "celery": 26
        }
      }
    },
    "period": "month",
    "bot": {
      "botid": "1234567",
      "name": "Support Bot",
      "username": "support_bot",
      "status": "working"
    }
  }
}
```

#### get\_bots\_stats

Retrieves statistics for all bots in the account.

```python
Account.get_bots_stats()
```

**Example:**

```python
stats = Account.get_bots_stats()
if stats["ok"]:
    all_stats = stats["result"]
    Bot.sendMessage(f"Total bots: {all_stats['total_bots']}, Total users: {all_stats['total_users']}")
```

**Example Output:**

```json
{
  "ok": true,
  "result": {
    "total_bots": 5,
    "total_users": 2584,
    "total_active_users": 943,
    "total_commands": 68,
    "bots": [
      {
        "botid": "1234567",
        "name": "Support Bot",
        "username": "support_bot",
        "status": "working",
        "users": 1250,
        "active_users": 450,
        "commands": 15,
        "points_used": 5432,
        "blocked_users": 12
      },
      {
        "botid": "7654321",
        "name": "Quiz Bot",
        "username": "quiz_master_bot",
        "status": "working",
        "users": 856,
        "active_users": 312,
        "commands": 8,
        "points_used": 2345,
        "blocked_users": 5
      }
    ]
  }
}
```

#### get\_stats

Retrieves comprehensive account-level statistics.

```python
Account.get_stats()
```

**Example:**

```python
stats = Account.get_stats()
if stats["ok"]:
    account_stats = stats["result"]
    Bot.sendMessage(f"Account stats: {account_stats['bots']['total']} bots, {account_stats['users']['total']} users")
```

**Example Output:**

```json
{
  "ok": true,
  "result": {
    "email": "user@example.com",
    "plan": "Premium",
    "points_left": 8500,
    "points_used": 23450,
    "points_reset_at": "2023-06-01",
    "account_created": "2022-11-15 09:30:45",
    "bots": {
      "total": 5,
      "botids": ["1234567", "7654321", "2345678", "8765432", "3456789"]
    },
    "users": {
      "total": 2584,
      "active_30d": 943
    },
    "commands": {
      "total": 68
    }
  }
}
```

### Import/Export Methods

#### export\_bot

Exports a bot's configuration and commands as a JSON file.

```python
Account.export_bot(botid)
```

**Parameters:**

* `botid` (Required): ID of the bot to export.

**Example:**

```python
try:
    file = Account.export_bot("1234567")
    Bot.sendDocument(file)
except ValueError as e:
    Bot.sendMessage(f"Export error: {str(e)}")
```

**Example Output:**

```
# Returns a file-like object that can be directly passed to Bot.sendDocument()
# The file contains a JSON object with the following structure:
# {
#   "bot": {
#     "botid": "1234567",
#     "bot_name": "Support Bot",
#     "bot_username": "support_bot",
#     "creation_date": "2023-05-01 14:30:22",
#     "_export_date": "2023-05-20 10:15:43"
#   },
#   "commands": [
#     {"command": "/start", "code": "Bot.sendMessage('Welcome!')"},
#     {"command": "/help", "code": "Bot.sendMessage('Help info')"}
#   ],
#   "global_data": [
#     {"name": "settings", "data": {"language": "en"}}
#   ],
#   "export_info": {
#     "date": "2023-05-20 10:15:43",
#     "exporter": "user@example.com",
#     "version": "1.0"
#   }
# }
```

#### import\_bot

Imports a bot from an export file.

```python
Account.import_bot(import_data, new_token=None)
```

**Parameters:**

* `import_data` (Required): The JSON data from an exported bot.
* `new_token` (Optional): Token for the new bot.

**Example:**

```python
# Assuming import_data contains valid bot export data
result = Account.import_bot(import_data, "123456789:ABCDEF-ghijklmnopqrstuvwxyz")
if result["ok"]:
    Bot.sendMessage(f"Imported bot with ID: {result['botid']}")
```

**Example Output:**

```json
{
  "ok": true,
  "result": "Bot imported successfully",
  "botid": "8765432",
  "command_count": 12
}
```

### API Management

#### revoke\_api

Revokes the current API key and generates a new one.

```python
Account.revoke_api()
```

**Example:**

```python
result = Account.revoke_api()
if result["ok"]:
    Bot.sendMessage(f"New API key: {result['api_key']}")
```

**Example Output:**

```json
{
  "ok": true,
  "result": "API key revoked successfully and new key generated",
  "api_key": "abcdef1234567890abcdef1234567890"
}
```

## Enhanced Resource Management

### New accountRes Class

The 4.8.0 update introduces a new `accountRes` class for managing account-level resources, complementing the existing resource management system.

```python
res = libs.Resources.accountRes(name)
```

**Parameters:**

* `name` (Required): The name of the resource to manage.

### Resource Management Methods

All methods from the BaseRes class are available:

* `value()`: Gets the current value of the resource.
* `add(value)`: Adds to the resource value.
* `cut(value)`: Subtracts from the resource value.
* `set(value)`: Sets the resource to a specific value.
* `reset()`: Resets the resource value to zero.

**Example:**

```python
# Create an account-level resource
account_points = libs.Resources.accountRes("subscription_points")

# Add points
new_value = account_points.add(100)
Bot.sendMessage(f"Added points. New value: {new_value}")

# Check current value
current = account_points.value()
Bot.sendMessage(f"Current points: {current}")

# Use points
account_points.cut(50)
Bot.sendMessage(f"Used 50 points. Remaining: {account_points.value()}")
```

**Example Output:**

```
# For add():
100.0  # Returns the new value after addition

# For value():
100.0  # Returns the current value

# For cut():
50.0  # Returns the new value after subtraction

# For set():
200.0  # Returns the value that was set

# For reset():
0.0  # Always returns zero
```

## Server Improvements

The 4.8.0 update includes significant server-side improvements:

1. **Enhanced Stability**: Improved error handling and recovery mechanisms to prevent service disruptions.
2. **Optimized Performance**: Reduced response times and better resource allocation for smoother operation under high load.
3. **Improved Webhook Handling**: Faster and more reliable webhook processing for better bot responsiveness.
4. **Advanced Monitoring**: Better monitoring systems to detect and address issues before they affect users.

These improvements ensure that your bots remain operational and responsive, even during peak usage times or when handling complex commands.

## Command Aliases

The upcoming UI update will introduce support for command aliases, allowing multiple command triggers to execute the same code. This powerful feature will enable:

1. **Multi-language Support**: Create different command names for different languages.
2. **Command Variations**: Support both full and abbreviated versions of commands.
3. **Intuitive Interactions**: Allow users to trigger commands with natural language variations.

The alias system will be fully integrated into the command management system and accessible through both the UI and API.

## Bot Recovery System

The new bot recovery system allows users to recover accidentally deleted bots within 90 days, with features including:

1. **Temporary Deletion**: Bots are moved to a recovery collection rather than being permanently deleted.
2. **90-Day Recovery Window**: Generous timeframe to recover deleted bots.
3. **Statistics Tracking**: Monitor how many bots you've deleted and how many can be recovered.
4. **Expiration Management**: Clear visibility into when deleted bots will expire.

**Example:**

```python
# Get list of deleted bots
deleted_bots = Account.get_deleted_bots()
for bot_info in deleted_bots["result"]:
    Bot.sendMessage(f"Bot: {bot_info['name']}, Days remaining: {bot_info['days_remaining']}")

# Recover a bot
Account.recover_bot("1234567")

# Get stats about deleted bots
stats = Account.get_deleted_bots_stats()
Bot.sendMessage(f"Total deleted: {stats['result']['total']}, Recoverable: {stats['result']['recoverable']}")
```

## Coming Soon Features

### Bot Store

The upcoming Bot Store will revolutionize how users discover and implement Telegram bots:

* **Pre-made Bot Templates**: Access a library of ready-to-use bot templates for various industries and use cases.
* **Community Sharing**: Share your own bot creations with the TBC community.
* **One-Click Deployment**: Deploy complete bots with just a single click, without any coding required.
* **Categorized Listings**: Browse bots by category, popularity, or functionality.
* **Custom Modifications**: Use templates as starting points and customize them to your specific needs.

This feature will significantly reduce the time and effort needed to create powerful bots, making advanced bot functionality accessible to users of all skill levels.

### Points Faucet

The Points Faucet system will ensure that all users have unlimited access to points for running their bots:

* **Unlimited Points**: Obtain as many points as you need to run your bots without restrictions.
* **Completely Free**: All points remain 100% free, with no hidden costs or premium tiers.
* **Automated System**: Request points automatically through the faucet system without needing to contact admins.
* **Instant Credits**: Points are credited instantly to your account.
* **No Usage Limits**: Create and run as many bots as you want without worrying about running out of points.

This system reinforces Telebot Creator's commitment to providing a completely free platform for bot creation and hosting.

Both of these features are currently in final development and will be released in an upcoming update. Stay tuned to the TBC announcements channel for release dates and additional information.


<!-- Source: https://help.telebotcreator.com/version-4.9.0-update.md -->

# Version 4.9.0 Update

We're excited to announce the release of TeleBot Creator 4.9.0 with significant improvements to stability, performance, and functionality.

## Major Improvements

### 🛠️ Bug Fixes

* Most of the previously reported bugs have been fixed in this release
* Improved stability across all components and libraries

### ⏱️ New Timing Controls

* Added native `time.sleep()` function with a maximum limit of 10 seconds
* Increased code execution timeout from 60 to 120 seconds
* Enhanced `run_after` command:
  * Maximum timeout extended to 1 year (365 days)
  * Minimum timeout reduced to 0.1 seconds
  * Smart rate limiting: For ultra-fast commands (under 0.4 seconds), a limit of 5 executions within 5 seconds to prevent abuse
  * Increased maximum scheduled `run_after` commands per user from 20 to 100

### 💰 TON Integration

* Added comprehensive TON blockchain support through the new `TonLib` (see dedicated [TON Library Documentation](ton-library-documentation))
* Features include wallet creation, balance checking, transactions, and more

### 🔄 Code Improvements

* Direct HTTP module usage is now recommended over `libs.customHTTP()`
* For handling inline queries and other update types, use the `/handler_<update_type>` command format

### ⚠️ Important Changes

* The `import x` statement should not be present in any user code
* Use built-in libraries and modules instead of external imports

## Documentation Updates

We've added new documentation pages:

* [TON Library Documentation](ton-library-documentation): Complete guide to blockchain integration
* Updated examples and use cases across all documentation

## Upgrading

To take advantage of these new features, simply restart your bot or create a new one. All improvements are automatically available in your workspace.

## Feedback

As always, we value your feedback. If you encounter any issues or have suggestions for further improvements, please let us know through our support channels.


<!-- Source: https://help.telebotcreator.com/version-5.0.0-update.md -->

# Version 5.0.0 Update

We're excited to announce the release of TeleBot Creator 5.0.0, featuring significant improvements to performance, stability, and functionality.

## Major Improvements

### ⏱️ Extended Command Runtime

* Commands can now run up to 160 seconds (increased from 120 seconds)
* Performance optimizations for better command execution
* Major bug fixes improving overall stability

### 📊 New Statistics Functions

Account and Bot classes now include powerful statistics tracking capabilities:

#### Account.getStats

This function allows you to retrieve user statistics across multiple bots in your account:

```python
# Get user statistics for all bots in your account
stats = Account.getStats()

# Get user statistics for specific time frames
stats = Account.getStats(time_frames=["24h", "7d", "30d"])

# Get user statistics for specific bots
stats = Account.getStats(bot_ids=["bot123456", "bot654321"])

# Combine both parameters
stats = Account.getStats(time_frames=["24h", "7d"], bot_ids=["bot123456"])
```

**Parameters:**

* `time_frames`: List of time frames to query (optional, default: \["24h"])
  * Format: "h" for hours or "d" for days (e.g., "24h", "7d")
  * Maximum time frame: 365 days
* `bot_ids`: List of bot IDs to query (optional, default: all bots in account)

**Returns:**

* Dictionary with time frames as keys and active user counts as values
* Example: `{"24h": 150, "7d": 350}`

#### Bot.getStats

Similar to Account.getStats but for a specific bot:

```python
# Get user statistics for current bot
stats = Bot.getStats()

# Get user statistics for specific time frames
stats = Bot.getStats(time_frames=["24h", "7d", "30d"])

# Get statistics for a specific bot with API key authentication
stats = Bot.getStats(bot_id="bot123456", api_key="your_api_key")
```

**Parameters:**

* `time_frames`: List of time frames to query (optional, default: \["24h"])
* `bot_id`: Bot ID to query (optional, default: current bot)
* `api_key`: API key for authentication when querying other bots (optional)

**Returns:**

* Dictionary with time frames as keys and active user counts as values
* Example: `{"24h": 150, "7d": 350}`

### 🔄 Data Transfer Functionality

The new TransferData function in the Account class allows you to transfer bot data between bots:

```python
# Transfer data from one bot to another
result = Account.TransferData(from_bot="source_bot_id", to_bot="destination_bot_id")
```

**Parameters:**

* `from_bot`: Source bot ID to transfer data from
* `to_bot`: Destination bot ID to transfer data to

**Returns:**

* Dictionary with operation status
* Success: `{"ok": True, "result": "Data transferred successfully"}`
* Failure: `{"ok": False, "result": "Error message"}`

### 🤖 OpenRouter AI Integration

OpenRouter API is now fully supported through the openai\_lib, with enhanced timeout capabilities:

```python
# Initialize OpenAI client with OpenRouter
API_KEY = "YOUR_OPENROUTER_API_KEY"
MESSAGE = "hello"

# Create client with extended timeout (up to 160 seconds)
client = libs.openai_lib.OpenAIClient(api_key=API_KEY, timeout=120)

# Initialize AI assistant with specific model
assistant = libs.openai_lib.AIAssistant(
    openai_client=client,
    model="meta-llama/llama-3.3-8b-instruct:free",
    system_message="You're helpful assistant."
)

# Send message and get response
response = assistant.send_message(MESSAGE)
response_text = str(response.get("content")[0]['text']['value'])
bot.sendMessage(response_text)
```

**Key Features:**

* Support for OpenRouter API with access to multiple AI models
* Extended timeout up to 160 seconds (configurable)
* Automatic error handling and retries
* System message customization
* Compatible with various models including Meta's Llama models

## Stability Improvements

* Enhanced bot optimization for better performance
* Improved error handling and logging
* Memory usage optimizations
* Fixed issues with long-running commands

## Upgrading

To take advantage of these new features, simply restart your bot or create a new one. All improvements are automatically available in your workspace.

## Feedback

As always, we value your feedback. If you encounter any issues or have suggestions for further improvements, please let us know through our support channels.


<!-- Source: https://help.telebotcreator.com/conclusion-and-next-steps.md -->

# Conclusion and Next Steps

#### **13. Conclusion and Next Steps**

Thank you for exploring the comprehensive documentation for Telebot Creator. This platform is designed to empower developers and businesses with the tools to build and manage highly functional Telegram bots. Whether you're a beginner or an advanced user, Telebot Creator offers endless possibilities to innovate, automate, and engage.

***

### **13.1 Summary of Key Features**

Here’s a recap of the major topics covered in this documentation:

1. **Bot Creation**:
   * Step-by-step guide to creating bots using the Bot API token.
   * Customizing commands with TPY (Telebot Python).
2. **Libraries and Integrations**:
   * Leveraging `libs.Coinbase`, `libs.CSV`, `libs.Polygon`, and more to extend bot functionality.
   * Automating cryptocurrency transactions, data management, and API integrations.
3. **Advanced Features**:
   * Creating dynamic workflows with `handleNextCommand` and `runCommand`.
   * Managing broadcasts and multi-bot communication with `Bot.broadcast` and webhooks.
4. **Best Practices and Troubleshooting**:
   * Optimizing point usage.
   * Debugging and handling errors effectively.
   * Securing sensitive data and ensuring webhook integrity.

***

### **13.2 Getting the Most Out of Telebot Creator**

#### **Explore New Use Cases**

Push the boundaries of what your bots can achieve:

* Experiment with libraries like `libs.Coinbase` for payment handling or `libs.Webhook` for real-time updates.
* Combine features to create bots for referral systems, event management, and more.

#### **Leverage Multi-Bot Management**

* Use `Bot.info` and `libs.Webhook.getUrlFor` to enable bots to communicate and share workloads seamlessly.

#### **Optimize Bot Performance**

* Analyze bot usage and performance metrics with `Bot.info`.
* Ensure efficient workflows to handle large user bases or complex processes.

***

### **13.3 Community and Support**

#### **Join the Community**

Connect with other developers and share your experiences in the official Telebot Creator Help Group:

* [Join Now](http://t.me/telebotcreatorbetachat)

#### **Request Features or Report Bugs**

We’re always looking to improve. Share your feedback or report issues:

* Use the feedback form available on the platform.
* Participate in community discussions to suggest enhancements.

***

### **13.4 Looking Ahead**

#### **Planned Updates**

The Telebot Creator team is constantly evolving the platform. Here’s what’s coming next:

1. **Enhanced User Interface**:
   * A redesigned dashboard for easier bot management.
2. **Expanded Library Support**:
   * Additional libraries for advanced integrations.
3. **Improved Analytics**:
   * Real-time monitoring and usage insights for your bots.

#### **Stay Updated**

Keep an eye on the release notes and announcements for the latest features.

***

### **13.5 Thank You**

We sincerely thank you for choosing Telebot Creator as your bot development platform. Your creativity and innovation drive the success of this community. We’re excited to see the amazing bots you’ll create.

**Let’s build the future of automation together!**


<!-- Source: https://help.telebotcreator.com/crypto-libraries-documentation.md -->

# Crypto libraries Documentation

**Overview**\
The new **libs.web3lib** library is designed to simplify and secure transactions on Ethereum-compatible (EVM) blockchains. This library is packed with robust features like:

* **Multi-network support:** Interact with over 30 EVM chains effortlessly.
* **Automatic gas estimation:** Avoid under- or overestimating gas.
* **Retry logic:** Optionally retry transactions on transient errors.
* **Proxy:** The library uses a large set of proxies, which minimizes rate limit errors.
* **Centralized key management:** Easily store and retrieve private keys using Telebot Creator's MongoDB integration.

**Deprecated Libraries**\
Please note that the following libraries are now deprecated and no longer supported:

* **libs.Polygon**
* **libs.ARB**
* **libs.TTcoin**
* **libs.Tomochain**

We strongly recommend using **libs.web3lib** for all new projects.\\

#### Below is a comprehensive explanation of each function, its parameters, and how to use them.

***

### **`sendNativeCoin(...)`**

This function allows you to send native coins like **ETH**, **BNB**, **MATIC**, etc., on supported EVM chains. It’s ideal for simple value transfers without smart contracts.

#### **Function Signature**

```tpy
def sendNativeCoin(
    value: float,
    to: str,
    rpc_url: Optional[str] = None,
    gas: Optional[int] = None,
    gasPrice: Optional[int] = None,
    private_key: Optional[str] = None,
    increase_gas: Optional[int] = None,
    wait_for_confirmation: bool = True,
    confirmation_timeout: int = 15,
    network: Optional[str] = None,
    estimate_gas: bool = True,
    retry: bool = False,
)
```

#### **Parameter Details**

| Parameter                   | Type            | Description                                                                                                                                |
| --------------------------- | --------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| **`value`**                 | `float`         | Amount of native coin (e.g., ETH, BNB) to send.                                                                                            |
| **`to`**                    | `str`           | The recipient's wallet address.                                                                                                            |
| **`rpc_url`**               | `Optional[str]` | Custom RPC URL for the target network. If not provided, you must define the `network` parameter.                                           |
| **`gas`**                   | `Optional[int]` | Manually set gas limit. If not provided, gas will be estimated automatically.                                                              |
| **`gasPrice`**              | `Optional[int]` | Specify the gas price. Defaults to network’s current gas price if omitted.                                                                 |
| **`private_key`**           | `Optional[str]` | Your wallet’s private key for signing the transaction. Required for successful execution.                                                  |
| **`increase_gas`**          | `Optional[int]` | Increase the estimated gas price by a percentage. Useful for faster confirmations.                                                         |
| **`wait_for_confirmation`** | `bool`          | If `True`, the function waits until the transaction is confirmed. Default is `True`.                                                       |
| **`confirmation_timeout`**  | `int`           | Maximum seconds to wait for confirmation. Default is `15`.                                                                                 |
| **`network`**               | `Optional[str]` | Instead of defining an `rpc_url`, specify the network name (e.g., `"ethereum"`, `"bsc"`, `"polygon"`).                                     |
| **`estimate_gas`**          | `bool`          | If `True`, gas will be estimated automatically. Recommended for convenience. Default is `True`.                                            |
| **`retry`**                 | `bool`          | If `True`, the function retries the transaction once if it fails. Useful to bypass common errors like "nonce too low". Default is `False`. |

***

### **`sendETHER(...)`**

This function is used to send **ERC-20 tokens** by specifying a token contract address. It's designed for token transfers that require interacting with smart contracts.

#### **Function Signature**

```tpy
def sendETHER(
    value: float, 
    to: str, 
    rpc_url: Optional[str] = None, 
    gas: Optional[int] = None,
    gasPrice: Optional[int] = None, 
    private_key: Optional[str] = None,
    increase_gas: Optional[int] = None,
    wait_for_confirmation: bool = True,
    confirmation_timeout: int = 15,
    network: Optional[str] = None,
    contract_address: Optional[str] = None,
    retry: bool = False,
    estimate_gas: bool = True,
)
```

#### **Parameter Details**

| Parameter                   | Type            | Description                                                                                                                                |
| --------------------------- | --------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| **`value`**                 | `float`         | Amount of tokens to send.                                                                                                                  |
| **`to`**                    | `str`           | The recipient's wallet address.                                                                                                            |
| **`rpc_url`**               | `Optional[str]` | Custom RPC URL for the target network. If not provided, you must define the `network` parameter.                                           |
| **`gas`**                   | `Optional[int]` | Manually set gas limit. If not provided, gas will be estimated automatically.                                                              |
| **`gasPrice`**              | `Optional[int]` | Specify the gas price. Defaults to network’s current gas price if omitted.                                                                 |
| **`private_key`**           | `Optional[str]` | Your wallet’s private key for signing the transaction. Required for successful execution.                                                  |
| **`increase_gas`**          | `Optional[int]` | Increase the estimated gas price by a percentage. Useful for faster confirmations.                                                         |
| **`wait_for_confirmation`** | `bool`          | If `True`, the function waits until the transaction is confirmed. Default is `True`.                                                       |
| **`confirmation_timeout`**  | `int`           | Maximum seconds to wait for confirmation. Default is `15`.                                                                                 |
| **`network`**               | `Optional[str]` | Instead of defining an `rpc_url`, specify the network name (e.g., `"ethereum"`, `"bsc"`, `"polygon"`).                                     |
| **`contract_address`**      | `Optional[str]` | The ERC-20 contract address. **Required for token transfers.**                                                                             |
| **`estimate_gas`**          | `bool`          | If `True`, gas will be estimated automatically. Recommended for convenience. Default is `True`.                                            |
| **`retry`**                 | `bool`          | If `True`, the function retries the transaction once if it fails. Useful to bypass common errors like "nonce too low". Default is `False`. |

***

### Supported Networks

Below is a table listing all the EVM chains supported by libs.web3lib:

| Network   | Chain ID   | Default RPC URL                                                                    |
| --------- | ---------- | ---------------------------------------------------------------------------------- |
| Ethereum  | 1          | [https://rpc.ankr.com/eth](https://rpc.ankr.com/eth)                               |
| BSC       | 56         | [https://bsc-dataseed.binance.org/](https://bsc-dataseed.binance.org/)             |
| Polygon   | 137        | [https://polygon-rpc.com/](https://polygon-rpc.com/)                               |
| Avalanche | 43114      | [https://api.avax.network/ext/bc/C/rpc](https://api.avax.network/ext/bc/C/rpc)     |
| Fantom    | 250        | [https://rpc.ftm.tools/](https://rpc.ftm.tools/)                                   |
| Arbitrum  | 42161      | [https://arb1.arbitrum.io/rpc](https://arb1.arbitrum.io/rpc)                       |
| Optimism  | 10         | [https://mainnet.optimism.io/](https://mainnet.optimism.io/)                       |
| Harmony   | 1666600000 | [https://api.harmony.one/](https://api.harmony.one/)                               |
| Cronos    | 25         | [https://evm.cronos.org/](https://evm.cronos.org/)                                 |
| Moonriver | 1285       | [https://rpc.moonriver.moonbeam.network/](https://rpc.moonriver.moonbeam.network/) |
| Moonbeam  | 1284       | [https://rpc.api.moonbeam.network/](https://rpc.api.moonbeam.network/)             |
| Celo      | 42220      | [https://forno.celo.org/](https://forno.celo.org/)                                 |
| Heco      | 128        | [https://rpc.ankr.com/huobichain](https://rpc.ankr.com/huobichain)                 |
| Okexchain | 66         | [https://exchainrpc.okex.org/](https://exchainrpc.okex.org/)                       |
| Xdai      | 100        | [https://rpc.gnosischain.com/](https://rpc.gnosischain.com/)                       |
| KCC       | 321        | [https://rpc-mainnet.kcc.network/](https://rpc-mainnet.kcc.network/)               |
| Metis     | 1088       | [https://andromeda.metis.io/?owner=1088](https://andromeda.metis.io/?owner=1088)   |
| Aurora    | 1313161554 | [https://mainnet.aurora.dev](https://mainnet.aurora.dev)                           |
| Base      | 8453       | [https://mainnet.base.org](https://mainnet.base.org)                               |
| ZKSync    | 324        | [https://mainnet.era.zksync.io](https://mainnet.era.zksync.io)                     |
| Scroll    | 534352     | [https://rpc.scroll.io](https://rpc.scroll.io)                                     |
| Linea     | 59144      | [https://rpc.linea.build](https://rpc.linea.build)                                 |
| Boba      | 288        | [https://mainnet.boba.network](https://mainnet.boba.network)                       |
| Kava      | 2222       | [https://evm.kava.io](https://evm.kava.io)                                         |
| Fuse      | 122        | [https://rpc.fuse.io](https://rpc.fuse.io)                                         |
| Evmos     | 9001       | [https://evmos-evm.publicnode.com](https://evmos-evm.publicnode.com)               |
| Canto     | 7700       | [https://canto.slingshot.finance](https://canto.slingshot.finance)                 |
| Astar     | 592        | [https://evm.astar.network](https://evm.astar.network)                             |
| Telos     | 40         | [https://mainnet.telos.net/evm](https://mainnet.telos.net/evm)                     |
| Rootstock | 30         | [https://public-node.rsk.co](https://public-node.rsk.co)                           |
| TTcoin    | 22023      | [https://mainnet-rpc.tscscan.com](https://mainnet-rpc.tscscan.com)                 |

***

### Usage Examples

#### Example 1: Sending a Native Coin Transfer (ETH)

```tpy
dummy_private_key = "0xYOUR_PRIVATE_KEY_HERE"
test_rpc = "https://rpc.ankr.com/eth"
test_recipient = "0xRecipientAddressHere"

tx_hash = libs.web3lib.sendNativeCoin(
    value = 0.5,
    to = test_recipient,
    rpc_url = test_rpc,
    private_key = dummy_private_key,
    network = "ethereum",
    retry = True,
    estimate_gas = True
)

bot.sendMessage(f"Native Transfer TX Hash: {tx_hash}")
```

#### Example 2: Sending an ERC‑20 Token Transfer

```tpy
dummy_private_key = "0xYOUR_PRIVATE_KEY_HERE"
dummy_contract = "0xTokenContractAddressHere"
test_recipient = "0xRecipientAddressHere"
test_rpc = "https://rpc.ankr.com/eth"

tx_hash = libs.web3lib.sendETHER(
    value = 1,                     # Token amount (assuming 18 decimals)
    to = test_recipient,
    rpc_url = test_rpc,
    private_key = dummy_private_key,
    contract_address = dummy_contract,
    network = "ethereum",
    retry = True,
    estimate_gas = True
)

bot.sendMessage(f"Token Transfer TX Hash: {tx_hash}")
```

#### Example 3: Using Network Parameter Only

```tpy
dummy_private_key = "0xYOUR_PRIVATE_KEY_HERE"
dummy_contract = "0xTokenContractAddressHere"
test_recipient = "0xRecipientAddressHere"

tx_hash = libs.web3lib.sendETHER(
    value = 0.25,
    to = test_recipient,
    network = "polygon",
    private_key = dummy_private_key,
    contract_address = dummy_contract,
    retry = False,
    estimate_gas = True
)

bot.sendMessage(f"Token Transfer on Polygon TX Hash: {tx_hash}")
```

***

### Final Notes

* **Deprecated Libraries:**\
  The old libraries (libs.Polygon, libs.ARB, libs.TTcoin, libs.Tomochain) are now deprecated and should no longer be used.\
  Please update your projects to use **libs.web3lib**, which offers a unified and more powerful interface for all EVM chains.


<!-- Source: https://help.telebotcreator.com/telebot-creator-api-v2-flexible-authentication-documentation.md -->

# Telebot Creator API v2 - Flexible Authentication Documentation

### Overview

This document describes the flexible authentication system implemented for the Telebot Creator API v2. The system supports both JWT cookie-based authentication and API key authentication, allowing users to choose the most appropriate method for their use case.

### Authentication Methods

#### 1. JWT Cookie Authentication (Web Interface)

Used by the web interface for user sessions.

* **Cookie Name**: `login_token`
* **Algorithm**: HS256
* **Expiration**: 6 hours (default) or 30 days (remember me)

#### 2. API Key Authentication (Programmatic Access)

Used for programmatic access to the API.

* **Header**: `Authorization: Bearer <api_key>`
* **Query Parameter**: `?api_key=<api_key>`
* **JSON Body**: `{"api_key": "<api_key>"}`

### Endpoints with Flexible Authentication

The following endpoints support both authentication methods:

#### Bot Management

**Create Bot**

* **Endpoint**: `POST /v2/create-bot`
* **Description**: Creates a new bot with the provided token and name
*   **Request Body**:

    ```json
    {
      "bot_token": "1234567890:AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA",
      "bot_name": "My Bot"
    }
    ```
*   **Response**:

    ```json
    {
      "ok": true,
      "result": {
        "botid": "generated_bot_id",
        "bot_name": "My Bot",
        "bot_username": "mybotusername"
      }
    }
    ```

**Delete Bot**

* **Endpoint**: `DELETE /v2/bots/{botid}`
* **Description**: Soft deletes a bot (moves to deleted\_bots collection)
* **URL Parameters**:
  * `botid`: The unique identifier of the bot
*   **Response**:

    ```json
    {
      "ok": true,
      "result": "Bot deleted successfully"
    }
    ```

**Update Bot Token**

* **Endpoint**: `POST /v2/bots/{botid}/update-bot-token`
* **Description**: Updates the bot's Telegram token
* **URL Parameters**:
  * `botid`: The unique identifier of the bot
*   **Request Body**:

    ```json
    {
      "token": "1234567890:NEWAAAAAAAAAAAAAAAAAAAAAAAAAAAA"
    }
    ```
*   **Response**:

    ```json
    {
      "ok": true,
      "result": "Bot token updated successfully"
    }
    ```

**Update Bot Version**

* **Endpoint**: `POST /v2/bots/{botid}/version`
* **Description**: Updates the bot's telebot library version
* **URL Parameters**:
  * `botid`: The unique identifier of the bot
*   **Request Body**:

    ```json
    {
      "version": "4.19.0"
    }
    ```
*   **Response**:

    ```json
    {
      "ok": true,
      "result": "Bot version updated successfully"
    }
    ```

#### Command Management

**Create Command**

* **Endpoint**: `POST /v2/bots/{botid}/commands`
* **Description**: Creates a new command for the bot
* **URL Parameters**:
  * `botid`: The unique identifier of the bot
*   **Request Body**:

    ```json
    {
      "command": "hello",
      "code": "bot.reply_to(message, 'Hello World!')"
    }
    ```
*   **Response**:

    ```json
    {
      "ok": true,
      "result": "Command created successfully"
    }
    ```

**Update Command**

* **Endpoint**: `PUT /v2/bots/{botid}/commands/{command}`
* **Description**: Updates an existing command's code
* **URL Parameters**:
  * `botid`: The unique identifier of the bot
  * `command`: Base64 encoded command name
*   **Request Body**:

    ```json
    {
      "code": "bot.reply_to(message, 'Updated Hello World!')"
    }
    ```
*   **Response**:

    ```json
    {
      "ok": true,
      "command": "hello"
    }
    ```

**Get Command**

* **Endpoint**: `GET /v2/bots/{botid}/commands/{command}`
* **Description**: Retrieves a specific command's details
* **URL Parameters**:
  * `botid`: The unique identifier of the bot
  * `command`: Base64 encoded command name
*   **Response**:

    ```json
    {
      "ok": true,
      "command": {
        "command": "hello",
        "code": "bot.reply_to(message, 'Hello World!')",
        "is_pinned": false
      }
    }
    ```

**Delete Command**

* **Endpoint**: `DELETE /v2/bots/{botid}/commands/{command}`
* **Description**: Deletes a command from the bot
* **URL Parameters**:
  * `botid`: The unique identifier of the bot
  * `command`: Base64 encoded command name
*   **Response**:

    ```json
    {
      "ok": true,
      "result": "Command deleted successfully"
    }
    ```

**Rename Command**

* **Endpoint**: `PATCH /v2/bots/{botid}/commands/{command}/rename`
* **Description**: Renames an existing command
* **URL Parameters**:
  * `botid`: The unique identifier of the bot
  * `command`: Base64 encoded current command name
*   **Request Body**:

    ```json
    {
      "new_name": "greet"
    }
    ```
*   **Response**:

    ```json
    {
      "ok": true,
      "result": "Command renamed successfully"
    }
    ```

#### Folder Management

**Get Folders**

* **Endpoint**: `GET /v2/bots/{botid}/commands/folders`
* **Description**: Retrieves all folders for a bot
* **URL Parameters**:
  * `botid`: The unique identifier of the bot
*   **Response**:

    ```json
    {
      "ok": true,
      "folders": [
        {
          "name": "utility",
          "commands": ["help", "start"]
        }
      ]
    }
    ```

#### Data Management

**Export Users File**

* **Endpoint**: `POST /v2/export-users-file/{botid}`
* **Description**: Exports bot users data in specified format
* **URL Parameters**:
  * `botid`: The unique identifier of the bot
*   **Request Body**:

    ```json
    {
      "format": "json",
      "include_creation_date": true,
      "include_last_active_date": true
    }
    ```
* **Response**: File download with users data

**Export Bot**

* **Endpoint**: `GET /v2/bots/{botid}/export-bot`
* **Description**: Exports bot configuration and commands
* **URL Parameters**:
  * `botid`: The unique identifier of the bot
* **Query Parameters**:
  * `format`: `json`, `yaml`, or `txt` (default: `json`)
  * `include_data`: `true` or `false` (default: `false`)
* **Response**: File download with bot data

**Import Commands**

* **Endpoint**: `POST /v2/bots/{botid}/import-commands`
* **Description**: Imports commands from exported data
* **URL Parameters**:
  * `botid`: The unique identifier of the bot
*   **Request Body**:

    ```json
    {
      "import_data": "base64_encoded_data",
      "format": "json",
      "remove_old_commands": false
    }
    ```
*   **Response**:

    ```json
    {
      "ok": true,
      "result": "Commands imported successfully"
    }
    ```

#### Bot Operations

**Transfer Bot**

* **Endpoint**: `POST /v2/bots/{botid}/transfer-bot`
* **Description**: Transfers bot ownership to another user
* **URL Parameters**:
  * `botid`: The unique identifier of the bot
*   **Request Body**:

    ```json
    {
      "to_email": "recipient@example.com"
    }
    ```
*   **Response**:

    ```json
    {
      "ok": true,
      "result": "Bot transferred successfully"
    }
    ```

**Clone Bot**

* **Endpoint**: `POST /v2/bots/{botid}/clone-bot`
* **Description**: Creates a copy of the bot with optional new token
* **URL Parameters**:
  * `botid`: The unique identifier of the bot
*   **Request Body**:

    ```json
    {
      "new_token": "1234567890:CLONEDAAAAAAAAAAAAAAAAAAAAAAA"
    }
    ```
*   **Response**:

    ```json
    {
      "ok": true,
      "result": {
        "botid": "new_bot_id",
        "message": "Bot cloned successfully"
      }
    }
    ```

### Command Name Encoding

For endpoints that require a command name in the URL path, the command name must be Base64 encoded to handle special characters safely.

#### Encoding Process

1. **Original Command**: `/start`
2. **URL-Safe Base64 Encoding**: `L3N0YXJ0`
3. **Final URL**: `/v2/bots/{botid}/commands/L3N0YXJ0`

#### Examples

| Original Command | Base64 Encoded     |
| ---------------- | ------------------ |
| `/start`         | `L3N0YXJ0`         |
| `/help`          | `L2hlbHA=`         |
| `/settings`      | `L3NldHRpbmdz`     |
| `hello_world`    | `aGVsbG9fd29ybGQ=` |
| `user info`      | `dXNlciBpbmZv`     |

#### Code Examples

**JavaScript/Node.js**

```javascript
function encodeCommand(command) {
    return Buffer.from(command, 'utf8').toString('base64');
}

function decodeCommand(encoded) {
    return Buffer.from(encoded, 'base64').toString('utf8');
}

// Usage
const encoded = encodeCommand('/start'); // "L3N0YXJ0"
const decoded = decodeCommand('L3N0YXJ0'); // "/start"
```

**Python**

```python
import base64

def encode_command(command):
    return base64.b64encode(command.encode('utf-8')).decode('ascii')

def decode_command(encoded):
    return base64.b64decode(encoded.encode('ascii')).decode('utf-8')

# Usage
encoded = encode_command('/start')  # "L3N0YXJ0"
decoded = decode_command('L3N0YXJ0')  # "/start"
```

**cURL Examples**

```bash
# Get a command (command name: /start)
curl -X GET "https://api.telebotcreator.com/v2/bots/mybotid/commands/L3N0YXJ0" \
  -H "Authorization: Bearer your_api_key_here"

# Update a command
curl -X PUT "https://api.telebotcreator.com/v2/bots/mybotid/commands/L3N0YXJ0" \
  -H "Authorization: Bearer your_api_key_here" \
  -H "Content-Type: application/json" \
  -d '{"code": "bot.reply_to(message, \"Hello from API!\")"}'

# Delete a command
curl -X DELETE "https://api.telebotcreator.com/v2/bots/mybotid/commands/L3N0YXJ0" \
  -H "Authorization: Bearer your_api_key_here"
```

### Authentication Examples

#### Using Bearer Token in Header

```bash
curl -X GET "https://api.telebotcreator.com/v2/bots/mybotid/commands" \
  -H "Authorization: Bearer your_api_key_here"
```

#### Using API Key as Query Parameter

```bash
curl -X GET "https://api.telebotcreator.com/v2/bots/mybotid/commands?api_key=your_api_key_here"
```

#### Using API Key in JSON Body

```bash
curl -X POST "https://api.telebotcreator.com/v2/bots/mybotid/commands" \
  -H "Content-Type: application/json" \
  -d '{
    "api_key": "your_api_key_here",
    "command": "test",
    "code": "bot.reply_to(message, \"Test command\")"
  }'
```

### Error Responses

#### Authentication Errors

```json
{
  "ok": false,
  "result": "Authentication required"
}
```

#### Invalid API Key

```json
{
  "ok": false,
  "result": "Invalid API key"
}
```

#### Bot Not Found

```json
{
  "ok": false,
  "result": "Bot not found or not owned by you"
}
```

#### Command Not Found

```json
{
  "ok": false,
  "result": "Command not found"
}
```

#### Validation Errors

```json
{
  "ok": false,
  "result": "Invalid bot token format"
}
```

### Rate Limiting

The API implements rate limiting to prevent abuse:

* **Rate Limit**: 60 requests per minute per IP
* **Headers**: Rate limit information is provided in response headers
  * `X-RateLimit-Limit`: Maximum requests per window
  * `X-RateLimit-Remaining`: Remaining requests in current window
  * `X-RateLimit-Reset`: Time when the rate limit resets

### Best Practices

1. **Security**
   * Store API keys securely and never expose them in client-side code
   * Use HTTPS for all API requests
   * Rotate API keys regularly
2. **Error Handling**
   * Always check the `ok` field in responses
   * Implement proper retry logic for transient errors
   * Log errors for debugging purposes
3. **Performance**
   * Respect rate limits to avoid being temporarily blocked
   * Use batch operations when available
   * Cache responses when appropriate
4. **Command Encoding**
   * Always Base64 encode command names for URL paths
   * Use URL-safe Base64 encoding
   * Handle encoding/decoding errors gracefully

### Support

For additional support or questions about the API:

* Check the error messages for specific guidance
* Review this documentation for proper usage
* Contact support through the official channels

***

_Last updated: 2025-07-20_
