At the moment README have only the changes made on streaming application notebook to be added in the next push. 

!pip install --upgrade protobuf


project_guid = "e2b6e5b3-cab6-47cc-a753-e655d3ac8ef1"
refit = Refit(project_guid)


import requests
import time
delay_ = 175 ## seconds 
increament=0

def stream_usd(increament, delay=175):
    url = 'https://www.alphavantage.co/query?function=CURRENCY_EXCHANGE_RATE&from_currency=EUR&to_currency=USD&apikey='
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





****
def stream_usd_fromfile():
    from csv import reader
    count = 100
    with open('EURtoUSD_data.csv', 'r') as read_obj:
        csv_reader = reader(read_obj)
        is_header = True
        # Iterate over each row in the csv using reader object
        for row in csv_reader:
            if not is_header and count:
                data = ",".join(row)
                print(data)
                refit.stream_data(data)
                count -= 1
            else:
                is_header = False



import csv
import random
from datetime import datetime, timedelta

# Define the start date
start_date = datetime(2023, 1, 1, 0, 0, 0)

# Open the csv file in write mode
with open('EURtoUSD_data.csv', 'w', newline='') as file:
    writer = csv.writer(file)
    #writer.writerow(["index", "sensor_name", "timestamp", "value"])

    for i in range(1000):  # for each minute in a year (60 * 24 * 365 = 525600)
        # Calculate the current date and time
        current_date = start_date + timedelta(minutes=i)
        
        # Generate a random value between 0.9 and 1.23
        value = random.uniform(0.9, 1.23)
        
        # Write the data to the csv file
        writer.writerow([i, "EURtoUSD", current_date.strftime("%Y-%m-%d %H:%M:%S"), format(value, ".8f")])


