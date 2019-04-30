---
title: Función SQLValidDSN | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fb490b475c5795125d11915729693eb630934eb8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63233486"
---
# <a name="sqlvaliddsn-function"></a>Función SQLValidDSN
**Conformidad**  
 Versión de introducción: ODBC 2.0  
  
 **Resumen**  
 **SQLValidDSN** comprueba la longitud y la validez del nombre del origen de datos antes de que el nombre se agrega a la información del sistema.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
BOOL SQLValidDSN(  
     LPCSTR    lpszDSN);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszDSN*  
 [Entrada] Origen de datos nombre se va a comprobar.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si el nombre del origen de datos es válido. Devuelve FALSE si el nombre del origen de datos no es válido o no la llamada de función.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLValidDSN** devuelve FALSE, un asociado  *\*pfErrorCode* valor puede obtenerse mediante una llamada a **SQLInstallerError**. Un  *\*pfErrorCode* si se devuelve solo si la llamada de función no se pudo, no se devuelve FALSE porque el nombre del origen de datos no es válido. La siguiente tabla se enumeran los  *\*pfErrorCode* valores que pueden devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error del instalador general|Se produjo un error para que se ha producido ningún error de instalación concreto.|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El programa de instalación no pudo realizar la función debido a la falta de memoria.|  
  
## <a name="comments"></a>Comentarios  
 **SQLValidDSN** llama a un controlador [ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) para comprobar la longitud del nombre del origen de datos y la validez de los caracteres individuales en el nombre del origen de datos. Comprueba si la longitud del nombre es mayor que SQL_MAX_DSN_LENGTH, tal como se define en Sqlext.h. (También se comprueba la longitud del nombre del origen de datos por [SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md).) **SQLValidDSN** comprueba si cualquiera de los siguientes caracteres no válidos se incluyen en el nombre del origen de datos:  
  
 [ ] { } ( ) , ; ? * = ! \@ \  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Agregar, modificar o quitar un origen de datos|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) (en el archivo DLL de configuración)|  
|Agregar, modificar o quitar un origen de datos|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|Escribir un nombre de origen de datos en la información del sistema|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
