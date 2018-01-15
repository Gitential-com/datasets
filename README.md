# Gitential Datasets for Open Source Projects



## Python example



### Install Dependencies

Reading Parquet files requires [PyArrow](https://arrow.apache.org/docs/python/install.html)


```bash
conda install -y pandas pyarrow
```

    Fetching package metadata ...............
    Solving package specifications: .

    Package plan for installation in environment /Users/krisz/.pyenv/versions/miniconda3-latest/envs/ml3:

    The following packages will be UPDATED:

        pandas: 0.21.0-py36_0 conda-forge --> 0.22.0-py36_0 conda-forge

    pandas-0.22.0- 100% |################################| Time: 0:00:04   2.30 MB/s


### Download Files

Currently there two formats available: Parquet and JSON


```bash
wget https://s3.amazonaws.com/gitential-datasets/libgit2-libgit2/commits.parquet
wget https://s3.amazonaws.com/gitential-datasets/libgit2-libgit2/commits.json.gz
```

    --2018-01-15 11:09:00--  https://s3.amazonaws.com/gitential-datasets/libgit2-libgit2/commits.parquet
    Resolving s3.amazonaws.com (s3.amazonaws.com)... 52.216.100.149
    Connecting to s3.amazonaws.com (s3.amazonaws.com)|52.216.100.149|:443... connected.
    HTTP request sent, awaiting response... 200 OK
    Length: 1483345 (1.4M) [binary/octet-stream]
    Saving to: ‘commits.parquet’

    commits.parquet     100%[===================>]   1.41M   616KB/s    in 2.4s

    2018-01-15 11:09:03 (616 KB/s) - ‘commits.parquet’ saved [1483345/1483345]

    --2018-01-15 11:09:04--  https://s3.amazonaws.com/gitential-datasets/libgit2-libgit2/commits.json.gz
    Resolving s3.amazonaws.com (s3.amazonaws.com)... 52.216.100.149
    Connecting to s3.amazonaws.com (s3.amazonaws.com)|52.216.100.149|:443... connected.
    HTTP request sent, awaiting response... 200 OK
    Length: 1642853 (1.6M) [application/json]
    Saving to: ‘commits.json.gz’

    commits.json.gz     100%[===================>]   1.57M   903KB/s    in 1.8s

    2018-01-15 11:09:06 (903 KB/s) - ‘commits.json.gz’ saved [1642853/1642853]



### Reading Parquet file


```python
import pandas as pd

commits = pd.read_parquet('./commits.parquet')
```


```python
commits[['id', 'message']].head()
```


<table>
  <thead>
    <tr style="text-align: right;">
      <th>id</th>
      <th>message</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>c15648cbd059b92c177586ab1701a167222c7681</td>
      <td>Initial draft of libgit2\n\nSigned-off-by: Sha...</td>
    </tr>
    <tr>
      <td>44181c23ea6c39d51a4b481dc59ecf2cc3967e76</td>
      <td>Mark git_oid parameters const when they should...</td>
    </tr>
    <tr>
      <td>46d8b885bd65158e8cb53266ba4b627b5991bce8</td>
      <td>Rename git_odb_sread to just git_odb_read\n\nM...</td>
    </tr>
    <tr>
      <td>171aaf21d9f7582270c390962f61d3d2613c4d59</td>
      <td>Hide GIT_{BEGIN,END}_DECL from doxygen as its ...</td>
    </tr>
    <tr>
      <td>b51eb250ed0cbda59d3108d04569fab9413909fd</td>
      <td>Cleanup git_odb documentation formatting\n\nSi...</td>
    </tr>
  </tbody>
</table>


### Reading JSON.gz file


```python
import pandas as pd

commits = pd.read_json('./commits.json.gz', compression='infer')
```


```python
commits[['id', 'message']].head()
```


<table>
  <thead>
    <tr style="text-align: right;">
      <th>id</th>
      <th>message</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>c15648cbd059b92c177586ab1701a167222c7681</td>
      <td>Initial draft of libgit2\n\nSigned-off-by: Sha...</td>
    </tr>
    <tr>
      <td>44181c23ea6c39d51a4b481dc59ecf2cc3967e76</td>
      <td>Mark git_oid parameters const when they should...</td>
    </tr>
    <tr>
      <td>46d8b885bd65158e8cb53266ba4b627b5991bce8</td>
      <td>Rename git_odb_sread to just git_odb_read\n\nM...</td>
    </tr>
    <tr>
      <td>171aaf21d9f7582270c390962f61d3d2613c4d59</td>
      <td>Hide GIT_{BEGIN,END}_DECL from doxygen as its ...</td>
    </tr>
    <tr>
      <td>b51eb250ed0cbda59d3108d04569fab9413909fd</td>
      <td>Cleanup git_odb documentation formatting\n\nSi...</td>
    </tr>
  </tbody>
</table>
