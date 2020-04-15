---
title: Función SQLReadFileDSN ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3abda956ee7682c9ac49270e8bf69fb039641790
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303956"
---
# <a name="sqlreadfiledsn-function"></a>Función SQLReadFileDSN
**Conformidad**  
 Versión introducida: ODBC 3.0  
  
 **Resumen**  
 **SQLReadFileDSN** lee información de un DSN de archivo.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
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
 [Entrada] Puntero al búfer de datos que contiene el nombre del archivo .dsn. Una extensión .dsn se anexa a todos los nombres de archivo que aún no tienen una extensión .dsn. El valor * \*de lpszFileName* debe ser una cadena terminada en null.  
  
 *lpszAppName*  
 [Entrada] Puntero al búfer de datos que contiene el nombre de la aplicación. Esto es "ODBC" para la sección ODBC. El valor * \*de lpszAppName* debe ser una cadena terminada en null.  
  
 *lpszKeyName*  
 [Entrada] Puntero al búfer de datos que contiene el nombre de la clave que se va a leer. Consulte "Comentarios" para ver las palabras clave reservadas. El valor * \*de lpszAppName* debe ser una cadena terminada en null.  
  
 *lpszString*  
 [Salida] Puntero al búfer de datos que contiene la cadena asociada a la clave que se va a leer.  
  
 Si * \*lpszFileName* es un nombre de archivo .dsn válido, pero el argumento *lpszAppName* es un puntero nulo y el argumento *lpszKeyName* es un puntero nulo, * \*lpszString* contiene una lista de aplicaciones válidas. Si * \*lpszFileName* es un nombre de archivo .dsn válido y * \*lpszAppName* es un nombre de aplicación válido, pero el argumento *lpszKeyName* es un puntero nulo, * \*lpszString* contiene una lista de palabras clave reservadas válidas en la sección adecuada del archivo DSN, delimitada por punto y coma. Si * \*lpszFileName* es un nombre de archivo .dsn válido, pero * \*lpszAppName* es un puntero nulo y el argumento *lpszKeyName* es un puntero nulo, * \*lpszString* contiene una lista de las secciones del archivo DSN, delimitada por punto y coma.  
  
 *cbString*  
 [Entrada] Longitud del * \*búfer lpszString.*  
  
 *pcbString*  
 [Salida] Número total de bytes disponibles para devolver en * \*lpszString*. Si el número de bytes disponibles para devolver es mayor o igual que *cbString*, la cadena de salida de * \*lpszString* se trunca en *cbString* menos el carácter de terminación nula. El *argumento pcbString* puede ser un puntero nulo.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si se realiza correctamente, FALSE si se produce un error.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLReadFileDSN** devuelve FALSE, se puede obtener un valor * \*pfErrorCode* asociado llamando a **SQLInstallerError**. En la tabla * \** siguiente se enumeran los valores pfErrorCode que puede devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error general del instalador|Se ha producido un error para el que no se ha producido ningún error específico del instalador.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Longitud de búfer no válida|El argumento *lpszString* era NULL.<br /><br /> El *argumento cbString* era menor o igual que 0.|  
|ODBC_ERROR_INVALID_PATH|Ruta de instalación no válida|La ruta de acceso del nombre de archivo especificado en el argumento *lpszFileName* no era válida.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitud no válido|El argumento *lpszAppName* era NULL, mientras que el argumento *lpszKeyName* era válido.|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El instalador no pudo realizar la función debido a la falta de memoria.|  
|ODBC_ERROR_OUTPUT_STRING_TRUNCATED|Cadena de salida truncada|La cadena devuelta en * \*lpszString* se truncó porque el valor de *cbString* era menor o igual que el valor de * \*pcbString*.|  
|ODBC_ERROR_REQUEST_FAILED|Error en la solicitud|La palabra clave no existía en el archivo DSN.|  
  
## <a name="comments"></a>Comentarios  
 ODBC se reserva el nombre de sección [ODBC] en el que se almacenará la información de conexión. Las palabras clave reservadas para esta sección son las mismas que las reservadas para una cadena de conexión en **SQLDriverConnect**. (Para obtener más información, consulte la descripción de la función [SQLDriverConnect.)](../../../odbc/reference/syntax/sqldriverconnect-function.md)  
  
 Las aplicaciones pueden utilizar estas palabras clave reservadas para leer la información en un DSN de archivo. Si una aplicación desea averiguar la cadena de conexión sin DSN asociada a un DSN de archivo, puede llamar a **SQLReadFileDSN** para cualquiera de las palabras clave de cadena de conexión reservadas en la sección [ODBC]. La cadena de conexión completa que se pasa en una conexión sin DSN es una combinación de todas las palabras clave (reservadas y específicas del controlador) en la sección [ODBC].  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Escribir información en un Archivo DSN|[SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)|
