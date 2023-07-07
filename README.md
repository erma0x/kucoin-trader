# kucoin-trader
Kucoin trading module with python3 and ccxt

# Description

This is a high-level overview of the code provided. It demonstrates how to use the KuCoin Futures API to execute trading strategies.

### string to float prices

The string_to_float_prices function is used to convert the prices in the op_data_structure dictionary from strings to floats. It takes a dictionary as input and converts the values of the 'entry_prices', 'take_profits', and 'stop_losses' keys to floats. The updated dictionary is then returned.
Trader Function


### Sort orders
sort_orders(op_data_structure)
This function takes a parameter op_data_structure, which is a dictionary containing information about orders. It sorts the take_profits and stop_losses lists within the op_data_structure dictionary based on the value of the 'side' key.
If the value of 'side' is equal to 'buy', it sorts the take_profits list in ascending order and the stop_losses list in descending order. Otherwise, it sorts the take_profits list in descending order and the stop_losses list in ascending order.

The trader_kucoinfutures function is the main function for executing trades on the KuCoin Futures platform. It takes the order_data, exchange, and maintenance_capital as input parameters.

### Rebalancing Orders

The order_data is first passed through the string_to_float_prices function to convert the prices to floats. Then, the order_data is sorted using the sort_orders function.

### Getting Available Balance

The function calls the get_amount_position_usdt function to get the available balance in USDT.

### Checking Free Balance

The function checks if the free balance on the exchange is greater than (1+maintenance_capital) * amount_usd_position. If it is not, the function returns None.

### Looping through Entry Prices

The function then loops through each entry price in the order_data['entry_prices'] list. For each entry price, it calculates the amount_token_position based on the available balance and the number of entry prices.

### Entry Long Order

The function creates a limit order for entering a long position using the create_limit_order function from the exchange object. It uses the order_data['symbol'], order_data['side'], amount_token_position, and entry_price as parameters. It also includes additional parameters such as leverage and forceHold.

### Take Profit Orders

The function calculates the quantities for take profit orders using the balance_kucoinfutures_contract_quantity function. It then loops through each take profit price in the order_data['take_profits'] list and creates a limit order for each take profit using the create_limit_order function. It uses the opposite side of the entry order, the calculated quantity, and the take profit price as parameters. It also includes additional parameters such as leverage, reduceOnly, and stopPrice.

### Stop Loss Orders

The function calculates the quantities for stop loss orders using the balance_kucoinfutures_contract_quantity function. It then loops through each stop loss price in the order_data['stop_losses'] list and creates a limit order for each stop loss using the create_limit_order function. It uses the opposite side of the entry order, the calculated quantity, and the stop loss price as parameters. It also includes additional parameters such as leverage, reduceOnly, stopPriceType, and stopPrice.

