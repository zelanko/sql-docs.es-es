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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 54c8dbed5599952778ca7651acbdb55a21b8f876
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63259290"
---
# <a name="sqlgetconfigmode-function"></a>Función SQLGetConfigMode
**Conformidad**  
 Versión de introducción: ODBC 3.0  
  
 **Resumen**  
 **SQLGetConfigMode** recupera el modo de configuración que indica que la entrada del archivo Odbc.ini enumerar valores DSN de la información del sistema.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
BOOL SQLGetConfigMode(  
     UWORD *   pwConfigMode);  
```  
  
## <a name="arguments"></a>Argumentos  
 *pwConfigMode*  
 [Salida] Puntero al búfer que contiene el modo de configuración. (Vea "Comentarios".) El valor de  *\*pwConfigMode* puede ser:  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si es correcto, FALSE si se produce un error.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLGetConfigMode** devuelve FALSE, un asociado  *\*pfErrorCode* valor puede obtenerse mediante una llamada a **SQLInstallerError**. La siguiente tabla se enumeran los  *\*pfErrorCode* valores que pueden devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El programa de instalación no pudo realizar la función debido a la falta de memoria.|  
  
## <a name="comments"></a>Comentarios  
 Esta función se utiliza para determinar dónde está la entrada del archivo Odbc.ini enumerar valores DSN en la información del sistema. Si  *\*pwConfigMode* es ODBC_USER_DSN, el DSN es un DSN de usuario y la función lee la entrada del archivo Odbc.ini en HKEY_CURRENT_USER. Si es ODBC_SYSTEM_DSN, el DSN es un DSN de sistema y la función lee la entrada del archivo Odbc.ini en HKEY_LOCAL_MACHINE. Si es ODBC_BOTH_DSN, se ha intentado HKEY_CURRENT_USER y, si se produce un error, se usa HKEY_LOCAL_MACHINE.  
  
 De forma predeterminada, **SQLGetConfigMode** devuelve ODBC_BOTH_DSN. Cuando se crea un DSN de usuario o un DSN de sistema mediante una llamada a **SQLConfigDataSource**, la función establece el modo de configuración a ODBC_USER_DSN o ODBC_SYSTEM_DSN para distinguir los DSN del sistema y usuario al modificar un DSN. Antes de devolver, **SQLConfigDataSource** ODBC_BOTH_DSN restablece el modo de configuración.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Establecer el modo de configuración|[SQLSetConfigMode](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)|
