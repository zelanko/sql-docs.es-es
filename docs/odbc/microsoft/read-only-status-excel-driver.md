---
title: Estado de solo lectura (controlador de Excel) Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304026"
---
# <a name="read-only-status-excel-driver"></a>Estado de solo lectura (controlador de Excel)
Cuando se utiliza el controlador de Microsoft Excel, las tablas de origen de datos se abren como de solo lectura de forma predeterminada y solo pueden abrirlas un usuario a la vez. Aunque las tablas tienen un estado de solo lectura, sin embargo, las aplicaciones pueden realizar inserciones y actualizaciones para las tablas de Microsoft Excel.  
  
 Cuando una aplicación realiza un comando Guardar como en los datos de Microsoft Excel a través del controlador de Microsoft Excel, la aplicación debe crear una nueva tabla e insertar los datos que se guardarán en la nueva tabla. Las inserciones dan como resultado un anexo a la tabla. No se pueden realizar otras operaciones en la tabla hasta que se cierre y se vuelva a abrir. Una vez cerrada la tabla, no se puede realizar ninguna inserción posterior porque la tabla es entonces una tabla de solo lectura.  
  
 Es posible actualizar los valores cuando se usa el controlador de Microsoft Excel, pero no se puede eliminar una fila de una tabla basada en una hoja de cálculo de Microsoft Excel, por lo que las actualizaciones no se consideran admitidas oficialmente por el controlador de Microsoft Excel.
