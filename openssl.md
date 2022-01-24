## Extract public key from private key

    ssh-keygen -y -f /path/to/id_rsa

## Reading key from stdin

    ssh-keygen -f <(cat /tmp/manitou.id_rsa) -e -m pem
    
fails with

    Load key "/dev/fd/63": invalid format
    
As does

    cat /tmp/manitou.id_rsa | ssh-keygen -f /dev/stdin -e -m pem
    
You must save it as a file:

    key_path="$(mktemp)" && cat /tmp/manitou.id_rsa > $key_path && ssh-keygen -f "$key_path" -e -m pem > path/to/rsa-public-key.pem && rm "$key_path"
    
## Converting openssl formatted key to public PEM

    key_path="$(mktemp)" && cat /tmp/manitou.id_rsa > $key_path && ssh-keygen -f "$key_path" -e -m pem && rm "$key_path"
    
Where `/tmp/manitou.id_rsa` starts with `-----BEGIN OPENSSH PRIVATE KEY-----`
