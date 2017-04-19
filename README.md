
# Python binding for theyworkforyou.com API

Adaptation of Paul Doran's [twfython](http://code.google.com/p/twfython/). Now works in Python 2/3.

You will need an API key to use the theyworkforyou.com API, get one here http://www.theyworkforyou.com/api/key 

For more info on the theyworkforyou.com API see http://www.theyworkforyou.com/api/

Install with pip using:

```
pip install -e git+https://github.com/ajparsons/twfy_python.git#egg=twfy_python
```

Example:

```python
from twfy_python import TheyWorkForYou

twfy = TheyWorkForYou(TWFY_KEY)

#get one user from id
t_may = twfy.api.getPerson(id="10426")
for p in t_may:
    print (p["full_name"] + p["left_house"])
```

```python
import six
from twfy_python import TheyWorkForYou

twfy = TheyWorkForYou(TWFY_KEY)
#Get list of all MPs
#A date between '01/05/1997' and todays date.
mp_list = twfy.api.getMPs(date='01/08/2016')
results = {}

#Count the number of MPs for each party.
for mp in mp_list:
    party =  mp['party']
    if party in results.keys():
        results[party] += 1
    else:
        results[party] = 1
        
total_seats = float(sum(results.values()))

#Print the results.
for k, v in six.iteritems(results):
    print (k, ' = ', (v/total_seats)*100, '%')
```
