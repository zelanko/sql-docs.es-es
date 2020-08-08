---
title: Apéndice-1 (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: e01f8be5-ce68-4c9f-bd13-d65e73a16470
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: 17bc5783d70b4b2f7667b7c9cbf5cdf7d9fae030
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2020
ms.locfileid: "87935014"
---
# <a name="appendix---1-oracletosql"></a>Apéndice - 1 (OracleToSQL)
Vista rápida de las opciones de la línea de comandos de la consola de SSMA:  
  
|SL. No.|Modificador|¿Necesario?|Argumento de modificador|Valores permitidos|  
|-----------|----------|-------------|-------------------|--------------------|  
|1|-s/script|Sí|scriptfile|Nombre de archivo XML válido.<br /><br />Archivo de definición de script de consola.|  
|2|-v/variable|No|variablevaluefile|Nombre de archivo XML válido.<br /><br />Si se usan variables en el archivo de script, debe especificarse este archivo.|  
|3|-c/serverconnection|No|serverconnectionfile|Nombre de archivo XML válido.<br /><br />Este archivo contiene información de conexión de servidor.|  
|4|-x/xmloutput|No|xmloutputfile|Esta opción indica la salida de la consola en formato XML. Si no se especifica esta opción, la salida predeterminada está en formato de texto.<br /><br />Si no se especifica xmloutputfile, la salida XML se dirige a `STDOUT` .<br /><br />Xmloutputfile es el nombre del archivo en el que se escribe la salida de la consola en formato XML.|  
|5|-l/registro|No|archivoDeRegistro|Nombre de archivo válido.|  
|6|-e/projectenvironment|No|projectenvironmentfolder|Nombre de carpeta válido que contiene archivos de entorno de proyecto de SSMA.|  
|7|-p/securepassword|No|-a/agregar {<server_id> [,... n] &#124; todos}-c&#124;serverconnection <Server-connection-File> [-v&#124;variable <variable-Value-File>] [-o/overwrite]<br /><br />o<br /><br />-a/agregar {<server_id> [,... n] &#124; todos}-s&#124;script <archivo de script> [-v&#124;variable <variable-Value-File>] [-o/overwrite]<br /><br />-r/Remove {<server_id> [,... n] &#124; todos}<br /><br />-l/lista<br /><br />-e/Export {<Server-ID> [,... n] &#124; todos} <> de archivos de contraseña cifrada<br /><br />-i/Import {<Server-ID> [,... n] &#124; todos} <> de archivos de contraseña cifrada|Si se especifica, esta opción no se debe combinar con ninguna otra opción.<br /><br />Server-ID: un identificador único proporcionado para un servidor {String}<br /><br />servidor-conexión-archivo: archivo de definición del servidor (serverconnectionfile o scriptfile).<br /><br />variable-Value-File: es un archivo de definición de variable y se utiliza en Server-connection-File.<br /><br />cifrado de contraseña: es un archivo de contraseñas de servidor cifrado mediante una frase de contraseña especificada por el usuario.|  
|8|-?|No|No es aplicable|No es aplicable|  
  
## <a name="see-also"></a>Consulte también  
[Ejecutar la consola SSMA (Oracle)](https://msdn.microsoft.com/7228ccba-c69f-4b4c-8664-01a2750183c5)  
  
