Useful function to remove unwanted characters from some text.
```python
def remove_chars(text):
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
        r'\uf02a', r'\uf0ad', r'\uf03a', r'\uf029', r'\x00',
        " \d+", r'[A-Za-z0-9]*@[A-Za-z]*\.?[A-Za-z0-9]*',
    ]
    for c in chars_to_remove:
        text = re.sub(c, ' ', text)
    return text
```