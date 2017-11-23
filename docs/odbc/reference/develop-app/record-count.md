---
title: "Número de registros | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- record count [ODBC]
- descriptors [ODBC], record count
ms.assetid: 46eec3cc-0ecc-4980-9020-fb74a9af5730
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 11c30fb4abfeab58b1a6ea650bc41ce1f72524e0
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="record-count"></a>Número de registros
El campo de encabezado SQL_DESC_COUNT de un descriptor es el índice basado en uno del registro con el número mayor que contiene los datos. Este campo no es un recuento de todas las columnas o parámetros enlazados. Cuando se asigna un descriptor de, el valor inicial de SQL_DESC_COUNT es 0.  
  
 El controlador toma cualquier acción necesaria para asignar y mantener el almacenamiento que considere necesario para almacenar información del descriptor. La aplicación no explícitamente especificar el tamaño de un descriptor de ni asignar los nuevos registros. Si la aplicación proporciona información sobre un registro de descriptor cuyo número es mayor que el valor de SQL_DESC_COUNT, el controlador aumenta automáticamente a SQL_DESC_COUNT. Cuando la aplicación desenlaza el registro del descriptor con el número mayor, el controlador reducirá automáticamente SQL_DESC_COUNT para contener el número del mayor registro enlazado restante.
