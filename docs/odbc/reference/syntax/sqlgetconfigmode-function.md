---
title: FUNción SQLGetConfigMode ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetConfigMode
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetConfigMode
helpviewer_keywords:
- SQLGetConfigMode function [ODBC]
ms.assetid: b96ab3b8-08d5-4fea-9ffe-e03043efbf2d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cc11bec24ede3352dd43f3645fb8c720b77fdabe
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285695"
---
# <a name="sqlgetconfigmode-function"></a>Función SQLGetConfigMode
**Conformidad**  
 Versión introducida: ODBC 3.0  
  
 **Resumen**  
 **SQLGetConfigMode** recupera el modo de configuración que indica dónde está la entrada Odbc.ini que enumera los valores DSN en la información del sistema.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
BOOL SQLGetConfigMode(  
     UWORD *   pwConfigMode);  
```  
  
## <a name="arguments"></a>Argumentos  
 *pwConfigMode*  
 [Salida] Puntero al búfer que contiene el modo de configuración. (Véase "Comentarios.") El valor de * \*pwConfigMode* puede ser:  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si se realiza correctamente, FALSE si se produce un error.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLGetConfigMode** devuelve FALSE, se puede obtener un valor * \*pfErrorCode* asociado llamando a **SQLInstallerError**. En la tabla * \** siguiente se enumeran los valores pfErrorCode que puede devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El instalador no pudo realizar la función debido a la falta de memoria.|  
  
## <a name="comments"></a>Comentarios  
 Esta función se utiliza para determinar dónde se encuentra la entrada Odbc.ini que enumera los valores DSN en la información del sistema. Si * \*pwConfigMode* es ODBC_USER_DSN, el DSN es un DSN de usuario y la función lee de la entrada Odbc.ini en HKEY_CURRENT_USER. Si se ODBC_SYSTEM_DSN, el DSN es un DSN del sistema y la función lee de la entrada Odbc.ini en HKEY_LOCAL_MACHINE. Si se ODBC_BOTH_DSN, se intenta HKEY_CURRENT_USER y, si se produce un error, se utiliza HKEY_LOCAL_MACHINE.  
  
 De forma predeterminada, **SQLGetConfigMode** devuelve ODBC_BOTH_DSN. Cuando un DSN de usuario o un DSN de sistema se crea mediante una llamada a **SQLConfigDataSource**, la función establece el modo de configuración en ODBC_USER_DSN o ODBC_SYSTEM_DSN para distinguir los DSN de usuario y del sistema mientras se modifica un DSN. Antes de devolver, **SQLConfigDataSource** restablece el modo de configuración a ODBC_BOTH_DSN.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Establecimiento del modo de configuración|[SQLSetConfigMode](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)|
