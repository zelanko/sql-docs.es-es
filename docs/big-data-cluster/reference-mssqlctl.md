---
title: Referencia de mssqlctl
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para los comandos mssqlctl.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ebd3b63d641c77dae1afbff21264ec4fe34df4d0
ms.sourcegitcommit: d5cd4a5271df96804e9b1a27e440fb6fbfac1220
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2019
ms.locfileid: "64775503"
---
# <a name="mssqlctl"></a>mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

El siguiente artículo proporciona la referencia para la **mssqlctl** herramienta para [clústeres de macrodatos de 2019 de SQL Server (versión preliminar)](big-data-cluster-overview.md). Para obtener más información sobre cómo instalar el **mssqlctl** herramienta, consulte [instalar mssqlctl para administrar clústeres de SQL Server 2019 macrodatos](deploy-install-mssqlctl.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
|[aplicación mssqlctl](reference-mssqlctl-app.md) | Crear, eliminar, ejecutar y administrar aplicaciones. |
|[clúster mssqlctl](reference-mssqlctl-cluster.md) | Seleccione, administrar y operar los clústeres. |
[inicio de sesión mssqlctl](#mssqlctl-login) | Inicie sesión en el clúster.
[mssqlctl logout](#mssqlctl-logout) | Cerrar la sesión de clúster.
|[mssqlctl storage](reference-mssqlctl-storage.md) | Administrar el almacenamiento de clúster. |
## <a name="mssqlctl-login"></a>inicio de sesión mssqlctl
Inicie sesión en el clúster.
```bash
mssqlctl login [--username -u] 
               [--password -p]  
               [--endpoint -e]
```
### <a name="examples"></a>Ejemplos
Sesión de forma interactiva.
```bash
mssqlctl login
```
Inicie sesión con el nombre de usuario y contraseña.
```bash
mssqlctl login -u johndoe@contoso.com -p VerySecret
```
Inicie sesión con el nombre de usuario, contraseña y el punto de conexión de clúster.
```bash
mssqlctl login -u johndoe@contoso.com -p VerySecret --endpoint https://host.com:12800
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--username -u`
Usuario de la cuenta.
#### `--password -p`
Credenciales de contraseña.
#### `--endpoint -e`
Clúster de host y puerto (ex) "http://host:port".
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumentar el nivel de detalle de registro para mostrar que todos los registros de depuración.
#### `--help -h`
Mostrar este mensaje de ayuda y salir.
#### `--output -o`
Formato de salida.  Los valores permitidos: json, jsonc, table y tsv.  Predeterminado: json.
#### `--query -q`
Cadena de consulta JMESPath. Consulte [ http://jmespath.org/ ](http://jmespath.org/]) para obtener más información y ejemplos.
#### `--verbose`
Aumentar el nivel de detalle de registro. Use--debug para registros de depuración completos.
## <a name="mssqlctl-logout"></a>Cierre de sesión mssqlctl
Cerrar la sesión de clúster.
```bash
mssqlctl logout 
```
### <a name="examples"></a>Ejemplos
Cierra la sesión este usuario.
```bash
mssqlctl logout
```
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumentar el nivel de detalle de registro para mostrar que todos los registros de depuración.
#### `--help -h`
Mostrar este mensaje de ayuda y salir.
#### `--output -o`
Formato de salida.  Los valores permitidos: json, jsonc, table y tsv.  Predeterminado: json.
#### `--query -q`
Cadena de consulta JMESPath. Consulte [ http://jmespath.org/ ](http://jmespath.org/]) para obtener más información y ejemplos.
#### `--verbose`
Aumentar el nivel de detalle de registro. Use--debug para registros de depuración completos.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre cómo instalar el **mssqlctl** herramienta, consulte [instalar mssqlctl para administrar clústeres de SQL Server 2019 macrodatos](deploy-install-mssqlctl.md).