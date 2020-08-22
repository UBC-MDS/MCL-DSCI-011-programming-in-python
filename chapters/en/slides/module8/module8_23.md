---
type: slides
---

# More Advanced String Processing

Notes: Script here

<html>

<audio controls >

<source src="/placeholder_audio.mp3" />

</audio>

</html>

---

Ok, we have an idea on how we can do some fairly standard strings
processing, however, it’s time we dived a little deeper into this.

There are **MANY** different functions but I want to concentrate on a
couple here that you will use often and give you a list of several that
you may need in your future string processing days.

Notes: Script here

<html>

<audio controls >

<source src="/placeholder_audio.mp3" />

</audio>

</html>

---

## Replace

Just like in regular text, there will be times in your data analysis
where you will want to replace some of the text within a string.  
That’s where `.replace()` comes in. We usually like our data to be
consistent, however, consistency is not also present even in the best of
dataframes. Let’s take a look at our cycling dataset:

``` python
cycling = pd.read_csv('cycling_data.csv')
cycling.head(9)
```

```out
               Date            Name  Type  Time  Distance                      Comments
0   2019-09-10 0:13  Afternoon Ride  Ride  2084     12.62                          Rain
1  2019-09-10 13:52    Morning Ride  Ride  2531     13.03                          rain
2   2019-09-11 0:23  Afternoon Ride  Ride  1863     12.52     Wet road but nice weather
3  2019-09-11 14:06    Morning Ride  Ride  2192     12.84  Stopped for photo of sunrise
4   2019-09-12 0:28  Afternoon Ride  Ride  1891     12.48  Tired by the end of the week
5  2019-09-16 13:57    Morning Ride  Ride  2272     12.45     Rested after the weekend!
6   2019-09-17 0:15  Afternoon Ride  Ride  1973     12.45          Legs feeling strong!
7  2019-09-17 13:43    Morning Ride  Ride  2285     12.60                       Raining
8  2019-09-18 13:49    Morning Ride  Ride  2903     14.57                 Raining today
```

In the first 10 rows of this dataset, there are multiple ways that
“rain” appears in the `Comments` column. Let’s attempt to add some
consistency to this.

Notes: Script here

<html>

<audio controls >

<source src="/placeholder_audio.mp3" />

</audio>

</html>

---

Before we do anything, let’s convert this whole column to lowercase, to
make our life easier. This means we only need to be replacing 1 version
of a single word instead of taking consideration all different case
versions.

``` python
cycling_lower = cycling.assign(Comments = cycling['Comments'].str.lower())
cycling_lower.head(9)
```

```out
               Date            Name  Type  Time  Distance                      Comments
0   2019-09-10 0:13  Afternoon Ride  Ride  2084     12.62                          rain
1  2019-09-10 13:52    Morning Ride  Ride  2531     13.03                          rain
2   2019-09-11 0:23  Afternoon Ride  Ride  1863     12.52     wet road but nice weather
3  2019-09-11 14:06    Morning Ride  Ride  2192     12.84  stopped for photo of sunrise
4   2019-09-12 0:28  Afternoon Ride  Ride  1891     12.48  tired by the end of the week
5  2019-09-16 13:57    Morning Ride  Ride  2272     12.45     rested after the weekend!
6   2019-09-17 0:15  Afternoon Ride  Ride  1973     12.45          legs feeling strong!
7  2019-09-17 13:43    Morning Ride  Ride  2285     12.60                       raining
8  2019-09-18 13:49    Morning Ride  Ride  2903     14.57                 raining today
```

Notes: Script here

<html>

<audio controls >

<source src="/placeholder_audio.mp3" />

</audio>

</html>

---

```out
               Date            Name  Type  Time  Distance              Comments
6   2019-09-17 0:15  Afternoon Ride  Ride  1973     12.45  legs feeling strong!
7  2019-09-17 13:43    Morning Ride  Ride  2285     12.60               raining
8  2019-09-18 13:49    Morning Ride  Ride  2903     14.57         raining today
9   2019-09-18 0:15  Afternoon Ride  Ride  2101     12.48       pumped up tires
```

Let’s replace the word `raining` with just `rain` in the entire
dataset.  
In `replace()`, the first argument is the word we are identifying, and
the second is the one that we are replacing it with.

``` python
cycling_rain = cycling_lower.assign(Comments = cycling_lower['Comments'].str.replace('raining', 'rain'))
cycling_rain.head(9)
```

```out
               Date            Name  Type  Time  Distance                      Comments
0   2019-09-10 0:13  Afternoon Ride  Ride  2084     12.62                          rain
1  2019-09-10 13:52    Morning Ride  Ride  2531     13.03                          rain
2   2019-09-11 0:23  Afternoon Ride  Ride  1863     12.52     wet road but nice weather
3  2019-09-11 14:06    Morning Ride  Ride  2192     12.84  stopped for photo of sunrise
4   2019-09-12 0:28  Afternoon Ride  Ride  1891     12.48  tired by the end of the week
5  2019-09-16 13:57    Morning Ride  Ride  2272     12.45     rested after the weekend!
6   2019-09-17 0:15  Afternoon Ride  Ride  1973     12.45          legs feeling strong!
7  2019-09-17 13:43    Morning Ride  Ride  2285     12.60                          rain
8  2019-09-18 13:49    Morning Ride  Ride  2903     14.57                    rain today
```

We can see that the word “raining” has become `rain` in row 7 and 8\!

Notes: Script here

<html>

<audio controls >

<source src="/placeholder_audio.mp3" />

</audio>

</html>

---

## Contains

`contains()` can be used to filter our dataframe. Instead of checking if
a column equals an exact value, we can check in a pattern is
***contained*** in the column. For example, what if we want all the rows
that have some portion of “rain”.

``` python
cycling_lower['Comments'].str.contains('rain')
```

```out
0      True
1      True
2     False
3     False
4     False
      ...  
28    False
29    False
30    False
31    False
32    False
Name: Comments, Length: 33, dtype: bool
```

This will return a pandas series with Boolean values.

Notes: Script here

<html>

<audio controls >

<source src="/placeholder_audio.mp3" />

</audio>

</html>

---

``` python
cycling_lower[cycling_lower['Comments'].str.contains('rain')]
```

```out
                Date            Name  Type  Time  Distance       Comments
0    2019-09-10 0:13  Afternoon Ride  Ride  2084     12.62           rain
1   2019-09-10 13:52    Morning Ride  Ride  2531     13.03           rain
7   2019-09-17 13:43    Morning Ride  Ride  2285     12.60        raining
8   2019-09-18 13:49    Morning Ride  Ride  2903     14.57  raining today
18   2019-09-26 0:13  Afternoon Ride  Ride  1860     12.52        raining
```

Here we see all the rows that contain the pattern `rain` even if they
did not match directly. We can then use this subset to see if our
cyclist Tom, was slower on average, on days that it rained\!

Notes: Script here

<html>

<audio controls >

<source src="/placeholder_audio.mp3" />

</audio>

</html>

---

`.replace()` can be somewhat limiting since we saw it can only replace
specific strings that we specify. What if we want to replace any of the
values in the entire dataframe that contains the word `"rain"` to the
word `"rained"`?

We actually know how to do this\! We can pair our `.contains()` function
with conditional value replacement using `.loc[]`\! We learned this back
in module 2. Let’s see what this looks like.

let’s replace all rows with values that only contains `"rain"` with
`"rained"`:

``` python
cycling_lower.loc[cycling_lower['Comments'].str.contains('rain'), 'Comments'] = 'rained'
```

What does `cycling_lower` look like now?

Notes: Script here

<html>

<audio controls >

<source src="/placeholder_audio.mp3" />

</audio>

</html>

---

The rows originally filtered with “rain” in the dataset:

```out
                Date            Name  Type  Time  Distance       Comments
0    2019-09-10 0:13  Afternoon Ride  Ride  2084     12.62           rain
1   2019-09-10 13:52    Morning Ride  Ride  2531     13.03           rain
7   2019-09-17 13:43    Morning Ride  Ride  2285     12.60        raining
8   2019-09-18 13:49    Morning Ride  Ride  2903     14.57  raining today
18   2019-09-26 0:13  Afternoon Ride  Ride  1860     12.52        raining
```

Have now been been been replaced with “rained” in the `Comments` column:

``` python
cycling_lower.head(9)
```

```out
               Date            Name  Type  Time  Distance                      Comments
0   2019-09-10 0:13  Afternoon Ride  Ride  2084     12.62                        rained
1  2019-09-10 13:52    Morning Ride  Ride  2531     13.03                        rained
2   2019-09-11 0:23  Afternoon Ride  Ride  1863     12.52     wet road but nice weather
3  2019-09-11 14:06    Morning Ride  Ride  2192     12.84  stopped for photo of sunrise
4   2019-09-12 0:28  Afternoon Ride  Ride  1891     12.48  tired by the end of the week
5  2019-09-16 13:57    Morning Ride  Ride  2272     12.45     rested after the weekend!
6   2019-09-17 0:15  Afternoon Ride  Ride  1973     12.45          legs feeling strong!
7  2019-09-17 13:43    Morning Ride  Ride  2285     12.60                        rained
8  2019-09-18 13:49    Morning Ride  Ride  2903     14.57                        rained
```

rows 0, and 1 which both had values of `"rain"` and Rows 7 and 8 which
were both `"raining"` and `"raining today"` repectively have now all
been changed to the value `"rained"`.

Notes: Script here

<html>

<audio controls >

<source src="/placeholder_audio.mp3" />

</audio>

</html>

---

There are quite a few other string methods that are available but this
should get you started.

Here is a table of some of the other string processing possibilities
available.

| verb                                                                                                                                                              | description                                                                      |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| [`.cat()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.str.cat.html?highlight=cat#pandas.Series.str.cat)                             | Concatenate strings in different columns with given separator                    |
| [`.contains()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.str.contains.html?highlight=contains#pandas.Series.str.contains)         | Return Boolean series if each string contains the specified pattern              |
| [`.count()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.str.count.html?highlight=count#pandas.Series.str.count)                     | Count occurrences of pattern                                                     |
| [`.get()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.str.get.html?highlight=get#pandas.Series.str.get)                             | obtains the element from each row at specified position. (retrieve i-th element) |
| [`.join()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.str.join.html?highlight=str%20join#pandas.Series.str.join)                   | Join strings in from a list with passed delimiter                                |
| [`.replace()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.str.replace.html?highlight=replace#pandas.Series.str.replace)             | Replaces each occurrence of a pattern with some other string                     |
| [`.repeat()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.str.repeat.html?highlight=repeat#pandas.Series.str.repeat)                 | Duplicate values (s.str.repeat(3) equivalent to x \* 3)                          |
| [`.slice()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.str.slice.html?highlight=series%20str%20slice#pandas.Series.str.slice)      | Slice each string in the Series given specified arguments                        |
| [`.startswith()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.str.startswith.html?highlight=startswith#pandas.Series.str.startswith) | Test if the start of each string element matches a pattern                       |
| [`.endswith()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.str.endswith.html?highlight=ends#pandas-series-str-endswith)             | Test if the end of each string element matches a pattern                         |
| [`.findall()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.str.findall.html)                                                         | Finds all occurrences of pattern in the Series and returns them as a list.       |
| [`.len()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.str.len.html?highlight=len#pandas.Series.str.len)                             | Computes the length of each element in the Series/Index                          |

Notes: Script here

<html>

<audio controls >

<source src="/placeholder_audio.mp3" />

</audio>

</html>

---

| verb                                                                                                                                              | description                                                                                                       |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| [`.strip()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.str.strip.html#pandas-series-str-strip)                     | Strips whitespaces or a set of specified characters from each string in the Series/Index from left and right side |
| [`.lstrip()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.str.lstrip.html#pandas-series-str-lstrip)                  | Strip whitespaces or a set of specified characters from each string in the Series/Index from left side            |
| [`.rstrip()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.str.lstrip.html?highlight=lstrip#pandas-series-str-lstrip) | Strip whitespaces or a set of specified characters from each string in the Series/Index from right side           |
| [`.upper()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.str.lower.html#pandas.Series.str.lower)                     | Convert strings in the Series/Index to uppercase                                                                  |
| [`.lower()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.str.upper.html#pandas-series-str-upper)                     | Convert strings in the Series/Index to lowercase                                                                  |
| [`.title()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.str.title.html#pandas-series-str-title)                     | Converts first character of each word to uppercase and remaining to lowercase                                     |
| [`.capitalize()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.str.capitalize.html#pandas-series-str-capitalize)      | Converts first character to uppercase and remaining to lowercase                                                  |
| [`.swapcase()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.str.swapcase.html#pandas.Series.str.swapcase)            | Converts uppercase to lowercase and lowercase to uppercase                                                        |

Notes: Script here

<html>

<audio controls >

<source src="/placeholder_audio.mp3" />

</audio>

</html>

---

| verb                                                                                                                                                  | description                                   |
| ----------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------- |
| [`.isalnum()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.str.isalnum.html?highlight=isalnum#pandas.Series.str.isalnum) | Check whether all characters are alphanumeric |
| [`.isalpha()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.str.isalpha.html#pandas.Series.str.isalpha)                   | Check whether all characters are alphabetic   |
| [`.isdigit()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.str.isdigit.html#pandas-series-str-isdigit)                   | Check whether all characters are digits       |
| [`.isspace()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.str.isspace.html#pandas.Series.str.isspace)                   | Check whether all characters are digits       |
| [`.islower()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.str.islower.html#pandas-series-str-islower)                   | Check whether all characters are uppercase    |
| [`.isupper()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.str.isupper.html#pandas.Series.str.isupper)                   | Check whether all characters are lowercase    |
| [`.istitle()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.str.istitle.html#pandas-series-str-istitle)                   | Check whether all characters are titlecase    |
| [`.isnumeric()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.str.isnumeric.html#pandas-series-str-isnumeric)             | Check whether all characters are numeric      |

Notes: Script here

<html>

<audio controls >

<source src="/placeholder_audio.mp3" />

</audio>

</html>

---

# Let’s practice what we learned\!

Notes: Script here

<html>

<audio controls >

<source src="/placeholder_audio.mp3" />