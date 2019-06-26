---
title: referencia de sección de configuración de bdc mssqlctl
titleSuffix: SQL Server big data clusters
description: Artículo de referencia de comandos de sección de configuración de bdc mssqlctl.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2522aa41f860d7552df934ffc1751d2e7e8d43d1
ms.sourcegitcommit: ce5770d8b91c18ba5ad031e1a96a657bde4cae55
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/25/2019
ms.locfileid: "67394407"
---
# <a name="mssqlctl-bdc-config-section"></a>sección de configuración de bdc mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

El siguiente artículo proporciona la referencia para la **sección de configuración de bdc** comandos en el **mssqlctl** herramienta. Para obtener más información acerca de otros **mssqlctl** comandos, consulte [mssqlctl referencia](reference-mssqlctl.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[presentación de sección de configuración de bdc mssqlctl](#mssqlctl-bdc-config-section-show) | Obtiene una sección de un perfil de configuración.
[conjunto de sección de configuración de bdc mssqlctl](#mssqlctl-bdc-config-section-set) | Establece una sección de un perfil de configuración.
## <a name="mssqlctl-bdc-config-section-show"></a>presentación de sección de configuración de bdc mssqlctl
Obtiene la sección especificada desde el perfil de configuración seleccionado según la ruta de acceso json especificada.
```bash
mssqlctl bdc config section show --json-path -j 
                                 --config-profile -c  
                                 [--target -t]  
                                 [--force -f]
```
### <a name="examples"></a>Ejemplos
Obtiene un valor al final de una ruta de acceso json sencillo.
```bash
mssqlctl bdc config section show --config-profile custom-config --json-path 'metadata.name' --target section.json
```
Obtiene un valor al final de una ruta de acceso de clave de json con una instrucción condicional
```bash
mssqlctl bdc config section show --config-profile custom-config  --json-path '$.spec.pools[?(@.spec.type=="Storage")].spec' --target section.json
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--json-path -j`
La ruta de acceso de la clave de json que conduce a la sección o el valor que se desee en el archivo de cluster.json del perfil de configuración, es decir, key1.key2.key3. Usa el lenguaje de consulta de jsonpath https://github.com/h2non/jsonpath-ng, por ejemplo: -j ' $. spec.pools [? () @.spec.type == "Master")]... puntos de conexión
#### `--config-profile -c`
Ruta de acceso de perfil de configuración BDC.
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--target -t`
Coloca la ruta de acceso de donde desea que el archivo de sección. Valor predeterminado: se dirigen a stdout.
#### `--force -f`
Forzar la sobrescritura del archivo de destino.
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
## <a name="mssqlctl-bdc-config-section-set"></a>conjunto de sección de configuración de bdc mssqlctl
Establece la sección especificada en el perfil de configuración seleccionado según la ruta de acceso json especificada.  Examplesbelow todas se proporcionan en Bash.  Si usa otra línea de comandos, ten en cuenta que es posible que deba escapequotations adecuadamente.  Como alternativa, puede usar la funcionalidad del archivo de revisión.
```bash
mssqlctl bdc config section set --config-profile -c 
                                [--json-values -j]  
                                [--patch-file -p]
```
### <a name="examples"></a>Ejemplos
P. ej. 1 (inline): establezca el puerto de un único punto de conexión (punto de conexión del controlador).
```bash
mssqlctl bdc config section set --config-profile custom-config --json-values '$.spec.controlPlane.spec.endpoints[?(@.name=="Controller")].port=30080'
```
P. ej. 1 (patch): establezca el puerto de un único punto de conexión (punto de conexión del controlador) con un archivo de revisión.
```bash
mssqlctl bdc config section set --config-profile custom-config --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":"$.spec.controlPlane.spec.endpoints[?(@.name=='Controller')].port","value":30080}]}
```
Por ejemplo, 2 (inline) - almacenamiento de plano de control de conjunto.
```bash
mssqlctl bdc config section set --config-profile custom-config --json-values 'spec.controlPlane.spec.storage=spec.controlPlane.spec.storage={"accessMode":"ReadWriteOnce","className":"managed-premium","size":"10Gi"}'
```
Por ejemplo, 2 (patch): almacenamiento de plano de control de conjunto con un archivo de revisión.
```bash
mssqlctl bdc config section set --config-profile custom-config --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":"spec.controlPlane.spec.storage","value":{"accessMode":"ReadWriteMany","className":"managed-premium","size":"10Gi"}}]}
```
Ex 3(inline) - establecer el almacenamiento de grupo, incluidas las réplicas (bloque de almacenamiento).
```bash
mssqlctl bdc config section set --config-profile custom-config --json-values '$.spec.pools[?(@.spec.type == "Storage")].spec={"replicas": 2,"storage": {"className": "managed-premium","size": "10Gi","accessMode": "ReadWriteOnce"},"type": "Storage"}'
```
Ex 3 (patch): establecer el almacenamiento del grupo, incluidas las réplicas (bloque de almacenamiento) con un archivo de revisión.
```bash
mssqlctl bdc config section set --config-profile custom-config --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":"$.spec.pools[?(@.spec.type == 'Storage')].spec","value":{"replicas": 2,"storage": {"className": "managed-premium","size": "10Gi","accessMode": "ReadWriteOnce"},"type": "Storage"}}]}
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--config-profile -c`
Ruta de acceso del perfil de configuración BDC de la configuración que le gustaría establecer
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--json-values -j`
Una lista de pares clave-valor de rutas de acceso a los valores json: key1.subkey1=value1,key2.subkey2=value2. Puede proporcionar insertada valores json, como: clave = "{"tipo":"clúster","name":"test-cluster"}' o proporcione una ruta de acceso de archivo, como key=./values.json. Si desea establecer un valor que requiere una instrucción condicional, use la notación de jsonpath mediante el comienzo de la ruta de acceso con un carácter $. Esto le permitirá hacer una instrucción condicional, como -j $. key1.key2 [? () @.key3== "someValue"] .key4 = valor. Es posible que vea los ejemplos siguientes. Para obtener ayuda adicional, consulte: https://jsonpath.com/
#### `--patch-file -p`
Ruta de acceso a un archivo json de revisión que se basa en la biblioteca jsonpatch: http://jsonpatch.com/. Debe iniciar el archivo de revisión json con una clave denominada "revisión", cuyo valor es una matriz de las operaciones de revisiones que se va a hacer. La ruta de acceso de una operación de revisión, puede usar la notación de puntos, como key1.key2 para la mayoría de las operaciones. Si desea realizar una operación de reemplazo y va a reemplazar un valor en una matriz que requiere una instrucción condicional, use la notación de jsonpath mediante el comienzo de la ruta de acceso con un carácter $. Esto le permitirá hacer una instrucción condicional, como $. key1.key2 [? () @.key3== "someValue"] .key4. Consulte los ejemplos siguientes. Para obtener ayuda adicional, consulte: https://jsonpath.com/.
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