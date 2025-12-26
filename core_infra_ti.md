# Criar um identificador para o dispositivo na rede.

```
/system/identity/set name=roteador-001
```

# Ativar o romon para que possa administrar mais de um dispositivo conectado à rede.

```
/tool/romon/set enable=yes secrets=123
```

# Exportar configurações de um dispositivo para replica-las em outros dispositivos.
```
export
```
<p> Em casos de exportação de conteúdos sensíveis como senhas, usa-se o parametro 'show-sensitive'</p>

```
export show-sensitive
```
## Configurações exportadas (exemplo).
```
/system identity set name=oper-0001

/tool romon set enabled=yes secrets=123

```
## Identificar as interfaces

Esse tipo de procedimento é importante para identificar cada serviço que está atribuído em determinado equipamento. 

Estrutura do comando: interface/set [id da interface] name=[nome da interface]
```
interface/set ether1 name=operadora_0
```

