
## Read the Doc安装配置

### 安装
1. 软件安装
    ```bash
    pip install -i https://pypi.tuna.tsinghua.edu.cn/simple sphinx
    ```
2. 创建工作目录及项目
   ```bash
    mkdir notes && cd notes
    sphinx-quickstart
    ```
3. 部署http服务(打开http://127.0.0.1:8000即可看到对应的页面)
    ```bash
    pip install -i https://pypi.tuna.tsinghua.edu.cn/simple sphinx-autobuild
    sphinx-autobuild source build/html 
    ```

### 配置

#### 更换主题
1. 查看可用主题https://sphinx-themes.org/
2. 安装主题
    ```bash
    pip install -i https://pypi.tuna.tsinghua.edu.cn/simple sphinx_rtd_theme
    ```
3. 修改conf.py中内容
   ```python
   html_theme = 'sphinx_rtd_theme'
   ```


#### 配置markdown
1. 安装插件
   ```bash
   # 支持markdown
   pip install -i https://pypi.tuna.tsinghua.edu.cn/simple recommonmark
   # 支持markdown表格
   pip install -i https://pypi.tuna.tsinghua.edu.cn/simple sphinx_markdown_tables
    ```
2. 在conf.py中配置extention
   ```python
   extensions = ['recommonmark','sphinx_markdown_tables']
   ```

#### 中文搜索

1. 安装“结巴”中文分词
    ```bash
    # python2
    pip install jieba
    # python3
    pip install jieba3k
    ```

2. 安装sphinx中文搜索插件
    ```bash
    git clone https://github.com/bosbyj/sphinx.search.zh_CN.git
    # conda
    mv sphinx.search.zh_CN/zh_CN.py ~/anaconda3/lib/python3.9/site-packages/sphinx/search/
    ```

3. 编辑search目录下__init__.py
    ```python
    languages = {
        'en': en.SearchEnglish,
        'ja': ja.SearchJapanese,
    }
    #增加一行
    'zh_CN': 'sphinx.search.zh_CN.SearchChinese',
    ```

4. 确保conf.py中添加 `language = 'zh_CN'`
