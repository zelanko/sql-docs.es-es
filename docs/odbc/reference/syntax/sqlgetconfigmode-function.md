---
title: Función SQLGetConfigMode | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81285695"
---
# <a name="sqlgetconfigmode-function"></a>Función SQLGetConfigMode
**Conformidad**  
 Versión introducida: ODBC 3,0  
  
 **Resumen**  
 **SQLGetConfigMode** recupera el modo de configuración que indica dónde se encuentra la entrada ODBC. ini que enumera los valores DSN en la información del sistema.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
BOOL SQLGetConfigMode(  
     UWORD *   pwConfigMode);  
```  
  
## <a name="arguments"></a>Argumentos  
 *pwConfigMode*  
 Genere Puntero al búfer que contiene el modo de configuración. (Vea "Comentarios"). El valor de * \*pwConfigMode* puede ser:  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si es correcto, FALSE si se produce un error.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLGetConfigMode** devuelve false, se puede obtener un valor de * \*pfErrorCode* asociado mediante una llamada a **SQLInstallerError**. En la tabla siguiente se * \** enumeran los valores de pfErrorCode que puede devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El instalador no pudo realizar la función debido a una falta de memoria.|  
  
## <a name="comments"></a>Comentarios  
 Esta función se usa para determinar dónde se encuentra la entrada de ODBC. ini que enumera los valores DSN en la información del sistema. Si * \*pwConfigMode* es ODBC_USER_DSN, el DSN es un DSN de usuario y la función Lee de la entrada ODBC. ini en HKEY_CURRENT_USER. Si se ODBC_SYSTEM_DSN, el DSN es un DSN del sistema y la función Lee de la entrada ODBC. ini en HKEY_LOCAL_MACHINE. Si se ODBC_BOTH_DSN, se intenta HKEY_CURRENT_USER y, si se produce un error, se usa HKEY_LOCAL_MACHINE.  
  
 De forma predeterminada, **SQLGetConfigMode** devuelve ODBC_BOTH_DSN. Cuando un DSN de usuario o un DSN de sistema se crean mediante una llamada a **SQLConfigDataSource**, la función establece el modo de configuración en ODBC_USER_DSN o ODBC_SYSTEM_DSN para distinguir los DSN de usuario y sistema al modificar un DSN. Antes de devolver, **SQLConfigDataSource** restablece el modo de configuración en ODBC_BOTH_DSN.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Establecimiento del modo de configuración|[SQLSetConfigMode](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)|
