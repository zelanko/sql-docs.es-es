---
title: FUNción SQLSetScrollOptions ( SQLSetScrollOptions) Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetScrollOptions
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLSetScrollOptions
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC]
ms.assetid: 2a825ba7-7942-4c23-bcdb-c80dc12f8c86
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 056fc203581e1d5d8323b09ac62d692093d8c0f5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287275"
---
# <a name="sqlsetscrolloptions-function"></a>Función SQLSetScrollOptions
**Conformidad**  
 Versión introducida: Cumplimiento de normas ODBC 1.0: en desuso  
  
 **Resumen**  
 En ODBC *3.x*, la función ODBC 2.0 **SQLSetScrollOptions** se ha reemplazado por llamadas a **SQLGetInfo** y **SQLSetStmtAttr**.  
  
> [!NOTE]
>  Para obtener más información acerca de lo que el Administrador de controladores asigna esta función cuando una aplicación ODBC *2.x* está trabajando con un controlador ODBC *3.x,* vea asignación de [funciones en desuso](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) en apéndice G: directrices de controlador para la compatibilidad con versiones anteriores.  
> 
> [!NOTE]
>  Cuando el Administrador de controladores asigna **SQLSetScrollOptions** para una aplicación que trabaja con un controlador ODBC *3.x* que no admite **SQLSetScrollOptions**, el Administrador de controladores establece la opción de instrucción SQL_ROWSET_SIZE, no el atributo de instrucción *SQL_ATTR_ROW_ARRAY_SIZE,* en el argumento RowsetSize de **SQLSetScrollOption**. Como resultado, **SQLSetScrollOptions** no se puede utilizar una aplicación al capturar varias filas mediante una llamada a **SQLFetch** o **SQLFetchScroll**. Solo se puede utilizar cuando se capturan varias filas mediante una llamada a **SQLExtendedFetch**.  
  
## <a name="remarks"></a>Observaciones  
 Si la aplicación se ejecutará en un sistema operativo de 64 bits, vea Información de ODBC de [64 bits](../../../odbc/reference/odbc-64-bit-information.md).  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
