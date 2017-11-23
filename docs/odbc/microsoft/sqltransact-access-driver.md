---
title: SQLTransact (controlador de acceso) | Documentos de Microsoft
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
- Access driver [ODBC], SQLTransact
- SQLTransact function [ODBC], Access Driver
ms.assetid: 892b79c7-9e20-4d1f-bc60-d4b25694ca25
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 041bd1a56db21dda374a8bd279c890e187f04beb
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="sqltransact-access-driver"></a>SQLTransact (controlador de Access)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de acceso. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Cuando se utiliza el controlador de Microsoft Access, SQL_COMMIT o SQL_ROLLBACK se admiten para la *fType* argumento en una llamada a **SQLTransact**.  
  
 Si se produce un error durante el proceso de confirmación, se puede reparar la base de datos mediante la opción de base de datos de reparación en el programa de instalación del controlador de Microsoft Access, o mediante el uso de la palabra clave REPAIR_DB en el **SQLConfigDataSource** función.
