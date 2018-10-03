---
title: Número de registros | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8f8b0a6fc7aa5765d9373af33ab4fac0a4a07aac
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47610435"
---
# <a name="record-count"></a>Número de registros
El campo de encabezado SQL_DESC_COUNT de un descriptor de es el índice basado en uno del registro con el número mayor que contiene los datos. Este campo no es un recuento de todas las columnas o parámetros enlazados. Cuando se asigna un descriptor, el valor inicial de SQL_DESC_COUNT es 0.  
  
 El controlador toma cualquier acción necesaria para asignar y mantener cualquier almacenamiento que necesita para almacenar información del descriptor. La aplicación explícitamente no especificar el tamaño de un descriptor de ni asignar nuevos registros. Cuando la aplicación proporciona la información de registro de descriptor cuyo número es mayor que el valor de SQL_DESC_COUNT, el controlador aumenta automáticamente SQL_DESC_COUNT. Cuando la aplicación desenlaza el registro del descriptor con el número mayor, el controlador reducirá automáticamente SQL_DESC_COUNT para contener el número del registro enlazado restante más alta.
