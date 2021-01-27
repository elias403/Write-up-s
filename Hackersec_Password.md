
<h2>Observando e inspecionando a área do input do password vemos que já está preenchida com uma hash</h2>
![1](https://github.com/elias403/Write-up-s/blob/main/images/HackerSec/1.PNG)
![2]()

usando o [cyberchef](https://gchq.github.io/CyberChef/) ele nos mostra que é um base64 e nos retorna o resultado, analisando com o [hash-analyzer](https://www.tunnelsup.com/hash-analyzer/) temos uma hash do tipo SHA1, e usando o [crackstation](https://crackstation.net/) ele quebra o SHA1 e nos retorna a senha  
![3]()
![4]()
![5]()

Voltando em inspecionar elemento, substituimos a hash pela senha e apagamos o DISABLED
![6]()
![7]()
