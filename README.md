# utl-transposing-data-wide-to-long-with-multiple-observations-per-subject
Transposing data wide to long with multiple observations per subject 
    Transposing data wide to long with multiple observations per subject                                                                               
                                                                                                                                                       
    No need for four steps                                                                                                                             
                                                                                                                                                       
    github                                                                                                                                             
    https://tinyurl.com/y465ygqb                                                                                                                       
    https://github.com/rogerjdeangelis/utl-transposing-data-wide-to-long-with-multiple-observations-per-subject                                        
                                                                                                                                                       
    SAS Forum                                                                                                                                          
    https://tinyurl.com/y4lmjzgy                                                                                                                       
    https://communities.sas.com/t5/New-SAS-User/transposing-data-wide-to-long-with-multiple-observations-per/m-p/583406                                
                                                                                                                                                       
                                                                                                                                                       
    utl_transpose (very fast transpose by                                                                                                              
    AUTHORS: Arthur Tabachneck, Xia Ke Shan, Robert Virgile and Joe Whitehurst                                                                         
    https://tinyurl.com/y9nfugth                                                                                                                       
    https://github.com/rogerjdeangelis/utl-macros-used-in-many-of-rogerjdeangelis-repositories                                                         
                                                                                                                                                       
    *_                   _                                                                                                                             
    (_)_ __  _ __  _   _| |_                                                                                                                           
    | | '_ \| '_ \| | | | __|                                                                                                                          
    | | | | | |_) | |_| | |_                                                                                                                           
    |_|_| |_| .__/ \__,_|\__|                                                                                                                          
            |_|                                                                                                                                        
    ;                                                                                                                                                  
                                                                                                                                                       
    data have;                                                                                                                                         
       format indate mmddyy10.;                                                                                                                        
       input id side indate mmddyy8. isolate $32.;                                                                                                     
    cards4;                                                                                                                                            
    1 1 07-03-17 s.aureus vile                                                                                                                         
    1 1 07-03-17 s.hominis bottle                                                                                                                      
    2 1 10-3-16  s.epiderm vile                                                                                                                        
    2 1 10-3-16  s.epiderm bottle                                                                                                                      
    2 1 04-10-17 s.pyogenes vile                                                                                                                       
    2 1 04-10-17 s.pyogenes bottle                                                                                                                     
    3 2 05-05-18 neg vile                                                                                                                              
    4 2 04-25-16 anaerobic vile                                                                                                                        
    4 2 04-25-16 e.coli vile                                                                                                                           
    4 2 04-25-16 e.faecalis bottle                                                                                                                     
    4 2 12-13-16 neg vile                                                                                                                              
    ;;;;                                                                                                                                               
    run;quit;                                                                                                                                          
                                                                                                                                                       
    workHAVE total obs=11                                                                                                                              
                                                                                                                                                       
       ID    SIDE   INDATE      ISOLATE                                                                                                                
                                                                                                                                                       
        1      1  07/03/2017    s.aureus vile                                                                                                          
        1      1  07/03/2017    s.hominis bottle                                                                                                       
        2      1  10/03/2016    s.epiderm vile                                                                                                         
        2      1  10/03/2016    s.epiderm bottle                                                                                                       
        2      1  04/10/2017    s.pyogenes vile                                                                                                        
        2      1  04/10/2017    s.pyogenes bottle                                                                                                      
        3      2  05/05/2018    neg vile                                                                                                               
        4      2  04/25/2016    anaerobic vile                                                                                                         
        4      2  04/25/2016    e.coli vile                                                                                                            
        4      2  04/25/2016    e.faecalis bottle                                                                                                      
        4      2  12/13/2016    neg vile                                                                                                               
                                                                                                                                                       
    *            _               _                                                                                                                     
      ___  _   _| |_ _ __  _   _| |_                                                                                                                   
     / _ \| | | | __| '_ \| | | | __|                                                                                                                  
    | (_) | |_| | |_| |_) | |_| | |_                                                                                                                   
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                                                                  
                    |_|                                                                                                                                
    ;                                                                                                                                                  
                                                                                                                                                       
                                                                                                                                                       
    Up to 40 obs from WANT total obs=4                                                                                                                 
                                                                                                                                                       
      ID  SIDE   INDATE1    ISOLATE1              INDATE2      ISOLATE2          INDATE3     ISOLATE3         INDATE4      ISOLATE4                    
                                                                                                                                                       
       1    1   07/03/2017  s.hominis bottle   07/03/2017  s.aureus vile               .                            .                                  
       2    1   04/10/2017  s.pyogenes bottle  10/03/2016  s.epiderm vile     04/10/2017  s.pyogenes vile  10/03/2016  s.epiderm bottle                
       3    2   05/05/2018  neg vile                    .                              .                            .                                  
       4    2   12/13/2016  neg vile           04/25/2016  e.faecalis bottle  04/25/2016  e.coli vile      04/25/2016  anaerobic vile                  
                                                                                                                                                       
    *                                                                                                                                                  
     _ __  _ __ ___   ___ ___  ___ ___                                                                                                                 
    | '_ \| '__/ _ \ / __/ _ \/ __/ __|                                                                                                                
    | |_) | | | (_) | (_|  __/\__ \__ \                                                                                                                
    | .__/|_|  \___/ \___\___||___/___/                                                                                                                
    |_|                                                                                                                                                
    ;                                                                                                                                                  
                                                                                                                                                       
    %utl_transpose(data=have, out=want, by=id side,var=indate isolate,sort=yes);                                                                       
                                                                                                                                                       
                                                                                                                                                       
                                                                                                                                                       
