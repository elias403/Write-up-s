
#Observando e inspecionando a área do input do password vemos que já está preenchida com uma hash 
![1](https://raw.githubusercontent.com/elias403/Write-up-s/main/images/HackerSec/1.PNG)
![2](https://github.com/elias403/Write-up-s/blob/main/images/HackerSec/2.PNG?raw=true)

usando o [cyberchef](https://gchq.github.io/CyberChef/) ele nos mostra que é um base64 e nos retorna o resultado, analisando com o [hash-analyzer](https://www.tunnelsup.com/hash-analyzer/) temos uma hash do tipo SHA1, e usando o [crackstation](https://crackstation.net/) ele quebra o SHA1 e nos retorna a senha  

![3](https://github.com/elias403/Write-up-s/blob/main/images/HackerSec/3.PNG?raw=true)
![4](https://github.com/elias403/Write-up-s/blob/main/images/HackerSec/4.PNG?raw=true)
![5](https://github.com/elias403/Write-up-s/blob/main/images/HackerSec/5.PNG?raw=true)

Voltando em inspecionar elemento, substituimos a hash pela senha e apagamos o DISABLED
![6](https://github.com/elias403/Write-up-s/blob/main/images/HackerSec/6.PNG?raw=true)
![7](https://github.com/elias403/Write-up-s/blob/main/images/HackerSec/7.PNG?raw=true)
