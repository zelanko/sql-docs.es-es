---
description: Función SQLRemoveDSNFromIni
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f49646881539d7c90c057633e7151b31cfe52b52
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499618"
---
# <a name="sqlremovedsnfromini-function"></a>Función SQLRemoveDSNFromIni
**Conformidad**  
 Versión introducida: ODBC 1,0  
  
 **Resumen**  
 **SQLRemoveDSNFromIni** quita un origen de datos de la información del sistema.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
BOOL SQLRemoveDSNFromIni(  
     LPCSTR   lpszDSN);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszDSN*  
 Entradas Nombre del origen de datos que se va a quitar.  
  
## <a name="returns"></a>Devoluciones  
 La función devuelve TRUE si quita el origen de datos o el origen de datos no estaba en el archivo de Odbc.ini. Devuelve FALSE si no puede quitar el origen de datos.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLRemoveDSNFromIni** devuelve false, se puede obtener un valor de * \* pfErrorCode* asociado mediante una llamada a **SQLInstallerError**. En la tabla siguiente se enumeran los valores de * \* pfErrorCode* que puede devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error general del instalador|Se produjo un error en el que no había ningún error específico del instalador.|  
|ODBC_ERROR_INVALID_DSN|DSN no válido|El argumento *lpszDSN* no era válido.|  
|ODBC_ERROR_REQUEST_FAILED|Error en la solicitud|El instalador no pudo quitar la información de DSN del registro.|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El instalador no pudo realizar la función debido a una falta de memoria.|  
  
## <a name="comments"></a>Comentarios  
 **SQLRemoveDSNFromIni** quita el nombre del origen de datos de la sección [orígenes de datos ODBC] de la información del sistema. También quita la sección especificación de origen de datos de la información del sistema.  
  
 Solo se debe llamar a esta función desde una biblioteca de instalación de controladores.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Agregar, modificar o quitar un origen de datos|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)|  
|Agregar, modificar o quitar un origen de datos|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|Quitar el origen de datos predeterminado|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|  
|Agregar un nombre de origen de datos a la información del sistema|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
