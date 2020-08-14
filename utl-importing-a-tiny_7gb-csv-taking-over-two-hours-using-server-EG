%let pgm=utl-importing-a-tiny_7gb-csv-taking-over-two-hours-using-server-EG;                                                                                    
                                                                                                                                                                
SAS Forum: Importing a tiny csv taking over two hours using server EG                                                                                           
                                                                                                                                                                
Took less than a minute.                                                                                                                                        
                                                                                                                                                                
SAS Forum                                                                                                                                                       
https://tinyurl.com/yyac5nja                                                                                                                                    
https://communities.sas.com/t5/SAS-Enterprise-Guide/Importing-a-large-CSV-file-and-getting-Insuffcient-Memory/m-p/676857                                        
                                                                                                                                                                
SOAPBOX ON                                                                                                                                                      
I have seen server EG with as little as 500mb of ram. However, I don't think this was your problem.                                                             
If you happen hit the 500mg ram limit EG will start pafing it brains out and a 1 minute job                                                                     
can take hours. Count distinct is notorius for pager thrashing?                                                                                                 
SOAPBOX OFF                                                                                                                                                     
                                                                                                                                                                
On my inexpensive Dell 7610 less than $1,000. It took less than a minute and very little memory.                                                                
If you had a moderate size CSV say 700gb you could parition the csv in say 28 250mb files and run 28                                                            
sinultaneous jobs and then create a view to put the 14 SAS datasets back together.                                                                              
I have 16 cores and 32 threads.                                                                                                                                 
SOAPBOX OFF.                                                                                                                                                    
                                                                                                                                                                
BENCHMARK 59.66 SECONDS                                                                                                                                         
                                                                                                                                                                
NOTE: The infile "m:/csv/tiny.csv" is:                                                                                                                          
      Filename=m:\csv\tiny.csv,                                                                                                                                 
      RECFM=V,LRECL=500,File Size (bytes)=7,542,000,190 (bytes),                                                                                                
                                                                                                                                                                
NOTE: 18,000,000 records were read from the infile "m:/csv/tiny.csv".                                                                                           
      The minimum record length was 417.                                                                                                                        
      The maximum record length was 417.                                                                                                                        
                                                                                                                                                                
NOTE: The data set WORK.WANT has 18000000 observations and 38 variables.                                                                                        
NOTE: DATA statement used (Total process time):                                                                                                                 
      real time           59.66 seconds                                                                                                                         
      user cpu time       53.84 seconds                                                                                                                         
      system cpu time     5.79 seconds                                                                                                                          
      memory              1105.06k                                                                                                                              
      OS Memory           45740.00k                                                                                                                             
      Timestamp           08/14/2020 05:24:53 PM                                                                                                                
      Step Count                        525  Switch Count  0                                                                                                    
                                                                                                                                                                
/*                   _                                                                                                                                          
(_)_ __  _ __  _   _| |_                                                                                                                                        
| | `_ \| `_ \| | | | __|                                                                                                                                       
| | | | | |_) | |_| | |_                                                                                                                                        
|_|_| |_| .__/ \__,_|\__|                                                                                                                                       
        |_|                                                                                                                                                     
*/                                                                                                                                                              
                                                                                                                                                                
%let vars=38 ;                                                                                                                                                  
                                                                                                                                                                
data _null_;                                                                                                                                                    
  length nam $12;                                                                                                                                               
  file "m:/csv/tiny.csv" lrecl=500 recfm=v;                                                                                                                     
                                                                                                                                                                
  array chrs[&vars] $10 c1-c&vars (&vars*"A234567890");                                                                                                         
                                                                                                                                                                
  do _iorc_=1 to &vars - 1;                                                                                                                                     
     nam = vname(chrs[_iorc_]);                                                                                                                                 
     put nam $5. +(-1) "," @@;                                                                                                                                  
  end;                                                                                                                                                          
                                                                                                                                                                
  nam = vname(chrs[_iorc_]);                                                                                                                                    
  put nam;                                                                                                                                                      
                                                                                                                                                                
  do rec=1 to 18000000;                                                                                                                                         
     put (c1-c&vars) ( $ +(-1) ',');                                                                                                                            
  end;                                                                                                                                                          
                                                                                                                                                                
run;quit;                                                                                                                                                       
                                                                                                                                                                
* About 1 minute to run;                                                                                                                                        
                                                                                                                                                                
Directory of m:\csv                                                                                                                                             
                          SIZE(Bytes)                                                                                                                           
08/14/2020  05:19 PM     7,542,000,190 tiny.csv                                                                                                                 
                                                                                                                                                                
38 Variables 18,000,000 million records                                                                                                                         
                                                                                                                                                                
C1,C2,C3,C4,C5,C6,C7,C8,C9,C10,C11,C12,C13,C14,C15,C16,C17,C18,C19,C20,C21,C22,C23,C24,C25,C26,C27,C28,C29,C30,C31,C32,C33,C34,C35,C36,C37,C38                  
A234567890,A234567890,A234567890,A234567890,A234567890,A234567890,A234567890,A234567890,A234567890,A234567890,A234567890,,A234567890,A234567890.....            
A234567890,A234567890,A234567890,A234567890,A234567890,A234567890,A234567890,A234567890,A234567890,A234567890,A234567890,,A234567890,A234567890.....            
A234567890,A234567890,A234567890,A234567890,A234567890,A234567890,A234567890,A234567890,A234567890,A234567890,A234567890.,A234567890,A234567890.....            
...                                                                                                                                                             
                                                                                                                                                                
/*           _               _                                                                                                                                  
  ___  _   _| |_ _ __  _   _| |_                                                                                                                                
 / _ \| | | | __| `_ \| | | | __|                                                                                                                               
| (_) | |_| | |_| |_) | |_| | |_                                                                                                                                
 \___/ \__,_|\__| .__/ \__,_|\__|                                                                                                                               
                |_|                                                                                                                                             
*/                                                                                                                                                              
                                                                                                                                                                
Observations          18,000,000                                                                                                                                
Variables             38                                                                                                                                        
Observation Length    380                                                                                                                                       
Deleted Observations  0                                                                                                                                         
Compressed            NO                                                                                                                                        
Sorted                NO                                                                                                                                        
File Size (bytes)     6,858,539,008 (no comma and quotes so it is amaller)                                                                                      
                                                                                                                                                                
                                                                                                                                                                
WORK.WANT total obs=18,000,00                                                                                                                                   
                                                                                                                                                                
      C1          C2          C3                C36          C37          C38                                                                                   
                                                                                                                                                                
  A234567890  A234567890  A234567890         A234567890   A234567890   A234567890                                                                               
  A234567890  A234567890  A234567890         A234567890   A234567890   A234567890                                                                               
  A234567890  A234567890  A234567890         A234567890   A234567890   A234567890                                                                               
  A234567890  A234567890  A234567890         A234567890   A234567890   A234567890                                                                               
  ....                                                                                                                                                          
                                                                                                                                                                
/*                                                                                                                                                              
 _ __  _ __ ___   ___ ___  ___ ___                                                                                                                              
| `_ \| `__/ _ \ / __/ _ \/ __/ __|                                                                                                                             
| |_) | | | (_) | (_|  __/\__ \__ \                                                                                                                             
| .__/|_|  \___/ \___\___||___/___/                                                                                                                             
|_|                                                                                                                                                             
*/                                                                                                                                                              
                                                                                                                                                                
data want;                                                                                                                                                      
                                                                                                                                                                
  infile "m:/csv/tiny.csv" lrecl=500 recfm=v delimiter=',' firstobs=2 dsd;                                                                                      
  informat c1-c&vars $10.;                                                                                                                                      
  input c1-c&vars;                                                                                                                                              
                                                                                                                                                                
run;quit;                                                                                                                                                       
                                                                                                                                                                
                                                                                                                                                                
                                                                                                                                                                
