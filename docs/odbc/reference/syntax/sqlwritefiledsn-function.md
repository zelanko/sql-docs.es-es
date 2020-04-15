---
title: Función SQLWriteFileDSN ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLWriteFileDSN
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLWriteFileDSN
helpviewer_keywords:
- SQLWriteFileDSN [ODBC]
ms.assetid: 9e18f56f-1061-416b-83d4-ffeec42ab5a9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e781f1be79e0079f33b3d0800c665f5f5e9fda4d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286895"
---
# <a name="sqlwritefiledsn-function"></a>Función SQLWriteFileDSN
**Conformidad**  
 Versión introducida: ODBC 3.0  
  
 **Resumen**  
 **SQLWriteFileDSN** escribe información en un DSN de archivo.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
BOOL SQLWriteFileDSN(  
     LPCSTR     lpszFileName,  
     LPCSTR     lpszAppName,  
     LPCSTR     lpszKeyName,  
     LPCSTR     lpszString);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszFileName*  
 [Entrada] Puntero al nombre del DSN de archivo. Una extensión DSN se anexa a todos los nombres de archivo que aún no tienen una extensión DSN.  
  
 *lpszAppName*  
 [Entrada] Puntero al nombre de la aplicación. Esto es "ODBC" para la sección ODBC.  
  
 *lpszKeyName*  
 [Entrada] Puntero al nombre de la clave que se va a leer. Consulte "Comentarios" para ver las palabras clave reservadas.  
  
 *lpszString*  
 [Salida] Señaló la cadena asociada a la clave que se va a escribir. La longitud máxima de la cadena señalada por este argumento es de 32.767 bytes.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si se realiza correctamente, FALSE si se produce un error.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLWriteFileDSN** devuelve FALSE, se puede obtener un valor * \*pfErrorCode* asociado llamando a **SQLInstallerError**. En la tabla * \** siguiente se enumeran los valores pfErrorCode que puede devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error general del instalador|Se ha producido un error para el que no se ha producido ningún error específico del instalador.|  
|ODBC_ERROR_INVALID_PATH|Ruta de instalación no válida|La ruta de acceso del nombre de archivo especificado en el argumento *lpszFileName* no era válida.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitud no válido|El argumento *lpszAppName*, *lpszKeyName*o *lpszString* era NULL.|  
  
## <a name="comments"></a>Comentarios  
 ODBC se reserva el nombre de sección [ODBC] en el que se almacenará la información de conexión. Las palabras clave reservadas para esta sección son las mismas que las reservadas para una cadena de conexión en **SQLDriverConnect**. (Para obtener más información, consulte la descripción de la función [SQLDriverConnect.)](../../../odbc/reference/syntax/sqldriverconnect-function.md)  
  
 Las aplicaciones pueden utilizar estas palabras clave reservadas para escribir información directamente en un DSN de archivo. Si una aplicación desea crear o modificar la cadena de conexión sin DSN asociada a un DSN de archivo, puede llamar a **SQLWriteFileDSN** para cualquiera de las palabras clave de cadena de conexión reservadas en la sección [ODBC].  
  
 Si el argumento *lpszString* es un puntero nulo, la palabra clave a la que apunta el argumento *lpszKeyName* se eliminará del archivo .dsn. Si los argumentos *lpszString* y *lpszKeyName* son punteros nulos, la sección a la que apunta el argumento *lpszAppName* se eliminará del archivo .dsn.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Lectura de información de DSN de archivos|[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)|
