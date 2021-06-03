### Description

stagedomain - tool, that makes subdomain mutations with popular state keywords, like **stage**, **prod**, **dev**, **test**, **admin**, etc.


### Requirements
`python 3.6+`


### Installation

* Usging pip
```
pip install stagedomain
```
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
<details>
  <summary>
    out.txt
  </summary>
```origin-test-dev-assets-pay.example.com
api-stag.example.com
api-stg.example.com
manage.local-host.example.com
api-stag-admin.example.com
origin-dev-admin-assets-pay.example.com
api-admin.example.com
api-prod-admin.example.com
origin-dev-stage-assets-pay.example.com
origin-test-assets-pay.example.com
manage.test-stage.example.com
origin-test-admin-assets-pay.example.com
manage.localhost.example.com
origin-testing-assets-pay.example.com
origin-prod-admin-assets-pay.example.com
api-stag-dev.example.com
origin-developing-assets-pay.example.com
api-administrating.example.com
manage.stag.example.com
manage.developing.example.com
origin-localhost-assets-pay.example.com
origin-dev-assets-pay.example.com
api-test-dev.example.com
manage.internal.example.com
origin-administrating-assets-pay.example.com
api-local-host.example.com
api-testing.example.com
manage.stag-dev.example.com
manage.develop.example.com
manage.dev.example.com
manage.dev-admin.example.com
manage.test-dev.example.com
manage.admin.example.com
origin-local-host-assets-pay.example.com
api-staging.example.com
api-localhost.example.com
origin-prod-assets-pay.example.com
manage.stag-admin.example.com
manage.developer.example.com
manage.test.example.com
manage.test-admin.example.com
api-prod.example.com
api-prod-dev.example.com
manage.testing.example.com
origin-production-assets-pay.example.com
origin-prd-assets-pay.example.com
origin-prod-dev-assets-pay.example.com
origin-local-assets-pay.example.com
origin-test-stage-assets-pay.example.com
api-prd.example.com
api-local.example.com
manage.stg.example.com
manage.adm.example.com
api-stage.example.com
api-test.example.com
api-internal.example.com
api-adm.example.com
origin-develop-assets-pay.example.com
origin-internal-assets-pay.example.com
origin-admin-assets-pay.example.com
manage.stage.example.com
origin-developer-assets-pay.example.com
api-production.example.com
manage.administrating.example.com
origin-adm-assets-pay.example.com
api-test-stage.example.com
manage.staging.example.com
manage.local.example.com
api-test-admin.example.com
manage.dev-stage.example.com
```
</details>

47 new subdomains. `apidev.example.com` has not been changed because we use **-f** arg.

#### Input file

```
stagedomain.py -i example.txt > out.txt
```
<details>
  <summary>
    out.txt
  </summary>
```
origin-adm-assets-pay.example.com
origin-internal-assets-pay.example.com
apiprod-dev.example.com
apistag.example.com
manage.developing.example.com
origin-test-assets-pay.example.com
origin-administrating-assets-pay.example.com
origin-dev-stage-assets-pay.example.com
manage.stg.example.com
manage.local.example.com
origin-prod-assets-pay.example.com
manage.stag-admin.example.com
manage.test-dev.example.com
apistag-admin.example.com
manage.stag-dev.example.com
manage.local-host.example.com
manage.developer.example.com
apiprd.example.com
manage.administrating.example.com
apiadmin.example.com
apitest-stage.example.com
manage.dev.example.com
origin-dev-admin-assets-pay.example.com
apiadm.example.com
origin-production-assets-pay.example.com
manage.develop.example.com
manage.testing.example.com
apiadministrating.example.com
manage.localhost.example.com
origin-testing-assets-pay.example.com
origin-dev-assets-pay.example.com
apilocalhost.example.com
origin-admin-assets-pay.example.com
origin-developing-assets-pay.example.com
manage.stage.example.com
origin-prd-assets-pay.example.com
origin-localhost-assets-pay.example.com
manage.test-stage.example.com
manage.dev-admin.example.com
origin-prod-dev-assets-pay.example.com
apitest.example.com
manage.test.example.com
origin-developer-assets-pay.example.com
manage.stag.example.com
origin-test-stage-assets-pay.example.com
origin-local-host-assets-pay.example.com
apitest-admin.example.com
origin-prod-admin-assets-pay.example.com
apiprod.example.com
manage.dev-stage.example.com
manage.admin.example.com
manage.staging.example.com
manage.internal.example.com
apistage.example.com
manage.adm.example.com
apilocal-host.example.com
origin-test-dev-assets-pay.example.com
origin-test-admin-assets-pay.example.com
apistg.example.com
manage.test-admin.example.com
origin-local-assets-pay.example.com
apiprod-admin.example.com
apitest-dev.example.com
origin-develop-assets-pay.example.com
apitesting.example.com
apilocal.example.com
apistag-dev.example.com
apiinternal.example.com
apistaging.example.com
apiproduction.example.com
```
</details>

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