# NomNotes

TW collateral management
Nic manage the bilateral repo to borrow USD and use the pledge some TW stock as collateral at SOD
the rest of the collateral pool will be used for the intraday collateral for the onshore lender borrow
pledge stock collateral is not efficient
if we borrow 1M notional of a particular stock, then we need to pledge 110% collateral if it is cash collateral (TWD, JPY, USD)
for stock, it will require around 158% collateral, because 110% , and the collateral value apply 30% hair cut.
but if not used for collateral, we don't know what to use that stock for.
There is credit limit check on SBL business
SBL exposure is the 58% of the borrow trade
if we borrow 1M, we pledge 1.58M collateral, the business exposure is around 0.58M
there is limit on the overall credit limit on the desk, it actually kind of set the hard limit for the business
that's why the desk will choose to flip some of the borrow to ofsshore lenders because offshore lenders are global firm, the credit limit is larger
for  onshore lenders, we need to pick carefully for the borrow trade (choose higher rate borrow)
Flo monitor this credit limit daily
There is a SS borrow requirement (the stocks need to borrow for client, e.g. Citadel)
can choose either to borrow from onshore or offshore lenders
offshore lender is more relaxed for the credit limit, but you may not be able to borrow for some small or mid cap stock
small or mid cap stock will need to be borrow from onshore lender (onshore are smaller firm, then credit limit is tighter)
we need to pledge the collateral for the borrow
offshore usually can accept wider range of collateral
onshore accept only TW stock as collateral
when we pledge the collateral stock, there will be lot size for the stock, there will be rounding lot issue which make it overpledge.
the overpledge will be bigger if the stock price is big and lot size is big.
the onshore lenders have some fix size collateral buffer 
it is some fixed notional collateral we pledged and keep in the onshore lenders
it is larger for some onshored lender which have more trades with us, e.g. Yuanta
this buffer is to cover some sudden change of the collateral amount shortage due to sudden collatera/borrow stock price change.
Flo mentioned that the T0 SOD borrow requirement can be done in T-1 EOD
then can ask lender to hold T-1
if T0 SOD exchange published some update on uptick/Quota rules, then desk can ask client to cancel the locate for the updated stocks.
Client Order comes in as Buy or Sell
for sell
if client position is long, then it is unwind => Long Sell
if client position <=0, then need to submit locate
the locate will be approved as LS locate or SS locate
When order comes in, there will be two level check for sell order

Client level check
check if client position enough to sell
if not, is the a SS locate approved
firm level check
if it is LS locate, is firm position enough to cover it?
if it is SS locate, is the SS locate approved? 
for SS locate, normally the desk need to look at external availability to decide if that SS locate should be approved
The hedge can be separated from the client order
For current Nomura limitation, the desk cannot lend the stock from client A to another client B
because if client A want to sell the stock, we need to notified and recall from client B 
but this procedure is not in place, doesn't link them together
that's why now the desk only use the stock from client to pledge as collateral instead
collateral swapping can be done intra-day
TW trade is settled on T+2
if client want to sell the stock, can swap the collateral and get that stock back to client on time
For other better firms, the desk can lend the stock from client A to another client B
if client A want to sell the stock
the system will notify the desk and the desk will do synthetic fill (risk fill on the sell hedge order)
basically the desk is taking risk on the hedge, and manage the size of total risk fill




SBL short depot	SS Locate	Lender Hold	SS Execution	Deficit
Rules
Execution - short depot = Deficit

The deficit then the desk need to take down from Onshore lenders or external. (from the hold)

For TW, as long as there is hold from the onshore lenders, the SS order can be placed. 

the hold is the onshore lender guarantee to reserve that for us. 
approved SS Locate  <= hold -  short depot 

if approved SS locate larger than the short depot + hold, we are over-locate
SS Execution <= approved SS Locate



Questions: How Citibank decide what is in the long depot, what are in the short depot?
