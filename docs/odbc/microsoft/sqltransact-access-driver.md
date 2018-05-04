---
title: SQLTransact (controlador de acceso) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLTransact
- SQLTransact function [ODBC], Access Driver
ms.assetid: 892b79c7-9e20-4d1f-bc60-d4b25694ca25
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5f157d3423f6a409ea165a32d058f16d14d1d949
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqltransact-access-driver"></a>SQLTransact (controlador de Access)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de acceso. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Cuando se utiliza el controlador de Microsoft Access, SQL_COMMIT o SQL_ROLLBACK se admiten para la *fType* argumento en una llamada a **SQLTransact**.  
  
 Si se produce un error durante el proceso de confirmación, se puede reparar la base de datos mediante la opción de base de datos de reparación en el programa de instalación del controlador de Microsoft Access, o mediante el uso de la palabra clave REPAIR_DB en el **SQLConfigDataSource** función.
