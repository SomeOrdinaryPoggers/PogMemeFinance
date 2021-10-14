# PogMemeFinance
SomeOrdinaryPoggers's 
Tau is a smart contract, that creates an ERC20 token from another one or from a native token.
It is not ownable, meaning the deployer or the developer: SomeOrdinaryPoggers, has no benefit more than the user, except knowing when the contract is deployed, giving the deployer the possibility to invest first.
It has no initial supply.
It has 2 additional variables to the openzepplin ERC20: SellingPricePerTauToken and BuyingPricePerTauToken which give the prices of one token of a tau contract in relation to the token from which it was created(which we will refer from now on as “token From”), the initial selling price is 1 (followed by 18 zeros decimals) and the initial buying price is 1.16...
And it has 4 additionnal functions to the openzepplin ERC20:
-The Buy function allows users to exchange the token From(they go to the contract’s balance) for freshly minted token with the tau contact's address for the price of SellingPricePerTauToken*7/6, meaning there is a 1/7 fee(=14,29%), that gets transfered to the contract together with the other 6/7 , the fee causes the price to increase (except sometimes during flash loans) when the SellingPricePerTauToken gets recalculated at the end of this function. note: there are two variants of this function LowerGasFee is recomended for year 2021.
-The Sell function allows users to burn the tau contract’s tokens in exchange for the tokens From, for the price SellingPricePerTauToken. At the end of this function, the price does not change, because the same proportion of the tau tokens gets burned that the proportion of this contract of token From's balance get sent to the caller(user). Selling using SellTokens can help increase the price of Tau in From, because the contract’s From token balance becomes lower, the fee when buying represents a higher proportion of the balance when the prices get recalculated.
Example with BuyTokens and SellTokens
The contract gets deployed. SellingPricePerTauToken=1000000000000000000
User 1 exchanges 0.0002 WBTC for Tau tokens, they get 0.0002/1*6/7=0.000171428571428571 Tau tokens and SellingPricePerTauToken gets updated to 0.0002/ 0.000171428571428571=1.166666666666669583. (if user 1 resold immediatly they would get 1.166666666666669583* 0.000171428571428571=0.000199999999999999 WBTC=99% of his investment)
User 2 buys Tau tokens with 0.001 WBTC, they get 0.001/1.166666666666669583*6/7=0.000734693877551018 Tau tokens and SellingPricePerTauToken gets updated to (0.0002+0.001)/ (0.000171428571428571+0.000734693877551018)=0.0012/0.000906122448979589=1.324324324324328470. (if user 2 resold immediately they would get 1.324324324324328470* 0.000734693877551018=0.000972972972972972 WBTC=97% of their wbtc investment)
User 1 sells all his tokens for WBTC , they get 1.324324324324328470* 0.000171428571428571=0.000227027027027027 WBTC=114% of their wbtc investment= 14% profit
*note: The Tau contracts remain normal functioning ERC20s, users can buy or sell or provide liquidity on a dex like Uniswap normally without additional fee from the usual.
-The openzepplin FlashMint function which gives flash loan with 0 fee. -The pump it function allows someone to donate the tokens From to the contract(to the TAU token holders), increasing the price without getting any token in return.
Why the name Tau?
Tau is the ratio between the fee and the rest of the sent tokens in the BuyTokens function, also the ratio between the diameter and the circumference of a circle=6(rounded with an algorithm I created).
Why free flash loan?
During a flash loan the borrower sells the borrowed tokens on uniswap then buys back the sold amount on uniswap, doing so they pay a fee in the tau token, and a fee in the tau token’s liquidity pair token. The flash loan rewards liquidity providers of the Tau tokens, this incentivizes buying and providing liquidity.
What will the price on a dex like uniswap be?
The price on a dex should most of the time be between the BuyingPricePerTauTokens and SellingPricePerTauTokens, which means lower (better) buying price and higher (better) selling price than the tau contract’s.
Why is the fee so high?
The 14.29% fee can be considered a fee for whales, or early buyers which technically are whales, whales are used to buying with higher price than market and selling with lower price than market. This is a good deal for them.
How much can I loose with this token, how much can I gain?
The maximum percent in infinite time this token’s dex price could drop in the token From price should be 14.29%, it can increase price in the token From price as long a the contract owns a small percentage of the tonkens From’s total supply, meaning it can in theory many many x. However if we talk in the usd price you have to multiply the tau token’s token From price by the token From’s usd price, meaning if the token From’s usd price decreases or increases, so does the Tau token’s usd price. The contract’s sell and buy prices in tokens From can only increase or remain the same.
Is this contract rug pull proof?
Yes, if the token From’s contract is rug pull proof because the tau contract has no owner who can rug pull. However be careful if a contract has the name Tau but not the same code that I, SomeOrdinaryPoggers designed.
Is this contract hackable?
Not intentionally, at least.
