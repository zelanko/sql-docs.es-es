---
title: Función SQLValidDSN ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6dfafca22d0b04f2147b1af24b53e787493efe67
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286975"
---
# <a name="sqlvaliddsn-function"></a>Función SQLValidDSN
**Conformidad**  
 Versión introducida: ODBC 2.0  
  
 **Resumen**  
 **SQLValidDSN** comprueba la longitud y validez del nombre del origen de datos antes de agregar el nombre a la información del sistema.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
BOOL SQLValidDSN(  
     LPCSTR    lpszDSN);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszDSN*  
 [Entrada] Nombre del origen de datos que se va a comprobar.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si el nombre del origen de datos es válido. Devuelve FALSE si el nombre del origen de datos no es válido o la llamada de función ha fallado.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLValidDSN** devuelve FALSE, se puede obtener un valor * \*pfErrorCode* asociado llamando a **SQLInstallerError**. Un * \*pfErrorCode* se devuelve sólo si se produjo un error en la llamada de función, no si FALSE se devolvió porque el nombre del origen de datos no es válido. En la tabla * \** siguiente se enumeran los valores pfErrorCode que puede devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error general del instalador|Se ha producido un error para el que no se ha producido ningún error específico del instalador.|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El instalador no pudo realizar la función debido a la falta de memoria.|  
  
## <a name="comments"></a>Comentarios  
 [El ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) de un controlador llama a **SQLValidDSN** para comprobar la longitud del nombre del origen de datos y la validez de los caracteres individuales en el nombre del origen de datos. Comprueba si la longitud del nombre es mayor que SQL_MAX_DSN_LENGTH, tal como se define en Sqlext.h. (LA longitud del nombre del origen de datos también se comprueba mediante [SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md).) **SQLValidDSN** comprueba si alguno de los siguientes caracteres no válidos se incluye en el nombre del origen de datos:  
  
 [ ] { } ( ) , ; ? * = ! \@ \  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Agregar, modificar o quitar un origen de datos|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) (en el archivo DLL de instalación)|  
|Agregar, modificar o quitar un origen de datos|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|Escribir un nombre de origen de datos en la información del sistema|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
