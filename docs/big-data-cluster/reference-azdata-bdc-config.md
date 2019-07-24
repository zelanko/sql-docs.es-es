---
title: referencia de configuración de azdata BDC
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para los comandos BDC de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ed777391af3695da69e04c0e2693cff912c76771
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426295"
---
# <a name="azdata-bdc-config"></a>configuración de azdata BDC

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En el siguiente artículo se proporciona una referencia para los comandos de **configuración de BDC** en la herramienta **azdata** . Para obtener más información sobre otros comandos de **azdata** , consulte [referencia de azdata](reference-azdata.md).

## <a name="commands"></a>Comandos:
|     |     |
| --- | --- |
[azdata de configuración de BDC](#azdata-bdc-config-init) | Inicializa un perfil de configuración de clúster de Big Data que se puede usar con la creación de clústeres.
[azdata lista de configuración de BDC](#azdata-bdc-config-list) | Muestra las opciones de Perfil de configuración disponibles.
[azdata configuración de BDC](#azdata-bdc-config-show) | Muestra la configuración actual del BDC o la configuración de un archivo local que especifique, es decir, personalizado/cluster. JSON.
[azdata Agregar configuración de BDC](#azdata-bdc-config-add) | Agregue un valor para una ruta de acceso JSON en un archivo de configuración.
[quitar configuración de BDC de azdata](#azdata-bdc-config-remove) | Quite un valor para una ruta de acceso JSON en un archivo de configuración.
[azdata de configuración de BDC](#azdata-bdc-config-replace) | Reemplace un valor para una ruta de acceso JSON en un archivo de configuración.
[revisión de configuración de BDC de azdata](#azdata-bdc-config-patch) | Revisa un archivo de configuración basado en un archivo de revisión JSON.
## <a name="azdata-bdc-config-init"></a>azdata de configuración de BDC
Inicializa un perfil de configuración de clúster de Big Data que se puede usar con la creación de clústeres. El origen específico del perfil de configuración se puede especificar en los argumentos de 3 elecciones.
```bash
azdata bdc config init [--target -t] 
                       [--source -s]  
                       [--force -f]  
                       [--accept-eula -a]
```
### <a name="examples"></a>Ejemplos
Experiencia de inicialización de configuración de BDC guiada: recibirá mensajes para los valores necesarios.
```bash
azdata bdc config init
```
BDC config init with arguments, crea un perfil de configuración de AKS-dev-test en./Custom.
```bash
azdata bdc config init --source aks-dev-test --target custom
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--target -t`
Ruta de acceso del archivo donde desea que se ubique el perfil de configuración. el valor predeterminado es CWD con Custom-config. JSON.
#### `--source -s`
Origen de Perfil de configuración: [' AKS-dev-test ', ' kubeadm-dev-test ', ' minikube-dev-test ']
#### `--force -f`
Forzar la sobrescritura del archivo de destino.
#### `--accept-eula -a`
¿Acepta los términos de licencia? [sí/no]. Si no desea utilizar este argumento, puede establecer la variable de entorno ACCEPT_EULA en "Yes". Los términos de licencia de este producto se pueden ver https://aka.ms/azdata-eula en.
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumenta el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestra este mensaje de ayuda y sale.
#### `--output -o`
Formato de salida.  Valores permitidos: JSON, jsonc, Table y TSV.  Valor predeterminado: JSON.
#### `--query -q`
Cadena de consulta de JMESPath. Vea [http://jmespath.org/](http://jmespath.org/]) para obtener más información y ejemplos.
#### `--verbose`
Aumenta el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.
## <a name="azdata-bdc-config-list"></a>azdata lista de configuración de BDC
Muestra las opciones de Perfil de configuración disponibles para su uso en`bdc config init`
```bash
azdata bdc config list [--config-profile -c] 
                       [--type -t]  
                       [--accept-eula -a]
```
### <a name="examples"></a>Ejemplos
Muestra todos los nombres de Perfil de configuración disponibles.
```bash
azdata bdc config list
```
Muestra JSON de un perfil de configuración específico.
```bash
azdata bdc config list --config-profile aks-dev-test
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--config-profile -c`
Perfil de configuración predeterminado: [' AKS-dev-test ', ' kubeadm-dev-test ', ' minikube-dev-test ']
#### `--type -t`
El tipo de configuración que desea ver.
`cluster`
#### `--accept-eula -a`
¿Acepta los términos de licencia? [sí/no]. Si no desea utilizar este argumento, puede establecer la variable de entorno ACCEPT_EULA en "Yes". Los términos de licencia de este producto se pueden ver https://aka.ms/azdata-eula en.
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumenta el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestra este mensaje de ayuda y sale.
#### `--output -o`
Formato de salida.  Valores permitidos: JSON, jsonc, Table y TSV.  Valor predeterminado: JSON.
#### `--query -q`
Cadena de consulta de JMESPath. Vea [http://jmespath.org/](http://jmespath.org/]) para obtener más información y ejemplos.
#### `--verbose`
Aumenta el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.
## <a name="azdata-bdc-config-show"></a>azdata configuración de BDC
Muestra la configuración actual del BDC o la configuración de un archivo local que especifique, es decir, personalizado/cluster. JSON. El comando también puede tomar una ruta de acceso JSON si desea obtener solo una sección.  También puede especificar un archivo de destino para la salida.  Si no se especifica un archivo de destino, solo se generará en el terminal.
```bash
azdata bdc config show [--config-file -c] 
                       [--target -t]  
                       [--json-path -j]  
                       [--force -f]
```
### <a name="examples"></a>Ejemplos
Mostrar la configuración de BDC en la consola
```bash
azdata bdc config show
```
En un archivo de configuración local, obtenga un valor al final de una ruta de acceso de clave JSON simple.
```bash
azdata bdc config show --config-file custom-config/cluster.json --json-path 'metadata.name' --target section.json
```
En un archivo de configuración local, obtiene un valor al final de una ruta de acceso de clave JSON con un condicional
```bash
azdata bdc config show --config-file custom-config/cluster.json  --json-path '$.spec.pools[?(@.spec.type=="Storage")].spec' --target section.json
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--config-file -c`
Ruta de acceso del archivo de configuración del clúster de Big Data si no desea la configuración del clúster en el que está currentlylogged, es decir, Custom/cluster. JSON
#### `--target -t`
Archivo de salida en el que se almacena el resultado. Valor predeterminado: dirigido a stdout.
#### `--json-path -j`
La ruta de acceso de la clave JSON que conduce a la sección o el valor que desea de la configuración, es decir, Key1. KEY2. key3. Usa el lenguaje de consulta jsonpath https://jsonpath.com/ ,, por ejemplo:-j ' $. spec. pools [? ( @.spec.type = = "Master")].. extremos
#### `--force -f`
Forzar la sobrescritura del archivo de destino.
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumenta el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestra este mensaje de ayuda y sale.
#### `--output -o`
Formato de salida.  Valores permitidos: JSON, jsonc, Table y TSV.  Valor predeterminado: JSON.
#### `--query -q`
Cadena de consulta de JMESPath. Vea [http://jmespath.org/](http://jmespath.org/]) para obtener más información y ejemplos.
#### `--verbose`
Aumenta el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.
## <a name="azdata-bdc-config-add"></a>azdata Agregar configuración de BDC
Agrega el valor en la ruta de acceso JSON en el archivo de configuración.  Todos los ejemplos siguientes se proporcionan en bash.  Si usa otra línea de comandos, tenga en cuenta que puede que necesite escapequotations correctamente.  Como alternativa, puede usar la funcionalidad de archivo de revisión.
```bash
azdata bdc config add --config-file -c 
                      --json-values -j
```
### <a name="examples"></a>Ejemplos
Ex 1-agregar almacenamiento de plano de control.
```bash
azdata bdc config add --config-file custom/control.json --json-values 'spec.storage={"accessMode":"ReadWriteOnce","className":"managed-premium","size":"10Gi"}'
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--config-file -c`
Ruta de acceso del archivo de configuración del clúster de Big Data de la configuración que desea establecer, es decir, Custom/cluster. JSON
#### `--json-values -j`
Una lista de pares clave-valor de rutas de acceso JSON a valores: Key1. SUBKEY1 = value1, KEY2. subkey2 = value2. Puede proporcionar valores JSON en línea como: clave = ' {' Kind ': ' cluster ', ' name ': ' test-cluster '} ' o proporcionar una ruta de acceso de archivo, como Key =./Values.JSON. Agregar no admite los condicionales.  Consulte http://jsonpatch.com/ para obtener ejemplos de cómo debería ser la ruta de acceso.  Si desea obtener acceso a una matriz, debe hacerlo indicando el índice, como Key. 0 = Value.
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumenta el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestra este mensaje de ayuda y sale.
#### `--output -o`
Formato de salida.  Valores permitidos: JSON, jsonc, Table y TSV.  Valor predeterminado: JSON.
#### `--query -q`
Cadena de consulta de JMESPath. Vea [http://jmespath.org/](http://jmespath.org/]) para obtener más información y ejemplos.
#### `--verbose`
Aumenta el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.
## <a name="azdata-bdc-config-remove"></a>quitar configuración de BDC de azdata
Quita el valor de la ruta de acceso JSON del archivo de configuración.  Todos los ejemplos siguientes se proporcionan en bash.  Si usa otra línea de comandos, tenga en cuenta que puede que necesite escapequotations correctamente.  Como alternativa, puede usar la funcionalidad de archivo de revisión.
```bash
azdata bdc config remove --config-file -c 
                         --json-path -j
```
### <a name="examples"></a>Ejemplos
Ex 1: quitar el almacenamiento del plano de control.
```bash
azdata bdc config remove --config-file custom/control.json --json-path '.spec.storage'
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--config-file -c`
Ruta de acceso del archivo de configuración del clúster de Big Data de la configuración que desea establecer, es decir, Custom/cluster. JSON
#### `--json-path -j`
Una lista de rutas de acceso JSON basadas en la biblioteca jsonpatch que indica los valores que desea quitar, como: Key1. SUBKEY1, KEY2. subkey2. Quitar no es compatible con los condicionales. Consulte http://jsonpatch.com/ para obtener ejemplos de cómo debería ser la ruta de acceso.  Si desea obtener acceso a una matriz, debe hacerlo indicando el índice, como Key. 0 = Value.
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumenta el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestra este mensaje de ayuda y sale.
#### `--output -o`
Formato de salida.  Valores permitidos: JSON, jsonc, Table y TSV.  Valor predeterminado: JSON.
#### `--query -q`
Cadena de consulta de JMESPath. Vea [http://jmespath.org/](http://jmespath.org/]) para obtener más información y ejemplos.
#### `--verbose`
Aumenta el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.
## <a name="azdata-bdc-config-replace"></a>azdata de configuración de BDC
Reemplaza el valor de la ruta de acceso JSON en el archivo de configuración.  Todos los examplesbelow se proporcionan en bash.  Si usa otra línea de comandos, tenga en cuenta que puede que necesite escapequotations correctamente.  Como alternativa, puede usar la funcionalidad de archivo de revisión.
```bash
azdata bdc config replace --config-file -c 
                          --json-values -j
```
### <a name="examples"></a>Ejemplos
Ex 1: reemplazar el puerto de un punto de conexión único (punto de conexión del controlador).
```bash
azdata bdc config replace --config-file custom/control.json --json-values '$.spec.endpoints[?(@.name=="Controller")].port=30080'
```
Ex 2-reemplazar el almacenamiento del plano de control.
```bash
azdata bdc config replace --config-file custom/control.json --json-values 'spec.storage={"accessMode":"ReadWriteOnce","className":"managed-premium","size":"10Gi"}'
```
Ex 3-reemplazar el almacenamiento del grupo, incluidas las réplicas (grupo de almacenamiento).
```bash
azdata bdc config replace --config-file custom/cluster.json --json-values '$.spec.pools[?(@.spec.type == "Storage")].spec={"replicas": 2,"storage": {"className": "managed-premium","size": "10Gi","accessMode": "ReadWriteOnce"},"type": "Storage"}'
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--config-file -c`
Ruta de acceso del archivo de configuración del clúster de Big Data de la configuración que desea establecer, es decir, Custom/cluster. JSON
#### `--json-values -j`
Una lista de pares clave-valor de rutas de acceso JSON a valores: Key1. SUBKEY1 = value1, KEY2. subkey2 = value2. Puede proporcionar valores JSON en línea como: clave = ' {' Kind ': ' cluster ', ' name ': ' test-cluster '} ' o proporcionar una ruta de acceso de archivo, como Key =./Values.JSON. Replace admite los condicionales a través de la biblioteca jsonpath.  Para usar esto, inicie la ruta de acceso con un $. Esto le permitirá hacer un condicional como-j $. Key1. KEY2 [? ( @.key3= = ' someValue ']. key4 = valor. Puede ver los ejemplos siguientes. Para obtener más ayuda, consulte: https://jsonpath.com/
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumenta el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestra este mensaje de ayuda y sale.
#### `--output -o`
Formato de salida.  Valores permitidos: JSON, jsonc, Table y TSV.  Valor predeterminado: JSON.
#### `--query -q`
Cadena de consulta de JMESPath. Vea [http://jmespath.org/](http://jmespath.org/]) para obtener más información y ejemplos.
#### `--verbose`
Aumenta el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.
## <a name="azdata-bdc-config-patch"></a>revisión de configuración de BDC de azdata
Revisa el archivo de configuración según el archivo de revisión especificado. Consulte http://jsonpatch.com/ para comprender mejor cómo se deben crear las rutas de acceso. La operación de reemplazo puede usar los condicionales en su ruta de acceso debido https://jsonpath.com/ a la biblioteca jsonpath. Todos los archivos JSON de revisión deben comenzar con una clave de "patch" que tenga una matriz de revisiones con su correspondiente operación (agregar, reemplazar, quitar), ruta de acceso y valor. La operación "quitar" no requiere un valor, solo una ruta de acceso. Vea los ejemplos siguientes.
```bash
azdata bdc config patch --config-file -c 
                        --patch-file -p
```
### <a name="examples"></a>Ejemplos
Ex 1: reemplazar el puerto de un punto de conexión único (punto de conexión del controlador) por el archivo de revisión.
```bash
azdata bdc config patch --config-file custom/control.json --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":"$.spec.endpoints[?(@.name=='Controller')].port","value":30080}]}
```
Ex 2-reemplazar el almacenamiento del plano de control por el archivo de revisión.
```bash
azdata bdc config patch --config-file custom/control.json --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":".spec.storage","value":{"accessMode":"ReadWriteMany","className":"managed-premium","size":"10Gi"}}]}
```
Ex 3-reemplazar el almacenamiento del grupo, incluidas las réplicas (grupo de almacenamiento) con el archivo de revisión.
```bash
azdata bdc config patch --config-file custom/cluster.json --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":"$.spec.pools[?(@.spec.type == 'Storage')].spec","value":{"replicas": 2,"storage": {"className": "managed-premium","size": "10Gi","accessMode": "ReadWriteOnce"},"type": "Storage"}}]}
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--config-file -c`
Ruta de acceso del archivo de configuración del clúster de Big Data de la configuración que desea establecer, es decir, Custom/cluster. JSON
#### `--patch-file -p`
Ruta de acceso a un archivo JSON de revisión que se basa en la http://jsonpatch.com/ biblioteca jsonpatch:. Debe iniciar el archivo JSON de la revisión con una clave denominada "patch", cuyo valor es una matriz de operaciones patch que pretende realizar. Para la ruta de acceso de una operación de revisión, puede usar la notación de puntos, como Key1. KEY2 para la mayoría de las operaciones. Si desea realizar una operación de reemplazo y está reemplazando un valor en una matriz que requiere un condicional, use la notación jsonpath iniciando la ruta de acceso con un $. Esto le permitirá hacer un condicional como $. Key1. KEY2 [? ( @.key3= = ' someValue ']. key4. Vea los ejemplos siguientes. Para obtener ayuda adicional con los condicionales, consulte https://jsonpath.com/:.
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumenta el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestra este mensaje de ayuda y sale.
#### `--output -o`
Formato de salida.  Valores permitidos: JSON, jsonc, Table y TSV.  Valor predeterminado: JSON.
#### `--query -q`
Cadena de consulta de JMESPath. Vea [http://jmespath.org/](http://jmespath.org/]) para obtener más información y ejemplos.
#### `--verbose`
Aumenta el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre otros comandos de **azdata** , consulte [referencia de azdata](reference-azdata.md). Para obtener más información sobre cómo instalar la herramienta **azdata** , consulte [instalación de azdata para administrar clústeres de macrodatos SQL Server 2019](deploy-install-azdata.md).