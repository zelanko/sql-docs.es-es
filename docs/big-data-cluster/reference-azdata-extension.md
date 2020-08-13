---
title: Referencia de azdata extension
titleSuffix: SQL Server big data clusters
description: Artículo de referencia de los comandos azdata extension.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9e2585a77c3117df8514622728d0f09df93d7bc2
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87243006"
---
# <a name="azdata-extension"></a>azdata extension

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

En el artículo siguiente se proporciona una referencia de los comandos `sql` de la herramienta `azdata`. Para obtener más información sobre otros comandos de `azdata`, vea [Referencia de azdata](reference-azdata.md).

## <a name="commands"></a>Comandos
| Comando | Descripción |
| --- | --- |
[azdata extension add](#azdata-extension-add) | Agrega una extensión.
[azdata extension remove](#azdata-extension-remove) | Quita una extensión.
[azdata extension list](#azdata-extension-list) | Enumera todas las extensiones instaladas.
## <a name="azdata-extension-add"></a>azdata extension add
Agrega una extensión.
```bash
azdata extension add --source -s 
                     [--index]  
                     
[--pip-proxy]  
                     
[--pip-extra-index-urls]  
                     
[--yes -y]
```
### <a name="examples"></a>Ejemplos
Agregar una extensión desde una dirección URL.
```bash
azdata extension add --source https://contoso.com/some_ext-0.0.1-py2.py3-none-any.whl
```
Agregar una extensión desde un disco local.
```bash
azdata extension add --source ~/some_ext-0.0.1-py2.py3-none-any.whl
```
Agregue la extensión desde el disco local y use el proxy de pip para las dependencias.
```bash
azdata extension add --source ~/some_ext-0.0.1-py2.py3-none-any.whl --pip-proxy https://user:pass@proxy.server:8080
```
### <a name="required-parameters"></a>Parámetros obligatorios
#### `--source -s`
Ruta de acceso a una rueda de extensión en el disco o la dirección URL a una extensión
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--index`
Dirección URL base del índice de paquetes de Python (valor predeterminado: https://pypi.org/simple). Esto debería apuntar a un repositorio compatible con PEP 503 (la API de repositorio simple) o un directorio local con el mismo formato.
#### `--pip-proxy`
Proxy para que use pip para las dependencias de la extensión con el formato [usuario:contraseña@]proxy.servidor:puerto
#### `--pip-extra-index-urls`
Lista separada por espacios de direcciones URL adicionales de los índices de paquetes que se van a usar. Esto debería apuntar a un repositorio compatible con PEP 503 (la API de repositorio simple) o un directorio local con el mismo formato.
#### `--yes -y`
No solicita confirmación.
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumente el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestre este mensaje de ayuda y salga.
#### `--output -o`
Formato de salida.  Valores permitidos: json, jsonc, table y tsv.  Valor predeterminado: json.
#### `--query -q`
Cadena de consulta de JMESPath. Para obtener más información y ejemplos, vea [http://jmespath.org/](http://jmespath.org).
#### `--verbose`
Aumente el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.
## <a name="azdata-extension-remove"></a>azdata extension remove
Quita una extensión.
```bash
azdata extension remove --name -n 
                        [--yes -y]
```
### <a name="examples"></a>Ejemplos
Quita una extensión.
```bash
azdata extension remove --name some-ext
```
### <a name="required-parameters"></a>Parámetros obligatorios
#### `--name -n`
Nombre de la extensión.
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--yes -y`
No solicita confirmación.
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumente el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestre este mensaje de ayuda y salga.
#### `--output -o`
Formato de salida.  Valores permitidos: json, jsonc, table y tsv.  Valor predeterminado: json.
#### `--query -q`
Cadena de consulta de JMESPath. Para obtener más información y ejemplos, vea [http://jmespath.org/](http://jmespath.org).
#### `--verbose`
Aumente el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.
## <a name="azdata-extension-list"></a>azdata extension list
Enumera todas las extensiones instaladas.
```bash
azdata extension list 
```
### <a name="examples"></a>Ejemplos
Enumerar extensiones.
```bash
azdata extension list
```
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumente el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestre este mensaje de ayuda y salga.
#### `--output -o`
Formato de salida.  Valores permitidos: json, jsonc, table y tsv.  Valor predeterminado: json.
#### `--query -q`
Cadena de consulta de JMESPath. Para obtener más información y ejemplos, vea [http://jmespath.org/](http://jmespath.org).
#### `--verbose`
Aumente el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre otros comandos de `azdata`, vea [Referencia de azdata](reference-azdata.md). Para obtener más información sobre cómo instalar la herramienta `azdata`, vea [Instalación de azdata para administrar clústeres de macrodatos de SQL Server 2019](deploy-install-azdata.md).
