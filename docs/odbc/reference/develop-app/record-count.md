---
title: Recuento de registros de registros de registros de Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- record count [ODBC]
- descriptors [ODBC], record count
ms.assetid: 46eec3cc-0ecc-4980-9020-fb74a9af5730
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 28e503ae4602d87fc9138ed018ee1e95f135ec57
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281821"
---
# <a name="record-count"></a>Número de registros
El campo de encabezado SQL_DESC_COUNT de un descriptor es el índice basado en uno del registro con el número más alto que contiene datos. Este campo no es un recuento de todas las columnas o parámetros enlazados. Cuando se asigna un descriptor, el valor inicial de SQL_DESC_COUNT es 0.  
  
 El controlador realiza cualquier acción necesaria para asignar y mantener cualquier almacenamiento que necesite para contener información del descriptor. La aplicación no especifica explícitamente el tamaño de un descriptor ni asigna nuevos registros. Cuando la aplicación proporciona información para un registro descriptor cuyo número es mayor que el valor de SQL_DESC_COUNT, el controlador aumenta automáticamente SQL_DESC_COUNT. Cuando la aplicación desenlaza el registro descriptor con el número más alto, el controlador disminuye automáticamente SQL_DESC_COUNT para contener el número del registro enlazado restante más alto.
