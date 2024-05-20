


/ip/dns/set servers=1.1.1.1

/tool fetch url="https://cacerts.digicert.com/DigiCertGlobalRootCA.crt.pem"

/certificate import file-name=DigiCertGlobalRootCA.crt.pem  passphrase="" 

/ip dns static add address=1.1.1.1 name=cloudflare-dns.com

/ip dns set use-doh-server=https://cloudflare-dns.com/dns-query verify-doh-cert=yes

/ip/dns/set servers=""
