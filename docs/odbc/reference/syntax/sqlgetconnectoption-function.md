---
title: Función SQLGetConnectOption ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetConnectOption
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetConnectOption
helpviewer_keywords:
- SQLGetConnectOption function [ODBC]
ms.assetid: 59cde899-7957-4b5e-8677-f34d3b859bfd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 94a29637365862990ea067f663023fae04a7af3e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285575"
---
# <a name="sqlgetconnectoption-function"></a>Función SQLGetConnectOption
**Conformidad**  
 Versión introducida: Cumplimiento de normas ODBC 1.0: en desuso  
  
 **Resumen**  
 En ODBC *3.x*, la función ODBC *2.x* **SQLGetConnectOption** se ha reemplazado por **SQLGetConnectAttr**. Para obtener más información, vea [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md).  
  
> [!NOTE]
>  Para obtener más información acerca de lo que el Administrador de controladores asigna esta función cuando una aplicación ODBC *2.x* está trabajando con un controlador ODBC *3.x,* vea asignación de [funciones en desuso](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) en apéndice G: directrices de controlador para la compatibilidad con versiones anteriores.  
> 
> [!NOTE]
>  **SQLGetConnectOption**no admite el atributo SQL_ASYNC_DBC_FUNCTION_ENABLE introducido en ODBC 3.8. Las aplicaciones que usan la operación asincrónica en un identificador de conexión deben usar **SQLGetConnectAttr**.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
