---
title: Referencia de azdata bdc hdfs
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para los comandos azdata bdc hdfs.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 8e892c2d501902ef915a297440ae5a6ffda83bce
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "68426185"
---
# <a name="azdata-bdc-hdfs"></a>azdata bdc hdfs

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En el siguiente artículo se proporciona una referencia sobre los comandos de **bdc hdfs** de la herramienta **azdata**. Para obtener más información sobre otros comandos de **azdata**, vea la [Referencia de azdata](reference-azdata.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[azdata bdc hdfs shell](#azdata-bdc-hdfs-shell) | El shell de HDFS es un sencillo shell de comandos interactivo para el sistema de archivos HDFS.
[azdata bdc hdfs ls](#azdata-bdc-hdfs-ls) | Muestre el estado del archivo o el directorio especificados.
[azdata bdc hdfs exists](#azdata-bdc-hdfs-exists) | Determine si un archivo o un directorio existen.  Devuelve true si existe; en caso contario, false.
[azdata bdc hdfs mkdir](#azdata-bdc-hdfs-mkdir) | Cree un directorio en la ruta de acceso especificada.
[azdata bdc hdfs mv](#azdata-bdc-hdfs-mv) | Mueva el archivo o la ruta de acceso especificados a la ubicación especificada.
[azdata bdc hdfs create](#azdata-bdc-hdfs-create) | Cree el archivo de texto en la ubicación especificada.  Se puede agregar contenido de texto simple mediante el parámetro data.
[azdata bdc hdfs cat](#azdata-bdc-hdfs-cat) | Lea el contenido de un archivo.  El desplazamiento y la longitud en bytes son parámetros opcionales.
[azdata bdc hdfs rm](#azdata-bdc-hdfs-rm) | Quite un archivo o directorio.
[azdata bdc hdfs rmr](#azdata-bdc-hdfs-rmr) | Quite un archivo o directorio de forma recursiva.
[azdata bdc hdfs chmod](#azdata-bdc-hdfs-chmod) | Cambie el permiso en el archivo o el directorio especificados.
[azdata bdc hdfs chown](#azdata-bdc-hdfs-chown) | Cambie el propietario o el grupo del archivo especificado.
[azdata bdc hdfs mount](reference-azdata-bdc-hdfs-mount.md) | Administre el montaje de almacenes remotos en HDFS.
## <a name="azdata-bdc-hdfs-shell"></a>azdata bdc hdfs shell
El shell de HDFS es un sencillo shell de comandos interactivo para el sistema de archivos HDFS.
```bash
azdata bdc hdfs shell 
```
### <a name="examples"></a>Ejemplos
Inicie el shell.
```bash
azdata bdc hdfs shell
```
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
## <a name="azdata-bdc-hdfs-ls"></a>azdata bdc hdfs ls
Muestre el estado del archivo o el directorio especificados.
```bash
azdata bdc hdfs ls --path -p 
                   
```
### <a name="examples"></a>Ejemplos
Mostrar el estado
```bash
azdata bdc hdfs ls --path '/tmp'
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--path -p`
Ruta de acceso para mostrar el estado.
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
## <a name="azdata-bdc-hdfs-exists"></a>azdata bdc hdfs exists
Determine si un archivo o un directorio existen.  Devuelve true si existe; en caso contario, false.
```bash
azdata bdc hdfs exists --path -p 
                       
```
### <a name="examples"></a>Ejemplos
Compruebe si existen archivos o directorios.
```bash
azdata bdc hdfs exists --path '/tmp'
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--path -p`
Ruta de acceso para comprobar si existen.
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
## <a name="azdata-bdc-hdfs-mkdir"></a>azdata bdc hdfs mkdir
Cree un directorio en la ruta de acceso especificada.
```bash
azdata bdc hdfs mkdir --path -p 
                      
```
### <a name="examples"></a>Ejemplos
Crear directorio.
```bash
azdata bdc hdfs mkdir --path '/tmp'
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--path -p`
Nombre del directorio que se va a crear.
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
## <a name="azdata-bdc-hdfs-mv"></a>azdata bdc hdfs mv
Mueva el archivo o la ruta de acceso especificados a la ubicación especificada.
```bash
azdata bdc hdfs mv --source-path -s 
                   --target-path -t
```
### <a name="examples"></a>Ejemplos
Mover el archivo o directorio.
```bash
azdata bdc hdfs mv --source-path '/tmp' --target-path '/dest'
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--source-path -s`
Directorio que se va a mover.
#### `--target-path -t`
Ubicación a la que se va a mover.
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
## <a name="azdata-bdc-hdfs-create"></a>azdata bdc hdfs create
Cree el archivo de texto en la ubicación especificada.  Se puede agregar contenido de texto simple mediante el parámetro data.
```bash
azdata bdc hdfs create --path -p 
                       --data -d
```
### <a name="examples"></a>Ejemplos
Crear archivo.
```bash
azdata bdc hdfs create --path '/tmp/test.txt' --data "This is a test."
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--path -p`
Nombre del archivo que se va a crear.
#### `--data -d`
Contenido del archivo.  Diseñado para contenido de texto simple.
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
## <a name="azdata-bdc-hdfs-cat"></a>azdata bdc hdfs cat
Lea el contenido de un archivo.  El desplazamiento y la longitud en bytes son parámetros opcionales.
```bash
azdata bdc hdfs cat --path -p 
                    --offset  
                    --length -l
```
### <a name="examples"></a>Ejemplos
Leer archivo.
```bash
azdata bdc hdfs cat --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--path -p`
Nombre del archivo que se va a leer.
#### `--offset`
Número de desplazamiento de bytes en el archivo que se va a leer.
#### `--length -l`
Longitud de los datos que se van a leer.
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
## <a name="azdata-bdc-hdfs-rm"></a>azdata bdc hdfs rm
Quite un archivo o directorio.
```bash
azdata bdc hdfs rm --path -p 
                   
```
### <a name="examples"></a>Ejemplos
Quite un archivo o directorio.
```bash
azdata bdc hdfs rm --path '/tmp'
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--path -p`
Nombre del archivo que se va a quitar.
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
## <a name="azdata-bdc-hdfs-rmr"></a>azdata bdc hdfs rmr
Quite un archivo o directorio de forma recursiva.
```bash
azdata bdc hdfs rmr --path -p 
                    
```
### <a name="examples"></a>Ejemplos
Quitar directorio recursivo.
```bash
azdata bdc hdfs rmr --path '/tmp'
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--path -p`
Nombre del archivo que se va a quitar de forma recursiva.
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
## <a name="azdata-bdc-hdfs-chmod"></a>azdata bdc hdfs chmod
Cambie el permiso en el archivo o el directorio especificados.
```bash
azdata bdc hdfs chmod --path -p 
                      --permission
```
### <a name="examples"></a>Ejemplos
Cambiar el permiso del archivo o directorio.
```bash
azdata bdc hdfs chmod --permission 775 --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--path -p`
Nombre del archivo o directorio en el que se van a establecer los permisos.
#### `--permission`
Octetos de permiso que se van a establecer.  Por ejemplo, "775".
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
## <a name="azdata-bdc-hdfs-chown"></a>azdata bdc hdfs chown
Cambie el propietario o el grupo del archivo especificado.
```bash
azdata bdc hdfs chown --path -p 
                      --owner  
                      --group -g
```
### <a name="examples"></a>Ejemplos
Cambiar el propietario y el grupo.
```bash
azdata bdc hdfs chown --owner hdfs --group superusergroup --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--path -p`
Nombre del archivo o directorio del que se va a cambiar el propietario.
#### `--owner`
Nombre del propietario que se va a establecer.
#### `--group -g`
Nombre del grupo que se va a establecer.
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

Para obtener más información sobre otros comandos de **azdata**, vea la [Referencia de azdata](reference-azdata.md). Para obtener más información sobre cómo instalar la herramienta **azdata**, vea [Instalación de azdata para administrar clústeres de macrodatos de SQL Server 2019](deploy-install-azdata.md).
