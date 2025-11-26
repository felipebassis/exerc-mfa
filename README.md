# exerc-mfa
Instruções para desenvolvimento de um projeto simples para MFA

## Proposta
Esse projeto visa criar uma API que forneça endpoints para login utilizando o processo de Múltiplo Fator de Autenticação, que visa minimizar acessos não autorizados. A idéia é a princípio permitir o uso somente de email para envio do código MFA.\

## Requisitos
A cerca das funcionalidades:
- O sistema deve armazenar as credenciais do usuário de forma segura.
- O sistema deve permitir acesso via email, nome de usuário ou celular.
- O sistema deve permitir cadastro e alteração de senha. O cadastro somente deve ser feito após o usuário confirmar o email realizando um fluxo de MFA e a alteração da senha deve ser feito mediante a confirmação por MFA.
- O sistema deve ter um template de email para facilitar a confirmação do usuário.
- O sistema deve gerar um token JWT após a autenticação com sucesso que deve ser válido.
- O sistema deve manter um histórico de todas as operações abaixo, sendo necessário atrelar ao usuário quando possível:
    - Login (Inserir usuário e senha)
        - Login bem sucedido por email.
        - Login bem sucedido por nome de usuário.
        - Login bem sucedido por celular.
        - Login mal sucedido devido a senha inválida.
        - Login mal sucedido por email.
        - Login mal sucedido por nome de usuário.
        - Login mal sucedido por celular.
    - MFA
        - Código gerado.
        - Código inserido corretamente.
        - Código inserido incorretamente.
        - Código inserido está expirado.
    - Alteração de senha
        - Alteração de senha solicitada.
        - Alteração de senha concluída.
- O sistema deve permitir que o usuário marque dispositivos como dispositivos confiáveis, caso ele tente acessar o sistema novamente utilizando o dispositivo confiável, deve ser possível pular a etapa de validação via MFA.
- O sistema deve bloquear um usuário caso sua senha seja inserida incorretamente 3 vezes, exigindo que o usuário altere sua senha para reativa-lo.

A cerca do fluxo de MFA:
- O código MFA deve ser salvo de forma temporária.
- O código MFA deve ser uma string de 6 caractéres, podendo conter números e letras.
- O código MFA deve ser gerado de forma aleatória a cada nova solicitação.
- O código deve ter uma validade máxima de 5 minutos.

A cerca da senha:
- A senha deve atender aos requisitos abaixo:
    - Entre 8 e 32 caractéres
    - 1 letra maiúscula
    - 1 letra minúscula
    - 1 caracter especial
    - 1 numero
    - Não pode possuir ponto (.) ou hífen (-)
- O usuário não pode alterar uma senha caso ela seja uma de suas 3 senhas anteriores.
