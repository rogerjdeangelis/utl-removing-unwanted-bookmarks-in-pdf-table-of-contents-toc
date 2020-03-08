# utl-removing-unwanted-bookmarks-in-pdf-table-of-contents-toc
Removing unwanted bookmarks in pdf table of contents toc;
    Removing unwanted bookmarks in pdf table of contents toc;

    github
    https://tinyurl.com/qrx5mnn
    https://github.com/rogerjdeangelis/utl-removing-unwanted-bookmarks-in-pdf-table-of-contents-toc

    SAS Forum (related to these two)
    https://tinyurl.com/qlcg8wb
    https://communities.sas.com/t5/ODS-and-Base-Reporting/Remove-empty-lines-proc-contents-in-the-TOC-created-using-ods/m-p/630491

    https://goo.gl/GpPt8l
    https://communities.sas.com/t5/ODS-and-Base-Reporting/How-to-delete-Extra-bookmark-of-the-pdf-file-using-proc-document/m-p/358174

    *                _     _
     _ __  _ __ ___ | |__ | | ___ _ __ ___
    | '_ \| '__/ _ \| '_ \| |/ _ \ '_ ` _ \
    | |_) | | | (_) | |_) | |  __/ | | | | |
    | .__/|_|  \___/|_.__/|_|\___|_| |_| |_|
    |_|
    ;

    ods pdf file='d:/pdf/problem.pdf';
      ods proclabel="Female Participants";
      proc report data=sashelp.class(obs=4  where=(sex="F"));
            column _all_;
      run;
      ods proclabel="Male Participants";
      proc report data=sashelp.class(obs=4 where=(sex="M"));
            column _all_;
      run;
    ods pdf close;

    YEILDS these Bookmarks

        Female Paticipants
           Detailed an/or Summarized Reports
             Table 1

        Male Paticipants
           Detailed an/or Summarized Reports
             Table 1

     *_                   _
    (_)_ __  _ __  _   _| |_
    | | '_ \| '_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    ;

    data have;
      retain count 1;
      set class ;
    run;quit;

    *            _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| '_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    ;
        Female Paticipants
           Demographics

         Male Paticipants
           Demographics

    *
     _ __  _ __ ___   ___ ___  ___ ___
    | '_ \| '__/ _ \ / __/ _ \/ __/ __|
    | |_) | | | (_) | (_|  __/\__ \__ \
    | .__/|_|  \___/ \___\___||___/___/
    |_|
    ;

    /* In the PROC REPORT, add this variable to the beginning of the COL
     statement, DEFINE it as either GROUP or ORDER, then add a BREAK BEFORE
     with a PAGE option and a null CONTENTS=. */

    ods pdf file="d:/pdf/want.pdf" contents ;

    ods proclabel="Male Participants";
     proc report nowd data=have(where=(sex="M")) contents="Demographics";
        col count name age height weight;
        define count / group noprint;
     /* Note that CONTENTS= on the BREAK statement is new syntax for SAS 9.2 */
        break before count / contents="" page;
     run;
    ods proclabel="Female Participants";
     proc report nowd data=have(where=(sex="F")) contents="Demographics";
        col count name age height weight;
        define count / group noprint;
     /* Note that CONTENTS= on the BREAK statement is new syntax for SAS 9.2 */
        break before count / contents="" page;
     run;

    ods pdf close;

