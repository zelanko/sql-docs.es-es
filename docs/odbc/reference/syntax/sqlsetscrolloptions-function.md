---
title: Función SQLSetScrollOptions | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 77a85caefadb54c3db2716c4db18b504e02da996
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68342942"
---
# <a name="sqlsetscrolloptions-function"></a>Función SQLSetScrollOptions
**Conformidad**  
 Versión introducida: compatibilidad con estándares de ODBC 1,0: desusado  
  
 **Resumen**  
 En ODBC *3. x*, la función **SQLSetScrollOptions** de ODBC 2,0 se ha reemplazado por llamadas a **SQLGetInfo** y **SQLSetStmtAttr**.  
  
> [!NOTE]
>  Para obtener más información sobre lo que el administrador de controladores asigna a esta función cuando una aplicación ODBC *2. x* está trabajando con un controlador ODBC *3. x* , consulte [asignación de funciones en desuso](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) en el Apéndice G: instrucciones de controlador para la compatibilidad con versiones anteriores.  
> 
> [!NOTE]
>  Cuando el administrador de controladores asigna **SQLSetScrollOptions** para una aplicación que trabaja con un controlador ODBC *3. x* que no admite **SQLSetScrollOptions**, el administrador de controladores establece la opción de instrucción SQL_ROWSET_SIZE, no el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE, en el argumento *RowsetSize* de **SQLSetScrollOption**. Como resultado, una aplicación no puede usar **SQLSetScrollOptions** al capturar varias filas mediante una llamada a **SQLFetch** o **SQLFetchScroll**. Solo se puede usar al capturar varias filas mediante una llamada a **SQLExtendedFetch**.  
  
## <a name="remarks"></a>Observaciones  
 Si la aplicación se ejecutará en un sistema operativo de 64 bits, consulte [la información de ODBC 64](../../../odbc/reference/odbc-64-bit-information.md)bits.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
