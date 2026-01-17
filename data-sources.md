
# Available Data Sources

Your Mac stores an incredible amount of data about your life. Here's everything we can sync.

## Currently Syncing

| Data Source | Table | Records | Status |
|-------------|-------|---------|--------|
| iCloud Photos | `bronze.apple_photos` | 50,751 total | ✅ 5.8% synced |
| iMessages/SMS | `bronze.apple_messages` | All | ✅ Full sync |
| Attachments | `bronze.apple_attachments` | 5,596 | ✅ Full sync |
| Contacts | `bronze.apple_contacts` | All | ✅ Full sync |
| Handles | `bronze.apple_handles` | 1,261 | ✅ Full sync |
| Chats | `bronze.apple_chats` | 798 | ✅ Full sync |

## Ready to Add

### Browser History

| Source | Location | Records | Notes |
|--------|----------|---------|-------|
| **Perplexity (Comet)** | `~/Library/Application Support/Comet/Default/History` | **39,906** | Your main browser |
| Safari | `~/Library/Safari/History.db` | 3,356 | Secondary |
| Chrome | `~/Library/Application Support/Google/Chrome/Default/History` | 182 | Barely used |

### Screen Time (knowledgeC.db)

Location: `~/Library/Application Support/Knowledge/knowledgeC.db`

| Stream | Records | What It Tracks |
|--------|---------|----------------|
| `/app/usage` | **11,036** | App name, start time, end time |
| `/display/isBacklit` | 1,220 | Screen on/off events |
| `/app/intents` | 1,189 | Siri intents, shortcuts |
| `/notification/usage` | 497 | Notification interactions |
| `/bluetooth/isConnected` | 132 | Device connections |

### Communication

| Source | Location | Records |
|--------|----------|---------|
| Call History | `~/Library/Application Support/CallHistoryDB/CallHistory.storedata` | **275** |
| Apple Notes | `~/Library/Group Containers/group.com.apple.notes/NoteStore.sqlite` | **459** |

### System

| Source | Location | Records |
|--------|----------|---------|
| Shell History | `~/.zsh_history` | **1,137** |
| WiFi Networks | `/Library/Preferences/SystemConfiguration/com.apple.airport.preferences.plist` | Various |
| Recent Files | `~/Library/Application Support/com.apple.sharedfilelist/` | Various |

## Attachment Breakdown

The 5,596 synced attachments break down as:

| Type | Count | % |
|------|-------|---|
| image/jpeg | 2,110 | 37.7% |
| image/png | 895 | 16.0% |
| image/heic | 428 | 7.6% |
| video/quicktime | 352 | 6.3% |
| image/gif | 139 | 2.5% |
| audio/x-m4a | 87 | 1.6% |
| video/3gpp | 58 | 1.0% |
| text/vcard | 40 | 0.7% |
| application/pdf | 18 | 0.3% |
| Other | 1,469 | 26.2% |

## Harder to Access

### AI Conversations

| Source | Challenge | Solution |
|--------|-----------|----------|
| Perplexity threads | Server-side storage | API or data export request |
| ChatGPT history | Server-side storage | OpenAI data export |
| Claude history | Server-side storage | Anthropic data export |

**Partial local data available:**
- Thread UUIDs (conversation IDs)
- User ID
- Weather widget responses
- Search queries (partial)

### Calendar & Reminders

Not found locally - likely iCloud-only sync. Would need:
- EventKit framework
- iCloud API integration

### Location History

`~/Library/Caches/com.apple.routined/Local.sqlite` doesn't exist on this Mac.

Significant Locations are system-protected and require Full Disk Access + decryption.

### Keychain

Can access:
- Metadata (creation dates, item names)
- Which apps accessed keychain

Cannot bulk access:
- Actual passwords (each requires auth prompt)

## Data Volume Summary

```
CURRENTLY SYNCING:        ~58,000 records
├── Photos:               50,751 (2,938 synced)
├── Messages:             Full
├── Attachments:          5,596
└── Contacts/Handles:     ~2,000

READY TO ADD:             ~57,000 records
├── Perplexity History:   39,906
├── App Usage:            11,036
├── Safari History:       3,356
├── Notes:                459
├── Calls:                275
├── Shell History:        1,137
└── System data:          ~1,000

TOTAL POTENTIAL:          ~115,000+ records
```

## File Locations Reference

```bash
# Browser Data
~/Library/Application Support/Comet/Default/History          # Perplexity
~/Library/Safari/History.db                                   # Safari
~/Library/Application Support/Google/Chrome/Default/History   # Chrome

# Apple Data
~/Library/Messages/chat.db                                    # Messages
~/Library/Group Containers/group.com.apple.notes/NoteStore.sqlite  # Notes
~/Library/Application Support/CallHistoryDB/CallHistory.storedata  # Calls
~/Library/Application Support/AddressBook/                    # Contacts

# System Data
~/Library/Application Support/Knowledge/knowledgeC.db         # Screen Time
~/.zsh_history                                                # Shell
/Library/Preferences/SystemConfiguration/...                  # WiFi
~/Library/Application Support/com.apple.sharedfilelist/       # Recents
```

[Continue to Home Mac Setup →](./home-mac)
