---
type: slides
---

# Quick Viz with Pandas\!

Notes: Script here.

<html>

<audio controls >

<source src="placeholder_audio.mp3" />

</audio>

</html>

---

If we want to visualize things using different plots we can do that
pretty quickly and with little code\! Take `manufacturer_freq` object we
made in the last deck of slide.

``` python
freq_mfr_df
```

```out
    ##    freq
    ## K    23
    ## G    22
    ## P     9
    ## R     8
    ## Q     8
    ## N     6
    ## A     1
```

This would be great to express as a bar chart. But how do we do it?

Notes: Script here.

<html>

<audio controls >

<source src="placeholder_audio.mp3" />

</audio>

</html>

---

1.  We take the dataframe we wish to plot, in this case `freq_mfr_df`.  
2.  Next we add `.plot` since we want to plot it\!  
3.  But what kind of plot do we want?\! A bar chart in this case would
    work nicely so lets add `.bar()` after
that

<!-- end list -->

``` python
freq_mfr_df.plot.bar()
```

<img src="module1/module1_24/unnamed-chunk-4-1.png" width="672" />

``` out
   
```

<img src="module1/module1_24/unnamed-chunk-5-1.png" width="672" />

The important things to notice here is that we want to `.plot` a
`.bar()` graph.

Notes: Script here.

<html>

<audio controls >

<source src="placeholder_audio.mp3" />

</audio>

</html>

---

What else can we plot from our original cereal dataframe named `df`?
Maybe we want to see the relationship between `sugars` and `calories` in
cereals?  
This would require a `scatter` plot\! In the code we would need to
specify the x and y axis which means we would need to specify the column
names for each axis. We are going to call it
`sug_cal_scatter1`.

``` python
df.plot.scatter(x='sugars', y='calories')
```

<img src="module1/module1_24/unnamed-chunk-6-1.png" width="672" />

``` out
  
            
```

<img src="module1/module1_24/unnamed-chunk-7-1.png" width="672" />

Notes: Script here.

<html>

<audio controls >

<source src="placeholder_audio.mp3" />

</audio>

</html>

---

Something you may have noticed is that there are 77 cereals but there
doesn’t seem to be 77 data points\! That’s because some of them are
lying on top of each other with the same sugar ar calorie values. It may
be of use to set an opacity to the graph to differential those points.
Opacity is set with the argument `alpha` and accepts values between 0
and 1, 1 being full
intensity.

``` python
df.plot.scatter(x='sugars',y='calories', alpha= 0.3)
```

<img src="module1/module1_24/unnamed-chunk-8-1.png" width="672" />

``` out
                               
```

<img src="module1/module1_24/unnamed-chunk-9-1.png" width="672" />

Notes: Script here.

<html>

<audio controls >

<source src="placeholder_audio.mp3" />

</audio>

</html>

---

Look at that\! Now we can see there are multiple cereals that have 2.5g
of sugar with 100 calories. What if we wanted to change the colour to
purple? Enter parameter `color`\! We can also add a bit of readability
by separating the arguments into separate lines.

``` python
df.plot.scatter(x="sugars", 
                y="calories", 
                alpha= .3, 
                color= "purple")
```

<img src="module1/module1_24/unnamed-chunk-10-1.png" width="672" />

``` out
                                   
```

<img src="module1/module1_24/unnamed-chunk-11-1.png" width="672" />

Notes: Script here.

<html>

<audio controls >

<source src="placeholder_audio.mp3" />

</audio>

</html>

---

Those data points look pretty small. To enlarge them, the argument `s`
should do the trick. Also every good graph should havew a title\! Let’s
take this opportunity to finish off this graph and set the argument
`title` to something as well.

``` python
df.plot.scatter(x="sugars",
                y="calories",
                alpha= 0.3, 
                color="purple",
                s= 80, 
                title = "The relationship between sugar and calories in cereals")
```

<img src="module1/module1_24/unnamed-chunk-12-1.png" width="672" />

``` out
                        
                              
```

<img src="module1/module1_24/unnamed-chunk-13-1.png" width="672" />

Notes: Script here.

<html>

<audio controls >

<source src="placeholder_audio.mp3" />

</audio>

</html>

---

# let’s apply what we learned\!

Notes: Script here

<html>

<audio controls >

<source src="placeholder_audio.mp3" />

</audio>

</html>