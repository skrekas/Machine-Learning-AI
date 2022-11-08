#### Functions
Plot the distribution of values in a Pandas DataFrame
```python
from plotly.subplots import make_subplots
import plotly.graph_objects as go

def df_dist(csv_path, threshold=50, ncols=2):
    """
    Plots the distribution of values in each column of a dataframe.
    :param csv_path: The file path of the cav  file for which to plot the distribution of values.
    :param threshold: Threshold for the number of categories in each column. If the number
                      of categories is above this threshold, the column is ignored since
                      the plot bar will be confusing/unclear.
    :param ncols: The number of column in the plot. Rows are adjusted accordingly.
    :return: None
    """
    # Find columns to keep
    keep_cols = []
    df = pd.read_csv(csv_path)
    for col in list(df.columns.unique()):
        if len(df[col].unique()) <= threshold:
            keep_cols.append(col)

    rows = round(len(keep_cols) / ncols)
    fig = make_subplots(rows=rows, cols=ncols, subplot_titles=keep_cols)
    idx = 0
    for i in range(rows):
        for j in range(ncols):
            fig.add_trace(go.Bar(
                x=df[keep_cols[idx]].value_counts().index,
                y=df[keep_cols[idx]].value_counts().values,
                text=df[keep_cols[idx]].value_counts().values, width=0.8
            ), row=(i+1), col=(j+1))
            idx += 1
    fig.update_xaxes(title="Categories", showline=True, linecolor='#757575', linewidth=1)
    fig.update_yaxes(title="<b>Num. of Rows</b>", showline=True, linecolor='#757575', linewidth=1)
    fig.update_layout(template='plotly_white', height=rows*350, showlegend=False)
    fig.show()

```
