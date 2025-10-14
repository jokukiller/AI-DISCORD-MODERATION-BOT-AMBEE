# 🤖 AI-Powered Discord Moderation Bot - AMBEE

A sophisticated 3-stage AI moderation system for Discord servers that uses multiple AI layers to analyze, verify, and execute moderation actions with minimal false positives.

## ⚠️ License Notice

**This software is SOURCE AVAILABLE, not Open Source.**

- ✅ You may **view and learn** from the code
- ✅ You may **contribute** via pull requests
- ❌ You may **NOT run, deploy, or host** this software yourself
- ❌ **NO commercial use** allowed

See [LICENSE](LICENSE) for full terms.

### 🤖 Want to use AMBEE?
**You can add the official hosted bot to your server FOR FREE:**

👉 **[Invite AMBEE from Top.gg](https://top.gg/bot/1418185634195050496)**

*The code is public for educational purposes and contributions only. To use the bot, please invite the official instance above.*

---

## 🌟 Features

Core Features
Three-Stage AI Moderation Pipeline

AI #1: Initial message screening (FLAG/PASS)

AI #2: Contextual analysis and violation assessment

AI #3: Verification with web search capabilities

Complete Context Awareness

Analyzes all messages within a 30-minute window around each message

Cross-channel context tracking for severe violations

Edit and deletion tracking with full audit history

Advanced Content Analysis

Text moderation with nuanced understanding of context, humor, and sarcasm

Image analysis via Grok Vision for visual content violations

Media attachment processing (images, videos, files)

Multi-Server Architecture

Isolated configurations per server

Automatic log channel creation (#ambee-logs)

Server-specific rules and AI behavior customization

Setup & Configuration
Essential Commands:

!help - View all available commands and setup options

!server_rules - Configure your server's specific rules that the AI will enforce

!set_sensitivity - Adjust moderation strictness (lenient/balanced/strict/very_strict)

!log_channel - Manage moderation logs

Recommended Setup:

Invite the bot to your server

Use !server_rules to define your community guidelines

Adjust sensitivity with !set_sensitivity as needed

Review !help for additional customization options

Administrative Controls
Custom server rule integration

Real-time moderation analytics

Warning system with user history

Per-server AI behavior tuning

Technical Specifications
Real-time message processing

MongoDB/Cosmos DB backend

Unlimited contextual message analysis within active time windows

For support and documentation: https://discord.gg/zAA9XbWc2s

## 📋 Prerequisites

- **C++17 or higher**
- **CMake 3.15+**
- **[D++ (DPP) library](https://github.com/brainboxdotcc/DPP)** - Discord API library
- **[CPR library](https://github.com/libcpr/cpr)** - HTTP requests
- **[nlohmann/json](https://github.com/nlohmann/json)** - JSON parsing
- **OpenSSL**
- **libcurl**
- A compatible AI API endpoint (OpenAI-compatible REST API)

---

## 🚀 Installation (For Contributors Only)

⚠️ **Note:** These instructions are for developers who want to contribute to the project.
**End users should [invite the official bot](https://top.gg/bot/1418185634195050496) instead.**

### Windows Installation

#### Step 1: Install Build Tools

1. **Install Visual Studio 2019 or newer**
   - Download from [Visual Studio](https://visualstudio.microsoft.com/)
   - During installation, select "Desktop development with C++"
   - Make sure to include CMake tools

2. **Install vcpkg (Package Manager)**
   ```cmd
   cd C:\
   git clone https://github.com/Microsoft/vcpkg.git
   cd vcpkg
   .\bootstrap-vcpkg.bat
   .\vcpkg integrate install
   ```

#### Step 2: Install Dependencies via vcpkg

```cmd
cd C:\vcpkg
.\vcpkg install dpp:x64-windows
.\vcpkg install cpr:x64-windows
.\vcpkg install nlohmann-json:x64-windows
.\vcpkg install openssl:x64-windows
.\vcpkg install curl:x64-windows
```

**Note:** This will take 15-30 minutes. Go grab a coffee! ☕

#### Step 3: Clone the Repository

```cmd
cd C:\Projects
git clone https://github.com/jokukiller/AI-DISCORD-MODERATION-BOT-AMBEE.git
cd AI-DISCORD-MODERATION-BOT-AMBEE
```

#### Step 4: Configure CMake with vcpkg

Create a `CMakeLists.txt` if you're using the provided one, or update it:

```cmake
cmake_minimum_required(VERSION 3.15)
project(AMBEE_moderation_bot)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Find packages
find_package(dpp CONFIG REQUIRED)
find_package(cpr CONFIG REQUIRED)
find_package(nlohmann_json CONFIG REQUIRED)

# Add executable
add_executable(AMBEE_moderation_bot main.cpp)

# Link libraries
target_link_libraries(AMBEE_moderation_bot PRIVATE
    dpp::dpp
    cpr::cpr
    nlohmann_json::nlohmann_json
)
```

#### Step 5: Build the Project

**Using Visual Studio:**
1. Open the project folder in Visual Studio
2. Visual Studio will auto-detect CMakeLists.txt
3. Select "Build" → "Build All"

**Using Command Line:**
```cmd
mkdir build
cd build
cmake .. -DCMAKE_TOOLCHAIN_FILE=C:/vcpkg/scripts/buildsystems/vcpkg.cmake
cmake --build . --config Release
```

#### Step 6: Configure the Bot

Open `main.cpp` and update these constants:

```cpp
const std::string BOT_TOKEN = "YOUR_DISCORD_BOT_TOKEN_HERE";
const std::string API_KEY = "YOUR_API_KEY_HERE";
const std::string LOG_CHANNEL_ID = "YOUR_LOG_CHANNEL_ID";
const std::unordered_set<std::string> ADMIN_ROLES = {
    "admin", "moderator", "owner"  // Replace with your server's role names (lowercase)
};
const std::string API_ENDPOINT = "YOUR_REST_API_ENDPOINT_HERE";
```

#### Step 7: Run the Bot

```cmd
cd build\Release
.\AMBEE_moderation_bot.exe
```

---

### Linux/Ubuntu Installation

#### Step 1: Install Build Tools

```bash
sudo apt-get update
sudo apt-get install build-essential cmake git libssl-dev libcurl4-openssl-dev
```

#### Step 2: Install D++ Library

```bash
cd ~
git clone https://github.com/brainboxdotcc/DPP.git
cd DPP
mkdir build && cd build
cmake ..
make -j$(nproc)
sudo make install
sudo ldconfig
```

#### Step 3: Install CPR Library

```bash
cd ~
git clone https://github.com/libcpr/cpr.git
cd cpr
mkdir build && cd build
cmake .. -DCPR_USE_SYSTEM_CURL=ON
make -j$(nproc)
sudo make install
sudo ldconfig
```

#### Step 4: Install nlohmann/json

```bash
sudo apt-get install nlohmann-json3-dev
```

#### Step 5: Clone the Repository

```bash
cd ~
git clone https://github.com/jokukiller/AI-DISCORD-MODERATION-BOT-AMBEE.git
cd AI-DISCORD-MODERATION-BOT-AMBEE
```

#### Step 6: Configure the Bot

Open `main.cpp` and update the configuration constants (same as Windows Step 6).

#### Step 7: Build the Project

```bash
mkdir build && cd build
cmake ..
make -j$(nproc)
```

#### Step 8: Run the Bot

```bash
./AMBEE_moderation_bot
```

---

### macOS Installation

#### Step 1: Install Homebrew (if not installed)

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

#### Step 2: Install Dependencies

```bash
brew install cmake openssl curl nlohmann-json
```

#### Step 3: Install D++ Library

```bash
cd ~
git clone https://github.com/brainboxdotcc/DPP.git
cd DPP
mkdir build && cd build
cmake ..
make -j$(sysctl -n hw.ncpu)
sudo make install
```

#### Step 4: Install CPR Library

```bash
cd ~
git clone https://github.com/libcpr/cpr.git
cd cpr
mkdir build && cd build
cmake .. -DCPR_USE_SYSTEM_CURL=ON
make -j$(sysctl -n hw.ncpu)
sudo make install
```

#### Step 5: Clone and Build (same as Linux Steps 5-8)

---

## 🔧 Configuration

### Getting Your Discord Bot Token

1. Go to [Discord Developer Portal](https://discord.com/developers/applications)
2. Click "New Application" → Give it a name
3. Go to "Bot" section → Click "Add Bot"
4. Under "Token", click "Reset Token" and copy it
5. **Enable these Privileged Gateway Intents:**
   - ✅ **MESSAGE CONTENT INTENT** (Required!)
   - ✅ Server Members Intent (Recommended)
   - ✅ Presence Intent (Optional)

### Getting Your Log Channel ID

1. Enable Developer Mode in Discord:
   - User Settings → Advanced → Developer Mode (toggle ON)
2. Right-click on your desired log channel → "Copy ID"
3. Paste this ID into `LOG_CHANNEL_ID` in `main.cpp`

### Supported AI API Endpoints

Any OpenAI-compatible REST API endpoint works:
- **OpenAI API** - `https://api.openai.com/v1/chat/completions`
- **xAI (Grok)** - `https://api.x.ai/v1/chat/completions`
- **OpenRouter** - `https://openrouter.ai/api/v1/chat/completions`
- **Local LLMs** - Via LM Studio, Ollama with OpenAI compatibility
- Other compatible providers

**Example for xAI/Grok:**
```cpp
const std::string API_ENDPOINT = "https://api.x.ai/v1/chat/completions";
const std::string API_KEY = "xai-your-key-here";
```

In `main.cpp`, update the model names:
```cpp
payload["model"] = "grok-beta";  // For AI #1
payload["model"] = "grok-beta";  // For AI #2
payload["model"] = "grok-beta";  // For AI #3
```

---

## 📖 Bot Configuration

### Sensitivity Presets

| Preset | Description | Use Case |
|--------|-------------|----------|
| **lenient** (default) | Minimal false positives, high tolerance for humor/sarcasm | Community-focused servers, casual environments |
| **balanced** | Moderate enforcement, fair tolerance | General-purpose servers |
| **strict** | Low tolerance, strong enforcement | Professional servers, strict communities |
| **very_strict** | Zero tolerance, maximum enforcement | High-security environments |

### Configurable Parameters in Code

```cpp
// Message cache size (line ~95)
const size_t MAX_CACHE_SIZE = 500;  // Messages stored in memory

// Context range for analysis (line ~104)
int context_range = 200  // Maximum messages to analyze (default: 5 in practice)

// AI Token limits (adjust based on your API costs)
// AI #1 screening (line ~350)
payload["max_tokens"] = 5;

// AI #2 analysis (line ~520)
payload["max_tokens"] = 500;

// AI #3 verification (line ~650)
payload["max_tokens"] = 50;
```

---

## 🎮 Commands

### User Commands
| Command | Description |
|---------|-------------|
| `!warnings <user_id>` | View warning history for a user |
| `!status` | Show bot status and available commands |
| `!ai_behaviors` | View current AI behavior configurations |

### Admin Commands
| Command | Description |
|---------|-------------|
| `!ai_tune <preset>` | Apply sensitivity preset (lenient/balanced/strict/very_strict) |
| `!ai_settings` | View current AI configuration |
| `!ai_behavior <1-3> <description>` | Update individual AI agent behavior |
| `!ai_reset_behavior <1-3>` | Reset specific AI agent to default |
| `!ai_reset` | Reset entire AI configuration to default |
| `!clear_warnings <user_id>` | Clear all warnings for a user |

### Testing Commands
| Command | Description |
|---------|-------------|
| `!test_ai1 <message>` | Test AI #1 screening only |
| `!test_ai2 <message>` | Test AI #2 analysis only |
| `!test_ai3 <message>` | Test AI #3 verification only |
| `!test_full <message>` | Test complete 3-stage pipeline |

---

## 🔧 How It Works

### 3-Stage Moderation Pipeline

```
Message Received
    ↓
┌─────────────────────┐
│   AI #1: Screening  │ ← Fast scan (FLAG/PASS)
└─────────────────────┘
    ↓ (if FLAGGED)
┌─────────────────────┐
│  AI #2: Analysis    │ ← Context analysis (PUNISH/DISMISS)
└─────────────────────┘
    ↓ (if PUNISH)
┌─────────────────────┐
│ AI #3: Verification │ ← Web search & verify (APPROVE/DENY)
└─────────────────────┘
    ↓ (if APPROVED)
Execute Punishment
```

### AI Agent Roles

**AI #1 - Initial Screener**
- Fast, lightweight scanning (< 1 second)
- Filters obvious safe messages (99% of traffic)
- Flags potential violations for deeper analysis
- Low temperature (0.0) for consistent results
- Only outputs: `FLAG` or `PASS`

**AI #2 - Context Analyzer**
- Analyzes full conversation context
- Considers user warning history
- Understands humor, sarcasm, and intent
- Recommends specific punishment if needed
- Outputs: Decision, Punishment Type, Severity, Reasoning

**AI #3 - Final Verifier**
- Web search capabilities for fact-checking
- Verifies AI #2's recommendation
- Checks current meme culture and trends
- Ensures punishment matches severity
- Final decision maker: `APPROVE` or `DENY`

---

## 🛡️ Punishment Types

| Type | Duration | Description |
|------|----------|-------------|
| `warn` | N/A | Warning DM sent to user, logged in system |
| `timeout_1h` | 1 hour | User cannot send messages for 1 hour |
| `timeout_24h` | 24 hours | User cannot send messages for 24 hours |
| `kick` | N/A | User removed from server (can rejoin) |
| `ban_temp` | Manual unban | Temporary ban (requires manual unban) |
| `ban_perm` | Permanent | Permanent ban from server |

---

## 📝 Example Usage

### Setting Up for Your Server (Admin)

1. **Test the bot is responding:**
```
!status
```

2. **Set initial sensitivity:**
```
!ai_tune lenient
```

3. **View current configuration:**
```
!ai_settings
```

4. **Customize AI behavior (Optional):**
```
!ai_behavior 1 You are a screening AI for a gaming server. Be lenient with gaming terminology and competitive banter.
```

5. **Test the system:**
```
!test_full This is a test message to see how the AI responds
```

6. **Monitor your log channel** for all moderation actions

### Managing User Warnings

**View warnings:**
```
!warnings @username
!warnings 123456789012345678
```

**Clear warnings (Admin only):**
```
!clear_warnings @username
```

---

## 🔒 Security & Privacy

- ✅ **No Data Persistence**: All messages cached in memory only (cleared on restart)
- ✅ **Minimal Data Sent**: Only necessary context sent to AI for analysis
- ✅ **Admin-Only Controls**: Sensitive commands require admin role
- ✅ **Audit Logging**: All punishments logged with full context
- ✅ **API Key Security**: Never commit API keys to version control
- ✅ **No Message Storage**: No database, no permanent message logs

---

## 🐛 Troubleshooting

### Windows-Specific Issues

**"DLL not found" errors:**
```cmd
# Copy required DLLs to your build directory
copy C:\vcpkg\installed\x64-windows\bin\*.dll build\Release\
```

**vcpkg integration not working:**
```cmd
cd C:\vcpkg
.\vcpkg integrate install
# Restart Visual Studio
```

**CMake can't find packages:**
```cmd
# Always specify vcpkg toolchain
cmake .. -DCMAKE_TOOLCHAIN_FILE=C:/vcpkg/scripts/buildsystems/vcpkg.cmake
```

### Linux-Specific Issues

**"libdpp.so not found":**
```bash
sudo ldconfig
```

**Permission denied when running:**
```bash
chmod +x AMBEE_moderation_bot
./AMBEE_moderation_bot
```

### General Issues

**Bot Won't Start:**
- ✅ Check all config constants are set (not `"YOUR_*_HERE"`)
- ✅ Verify bot token is valid
- ✅ Ensure "Message Content Intent" is enabled in Discord Developer Portal
- ✅ Check bot has proper permissions in server

**Bot Not Responding to Commands:**
- ✅ Verify bot is online in your server
- ✅ Check your role is in `ADMIN_ROLES` (for admin commands)
- ✅ Ensure bot has "Read Messages" and "Send Messages" permissions
- ✅ Check console for error messages

**AI Not Working:**
- ✅ Verify API endpoint is correct and accessible
- ✅ Check API key is valid and has credits
- ✅ Review console logs for API error messages
- ✅ Test with `!test_ai1 hello` to isolate the issue
- ✅ Ensure your firewall allows outbound HTTPS connections

**High API Costs:**
- Lower context range from 200 to 5-10
- Reduce `max_tokens` for AI #2 and AI #3
- Use cheaper models (e.g., `grok-beta` instead of `gpt-4`)
- Increase AI #1 temperature slightly to be more lenient (fewer flags)

---

## 🤝 Contributing

Contributions are welcome! Here's how you can help:

### How to Contribute

1. **Fork the repository**
2. **Clone your fork:**
   ```bash
   git clone https://github.com/YOUR_USERNAME/AI-DISCORD-MODERATION-BOT-AMBEE.git
   ```
3. **Create a feature branch:**
   ```bash
   git checkout -b feature/AmazingFeature
   ```
4. **Make your changes and test thoroughly**
5. **Commit your changes:**
   ```bash
   git commit -m "Add some AmazingFeature"
   ```
6. **Push to your fork:**
   ```bash
   git push origin feature/AmazingFeature
   ```
7. **Open a Pull Request** on GitHub

### Contribution Guidelines

- ✅ Test your changes thoroughly
- ✅ Follow existing code style
- ✅ Add comments for complex logic
- ✅ Update documentation if needed
- ✅ Keep PRs focused on a single feature/fix

### Areas We Need Help With

- 🔧 Performance optimizations
- 🌐 Multi-language support
- 📊 Advanced analytics/statistics
- 🎨 Better logging formats
- 🐛 Bug fixes
- 📝 Documentation improvements

---

## 📄 License

This project is **Source Available** under a custom license - see the [LICENSE](LICENSE) file for details.

**TL;DR:**
- ✅ You can view and learn from the code
- ✅ You can contribute via pull requests
- ❌ You **cannot** run, deploy, or host this software yourself
- ❌ **NO commercial use** allowed

**To use AMBEE completely FOR FREE, [invite the official hosted bot](https://top.gg/bot/1418185634195050496) instead.**

---

## ⚠️ Disclaimer

This bot uses AI for moderation decisions. While the 3-stage pipeline minimizes false positives, no AI system is perfect.

**Always:**
- 👀 Monitor the bot's decisions regularly
- 📋 Review logs in your log channel
- ⚙️ Adjust sensitivity settings based on your community

**The bot creator is not responsible for:**
- False positives or false negatives
- Decisions made by the AI
- Server disruptions
- API costs incurred by disobeying the licence and hosting your own local instance

---

## 🙏 Acknowledgments

- **[D++ (DPP)](https://github.com/brainboxdotcc/DPP)** - Excellent Discord API library for C++
- **[CPR](https://github.com/libcpr/cpr)** - Simple and elegant HTTP library
- **[nlohmann/json](https://github.com/nlohmann/json)** - Modern JSON library for C++
- **AI Providers** - For making powerful AI moderation possible
- **Discord Community** - For testing and feedback

---

## 📧 Support

**For the Official Bot:**
- 🤖 [Invite AMBEE](https://top.gg/bot/1418185634195050496)
- 💬 Support server: *(https://discord.gg/89rFga73cC)*

**For Development/Contributions:**
- 🐛 [Report bugs via GitHub Issues](https://github.com/jokukiller/AI-DISCORD-MODERATION-BOT-AMBEE/issues)
- 💡 [Feature requests via Discussions](https://github.com/jokukiller/AI-DISCORD-MODERATION-BOT-AMBEE/discussions)
- 🔧 Pull requests are welcome!

---

## 📊 Statistics

- ⚡ **Response Time**: < 2 seconds average
- 🎯 **Accuracy**: 95%+ (with 3-stage pipeline)
- 💰 **API Cost**: COMPLETELY FREE IF YOU USE THE OFFICIAL HOSTED VERSION. 
- 🔄 **Uptime**: 99.9% (official hosted version)

---

**Built with ❤️ by [jokukiller](https://github.com/jokukiller)**

*Last Updated: 2025-10-06*

---

**Want to see a feature?** Open a discussion on GitHub or join the support discord server (https://discord.gg/89rFga73cC) !
