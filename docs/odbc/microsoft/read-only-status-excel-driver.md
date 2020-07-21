---
title: Estado de solo lectura (controlador de Excel) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- read-only status for Excel driver [ODBC]
- Excel driver [ODBC], read-only status
ms.assetid: ef5d773b-4f8f-4005-b985-84b53d8e9f9b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eb585d4712b6cac5e09b65ee8e13604763cd0164
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304026"
---
# <a name="read-only-status-excel-driver"></a>Estado de solo lectura (controlador de Excel)
Cuando se usa el controlador de Microsoft Excel, las tablas de orígenes de datos se abren como de solo lectura de forma predeterminada y solo se pueden abrir con un usuario a la vez. Aunque las tablas tienen el estado de solo lectura, sin embargo, las aplicaciones pueden realizar inserciones y actualizaciones para las tablas de Microsoft Excel.  
  
 Cuando una aplicación ejecuta un comando Guardar como en datos de Microsoft Excel a través del controlador de Microsoft Excel, la aplicación debe crear una nueva tabla e insertar los datos que se van a guardar en la nueva tabla. Las inserciones dan como resultado una anexión a la tabla. No se puede realizar ninguna otra operación en la tabla hasta que se cierre y se vuelva a abrir. Una vez que se cierra la tabla, no se puede realizar ninguna inserción posterior porque la tabla es una tabla de solo lectura.  
  
 Es posible actualizar los valores cuando se usa el controlador de Microsoft Excel, pero no se puede eliminar una fila de una tabla basada en una hoja de cálculo de Microsoft Excel, por lo que las actualizaciones no se consideran oficialmente compatibles con el controlador de Microsoft Excel.
