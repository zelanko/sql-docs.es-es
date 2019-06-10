---
title: referencia de configuración de clúster mssqlctl
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para los comandos de clúster mssqlctl.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 05/22/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 74097057702ad32a803c440d92b0ed7c8f855880
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66779424"
---
# <a name="mssqlctl-cluster-config"></a>Configuración de clúster mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

El siguiente artículo proporciona la referencia para la **cluster config** comandos en el **mssqlctl** herramienta. Para obtener más información acerca de otros **mssqlctl** comandos, consulte [mssqlctl referencia](reference-mssqlctl.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[presentación de configuración de clúster mssqlctl](#mssqlctl-cluster-config-show) | Obtiene la configuración actual de SQL Server Big Data del clúster.
[init de configuración de clúster mssqlctl](#mssqlctl-cluster-config-init) | Inicializa que cree un perfil de configuración de clúster que se puede usar con el clúster.
[lista de configuración de clúster mssqlctl](#mssqlctl-cluster-config-list) | Enumera las opciones del archivo de configuración disponibles.
[sección de configuración de clúster mssqlctl](reference-mssqlctl-cluster-config-section.md) | Comandos para trabajar con las secciones del archivo de configuración de clúster.
## <a name="mssqlctl-cluster-config-show"></a>presentación de configuración de clúster mssqlctl
Obtiene el archivo de configuración de SQL Server Big Data del clúster actual y lo envía al archivo de destino o bastante se imprime en la consola.
```bash
mssqlctl cluster config show [--target -t] 
                             [--force -f]
```
### <a name="examples"></a>Ejemplos
Mostrar la configuración del clúster en la consola
```bash
mssqlctl cluster config show
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--target -t`
Archivo de salida para almacenar el resultado en. Valor predeterminado: se dirigen a stdout.
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
## <a name="mssqlctl-cluster-config-init"></a>init de configuración de clúster mssqlctl
Inicializa que cree un perfil de configuración de clúster que se puede usar con el clúster. La fuente específica del perfil de configuración puede especificarse en los argumentos de 3 opciones.
```bash
mssqlctl cluster config init [--target -t] 
                             [--src -s]  
                             [--force -f]
```
### <a name="examples"></a>Ejemplos
Experiencia de init de configuración de clúster - guiada recibirá indicaciones para los valores necesarios.
```bash
mssqlctl cluster config init
```
Init config con argumentos del clúster, crea un perfil de configuración de aks-dev-test en. / custom.json.
```bash
mssqlctl cluster config init --src aks-dev-test.json --target custom.json
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--target -t`
Colocado en la ruta de acceso de donde desea que el perfil de configuración, el valor predeterminado es cwd con custom-config.json.
#### `--src -s`
Origen del perfil de configuración: ['aks-dev-test.json', ' kubeadm-dev-test.json', ' minikube-dev-test.json']
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
## <a name="mssqlctl-cluster-config-list"></a>lista de configuración de clúster mssqlctl
Enumera las opciones de archivo de configuración disponibles para su uso en init de la configuración de clúster
```bash
mssqlctl cluster config list [--config-file -c] 
                             
```
### <a name="examples"></a>Ejemplos
Muestra todos los nombres de perfil de configuración disponibles.
```bash
mssqlctl cluster config list
```
Muestra el json de un perfil de configuración específico.
```bash
mssqlctl cluster config list --config-file aks-dev-test.json
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--config-file -c`
Archivo de configuración predeterminado: ['aks-dev-test.json', ' kubeadm-dev-test.json', ' minikube-dev-test.json']
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