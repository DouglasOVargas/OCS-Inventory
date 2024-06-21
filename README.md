# Configurando o OCS Inventory para Autenticação LDAP

Este guia fornece instruções detalhadas para configurar o OCS Inventory para autenticar usuários via LDAP. Siga os passos abaixo para garantir que o OCS Inventory esteja configurado corretamente para usar o LDAP.

## Nota Importante

Lembre-se de que não explicaremos como configurar um servidor LDAP e nem como depurar a conexão LDAP. Acreditamos que esta parte está mais relacionada ao próprio servidor LDAP do que ao OCS.

## Requisitos

Antes de começar, certifique-se de que você possui:
- Um servidor OCS Inventory em funcionamento.
- Acesso a um servidor LDAP.

## Ativar Configuração Avançada

Primeiro, você precisa habilitar a configuração avançada:

1. Navegue até `Configuration > General configuration`.
2. Clique na aba `Server`.
3. Defina `ADVANCE_CONFIGURATION` como `ON`.
4. Clique em `Update`.

## Verificar Dependências

Verifique se o `php-ldap` está instalado no seu servidor OCS Inventory. Execute o comando abaixo para listar os pacotes PHP instalados:

```bash
yum list installed | grep -i php
```

## Instalar Dependências

Se o `php-ldap` não estiver instalado, instale-o usando o seguinte comando:

```bash
yum install php73-php-ldap.x86_64 -y
```

## Configurar o OCS Inventory

1. Abra o arquivo de configuração `var.php`, localizado no diretório `/usr/share/ocsinventory-reports/ocsreports/`:

```bash
nano /usr/share/ocsinventory-reports/ocsreports/var.php
```

2. Adicione a seguinte linha ao arquivo `var.php` para definir o tipo de autenticação como LDAP:

```php
define('AUTH_TYPE', 2);
```

3. Salve e feche o arquivo.


## Configuração LDAP no OCS Inventory

No OCS Inventory, acesse `Configurações Gerais > Configuração LDAP` e preencha os campos abaixo conforme o seu cenário:

```
CONEX_LDAP_SERVEUR=IPLDAP
CONEX_ROOT_DN=bind_dn
CONEX_ROOT_PW=bind_password
CONEX_LDAP_PORT=389
CONEX_DN_BASE_LDAP=OU=Users,DC=domain,DC=local
CONEX_LOGIN_FIELD=sAMAccountName
CONEX_LDAP_PROTOCOL_VERSION=3
CONEX_LDAP_CHECK_FIELD1_NAME=memberOf
CONEX_LDAP_CHECK_FIELD1_VALUE=CN=ocsinventory_superadmin,OU=OCSInventory,OU=Integracoes,DC=domain,DC=local
CONEX_LDAP_CHECK_FIELD1_ROLE=Super administradores
CONEX_LDAP_CHECK_FIELD2_NAME=memberOf
CONEX_LDAP_CHECK_FIELD2_VALUE=CN=ocsinventory_admin,OU=OCSInventory,OU=Integracoes,DC=domain,DC=local
CONEX_LDAP_CHECK_FIELD2_ROLE=Administradores
CONEX_LDAP_CHECK_DEFAULT_ROLE=RO
```

## Conclusão

Após seguir esses passos, o OCS Inventory estará configurado para autenticação LDAP. Teste a configuração tentando fazer login com um usuário LDAP.

Para mais detalhes, consulte a [documentação oficial do OCS Inventory](https://wiki.ocsinventory-ng.org/). Se você encontrar problemas ou tiver dúvidas, por favor, abra uma issue neste repositório.

---

Esta configuração pode variar dependendo do ambiente e das versões específicas dos pacotes instalados. Sempre faça backup de seus arquivos de configuração antes de fazer alterações.