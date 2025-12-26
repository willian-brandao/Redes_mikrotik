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
## Configurações exportadas
```
/system identity set name=oper-0001

/tool romon set enabled=yes secrets=123

```
