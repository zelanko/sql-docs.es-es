---
title: Función SQLSetConfigMode ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetConfigMode
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetConfigMode
helpviewer_keywords:
- SQLSetConfigMode function [ODBC]
ms.assetid: 09eb88ea-b6f6-4eca-b19d-0951cebc6c0a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c36da48fa1493f61131d23a07f7a820b67ebac82
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81293285"
---
# <a name="sqlsetconfigmode-function"></a>Función SQLSetConfigMode
**Conformidad**  
 Versión introducida: ODBC 3.0  
  
 **Resumen**  
 **SQLSetConfigMode** establece el modo de configuración que indica dónde está la entrada Odbc.ini que enumera los valores DSN en la información del sistema.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
BOOL SQLSetConfigMode(  
     UWORD     wConfigMode);  
```  
  
## <a name="arguments"></a>Argumentos  
 *wConfigMode*  
 [Entrada] El modo de configuración del instalador (consulte "Comentarios"). El valor de *wConfigMode* puede ser:  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si se realiza correctamente, FALSE si se produce un error.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLSetConfigMode** devuelve FALSE, se puede obtener un valor * \*pfErrorCode* asociado llamando a **SQLInstallerError**. En la tabla * \** siguiente se enumeran los valores pfErrorCode que puede devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|Secuencia de parámetros no válida|El argumento *wConfigMode* no contenía ODBC_USER_DSN, ODBC_SYSTEM_DSN ni ODBC_BOTH_DSN.|  
  
## <a name="comments"></a>Comentarios  
 Esta función se utiliza para establecer dónde se encuentra la entrada Odbc.ini que enumera los valores DSN en la información del sistema. Si *wConfigMode* es ODBC_USER_DSN, el DSN es un DSN de usuario y la función lee de la entrada Odbc.ini en HKEY_CURRENT_USER. Si se ODBC_SYSTEM_DSN, el DSN es un DSN del sistema y la función lee de la entrada Odbc.ini en HKEY_LOCAL_MACHINE. Si se ODBC_BOTH_DSN, se intenta HKEY_CURRENT_USER y, si se produce un error, se utiliza HKEY_LOCAL_MACHINE.  
  
 Esta función no afecta a **SQLCreateDataSource** y **SQLDriverConnect**. El modo de configuración debe establecerse cuando un controlador lee del Registro llamando a **SQLGetPrivateProfileString** o escribe en el registro llamando a **SQLWritePrivateProfileString**. Las llamadas a **SQLGetPrivateProfileString** y **SQLWritePrivateProfileString** usan el modo de configuración para saber en qué parte del registro se va a operar.  
  
> [!CAUTION]  
>  **SQLSetConfigMode** debe llamarse sólo cuando sea necesario; si el modo se establece incorrectamente, es posible que el instalador ODBC no funcione correctamente.  
  
 **SQLSetConfigMode** realiza una modificación directa del registro del modo de configuración. Esto es distinto del proceso de modificación del modo de configuración mediante una llamada a **SQLConfigDataSource**. Una llamada a **SQLConfigDataSource** establece el modo de configuración para distinguir los DSN del usuario y del sistema al modificar un DSN. Antes de devolver, **SQLConfigDataSource** restablece el modo de configuración a BOTHDSN.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Creación de un origen de datos|[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|  
|Conexión a un origen de datos mediante una cadena de conexión o un cuadro de diálogo|[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Recuperar el modo de configuración|[SQLGetConfigMode](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)|
