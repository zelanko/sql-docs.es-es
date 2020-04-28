---
title: Apéndice-1 (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,Appendix
ms.assetid: 6dcfd6d5-772c-4876-aa94-a7f43c4b9d59
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 9d2d58b06c1a222a2ff6042bb5ca46338f752f7c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68083540"
---
# <a name="appendix---1-sybasetosql"></a>Apéndice - 1 (SybaseToSQL)
Vista rápida de las opciones de la línea de comandos de la consola de SSMA:  
  
|SL. No.|Modificador|¿Necesario?|Argumento de modificador|Valores permitidos|  
|-----------|----------|-------------|-------------------|--------------------|  
|1|-s/script|Sí|scriptfile|Nombre de archivo XML válido.<br /><br />Archivo de definición de script de consola.|  
|2|-v/variable|No|variablevaluefile|Nombre de archivo XML válido.<br /><br />Si se usan variables en el archivo de script, debe especificarse este archivo.|  
|3|-c/serverconnection|No|serverconnectionfile|Nombre de archivo XML válido.<br /><br />Este archivo contiene información de conexión de servidor.|  
|4|-x/xmloutput|No|xmloutputfile|Esta opción indica la salida de la consola en formato XML. Si no se especifica esta opción, la salida predeterminada está en formato de texto.<br /><br />Si no se especifica xmloutputfile, la salida XML se dirige a STDOUT.<br /><br />Xmloutputfile es el nombre del archivo en el que se escribe la salida de la consola en formato XML.|  
|5|-l/registro|No|archivoDeRegistro|Nombre de archivo válido.|  
|6|-e/projectenvironment|No|projectenvironmentfolder|Nombre de carpeta válido que contiene archivos de entorno de proyecto de SSMA.|  
|7|-p/securepassword|No|-a/agregar {<server_id> [,... n] &#124; todos}-c&#124;serverconnection <Server-connection-File> [-v&#124;variable <variable-Value-File>] [-o/overwrite]<br /><br />or<br /><br />-a/agregar {<server_id> [,... n] &#124; todos}-s&#124;script <archivo de script> [-v&#124;variable <variable-Value-File>] [-o/overwrite]<br /><br />-r/Remove {<server_id> [,... n] &#124; todos}<br /><br />-l/lista<br /><br />-e/Export {<Server-ID> [,... n] &#124; todos} <> de archivos de contraseña cifrada<br /><br />-i/Import {<Server-ID> [,... n] &#124; todos} <> de archivos de contraseña cifrada|Si se especifica, esta opción no se debe combinar con ninguna otra opción.<br /><br />Server-ID: un identificador único proporcionado para un servidor {String}<br /><br />servidor-conexión-archivo: archivo de definición del servidor (serverconnectionfile o scriptfile).<br /><br />variable-Value-File: es un archivo de definición de variable y se utiliza en Server-connection-File.<br /><br />cifrado de contraseña: es un archivo de contraseñas de servidor cifrado mediante una frase de contraseña especificada por el usuario.|  
|8|-?|No|No aplicable|No aplicable|  
  
## <a name="see-also"></a>Consulte también  
[Ejecutar la consola SSMA (Sybase)](https://msdn.microsoft.com/ea8950b7-fabc-4aa4-89f8-9573a2617d70)  
  
