# utl-a-more-robust-method-to-delete-files
A more robust method to delete files
    %let pgm=utl-a-more-robust-method-to-delete-files;

    A more robust method to delete files

    Thanks to Ron Fehd
    https://support.sas.com/resources/papers/proceedings15/SAS1573-2015.pdf

    SAS fails to delete the text files below, while perl anf python have no problem?
    Please correct me if I am wrong.

    Perl provides a lot of bells and whistles

    github
    https://github.com/rogerjdeangelis/utl-a-more-robust-method-to-delete-files

    see github
    https://tinyurl.com/y87ncq4b
    https://github.com/rogerjdeangelis/utl-cross-patform-perl-script-to-parse-a-config-file-and-pass-parameters-to-SAS-batch

    /*                     _
     ___  ___   __ _ _ __ | |__   _____  __   ___  _ __
    / __|/ _ \ / _` | `_ \| `_ \ / _ \ \/ /  / _ \| `_ \
    \__ \ (_) | (_| | |_) | |_) | (_) >  <  | (_) | | | |
    |___/\___/ \__,_| .__/|_.__/ \___/_/\_\  \___/|_| |_|
                    |_|
    */
    I prefer perl for scripting batch processing and the windows shell.
    I like perl even over c-shell and bash.

    I avoid powershell because it is tightly linked to the limitied availability of MS-365(1 year only).
    It does not seem to work well with legacy office?
    Also I prefer open source, who knows when MS will require 1 year availability for all it products(1 year .net powershell?).
    /*                     _                        __  __
     ___  ___   __ _ _ __ | |__   _____  __   ___  / _|/ _|
    / __|/ _ \ / _` | `_ \| `_ \ / _ \ \/ /  / _ \| |_| |_
    \__ \ (_) | (_| | |_) | |_) | (_) >  <  | (_) |  _|  _|
    |___/\___/ \__,_| .__/|_.__/ \___/_/\_\  \___/|_| |_|
                    |_|
    */
    /*                __       _ _
     ___  __ _ ___   / _| __ _(_) |___
    / __|/ _` / __| | |_ / _` | | / __|
    \__ \ (_| \__ \ |  _| (_| | | \__ \
    |___/\__,_|___/ |_|  \__,_|_|_|___/

    */
    options xwait;
    x 'del d:/temp/a & b/a & b.txt; /* on Windows */
    'b.txt' is not recognized as an internal or external command,
    operable program or batch file.

    x 'del "d:/temp/a & b/a & b.txt"'; /* on Windows */
    'b.txt' is not recognized as an internal or external command,

    filename xyz 'd:/temp/a & b/a & b.txt.txt';
    data _null_; rc = fdelete('xyz'); run; /* do this */
    %let x = %sysfunc(fdelete(xyz)); /* or this */
    filename xyz clear;

    /*           _   _                                      _
     _ __  _   _| |_| |__   ___  _ __   __      _____  _ __| | _____
    | `_ \| | | | __| `_ \ / _ \| `_ \  \ \ /\ / / _ \| `__| |/ / __|
    | |_) | |_| | |_| | | | (_) | | | |  \ V  V / (_) | |  |   <\__ \
    | .__/ \__, |\__|_| |_|\___/|_| |_|   \_/\_/ \___/|_|  |_|\_\___/
    |_|    |___/
    */
    %utl_submit_py64_310('
    import os;
    os.remove("d:/temp/a & b/a & b.txt");
    ');

    /*               _                      _
     _ __   ___ _ __| | __      _____  _ __| | _____
    | `_ \ / _ \ `__| | \ \ /\ / / _ \| `__| |/ / __|
    | |_) |  __/ |  | |  \ V  V / (_) | |  |   <\__ \
    | .__/ \___|_|  |_|   \_/\_/ \___/|_|  |_|\_\___/
    |_|
    */

    %utl_submit_pl64('
    #!/usr/bin/perl;`
    unlink("d:/temp/a & b/a & b.txt") or die "Could not delete the file!\n";`
    ');

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
