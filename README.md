# <ins>Data_Analysis-NYC_Public_School</ins>
Analyzing test scores data across New York City's public schools with pandas

## <ins>Importing libraries and Loading the CSV file</ins>
```python
import pandas as pd
# Read in the data
schools = pd.read_csv("schools.csv")
```

## <ins>Preview first five data with .head() </ins>
```python
# Preview first 5 data of dataset
schools.head()
```

![image](https://github.com/yavuzCodiin/Data_Analysis-NYC_Public_School/assets/82445309/ec976040-7f60-469c-bfe7-658781db19d0)

## <ins>Best schools for math?</ins>
```python
best_math_schools = schools[schools["average_math"] >= 640][["school_name", "average_math"]].sort_values("average_math", ascending=False)
```

![image](https://github.com/yavuzCodiin/Data_Analysis-NYC_Public_School/assets/82445309/af0d120c-d3d2-411d-8a17-b3e3fe335280)

## <ins>total_SAT per school</ins>
```python
schools["total_SAT"] = schools["average_math"] + schools["average_reading"] + schools["average_writing"]
schools
```

![image](https://github.com/yavuzCodiin/Data_Analysis-NYC_Public_School/assets/82445309/2dc03fd1-272b-4287-a938-aa21db137272)

## <ins>Top 10 performing schools</ins>
```python
top_10_schools = schools.groupby("school_name", as_index=False)["total_SAT"].mean().sort_values("total_SAT", ascending=False).head(10)
```

![image](https://github.com/yavuzCodiin/Data_Analysis-NYC_Public_School/assets/82445309/f3d29d2c-88c3-4e97-bdeb-68aa8a27147c)

## <ins>Borough comparison for highest standard deviation for total_SAT</ins>
```python
boroughs = schools.groupby("borough")["total_SAT"].agg(["count", "mean", "std"]).round(2)
```

![image](https://github.com/yavuzCodiin/Data_Analysis-NYC_Public_School/assets/82445309/79d8c0b1-daf2-4920-a3ce-a31d345f8152)

## <ins>Filtering for max std</ins>
```python
largest_std_dev = boroughs[boroughs["std"] == boroughs["std"].max()]
```

![image](https://github.com/yavuzCodiin/Data_Analysis-NYC_Public_School/assets/82445309/6715a915-599c-471e-99f4-c74c66bd6e2e)

## <ins>Column Configuration</ins>
```python
largest_std_dev = largest_std_dev.rename(columns={"count": "num_schools", "mean": "average_SAT", "std": "std_SAT"})
largest_std_dev
```

![image](https://github.com/yavuzCodiin/Data_Analysis-NYC_Public_School/assets/82445309/ec1ec3f6-aa09-4e83-a8ee-c0ffd04cd5db)









