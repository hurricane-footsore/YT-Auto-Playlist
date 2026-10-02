# YT Channel to Playlist Sync

An open-source, local-first utility that automatically fetches the latest uploads from specified YT channels and syncs them into your personal YT playlist.

## Features

- **Automated Sync**: Automatically checks for new uploads from target YouTube channels.
- **Quota-Efficient**: Uses low-cost API requests (`playlistItems.list`) to stay well within daily API limits.
- **100% Local & Private**: Runs entirely on your local machine with zero telemetry, tracking, or intermediary servers.
- **Open Source**: Full transparency—audit the code or build it yourself.

## Prerequisites

- **Python 3.8+** (or your runtime of choice)
- A **Google Cloud Project** with the **YouTube Data API v3** enabled.
- Your OAuth 2.0 Credentials file (`client_secret.json`) from the Google Cloud Console.

## Setup & Installation

### 1. Clone the Repository

```bash
git clone https://github.com/hurricane-footsore/YT-Auto-Playlist.git
cd YT-Auto-Playlist
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

*(Note: Required dependencies include `google-api-python-client`, `google-auth-oauthlib`, and `google-auth-httplib2`.)*

### 3. Google Cloud API Credentials Setup

1. Go to the [Google Cloud Console](https://console.cloud.google.com/).
2. Create a project and enable the **YouTube Data API v3**.
3. Configure the **OAuth Consent Screen**:
   - Set **Publishing Status** to **In Production** (or **Testing** if using test user emails).
   - Add the scope: `https://www.googleapis.com/auth/youtube` (or `https://www.googleapis.com/auth/youtube.force-ssl`).
4. Go to **Credentials** -> **Create Credentials** -> **OAuth client ID**.
5. Select **Desktop Application**, download the client secret JSON file, and save it as `client_secret.json` in the root directory of this project.

## Usage

Run the sync script locally:

```bash
python yt-main.py
```

On your first run:
1. A browser window will open requesting access to your YouTube account.
2. Sign in and grant permissions. *(If prompted with an "Unverified App" screen, click **Advanced** -> **Go to [App Name] (unsafe)** to proceed).*
3. A local `token.pickle` file will be generated to preserve your authentication for future automated runs. The token file will be encrypted to keep file scanners from finding the token file.

## Configuration

You can configure target channels and destination playlists inside `ytfetch.py` CHANNELS_CONFIG:

```json
{
    "channel_name": "Name used for log file/display",
    "channel_id": "UC_xxxxxxxxxxxxx",
    "target_playlist_id": "PLxxxxxxxxxxxxxx",
    "min_length": 3,      # minutes (0 to ignore)
    "max_length": -1,     # minutes (-1 to ignore)
    "must_contain": {}, # keywords the title must contain. Leave empty set set() to ignore
    "must_not_contain": {} # keywords the title must not contain.
}
```

## Privacy & Security

This tool runs locally on your hardware. Your OAuth tokens and API secrets are stored strictly on your local filesystem and are never shared with external parties.

For full details, read our [Privacy Policy](PRIVACY_POLICY.md).

## License

See project license in github.
