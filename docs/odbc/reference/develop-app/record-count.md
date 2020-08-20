---
description: Número de registros
title: Recuento de registros | Microsoft Docs
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
ms.openlocfilehash: 3d329ca3638f964244cea8c28f7e07e171887fb9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465675"
---
# <a name="record-count"></a>Número de registros
El SQL_DESC_COUNT campo de encabezado de un descriptor es el índice de base uno del registro con el número más alto que contiene los datos. Este campo no es un recuento de todas las columnas o parámetros enlazados. Cuando se asigna un descriptor, el valor inicial de SQL_DESC_COUNT es 0.  
  
 El controlador toma las medidas necesarias para asignar y mantener el almacenamiento que necesita para contener información del descriptor. La aplicación no especifica explícitamente el tamaño de un descriptor ni asigna nuevos registros. Cuando la aplicación proporciona información para un registro de descriptor cuyo número es mayor que el valor de SQL_DESC_COUNT, el controlador aumenta automáticamente SQL_DESC_COUNT. Cuando la aplicación desenlaza el registro del descriptor con el número más alto, el controlador disminuye automáticamente SQL_DESC_COUNT para que contenga el número del registro enlazado más alto.
