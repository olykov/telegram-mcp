# Telegram MCP Server (streamable-http)

This is a Telegram MCP server that allows you to interact with your Telegram account via HTTP.

# How to run

0. Get your API credentials at [my.telegram.org/apps](https://my.telegram.org/apps).
1. Copy `.env.example` to `.env` and fill only
  - TELEGRAM_API_ID
  - TELEGRAM_API_HASH

2. Run `session_string_generator.py`.
3. Copy the session string from the output and paste it into the .env file.

Your .env now looks like this
```
TELEGRAM_API_ID=your_api_id_here
TELEGRAM_API_HASH=your_api_hash_here
TELEGRAM_SESSION_NAME=anon
TELEGRAM_SESSION_STRING=your_session_string_here
```

4. run `docker-compose -f docker-compose.local.yml up -d`
5. You can see that it's up om http://localhost:8004/mcp but to test it see next step

Optional: 
1. Download Anthropic MCP inspector: `npx @modelcontextprotocol/inspector`
2. Setup all default with 
    - Transport Type: `Streamable HTTP`
    - URL: `http://localhost:8004/mcp`
3. Go to `tools` and feel free to test all your MCP tools

# Available methods

### Chat & Group Management
- **get_chats(page, page_size)**: Paginated list of chats
- **list_chats(chat_type, limit)**: List chats with metadata and filtering
- **get_chat(chat_id)**: Detailed info about a chat
- **create_group(title, user_ids)**: Create a new group
- **create_channel(title, about, megagroup)**: Create a channel or supergroup
- **edit_chat_title(chat_id, title)**: Change chat/group/channel title
- **delete_chat_photo(chat_id)**: Remove chat/group/channel photo
- **leave_chat(chat_id)**: Leave a group or channel
- **get_participants(chat_id)**: List all participants
- **get_admins(chat_id)**: List all admins
- **get_banned_users(chat_id)**: List all banned users
- **promote_admin(chat_id, user_id)**: Promote user to admin
- **demote_admin(chat_id, user_id)**: Demote admin to user
- **ban_user(chat_id, user_id)**: Ban user
- **unban_user(chat_id, user_id)**: Unban user
- **get_invite_link(chat_id)**: Get invite link
- **export_chat_invite(chat_id)**: Export invite link
- **import_chat_invite(hash)**: Join chat by invite hash
- **join_chat_by_link(link)**: Join chat by invite link

### Messaging
- **get_messages(chat_id, page, page_size)**: Paginated messages
- **list_messages(chat_id, limit, search_query, from_date, to_date)**: Filtered messages
- **list_topics(chat_id, limit, offset_topic, search_query)**: List forum topics in supergroups
- **send_message(chat_id, message)**: Send a message
- **reply_to_message(chat_id, message_id, text)**: Reply to a message
- **edit_message(chat_id, message_id, new_text)**: Edit your message
- **delete_message(chat_id, message_id)**: Delete a message
- **forward_message(from_chat_id, message_id, to_chat_id)**: Forward a message
- **pin_message(chat_id, message_id)**: Pin a message
- **unpin_message(chat_id, message_id)**: Unpin a message
- **mark_as_read(chat_id)**: Mark all as read
- **get_message_context(chat_id, message_id, context_size)**: Context around a message
- **get_history(chat_id, limit)**: Full chat history
- **get_pinned_messages(chat_id)**: List pinned messages
- **get_last_interaction(contact_id)**: Most recent message with a contact
- **create_poll(chat_id, question, options, multiple_choice, quiz_mode, public_votes, close_date)**: Create a poll

### Contact Management
- **list_contacts()**: List all contacts
- **search_contacts(query)**: Search contacts
- **add_contact(phone, first_name, last_name)**: Add a contact
- **delete_contact(user_id)**: Delete a contact
- **block_user(user_id)**: Block a user
- **unblock_user(user_id)**: Unblock a user
- **import_contacts(contacts)**: Bulk import contacts
- **export_contacts()**: Export all contacts as JSON
- **get_blocked_users()**: List blocked users
- **get_contact_ids()**: List all contact IDs
- **get_direct_chat_by_contact(contact_query)**: Find direct chat with a contact
- **get_contact_chats(contact_id)**: List all chats with a contact

### User & Profile
- **get_me()**: Get your user info
- **update_profile(first_name, last_name, about)**: Update your profile
- **delete_profile_photo()**: Remove your profile photo
- **get_user_photos(user_id, limit)**: Get a user's profile photos
- **get_user_status(user_id)**: Get a user's online status

### Media
- **get_media_info(chat_id, message_id)**: Get info about media in a message

### Search & Discovery
- **search_public_chats(query)**: Search public chats/channels/bots
- **search_messages(chat_id, query, limit)**: Search messages in a chat
- **resolve_username(username)**: Resolve a username to ID

### Stickers, GIFs, Bots
- **get_sticker_sets()**: List sticker sets
- **get_bot_info(bot_username)**: Get info about a bot
- **set_bot_commands(bot_username, commands)**: Set bot commands (bot accounts only)

### Privacy, Settings, and Misc
- **get_privacy_settings()**: Get privacy settings
- **set_privacy_settings(key, allow_users, disallow_users)**: Set privacy settings
- **mute_chat(chat_id)**: Mute notifications
- **unmute_chat(chat_id)**: Unmute notifications
- **archive_chat(chat_id)**: Archive a chat
- **unarchive_chat(chat_id)**: Unarchive a chat
- **get_recent_actions(chat_id)**: Get recent admin actions
---

Source: [telegram-mcp by chigwell](https://github.com/chigwell/telegram-mcp)