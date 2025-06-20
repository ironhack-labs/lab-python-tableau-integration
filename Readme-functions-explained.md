## main `TabPy` functions implemented


### ✅ **High Price Property Indicator**

I used `SCRIPT_BOOL` with Python code to check if each property’s price is greater than \$100. The script looped through the list of prices and returned `True` or `False` for each, helping identify high-price properties.


SCRIPT_STR("
result = []
for price in _arg1:
    if price < 30:
        result.append('cheap')
    elif price <=80:
         result.append('good price')
    else:
        result.append('expensive')
return result
",
sum([Price])

)

### 3. ✅ **Property Category**

I used `SCRIPT_STR` to categorize properties based on price into `"cheap"`, `"good price"`, or `"expensive"`. The Python code looped through price values, applied conditional checks, and assigned a label accordingly.



SCRIPT_STR("
result = []
for price in _arg1:
    if price < 30:
        result.append('cheap')
    elif price <=80:
         result.append('good price')
    else:
        result.append('expensive')
return result
",
sum([Price])

)



### 4. ✅ **Price Per Review**

I created a `SCRIPT_REAL` calculated field to compute the ratio of price to number of reviews for each listing. The code looped through both lists (prices and reviews) using `zip()`, divided the values, and safely handled cases where the number of reviews was zero by filtering out in the dataset the rows that have 0 reviews.

Note: there is not a 'review' field / column in the dataset. the one that aproximates the best could be 'Number of reviews', any other column does not makes sence for this.

- I filtered out the review that has got 0 Number of reviews

SCRIPT_REAL("
result = []
for price, review in zip(_arg1, _arg2):
    ratio = price / review
    result.append(ratio)

return result
"
,
sum([Price]),
sum([Number Of Reviews])
)

### 5. ✅ **Availability Score**

I implemented `SCRIPT_INT` to assign an availability score between 1 and 5. The script looped through availability values and mapped them to 5 equal ranges (73-day buckets), helping to group listings by availability levels.


SCRIPT_INT("
result = []

for days in _arg1:
    if days <= 73:
        result.append(1)
    elif days <= 146:
        result.append(2)
    elif days <= 219:
        result.append(3)
    elif days <= 292:
        result.append(4)
    else:
        result.append(5)

return result
",
sum([Availability 365])
)
