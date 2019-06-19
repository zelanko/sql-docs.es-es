---
title: Función SQLRemoveDSNFromIni | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 01ecb5457ce3fbc343541063047cb935cbf85a72
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537398"
---
# <a name="sqlremovedsnfromini-function"></a>Función SQLRemoveDSNFromIni
**Conformidad**  
 Versión de introducción: ODBC 1.0  
  
 **Resumen**  
 **SQLRemoveDSNFromIni** quita un origen de datos de la información del sistema.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
BOOL SQLRemoveDSNFromIni(  
     LPCSTR   lpszDSN);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszDSN*  
 [Entrada] Nombre del origen de datos para quitar.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si quita el origen de datos o el origen de datos no se encuentra en el archivo Odbc.ini. Devuelve FALSE si se produce un error al quitar el origen de datos.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLRemoveDSNFromIni** devuelve FALSE, un asociado  *\*pfErrorCode* valor puede obtenerse mediante una llamada a **SQLInstallerError**. La siguiente tabla se enumeran los  *\*pfErrorCode* valores que pueden devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error del instalador general|Se produjo un error para que se ha producido ningún error de instalación concreto.|  
|ODBC_ERROR_INVALID_DSN|DSN no válido|El *lpszDSN* argumento no era válido.|  
|ODBC_ERROR_REQUEST_FAILED|Error en la solicitud|El programa de instalación no pudo quitar la información DSN del registro.|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El programa de instalación no pudo realizar la función debido a la falta de memoria.|  
  
## <a name="comments"></a>Comentarios  
 **SQLRemoveDSNFromIni** quita el nombre del origen de datos de la sección [ODBC Data Sources] de la información del sistema. También se quita la sección de especificación del origen de datos de la información del sistema.  
  
 Esta función debe llamarse únicamente desde una biblioteca de programa de instalación de controladores.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Agregar, modificar o quitar un origen de datos|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)|  
|Agregar, modificar o quitar un origen de datos|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|Quitando el origen de datos predeterminado|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|  
|Agregar un nombre de origen de datos a la información del sistema|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
