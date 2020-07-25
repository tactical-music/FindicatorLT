# FindicatorLT
An algorithmic trading program exploration which uses TA (Technical Analysis) indicators. Not Financial Advice, this is for educational purposes.  Please read the Licenses for this program as well as the dependencies found in the library area.

FindicatorLT (Light) is a program which can connect to a cryptocurrency market, be aware of a portfolio's content, analyze real time market data from the exchange, and buy or sell assets based on indicators. This version does not include backtesting functionality.

The program is designed to be as light and portable as possible.  Therefore, it is not designed with a UI (User Interface).  Interactions with the program are determined by a Properties configuration file and analyzing the output logs (or monitoring via the programs actions on the exchange.

This program, especially in its current early version state, should absolutely not be used for live trading.  There are certainly some configurations and market conditions in which the program will thrive, but at the least the program is too optimistic. The program would be best used to "catch" breakouts and make purchases, but during favorable market conditions. It will tend to keep buying despite falling trends.

You will need Java 11 or greater to run this program.  While you can run it from your local or laptop computer, it is designed to be run "headless" on a remote server.  The memory footprint is reliatvely light at 500 MB, and file usage should be less than 1GB per month as this version does not include backtesting.

Warning: Parts of this program were written while I was staying in one of the noisiest cities in the world. I am currently reviewing the code and expect to find some very dumb mistakes made after several weeks with little sleep.

Example usage:

Compile project into a jar using the main class StartMarket.   Be sure to include the library jars.

Create a system environmental variable called FINCONFIG which is pointed to a directory of your choice that has the following file:

pro.properties

sandbox.properties

Edit these files to correspond to the API key you created on CBP.  This program only works with that exchange. I am checking into copyright instructions for how and if I can use the full name of the CBP exchange.

Create another directory (pointed to in the .properties files) and copy the files and subfolders you find in the REF/findicator folder here in this project.

Note the vars/vars.properties file and its first few variables. Variables can be changed while the program is running

indibuy=7

buy=false

sell=false

profitsell=1.2

fiatreserve=25.00

"indibuy" is the number of indicators to buy on. There are 11 indicators, and 7 or 8 is a reasonable number.  As stated before, it is not wise to allow the program to keep purchasing when markets turn bearish. It will always buy some at the top and maybe some on the way down.
"buy" and "sell" should be set to true or false depending on your intent.

"profitsell" (if "sell" is true) is the amount of profit you wish to make, including fees of .05% x 2 = .1%.  The LT version of the program will only set sell orders at a fixed percentage over purchase price.

Purchases are automatically placed in as limit orders which split the difference on the BUY and SELL orders on the order book.
The program will give up after one cycle and only put the same order in if indicators are above the indisell variable value, and other assets in the stock.csv file are not "more positive". Each purchase will be for the minimum fiat or asset possible.
fiatreserve is the amount of the base currency (USD, for example) you wish to leave untouched in the portfolio.

In the findicator/csv/stock folder, edit the stock.csv file to correspond to asset pairs you wish to work with. For example:

BTC-USD

ETH-USD

From the location of the jar you have made, run the program in this format:

java -jar findicator.jar FIFTEEN_MINUTE USD SANDBOX ONLYONE

The first argument is the timing period for the program to analyze market data, just as you would choose a candle interval on a market chart.  The possible values are:

MINUTE,
FIVE_MINUTE,
FIFTEEN_MINUTE,
HOURLY,
SIX_HOUR,
DAILY

The second argument is the base currency to use.  If you will be trading BTCUSD and ETHUSD for example, you would choose USD.  If you wanted to trade ETHBTC or LTCBTC, you would choose BTC.

The third argument will be either PRODUCTION or SANDBOX. These correspond to the hard-coded values:

sandbox: https:// api-public.sandbox.pro.coinbase.com
production: https:// api.pro.coinbase.com
(without the extra space)

The last argument is ONLYONE which will cause the program to only buy one asset per interval.  A value of anything except ONLYONE will result in the program buying as many assets per cycle as it sees worth buying until there is no more money in that portfolio or it has bought some of every asset.




