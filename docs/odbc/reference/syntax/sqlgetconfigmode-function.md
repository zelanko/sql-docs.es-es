---
title: Función SQLGetConfigMode | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
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
- SQLGetConfigMode
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetConfigMode
helpviewer_keywords:
- SQLGetConfigMode function [ODBC]
ms.assetid: b96ab3b8-08d5-4fea-9ffe-e03043efbf2d
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c00416f664f8c4e6049b37ee8c408c7c7563a11f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sqlgetconfigmode-function"></a>SQLGetConfigMode (función)
**Conformidad**  
 Versión introdujo: ODBC 3.0  
  
 **Resumen**  
 **SQLGetConfigMode** recupera el modo de configuración que indica que la entrada de Odbc.ini enumerar valores DSN en la información del sistema.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
BOOL SQLGetConfigMode(  
     UWORD *   pwConfigMode);  
```  
  
## <a name="arguments"></a>Argumentos  
 *pwConfigMode*  
 [Salida] Puntero al búfer que contiene el modo de configuración. (Vea "Comentarios".) El valor de  *\*pwConfigMode* puede ser:  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si se realiza correctamente, FALSE si se produce un error.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLGetConfigMode** devuelve FALSE, un asociado  *\*pfErrorCode* valor puede obtenerse mediante una llamada a **SQLInstallerError**. La siguiente tabla se recogen los  *\*pfErrorCode* valores que pueden ser devueltos por **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El programa de instalación no pudo realizar la función debido a la falta de memoria.|  
  
## <a name="comments"></a>Comentarios  
 Esta función se utiliza para determinar dónde está la entrada de Odbc.ini enumerar valores DSN en la información del sistema. Si  *\*pwConfigMode* es ODBC_USER_DSN, el DSN es un DSN de usuario y la función lee de la entrada Odbc.ini en HKEY_CURRENT_USER. Si es ODBC_SYSTEM_DSN, el DSN es un DSN de sistema y la función lee de la entrada Odbc.ini en HKEY_LOCAL_MACHINE. Si es ODBC_BOTH_DSN, se prueba con HKEY_CURRENT_USER, y si se produce un error, se utiliza HKEY_LOCAL_MACHINE.  
  
 De forma predeterminada, **SQLGetConfigMode** devuelve ODBC_BOTH_DSN. Cuando se crea un DSN de usuario o un DSN de sistema mediante una llamada a **SQLConfigDataSource**, la función establece el modo de configuración para ODBC_USER_DSN o ODBC_SYSTEM_DSN para distinguir los DSN de sistema y de usuario al modificar un DSN. Antes de devolver, **SQLConfigDataSource** restablece el modo de configuración a ODBC_BOTH_DSN.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Establecer el modo de configuración|[SQLSetConfigMode](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)|
