---
title: Apéndice - 1 (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2d22766d-ff09-420d-ae7c-13b443e28bd0
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: aa858ed572260ffa89baa5dabf735e838cf1b083
ms.sourcegitcommit: 9f2edcdf958e6afce9a09fb2e572ae36dfe9edb0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/25/2018
ms.locfileid: "50099237"
---
# <a name="appendix---1-mysqltosql"></a>Apéndice - 1 (MySQLToSQL)
Vista rápida de las opciones de línea de comandos de la consola SSMA:  
  
|SL. No.|Switch|¿Requerido?|Argumento de modificador|Valores permitidos|  
|-----------|----------|-------------|-------------------|--------------------|  
|1|-s o secuencia de comandos|Sí|scriptfile|Nombre de archivo XML válido.<br /><br />Archivo de definición de la secuencia de comandos de consola.|  
|2|-v o variable|no|variablevaluefile|Nombre de archivo XML válido.<br /><br />Si se utilizan variables en el archivo de script, debe especificarse este archivo.|  
|3|-c/serverconnection|no|serverconnectionfile|Nombre de archivo XML válido.<br /><br />Este archivo contiene información de conexión de servidor.|  
|4|-x / xmloutput|no|xmloutputfile|Esta opción indica el resultado de la consola en formato XML. Si no se especifica esta opción, el resultado predeterminado es texto sin formato.<br /><br />Si no se especifica xmloutputfile, se dirige la salida XML a STDOUT.<br /><br />Xmloutputfile es el nombre del archivo donde se escribe la salida de consola en formato XML.|  
|5|-l/log|no|archivoDeRegistro|Nombre de archivo válido.|  
|6|-e/projectenvironment|no|projectenvironmentfolder|Nombre de carpeta válido que contiene los archivos del entorno de proyecto SSMA.|  
|7|-p/securepassword|no|-a/agregar {< server_id > [,... n] &#124; todas} – c&#124;serverconnection < archivo de conexión de servidor > [-v&#124;variable < variable-valor-file >] [-o/sobrescribir]<br /><br />o Administrador de configuración de<br /><br />-a/agregar {< server_id > [,... n] &#124; todas} – s&#124;script < archivo de script > [-v&#124;variable < archivo de valores de variable >] [-o/sobrescribir]<br /><br />– r o quitar {< server_id > [,... n] &#124; todas}<br /><br />-l/list<br /><br />– e/export {< Id. de servidor > [,... n] &#124; todas} < contraseña cifrada - archivo ><br /><br />– i / Importar {< Id. de servidor > [,... n] &#124; todas} < cifrado de contraseña de archivo >|Si se especifica, esta opción no debe combinarse con otras opciones.<br /><br />Id. de servidor: proporciona un identificador único para un servidor de {cadena}<br /><br />archivo de conexión de servidor: archivo de definición de servidor (serverconnectionfile o scriptfile).<br /><br />archivo de valores de variable: es un archivo de definición de variable y usar en el archivo de conexión de servidor.<br /><br />archivo del contraseña de cifrado: es un archivo de las contraseñas de servidor cifrado mediante una frase de contraseña especificado por el usuario.|  
|8|-?|no|No aplicable|No aplicable|  
  
## <a name="see-also"></a>Vea también  
[Ejecución de la consola SSMA (MySQL)](http://msdn.microsoft.com/e3e9f7e4-0619-4861-a202-3d5d39953b26)  
  
