# CS 152 Trust and Safety Engineering - Extremist Content Moderation System

This repository contains a comprehensive Discord bot implementation for automated extremist content detection and moderation, developed as part of the CS 152 Trust and Safety Engineering course. The system combines AI-powered content classification with human moderation workflows.

## Project Overview

The system includes:
- **Discord Bot**: Automated content monitoring with Gemini AI integration
- **Reporting System**: User-initiated report flow through DMs
- **Moderation Queue**: Priority-based report management system
- **Research Components**: Evaluation datasets and AI model performance analysis

## Key Features

### Automated Content Detection
- Real-time message scanning using Gemini AI
- Classification of extremist content (Propaganda, Radicalization, Recruitment)
- Automatic report generation and queue management

### User Reporting System
- DM-based report flow with guided categorization
- Support for various abuse types (Spam, Harassment, Offensive Content, Threats)
- Block user functionality and additional comment collection

### Moderation Interface
- Priority queue system (high/medium/low) based on threat severity
- Mod commands for queue management (`\count`, `\preview`, `\start next`)
- Severity assignment with automated response system (0-3 scale)
- Account action tracking and false report detection

## Setup Instructions

### Prerequisites

Install required Python packages:
```bash
python3 -m pip install requests
python3 -m pip install discord.py
python3 -m pip install google-generativeai
```

### Configuration

Create `DiscordBot/tokens.json` with your API keys:
```json
{
    "discord": "your_discord_bot_token",
    "gemini_google_ai_studio": "your_gemini_api_key"
}
```

### Discord Bot Setup

1. Create a Discord application at https://discord.com/developers
2. Name your bot "Group # Bot" (where # is your group number)
3. Copy the bot token to your tokens.json file
4. Enable the following Privileged Gateway Intents:
   - Presence Intent
   - Server Members Intent  
   - Message Content Intent
5. Generate an OAuth2 URL with bot permissions and invite to your server

### Running the Bot

```bash
cd DiscordBot
python3 bot.py
```

The bot will automatically:
- Monitor messages in `group-#` channels
- Scan content for extremist language using Gemini AI
- Generate reports for detected harmful content
- Handle user reports via DM

## Architecture

### Core Components

- **`DiscordBot/bot.py`**: Main bot implementation with message handling and AI integration
- **`DiscordBot/report.py`**: Report flow state machine for user-initiated reports
- **`data/`**: Research datasets and evaluation components

### Key Classes

- **`ModBot`**: Main Discord client handling all bot functionality
- **`ReportQueue`**: Priority-based queue for managing reports  
- **`Report`**: State machine managing user reporting workflow
- **Content Type Enums**: Classification system for abuse types

## Research Data

The `data/` directory contains:

### Datasets
- **MIWS (Multi-ideology ISIS/Jihadist White Supremacist)**: Seed datasets for training
- **Evaluation Data**: Formatted datasets for OpenAI, Gemini, and Perspective API testing
- **Performance Metrics**: Confusion matrices and statistical analysis

### Files
- `eval_data_*.json`: Formatted evaluation datasets for different AI models
- `predictions_*.json`: Model classification outputs
- `stats_*.json`: Performance metrics and accuracy analysis
- `sub_confusion_*.json`: Detailed confusion matrices by content type
- `data_processing.ipynb`: Jupyter notebook for data analysis and model evaluation

## Usage

### User Commands
- `\report`: Start reporting process via DM
- `\cancel`: Cancel current report
- `\help`: Get help information

### Moderator Commands
- `\start mod`: Enter moderation mode
- `\count`: View queue size
- `\preview`: See next report
- `\start next`: Begin processing next report
- `\quit`: Exit moderation mode

### Bot Behavior
- Automatically scans all messages in monitored channels
- Generates reports for detected extremist content
- Routes reports to moderation queue based on priority
- Sends system messages to mod channels for review

## Model Performance

The system has been evaluated using multiple AI models:

### Gemini AI Performance
- **Accuracy**: 96.5%
- **F1 Score**: 93.4%
- **Precision**: 99.7%
- **Recall**: 87.9%

### GPT Performance
- **Accuracy**: 91.1%
- **F1 Score**: 81.4%
- **Precision**: 100%
- **Recall**: 68.6%

## Content Classification

The system classifies content into:
- **Propaganda**: Extremist messaging and ideology promotion
- **Radicalization**: Content promoting extremist beliefs
- **Recruitment**: Active recruitment for extremist organizations
- **None**: Non-extremist content

## Security Features

- API key management through separate token files
- Safety filter bypass for content analysis (necessary for extremist content detection)
- False report tracking and automatic account actions
- Graduated response system based on report severity

## Academic Context

This project demonstrates practical application of:
- AI-powered content moderation
- Human-in-the-loop systems
- Trust and safety engineering principles  
- Multi-model evaluation and comparison
- Real-time threat detection and response

## Requirements

- Python 3.7+
- Discord.py library
- Google Generative AI library
- Valid Discord bot token
- Gemini AI API key
- Discord server with appropriate channel naming (`group-#`, `group-#-mod`)