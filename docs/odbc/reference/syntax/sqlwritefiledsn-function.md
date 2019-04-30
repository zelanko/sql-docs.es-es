---
title: Función SQLWriteFileDSN | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 73092fcd7091665f9a3dae969b7821cbf9777c9a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63284451"
---
# <a name="sqlwritefiledsn-function"></a>Función SQLWriteFileDSN
**Conformidad**  
 Versión de introducción: ODBC 3.0  
  
 **Resumen**  
 **SQLWriteFileDSN** escribe información en un DSN de archivo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
BOOL SQLWriteFileDSN(  
     LPCSTR     lpszFileName,  
     LPCSTR     lpszAppName,  
     LPCSTR     lpszKeyName,  
     LPCSTR     lpszString);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszFileName*  
 [Entrada] Puntero al nombre del DSN de archivo. Se anexa una extensión de DSN a todos los nombres de archivo que ya no tienen una extensión de DSN.  
  
 *lpszAppName*  
 [Entrada] Puntero al nombre de la aplicación. Esto es "ODBC" de la sección ODBC.  
  
 *lpszKeyName*  
 [Entrada] Puntero al nombre de la clave que se puede leer. Vea "Comentarios" para las palabras clave reservadas.  
  
 *lpszString*  
 [Salida] Señala a la cadena asociada a la clave que se va a escribir. La longitud máxima de la cadena señalada por este argumento es 32 767 bytes.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si es correcto, FALSE si se produce un error.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLWriteFileDSN** devuelve FALSE, un asociado  *\*pfErrorCode* valor puede obtenerse mediante una llamada a **SQLInstallerError**. La siguiente tabla se enumeran los  *\*pfErrorCode* valores que pueden devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error del instalador general|Se produjo un error para que se ha producido ningún error de instalación concreto.|  
|ODBC_ERROR_INVALID_PATH|Ruta de acceso de instalación no válido|La ruta de acceso del nombre de archivo especificado en el *lpszFileName* argumento no era válido.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitud no válido|El *lpszAppName*, *lpszKeyName*, o *lpszString* argumento era NULL.|  
  
## <a name="comments"></a>Comentarios  
 ODBC reserva el nombre de la sección [ODBC] en el que se va a almacenar la información de conexión. Las palabras clave reservadas de esta sección son los mismos que los reservados para una cadena de conexión en **SQLDriverConnect**. (Para obtener más información, consulte el [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) descripción de la función.)  
  
 Aplicaciones pueden utilizar estas palabras clave reservadas para escribir información directamente en un DSN de archivo. Si una aplicación desea crear o modificar la cadena de conexión sin DSN asociada con un DSN de archivo, puede llamar a **SQLWriteFileDSN** para cualquiera de las palabras clave de cadena de conexión reservado en la sección [ODBC].  
  
 Si el *lpszString* argumento es un puntero nulo, la palabra clave que apunta el *lpszKeyName* argumento se eliminarán del archivo DSN. Si el *lpszString* y *lpszKeyName* argumentos son ambos punteros nulos, la sección en la que apunta el *lpszAppName* argumento se eliminarán del archivo DSN.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Leer información de DSN de archivo|[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)|
