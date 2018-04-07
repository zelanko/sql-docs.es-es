---
title: Apéndice - 1 (DB2ToSQL) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-db2
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: c6a30367-d56f-4fcc-8920-c6a6b0335a67
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2e06f1f7e7152bb65f6c6625c87ad3fdb7542ac7
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="appendix---1-db2tosql"></a>Apéndice - 1 (DB2ToSQL)
Vista rápida de las opciones de línea de comandos de consola SSMA:  
  
|Sl. No.|Switch|¿Requerido?|Argumento de modificador|Valores permitidos|  
|-----------|----------|-------------|-------------------|--------------------|  
|1|-s/script|Sí|scriptfile|Nombre de archivo XML válido.<br /><br />Archivo de definición de la secuencia de comandos de consola.|  
|2|variable o - v|no|variablevaluefile|Nombre de archivo XML válido.<br /><br />Si se usan variables en el archivo de script, debe especificarse este archivo.|  
|3|-c/serverconnection|no|serverconnectionfile|Nombre de archivo XML válido.<br /><br />Este archivo contiene información de conexión de servidor.|  
|4|-x/xmloutput|no|xmloutputfile|Esta opción indica el resultado de la consola en el formato XML. Si no se especifica esta opción, el resultado predeterminado es texto sin formato.<br /><br />Si no se especifica xmloutputfile, se dirige la salida XML a STDOUT.<br /><br />Xmloutputfile es el nombre del archivo donde se escribe la salida de la consola en el formato XML.|  
|5|-l/registro|no|archivoDeRegistro|Nombre de archivo válido.|  
|6|-e/projectenvironment|no|projectenvironmentfolder|Nombre de carpeta válido que contiene los archivos del entorno de proyecto SSMA.|  
|7|-p/securepassword|no|-a/agregar {< server_id > [,... n] &#124; todos} – c&#124;serverconnection < archivo de conexión de servidor > [-v&#124;variable < archivo de valores de variable >] [-o/sobrescribir]<br /><br />o bien<br /><br />-a/agregar {< server_id > [,... n] &#124; todos} – s&#124;script < archivo de script > [-v&#124;variable < archivo de valores de variable >] [-o/sobrescribir]<br /><br />-r o quitar {< server_id > [,... n] &#124; todos}<br /><br />-l/lista<br /><br />– e/exportación {< Id. de servidor > [,... n] &#124; todos} < contraseña cifrada - archivo ><br /><br />–i/import {<server-id> [, …n] &#124; all} <encrypted-password-file>|Si se especifica, esta opción no debe combinarse con otras opciones.<br /><br />Id. de servidor: proporciona un identificador único para un servidor {cadena}<br /><br />archivo de conexión de servidor: archivo de definición de servidor (serverconnectionfile o scriptfile).<br /><br />archivo de valores de variable: es un archivo de definición de variable y usar en el archivo de conexión de servidor.<br /><br />archivo del contraseña cifrada: es un archivo de contraseñas del servidor cifrado con una frase de contraseña especificada por el usuario.|  
|8|-?|no|No es aplicable|No es aplicable|  
  
## <a name="see-also"></a>Vea también  
[Ejecución de la consola de SSMA](http://msdn.microsoft.com/en-us/ce63f633-067d-4f04-b8e9-e1abd7ec740b)  
  
