# Configurando o OCS Inventory para Autenticação LDAP

Este guia fornece instruções detalhadas para configurar o OCS Inventory para autenticar usuários via LDAP. Siga os passos abaixo para garantir que o OCS Inventory esteja configurado corretamente para usar o LDAP.

## Requisitos

Antes de começar, certifique-se de que você possui:
- Um servidor OCS Inventory em funcionamento
- Acesso a um servidor LDAP
- O pacote `php-ldap` instalado no servidor OCS Inventory

## Passo 1: Verificar Dependências

Primeiro, verifique se o `php-ldap` está instalado no seu servidor OCS Inventory. Execute o comando abaixo para listar os pacotes PHP instalados:

```bash
yum list installed | grep -i php
```

## Passo 2: Instalar Dependências

Se o `php-ldap` não estiver instalado, instale-o usando o seguinte comando:

```bash
yum install php73-php-ldap.x86_64 -y
```

## Passo 3: Configurar o OCS Inventory

1. Abra o arquivo de configuração `var.php`, localizado no diretório `/usr/share/ocsinventory-reports/ocsreports/`:

```bash
nano /usr/share/ocsinventory-reports/ocsreports/var.php
```

2. Adicione a seguinte linha ao arquivo `var.php` para definir o tipo de autenticação como LDAP:

```php
define('AUTH_TYPE', 2);
```

3. Salve e feche o arquivo.

## Passo 4: Configurar Parâmetros LDAP (Opcional)

Dependendo da sua configuração LDAP específica, você pode precisar adicionar ou ajustar outros parâmetros de configuração LDAP no arquivo `var.php`. Consulte a documentação do OCS Inventory e do seu servidor LDAP para informações adicionais sobre esses parâmetros.

## Conclusão

Após seguir esses passos, o OCS Inventory estará configurado para autenticação LDAP. Teste a configuração tentando fazer login com um usuário LDAP.

Para mais detalhes, consulte a [documentação oficial do OCS Inventory](https://wiki.ocsinventory-ng.org/). Se você encontrar problemas ou tiver dúvidas, por favor, abra uma issue neste repositório.

---

Esta configuração pode variar dependendo do ambiente e das versões específicas dos pacotes instalados. Sempre faça backup de seus arquivos de configuração antes de fazer alterações.
