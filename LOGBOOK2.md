# Trabalho realizado nas Semanas #2 e #3

## Identificação

- O CVE-2020-1472, popularmente conhecido como ZeroLogon, é uma vulnerabilidade crítica que afeta o protocolo Netlogon (serviço que autentica utilizadores e serviços) no Microsoft Windows.(1)(3)
- Esta vulnerabilidade pode permitir a um atacante assumir o controlo total de uma rede de domínio do Windows, executando um ataque de elevação de privilégio e passando assim a ter capacidade de comprometer a segurança da rede e causar danos significativos.(4)

## Catalogação

- Foi corrigida em agosto de 2020 pela Microsoft e identificada e relatada por Tom Tervoort, um investigador da Secura.(4)
- Não houve qualquer programa de bug bounty público associado a resolução da mesma.
- Avaliada com um grau de gravidade crítico e um CVSS Score de 10.0/10.0 (1)

## Exploit

- O atacante utiliza um exploit que envolve a criação de pacotes de autenticação falsos. Esses pacotes são manipulados para explorar a vulnerabilidade no protocolo Netlogon. (8)
- O atacante cria pacotes de autenticação falsos para mudar o controlador de domínio, envia esses pacotes e o controlador de domínio ao processar esses pacotes pode ser enganado e conceder ao atacante um nível de acesso maior que o devido. (8)
- Posto isso, é possível assumir o controlo de domínio da rede, aceder a dados sensíveis, realizar atividades não autorizadas na rede, entre outros.(8)
- Não há uma automação específica no Metasploit relacionada à exploração da vulnerabilidade ZeroLogon.

## Ataques

- Rápida identificação e correção da Microsoft, sem grande impacto mundial. (5)(6)
- Apesar desta rápida descoberta, o potencial de impacto era elevado.(6)
- Os sistemas operativos mais antigos não estão protegidos deste tipo de ataques. (9)
- A Microsoft recomenda a utilização de passwords fortes, autenticação multi-fatores e atualizações regulares aos sistemas. (5)

### Fontes consultadas

- (1) - https://nvd.nist.gov/vuln/detail/cve-2020-1472
- (2) - https://www.malwarebytes.com/blog/news/2021/01/the-story-of-zerologon
- (3) - https://msrc.microsoft.com/update-guide/vulnerability/CVE-2020-1472
- (4) - https://resources.infosecinstitute.com/topics/vulnerabilities/zerologon-cve-2020-1472-technical-overview-and-walkthrough/
- (5) - https://msrc.microsoft.com/update-guide/en-US/advisory/CVE-2020-1472
- (6) - https://www.secpod.com/blog/attention-your-server-machines-in-domains-are-no-more-safe-cve-2020-1472-zerologon
- (7) - https://support.microsoft.com/pt-br/topic/vulnerabilidade-de-eleva%C3%A7%C3%A3o-de-privil%C3%A9gio-de-integridade-de-c%C3%B3digo-do-hipervisor-13-de-junho-de-2017-e6562dab-0302-06c9-9c34-c99c638a610c
- (8) - https://www.trendmicro.com/pt_br/what-is/zerologon.html
- (9) - https://www.malwarebytes.com/blog/news/2021/01/the-story-of-zerologon
