## Getting Started
Import calendar entries from a date range into Obsidian's daily notes via ics links

![Watch the video](video.mp4)

### Install Python
- Install Python with the following libraries:
  - **requests** - For downloading the ICS file over HTTP(S).
  - **ics** - For reading and processing calendar information in ICS format.
  - **datetime** - Built into Python, provides functionality for date and time manipulation.
  - **os** - Another standard library in Python that provides access to operating system functions (e.g., file system).
  - **re** - A standard library for regular expressions for text processing and pattern matching.
  - **tkinter** - A standard Python library (may need to be installed separately with some Python distributions) for creating GUI applications.
  - **tkcalendar** - For selecting a date in the GUI (extends tkinter).
  - **pytz** - For working with time zones.
  
- You may need to install some of these libraries using commands like the following:

```bash
  pip install requests
  pip install ics
  pip install tkcalendar
  pip install pytz
  pip install tk
```

### Plugins in Obsidian
- Install the [Calendar plugin](https://github.com/liamcain/obsidian-calendar-plugin) (optional).
- Install the [Python Scripter](https://github.com/nickrallison/obsidian-python-scripter) plugin (required).
- Add the CalendarToMarkdown.py file to the .obsidian/scripts/python/ folder.

### Edit the CalendarToMarkdown.py file
1. Add the URL of your ICS calendar with apostrophes and separated by commas, for example:

```python
Code kopieren
ics_urls = [
    'https://www.[your-url-address].ics',
    'https://calendar.google.com/calendar/ical/[your-secret-ics-link]/basic.ics',
]
```

2. Adjust the notes folder and the templates folder. In this example, daily notes are located in the daily notes folder, and the template for daily notes is in the templates folder with the template dailynote.md.

```python
Code kopieren
notes_folder = os.path.join(os.path.abspath(os.path.join(os.path.dirname(__file__), '..', '..', '..')), 'daily notes')
placeholder = "<!-- CALENDAR_ENTRIES -->"
template_path = os.path.join(os.path.abspath(os.path.join(os.path.dirname(__file__), '..', '..', '..')), 'templates', 'dailynote.md')
```

3. Set your time zone:

```python
Code kopieren
local_tz = pytz.timezone('Europe/Berlin')
```

In your daily note template, add the following placeholder:

```
> [!TIP] Today
><!-- CALENDAR_ENTRIES -->
```

## Importing Events
1. Open a daily note (optional; if no daily note is open, the import will start from the current day).
2. Daily notes should be titled in the 'YYYY-MM-DD' format. If you use a different format, you will need to adjust the script.
3. Open the command palette and select Python Scripter: Run CalendarToMarkdown.py.
4. Select your desired date range.
5. Click Import: on each import, all events will be deleted and reinserted.