# utl_fast_join_of_seven_tiny_tables_each_with_30_million_records
Fast join of seven tiny tables each with 30 million.  Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverflow SAS community.
    Fast join of seven tiny tables each with 30 million records each

    Tiny table join (unless large cartesion join or poorly normalized tables this is NOT the large table join.
                     Tables are much smaller than a terabyte)

     Fast join of seven tiny tables each with 30 million records each

     github
     https://tinyurl.com/ycupcppa
     https://github.com/rogerjdeangelis/utl_fast_join_of_seven_tiny_tables_each_with_30_million_records

     stackoverflow SAS
     https://stackoverflow.com/questions/51893315/hash-merge-in-sas

      Benchmark
      ========

         136 seconds to join 7 tables using master

            Master table - 300,300 records prmary jey variable rec

            Tables t1-t7 30.000,000 records an 11 numeric variable each

            Resuntant table 300,300 records


     INPUT
     =====

     WORK.MASTER total obs=300,300

      STATE      REC

      TEXAS    100000
      TEXAS    100001
      TEXAS    100002
      TEXAS    100003
      TEXAS    100004
      TEXAS    100005


     TABLE 1

      WORK.T1 obs=30,000,000

      REC    A1    A2    A3    A4    A5    A6    A7    A8    A9    A10

        1     1     3     5     7     9     1     2     3     4     8
        2     1     3     5     7     9     1     2     3     4     8
        3     1     3     5     7     9     1     2     3     4     8
        4     1     3     5     7     9     1     2     3     4     8
        5     1     3     5     7     9     1     2     3     4     8
        6     1     3     5     7     9     1     2     3     4     8
        7     1     3     5     7     9     1     2     3     4     8
        8     1     3     5     7     9     1     2     3     4     8
        9     1     3     5     7     9     1     2     3     4     8
       10     1     3     5     7     9     1     2     3     4     8

     ....

     TABLE 7

      WORK.T7  total obs=30,000,000

      REC    Obs    G1    G2    G3    G4    G5    G6    G7    G8    G9    G10

        1      1     7     9     1     3     9     7     8     8     4     5
        2      2     7     9     1     3     9     7     8     8     4     5
        3      3     7     9     1     3     9     7     8     8     4     5
        4      4     7     9     1     3     9     7     8     8     4     5
        5      5     7     9     1     3     9     7     8     8     4     5
        6      6     7     9     1     3     9     7     8     8     4     5
        7      7     7     9     1     3     9     7     8     8     4     5
        8      8     7     9     1     3     9     7     8     8     4     5

     EXAMPLE OUTPUT
     --------------

     WORK.WANT total obs=300,300

       STATE      REC     A1    A2   ..  B4    B5    C5    C6 ..  E4    F4    G7

       TEXAS    100000     1     3   ..   8     9     9     3 ..   1     2     8
       TEXAS    100002     1     3   ..   8     9     9     3 ..   1     2     8
       TEXAS    100004     1     3   ..   8     9     9     3 ..   1     2     8
      ....

    PROCESS  (Iprefer SQL for the join)
    =====================================

     proc sql;
       create
         table want as
       select
         *
       from
         master m
            left join t1(keep=rec a1-a3) a on m.rec  = a.rec
            left join t2(keep=rec b3-b5) b on m.rec  = b.rec
            left join t3(keep=rec c5-c8) c on m.rec  = c.rec
            left join t4(keep=rec d7-d9) d on m.rec  = d.rec
            left join t5(keep=rec e2-e4) e on m.rec  = e.rec
            left join t6(keep=rec f4-f5) f on m.rec  = f.rec
            left join t7(keep=rec g5-g7) g on m.rec  = g.rec
     ;quit;

    OUTPUT
    ======

     WORK.WANT total obs=300,300

      STATE      REC    A1 A2 A3 B3 B4 B5 C5 C6 C7 C8 D7 D8 D9 E2 E3 E4 F4 F5 G5 G6 G7

      TEXAS    100000   1  3  5  6  8  9  9  3  4  5  5  6  4  7  9  1  2  9  9  7  8
      TEXAS    100001   1  3  5  6  8  9  9  3  4  5  5  6  4  7  9  1  2  9  9  7  8
      TEXAS    100002   1  3  5  6  8  9  9  3  4  5  5  6  4  7  9  1  2  9  9  7  8
      TEXAS    100003   1  3  5  6  8  9  9  3  4  5  5  6  4  7  9  1  2  9  9  7  8
      TEXAS    100004   1  3  5  6  8  9  9  3  4  5  5  6  4  7  9  1  2  9  9  7  8
      TEXAS    100005   1  3  5  6  8  9  9  3  4  5  5  6  4  7  9  1  2  9  9  7  8
      TEXAS    100006   1  3  5  6  8  9  9  3  4  5  5  6  4  7  9  1  2  9  9  7  8
      TEXAS    100007   1  3  5  6  8  9  9  3  4  5  5  6  4  7  9  1  2  9  9  7  8
      TEXAS    100008   1  3  5  6  8  9  9  3  4  5  5  6  4  7  9  1  2  9  9  7  8
      ....

    *                _              _       _
     _ __ ___   __ _| | _____    __| | __ _| |_ __ _
    | '_ ` _ \ / _` | |/ / _ \  / _` |/ _` | __/ _` |
    | | | | | | (_| |   <  __/ | (_| | (_| | || (_| |
    |_| |_| |_|\__,_|_|\_\___|  \__,_|\__,_|\__\__,_|

    ;

    data
       t1(index=(rec/unique) keep=rec a:)
       t2(index=(rec/unique) keep=rec b:)
       t3(index=(rec/unique) keep=rec c:)
       t4(index=(rec/unique) keep=rec d:)
       t5(index=(rec/unique) keep=rec e:)
       t6(index=(rec/unique) keep=rec f:)
       t7(index=(rec/unique) keep=rec g:)
       t8(index=(rec/unique) keep=rec h:);

      array xa[10] a1-a10 (1,3,5,7,9,1,2,3,4,8);
      array xb[10] b1-b10 (2,4,6,8,9,2,3,4,4,5);
      array xc[10] c1-c10 (3,5,7,9,9,3,4,5,5,1);
      array xd[10] d1-d10 (4,6,8,0,9,4,5,6,4,5);
      array xe[10] e1-e10 (5,7,9,1,9,5,6,7,5,5);
      array xf[10] f1-f10 (6,8,0,2,9,6,7,7,4,7);
      array xg[10] g1-g10 (7,9,1,3,9,7,8,8,4,5);
      array xh[10] h1-h10 (8,0,2,4,9,8,9,8,4,5);

      do rec=1 to 30000000;
         output;
      end;
    run;quit;

    real time           4:18.67
    user cpu time       1:43.11


