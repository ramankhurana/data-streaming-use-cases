At the moment README have only the changes made on streaming application notebook to be added in the next push. 

!pip install --upgrade protobuf


project_guid = "e2b6e5b3-cab6-47cc-a753-e655d3ac8ef1"
refit = Refit(project_guid)


import requests
import time
delay_ = 175 ## seconds 
increament=0

def stream_usd(increament, delay=175):
    url = 'https://www.alphavantage.co/query?function=CURRENCY_EXCHANGE_RATE&from_currency=EUR&to_currency=USD&apikey=WEJ426P3DZIP5YNK'
    r = requests.get(url)
    data = r.json()
    usd_val = data["Realtime Currency Exchange Rate"]["9. Ask Price"]
    timestamp = pd.Timestamp (data["Realtime Currency Exchange Rate"]["6. Last Refreshed"])
    timestamp, usd_val
    id='EURtoUSD'
    pd.Timestamp(data["Realtime Currency Exchange Rate"]["6. Last Refreshed"])
    data_row = str(increament) + ","+id+"," + str (timestamp) +","+ usd_val
    #print(data_row)
    
    increament=increament+1
    #print (increament)
    refit.stream_data(data_row)
    time.sleep(delay)
    if usd_val > 1.096:
        return (increament)
    return (stream_usd(increament, delay_))



stream_usd(0,delay_)
