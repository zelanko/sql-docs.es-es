---
title: Función SQLGetInstalledDrivers | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0ff675a184ea0804988972ef10e9a383cdd45230
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537223"
---
# <a name="sqlgetinstalleddrivers-function"></a>Función SQLGetInstalledDrivers
**Conformidad**  
 Versión de introducción: ODBC 1.0  
  
 **Resumen**  
 **SQLGetInstalledDrivers** lee la sección [ODBC Drivers] de la información del sistema y devuelve una lista de descripciones de los controladores instalados.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
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
 [Salida] Número total de bytes (sin incluir los bytes de terminación null) devuelven en *lpszBuf*. Si el número de bytes disponible para devolver es mayor o igual a *cbBufMax*, la lista de descripciones de controlador de *lpszBuf* se trunca a *cbBufMax* menos el carácter de terminación NULL. El *pcbBufOut* argumento puede ser un puntero nulo.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si es correcto, FALSE si se produce un error.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLGetInstalledDrivers** devuelve FALSE, un asociado  *\*pfErrorCode* valor puede obtenerse mediante una llamada a **SQLInstallerError**. La siguiente tabla se enumeran los  *\*pfErrorCode* valores que pueden devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error del instalador general|Se produjo un error para que se ha producido ningún error de instalación concreto.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Longitud de búfer no válido|El *lpszBuf* argumento era NULL o no es válido, o el *cbBufMax* argumento era menor o igual que 0.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|No se encuentra en el registro de componente|El programa de instalación no encontró la sección [ODBC Drivers] en el registro.|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El programa de instalación no pudo realizar la función debido a la falta de memoria.|  
  
## <a name="comments"></a>Comentarios  
 Descripción de cada controlador se termina con un byte nulo y se termina toda la lista con un byte nulo. (Es decir, dos bytes nulos marcan el final de la lista). Si el búfer asignado no es lo suficientemente grande como para contener toda la lista, la lista se trunca sin errores. Se devuelve un error si se pasa un puntero nulo como *lpszBuf*.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Devuelve la descripción de los controladores y atributos|[SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|
