# send.mb-plugin howto

#send #nb #plugin #howto #tech

note :: this document is needed because *nb send --help* returns nothing

send.nb-plugin

    For desktop Linux users — import any file from your file manager (Caja, Nemo, or terminal) directly into an nb notebook with a two-step GUI dialog.

What this does

nb send opens a two-step zenity dialog: first choose a notebook, then choose a folder and optionally rename the file. The actual import — file copy, .index entry, git commit — is handled by nb's own import copy command.

Calling convention is auto-detected:

    Nemo action: called with a file:/// URI argument
    Caja Scripts menu: reads $CAJA_SCRIPT_SELECTED_FILE_PATHS
    Terminal: plain file path argument

Files with unrecognised MIME types (executables, unknown binaries) trigger a
warning with the option to cancel or proceed. The original file extension is
always preserved — the rename field accepts only the stem.

Install

nb plugin install https://raw.githubusercontent.com/linuxcaffe/nb-plugins/main/send.nb-plugin

For Caja / Nemo file manager integration, see nb-desktop.
Usage

nb send ~/Pictures/photo.jpg          # terminal — plain path
nb send file:///home/djp/doc.pdf      # terminal — URI (as passed by Nemo)
nb send                               # Caja script — reads env var automatically

All activity is logged to /tmp/nb-send.log — useful for debugging file manager invocations where there is no visible terminal.

