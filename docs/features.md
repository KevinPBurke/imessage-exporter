# Features

This exporter is fully-featured and well-documented.

## Targeted Versions

This tool targets the current latest public release for macOS and iMessage. It may work with older databases, but all features may not be available.

## Supported Message Features

- Plain Text
  - Correctly extracts time-zone corrected timestamps
  - Detects when a message was read and calculates the time until read for both parties
    - Humanizes display of time-until-read duration
  - Parses `typedstream` message body data
  - Detects the service a message was sent from
    - In HTML exports, balloons are colored correctly for the service they were sent with
- Edited and Unsent messages
  - Detects if messages were edited or unsent
    - Edited messages
      - Parses `typedstream` message data
      - Displays content and timestamps for each edit
      - Humanizes display of edit timestamp gaps
      - Edited messages received before Ventura display as normal messages without history
    - Unsent messages
      - No content, but are noted in context
- Multi-part messages
  - iMessages can have multiple parts, separated by some special characters
  - Parts are displayed as
    - New lines in TXT exports
    - Separate balloons in HTML exports
- Threads and Message Replies
  - Threads are displayed both threaded under the parent as well as in-place
    - This is to preserve context, which can be lost if replying to older messages
    - Messages from a thread and were rendered in-place are annotated as such
    - In HTML exports, threaded messages are hyperlinked to allow for easy reading in context
  - For multi-part messages, replies are threaded under the correct message part
- Attachments
  - Any type of attachment that can be displayed on the web is embedded in the HTML exports
  - Attachments can be copied to the export directory or referenced in-place
  - Less-compatible images can be converted for even more portable exports:
    - Attachment `HEIC` files convert to `JPEG`
    - Sticker `HEIC` files convert to `PNG`
    - Sticker `HEICS` files convert to `GIF`
  - Attachments are displayed as
    - File paths in TXT exports
    - Embeds in HTML exports (including `<img>`, `<video>`, and `<audio>`)
- Expressives
  - Detects both bubble and screen effects
  - Messages sent with expressives are annotated
- Reactions
  - Detects reactions to messages
  - Messages sent with reactions are annotated
  - For multi-part messages, reactions are placed under the correct message part
- Stickers
  - Detects stickers sent or placed on messages
  - Messages sent with stickers are
    - Displayed in HTML exports
    - Annotated in TXT exports
  - For multi-part messages, stickers are placed under the correct message part
  - Sticker effects are annotated in all exports
- Apple Pay
  - Detects the transaction source, amount, and type
- URL previews
  - Parses the `NSKeyedArchiver` payload to extract preview data
    - Extracts cached metadata for each URL
    - Preview images display in HTML exports
    - URLs that have rotten may still retain some context if they have cached data
  - Handles cases where URL messages are overloaded with other message types
    - Apple Music (including preview streams)
    - Apple Maps (including Placemark data)
    - App Store (including app metadata)
    - Rich Collaboration
- App Integrations
  - Parses the `NSKeyedArchiver` payload to extract balloon data
  - Supports system message types as well as third party applications
    - Apple Fitness messages
    - Photo Slideshow messages
    - SharePlay/Facetime messages
    - Check In messages
    - Find My messages
- Duplicated group chats
  - Handles (participants) and chats (threads) can become duplicated
  - On startup:
    - Different handles that belong to the same person are combined
    - Chatrooms that contain identical contacts (i.e., duplicated handles) are combined
