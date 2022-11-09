### Functions
Plot the distribution of values in a Pandas DataFrame
```python
import pandas as pd
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

Parse GMails
```python
import imaplib,email,getpass
import pandas as pd
import os,sys
from IPython.display import clear_output
    

def parser_email(useremail, password, output_csv, connection="INBOX"):
    """
    Function that parses gmails and stores them in an Excel File
    
    Params
    ------
    email: The gmail (eg. someone@gmail.com)
    password: The two-way authentication password
    connection: The type of gmail folder (default= "INBOX")
                Example Options
                "INBOX", "[Gmail]","[Gmail]/All Mail", "[Gmail]/Drafts", "[Gmail]/Important",
                 "[Gmail]/Sent Mail","[Gmail]/Spam", "[Gmail]/Starred", "[Gmail]/Trash"
    output_excel_file: The file path of the excel file where data is stored.
    """
    
    imap_url ="imap.gmail.com"
    con = imaplib.IMAP4_SSL(imap_url)
    con.login(useremail, password)

    con.select(f'{connection}')
    result, data = con.uid('search',None,'ALL')
    mails=data[0].split()
    
    df = pd.DataFrame()
    Subject = []
    DeliveredTo = []
    From = []
    From_Email = []
    Date = []
    ContentType = []
    Content = []
    
    counter = 1
    for j, i in enumerate(mails):
        e_result, e_data = con.uid('fetch' ,i,'(RFC822)')
        raw_email = e_data[0][1].decode("utf-8")
        email_msg = email.message_from_string(raw_email)
        lines = str(email_msg).split('\n')
        subject = None
        Delivered_To = None
        From_ = None
        date = None
        content_type = None
        content_start_line_idx = None
        content_end_line_idx = None
        content_signature = None
        line_idx = 0
        for line in lines:
            if line.split(':')[0] == 'Subject':
                subject = line.split(':')[1]

            if line.split(':')[0] == 'Delivered-To':
                Delivered_To = line.split(':')[1]

            if line.split(':')[0] == 'From':
                From_ = line.split(':')[1]

            if line.split(':')[0] == 'Date':
                date = line.split(':')[1].split(' ')[1:-2]

            if line.split(':')[0] == 'Content-Type':
                content_type = line.split(':')[1].split(';')[0]

            if line == 'Content-Type: text/plain; charset="UTF-8"':
                content_start_line_idx = line_idx

            if line == 'Content-Type: text/html; charset="UTF-8"':
                content_end_line_idx = line_idx

            c = None
            if content_start_line_idx and content_end_line_idx:
                c  = ' '.join(lines[content_start_line_idx:content_end_line_idx][2:-2])
            line_idx += 1
            
        Subject.append(subject)
        DeliveredTo.append(Delivered_To)
        From.append(From_)
        try: 
            From_Email.append(From_.split('<')[1].replace('>', ''))
        except:
            From_Email.append(From_)
        Date.append(date)
        ContentType.append(content_type)
        Content.append(c)
        
        counter += 1
        
        print(f"Parsed {counter}/{len(mails)} [{(counter/len(mails))*100:.2f}%] emails [Working in Gmail folder: {connection}]")
        clear_output(wait=True)
        
    df['Subject'] = Subject
    df['DeliveredTo'] = DeliveredTo
    df['From'] = From
    df['From_Email'] = From_Email
    df['Date'] = Date
    df['ContentType'] = ContentType
    df['Content'] = Content
    df.to_csv(output_csv)
    
    print('Job completed')
```
