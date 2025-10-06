# 🤖 AI-Powered Discord Moderation Bot

A sophisticated 3-stage AI moderation system for Discord servers that uses multiple AI layers to analyze, verify, and execute moderation actions with minimal false positives.

## 🌟 Features

### Core Functionality
- **3-Stage AI Pipeline**: Multiple AI agents work together to ensure accurate moderation
  - **AI #1**: Fast initial screening for potential violations
  - **AI #2**: Deep context analysis with conversation history
  - **AI #3**: Final verification with web search capabilities
- **Configurable Sensitivity**: Four preset modes (lenient, balanced, strict, very_strict)
- **Smart Context Analysis**: Analyzes up to 200 messages of conversation history
- **Warning System**: Tracks user violations and warning history
- **Full Punishment Suite**: warn, timeout (1h/24h), kick, temporary ban, permanent ban

### Admin Controls
- Real-time AI behavior customization
- Sensitivity preset switching
- Individual AI agent configuration
- Warning management (view/clear)
- Comprehensive testing commands

### Safety Features
- Multi-stage verification to prevent false positives
- Context-aware decision making
- Humor and sarcasm detection
- Reply chain analysis
- User warning history consideration

## 📋 Prerequisites

- C++17 or higher
- [D++ (DPP) library](https://github.com/brainboxdotcc/DPP) - Discord API library
- [CPR library](https://github.com/libcpr/cpr) - HTTP requests
- [nlohmann/json](https://github.com/nlohmann/json) - JSON parsing
- CMake (for building)
- A compatible AI API endpoint (OpenAI-compatible REST API)

## 🚀 Installation

### 1. Clone the Repository
```bash
git clone https://github.com/jokukiller/discord-ai-moderation-bot.git
cd discord-ai-moderation-bot
```

### 2. Install Dependencies

#### Ubuntu/Debian
```bash
sudo apt-get update
sudo apt-get install build-essential cmake libssl-dev libcurl4-openssl-dev
```

#### Install D++ Library
```bash
git clone https://github.com/brainboxdotcc/DPP.git
cd DPP
mkdir build && cd build
cmake ..
make -j$(nproc)
sudo make install
```

#### Install CPR Library
```bash
git clone https://github.com/libcpr/cpr.git
cd cpr
mkdir build && cd build
cmake .. -DCPR_USE_SYSTEM_CURL=ON
make -j$(nproc)
sudo make install
```

#### Install nlohmann/json
```bash
# Header-only library - can be installed via package manager
sudo apt-get install nlohmann-json3-dev
```

### 3. Configure the Bot

Open `discord_moderation_system.cpp` and update the following constants:

```cpp
const std::string BOT_TOKEN = "YOUR_DISCORD_BOT_TOKEN_HERE";
const std::string API_KEY = "YOUR_API_KEY_HERE";
const std::string LOG_CHANNEL_ID = "YOUR_LOG_CHANNEL_ID";
const std::unordered_set<std::string> ADMIN_ROLES = {
    "admin", "moderator", "owner"  // Replace with your server's role names (lowercase)
};
const std::string API_ENDPOINT = "YOUR_REST_API_ENDPOINT_HERE";
```

#### Getting Your Discord Bot Token
1. Go to [Discord Developer Portal](https://discord.com/developers/applications)
2. Create a New Application
3. Go to "Bot" section → Click "Add Bot"
4. Under "Token", click "Reset Token" and copy it
5. Enable "MESSAGE CONTENT INTENT" under "Privileged Gateway Intents"

#### Getting Your Log Channel ID
1. Enable Developer Mode in Discord (Settings → Advanced → Developer Mode)
2. Right-click on your desired log channel → "Copy ID"

#### Supported API Endpoints
Any OpenAI-compatible REST API endpoint works:
- OpenAI API
- xAI (Grok)
- OpenRouter
- Local LLMs (via LM Studio, Ollama with OpenAI compatibility)
- Other compatible providers

### 4. Build the Bot

```bash
mkdir build && cd build
cmake ..
make
```

### 5. Run the Bot

```bash
./discord_moderation_bot
```

## 📖 Configuration

### Sensitivity Presets

| Preset | Description | Use Case |
|--------|-------------|----------|
| **lenient** (default) | Minimal false positives, high tolerance for humor/sarcasm | Community-focused servers, casual environments |
| **balanced** | Moderate enforcement, fair tolerance | General-purpose servers |
| **strict** | Low tolerance, strong enforcement | Professional servers, strict communities |
| **very_strict** | Zero tolerance, maximum enforcement | High-security environments |

### Configurable Parameters

#### In Code:
```cpp
// Cache size (line ~95)
const size_t MAX_CACHE_SIZE = 500;  // Messages stored in memory

// Context range (line ~104)
int context_range = 200)  // Messages analyzed for context (default: 5 in actual calls)

// AI Max Tokens (lines ~350, ~520, ~650)
payload["max_tokens"] = 5;    // AI #1 (screening)
payload["max_tokens"] = 500;  // AI #2 (analysis)
payload["max_tokens"] = 50;   // AI #3 (verification)
```

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
- Fast, lightweight scanning
- Filters obvious safe messages
- Flags potential violations for deeper analysis
- Low temperature (0.0) for consistent results

**AI #2 - Context Analyzer**
- Analyzes conversation context
- Considers user warning history
- Understands humor, sarcasm, and intent
- Recommends specific punishment if needed

**AI #3 - Final Verifier**
- Web search capabilities for fact-checking
- Verifies AI #2's recommendation
- Checks current meme culture and trends
- Final decision maker (APPROVE/DENY)

## 🛡️ Punishment Types

| Type | Duration | Description |
|------|----------|-------------|
| `warn` | N/A | Warning DM sent to user, logged in system |
| `timeout_1h` | 1 hour | User cannot send messages for 1 hour |
| `timeout_24h` | 24 hours | User cannot send messages for 24 hours |
| `kick` | N/A | User removed from server (can rejoin) |
| `ban_temp` | Manual | Temporary ban (requires manual unban) |
| `ban_perm` | Permanent | Permanent ban from server |

## 📝 Example Usage

### Setting Up for Your Server

1. **Initial Setup** (Admin only)
```
!ai_tune lenient
!ai_settings
```

2. **Customize Behavior** (Optional)
```
!ai_behavior 1 You are a screening AI for a gaming server. Be lenient with gaming terminology and competitive banter.
```

3. **Test the System**
```
!test_full This is a test message with some questionable content
```

4. **Monitor Logs**
- Check your designated log channel for all moderation actions
- Review console output for detailed AI decision logs

### Managing Warnings

```
!warnings @username
!clear_warnings @username  (Admin only)
```

## 🔒 Security & Privacy

- **No Data Persistence**: All messages cached in memory only (cleared on restart)
- **Minimal Data Sent**: Only necessary context sent to AI for analysis
- **Admin-Only Controls**: Sensitive commands require admin role
- **Audit Logging**: All punishments logged with full context
- **API Key Security**: Keep your API keys private and never commit them to version control

## 🐛 Troubleshooting

### Bot Won't Start
- ✅ Check that all configuration constants are set (not "YOUR_*_HERE")
- ✅ Verify bot token is valid
- ✅ Ensure "Message Content Intent" is enabled in Discord Developer Portal
- ✅ Check that bot has proper permissions in your server

### Bot Not Responding to Commands
- ✅ Verify bot is online in your server
- ✅ Check that your role is in the `ADMIN_ROLES` set (for admin commands)
- ✅ Ensure bot has "Read Messages" and "Send Messages" permissions

### AI Not Working
- ✅ Verify API endpoint is correct and accessible
- ✅ Check API key is valid and has credits
- ✅ Review console logs for API error messages
- ✅ Test with `!test_ai1` to isolate the issue

### High API Costs
- Lower context range from 200 to 5-10 (line ~790)
- Reduce max_tokens for AI #2 and AI #3
- Use cheaper models (adjust model names in code)

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

### Development Setup
1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## ⚠️ Disclaimer

This bot uses AI for moderation decisions. While the 3-stage pipeline minimizes false positives, no AI system is perfect. Always:
- Monitor the bot's decisions regularly
- Review logs in your log channel
- Adjust sensitivity settings based on your community
- Have human moderators as backup

## 🙏 Acknowledgments

- [D++ (DPP)](https://github.com/brainboxdotcc/DPP) - Excellent Discord API library
- [CPR](https://github.com/libcpr/cpr) - Simple HTTP library
- [nlohmann/json](https://github.com/nlohmann/json) - Modern JSON library
- AI providers for making powerful moderation possible

## 📧 Support

- Create an issue for bug reports
- Discussions for feature requests
- Pull requests are welcome!

---

**Built with ❤️ by [jokukiller](https://github.com/jokukiller)**

*Last Updated: 2025-10-06*
