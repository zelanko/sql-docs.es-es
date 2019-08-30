---
title: Referencia de azdata bdc config
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para los comandos de configuración de azdata BDC.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: cb999ede4516f903b7d2f409e53940adc79b4f9a
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155279"
---
# <a name="azdata-bdc-config"></a>azdata bdc config

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

Este artículo es un artículo de referencia para **azdata**. 

## <a name="commands"></a>Comandos:
|     |     |
| --- | --- |
[azdata bdc config init](#azdata-bdc-config-init) | Inicializa un perfil de configuración de clúster de macrodatos que puede usarse con la creación de clústeres.
[azdata bdc config list](#azdata-bdc-config-list) | Muestra una lista de opciones de perfil de configuración disponibles.
[azdata bdc config show](#azdata-bdc-config-show) | Muestra la configuración actual del BDC o la configuración de un archivo local que especifique, es decir, personalizado/BDC. JSON.
[azdata bdc config add](#azdata-bdc-config-add) | Agrega un valor a una ruta de acceso json en un archivo de configuración.
[azdata bdc config remove](#azdata-bdc-config-remove) | Quita un valor de una ruta de acceso json en un archivo de configuración.
[azdata bdc config replace](#azdata-bdc-config-replace) | Reemplaza un valor de una ruta de acceso json en un archivo de configuración.
[azdata bdc config patch](#azdata-bdc-config-patch) | Aplica una revisión en un archivo de configuración basándose en un archivo de revisión json.
## <a name="azdata-bdc-config-init"></a>azdata bdc config init
Inicializa un perfil de configuración de clúster de macrodatos que puede usarse con la creación de clústeres. El origen concreto del perfil de configuración se puede especificar en los argumentos desde tres opciones.
```bash
azdata bdc config init [--target -t] 
                       [--source -s]  
                       [--force -f]  
                       [--accept-eula -a]
```
### <a name="examples"></a>Ejemplos
Experiencia de inicialización de configuración de BDC guiada: se le solicitarán los valores necesarios.
```bash
azdata bdc config init
```
Inicialización de configuración de BDC con argumentos, se crea un perfil de configuración de aks-dev-test en ./custom.
```bash
azdata bdc config init --source aks-dev-test --target custom
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--target -t`
Ruta del archivo donde quiera colocar el perfil de configuración (de forma predeterminada, se usa cwd con custom-config.json).
#### `--source -s`
Origen de Perfil de configuración: [' AKS-dev-test ', ' kubeadm-Prod ', ' minikube-dev-test ', ' kubeadm-dev-test ']
#### `--force -f`
Obliga a sobrescribir el archivo de destino.
#### `--accept-eula -a`
¿Acepta los términos de licencia? [sí/no]. Si no quiere usar este argumento, puede establecer la variable de entorno ACCEPT_EULA en “yes”. Los términos de licencia de este producto se pueden ver en https://aka.ms/azdata-eula.
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumente el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestre este mensaje de ayuda y salga.
#### `--output -o`
Formato de salida.  Valores permitidos: json, jsonc, table y tsv.  Valor predeterminado: json.
#### `--query -q`
Cadena de consulta de JMESPath. Para obtener más información y ejemplos, vea [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Aumente el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.
## <a name="azdata-bdc-config-list"></a>azdata bdc config list
Muestra una lista de las opciones disponibles del perfil de configuración para su uso en `bdc config init`.
```bash
azdata bdc config list [--config-profile -c] 
                       [--type -t]  
                       [--accept-eula -a]
```
### <a name="examples"></a>Ejemplos
Muestra todos los nombres disponibles del perfil de configuración.
```bash
azdata bdc config list
```
Muestra código json de un perfil de configuración específico.
```bash
azdata bdc config list --config-profile aks-dev-test
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--config-profile -c`
Perfil de configuración predeterminado: [' AKS-dev-test ', ' kubeadm-Prod ', ' minikube-dev-test ', ' kubeadm-dev-test ']
#### `--type -t`
El tipo de configuración que quiere ver.
`cluster`
#### `--accept-eula -a`
¿Acepta los términos de licencia? [sí/no]. Si no quiere usar este argumento, puede establecer la variable de entorno ACCEPT_EULA en “yes”. Los términos de licencia de este producto se pueden ver en https://aka.ms/azdata-eula.
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumente el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestre este mensaje de ayuda y salga.
#### `--output -o`
Formato de salida.  Valores permitidos: json, jsonc, table y tsv.  Valor predeterminado: json.
#### `--query -q`
Cadena de consulta de JMESPath. Para obtener más información y ejemplos, vea [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Aumente el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.
## <a name="azdata-bdc-config-show"></a>azdata bdc config show
Muestra la configuración actual del BDC o la configuración de un archivo local que especifique, es decir, personalizado/BDC. JSON. El comando también puede admitir una ruta de acceso json si quiere obtener únicamente una sección.  También puede especificar un archivo de destino donde quiera enviar el resultado.  Si no se especifica un archivo de destino, el resultado se mostrará en el terminal.
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
En un archivo de configuración local, obtiene un valor al final de una ruta de clave json sencilla.
```bash
azdata bdc config show --config-file custom-config/bdc.json --json-path 'metadata.name' --target section.json
```
En un archivo de configuración local, obtiene los recursos de un servicio.
```bash
azdata bdc config show --config-file custom-config/bdc.json  --json-path '$.spec.services.sql.resources' --target section.json
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--config-file -c`
Ruta de acceso del archivo de configuración del clúster de Big Data si no desea la configuración del clúster en el que está currentlylogged, es decir, Custom/BDC. JSON
#### `--target -t`
Archivo de salida donde se almacenará el resultado. Predeterminado: se dirige a StdOut.
#### `--json-path -j`
La ruta de la clave json que lleva a la sección o valor y que quiere obtener de la configuración (por ejemplo, “clave1.clave2.clave3”). Usa el lenguaje de consulta de ruta de acceso json (https://jsonpath.com/ ), por ejemplo: -j '$.spec.pools[?(@.spec.type == "Master")]..endpoints'
#### `--force -f`
Obliga a sobrescribir el archivo de destino.
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumente el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestre este mensaje de ayuda y salga.
#### `--output -o`
Formato de salida.  Valores permitidos: json, jsonc, table y tsv.  Valor predeterminado: json.
#### `--query -q`
Cadena de consulta de JMESPath. Para obtener más información y ejemplos, vea [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Aumente el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.
## <a name="azdata-bdc-config-add"></a>azdata bdc config add
Agrega el valor a la ruta de acceso json del archivo de configuración.  Todos los ejemplos siguientes se proporcionan en Bash.  Si usa otra línea de comandos, tenga en cuenta que puede que necesite escapar las comillas (según corresponda).  Como alternativa, puede usar la función del archivo de revisión.
```bash
azdata bdc config add --config-file -c 
                      --json-values -j
```
### <a name="examples"></a>Ejemplos
Ejemplo 1: agregar almacenamiento de plano de control.
```bash
azdata bdc config add --config-file custom/control.json --json-values 'spec.storage={"accessMode":"ReadWriteOnce","className":"managed-premium","size":"10Gi"}'
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--config-file -c`
Ruta de acceso del archivo de configuración del clúster de Big Data de la configuración que desea establecer, es decir, Custom/BDC. JSON
#### `--json-values -j`
Lista de pares de clave y valor de rutas json a valores: clave1.subclave1=valor1,clave2.subclave2=valor2. Puede proporcionar valores json insertados (como key='{"kind":"cluster","name":"test-cluster"}'), o bien puede especificar una ruta de archivo (por ejemplo, clave=./valores.json). La adición no admite condicionales.  Si el valor insertado que está proporcionando es un par clave-valor con ' = ' y ', ' debe escapar esos caracteres.  Por ejemplo, Key1 = "KEY2\=val2\,Key3\=val3". Vea ejemplos de la apariencia de la ruta en http://jsonpatch.com/.  Para acceder a una matriz, necesita indicar del índice (por ejemplo, clave.0=valor).
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumente el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestre este mensaje de ayuda y salga.
#### `--output -o`
Formato de salida.  Valores permitidos: json, jsonc, table y tsv.  Valor predeterminado: json.
#### `--query -q`
Cadena de consulta de JMESPath. Para obtener más información y ejemplos, vea [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Aumente el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.
## <a name="azdata-bdc-config-remove"></a>azdata bdc config remove
Quita el valor de la ruta de acceso json del archivo de configuración.  Todos los ejemplos siguientes se proporcionan en Bash.  Si usa otra línea de comandos, tenga en cuenta que puede que necesite escapar las comillas (según corresponda).  Como alternativa, puede usar la función del archivo de revisión.
```bash
azdata bdc config remove --config-file -c 
                         --json-path -j
```
### <a name="examples"></a>Ejemplos
Ejemplo 1: quitar almacenamiento de plano de control.
```bash
azdata bdc config remove --config-file custom/control.json --json-path '.spec.storage'
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--config-file -c`
Ruta de acceso del archivo de configuración del clúster de Big Data de la configuración que desea establecer, es decir, Custom/BDC. JSON
#### `--json-path -j`
Lista de rutas json basadas en la biblioteca jsonpatch que indica qué valores quiere quitar (por ejemplo, “clave1.subclave1,clave2.subclave2”). La eliminación no admite el uso de condicionales. Vea ejemplos de la apariencia de la ruta en http://jsonpatch.com/.  Para acceder a una matriz, necesita indicar del índice (por ejemplo, clave.0=valor).
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumente el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestre este mensaje de ayuda y salga.
#### `--output -o`
Formato de salida.  Valores permitidos: json, jsonc, table y tsv.  Valor predeterminado: json.
#### `--query -q`
Cadena de consulta de JMESPath. Para obtener más información y ejemplos, vea [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Aumente el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.
## <a name="azdata-bdc-config-replace"></a>azdata bdc config replace
Reemplaza el valor en la ruta de acceso json del archivo de configuración.  Todos los ejemplos siguientes se proporcionan en Bash.  Si usa otra línea de comandos, tenga en cuenta que puede que necesite escapar las comillas (según corresponda).  Como alternativa, puede usar la función del archivo de revisión.
```bash
azdata bdc config replace --config-file -c 
                          --json-values -j
```
### <a name="examples"></a>Ejemplos
Ejemplo 1: reemplazar el puerto de un único punto de conexión (punto de conexión del controlador).
```bash
azdata bdc config replace --config-file custom/control.json --json-values '$.spec.endpoints[?(@.name=="Controller")].port=30080'
```
Ejemplo 2: reemplazar el almacenamiento de plano de control.
```bash
azdata bdc config replace --config-file custom/control.json --json-values 'spec.storage={"accessMode":"ReadWriteOnce","className":"managed-premium","size":"10Gi"}'
```
Ex 3-Reemplace Storage-0 Especificaciones de recursos, incluidas las réplicas.
```bash
azdata bdc config replace --config-file custom/bdc.json --json-values '$.spec.resources.storage-0.spec={"replicas": 2,"storage": {"className": "managed-premium","size": "10Gi","accessMode": "ReadWriteOnce"},"type": "Storage"}'
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--config-file -c`
Ruta de acceso del archivo de configuración del clúster de Big Data de la configuración que desea establecer, es decir, Custom/BDC. JSON
#### `--json-values -j`
Lista de pares de clave y valor de rutas json a valores: clave1.subclave1=valor1,clave2.subclave2=valor2. Puede proporcionar valores json insertados (como key='{"kind":"cluster","name":"test-cluster"}'), o bien puede especificar una ruta de archivo (por ejemplo, clave=./valores.json). El comando para reemplazar admite condicionales mediante la biblioteca jsonpath.  Para usar esto, inicie la ruta con un signo de $. De esta forma, podrá agregar una declaración condicional, como -j $.clave1.clave2[?(@.key3=='unValor'].clave4=valor. Si el valor insertado que está proporcionando es un par clave-valor con ' = ' y ', ' debe escapar esos caracteres.  Por ejemplo, Key1 = "KEY2\=val2\,Key3\=val3". A continuación, se muestran algunos ejemplos. Para obtener ayuda, vea: https://jsonpath.com/
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumente el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestre este mensaje de ayuda y salga.
#### `--output -o`
Formato de salida.  Valores permitidos: json, jsonc, table y tsv.  Valor predeterminado: json.
#### `--query -q`
Cadena de consulta de JMESPath. Para obtener más información y ejemplos, vea [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Aumente el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.
## <a name="azdata-bdc-config-patch"></a>azdata bdc config patch
Aplica una revisión en el archivo de configuración según el archivo de revisión especificado. Para obtener información sobre cómo crear las rutas, vea http://jsonpatch.com/. La operación de reemplazar puede usar declaraciones condicionales en la ruta debido a la biblioteca jsonpath https://jsonpath.com/. Todos los archivos json de revisión tienen que iniciarse con una clave de “patch”, que tiene una matriz de revisiones con la correspondiente operación (add [agregar], replace [reemplazar], remove [quitar]), ruta y valor. La operación “remove” (quitar) no necesita un valor, solo una ruta de acceso. A continuación, se muestran algunos ejemplos.
```bash
azdata bdc config patch --config-file -c 
                        --patch-file -p
```
### <a name="examples"></a>Ejemplos
Ejemplo 1: reemplazar el puerto de un único punto de conexión (punto de conexión del controlador) con un archivo de revisión.
```bash
azdata bdc config patch --config-file custom/control.json --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":"$.spec.endpoints[?(@.name=='Controller')].port","value":30080}]}
```
Ejemplo 2: reemplazar el almacenamiento de plano de control con un archivo de revisión.
```bash
azdata bdc config patch --config-file custom/control.json --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":".spec.storage","value":{"accessMode":"ReadWriteMany","className":"managed-premium","size":"10Gi"}}]}
```
Ejemplo 3: reemplazar el almacenamiento de grupos, incluidas las réplicas (grupo de almacenamiento) con un archivo de revisión.
```bash
azdata bdc config patch --config-file custom/bdc.json --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":"$.spec.resources.storage-0.spec","value":{"replicas": 2,"storage": {"className": "managed-premium","size": "10Gi","accessMode": "ReadWriteOnce"},"type": "Storage"}}]}
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--config-file -c`
Ruta de acceso del archivo de configuración del clúster de Big Data de la configuración que desea establecer, es decir, Custom/BDC. JSON
#### `--patch-file -p`
Ruta a un archivo json de revisión basado en la biblioteca jsonpatch: http://jsonpatch.com/. Tiene que empezar el archivo json de revisión con una clave denominada “patch”, cuyo valor es una matriz de operaciones de revisión que quiere realizar. Para la ruta de una operación de revisión, puede usar la notación de puntos (como clave1.clave2) para la mayoría de las operaciones. Si no quiere realizar una operación de reemplazo y va a reemplazar un valor en una matriz que necesita una condicional, use la notación jsonpath (para hacerlo, agregue un signo de $ al principio de la ruta de acceso). De esta forma, podrá agregar una declaración condicional, como $.clave1.clave2[?(@.key3=='unValor'].clave4. A continuación, se muestran algunos ejemplos. Para obtener más información sobre las declaraciones condicionales, vea: https://jsonpath.com/.
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumente el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestre este mensaje de ayuda y salga.
#### `--output -o`
Formato de salida.  Valores permitidos: json, jsonc, table y tsv.  Valor predeterminado: json.
#### `--query -q`
Cadena de consulta de JMESPath. Para obtener más información y ejemplos, vea [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Aumente el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.

## <a name="next-steps"></a>Pasos siguientes

- Para obtener más información sobre otros comandos de **azdata**, vea la [Referencia de azdata](reference-azdata.md). 

- Para obtener más información sobre cómo instalar la herramienta **azdata**, vea [Instalación de azdata para administrar clústeres de macrodatos de SQL Server 2019](deploy-install-azdata.md).
