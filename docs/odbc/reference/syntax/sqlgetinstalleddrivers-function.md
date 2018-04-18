---
title: Función SQLGetInstalledDrivers | Documentos de Microsoft
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
- SQLGetInstalledDrivers
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetInstalledDrivers
helpviewer_keywords:
- SQLGetInstalledDrivers function [ODBC]
ms.assetid: a1983a2e-0edf-422e-bd1b-ec5db40a34bc
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e8526c90a0fb6ec801b06ce415ff906b6b42c090
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sqlgetinstalleddrivers-function"></a>SQLGetInstalledDrivers (función)
**Conformidad**  
 Versión introdujo: ODBC 1.0  
  
 **Resumen**  
 **SQLGetInstalledDrivers** lee la sección [ODBC Drivers] de la información del sistema y devuelve una lista de descripciones de los controladores instalados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
BOOL SQLGetInstalledDrivers(  
     LPSTR   lpszBuf,  
     WORD    cbBufMax,  
     WORD *  pcbBufOut);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszBuf*  
 [Salida] Lista de descripciones de los controladores instalados. Para obtener información acerca de la estructura de lista, vea "Comentarios".  
  
 *cbBufMax*  
 [Entrada] Longitud de *lpszBuf*.  
  
 *pcbBufOut*  
 [Salida] Número total de bytes (excepto el byte de finalización en null) devuelven en *lpszBuf*. Si el número de bytes disponible para devolver es mayor o igual que *cbBufMax*, la lista de descripciones de controlador en *lpszBuf* se trunca a *cbBufMax* menos el carácter de terminación NULL. El *pcbBufOut* argumento puede ser un puntero nulo.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si se realiza correctamente, FALSE si se produce un error.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLGetInstalledDrivers** devuelve FALSE, un asociado  *\*pfErrorCode* valor puede obtenerse mediante una llamada a **SQLInstallerError**. La siguiente tabla se recogen los  *\*pfErrorCode* valores que pueden ser devueltos por **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error del instalador general|Se produjo un error para que no se produjo ningún error de instalación concreto.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Longitud de búfer no válido|El *lpszBuf* argumento era NULL o no es válido, o la *cbBufMax* argumento era menor o igual que 0.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|No se encuentra en el registro de componente|El instalador no pudo encontrar la sección [ODBC Drivers] en el registro.|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El programa de instalación no pudo realizar la función debido a la falta de memoria.|  
  
## <a name="comments"></a>Comentarios  
 Cada descripción del controlador se termina con un byte null, y toda la lista se termina con un byte nulo. (Es decir, dos bytes nulos marcan el final de la lista.) Si el búfer asignado no es lo suficientemente grande como para contener toda la lista, la lista se trunca sin errores. Se devuelve un error si se pasa un puntero nulo como *lpszBuf*.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Devuelve la descripción de los controladores y atributos|[SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|
