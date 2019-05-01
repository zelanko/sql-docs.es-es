---
title: referencia de sección de configuración de clúster mssqlctl
titleSuffix: SQL Server big data clusters
description: Artículo de referencia de comandos de sección de configuración de clúster mssqlctl.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d5a793e7d0fcaf782a09a4981491ef0a8d90ab5a
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/24/2019
ms.locfileid: "63759142"
---
# <a name="mssqlctl-cluster-config-section"></a>Sección configuración de clúster mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

El siguiente artículo proporciona la referencia para la **sección de configuración de clúster** comandos en el **mssqlctl** herramienta. Para obtener más información acerca de otros **mssqlctl** comandos, consulte [mssqlctl referencia](reference-mssqlctl.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[Obtiene la sección de configuración de clúster mssqlctl](#mssqlctl-cluster-config-section-get) | Obtiene una sección de un archivo de configuración.
[conjunto de sección de configuración de clúster mssqlctl](#mssqlctl-cluster-config-section-set) | Establece una sección de un archivo de configuración.
## <a name="mssqlctl-cluster-config-section-get"></a>Obtiene la sección de configuración de clúster mssqlctl
Obtiene la sección especificada del archivo de configuración seleccionado según la ruta de acceso json especificada.
```bash
mssqlctl cluster config section get --json-path -j 
                                    --config-file -f  
                                    [--target -t]
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--json-path -j`
La ruta de acceso de la clave de json que conduce a la sección o el valor que desee en el archivo de configuración, es decir, key1.key2.key3. Usa el lenguaje de consulta de jsonpath https://github.com/h2non/jsonpath-ng, por ejemplo: -j ' $. spec.pools [? () @.spec.type == "Master")]... puntos de conexión
#### `--config-file -f`
Ruta de acceso de archivo de configuración de clúster.
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--target -t`
Coloca la ruta de acceso de donde desea que el archivo de sección.
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
## <a name="mssqlctl-cluster-config-section-set"></a>conjunto de sección de configuración de clúster mssqlctl
Establece la sección especificada en el archivo de configuración seleccionado según la ruta de acceso json especificada.
```bash
mssqlctl cluster config section set --config-file -f 
                                    [--json-values -j]  
                                    [--patch-file -p]
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--config-file -f`
Ruta de acceso del archivo de configuración de clúster de la configuración que le gustaría establecer
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--json-values -j`
Una lista de pares clave-valor de rutas de acceso a los valores json: key1.subkey1=value1,key2.subkey2=value2. Puede proporcionar insertada valores json, como: clave = "{"tipo":"clúster","name":"test-cluster"}' o proporcione una ruta de acceso de archivo, como key=./values.json
#### `--patch-file -p`
Ruta de acceso a un archivo json de revisión que se basa en la biblioteca de jsonpatch y jsonpath: https://github.com/stefankoegl/python-json-patch , https://github.com/h2non/jsonpath-ng -un ejemplo sencillo: {"revisión": [{"op": "add", "path": "metadata.name", "value": "test"}, {"op": "add", "path": "metadata.array", "value": [1, 2, 3]}]} Incluya la clave "revisión" y que el valor sea una matriz de las revisiones que se va a hacer.  Se ejecuta como tal. Un ejemplo más complejo: {"revisión": [{"op": "reemplazar", "path": "$. spec.pools [? () @.spec.type == 'Master')]... puntos de conexión","value": {"name": "Nuevo punto de conexión"}}]}
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

Para obtener más información acerca de otros **mssqlctl** comandos, consulte [mssqlctl referencia](reference-mssqlctl.md). Para obtener más información sobre cómo instalar el **mssqlctl** herramienta, consulte [instalar mssqlctl para administrar clústeres de SQL Server 2019 macrodatos](deploy-install-mssqlctl.md).