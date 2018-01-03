---
title: "Función SQLSetConnectOption | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLSetConnectOption
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLSetConnectOption
helpviewer_keywords: SQLSetConnectOption function [ODBC]
ms.assetid: 8cd2c2a2-25c8-4aff-951c-b593bbfc90ad
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1a3ebe388429949f64e58ba8612328caf3a14ee2
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="sqlsetconnectoption-function"></a>SQLSetConnectOption (función)
**Conformidad**  
 Versión introdujo: Cumplimiento de estándares 1.0 de ODBC: en desuso  
  
 **Resumen**  
 En ODBC 3*.x*, la función de ODBC 2.0 **SQLSetConnectOption** se ha reemplazado por **SQLSetConnectAttr**. Para obtener más información, consulte [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
> [!NOTE]  
>  Para obtener más información sobre lo que el Administrador de controladores se asigna esta función cuando una API ODBC 2*.x* aplicación está trabajando con una aplicación ODBC 3*.x* controladores, consulte [asignación de funciones en desuso](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)".  
  
## <a name="remarks"></a>Comentarios  
 Vea [información ODBC de 64 bits](../../../odbc/reference/odbc-64-bit-information.md), si la aplicación se ejecutará en un sistema operativo de 64 bits.  
  
> [!NOTE]  
>  No admite el atributo SQL_ASYNC_DBC_FUNCTION_ENABLE introducidas en ODBC 3.8 **SQLSetConnectOption**. Las aplicaciones que usan la operación asincrónica en el identificador de conexión deben utilizar **SQLSetConnectAttr**.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
