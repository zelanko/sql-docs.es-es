---
title: Número de registros | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- record count [ODBC]
- descriptors [ODBC], record count
ms.assetid: 46eec3cc-0ecc-4980-9020-fb74a9af5730
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b4ab002f144070c94a659f0b1d67d09de9ceed50
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="record-count"></a>Número de registros
El campo de encabezado SQL_DESC_COUNT de un descriptor es el índice basado en uno del registro con el número mayor que contiene los datos. Este campo no es un recuento de todas las columnas o parámetros enlazados. Cuando se asigna un descriptor de, el valor inicial de SQL_DESC_COUNT es 0.  
  
 El controlador toma cualquier acción necesaria para asignar y mantener el almacenamiento que considere necesario para almacenar información del descriptor. La aplicación no explícitamente especificar el tamaño de un descriptor de ni asignar los nuevos registros. Si la aplicación proporciona información sobre un registro de descriptor cuyo número es mayor que el valor de SQL_DESC_COUNT, el controlador aumenta automáticamente a SQL_DESC_COUNT. Cuando la aplicación desenlaza el registro del descriptor con el número mayor, el controlador reducirá automáticamente SQL_DESC_COUNT para contener el número del mayor registro enlazado restante.
