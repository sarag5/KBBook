## Get the client secret token from the role ID and secret API

    curl --location 'https://1.0.0.0:8200/v1/<namespace>/auth/approle/login' \
    --header 'Content-Type: application/x-www-form-urlencoded' \
    --data-urlencode 'role_id=RoleID' \
    --data-urlencode 'secret_id=SecretId'


## Get the values from the vault using the token created

    curl --location 'https://1.0.0.0:8200/v1/<paste/path/here>' \ ## example projects/data/test
    --header 'X-Vault-Token: paste the generated token here' \
    --header 'X-Vault-Namespace: namespace value'


## Create Role ID and secret via CLI

    vault write auth/approle/role/<role created>\
        token_policies="<policy created>" \   ## updated the policy page according to the need
        token_type=batch \
        secret_id_ttl=0 \
        token_ttl=0 \
        token_max_ttl=0 \
        
    ## way to retrive the role ID and secret 
    
     vault read auth/approle/role/<role created>/role-id
     vault write -f auth/approle/role/<role created>/secret-id
