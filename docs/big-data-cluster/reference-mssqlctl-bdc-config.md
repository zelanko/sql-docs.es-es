---
title: referencia de configuración de bdc mssqlctl
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para los comandos de bdc mssqlctl.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
manager: jroth
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5c4182f216b13d4b56d1c37f6d003ad2ea6f5cf6
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67728684"
---
# <a name="mssqlctl-bdc-config"></a>configuración de bdc mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

El siguiente artículo proporciona la referencia para la **bdc config** comandos en el **mssqlctl** herramienta. Para obtener más información acerca de otros **mssqlctl** comandos, consulte [mssqlctl referencia](reference-mssqlctl.md).

## <a name="commands"></a>Comandos:
|     |     |
| --- | --- |
[mssqlctl bdc config show](#mssqlctl-bdc-config-show) | Obtiene la configuración actual del clúster de datos grande.
[mssqlctl bdc config init](#mssqlctl-bdc-config-init) | Inicializa un clúster grande de datos Crear perfil de configuración que se puede usar con el clúster.
[mssqlctl bdc config list](#mssqlctl-bdc-config-list) | Enumera las opciones de perfil de configuración disponibles.
[sección de configuración de bdc mssqlctl](reference-mssqlctl-bdc-config-section.md) | Comandos para trabajar con secciones individuales del perfil de configuración de clúster grande de datos.
## <a name="mssqlctl-bdc-config-show"></a>mssqlctl bdc config show
Obtiene el perfil de configuración actual del clúster de Big Data y lo envía al directorio de destino o bastante se imprime en la consola.
```bash
mssqlctl bdc config show [--target -t] 
                         [--force -f]
```
### <a name="examples"></a>Ejemplos
Mostrar la configuración BDC en la consola
```bash
mssqlctl bdc config show
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--target -t`
Archivo de salida para almacenar el resultado en. Valor predeterminado: se dirigen a stdout.
#### `--force -f`
Forzar la sobrescritura del archivo de destino.
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumenta el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestra este mensaje de ayuda y sale.
#### `--output -o`
Formato de salida.  Los valores permitidos: json, jsonc, table y tsv.  Predeterminado: json.
#### `--query -q`
Cadena de consulta de JMESPath. Consulte [ http://jmespath.org/ ](http://jmespath.org/]) para obtener más información y ejemplos.
#### `--verbose`
Aumenta el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.
## <a name="mssqlctl-bdc-config-init"></a>mssqlctl bdc config init
Inicializa un clúster grande de datos Crear perfil de configuración que se puede usar con el clúster. La fuente específica del perfil de configuración puede especificarse en los argumentos de 3 opciones.
```bash
mssqlctl bdc config init [--target -t] 
                         [--source -s]  
                         [--force -f]
```
### <a name="examples"></a>Ejemplos
Experiencia guiada de BDC config init - recibirá indicaciones para los valores necesarios.
```bash
mssqlctl bdc config init
```
Init config BDC con argumentos, se crea un perfil de configuración de aks-dev-test en. / personalizadas.
```bash
mssqlctl bdc config init --source aks-dev-test --target custom
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--target -t`
Colocado en la ruta de acceso de donde desea que el perfil de configuración, el valor predeterminado es cwd con custom-config.json.
#### `--source -s`
Origen del perfil de configuración: ['aks-dev-test', 'kubeadm-dev-test', 'minikube-dev-test']
#### `--force -f`
Forzar la sobrescritura del archivo de destino.
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumenta el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestra este mensaje de ayuda y sale.
#### `--output -o`
Formato de salida.  Los valores permitidos: json, jsonc, table y tsv.  Predeterminado: json.
#### `--query -q`
Cadena de consulta de JMESPath. Consulte [ http://jmespath.org/ ](http://jmespath.org/]) para obtener más información y ejemplos.
#### `--verbose`
Aumenta el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.
## <a name="mssqlctl-bdc-config-list"></a>mssqlctl bdc config list
Enumera las opciones de perfil de configuración disponibles para su uso en `bdc config init`
```bash
mssqlctl bdc config list [--config-profile -c] 
                         
```
### <a name="examples"></a>Ejemplos
Muestra todos los nombres de perfil de configuración disponibles.
```bash
mssqlctl bdc config list
```
Muestra el json de un perfil de configuración específico.
```bash
mssqlctl bdc config list --config-profile aks-dev-test
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--config-profile -c`
Perfil de configuración predeterminado: ['aks-dev-test', 'kubeadm-dev-test', 'minikube-dev-test']
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumenta el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestra este mensaje de ayuda y sale.
#### `--output -o`
Formato de salida.  Los valores permitidos: json, jsonc, table y tsv.  Predeterminado: json.
#### `--query -q`
Cadena de consulta de JMESPath. Consulte [ http://jmespath.org/ ](http://jmespath.org/]) para obtener más información y ejemplos.
#### `--verbose`
Aumenta el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de otros **mssqlctl** comandos, consulte [mssqlctl referencia](reference-mssqlctl.md). Para obtener más información sobre cómo instalar el **mssqlctl** herramienta, consulte [instalar mssqlctl para administrar clústeres de SQL Server 2019 macrodatos](deploy-install-mssqlctl.md).