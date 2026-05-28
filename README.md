# gpt4pro-portable-windows
a portable .exe file that uses GPT4 pro (only runs on windows machines)


## Settings Overview

| Setting | Description | Default | Range / Options |
|---------|-------------|---------|------------------|
| **System Prompt** | Text inserted as a user message **before** every request. It influences the assistant’s behaviour but does not appear in the visible chat history. | `You are a helpful assistant.` | Free‑form text |
| **Font Size** | Size of the text in the chat display (both user and assistant messages). | 16 | 12 – 24 px |
| **Assistant Name** | Display name shown above each assistant reply. | `🤖 Bot` | Any string |
| **Show Timestamps** | When enabled, each message shows the current time (HH:MM) next to the sender name. | Off | On / Off |
| **Timeout** | Maximum time (in seconds) to wait for a response from the API before raising an error. | 30 | 10 – 60 s |
| **Max Retries** | Number of automatic retry attempts after a failed request. Retries use exponential backoff (1s, 2s, 4s…). | 3 | 1 – 5 |
| **Random User‑Agent** | When enabled, every HTTP request uses a different, realistic browser User‑Agent string (provided by the `fake_useragent` library). | On | On / Off |
| **Accept‑Language** | Value of the `Accept-Language` HTTP header sent to the API. | `en` | Any language code (e.g., `en`, `fr`, `de`, `en-US,en`). |
| **Context Turns** | Number of past conversation pairs (user + assistant) included in each API request. Older messages are dropped. | 20 | 2 – 40 |
| **Clear history** | Button – deletes all stored messages from the current session. | – | – |
| **Export chat** | Button – saves the current conversation as a JSON file. | – | – |
| **Import chat** | Button – loads a previously exported JSON conversation, replacing the current one. | – | – |

## Important Notes

1. **System prompt behaviour**  
   - The system prompt is sent as a **user message** (with `"linksToParse": []`) because the target API does not accept a native `system` role.  
   - It is **not saved** in the visible chat history; it only affects the API response for each new message.

2. **SSL & TLS**  
   - SSL certificate verification is **permanently disabled** in the code.  
   - The connection forces **TLS 1.2** and uses a broad cipher suite (`DEFAULT@SECLEVEL=1`).  
   - This is necessary to avoid `SSLEOFError` caused by the server’s non‑standard TLS configuration.
