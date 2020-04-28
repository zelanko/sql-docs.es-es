---
title: Opciones de conexión | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection options [ODBC]
- ODBC driver for Oracle [ODBC], connection options
- custom connection options [ODBC]
ms.assetid: abfdc133-cb33-435f-a467-fbe15444f687
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 25cfe2a897b0c312f91cd0c1e41ad6fa11725ab8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81281315"
---
# <a name="connect-options"></a>Opciones de conexión
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Estas opciones permiten la personalización de la conexión de base de datos dentro de una aplicación.  
  
|Opción de conexión|Notas|  
|--------------------|-----------|  
|SQL_AUTOCOMMIT|Si elige SQL_AUTOCOMMIT_OFF, la aplicación debe confirmar o revertir explícitamente las transacciones con [SQLTransact](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md).|  
|SQL_ODBC_CURSORS|Este atributo de conexión se implementa en el administrador de controladores.|  
|SQL_OPT_TRACE|Este atributo de conexión se implementa en el administrador de controladores.|  
|SQL_OPT_TRACEFILE|Este atributo de conexión se implementa en el administrador de controladores.|  
|SQL_TRANSLATE_DLL|Devuelve el error: "controlador no compatible".|  
|SQL_TRANSLATE_OPTION|Un valor de 32 bits pasado a Translation. dll.|  
|SQL_TXN_ISOLATION|El controlador solo permite SQL_TXN_READ_COMMITTED.<br /><br /> No se admiten los siguientes vParams:<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
|SQL_ATTR_ENLIST_IN_DTC|Este atributo de conexión ODBC 3,0 le permite usar el controlador ODBC para Oracle en las transacciones distribuidas coordinadas por los servicios de componentes de Microsoft (o MTS, si usa Windows NT). Proporciona el puntero de interfaz *pITransaction* a la transacción como el argumento *vParam* .|  
|SQL_ATTR_CONNECTION_DEAD|Este atributo de conexión ODBC 3,5 de solo lectura permite determinar si se ha producido un error en la conexión con el servidor de Oracle. Solo obtener; no se puede establecer.|
