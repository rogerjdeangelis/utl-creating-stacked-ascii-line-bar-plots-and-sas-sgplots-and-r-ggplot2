# utl-creating-stacked-ascii-line-bar-plots-and-sas-sgplots-and-r-ggplot2
Creating stacked ascii line bar plots and sas sgplots and r ggplot2
    %let pgm=utl-creating-stacked-ascii-line-bar-plots-and-sas-sgplots-and-r-ggplot2;

    Creating stacked ascii line bar plots and sas sgplots and r ggplot2

      SOLUTIONS

             1. sas line vbar plot
             2  sas line hbar plot
             3  sas sgplot
             4  r ggplot


    SAS SGPLOT
    https://tinyurl.com/mpa3zmfx
    https://github.com/rogerjdeangelis/utl-creating-stacked-ascii-line-bar-plots-and-sas-sgplots-and-r-ggplot2/blob/main/subgroup.png

    R GGPLOT2
    https://tinyurl.com/yk9nzrxb
    https://github.com/rogerjdeangelis/utl-creating-stacked-ascii-line-bar-plots-and-sas-sgplots-and-r-ggplot2/blob/main/rbar.png

    github
    https://tinyurl.com/4a5b5pp9
    https://github.com/rogerjdeangelis/utl-creating-stacked-ascii-line-bar-plots-and-sas-sgplots-and-r-ggplot2

    related to
    https://tinyurl.com/5dv7vjm5
    https://stackoverflow.com/questions/79251252/how-can-i-create-a-stacked-barchart-with-this-data-using-ggplot2

    /*               _     _
     _ __  _ __ ___ | |__ | | ___ _ __ ___
    | `_ \| `__/ _ \| `_ \| |/ _ \ `_ ` _ \
    | |_) | | | (_) | |_) | |  __/ | | | | |
    | .__/|_|  \___/|_.__/|_|\___|_| |_| |_|
    |_|
    */


    /**************************************************************************************************************************/ /
    /*                        |                                            |                                                  */
    /*                        |                                            |                                                  */
    /*                        |                                            |                                                  */
    /*       INPUT            |    PROCESS                                 |                 OUTPUT                           */
    /*       =====            |    =======                                 |                                                  */
    /*                        |                                            |                                                  */
    /*                        |                                            |                                                  */
    /*  ID    VAR    VAL      | SAS ASCII VBAR                             |           VAL       ID                           */
    /*                        | ==============                             |                 A  B  C  D                       */
    /*  A     X1      40      |                                            |              ---------------                     */
    /*  A     X2      20      | options ps=32 ls=64;                       |              | 70          |                     */
    /*  A     X3      10      | proc chart data=sd1.have;                  |              | --          |                     */
    /*  B     X1      30      | vbar id/sumvar=val                         |              | X3          |                     */
    /*  B     X2      15      |   space=1 descending width=2               |              | X3          |                     */
    /*  B     X3       5      |   subgroup=var;                            |           60 + X2 50       + 60                  */
    /*  C     X1      20      | run;quit;                                  |              | X2 --       |                     */
    /*  C     X2      10      |                                            |              | X2 X3       |                     */
    /*  C     X3       3      |                                            |              | X2 X2 33    |                     */
    /*  D     X1      10      |                                            |           40 + X1 X2 --    + 40                  */
    /*  D     X2       5      |                                            |              | X1 X2 X3    |                     */
    /*  D     X3       1      |                                            |              | X1 X1 X2    |                     */
    /*                        |                                            |              | X1 X1 X2 16 |                     */
    /*  options               |                                            |           20 + X1 X1 X1 -- + 20                  */
    /*   validvarname=upcase; |                                            |              | X1 X1 X1 X2 |                     */
    /*  libname sd1 "d:/sd1"; |                                            |              | X1 X1 X1 X1 |                     */
    /*  data sd1.have;        |                                            |              | X1 X1 X1 X1 |                     */
    /*   input ID$ var$ val;  |                                            |              ---------------                     */
    /*  cards4;               |                                            |                 A  B  C  D                       */
    /*  A X1 40               |                                            |                     ID                           */
    /*  A X2 20               |                                            |                                                  */
    /*  A X3 10               |                                            |                                                  */
    /*  B X1 30               |                                            |                                                  */
    /*  B X2 15               |                                            |                                                  */
    /*  B X3 5                |                                            |                                                  */
    /*  C X1 20               |                                            |                                                  */
    /*  C X2 10               |                                            |                                                  */
    /*  C X3 3                |                                            |                                                  */
    /*  D X1 10               |                                            |                                                  */
    /*  D X2 5                |                                            |                                                  */
    /*  D X3 1                |                                            |                                                  */
    /*  ;;;;                  |                                            |                                                  */
    /*  run;quit;             |                                            |                                                  */
    /*                        |                                            |                                                  */
    /*                        |                                            |                                                  */
    /*                        |---------------------------------------------------------------------------------------------- */
    /*                        |                                            |                                                  */
    /*                        | SAS ASCII HBAR                             | ID                 VAL                           */
    /*                        | ==============                             |       10   20   30   40   50   60   70 Freq Sum  */
    /*                        |                                            |   -----+----+----+----+----+----+----+           */
    /*                        | options ps=44 ls=64;                       |  |                                   |           */
    /*                        | proc chart data=sd1.have;                  | A|AAAAAAAAAAAAAAAAAAAABBBBBBBBBBCCCCC| A  3  70  */
    /*                        | hbar id/sumvar=val                         | B|AAAAAAAAAAAAAAABBBBBBBBCCC         | B  3  50  */
    /*                        |  subgroup=var descending;                  | C|AAAAAAAAAABBBBBCC                  | C  3  33  */
    /*                        | run;quit;                                  | D|AAAAABBBC                          | D  3  16  */
    /*                        |                                            |  |                                   |           */
    /*                        |                                            |  -----+----+----+----+----+----+----+-           */
    /*                        |                                            |       10   20   30   40   50   60   70           */
    /*                        |                                            |                 VAL Sum                          */
    /*                        |                                            |                                                  */
    /*                        |                                            | Symbol VAR     Symbol VAR     Symbol VAR         */
    /*                        |                                            |    A   X1         B   X2         C   X3          */
    /*                        |                                            |                                                  */
    /*                        |-----------------------------------------------------------------------------------------------*/
    /*                        |                                            |                                                  */
    /*                        | SAS SGPLOT                                 |  d:/png/subgroup.png                             */
    /*                        | ==========                                 |                                                  */
    /*                        |                                            |  https://tinyurl.com/mpa3zmfx                    */
    /*                        | ods listing gpath='d:\png';                |                                                  */
    /*                        | ods graphics /reset                        |                                                  */
    /*                        | imagename="subgroup" imagefmt=png;         |                                                  */
    /*                        | proc sgplot data=sd1.have  noautolegend ;  |                                                  */
    /*                        | title "Average Concentration";             |                                                  */
    /*                        | vbar id/                                   |                                                  */
    /*                        |   group=var                                |                                                  */
    /*                        |   response=val                             |                                                  */
    /*                        |   seglabel                                 |                                                  */
    /*                        |   categoryorder=respdesc                   |                                                  */
    /*                        |   seglabelattrs=(family="Arial" size=12pt);|                                                  */
    /*                        | yaxis labelattrs=(size=15pt)               |                                                  */
    /*                        |   valueattrs=(size=13pt)                   |                                                  */
    /*                        |   label="Concentration"                    |                                                  */
    /*                        |   DISCRETEORDER=Data;;                     |                                                  */
    /*                        | xaxis labelattrs=(size=12pt)               |                                                  */
    /*                        |   valueattrs=(size=10pt)                   |                                                  */
    /*                        |   display=(nolabel) ;                      |                                                  */
    /*                        | keylegend /                                |                                                  */
    /*                        |  titleattrs=(size=12pt)                    |                                                  */
    /*                        |  title="";                                 |                                                  */
    /*                        | run;quit;                                  |                                                  */
    /*                        |  ods graphics off;                         |                                                  */
    /*                        |  ods listing;                              |                                                  */
    /*                        |                                            |                                                  */
    /*                        |-----------------------------------------------------------------------------------------------*/
    /*                        |                                            |                                                  */
    /*                        | R GGPLOT2                                  |                                                  */
    /*                        | =========                                  |  d:/png/rbar.png                                 */
    /*                        |                                            |                                                  */
    /*                        | %utl_rbeginx;                              |  https://tinyurl.com/4a5b5pp9                    */
    /*                        | parmcards4;                                |                                                  */
    /*                        | library(haven)                             |                                                  */
    /*                        | library(dplyr)                             |                                                  */
    /*                        | library(tidyr)                             |                                                  */
    /*                        | library(ggplot2)                           |                                                  */
    /*                        | source("c:/oto/fn_tosas9x.R")              |                                                  */
    /*                        | have<-                                     |                                                  */
    /*                        | read_sas("d:/sd1/have.sas7bdat")           |                                                  */
    /*                        | print(have)                                |                                                  */
    /*                        | png("d:/png/rbar.png");                    |                                                  */
    /*                        | have %>%                                   |                                                  */
    /*                        |   ggplot(aes(x=ID, y=VAL,fill=VAR)) +      |                                                  */
    /*                        |   geom_bar(stat="identity") +              |                                                  */
    /*                        |   geom_text(aes(label = VAL),              |                                                  */
    /*                        |   position= position_stack(vjust=0.5),     |                                                  */
    /*                        |   size = 4,color = "white") +              |                                                  */
    /*                        |   theme_bw()                               |                                                  */
    /*                        | png()                                      |                                                  */
    /*                        | ;;;;                                       |                                                  */
    /*                        | %utl_rendx;                                |                                                  */
    /*                        |                                            |                                                  */
    /*                        |                                            |                                                  */
    /**************************************************************************************************************************/

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    options
     validvarname=upcase;
    libname sd1 "d:/sd1";
    data sd1.have;
     input ID$ var$ val;
    cards4;
    A X1 40
    A X2 20
    A X3 10
    B X1 30
    B X2 15
    B X3 5
    C X1 20
    C X2 10
    C X3 3
    D X1 10
    D X2 5
    D X3 1
    ;;;;
    run;quit;

    /*                         _
    / |  ___  __ _ ___  __   _| |__   __ _ _ __
    | | / __|/ _` / __| \ \ / / `_ \ / _` | `__|
    | | \__ \ (_| \__ \  \ V /| |_) | (_| | |
    |_| |___/\__,_|___/   \_/ |_.__/ \__,_|_|

    */

    options ps=32 ls=64;
    proc chart data=sd1.have;
    vbar id/sumvar=val
      space=1 descending width=2
      subgroup=var;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*    VAL       ID                                                                                                        */
    /*          A  B  C  D                                                                                                    */
    /*       ---------------                                                                                                  */
    /*       | 70          |                                                                                                  */
    /*       | --          |                                                                                                  */
    /*       | X3          |                                                                                                  */
    /*       | X3          |                                                                                                  */
    /*    60 + X2 50       + 60                                                                                               */
    /*       | X2 --       |                                                                                                  */
    /*       | X2 X3       |                                                                                                  */
    /*       | X2 X2 33    |                                                                                                  */
    /*    40 + X1 X2 --    + 40                                                                                               */
    /*       | X1 X2 X3    |                                                                                                  */
    /*       | X1 X1 X2    |                                                                                                  */
    /*       | X1 X1 X2 16 |                                                                                                  */
    /*    20 + X1 X1 X1 -- + 20                                                                                               */
    /*       | X1 X1 X1 X2 |                                                                                                  */
    /*       | X1 X1 X1 X1 |                                                                                                  */
    /*       | X1 X1 X1 X1 |                                                                                                  */
    /*       ---------------                                                                                                  */
    /*          A  B  C  D                                                                                                    */
    /*              ID                                                                                                        */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*___                    _     _
    |___ \   ___  __ _ ___  | |__ | |__   __ _ _ __
      __) | / __|/ _` / __| | `_ \| `_ \ / _` | `__|
     / __/  \__ \ (_| \__ \ | | | | |_) | (_| | |
    |_____| |___/\__,_|___/ |_| |_|_.__/ \__,_|_|

    */

    options ps=44 ls=64;
    proc chart data=sd1.have;
    hbar id/sumvar=val
     subgroup=var descending;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  ID                                                      VAL                                                           */
    /*                                             Freq         Sum                                                           */
    /*       |                                                                                                                */
    /*  A    |AAAAAAAAAAAAAAAAAAAABBBBBBBBBBCCCCC     3    70.00000                                                           */
    /*       |                                                                                                                */
    /*  B    |AAAAAAAAAAAAAAABBBBBBBBCCC              3    50.00000                                                           */
    /*       |                                                                                                                */
    /*  C    |AAAAAAAAAABBBBBCC                       3    33.00000                                                           */
    /*       |                                                                                                                */
    /*  D    |AAAAABBBC                               3    16.00000                                                           */
    /*       |                                                                                                                */
    /*       -----+----+----+----+----+----+----+                                                                             */
    /*            10   20   30   40   50   60   70                                                                            */
    /*                                                                                                                        */
    /*                      VAL Sum                                                                                           */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /*  Symbol VAR     Symbol VAR     Symbol VAR                                                                              */
    /*                                                                                                                        */
    /*     A   X1         B   X2         C   X3                                                                               */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*____                                   _       _
    |___ /   ___  __ _ ___   ___  __ _ _ __ | | ___ | |_
      |_ \  / __|/ _` / __| / __|/ _` | `_ \| |/ _ \| __|
     ___) | \__ \ (_| \__ \ \__ \ (_| | |_) | | (_) | |_
    |____/  |___/\__,_|___/ |___/\__, | .__/|_|\___/ \__|
                                 |___/|_|
    */

    %utlfkil(d:/png/subgroup.png);

    ods listing gpath='d:\png';
    ods graphics /reset
    imagename="subgroup" imagefmt=png;
    proc sgplot data=sd1.have  noautolegend ;
    title "Average Concentration";
    vbar id/
      group=var
      response=val
      seglabel
      categoryorder=respdesc
      seglabelattrs=(family="Arial" size=12pt);
    yaxis labelattrs=(size=15pt)
      valueattrs=(size=13pt)
      label="Concentration"
      DISCRETEORDER=Data;;
    xaxis labelattrs=(size=12pt)
      valueattrs=(size=10pt)
      display=(nolabel) ;
    keylegend /
     titleattrs=(size=12pt)
     title="";
    run;quit;
     ods graphics off;
     ods listing;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* d:/png/subgroup.png                                                                                                    */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*  _                              _       _   ____
    | || |    _ __    __ _  __ _ _ __ | | ___ | |_|___ \
    | || |_  | `__|  / _` |/ _` | `_ \| |/ _ \| __| __) |
    |__   _| | |    | (_| | (_| | |_) | | (_) | |_ / __/
       |_|   |_|     \__, |\__, | .__/|_|\___/ \__|_____|
                     |___/ |___/|_|
    */

    %utlfkil(d:/png/rbar.png);

    %utl_rbeginx;
    parmcards4;
    library(haven)
    library(dplyr)
    library(tidyr)
    library(ggplot2)
    source("c:/oto/fn_tosas9x.R")
    have<-
    read_sas("d:/sd1/have.sas7bdat")
    print(have)
    png("d:/png/rbar.png");
    have %>%
      ggplot(aes(x=ID, y=VAL,fill=VAR)) +
      geom_bar(stat="identity") +
      geom_text(aes(label = VAL),
      position= position_stack(vjust=0.5),
      size = 4,color = "white") +
      theme_bw()
    png()
    ;;;;
    %utl_rendx;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* d:/png/rbar.png                                                                                                        */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
