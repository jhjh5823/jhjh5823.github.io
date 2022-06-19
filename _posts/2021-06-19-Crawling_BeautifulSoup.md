# Crawling - BeautifulSoup


```python
from bs4 import BeautifulSoup
```


```python
with open('00.Example.html') as file:
  soup = BeautifulSoup(file, 'html.parser')

soup
```

* find() : 해당 조건에 맞는 하나의 태그를 가져옴 중복시에는 첫번째 것만 가져온다.


```python
soup.find('p')
```




    <p>a</p>




```python
soup.find('div')
```




    <div>
    <p>a</p><p>b</p><p>c</p>
    </div>




```python
soup.find('ul')
```




    <ul>
    <li>삼겹살</li>
    <li>치킨</li>
    <li>비빕밥</li>
    </ul>



* find_all() 조건에 맞는 모든 태그를 리스트 형태로 반환


```python
all_ps = soup.find_all('p')
```


```python
all_ps
```




    [<p>a</p>,
     <p>b</p>,
     <p>c</p>,
     <p>X</p>,
     <p>Y</p>,
     <p>Z</p>,
     <p>1</p>,
     <p>2</p>,
     <p>3</p>,
     <p>This is a paragraph.</p>]




```python
len(all_ps)
```




    10




```python
divs = soup.find_all('div')
divs
```




    [<div>
     <p>a</p><p>b</p><p>c</p>
     </div>, <div class="ex_class sample">
     <p>X</p><p>Y</p><p>Z</p>
     </div>, <div id="ex_id">
     <p>1</p><p>2</p><p>3</p>
     </div>]




```python
divs[1].find_all('p')
```




    [<p>X</p>, <p>Y</p>, <p>Z</p>]



* select_one() : CSS selector로 하나의 노드만 찾는 메소드


```python
#tag 이름
soup.select_one('div')
```




    <div>
    <p>a</p><p>b</p><p>c</p>
    </div>




```python
# class 이름 : 클래스 이름 앞에 .을 붙임
# soup.select_one('a.a')
soup.select_one('.a')
```




    <a class="a sample" href="www.naver.com">네이버</a>




```python
# id 이름 : id 이름 앞에 #을 붙임
#soup.select_one('div#ex_id') #tag 이름 #id 이름
soup.select_one('#ex_id')
```




    <div id="ex_id">
    <p>1</p><p>2</p><p>3</p>
    </div>




```python
#여러개의 클래스 이름
soup.select_one('.ex_class.sample')
```




    <div class="ex_class sample">
    <p>X</p><p>Y</p><p>Z</p>
    </div>



* select():CSS selector로 모든 노드를 찾아 리스트로 반환


```python
soup.select('.sample')
```




    [<div class="ex_class sample">
     <p>X</p><p>Y</p><p>Z</p>
     </div>, <a class="a sample" href="www.naver.com">네이버</a>]




```python
soup.select("#ex_id")
```




    [<div id="ex_id">
     <p>1</p><p>2</p><p>3</p>
     </div>]



* 결과 값 가져오기


```python
atag = soup.find('a')
atag
```




    <a class="a sample" href="www.naver.com">네이버</a>




```python
atag.get_text()
```




    '네이버'




```python
atag.string
```




    '네이버'




```python
#속성값 가져오기
atag['href']
```




    'www.naver.com'




```python
lis = soup.find('ul').find_all('li')
lis
```




    [<li>삼겹살</li>, <li>치킨</li>, <li>비빕밥</li>]




```python
for li in lis:
  print(li.get_text())
```

    삼겹살
    치킨
    비빕밥



```python
menu = []
for li in lis:
  menu.append(li.get_text())
menu
```




    ['삼겹살', '치킨', '비빕밥']




```python
trs = soup.find('table').find_all('tr')
for tr in trs:
  tds = tr.find_all('td')
  for td in tds:
    print(td.get_text(), end=' ')
  print()
```

    A B C 
    x y z 



```python
!jupyter nbconvert --to markdown "/content/drive/MyDrive/Colab Notebooks/Python 기초/Crawling - BeautifulSoup.ipynb"
```

    [NbConvertApp] WARNING | pattern '/content/drive/MyDrive/Colab Notebooks/Python 기초/Crawling - BeautifulSoup.ipynb' matched no files
    This application is used to convert notebook files (*.ipynb)
            to various other formats.
    
            WARNING: THE COMMANDLINE INTERFACE MAY CHANGE IN FUTURE RELEASES.
    
    Options
    =======
    The options below are convenience aliases to configurable class-options,
    as listed in the "Equivalent to" description-line of the aliases.
    To see all configurable class-options for some <cmd>, use:
        <cmd> --help-all
    
    --debug
        set log level to logging.DEBUG (maximize logging output)
        Equivalent to: [--Application.log_level=10]
    --show-config
        Show the application's configuration (human-readable format)
        Equivalent to: [--Application.show_config=True]
    --show-config-json
        Show the application's configuration (json format)
        Equivalent to: [--Application.show_config_json=True]
    --generate-config
        generate default config file
        Equivalent to: [--JupyterApp.generate_config=True]
    -y
        Answer yes to any questions instead of prompting.
        Equivalent to: [--JupyterApp.answer_yes=True]
    --execute
        Execute the notebook prior to export.
        Equivalent to: [--ExecutePreprocessor.enabled=True]
    --allow-errors
        Continue notebook execution even if one of the cells throws an error and include the error message in the cell output (the default behaviour is to abort conversion). This flag is only relevant if '--execute' was specified, too.
        Equivalent to: [--ExecutePreprocessor.allow_errors=True]
    --stdin
        read a single notebook file from stdin. Write the resulting notebook with default basename 'notebook.*'
        Equivalent to: [--NbConvertApp.from_stdin=True]
    --stdout
        Write notebook output to stdout instead of files.
        Equivalent to: [--NbConvertApp.writer_class=StdoutWriter]
    --inplace
        Run nbconvert in place, overwriting the existing notebook (only 
                relevant when converting to notebook format)
        Equivalent to: [--NbConvertApp.use_output_suffix=False --NbConvertApp.export_format=notebook --FilesWriter.build_directory=]
    --clear-output
        Clear output of current file and save in place, 
                overwriting the existing notebook.
        Equivalent to: [--NbConvertApp.use_output_suffix=False --NbConvertApp.export_format=notebook --FilesWriter.build_directory= --ClearOutputPreprocessor.enabled=True]
    --no-prompt
        Exclude input and output prompts from converted document.
        Equivalent to: [--TemplateExporter.exclude_input_prompt=True --TemplateExporter.exclude_output_prompt=True]
    --no-input
        Exclude input cells and output prompts from converted document. 
                This mode is ideal for generating code-free reports.
        Equivalent to: [--TemplateExporter.exclude_output_prompt=True --TemplateExporter.exclude_input=True]
    --log-level=<Enum>
        Set the log level by value or name.
        Choices: any of [0, 10, 20, 30, 40, 50, 'DEBUG', 'INFO', 'WARN', 'ERROR', 'CRITICAL']
        Default: 30
        Equivalent to: [--Application.log_level]
    --config=<Unicode>
        Full path of a config file.
        Default: ''
        Equivalent to: [--JupyterApp.config_file]
    --to=<Unicode>
        The export format to be used, either one of the built-in formats
                ['asciidoc', 'custom', 'html', 'latex', 'markdown', 'notebook', 'pdf', 'python', 'rst', 'script', 'slides']
                or a dotted object name that represents the import path for an
                `Exporter` class
        Default: 'html'
        Equivalent to: [--NbConvertApp.export_format]
    --template=<Unicode>
        Name of the template file to use
        Default: ''
        Equivalent to: [--TemplateExporter.template_file]
    --writer=<DottedObjectName>
        Writer class used to write the 
                                            results of the conversion
        Default: 'FilesWriter'
        Equivalent to: [--NbConvertApp.writer_class]
    --post=<DottedOrNone>
        PostProcessor class used to write the
                                            results of the conversion
        Default: ''
        Equivalent to: [--NbConvertApp.postprocessor_class]
    --output=<Unicode>
        overwrite base name use for output files.
                    can only be used when converting one notebook at a time.
        Default: ''
        Equivalent to: [--NbConvertApp.output_base]
    --output-dir=<Unicode>
        Directory to write output(s) to. Defaults
                                      to output to the directory of each notebook. To recover
                                      previous default behaviour (outputting to the current 
                                      working directory) use . as the flag value.
        Default: ''
        Equivalent to: [--FilesWriter.build_directory]
    --reveal-prefix=<Unicode>
        The URL prefix for reveal.js (version 3.x).
                This defaults to the reveal CDN, but can be any url pointing to a copy 
                of reveal.js. 
                For speaker notes to work, this must be a relative path to a local 
                copy of reveal.js: e.g., "reveal.js".
                If a relative path is given, it must be a subdirectory of the
                current directory (from which the server is run).
                See the usage documentation
                (https://nbconvert.readthedocs.io/en/latest/usage.html#reveal-js-html-slideshow)
                for more details.
        Default: ''
        Equivalent to: [--SlidesExporter.reveal_url_prefix]
    --nbformat=<Enum>
        The nbformat version to write.
                Use this to downgrade notebooks.
        Choices: any of [1, 2, 3, 4]
        Default: 4
        Equivalent to: [--NotebookExporter.nbformat_version]
    
    Examples
    --------
    
        The simplest way to use nbconvert is
    
                > jupyter nbconvert mynotebook.ipynb
    
                which will convert mynotebook.ipynb to the default format (probably HTML).
    
                You can specify the export format with `--to`.
                Options include ['asciidoc', 'custom', 'html', 'latex', 'markdown', 'notebook', 'pdf', 'python', 'rst', 'script', 'slides'].
    
                > jupyter nbconvert --to latex mynotebook.ipynb
    
                Both HTML and LaTeX support multiple output templates. LaTeX includes
                'base', 'article' and 'report'.  HTML includes 'basic' and 'full'. You
                can specify the flavor of the format used.
    
                > jupyter nbconvert --to html --template basic mynotebook.ipynb
    
                You can also pipe the output to stdout, rather than a file
    
                > jupyter nbconvert mynotebook.ipynb --stdout
    
                PDF is generated via latex
    
                > jupyter nbconvert mynotebook.ipynb --to pdf
    
                You can get (and serve) a Reveal.js-powered slideshow
    
                > jupyter nbconvert myslides.ipynb --to slides --post serve
    
                Multiple notebooks can be given at the command line in a couple of 
                different ways:
    
                > jupyter nbconvert notebook*.ipynb
                > jupyter nbconvert notebook1.ipynb notebook2.ipynb
    
                or you can specify the notebooks list in a config file, containing::
    
                    c.NbConvertApp.notebooks = ["my_notebook.ipynb"]
    
                > jupyter nbconvert --config mycfg.py
    
    To see all available configurables, use `--help-all`.
    

