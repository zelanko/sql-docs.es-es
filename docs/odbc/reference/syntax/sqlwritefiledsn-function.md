---
title: Función SQLWriteFileDSN | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 973c27fb58411e0fd3ddc482a0a8cbee3d929ee8
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="sqlwritefiledsn-function"></a>SQLWriteFileDSN (función)
**Conformidad**  
 Versión introdujo: ODBC 3.0  
  
 **Resumen**  
 **SQLWriteFileDSN** escribe información en un DSN de archivo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
BOOL SQLWriteFileDSN(  
     LPCSTR     lpszFileName,  
     LPCSTR     lpszAppName,  
     LPCSTR     lpszKeyName,  
     LPCSTR     lpszString);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszFileName*  
 [Entrada] Puntero al nombre del DSN de archivo. Se anexa una extensión DSN a todos los nombres de archivo que aún no tiene una extensión DSN.  
  
 *lpszAppName*  
 [Entrada] Puntero al nombre de la aplicación. Esto es "ODBC" de la sección ODBC.  
  
 *lpszKeyName*  
 [Entrada] Puntero al nombre de la clave que se va a leer. Palabras clave reservadas, vea "Comentarios".  
  
 *lpszString*  
 [Salida] Que señala la cadena asociada a la clave que se va a escribir. La longitud máxima de la cadena que apunta este argumento es de 32.767 bytes.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si se realiza correctamente, FALSE si se produce un error.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLWriteFileDSN** devuelve FALSE, un asociado  *\*pfErrorCode* valor puede obtenerse mediante una llamada a **SQLInstallerError**. La siguiente tabla se recogen los  *\*pfErrorCode* valores que pueden ser devueltos por **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error del instalador general|Se produjo un error para que no se produjo ningún error de instalación concreto.|  
|ODBC_ERROR_INVALID_PATH|Ruta de acceso de instalación no válida|La ruta de acceso del nombre de archivo especificado en el *lpszFileName* argumento no era válido.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitud no válido|El *lpszAppName*, *lpszKeyName*, o *lpszString* argumento era nulo.|  
  
## <a name="comments"></a>Comentarios  
 ODBC reserva el nombre de la sección [ODBC] en el que se va a almacenar la información de conexión. Las palabras clave reservadas de esta sección son los mismos que los reservados para una cadena de conexión en **SQLDriverConnect**. (Para obtener más información, consulte el [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) descripción de la función.)  
  
 Aplicaciones pueden utilizar estas palabras clave reservadas para escribir información directamente en un DSN de archivo. Si una aplicación desea crear o modificar la cadena de conexión sin DSN asociada con un DSN de archivo, puede llamar a **SQLWriteFileDSN** para cualquiera de las palabras clave de cadena de conexión reservado en la sección [ODBC].  
  
 Si el *lpszString* argumento es un puntero nulo, la palabra clave que apunta el *lpszKeyName* argumento se eliminará del archivo de DSN. Si el *lpszString* y *lpszKeyName* argumentos son ambos punteros nulos, la sección que señala el *lpszAppName* argumento se eliminará del archivo de DSN.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Leer la información de DSN de archivo|[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)|
