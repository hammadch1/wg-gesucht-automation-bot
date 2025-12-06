# wg-gesucht-automation-bot
🤖 Automate your WG-Gesucht apartment search - automatically monitors listings and sends personalized messages to new matches. Powered by Python, Selenium, and OpenAI.



Reviewing the codebase to understand the bot's functionality, then drafting the documentation.


[7 tools called]


Exploring the `src` directory to understand the full functionality:


[7 tools called]


Drafting a README that's specific and easy to follow:


[1 tool called]


Here's a README that's specific and easy to follow:

```markdown
# WG-Gesucht Bot 🤖

*Let's face it, looking for a new WG (shared apartment) is a pain. You spend hours refreshing pages, writing the same message over and over, and still miss the best listings. This bot automates all of that for you.*

## What This Bot Does

This Python bot automatically monitors [WG-Gesucht.de](https://www.wg-gesucht.de) (Germany's largest shared apartment platform) and sends personalized messages to new listings that match your criteria. Here's what it does:

- **Monitors listings 24/7**: Checks for new listings every 60 seconds
- **Smart filtering**: Only contacts listings that meet your minimum rental period and custom conditions
- **Avoids duplicates**: Never sends the same message twice to the same listing
- **Personalized messages**: Uses OpenAI GPT to customize your message based on each listing's description
- **Auto-attach documents**: Optionally attaches your SCHUFA credit check document automatically
- **Handles popups**: Automatically dismisses cookie banners, security notices, and other popups
- **Auto-restart**: If something goes wrong, it automatically restarts after 10 seconds
- **Detailed logging**: Everything is logged so you can see exactly what's happening

## Features

### 🎯 Smart Filtering
- **Minimum rental period**: Only contact listings available for at least X months (e.g., 6 months minimum)
- **Custom conditions**: Write Python expressions to filter listings (e.g., skip listings with certain names)
- **Duplicate prevention**: Tracks all contacted listings to avoid sending multiple messages

### 🤖 AI-Powered Personalization
- **GPT integration**: If you provide an OpenAI API key, the bot will read each listing and personalize your message
- **Magic word detection**: Automatically includes any "magic words" that listings ask for (like "write 'banana' in your message")
- **Context-aware**: References specific details from each listing to make your message stand out

### 📎 Document Attachment
- **SCHUFA attachment**: Automatically attaches your credit check document if enabled
- **One-click setup**: Just place `SCHUFA-BonitaetsCheck.pdf` in the project folder

### 🔄 Reliability
- **Auto-restart**: Automatically restarts if any error occurs
- **Error handling**: Gracefully handles reCAPTCHAs, deactivated listings, and network issues
- **Headless mode**: Can run without a display (perfect for servers)

## Prerequisites

Before you start, make sure you have:

1. **Python 3.7+** installed on your system
2. **Firefox browser** installed
3. **A WG-Gesucht account** (free to create at wg-gesucht.de)
4. **(Optional) OpenAI API key** for message personalization (get one at platform.openai.com)

## Installation

### For macOS

1. **Clone or download this repository**
   ```bash
   cd wg-gesucht-bot-main
   ```

2. **Create a virtual environment**
   ```bash
   python3 -m venv env
   source env/bin/activate
   ```

3. **Install Python dependencies**
   ```bash
   pip install -r requirements.txt
   playwright install
   ```

4. **Install Firefox** (if not already installed)
   - Download from [mozilla.org/firefox](https://www.mozilla.org/firefox/)
   - Or use Homebrew: `brew install firefox`

5. **Install geckodriver** (Firefox automation driver)
   ```bash
   brew install geckodriver
   ```

### For Windows

1. **Clone or download this repository**
   ```cmd
   cd wg-gesucht-bot-main
   ```

2. **Create a virtual environment**
   ```cmd
   python -m venv env
   env\Scripts\activate
   ```

3. **Install Python dependencies**
   ```cmd
   pip install -r requirements.txt
   playwright install
   ```

4. **Install Firefox** (if not already installed)
   - Download from [mozilla.org/firefox](https://www.mozilla.org/firefox/windows/)

5. **Install geckodriver**
   - Download from [GitHub releases](https://github.com/mozilla/geckodriver/releases)
   - Extract and add to your system PATH, or specify the path in `config.yaml`

### For Linux (Ubuntu/Debian)

1. **Clone or download this repository**
   ```bash
   cd wg-gesucht-bot-main
   ```

2. **Create a virtual environment**
   ```bash
   python3 -m venv env
   source env/bin/activate
   ```

3. **Install Python dependencies**
   ```bash
   pip install -r requirements.txt
   playwright install
   playwright install-deps
   ```

4. **Install Firefox and geckodriver**
   ```bash
   # Remove snap version (doesn't work with Selenium)
   sudo snap remove firefox
   
   # Add Mozilla PPA
   sudo add-apt-repository ppa:mozillateam/ppa
   
   # Configure automatic updates
   echo 'Package: *
   Pin: release o=LP-PPA-mozillateam
   Pin-Priority: 1001' | sudo tee /etc/apt/preferences.d/mozilla-firefox
   
   echo 'Unattended-Upgrade::Allowed-Origins:: "LP-PPA-mozillateam:${distro_codename}";' | sudo tee -a /etc/apt/preferences.d/mozilla-firefox
   
   # Install Firefox
   sudo apt update
   sudo apt install firefox firefox-geckodriver
   ```

5. **Install additional dependencies** (if needed)
   ```bash
   sudo apt install libxml2 libxslt1.1
   ```

## Configuration

### Step 1: Create Your Configuration File

1. Copy `config.yaml` (it should already exist, but if not, create it)
2. Open `config.yaml` in a text editor

### Step 2: Configure Your Settings

Here's what each setting means:

```yaml
# The file containing your message template
message_file: "message.txt"

# Your WG-Gesucht login credentials
wg_gesucht_credentials:
  email: "your-email@example.com"      # Your WG-Gesucht email
  password: "your-password"             # Your WG-Gesucht password

# The filtered search URL from WG-Gesucht
url: "https://www.wg-gesucht.de/wg-zimmer-in-Berlin.1.2.3.html?offer_filter=1&city_id=8&noDeact=1&categories%5B%5D=0&rent_types%5B%5D=0&sMin=15&rMax=600"

# Run browser in headless mode (no visible window)
# Set to false if you want to see what the bot is doing
run_headless: true

# Minimum rental period in months (0 = any length, -1 = unlimited)
# Example: 6 means only contact listings available for 6+ months
min_listing_length_months: 6

# Automatically attach SCHUFA document to messages
attach_schufa: false

# OpenAI API key for message personalization (optional)
# Leave empty if you don't want AI personalization
openai_key: "sk-..."

# Custom Python expression to filter listings (optional)
# Example: Skip listings with "John Doe" in the user name
# custom_condition: "user_name not in 'John Doe'"

# Optional: Specify paths if Firefox/geckodriver not in PATH
geckodriver_path: ""  # e.g., "/opt/homebrew/bin/geckodriver"
firefox_path: ""       # e.g., "/opt/homebrew/bin/firefox"
```

### Step 3: Get Your Filtered Search URL

This is the most important step! The bot will only contact listings that match your filters.

1. Go to [wg-gesucht.de](https://www.wg-gesucht.de)
2. Enter your search criteria:
   - City/area
   - Price range
   - Room size
   - Any other filters you want
3. Click "Filter anwenden" (Apply Filter)
4. **Copy the entire URL from your browser's address bar**
5. Paste it into the `url:` field in `config.yaml`

**Example URL:**
```
https://www.wg-gesucht.de/wg-zimmer-in-Berlin.1.2.3.html?offer_filter=1&city_id=8&noDeact=1&categories%5B%5D=0&rent_types%5B%5D=0&sMin=15&rMax=600
```

### Step 4: Write Your Message Template

1. Open `message.txt` in a text editor
2. Write your message. Use `recipient` as a placeholder - it will be automatically replaced with the listing owner's first name.

**Example message:**
```
Hello recipient,

I came across your listing and I'm very interested! I'm a [your age]-year-old [your profession/student] looking for a new WG in [city].

[Add more about yourself - hobbies, interests, why you're looking for a WG, etc.]

I'd love to hear from you!

Best regards,
[Your name]
```

**Important notes:**
- The word `recipient` will be replaced with the person's first name automatically
- If you're using OpenAI personalization, the bot will enhance this message based on each listing
- Keep it friendly and authentic - this is your first impression!

### Step 5: (Optional) Add SCHUFA Document

If you want to automatically attach your credit check document:

1. Place your SCHUFA document in the project folder
2. **Rename it exactly to:** `SCHUFA-BonitaetsCheck.pdf` (case-sensitive!)
3. Set `attach_schufa: true` in `config.yaml`

### Step 6: (Optional) Set Up OpenAI Personalization

If you want AI-powered message personalization:

1. Get an API key from [platform.openai.com](https://platform.openai.com)
2. Add your credit (OpenAI charges per API call, but it's very cheap - around $0.002 per message)
3. Paste your API key into `openai_key:` in `config.yaml`

**What this does:**
- Reads each listing's description
- Personalizes your message to reference specific details
- Automatically includes any "magic words" the listing asks for
- Makes your message stand out from generic applications

## Running the Bot

### macOS/Linux

1. **Activate your virtual environment** (if not already active)
   ```bash
   source env/bin/activate
   ```

2. **Run the bot**
   ```bash
   python3 main.py
   ```
   
   Or use the provided script:
   ```bash
   bash run-mac.sh
   ```

### Windows

1. **Activate your virtual environment** (if not already active)
   ```cmd
   env\Scripts\activate
   ```

2. **Run the bot**
   ```cmd
   python main.py
   ```

## How It Works

Here's what happens when you run the bot:

1. **Initialization**: The bot loads your configuration and connects to WG-Gesucht
2. **Login**: Automatically logs into your WG-Gesucht account
3. **Monitoring loop** (runs every 60 seconds):
   - Fetches all listings matching your filtered URL
   - Compares with previously seen listings
   - For each new listing:
     - Checks if rental period meets your minimum requirement
     - Checks if it matches your custom conditions
     - Checks if you've already contacted this listing
     - If all checks pass:
       - Opens the listing page
       - (Optional) Uses GPT to personalize your message
       - Sends your message
       - (Optional) Attaches SCHUFA document
       - Records the listing as "contacted"
4. **Error handling**: If anything goes wrong, it logs the error and restarts after 10 seconds

## Understanding the Logs

The bot logs everything to both the console and `debug.log`. Here's what to look for:

- `Found X new listings.` - New listings detected
- `Trying to send message to: ...` - Processing a listing
- `Rental period of X months is below required Y months. Skipping ...` - Filtered out due to short rental period
- `Listing in 'prev_listings' file, therefore contacted in the past! Skipping ...` - Already contacted
- `Logged in.` - Successfully logged in
- `>>>> Message sent to: ... <<<<` - Message successfully sent! 🎉
- `Could not find or click the Send button.` - Something went wrong (check logs for details)

## Troubleshooting

### "Browser crashed! You might be trying to run it without a screen in terminal?"

**Solution**: Make sure `run_headless: true` in your `config.yaml`. If you're on Linux without a display, you may need to set up a virtual display or use a VNC server.

### "geckodriver not found"

**Solution**: 
- Make sure geckodriver is installed and in your PATH
- Or specify the full path in `config.yaml`: `geckodriver_path: "/full/path/to/geckodriver"`

### "Firefox not found"

**Solution**:
- Make sure Firefox is installed
- Or specify the full path in `config.yaml`: `firefox_path: "/full/path/to/firefox"`

### "reCAPTCHA detected"

**What it means**: WG-Gesucht is showing a CAPTCHA. This usually happens if you're making too many requests.

**Solution**: 
- Wait a few minutes - CAPTCHAs often disappear on their own
- The bot will continue checking and will proceed once the CAPTCHA is gone
- If it persists, you may need to manually solve it once in a browser session

### "Message has already been sent previously"

**What it means**: You've already contacted this listing before (either manually or via the bot).

**Solution**: This is normal! The bot skips listings you've already contacted to avoid spamming.

### "Ad is deactivated"

**What it means**: The listing has been removed or deactivated.

**Solution**: The bot automatically skips these. No action needed.

### Bot keeps restarting

**Solution**: 
- Check `debug.log` for the specific error
- Common issues:
  - Wrong credentials in `config.yaml`
  - Invalid URL format
  - Missing dependencies
  - Network connectivity issues

## Running 24/7 on a Server

### Option 1: Oracle Cloud (Free Tier)

Oracle Cloud offers a free tier that's perfect for running this bot 24/7:

1. Sign up at [cloud.oracle.com](https://cloud.oracle.com)
2. Create a VM instance (VM.Standard.A1.Flex, aarch64 architecture)
3. Follow the Linux installation instructions above
4. Use `screen` or `tmux` to keep the bot running:
   ```bash
   screen -S wg-bot
   source env/bin/activate
   python3 main.py
   # Press Ctrl+A then D to detach
   ```
5. To reconnect: `screen -r wg-bot`

### Option 2: Any Linux Server

1. Follow the Linux installation instructions
2. Use `systemd` to create a service (for automatic startup)
3. Or use `screen`/`tmux` as shown above

## File Structure

```
wg-gesucht-bot-main/
├── main.py                 # Main entry point (handles auto-restart)
├── wg_gesucht.py           # Core bot logic
├── config.yaml             # Your configuration (create this!)
├── message.txt             # Your message template
├── past_listings.txt       # Tracks contacted listings (auto-generated)
├── debug.log               # Detailed logs (auto-generated)
├── requirements.txt        # Python dependencies
├── run-mac.sh             # Quick start script for macOS
├── src/                   # Source code modules
│   ├── listing_getter.py  # Fetches listings from WG-Gesucht
│   ├── listing_info_getter.py  # Gets detailed listing information
│   ├── submit_wg.py       # Handles login and message sending
│   └── openai_helper.py   # OpenAI integration
└── README.md              # This file
```

## Important Notes & Best Practices

### ⚠️ Use Responsibly

- **Don't spam**: The bot respects rate limits and avoids duplicates, but use it responsibly
- **Personalize your message**: Even with AI, make sure your base message is authentic
- **Follow up manually**: The bot sends initial messages - you should still respond to replies personally
- **Respect the platform**: WG-Gesucht is a real platform with real people - be respectful

### 💡 Tips for Success

1. **Craft a good base message**: Your `message.txt` is the foundation - make it genuine and friendly
2. **Use filters wisely**: The more specific your filters, the better matches you'll get
3. **Enable GPT personalization**: It really makes a difference in response rates
4. **Attach SCHUFA**: Many listings prefer applicants with credit checks ready
5. **Check logs regularly**: Make sure everything is working as expected

### 🔒 Security

- **Never commit `config.yaml`**: It contains your password! (It's already in `.gitignore`)
- **Keep your API keys secret**: Don't share your OpenAI API key
- **Use a strong password**: Make sure your WG-Gesucht password is secure

## Contributing

Contributions are welcome! If you find a bug or have an idea for improvement:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## License

This project is open source. Use it responsibly and at your own risk.

## Acknowledgments

- Original inspiration from [nickirk/immo](https://github.com/nickirk/immo)
- Based on [jonasdieker/wg-gesucht-bot](https://github.com/jonasdieker/wg-gesucht-bot) with significant improvements

## Support

If you encounter issues:

1. Check the `debug.log` file for detailed error messages
2. Review the Troubleshooting section above
3. Make sure all dependencies are installed correctly
4. Verify your `config.yaml` settings are correct

---

**Good luck finding your perfect WG! 🏠✨**

*Remember: This bot helps with the initial contact, but building a good relationship with your future flatmates is still up to you!*
```
