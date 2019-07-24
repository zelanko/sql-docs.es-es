---
title: referencia HDFS de BDC de azdata
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para los comandos de azdata BDC HDFS.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 8e892c2d501902ef915a297440ae5a6ffda83bce
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426185"
---
# <a name="azdata-bdc-hdfs"></a>azdata BDC HDFS

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En el siguiente artículo se proporciona una referencia para los comandos **HDFS de BDC** en la herramienta **azdata** . Para obtener más información sobre otros comandos de **azdata** , consulte [referencia de azdata](reference-azdata.md).

## <a name="commands"></a>Comandos:
|     |     |
| --- | --- |
[Shell HDFS de BDC de azdata](#azdata-bdc-hdfs-shell) | El shell HDFS es un sencillo Shell de comandos interactivo para el sistema de archivos HDFS.
[azdata BDC HDFS LS](#azdata-bdc-hdfs-ls) | Muestra el estado del archivo o directorio especificado.
[azdata BDC HDFS existe](#azdata-bdc-hdfs-exists) | Determinar si existe un archivo o un directorio.  Devuelve true si existe y false en caso contrario.
[azdata BDC HDFS mkdir](#azdata-bdc-hdfs-mkdir) | Cree un directorio en la ruta de acceso especificada.
[azdata BDC HDFS MV](#azdata-bdc-hdfs-mv) | Mueve el archivo o la ruta de acceso especificados a la ubicación especificada.
[creación de HDFS de BDC de azdata](#azdata-bdc-hdfs-create) | Cree el archivo de texto en la ubicación especificada.  Se puede agregar contenido de texto simple mediante el parámetro de datos.
[CAT azdata BDC HDFS](#azdata-bdc-hdfs-cat) | Leer el contenido de un archivo.  El desplazamiento y la longitud en bytes son parámetros opcionales.
[RM de azdata BDC](#azdata-bdc-hdfs-rm) | Quite un archivo o un directorio.
[azdata BDC HDFS RMR](#azdata-bdc-hdfs-rmr) | Quitar un archivo o directorio de forma recursiva.
[azdata BDC HDFS](#azdata-bdc-hdfs-chmod) | Cambiar el permiso en el archivo o directorio especificado.
[azdata BDC HDFS chown](#azdata-bdc-hdfs-chown) | Cambiar el propietario o el grupo del archivo especificado.
[montaje de HDFS de BDC de azdata](reference-azdata-bdc-hdfs-mount.md) | Administrar el montaje de almacenes remotos en HDFS.
## <a name="azdata-bdc-hdfs-shell"></a>Shell HDFS de BDC de azdata
El shell HDFS es un sencillo Shell de comandos interactivo para el sistema de archivos HDFS.
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
Aumenta el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestra este mensaje de ayuda y sale.
#### `--output -o`
Formato de salida.  Valores permitidos: JSON, jsonc, Table y TSV.  Valor predeterminado: JSON.
#### `--query -q`
Cadena de consulta de JMESPath. Vea [http://jmespath.org/](http://jmespath.org/]) para obtener más información y ejemplos.
#### `--verbose`
Aumenta el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.
## <a name="azdata-bdc-hdfs-ls"></a>azdata BDC HDFS LS
Muestra el estado del archivo o directorio especificado.
```bash
azdata bdc hdfs ls --path -p 
                   
```
### <a name="examples"></a>Ejemplos
Mostrar estado
```bash
azdata bdc hdfs ls --path '/tmp'
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--path -p`
La ruta de acceso para mostrar el estado.
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
## <a name="azdata-bdc-hdfs-exists"></a>azdata BDC HDFS existe
Determinar si existe un archivo o un directorio.  Devuelve true si existe y false en caso contrario.
```bash
azdata bdc hdfs exists --path -p 
                       
```
### <a name="examples"></a>Ejemplos
Compruebe la existencia de archivos o directorios.
```bash
azdata bdc hdfs exists --path '/tmp'
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--path -p`
Ruta de acceso en la que se va a comprobar la existencia.
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
## <a name="azdata-bdc-hdfs-mkdir"></a>azdata BDC HDFS mkdir
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
Aumenta el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestra este mensaje de ayuda y sale.
#### `--output -o`
Formato de salida.  Valores permitidos: JSON, jsonc, Table y TSV.  Valor predeterminado: JSON.
#### `--query -q`
Cadena de consulta de JMESPath. Vea [http://jmespath.org/](http://jmespath.org/]) para obtener más información y ejemplos.
#### `--verbose`
Aumenta el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.
## <a name="azdata-bdc-hdfs-mv"></a>azdata BDC HDFS MV
Mueve el archivo o la ruta de acceso especificados a la ubicación especificada.
```bash
azdata bdc hdfs mv --source-path -s 
                   --target-path -t
```
### <a name="examples"></a>Ejemplos
Mueva el archivo o el directorio.
```bash
azdata bdc hdfs mv --source-path '/tmp' --target-path '/dest'
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--source-path -s`
Directorio que se va a quitar.
#### `--target-path -t`
Ubicación a la que se va a desplace.
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
## <a name="azdata-bdc-hdfs-create"></a>creación de HDFS de BDC de azdata
Cree el archivo de texto en la ubicación especificada.  Se puede agregar contenido de texto simple mediante el parámetro de datos.
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
Contenido del archivo.  Diseñado para el contenido de texto simple.
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
## <a name="azdata-bdc-hdfs-cat"></a>CAT azdata BDC HDFS
Leer el contenido de un archivo.  El desplazamiento y la longitud en bytes son parámetros opcionales.
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
Número de bytes de desplazamiento en el archivo que se va a leer.
#### `--length -l`
Longitud de los datos que se van a leer.
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
## <a name="azdata-bdc-hdfs-rm"></a>RM de azdata BDC
Quite un archivo o un directorio.
```bash
azdata bdc hdfs rm --path -p 
                   
```
### <a name="examples"></a>Ejemplos
Quite un archivo o un directorio.
```bash
azdata bdc hdfs rm --path '/tmp'
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
Formato de salida.  Valores permitidos: JSON, jsonc, Table y TSV.  Valor predeterminado: JSON.
#### `--query -q`
Cadena de consulta de JMESPath. Vea [http://jmespath.org/](http://jmespath.org/]) para obtener más información y ejemplos.
#### `--verbose`
Aumenta el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.
## <a name="azdata-bdc-hdfs-rmr"></a>azdata BDC HDFS RMR
Quitar un archivo o directorio de forma recursiva.
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
Aumenta el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestra este mensaje de ayuda y sale.
#### `--output -o`
Formato de salida.  Valores permitidos: JSON, jsonc, Table y TSV.  Valor predeterminado: JSON.
#### `--query -q`
Cadena de consulta de JMESPath. Vea [http://jmespath.org/](http://jmespath.org/]) para obtener más información y ejemplos.
#### `--verbose`
Aumenta el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.
## <a name="azdata-bdc-hdfs-chmod"></a>azdata BDC HDFS
Cambiar el permiso en el archivo o directorio especificado.
```bash
azdata bdc hdfs chmod --path -p 
                      --permission
```
### <a name="examples"></a>Ejemplos
Cambiar el permiso de archivo o directorio.
```bash
azdata bdc hdfs chmod --permission 775 --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--path -p`
Nombre del archivo o directorio en el que se van a establecer los permisos.
#### `--permission`
Octetos de permiso que se van a establecer.  Ejemplo "775".
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
## <a name="azdata-bdc-hdfs-chown"></a>azdata BDC HDFS chown
Cambiar el propietario o el grupo del archivo especificado.
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
Nombre del archivo o directorio para el que se va a cambiar el propietario.
#### `--owner`
Nombre del propietario que se va a establecer en.
#### `--group -g`
Nombre del grupo que se va a establecer en.
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
