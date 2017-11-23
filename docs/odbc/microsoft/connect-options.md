---
title: "Opciones de conexión | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connection options [ODBC]
- ODBC driver for Oracle [ODBC], connection options
- custom connection options [ODBC]
ms.assetid: abfdc133-cb33-435f-a467-fbe15444f687
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 43cb42e7d77cbf3471f2475af5290ba045db05fa
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="connect-options"></a>Opciones de conexión
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Estas opciones permiten la personalización de la conexión de base de datos dentro de una aplicación.  
  
|Opción de conexión|Notas|  
|--------------------|-----------|  
|SQL_AUTOCOMMIT|Si elige SQL_AUTOCOMMIT_OFF, la aplicación debe confirmar o revertir las transacciones con explícitamente [SQLTransact](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md).|  
|SQL_ODBC_CURSORS|Este atributo de conexión se implementa en el Administrador de controladores.|  
|SQL_OPT_TRACE|Este atributo de conexión se implementa en el Administrador de controladores.|  
|SQL_OPT_TRACEFILE|Este atributo de conexión se implementa en el Administrador de controladores.|  
|SQL_TRANSLATE_DLL|Devuelve el error: "Controladores no compatibles con".|  
|SQL_TRANSLATE_OPTION|Se pasa un valor de 32 bits a la DLL de traducción.|  
|SQL_TXN_ISOLATION|El controlador permite solo SQL_TXN_READ_COMMITTED.<br /><br /> No se admiten los siguientes vParams:<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
|SQL_ATTR_ENLIST_IN_DTC|Este atributo de conexión de ODBC 3.0 le permite usar el controlador ODBC para Oracle en transacciones distribuidas coordinadas por servicios de componentes de Microsoft (o MTS, si está utilizando Windows NT). Proporciona el puntero de interfaz *pITransaction* a la transacción como la *vParam* argumento.|  
|SQL_ATTR_CONNECTION_DEAD|Este atributo de conexión de ODBC 3.5 de solo lectura le permite determinar si la conexión con el servidor de Oracle no ha podido. Obtener solo; no se puede establecer.|
