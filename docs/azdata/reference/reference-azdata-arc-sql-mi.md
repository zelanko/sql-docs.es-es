---
title: Referencia de azdata arc sql mi
titleSuffix: SQL Server big data clusters
description: Artículo de referencia sobre los comandos de azdata arc sql mi.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 234a990cde52a6fd051410d30000413b9acfa3a0
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358683"
---
# <a name="azdata-arc-sql-mi"></a>azdata arc sql mi

Se aplica a [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)]

En el siguiente artículo se proporciona una referencia de los comandos **sql** de la herramienta **azdata**. Para obtener más información sobre otros comandos de **azdata**, vea la [Referencia de azdata](reference-azdata.md).

## <a name="commands"></a>Comandos

|Comando|Descripción|
| --- | --- |
[azdata arc sql mi create](#azdata-arc-sql-mi-create) | Crea una instancia de SQL Managed Instance.
[azdata arc sql mi edit](#azdata-arc-sql-mi-edit) | Edita la configuración de una instancia de SQL Managed Instance.
[azdata arc sql mi delete](#azdata-arc-sql-mi-delete) | Elimina una instancia de SQL Managed Instance.
[azdata arc sql mi show](#azdata-arc-sql-mi-show) | Muestra los detalles de una instancia de SQL Managed Instance.
[azdata arc sql mi list](#azdata-arc-sql-mi-list) | Enumera instancias de SQL Managed Instance.
[azdata arc sql mi config](reference-azdata-arc-sql-mi-config.md) | Comandos de configuración.
## <a name="azdata-arc-sql-mi-create"></a>azdata arc sql mi create
Para establecer la contraseña de la instancia de SQL Managed Instance, establezca la variable de entorno AZDATA_PASSWORD.
```bash
azdata arc sql mi create --name -n 
                         [--path]  
                         
[--cores-limit -cl]  
                         
[--cores-request -cr]  
                         
[--memory-limit -ml]  
                         
[--memory-request -mr]  
                         
[--storage-class-data -scd]  
                         
[--storage-class-logs -scl]  
                         
[--storage-class-data-logs -scdl]  
                         
[--storage-class-backups -scb]  
                         
[--volume-size-data -vsd]  
                         
[--volume-size-logs -vsl]  
                         
[--volume-size-data-logs -vsdl]  
                         
[--volume-size-backups -vsb]  
                         
[--no-external-endpoint]  
                         
[--dev]  
                         
[--no-wait]
```
### <a name="examples"></a>Ejemplos
Crea una instancia de SQL Managed Instance.
```bash
azdata arc sql mi create -n sqlmi1
```
### <a name="required-parameters"></a>Parámetros requeridos
#### `--name -n`
Nombre de la instancia de SQL Managed Instance.
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--path`
Ruta de acceso al archivo src del archivo JSON de la instancia de SQL Managed Instance.
#### `--cores-limit -cl`
Límite de núcleos de la instancia administrada como un entero.
#### `--cores-request -cr`
Solicitud de núcleos de la instancia administrada como un entero.
#### `--memory-limit -ml`
Límite de la capacidad de la instancia administrada como un entero.
#### `--memory-request -mr`
Solicitud de la capacidad de la instancia administrada como un entero de cantidad de memoria en GB.
#### `--storage-class-data -scd`
Clase de almacenamiento que se va a usar para los datos (.mdf). Si no se especifica ningún valor, no se especifica ninguna clase de almacenamiento, lo que da lugar a que Kubernetes use la predeterminada.
#### `--storage-class-logs -scl`
Clase de almacenamiento que se va a usar para los registros (/var/log). Si no se especifica ningún valor, no se especifica ninguna clase de almacenamiento, lo que da lugar a que Kubernetes use la predeterminada.
#### `--storage-class-data-logs -scdl`
Clase de almacenamiento que se va a usar para los registros de datos (.ldf). Si no se especifica ningún valor, no se especifica ninguna clase de almacenamiento, lo que da lugar a que Kubernetes use la predeterminada.
#### `--storage-class-backups -scb`
Clase de almacenamiento que se va a usar para las copias de seguridad (/var/opt/mssql/backups). Si no se especifica ningún valor, no se especifica ninguna clase de almacenamiento, lo que da lugar a que Kubernetes use la predeterminada.
#### `--volume-size-data -vsd`
Tamaño del volumen de almacenamiento que se va a usar para los datos como un número positivo seguido de K (kilobytes), MB (megabytes) o GB (gigabytes).
#### `--volume-size-logs -vsl`
Tamaño del volumen de almacenamiento que se va a usar para los registros como un número positivo seguido de K (kilobytes), MB (megabytes) o GB (gigabytes).
#### `--volume-size-data-logs -vsdl`
Tamaño del volumen de almacenamiento que se va a usar para los registros de datos como un número positivo seguido de K (kilobytes), MB (megabytes) o GB (gigabytes).
#### `--volume-size-backups -vsb`
Tamaño del volumen de almacenamiento que se va a usar para las copias de seguridad como un número positivo seguido de K (kilobytes), MB (megabytes) o GB (gigabytes).
#### `--no-external-endpoint`
Si se especifica, no se crea ningún servicio externo. De lo contrario, se crea un servicio externo con el mismo tipo de servicio que el controlador de datos.
#### `--dev`
Si se especifica, se considera una instancia de desarrollo y no se factura.
#### `--no-wait`
Si se especifica, el comando no espera a que la instancia esté lista para devolver un valor.
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
## <a name="azdata-arc-sql-mi-edit"></a>azdata arc sql mi edit
Edita la configuración de una instancia de SQL Managed Instance.
```bash
azdata arc sql mi edit --name -n 
                       [--path]  
                       
[--cores-limit -cl]  
                       
[--cores-request -cr]  
                       
[--memory-limit -ml]  
                       
[--memory-request -mr]  
                       
[--dev]  
                       
[--no-wait]
```
### <a name="examples"></a>Ejemplos
Edita la configuración de una instancia de SQL Managed Instance.
```bash
azdata arc sql mi edit --path ./spec.json -n sqlmi1
```
### <a name="required-parameters"></a>Parámetros requeridos
#### `--name -n`
Nombre de la instancia de SQL Managed Instance que se va a editar. El nombre con el que se implementa la instancia no se puede cambiar.
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--path`
Ruta de acceso al archivo src del archivo JSON de la instancia de SQL Managed Instance.
#### `--cores-limit -cl`
Límite de núcleos de la instancia administrada como un entero.
#### `--cores-request -cr`
Solicitud de núcleos de la instancia administrada como un entero.
#### `--memory-limit -ml`
Límite de la capacidad de la instancia administrada como un entero.
#### `--memory-request -mr`
Solicitud de la capacidad de la instancia administrada como un entero de cantidad de memoria en GB.
#### `--dev`
Si se especifica, se considera una instancia de desarrollo y no se factura.
#### `--no-wait`
Si se especifica, el comando no espera a que la instancia esté lista para devolver un valor.
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
## <a name="azdata-arc-sql-mi-delete"></a>azdata arc sql mi delete
Elimina una instancia de SQL Managed Instance.
```bash
azdata arc sql mi delete --name -n 
                         
```
### <a name="examples"></a>Ejemplos
Elimina una instancia de SQL Managed Instance.
```bash
azdata arc sql mi delete -n sqlmi1
```
### <a name="required-parameters"></a>Parámetros requeridos
#### `--name -n`
Nombre de la instancia de SQL Managed Instance que se va a eliminar.
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
## <a name="azdata-arc-sql-mi-show"></a>azdata arc sql mi show
Muestra los detalles de una instancia de SQL Managed Instance.
```bash
azdata arc sql mi show --name -n 
                       [--path -p]
```
### <a name="examples"></a>Ejemplos
Muestra los detalles de una instancia de SQL Managed Instance.
```bash
azdata arc sql mi show -n sqlmi1
```
### <a name="required-parameters"></a>Parámetros requeridos
#### `--name -n`
Nombre de la instancia de SQL Managed Instance que se va a mostrar.
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--path -p`
Ruta donde se debe escribir la especificación completa de la instancia de SQL Managed Instance. Si se omite, la especificación se escribe en la salida estándar.
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
## <a name="azdata-arc-sql-mi-list"></a>azdata arc sql mi list
Enumera instancias de SQL Managed Instance.
```bash
azdata arc sql mi list 
```
### <a name="examples"></a>Ejemplos
Enumera instancias de SQL Managed Instance.
```bash
azdata arc sql mi list
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

Para obtener más información sobre otros comandos de **azdata**, vea [Referencia de azdata](reference-azdata.md). 

Para obtener más información sobre cómo instalar la herramienta **azdata**, vea [Instalación de azdata](..\install\deploy-install-azdata.md).

