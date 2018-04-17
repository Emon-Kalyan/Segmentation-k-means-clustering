libname segfcs "/folders/myfolders/segmentationfinalcasestudy/segmentation reattempted/";
proc import datafile = "/folders/myfolders/segmentationfinalcasestudy/CC GENERAL.csv" 
out = segfcs.segdata1 dbms = "csv" replace;
/*Understanding the contents of the dataset*/
ods pdf file= "/folders/myfolders/segmentationfinalcasestudy/datacleaning&filter.pdf";
proc contents data = segfcs.segdata1 varnum;
run;
/* From the proc contents proceedure we get that there are 18 variables */
/* Proc means proceedure to understand the distribution of the data*/
proc means data = segfcs.segdata1 nmiss mean var skewness median std min P1  P5 P10 P25 P50
P75 P90 P95 P99 max;
run;

/*Outlier replacement */
data segfcs.segdata2;
set segfcs.segdata1;
   if BALANCE > 5911.51 then BALANCE =  5911.51 ; 
 if BALANCE_FREQUENCY > 1 then BALANCE_FREQUENCY =  1 ; 
 if PURCHASES > 3999.92 then PURCHASES =  3999.92 ; 
 if ONEOFF_PURCHASES > 2675 then ONEOFF_PURCHASES =  2675 ; 
 if INSTALLMENTS_PURCHASES > 1753.08 then INSTALLMENTS_PURCHASES =  1753.08 ; 
 if CASH_ADVANCE > 4653.69 then CASH_ADVANCE =  4653.69 ; 
 if PURCHASES_FREQUENCY > 1 then PURCHASES_FREQUENCY =  1 ; 
 if ONEOFF_PURCHASES_FREQUENCY > 1 then ONEOFF_PURCHASES_FREQUENCY =  1 ; 
 if PURCHASES_INSTALLMENTS_FREQUENCY > 1 then PURCHASES_INSTALLMENTS_FREQUENCY =  1 ; 
 if CASH_ADVANCE_FREQUENCY > 0.583333 then CASH_ADVANCE_FREQUENCY =  0.583333 ; 
 if CASH_ADVANCE_TRX > 15 then CASH_ADVANCE_TRX =  15 ; 
 if PURCHASES_TRX > 57 then PURCHASES_TRX =  57 ; 
 if CREDIT_LIMIT > 12000 then CREDIT_LIMIT =  12000 ; 
 if PAYMENTS > 6083.43 then PAYMENTS =  6083.43 ; 
 if MINIMUM_PAYMENTS > 2767.05 then MINIMUM_PAYMENTS =  2767.05 ; 
 if PRC_FULL_PAYMENT > 1 then PRC_FULL_PAYMENT =  1 ; 
 if TENURE > 12 then TENURE =  12 ; 
run;
data segfcs.segdata2;
set segfcs.segdata2;
  if BALANCE < 8.80954 then BALANCE =  8.80954 ; 
 if BALANCE_FREQUENCY < 0.272727 then BALANCE_FREQUENCY =  0.272727 ; 
 if PURCHASES < 0 then PURCHASES =  0 ; 
 if ONEOFF_PURCHASES < 0 then ONEOFF_PURCHASES =  0 ; 
 if INSTALLMENTS_PURCHASES < 0 then INSTALLMENTS_PURCHASES =  0 ; 
 if CASH_ADVANCE < 0 then CASH_ADVANCE =  0 ; 
 if PURCHASES_FREQUENCY < 0 then PURCHASES_FREQUENCY =  0 ; 
 if ONEOFF_PURCHASES_FREQUENCY < 0 then ONEOFF_PURCHASES_FREQUENCY =  0 ; 
 if PURCHASES_INSTALLMENTS_FREQUENCY < 0 then PURCHASES_INSTALLMENTS_FREQUENCY =  0 ; 
 if CASH_ADVANCE_FREQUENCY < 0 then CASH_ADVANCE_FREQUENCY =  0 ; 
 if CASH_ADVANCE_TRX < 0 then CASH_ADVANCE_TRX =  0 ; 
 if PURCHASES_TRX < 0 then PURCHASES_TRX =  0 ; 
 if CREDIT_LIMIT < 1000 then CREDIT_LIMIT =  1000 ; 
 if PAYMENTS < 89.921689 then PAYMENTS =  89.921689 ; 
 if MINIMUM_PAYMENTS < 73.203221 then MINIMUM_PAYMENTS =  73.203221 ; 
 if PRC_FULL_PAYMENT < 0 then PRC_FULL_PAYMENT =  0 ; 
 if TENURE < 8 then TENURE =  8 ; 

run;

/* As we have done the outlier treatment next we do the proc means proceedure to check the 
distribution of the data again */
proc means data= segfcs.segdata2 nmiss mean skewness median std min P1 P5 P25 P50 P75 
P95 P99 max;
/* We may see that the outlier treated data has reduced skewness and std, so we proceed to the next 
step of treating the missing values */
data segfcs.segdata2;
set segfcs.segdata2;
 if BALANCE =    .   then  BALANCE = 873.385231 ; 
 if BALANCE_FREQUENCY =    .   then  BALANCE_FREQUENCY = 1 ; 
 if PURCHASES =    .   then  PURCHASES = 361.28 ; 
 if ONEOFF_PURCHASES =    .   then  ONEOFF_PURCHASES = 38 ; 
 if INSTALLMENTS_PURCHASES =    .   then  INSTALLMENTS_PURCHASES = 89 ; 
 if CASH_ADVANCE =    .   then  CASH_ADVANCE = 0 ; 
 if PURCHASES_FREQUENCY =    .   then  PURCHASES_FREQUENCY = 0.5 ; 
 if ONEOFF_PURCHASES_FREQUENCY =    .   then  ONEOFF_PURCHASES_FREQUENCY = 0.083333 ; 
 if PURCHASES_INSTALLMENTS_FREQUENCY =    .   then  PURCHASES_INSTALLMENTS_FREQUENCY = 0.166667 ; 
 if CASH_ADVANCE_FREQUENCY =    .   then  CASH_ADVANCE_FREQUENCY = 0 ; 
 if CASH_ADVANCE_TRX =    .   then  CASH_ADVANCE_TRX = 0 ; 
 if PURCHASES_TRX =    .   then  PURCHASES_TRX = 7 ; 
 if CREDIT_LIMIT =    .   then  CREDIT_LIMIT = 3000 ; 
 if PAYMENTS =    .   then  PAYMENTS = 856.901546 ; 
 if MINIMUM_PAYMENTS =    .   then  MINIMUM_PAYMENTS = 312.343947 ; 
 if PRC_FULL_PAYMENT =    .   then  PRC_FULL_PAYMENT = 0 ; 
 if TENURE =    .   then  TENURE = 12 ; 
run;

/* The dataset is ready for the segmentation proceedure */
/*Next we  check the multicollinearity of the data by using factor analysis */
/* First we draw the scree plot and unserstand the cumulative variance to understand how many factors should be taken. */
Proc factor data= segfcs.segdata1 plots= (scree initloadings preloadings loadings);
run;
/*Next we run the proc factor using nfactor option for 9 factors*/
Proc factor data= segfcs.segdata2 nfactors= 7 method= principal rotate= varimax reorder out= segfcs.factor;
var
BALANCE
BALANCE_FREQUENCY
PURCHASES
ONEOFF_PURCHASES
INSTALLMENTS_PURCHASES
CASH_ADVANCE
PURCHASES_FREQUENCY
ONEOFF_PURCHASES_FREQUENCY
PURCHASES_INSTALLMENTS_FREQUENCY
CASH_ADVANCE_FREQUENCY
CASH_ADVANCE_TRX
PURCHASES_TRX
CREDIT_LIMIT
PAYMENTS
MINIMUM_PAYMENTS
PRC_FULL_PAYMENT
TENURE
;
run;
/* From factor analysis the variables extracted after remnoving the multicollinearity are 
ONEOFF_PURCHASES  
CASH_ADVANCE_TRX 
BALANCE
PURCHASES_INSTALLMENT_FREQUENCY
CREDIT_LIMIT  
PURCHASES_FULL_PAYMENT
PAYMENTS 
BALANCE_FREQUENCY 
TENURE 
 */
/* Next we create the variables for standardization */
data segfcs.segdata2;
set segfcs.segdata2;
Z_ONEOFF_PURCHASES = ONEOFF_PURCHASES;
Z_CASH_ADVANCE_TRX = CASH_ADVANCE_TRX;
Z_BALANCE = BALANCE;
Z_PRCH_INST_FREQ = PURCHASES_INSTALLMENTS_FREQUENCY;
Z_CREDIT_LIMIT = CREDIT_LIMIT; 	
Z_PRC_FULL_PAY = PRC_FULL_PAYMENT;
Z_PAYMENTS = PAYMENTS;
Z_BALANCE_FREQ = BALANCE_FREQUENCY;
Z_TENURE = TENURE;



/*Standardizing the variables for k-means factor analysis*/
proc standard data = segfcs.segdata2  mean = 0 std = 1  out = segfcs.stdsegdata3;
var
Z_ONEOFF_PURCHASES  
Z_CASH_ADVANCE_TRX 
Z_BALANCE
Z_PRCH_INST_FREQ 
Z_CREDIT_LIMIT  
Z_PRC_FULL_PAY 
Z_PAYMENTS 
Z_BALANCE_FREQ 
Z_TENURE 
;
run;
/* proc sql; */
/* select *  */
/* from segfcs.stdsegdata */
/* quit; */

/* Doing k-means cluster analysis from clusters 3 to 6 */
proc fastclus data = segfcs.stdsegdata3 out = segfcs.stdsegdata3 maxclusters = 3 cluster = clus_3 maxiter = 100;
var
Z_ONEOFF_PURCHASES   
Z_CASH_ADVANCE_TRX 
Z_BALANCE
Z_PRCH_INST_FREQ 
Z_CREDIT_LIMIT  
Z_PRC_FULL_PAY 
Z_PAYMENTS 
Z_BALANCE_FREQ 
Z_TENURE
;
run;
proc fastclus data = segfcs.stdsegdata3 out = segfcs.stdsegdata3 maxclusters = 4 cluster = clus_4 maxiter = 100;
var
Z_ONEOFF_PURCHASES   
Z_CASH_ADVANCE_TRX 
Z_BALANCE
Z_PRCH_INST_FREQ 
Z_CREDIT_LIMIT  
Z_PRC_FULL_PAY 
Z_PAYMENTS 
Z_BALANCE_FREQ 
Z_TENURE
;
run;
proc fastclus data = segfcs.stdsegdata3 out = segfcs.stdsegdata3 maxclusters = 5 cluster = clus_5 maxiter = 100;
var
Z_ONEOFF_PURCHASES   
Z_CASH_ADVANCE_TRX 
Z_BALANCE
Z_PRCH_INST_FREQ 
Z_CREDIT_LIMIT  
Z_PRC_FULL_PAY 
Z_PAYMENTS 
Z_BALANCE_FREQ 
Z_TENURE
;
run;
/* best sizes */
proc fastclus data = segfcs.stdsegdata3 out = segfcs.stdsegdata3 maxclusters = 6 cluster = clus_6 maxiter = 100;
var
Z_ONEOFF_PURCHASES   
Z_CASH_ADVANCE_TRX 
Z_BALANCE
Z_PRCH_INST_FREQ 
Z_CREDIT_LIMIT  
Z_PRC_FULL_PAY 
Z_PAYMENTS 
Z_BALANCE_FREQ 
Z_TENURE
;
run;

/*Checking the segment size of each clsuters*/
proc freq data = segfcs.stdsegdata3;
table clus_3 clus_4 clus_5 clus_6;
run;
/*Summarizing the mean of diff v'bles in diff cluster and comparing with overall*/
/* data segfcs.segdata2 ( keep= cust_id clus_3 clus_4 clus_5 clus_6) ; */
/* set segfcs.segdata1; */
/* run; */



data segfcs.stdsegdata3;
set segfcs.stdsegdata3;
Monthly_av_prch = CASH_ADVANCE + (PURCHASES/PURCHASES_FREQUENCY);
Av_prchcashadv_trx = PURCHASES_TRX + CASH_ADVANCE_TRX;
Purch_type = ONEOFF_PURCHASES + INSTALLMENTS_PURCHASES;
Limit_Usage = BALANCE/CREDIT_LIMIT;
Paytominpay = PAYMENTS/MINIMUM_PAYMENTS;





proc tabulate data = segfcs.stdsegdata3;
var
BALANCE
BALANCE_FREQUENCY
PURCHASES
ONEOFF_PURCHASES
INSTALLMENTS_PURCHASES
CASH_ADVANCE
PURCHASES_FREQUENCY
ONEOFF_PURCHASES_FREQUENCY
PURCHASES_INSTALLMENTS_FREQUENCY
CASH_ADVANCE_FREQUENCY
CASH_ADVANCE_TRX
PURCHASES_TRX
CREDIT_LIMIT
PAYMENTS
MINIMUM_PAYMENTS
PRC_FULL_PAYMENT
TENURE
Av_prchcashadv_trx
Monthly_av_prch
Purch_type
Limit_Usage
Paytominpay
;
class clus_3 clus_4 clus_5 clus_6;
table
(BALANCE
BALANCE_FREQUENCY
PURCHASES
ONEOFF_PURCHASES
INSTALLMENTS_PURCHASES
CASH_ADVANCE
PURCHASES_FREQUENCY
ONEOFF_PURCHASES_FREQUENCY
PURCHASES_INSTALLMENTS_FREQUENCY
CASH_ADVANCE_FREQUENCY
CASH_ADVANCE_TRX
PURCHASES_TRX
CREDIT_LIMIT
PAYMENTS
MINIMUM_PAYMENTS
PRC_FULL_PAYMENT
TENURE
Av_prchcashadv_trx
Monthly_av_prch
Purch_type
Limit_Usage
Paytominpay)*mean, clus_3 clus_4 clus_5 clus_6 ALL;
run;










































