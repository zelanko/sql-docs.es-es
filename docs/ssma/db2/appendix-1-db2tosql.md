---
title: Apéndice - 1 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: c6a30367-d56f-4fcc-8920-c6a6b0335a67
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: ee92addc2d77c8393c3378762618504344b8d477
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52521150"
---
# <a name="appendix---1-db2tosql"></a>Apéndice - 1 (DB2ToSQL)
Vista rápida de las opciones de línea de comandos de la consola SSMA:  
  
|SL. No.|Modificador|¿Requerido?|Argumento de modificador|Valores permitidos|  
|-----------|----------|-------------|-------------------|--------------------|  
|1|-s o secuencia de comandos|Sí|scriptfile|Nombre de archivo XML válido.<br /><br />Archivo de definición de la secuencia de comandos de consola.|  
|2|-v o variable|No|variablevaluefile|Nombre de archivo XML válido.<br /><br />Si se utilizan variables en el archivo de script, debe especificarse este archivo.|  
|3|-c/serverconnection|No|serverconnectionfile|Nombre de archivo XML válido.<br /><br />Este archivo contiene información de conexión de servidor.|  
|4|-x / xmloutput|No|xmloutputfile|Esta opción indica el resultado de la consola en formato XML. Si no se especifica esta opción, el resultado predeterminado es texto sin formato.<br /><br />Si no se especifica xmloutputfile, se dirige la salida XML a STDOUT.<br /><br />Xmloutputfile es el nombre del archivo donde se escribe la salida de consola en formato XML.|  
|5|-l/log|No|archivoDeRegistro|Nombre de archivo válido.|  
|6|-e/projectenvironment|No|projectenvironmentfolder|Nombre de carpeta válido que contiene los archivos del entorno de proyecto SSMA.|  
|7|-p/securepassword|No|-a/agregar {< server_id > [,... n] &#124; todas} - c&#124;serverconnection < archivo de conexión de servidor > [-v&#124;variable < variable-valor-file >] [-o/sobrescribir]<br /><br />o Administrador de configuración de<br /><br />-a/agregar {< server_id > [,... n] &#124; todas} -s&#124;script < archivo de script > [-v&#124;variable < archivo de valores de variable >] [-o/sobrescribir]<br /><br />-r o quitar {< server_id > [,... n] &#124; todas}<br /><br />-l/list<br /><br />-e/export {< Id. de servidor > [,... n] &#124; todas} < contraseña cifrada - archivo ><br /><br />-i / Importar {< Id. de servidor > [,... n] &#124; todas} < cifrado de contraseña de archivo >|Si se especifica, esta opción no debe combinarse con otras opciones.<br /><br />Id. de servidor: Un identificador único que se proporciona para un servidor de {cadena}<br /><br />archivo de conexión de servidor: archivo de definición de servidor (serverconnectionfile o scriptfile).<br /><br />variable de archivo valores: Es un archivo de definición de variable y usar en el archivo de conexión de servidor.<br /><br />contraseña-archivo cifrado: Es un archivo de las contraseñas de servidor cifrado mediante una frase de contraseña especificado por el usuario.|  
|8|-?|No|No aplicable|No aplicable|  
  
## <a name="see-also"></a>Vea también  
[Ejecución de la consola de SSMA](https://msdn.microsoft.com/ce63f633-067d-4f04-b8e9-e1abd7ec740b)  
  
