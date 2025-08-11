# Daily Zekr, Calendar, Tasks & AI News - n8n Template

**A lightweight n8n workflow that sends you a single morning email containing:**

- 🕌 **Zekr of the Day** (from Google Sheets)  
- 📅 **Today's Schedule** (Google Calendar — start & end times)  
- ✅ **Today's Tasks** (Todoist — cleaned and filtered)  
- 📰 **Daily AI News Highlights** (aggregated from AI news sources)

This repository includes an importable n8n workflow JSON file and instructions to help you set it up quickly on your own n8n instance.

---

<img width="2147" height="1062" alt="image" src="https://github.com/user-attachments/assets/72f12061-b0b6-4dda-8f45-c069efb60c65" />

## Quick Start (Import into n8n)

1. **Import the workflow**  
   - In n8n, go to **Workflows → Import** and upload the `workflow.json` file.  
   - Open the imported workflow in the editor.

2. **Connect your credentials**  
   - For every node requiring access (Google Sheets, Google Calendar, Todoist, Gmail, LLM, News API), click the node → **Credentials** → create or connect your account.  
   - Replace placeholders such as `REPLACE_WITH_YOUR_SHEET_ID` or API keys with your actual values.

3. **Prepare your Google Sheet**  
   - Create a Google Sheet with a header row containing at least the column:  
     - `zekr`  
   - Populate it with your azkar list (see dataset linked below).  
   - Note your Sheet ID from the URL.

4. **Configure nodes**  
   - **Google Sheets**: Set the Document to your sheet.  
   - **Google Calendar**: Select the calendar to fetch events from.  
   - **Todoist**: Connect your Todoist account.  
   - **News API or AI News Source**: Configure credentials and query parameters for AI news aggregation.  
   - **LLM / Formatter**: Add your API key or credentials if used.  
   - **Gmail (or SMTP)**: Set sending credentials and recipient email address.

5. **Test the workflow**  
   - Run individual nodes to verify data retrieval:  
     - Google Sheets: Azkar are fetched correctly.  
     - Google Calendar: Events have correct start and end times.  
     - Todoist: Tasks are filtered and cleaned as expected.  
     - News API: Confirm AI news articles are retrieved.  
   - Run the full workflow in dry-run mode or activate the Cron trigger to schedule daily emails.

---

## How It Works (High-Level Overview)

1. Cron trigger activates the workflow daily at a configured time.  
2. Google Sheets node reads your azkar list.  
3. Function node selects the **Zekr of the Day** based on the day or custom logic.  
4. Google Calendar node retrieves today’s events with start and end times.  
5. Todoist node fetches today’s tasks, with filtering applied.  
6. News API or AI news source node aggregates the latest AI news headlines.  
7. LLM or formatter node assembles a nicely formatted HTML email combining:  
   - Zekr of the Day  
   - Today’s events  
   - Today’s tasks  
   - AI news highlights  
8. Gmail node sends the email to your configured recipient.

---

## Customization Ideas

- Switch from email to WhatsApp messages using Twilio API.  
- Add text-to-speech audio of the Zekr attached to the email.  
- Integrate a personal assistant chatbot on Telegram for interactive daily briefings.  
- Extend news sources or tailor AI news topics according to your interests.

---

## Credits

Special thanks to **Osama Younis** for the Azkar dataset that inspired this project.  
[Azkar Dataset on GitHub](https://github.com/osamayy/azkar-db/blob/master/azkar.csv)
