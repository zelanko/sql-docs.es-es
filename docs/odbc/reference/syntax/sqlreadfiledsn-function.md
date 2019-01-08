---
title: Función SQLReadFileDSN | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLReadFileDSN
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLReadFileDSN
helpviewer_keywords:
- SQLReadFileDSN function [ODBC]
ms.assetid: ead464aa-cdc3-47dd-a0c0-997711205d31
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9a247b9916bd4b8bfe8704d7f374ef027043e2ae
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/11/2018
ms.locfileid: "53206594"
---
# <a name="sqlreadfiledsn-function"></a>Función SQLReadFileDSN
**Conformidad**  
 Versión de introducción: ODBC 3.0  
  
 **Resumen**  
 **SQLReadFileDSN** lee la información de un DSN de archivo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
BOOL SQLReadFileDSN(  
     LPCSTR   lpszFileName,  
     LPCSTR   lpszAppName,  
     LPCSTR   lpszKeyName,  
     LPSTR    lpszString,  
     WORD     cbString,  
     WORD *   pcbString);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszFileName*  
 [Entrada] Puntero al búfer de datos que contiene el nombre del archivo DSN. Se anexa una extensión .dsn a todos los nombres de archivo que ya no tienen una extensión .dsn. El valor de  *\*lpszFileName* debe ser una cadena terminada en null.  
  
 *lpszAppName*  
 [Entrada] Puntero al búfer de datos que contiene el nombre de la aplicación. Esto es "ODBC" de la sección ODBC. El valor de  *\*lpszAppName* debe ser una cadena terminada en null.  
  
 *lpszKeyName*  
 [Entrada] Puntero al búfer de datos que contiene el nombre de la clave que se puede leer. Vea "Comentarios" para las palabras clave reservadas. El valor de  *\*lpszAppName* debe ser una cadena terminada en null.  
  
 *lpszString*  
 [Salida] Puntero al búfer de datos que contiene la cadena asociada con la clave que se puede leer.  
  
 Si  *\*lpszFileName* es un nombre de archivo DSN válido, pero la *lpszAppName* argumento es un puntero nulo y la *lpszKeyName* argumento es un puntero nulo, a continuación,  *\*lpszString* contiene una lista de aplicaciones válidas. Si  *\*lpszFileName* es un nombre de archivo DSN válido y  *\*lpszAppName* es un nombre de aplicación válido, pero la *lpszKeyName* argumento es un valor null puntero, a continuación,  *\*lpszString* contiene una lista de palabras clave reservadas válidas en la sección correspondiente del archivo DSN, delimitado por punto y coma. Si  *\*lpszFileName* es un nombre de archivo DSN válido pero  *\*lpszAppName* es un puntero nulo y la *lpszKeyName* argumento es un puntero nulo, a continuación,  *\*lpszString* contiene una lista de las secciones en el archivo DSN, delimitados por punto y coma.  
  
 *cbString*  
 [Entrada] Longitud de la  *\*lpszString* búfer.  
  
 *pcbString*  
 [Salida] Número total de bytes disponible para devolver en  *\*lpszString*. Si el número de bytes disponible para devolver es mayor o igual a *cbString*, la cadena de salida en  *\*lpszString* se trunca a *cbString* menos el carácter de terminación null. El *pcbString* argumento puede ser un puntero nulo.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si es correcto, FALSE si se produce un error.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLReadFileDSN** devuelve FALSE, un asociado  *\*pfErrorCode* valor puede obtenerse mediante una llamada a **SQLInstallerError**. La siguiente tabla se enumeran los  *\*pfErrorCode* valores que pueden devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error del instalador general|Se produjo un error para que se ha producido ningún error de instalación concreto.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Longitud de búfer no válido|El *lpszString* argumento era NULL.<br /><br /> El *cbString* argumento era menor o igual que 0.|  
|ODBC_ERROR_INVALID_PATH|Ruta de acceso de instalación no válido|La ruta de acceso del nombre de archivo especificado en el *lpszFileName* argumento no era válido.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitud no válido|El *lpszAppName* argumento era NULL, mientras que el *lpszKeyName* argumento era válido.|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El programa de instalación no pudo realizar la función debido a la falta de memoria.|  
|ODBC_ERROR_OUTPUT_STRING_TRUNCATED|Cadena de resultado truncada|La cadena devuelta en  *\*lpszString* se ha truncado porque el valor de *cbString* era menor o igual al valor de  *\*pcbString*.|  
|ODBC_ERROR_REQUEST_FAILED|Error en la solicitud|La palabra clave no existía en el DSN de archivo.|  
  
## <a name="comments"></a>Comentarios  
 ODBC reserva el nombre de la sección [ODBC] en el que se va a almacenar la información de conexión. Las palabras clave reservadas de esta sección son los mismos que los reservados para una cadena de conexión en **SQLDriverConnect**. (Para obtener más información, consulte el [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) descripción de la función.)  
  
 Aplicaciones pueden utilizar estas palabras clave reservadas para leer la información en un DSN de archivo. Si desea implementar una aplicación averiguar la cadena de conexión sin DSN asociada con un DSN de archivo, puede llamar a **SQLReadFileDSN** para cualquiera de las palabras clave de cadena de conexión reservado en la sección [ODBC]. La cadena de conexión completa que se pasa una conexión sin DSN es una combinación de todas las palabras clave (y no reservados específicos del controlador) en la sección [ODBC].  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Escribir información en un DSN de archivo|[SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)|
