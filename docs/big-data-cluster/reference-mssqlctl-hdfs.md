---
title: referencia de hdfs mssqlctl
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para los comandos de hdfs mssqlctl.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6a2044594065e6f98ed919ace2171279e6f72c25
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67957914"
---
# <a name="mssqlctl-hdfs"></a>mssqlctl hdfs

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

El siguiente artículo proporciona la referencia para la **hdfs** comandos en el **mssqlctl** herramienta. Para obtener más información acerca de otros **mssqlctl** comandos, consulte [mssqlctl referencia](reference-mssqlctl.md).

## <a name="commands"></a>Comandos:
|     |     |
| --- | --- |
[shell de hdfs mssqlctl](#mssqlctl-hdfs-shell) | El shell HDFS es un shell sencillo comando interactivo para el sistema de archivos HDFS.
[mssqlctl hdfs ls](#mssqlctl-hdfs-ls) | Enumera el estado del directorio o archivo especificado.
[hdfs mssqlctl existe](#mssqlctl-hdfs-exists) | Determinar si existe un archivo o directorio.  Devuelve True si existe y False en caso contrario.
[mssqlctl hdfs mkdir](#mssqlctl-hdfs-mkdir) | Cree un directorio en la ruta especificada.
[mssqlctl hdfs mv](#mssqlctl-hdfs-mv) | Mover el archivo especificado o la ruta de acceso a la ubicación especificada.
[mssqlctl hdfs create](#mssqlctl-hdfs-create) | Cree el archivo de texto en la ubicación especificada.  Contenido de texto simple se puede agregar a través del parámetro de datos.
[hdfs mssqlctl leer](#mssqlctl-hdfs-read) | Leer el contenido de un archivo.  Desplazamiento y longitud en bytes son parámetros opcionales.
[mssqlctl hdfs rm](#mssqlctl-hdfs-rm) | Quitar un archivo o directorio.
[mssqlctl hdfs rmr](#mssqlctl-hdfs-rmr) | Quitan de forma recursiva un archivo o directorio.
[mssqlctl hdfs chmod](#mssqlctl-hdfs-chmod) | Cambie el permiso en el archivo o directorio especificado.
[mssqlctl hdfs chown](#mssqlctl-hdfs-chown) | Cambiar el propietario o grupo del archivo especificado.
## <a name="mssqlctl-hdfs-shell"></a>shell de hdfs mssqlctl
El shell HDFS es un shell sencillo comando interactivo para el sistema de archivos HDFS.
```bash
mssqlctl hdfs shell 
```
### <a name="examples"></a>Ejemplos
Inicie el shell.
```bash
mssqlctl hdfs shell
```
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
## <a name="mssqlctl-hdfs-ls"></a>mssqlctl ls de hdfs
Enumera el estado del directorio o archivo especificado.
```bash
mssqlctl hdfs ls --path -p 
                 
```
### <a name="examples"></a>Ejemplos
Estado de la lista
```bash
mssqlctl hdfs ls --path '/tmp'
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--path -p`
La ruta de acceso al estado de la lista.
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
## <a name="mssqlctl-hdfs-exists"></a>hdfs mssqlctl existe
Determinar si existe un archivo o directorio.  Devuelve True si existe y False en caso contrario.
```bash
mssqlctl hdfs exists --path -p 
                     
```
### <a name="examples"></a>Ejemplos
Compruebe la existencia del archivo o directorio.
```bash
mssqlctl hdfs exists --path '/tmp'
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--path -p`
Ruta de acceso para comprobar la existencia.
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
## <a name="mssqlctl-hdfs-mkdir"></a>mssqlctl hdfs mkdir
Cree un directorio en la ruta especificada.
```bash
mssqlctl hdfs mkdir --path -p 
                    
```
### <a name="examples"></a>Ejemplos
Asegúrese de directorio.
```bash
mssqlctl hdfs mkdir --path '/tmp'
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--path -p`
Nombre del directorio que se va a crear.
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
## <a name="mssqlctl-hdfs-mv"></a>mssqlctl hdfs mv
Mover el archivo especificado o la ruta de acceso a la ubicación especificada.
```bash
mssqlctl hdfs mv --source-path -s 
                 --target-path -t
```
### <a name="examples"></a>Ejemplos
Mover archivo o directorio.
```bash
mssqlctl hdfs mv --source-path '/tmp' --target-path '/dest'
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--source-path -s`
El directorio que se va a mover.
#### `--target-path -t`
Para mover a la ubicación.
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
## <a name="mssqlctl-hdfs-create"></a>crear mssqlctl hdfs
Cree el archivo de texto en la ubicación especificada.  Contenido de texto simple se puede agregar a través del parámetro de datos.
```bash
mssqlctl hdfs create --path -p 
                     --data -d
```
### <a name="examples"></a>Ejemplos
Cree el archivo.
```bash
mssqlctl hdfs create --path '/tmp/test.txt' --data "This is a test."
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--path -p`
Nombre del archivo que se creará.
#### `--data -d`
Contenido del archivo.  Pensado para el contenido de texto simple.
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
## <a name="mssqlctl-hdfs-read"></a>hdfs mssqlctl leer
Leer el contenido de un archivo.  Desplazamiento y longitud en bytes son parámetros opcionales.
```bash
mssqlctl hdfs read --path -p 
                   --offset  
                   --length -l
```
### <a name="examples"></a>Ejemplos
Leer el archivo.
```bash
mssqlctl hdfs read --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--path -p`
Nombre del archivo que se va a leer.
#### `--offset`
Número de bytes de desplazamiento dentro del archivo para lectura.
#### `--length -l`
Longitud de los datos que se va a leer.
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
## <a name="mssqlctl-hdfs-rm"></a>mssqlctl hdfs rm
Quitar un archivo o directorio.
```bash
mssqlctl hdfs rm --path -p 
                 
```
### <a name="examples"></a>Ejemplos
Quitar un archivo o directorio.
```bash
mssqlctl hdfs rm --path '/tmp'
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--path -p`
Nombre del archivo que se va a quitar.
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
## <a name="mssqlctl-hdfs-rmr"></a>mssqlctl hdfs rmr
Quitan de forma recursiva un archivo o directorio.
```bash
mssqlctl hdfs rmr --path -p 
                  
```
### <a name="examples"></a>Ejemplos
Eliminar directorio de recursiva.
```bash
mssqlctl hdfs rmr --path '/tmp'
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--path -p`
Nombre del archivo que se va a quitar de forma recursiva.
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
## <a name="mssqlctl-hdfs-chmod"></a>mssqlctl hdfs chmod
Cambie el permiso en el archivo o directorio especificado.
```bash
mssqlctl hdfs chmod --path -p 
                    --permission
```
### <a name="examples"></a>Ejemplos
Cambiar los permisos de archivo o directorio.
```bash
mssqlctl hdfs chmod --permission 775 --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--path -p`
Nombre del archivo o directorio para establecer permisos en.
#### `--permission`
Octetos de permiso para establecer.  Ejemplo "775".
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
## <a name="mssqlctl-hdfs-chown"></a>mssqlctl hdfs chown
Cambiar el propietario o grupo del archivo especificado.
```bash
mssqlctl hdfs chown --path -p 
                    --owner  
                    --group -g
```
### <a name="examples"></a>Ejemplos
Cambiar el propietario y el grupo.
```bash
mssqlctl hdfs chown --owner hdfs --group superusergroup --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--path -p`
Nombre del archivo o directorio para cambiar el propietario del.
#### `--owner`
Para establecer en el nombre del propietario.
#### `--group -g`
Nombre de grupo para establecer en.
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

Para obtener más información sobre cómo instalar el **mssqlctl** herramienta, consulte [instalar mssqlctl para administrar clústeres de SQL Server 2019 macrodatos](deploy-install-mssqlctl.md).