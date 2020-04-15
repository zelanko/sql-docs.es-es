---
title: FUNción SQLGetInstalledDrivers ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 24793473bf4f25253ac11673df852d10cfb2c558
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303332"
---
# <a name="sqlgetinstalleddrivers-function"></a>Función SQLGetInstalledDrivers
**Conformidad**  
 Versión introducida: ODBC 1.0  
  
 **Resumen**  
 **SQLGetInstalledDrivers** lee la sección [Controladores ODBC] de la información del sistema y devuelve una lista de descripciones de los controladores instalados.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
BOOL SQLGetInstalledDrivers(  
     LPSTR   lpszBuf,  
     WORD    cbBufMax,  
     WORD *  pcbBufOut);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszBuf*  
 [Salida] Lista de descripciones de los controladores instalados. Para obtener información sobre la estructura de la lista, consulte "Comentarios."  
  
 *cbBufMax*  
 [Entrada] Longitud de *lpszBuf*.  
  
 *pcbBufOut*  
 [Salida] Número total de bytes (excluyendo el byte de terminación nula) devueltos en *lpszBuf*. Si el número de bytes disponibles para devolver es mayor o igual que *cbBufMax*, la lista de descripciones de controladores en *lpszBuf* se trunca en *cbBufMax* menos el carácter de terminación nula. El *argumento pcbBufOut* puede ser un puntero nulo.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si se realiza correctamente, FALSE si se produce un error.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLGetInstalledDrivers** devuelve FALSE, se puede obtener un valor * \*pfErrorCode* asociado llamando a **SQLInstallerError**. En la tabla * \** siguiente se enumeran los valores pfErrorCode que puede devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error general del instalador|Se ha producido un error para el que no se ha producido ningún error específico del instalador.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Longitud de búfer no válida|El argumento *lpszBuf* era NULL o no válido, o el argumento *cbBufMax* era menor o igual que 0.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|Componente no encontrado en el registro|El instalador no pudo encontrar la sección [Controladores ODBC] en el registro.|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El instalador no pudo realizar la función debido a la falta de memoria.|  
  
## <a name="comments"></a>Comentarios  
 Cada descripción del controlador se termina con un byte nulo y toda la lista se termina con un byte nulo. (Es decir, dos bytes nulos marcan el final de la lista.) Si el búfer asignado no es lo suficientemente grande como para contener toda la lista, la lista se trunca sin errores. Se devuelve un error si se pasa un puntero nulo como *lpszBuf*.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Devolver las descripciones y atributos del controlador|[SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|
