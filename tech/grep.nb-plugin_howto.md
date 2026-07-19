# grep.nb-plugin howto

#grep #nb #plugin #howto #tech

note :: this note is necessary because *nb grep --help* returns nothing

grep.nb-plugin

    Addresses the longstanding limitation of nb search showing only one matched line per result. See: nb issue #437

The problem

nb search is great for finding which notes match — but it shows only a single
line per result. When your notes have structure (headings, metadata,
annotations), one line is rarely enough context to know why a note matched or
what surrounds the match.

What this does

nb g searches your notes like grep -C: results grouped by note, with
surrounding context lines, match term highlighted. Works across all notebooks
or scoped to one.

[home:12] 2026-03-01.md
────────────────────────────────────────────────
  4-
  5:## ✅ Fix the login bug                        ← match (highlighted)
  6-> #project/work/web #bug
  7-

Install

nb plugin install https://raw.githubusercontent.com/linuxcaffe/nb-plugins/main/grep.nb-plugin

Usage

nb g <pattern>                      # search all notebooks (default: 1 line context, case-insensitive)
nb g <pattern> tasks:               # scope to one notebook
nb g -C 3 <pattern>                 # 3 lines of context around each match
nb g -A 2 -B 0 <pattern>            # 2 lines after, none before
nb g -I <pattern>                   # case-sensitive search
nb g -w <pattern>                   # whole-word matches only
nb g -F "[project.home]"            # literal string, no regex
nb g -v <pattern> tasks:            # list notes NOT containing pattern
nb g -e foo -e bar                  # OR: notes containing either pattern
nb g -l <pattern>                   # list matching note titles only
NB_GREP_CONTEXT=3 nb g <pattern>    # set default context via env var

Both nb g (short alias) and nb nb_grep (full name) work.
Regex examples

The plugin uses ERE (extended regular expressions) by default — the same
dialect as grep -E and rg. Use -F to disable regex and search for a literal
string.

nb g "meeting|standup"              # OR: notes matching either word
nb g "(TODO|FIXME|HACK)"            # any of three keywords
nb g "^#+ "                         # lines that are markdown headings
nb g "\+\w+"                        # taskwarrior-style tags (+word)
nb g "[0-9]{4}-[0-9]{2}-[0-9]{2}"  # ISO date pattern
nb g "https?://"                    # any URL
nb g -C 3 "def \w+\("               # function definitions, 3 lines context
nb g -F "[project.home]"            # -F: literal string, brackets not special

Options
Flag 	Description
-C <n> 	Lines of context around each match (default: 1)
-A <n> 	Lines after each match
-B <n> 	Lines before each match
-I 	Case-sensitive search (default is case-insensitive)
-w 	Whole-word matches only
-F 	Literal string, no regex (useful for [tags], URLs, etc.) — disables ERE
-v 	List notes NOT containing the pattern (implies -l)
-e <pattern> 	Extra pattern; repeatable, OR logic
-l 	List matching note titles only
