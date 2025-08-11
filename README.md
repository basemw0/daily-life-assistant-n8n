# Daily Zekr, Calendar & Tasks — n8n Template

**A lightweight n8n workflow that sends a single morning email with:**
- 🕌 **Zekr of the Day** (from Google Sheets)
- 📅 **Today's schedule** (Google Calendar — start & end times)
- ✅ **Today's tasks** (Todoist — cleaned & filtered)

This repo contains an importable n8n workflow (JSON) and supporting instructions so you (or others) can plug it into your own n8n instance.

---

## Files in this repo
- `workflow.json` — the exported n8n workflow (credentials removed; import into your n8n)
- `README.md` — this file
- `screenshots/` — sample email & workflow screenshots
- `LICENSE` — project license (MIT)

---

## Quick start ( import into n8n )

1. **Import the workflow**
   - In n8n: click **Workflows → Import** and upload `workflow.json`.
   - After importing, open the workflow editor.

2. **Connect your credentials**
   - For each node that needs a credential (Google Sheets, Google Calendar, Todoist, Gmail, LLM), click the node → Credentials → create/connect your account.
   - Replace any placeholder values like `REPLACE_WITH_YOUR_SHEET_ID`.

3. **Verify the Google Sheets structure**
   - Create a Google Sheet with a header row containing at least:
     - `zekr` (Arabic text)
     - `description` (optional short explanation)
   - Upload your azkar list there and note the Sheet ID.

4. **Configure the nodes**
   - Google Sheets node: set **Document** to your sheet and **Range** to the column (e.g., `A:A` or the sheet page).
   - Google Calendar node: choose the calendar to read from.
   - Todoist node: connect your Todoist account.
   - LLM / AI node: set your API key or credentials if using the formatter.
   - Gmail node (or SMTP): configure sending credentials and `To` address (your email).

5. **Test the workflow**
   - In the editor, run nodes individually to confirm data flows:
     - Run the Google Sheets node → ensure the `zekr` and `description` appear.
     - Run Google Calendar → verify events return start & end times.
     - Run Todoist → ensure tasks are filtered (you may need to run the cleaning function).
   - Finally, run the full workflow (dry-run) or enable the Cron trigger for actual scheduled runs.

---

## Notes & security
- **⚠️ Remove secrets:** `workflow.json` has been sanitized, but always double-check for secrets before publishing.
- **Tokens & credentials** must be created by each user inside their own n8n instance.
- If you plan to distribute this widely, prefer using OAuth and instruct users to create their own API credentials.

---

## How it works (high level)
1. Cron trigger runs daily at configured time.
2. Google Sheets node reads the azkar list.
3. A function node picks the daily zekr (based on day-of-month or your chosen logic).
4. Google Calendar node retrieves today’s events (start & end time).
5. Todoist node retrieves today’s tasks (a Function node filters unwanted demo items).
6. An LLM/Formatter node constructs a nice HTML email (zekr + translation/description + events + tasks).
7. Gmail node sends the email (optionally attach a TTS MP3).

---

## Customization ideas
- Send via WhatsApp using Twilio instead of email.
- Add TTS audio of the Zekr and attach to the email.
- Multi-user onboarding (turn into a small service).
- Save sent emails in Google Drive or Notion for logging.

---

## Contributing
Contributions are welcome. Please open an issue or send a pull request. For significant changes, open an issue first to discuss.

---

## License
This project is licensed under the MIT License.

---

## Credits
Thanks to **Osama Younis** for the azkar dataset that inspired this project.
