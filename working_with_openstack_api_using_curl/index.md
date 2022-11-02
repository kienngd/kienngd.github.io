# Working with openstack api using curl


##### Get token
```bash
curl -s -i -H "Content-Type: application/json"   -d '
{
    "auth": {
        "identity": {
            "methods": [
                "password"
            ],
            "password": {
                "user": {
                    "name": "{USERNAME}",
                    "domain": { "id": "{DOMAIN_ID}" },
                    "password": "{PASSWORD}"
                }
            }
        },
        "scope": {
            "project": {
                "id": "{PROJECT_ID}"
            }
        }
    }
}'   "https://{BASE URL}:5000/v3/auth/tokens" | grep "X-Subject-Token:"
```
Default keystone port is **5000**

By default, this token will be expired after 6 hours.
<!--more-->
##### Export token
API_TOKEN="{TOKEN}"

##### Get domains
```bash
curl -s -H "X-Auth-Token: $API_TOKEN" "https://{BASE URL}:5000/v3/domains" | jq '.'
```
Use **jq** command to format return JSON data.

##### Get projects
```bash
curl -s -H "X-Auth-Token: $API_TOKEN" "https://{BASE URL}:5000/v3/projects" | jq '.'
```

##### Set storage policy quota for one project
```bash
curl -s -X PUT -H "Content-Type: application/json" -H "X-Auth-Token: $API_TOKEN" -d '
{
    "gigabytes_{POLICY_1_NAME}": {QUOTA_1_VALUE},
    "gigabytes_{POLICY_2_NAME}": {QUOTA_2_VALUE},
    "gigabytes_{POLICY_3_NAME}": {QUOTA_3_VALUE}
}'   "https://{BASE_URL}:8776/v3/{ADMIN_PROJECT_ID}/os-quota-sets/{PROJECT_ID}"
```

##### Get all project's vms with detail
```bash
curl -s -H "X-Auth-Token: $API_TOKEN" "https://{BASE_URL}:8774/v2.1/servers/detail" | jq '.'
```

##### Get all flavors with detail
```bash
curl -s -H "X-Auth-Token: $API_TOKEN" "https://{BASE_URL}:8774/v2.1/flavors/detail" | jq '.'
```

##### Grant one role on all domain's projects to one user
```bash
curl -s -X PUT -H "X-Auth-Token: $API_TOKEN" "https://{BASE_URL}:5000/v3/OS-INHERIT/domains/{DOMAIN_ID}/users/{USER_ID}/roles/{ROLE_ID}/inherited_to_projects" | jq '.'
```

##### Grant one system role to one user
```bash
curl -s -X PUT -H "X-Auth-Token: $API_TOKEN" "https://{BASE_URL}:5000/v3/system/users/{USER_ID}/roles/{SYSTEM_ROLE_ID}" | jq '.'
```

##### Set micro version for API
Using HTTP header: **X-OpenStack-Nova-API-Version: 2.4** Or **OpenStack-API-Version: compute 2.27** (valid from version 2.27).

