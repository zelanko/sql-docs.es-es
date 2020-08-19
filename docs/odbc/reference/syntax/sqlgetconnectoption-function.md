---
description: Función SQLGetConnectOption
title: Función SQLGetConnectOption | Microsoft Docs
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
ms.openlocfilehash: df3fd7dc9a024348c4371fabdbcabfab63a6f071
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421289"
---
# <a name="sqlgetconnectoption-function"></a>Función SQLGetConnectOption
**Conformidad**  
 Versión introducida: compatibilidad con estándares de ODBC 1,0: desusado  
  
 **Resumen**  
 En ODBC *3. x*, la función **SQLGetConnectOption** de ODBC *2. x* se ha reemplazado por **SQLGetConnectAttr**. Para obtener más información, vea [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md).  
  
> [!NOTE]
>  Para obtener más información sobre lo que el administrador de controladores asigna a esta función cuando una aplicación ODBC *2. x* está trabajando con un controlador ODBC *3. x* , consulte [asignación de funciones en desuso](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) en el Apéndice G: instrucciones de controlador para la compatibilidad con versiones anteriores.  
> 
> [!NOTE]
>  **SQLGetConnectOption**no admite el SQL_ASYNC_DBC_FUNCTION_ENABLE atributo introducido en ODBC 3,8. Las aplicaciones que usan la operación asincrónica en un identificador de conexión deben usar **SQLGetConnectAttr**.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
