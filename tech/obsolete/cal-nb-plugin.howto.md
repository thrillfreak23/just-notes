# cal.nb-plugin howto

#cal #nb #plugin #howto #tech

note: this page is necessary because there is not any *_nb cal --help* available

### Interactive calendar browser
nb cal                                               # current month
nb cal jan                                           # month by name (current year)
nb cal 2026-01                                       # specific month (YYYY-MM)

### Range listing — shows [notebook:id], date, title
nb cal --start 2026-01-01                            # from date to today
nb cal --end   2026-03-01                            # from start of month to date
nb cal --start 2026-01-01 --end 2026-03-01           # explicit range

### Range grep
nb cal --start 2026-01-01 --end 2026-03-01 g <term> # search in range (case-insensitive)
nb cal --start mar1 g -C 3 meeting                  # 3 lines of context
nb cal --start mar1 g -I Meeting                    # case-sensitive

### Interactive date pickers (omit date after --start / --end)
nb cal --start                                       # pick start date interactively
nb cal --start --end                                 # pick both dates

### Notebook scoping (append notebook: as last arg)
nb cal --start mar4 g gbct home:

### Navigation keys (browser and date picker)
Key 	Action
← / → 	Previous / next day
↑ / ↓ 	Previous / next week
< / > 	Previous / next month
Enter 	Select — lists notes for that day
q / Esc 	Quit

### Output format

[home:42]  2026-03-08  Daily Journal
[home:43]  2026-03-05  Meeting notes


### IDs match nb's own numbering — use them directly with nb edit home:42, nb show home:42, etc.
### Notes

    Notes are matched by filename prefix: YYYYMMDD*.md (or .txt, .org).
    Date arguments accept anything GNU date -d understands: 2026-03-01, mar1, last monday, 20260301, etc.
    g grep is case-insensitive by default; g -I for case-sensitive. All standard grep flags (-C, -A, -B) are supported.

