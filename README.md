# MyDataFrame
Extending Pandas DataFrame's with metadata support including unit (e.g. km/h to m/s) conversion.

# Pandas + Pint + MetaData =  MyDataFrame


## Background

1.
Manual unit conversion

    df["Z [g/km]"] = 0.001*df["X [g/s]"] / df["Y [km/h]] / 3600 # WRAAAAAAAAAAAA

What if

    df["Z"] = (df["X"] / df["Y]).to("gram per kilometer")
    df["Z"].unit
    >>> g/km

2.
Passing arguments in plotting

    plt.plot(df["X"],df["Y"],xlabel = "X [g/km]", ylabel = "Y [km/h]", xlim = ....)
    
What if

    df.plot("X", "Y") 
    
units, labels, labels taken care of by default.

3.
Error handling

    is_neg = df["X"] < 0
    df.loc[is_neq,"X"] = np.nan
    # repeat for every column

What if

    # defined centrally for all columns
    df["X"].lower_limit
    >>> 0
    df["X"].upper_limit
    >>> 200   
    
    df = df.enforce_limits()

4.
Documentation

What if
    
    df["X"].info
    >>> "X [g/s] measured with sensor AAAA. Call Guus at 0642114412 for more info."
