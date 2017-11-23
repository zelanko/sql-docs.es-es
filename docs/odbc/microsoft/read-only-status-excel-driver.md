---
title: Estado de solo lectura (controlador de Excel) | Documentos de Microsoft
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
- read-only status for Excel driver [ODBC]
- Excel driver [ODBC], read-only status
ms.assetid: ef5d773b-4f8f-4005-b985-84b53d8e9f9b
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f2aadcc2a1ce449b59f4ac360cad941203275e15
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="read-only-status-excel-driver"></a>Estado de solo lectura (controlador de Excel)
Cuando se utiliza el controlador de Microsoft Excel, tablas de origen de datos se abren como de solo lectura de forma predeterminada y se pueden abrir haciendo solo un usuario a la vez. Aunque las tablas que el estado de solo lectura, sin embargo, las aplicaciones pueden realizar inserciones y actualizaciones para las tablas de Microsoft Excel.  
  
 Cuando una aplicación realiza un comando Guardar como en los datos de Microsoft Excel a través del controlador de Microsoft Excel, la aplicación debe crear una nueva tabla e introducir los datos que se debe guardar en la nueva tabla. Inserciones dar un anexar a la tabla. Ninguna otra operación puede realizarse en la tabla hasta que se cierra y se vuelve a abrir. Una vez que se cierra la tabla, no se puede realizar ninguna inserción posterior porque la tabla es una tabla de sólo lectura.  
  
 Es posible actualizar valores cuando se utiliza el controlador de Microsoft Excel, pero no se puede eliminar una fila de una tabla basada en una hoja de cálculo de Microsoft Excel, por lo que las actualizaciones no se consideran compatibles oficialmente con el controlador de Microsoft Excel.
