# Data Manipulation with Pandas

## Transforming Data Frames

### Inspecting a DataGFrame
```.head()``` -- returns the first few rows (head)  
```.info()``` -- shows the information on each of the columns, such as data type and number of missing values     
```.shape```  -- returns the number of rows and columns of the DataFrame     
```.describe()``` -- calculates a few summary statistics for each column     

### Parts of a DataFrame
```.values```  -- A two-dimensional NumPy array of values    
```.columns``` -- An index of columns: the column names      
```.index```   -- An index for the rows: either row numbers or row names     

### Sorting rows 
```df.sort_values()``` -- sort the rows by passing a column name.    
``` df.sort_values([ , ])``` -- sort multiple columns    
```python
# Sort homelessness by region, then descending family members
homelessness_reg_fam = homelessness.sort_values(["region","family_members"], ascending=[True, False]
)

# Print the top few rows   
print(homelessness_reg_fam.head())
```

### Subsetting columns 
```[]``` -- select only the columns that you need. 
```df[" "]``` 

#### filtering rows / selecting rows 
```python
# Filter for rows where family_members is less than 1000 
# and region is Pacific
fam_lt_1k_pac = homelessness[(homelessness["family_members"] < 1000) & (homelessness["region"] == "Pacific")]

# See the result
print(fam_lt_1k_pac)
```

### Subsetting rows by categorical variables 
```python
# The Mojave Desert states
canu = ["California", "Arizona", "Nevada", "Utah"]

# Filter for rows in the Mojave Desert states
mojave_homelessness = homelessness[homelessness["state"].isin(canu)]

# See the result
print(mojave_homelessness)
```

### Adding new columns
adding names, such as transforming, mutating, feature engineering 
```python
# Add total col as sum of individuals and family_members
homelessness["total"] = homelessness["individuals"] + homelessness[ "family_members"]

# Add p_individuals col as proportion of total that are individuals
homelessness["p_individuals"] = homelessness["individuals"] / homelessness["total"]

# See the result
print(homelessness)
```

### example:
```python 
# Create indiv_per_10k col as homeless individuals per 10k state pop
homelessness["indiv_per_10k"] = 10000 * homelessness["individuals"] / homelessness["state_pop"] 

# Subset rows for indiv_per_10k greater than 20
high_homelessness = homelessness[homelessness["indiv_per_10k"] > 20]

# Sort high_homelessness by descending indiv_per_10k
high_homelessness_srt = high_homelessness.sort_values("indiv_per_10k", ascending=False)

# From high_homelessness_srt, select the state and indiv_per_10k cols
result = high_homelessness_srt[["state", "indiv_per_10k"]]

# See the result
print(result)
```

