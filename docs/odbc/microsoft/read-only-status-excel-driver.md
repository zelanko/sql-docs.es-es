---
title: Estado de solo lectura (controlador de Excel) | Documentos de Microsoft
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
- read-only status for Excel driver [ODBC]
- Excel driver [ODBC], read-only status
ms.assetid: ef5d773b-4f8f-4005-b985-84b53d8e9f9b
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d885124c9e4274d402bfa504b975f089d333af95
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="read-only-status-excel-driver"></a>Estado de solo lectura (controlador de Excel)
Cuando se utiliza el controlador de Microsoft Excel, tablas de origen de datos se abren como de solo lectura de forma predeterminada y se pueden abrir haciendo solo un usuario a la vez. Aunque las tablas que el estado de solo lectura, sin embargo, las aplicaciones pueden realizar inserciones y actualizaciones para las tablas de Microsoft Excel.  
  
 Cuando una aplicación realiza un comando Guardar como en los datos de Microsoft Excel a través del controlador de Microsoft Excel, la aplicación debe crear una nueva tabla e introducir los datos que se debe guardar en la nueva tabla. Inserciones dar un anexar a la tabla. Ninguna otra operación puede realizarse en la tabla hasta que se cierra y se vuelve a abrir. Una vez que se cierra la tabla, no se puede realizar ninguna inserción posterior porque la tabla es una tabla de sólo lectura.  
  
 Es posible actualizar valores cuando se utiliza el controlador de Microsoft Excel, pero no se puede eliminar una fila de una tabla basada en una hoja de cálculo de Microsoft Excel, por lo que las actualizaciones no se consideran compatibles oficialmente con el controlador de Microsoft Excel.
