# Remove Leading and Trailing Spaces

1. `str.strip()` removes both leading and trailing spaces.
2. `str.lstrip()` removes leading spaces (at beginning).
3. `str.rstrip()` removes trailing spaces (at end).

```
df1 = pd.DataFrame({'y1': [' jack', 'jill ', ' jesse ', 'frank ']})
df1['both']=df1['y1'].str.strip()
df1['left']=df1['y1'].str.lstrip()
df1['right']=df1['y1'].str.rstrip()

```

```
        y1   both    left   right
0     jack   jack    jack    jack
1    jill    jill   jill     jill
2   jesse   jesse  jesse    jesse
3   frank   frank  frank    frank

```