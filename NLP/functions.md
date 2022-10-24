#### Useful functions for NLP

- [Remove characters from text](#remove-characters-from-text)
- [Generate n-grams](#generate-n-grams)


### Remove characters from text
```python
import re

def remove_chars(text):
    """
    Removes unwanted characters defined inthe chars_to_remove list, from
    a string. Can help with processing a text document like a CV for NLP tasks.
    It also removes numbers and email addresses.
    
    Params
    ------
    text: (str) The text from which to remove the characters/
    
    Returns
    -------
    text: (str) The text without the unwanted characters.
    """
    chars_to_remove = [
        '\s{2,}', '\uf0b7', '–', '/', ':', '%', '“', '”', r"\(", r"\)",
        r"\+", r"\.", r"\,", r"\'", r"\|", r"\▪", r'\"', r'\-', r'\&', r'\²',
        r'\•', r'\…', r'\#', r'\«', r'\»', r'\;', r'\*', r'\©', r'\_', r'\uf0fc',
        r'\uf020', r'\t', r'\uf076', r'\uf0d8', r'\ue91e', r'\ue964', r'\ue947',
        r'\ue9a5', r'\uf0c0', r'\ue92e', r'\ue9ae', r'\uf09a', r'\ue971', r'\uf1ab',
        r'\uf0a7', r'\xa0Fall', r'\xa0480752', r'\xa0732', r'\xa0Key', r'\xa02013',
        r'\xa0', r'\➢', r'\[', r'\]', r'\uf0aa', r'\uf0a8', r'\uf0a2', r'\®', r'\uf046',
        r'\‘', r'\’', r'\·', r'\✓', r'\uf096', r'\‟', r'\„', r'\?', r'\´', r'\uf06e',
        r'\u200b', r'\ビ', r'\ン', r'\シ', r'\ワ', r'\タ', r'\グ', r'\リ', r'\ダ', r'\カ',
        r'\xad301', r'\xad5', r'\xad80', r'\xad4816', r'\xad', r'\〒', r'\uf06c', r'\❑',
        r'\Ø', r'\◆', r'\✉', r'\➔', r'\●', r'\\', r'\📞', r'\📧', r'\🏠', r'\›', r'\│',
        r'\│', r'\~', r'\<', r'\>', r'\!', r'\♦', r'\❖', r'\—', r'\★', r'\uf07d', r'\uf02a',
        r'\uf02a', r'\uf0ad', r'\uf03a', r'\uf029', r'\x00', '\ufb01', '\ufb00', '\ufb02',
        " \d+", r'[A-Za-z0-9]*@[A-Za-z]*\.?[A-Za-z0-9]*',
    ]
    for c in chars_to_remove:
        text = re.sub(c, ' ', text)
    return text
```

### Generate n-grams
```python
def nGrams(text, n=2, words_length=0):
    """
    Create grams of order n.
    
    Parameters:
    ----------
    text: (str) The text that the n-grams will be generated for.
    n: (int) The order of the n-gram (eg. 3 for 3-grams) - Default: 2
    words_legnth: (int) The min length of words to be considered.
    
    Returns:
    --------
    ngrams: (list) A list of the n order grams.
    """
    ngrams = []
    words = text.split(" ")
    valid_words = []
    for word in words:
        if len(word) > words_length:
            valid_words.append(word)
    for i in range(len(valid_words)-(n-1)):
        s = ""
        for j in range(n):
            s += valid_words[i+j] + " "
        ngrams.append(s)
    return ngrams
```
