---
title: Función SQLValidDSN | Documentos de Microsoft
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
- SQLValidDSN
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLValidDSN
helpviewer_keywords:
- SQLValidDSN [ODBC]
ms.assetid: 930d1d89-337a-4429-85a2-84ee10555ac9
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0c745b7ac285f09ff80478dab911b3cd3a9fc94d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="sqlvaliddsn-function"></a>SQLValidDSN (función)
**Conformidad**  
 Versión introdujo: ODBC 2.0  
  
 **Resumen**  
 **SQLValidDSN** comprueba la longitud y la validez del nombre del origen de datos antes de que el nombre se agrega a la información del sistema.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
BOOL SQLValidDSN(  
     LPCSTR    lpszDSN);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszDSN*  
 [Entrada] Nombre para que sea comprobado del origen de datos.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si el nombre de origen de datos es válido. Devuelve FALSE si el nombre de origen de datos no es válida o error de la llamada de función.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLValidDSN** devuelve FALSE, un asociado  *\*pfErrorCode* valor puede obtenerse mediante una llamada a **SQLInstallerError**. A  *\*pfErrorCode* si se devuelve solo si la llamada de función no se pudo, no se devuelve FALSE porque el nombre de origen de datos no es válido. La siguiente tabla se recogen los  *\*pfErrorCode* valores que pueden ser devueltos por **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error del instalador general|Se produjo un error para que no se produjo ningún error de instalación concreto.|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El programa de instalación no pudo realizar la función debido a la falta de memoria.|  
  
## <a name="comments"></a>Comentarios  
 **SQLValidDSN** llama a un controlador [ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) para comprobar la longitud del nombre del origen de datos y la validez de los caracteres individuales en el nombre del origen de datos. Comprueba si la longitud del nombre es mayor que SQL_MAX_DSN_LENGTH, tal como se define en Sqlext.h. (La longitud del nombre del origen de datos también se comprueba por [SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md).) **SQLValidDSN** comprueba si cualquiera de los siguientes caracteres no válidos se incluyen en el nombre del origen de datos:  
  
 [ ] { } ( ) , ; ? * = ! @ \  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Agregar, modificar o quitar un origen de datos|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) (en la configuración del archivo DLL)|  
|Agregar, modificar o quitar un origen de datos|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|Escribir un nombre de origen de datos en la información del sistema|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
