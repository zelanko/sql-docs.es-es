---
title: Función SQLRemoveDSNFromIni ( SQLRemoveDSNFromIni) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRemoveDSNFromIni
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveDSNFromIni
helpviewer_keywords:
- SQLRemoveDSNFromIni function [ODBC]
ms.assetid: bb2e8273-7b61-4113-bfc8-f7ccc607c811
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 848e82741954ab24941d5d519699292727ca25d6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301804"
---
# <a name="sqlremovedsnfromini-function"></a>Función SQLRemoveDSNFromIni
**Conformidad**  
 Versión introducida: ODBC 1.0  
  
 **Resumen**  
 **SQLRemoveDSNFromIni** quita un origen de datos de la información del sistema.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
BOOL SQLRemoveDSNFromIni(  
     LPCSTR   lpszDSN);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszDSN*  
 [Entrada] Nombre del origen de datos que se va a quitar.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si quita el origen de datos o el origen de datos no estaba en el archivo Odbc.ini. Devuelve FALSE si no puede quitar el origen de datos.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLRemoveDSNFromIni** devuelve FALSE, se puede obtener un valor * \*pfErrorCode* asociado llamando a **SQLInstallerError**. En la tabla * \** siguiente se enumeran los valores pfErrorCode que puede devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error general del instalador|Se ha producido un error para el que no se ha producido ningún error específico del instalador.|  
|ODBC_ERROR_INVALID_DSN|DSN no válido|El argumento *lpszDSN* no era válido.|  
|ODBC_ERROR_REQUEST_FAILED|Error en la solicitud|El instalador no pudo quitar la información DSN del registro.|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El instalador no pudo realizar la función debido a la falta de memoria.|  
  
## <a name="comments"></a>Comentarios  
 **SQLRemoveDSNFromIni** quita el nombre del origen de datos de la sección [Orígenes de datos ODBC] de la información del sistema. También elimina la sección de especificación del origen de datos de la información del sistema.  
  
 Esta función solo debe llamarse desde una biblioteca de configuración de controladores.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Agregar, modificar o quitar un origen de datos|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)|  
|Agregar, modificar o quitar un origen de datos|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|Eliminación del origen de datos predeterminado|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|  
|Adición de un nombre de origen de datos a la información del sistema|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
