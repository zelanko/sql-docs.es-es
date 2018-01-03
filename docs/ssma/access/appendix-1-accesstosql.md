---
title: "Apéndice - 1 (AccessToSQL) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-access
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 00665e16-2990-4bfc-8e17-d97ca9fb4999
caps.latest.revision: "9"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c259d2d1328902869a61a04bea401cb8d381ae2f
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="appendix---1-accesstosql"></a>Apéndice - 1 (AccessToSQL)
Vista rápida de las opciones de línea de comandos de consola SSMA:  
  
|SL. No.|Switch|¿Requerido?|Argumento de modificador|Valores permitidos|  
|-----------|----------|-------------|-------------------|--------------------|  
|1|-s/script|Sí|scriptfile|Nombre de archivo XML válido.<br /><br />Archivo de definición de la secuencia de comandos de consola.|  
|2|variable o - v|no|variablevaluefile|Nombre de archivo XML válido. Si se usan variables en el archivo de script, debe especificarse este archivo.|  
|3|-c/serverconnection|no|serverconnectionfile|Nombre de archivo XML válido. Este archivo contiene información de conexión de servidor.|  
|4|-x / xmloutput|no|xmloutputfile|Esta opción indica el resultado de la consola en el formato XML. Si no se especifica esta opción, el resultado predeterminado es texto sin formato.<br /><br />Si no se especifica xmloutputfile, se dirige la salida XML a STDOUT.<br /><br />Xmloutputfile es el nombre del archivo donde se escribe la salida de la consola en el formato XML.|  
|5|-l/registro|no|archivoDeRegistro|Nombre de archivo válido.|  
|6|-e/projectenvironment|no|projectenvironmentfolder|Nombre de carpeta válido que contiene los archivos del entorno de proyecto SSMA.|  
|7|-p/securepassword|no|-a/agregar {< server_id > [,... n] &#124; todos los} – c &#124; serverconnection < archivo de conexión de servidor > [-v &#124; variable < archivo de valores de variable >] [-o/sobrescribir]<br /><br />o Administrador de configuración de<br /><br />-a/agregar {< server_id > [,... n] &#124; todos los} – s &#124; el script < archivo de script > [-v &#124; variable < archivo de valores de variable >] [-o/sobrescribir]<br /><br />-r o quitar {< server_id > [,... n] &#124; todos los}<br /><br />-l/lista<br /><br />– e/exportación {< Id. de servidor > [,... n] &#124; todos los} < contraseña cifrada - archivo ><br /><br />– i / Importar {< Id. de servidor > [,... n] &#124; todos los} < cifrado de contraseña-archivo >|Si se especifica, esta opción no debe combinarse con otras opciones.<br /><br />Id. de servidor: proporciona un identificador único para un servidor {cadena}<br /><br />archivo de conexión de servidor: archivo de definición de servidor (serverconnectionfile o scriptfile).<br /><br />archivo de valores de variable: es un archivo de definición de variable y usar en el archivo de conexión de servidor.<br /><br />archivo del contraseña cifrada: es un archivo de contraseñas del servidor cifrado con una frase de contraseña especificada por el usuario.|  
|8|-?|no|No es aplicable|No es aplicable|  
  
## <a name="see-also"></a>Vea también  
[Ejecutar la consola SSMA (Access)](http://msdn.microsoft.com/en-us/aa1bf665-8dc0-4259-b36f-46ae67197a43)  
  
