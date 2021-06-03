### Description

stagedomain - tool, that makes subdomain mutations with popular state keywords, like **stage**, **prod**, **dev**, **test**, **admin**, etc.


### Requirements
`python 3.6+`


### Installation

* Installation from source (requires git):
```
git clone https://github.com/vionde/stagedomain.git
cd stagedomain
python stagedomain.py
```


### Usage
Script can be used in two ways: from **stdin** or by passing **-i** argument with input file.

* From stdin
```
cat "subdomains.txt" | stagedomain.py
```
or for windows:
```
type "subdomains.txt" | stagedomain.py
```

* By executing from python
```
python stagedomain.py [args]
```

## stagedomain -h
```
usage: stagedomain.py [-h] [-i [INPUT]] [-f] [-u]

Subdomain mutations with popular keywords

optional arguments:
  -h, --help            show this help message and exit
  -i [INPUT], --input [INPUT]
                        input file with subdomains
  -f, --full-match      replace only full words
  -u, --unique          save only unique subdomains
```

#### Args

| Argument | Description |
| ------------- | ------------- |
| -i | input file, if **stdin** not used. File must contain subdomains |
| -f<br/>--full-match  | match and replace full word only. Default: **False** <br/>If disabled, it will replace `prod` in `assetsprod.example.com` with payloads. If enabled - this subdomain will be skipped and script will replace only subdomains like `assets-prod.example.com` where keyword separated from other alphabet chars. Equivalent to `\b{keyword}\b` regex. |
| -u<br/>--unique | will save only unique mutations. Default: **True**<br/>If the generated domain is present in original input list, this domain will not be printed. |


## Examples
```
file: example.txt

edgedns.example.com
url5347.example.com
url2547.example.com
origin-stage-assets-pay.example.com
static-map.example.com
apidev.example.com
manage.prod.example.com
errlog.example.com
akamai-apigateway-payment.example.com
enterpriseregistration.contractors.contractors.example.com
```

#### Full match only

```
cat example.txt | stagedomain.py -f -u > out.txt
```
47 new subdomains. `apidev.example.com` has not been changed because we use **-f** arg.

#### Input file

```
stagedomain.py -i example.txt > out.txt
```
70 new subdomains. `apidev.example.com` was replaced by payloads too.


### Used payloads
For the first version i used this payloads:
```python
subnames = {'prod': ['prod', 'prd', 'production', 'prod-dev', 'prod-admin'],
            'stage': ['stage', 'stg', 'staging', 'stag', 'stag-dev', 'stag-admin'],
            'dev': ['dev', 'develop', 'developer', 'developing', 'dev-admin', 'dev-stage'],
            'admin': ['admin', 'adm', 'administrating'],
            'internal': ['internal', 'local', 'localhost', 'local-host'],
            'test': ['test', 'testing', 'test-dev', 'test-stage', 'test-admin']}
```
If you have any suggestions for expanding the payloads dict, I will be glad to hear!
