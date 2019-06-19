---
title: Función SQLSetConfigMode | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b40da961e3e659bf4cd3e3692b4674399bce47a6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537221"
---
# <a name="sqlsetconfigmode-function"></a>Función SQLSetConfigMode
**Conformidad**  
 Versión de introducción: ODBC 3.0  
  
 **Resumen**  
 **SQLSetConfigMode** establece el modo de configuración que indica que la entrada del archivo Odbc.ini enumerar valores DSN de la información del sistema.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
BOOL SQLSetConfigMode(  
     UWORD     wConfigMode);  
```  
  
## <a name="arguments"></a>Argumentos  
 *wConfigMode*  
 [Entrada] El modo de configuración del instalador (vea "Comentarios"). El valor de *wConfigMode* puede ser:  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si es correcto, FALSE si se produce un error.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLSetConfigMode** devuelve FALSE, un asociado  *\*pfErrorCode* valor puede obtenerse mediante una llamada a **SQLInstallerError**. La siguiente tabla se enumeran los  *\*pfErrorCode* valores que pueden devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|Secuencia de parámetros no válidos|El *wConfigMode* argumento no contenía ODBC_USER_DSN, ODBC_SYSTEM_DSN o ODBC_BOTH_DSN.|  
  
## <a name="comments"></a>Comentarios  
 Esta función se usa para establecer la entrada del archivo Odbc.ini enumerar valores DSN se encuentra en la información del sistema. Si *wConfigMode* es ODBC_USER_DSN, el DSN es un DSN de usuario y la función lee la entrada del archivo Odbc.ini en HKEY_CURRENT_USER. Si es ODBC_SYSTEM_DSN, el DSN es un DSN de sistema y la función lee la entrada del archivo Odbc.ini en HKEY_LOCAL_MACHINE. Si es ODBC_BOTH_DSN, se ha intentado HKEY_CURRENT_USER y, a continuación, si se produce un error, se utiliza HKEY_LOCAL_MACHINE.  
  
 Esta función no afecta a **SQLCreateDataSource** y **SQLDriverConnect**. El modo de configuración debe establecerse cuando un controlador que se lee desde el registro mediante una llamada a **SQLGetPrivateProfileString** o escribe en el registro mediante una llamada a **SQLWritePrivateProfileString**. Las llamadas a **SQLGetPrivateProfileString** y **SQLWritePrivateProfileString** utilizan el modo de configuración para saber qué parte del registro para operar en.  
  
> [!CAUTION]  
>  **SQLSetConfigMode** debe llamarse solo cuando sea necesario; si el modo está establecido incorrectamente, puede producir un error en el instalador de ODBC funcionar correctamente.  
  
 **SQLSetConfigMode** hace una modificación directa del registro del modo de configuración. Se trata aparte del proceso de modificar el modo de configuración mediante una llamada a **SQLConfigDataSource**. Una llamada a **SQLConfigDataSource** establece el modo de configuración para distinguir los DSN del sistema y usuario cuando se modifica un DSN. Antes de devolver, **SQLConfigDataSource** BOTHDSN restablece el modo de configuración.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Creación de un origen de datos|[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|  
|Conectarse a un origen de datos mediante un cuadro de diálogo o la cadena de conexión|[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Recuperar el modo de configuración|[SQLGetConfigMode](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)|
