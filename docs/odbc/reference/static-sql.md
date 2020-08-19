---
description: SQL estático
title: SQL estático | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- static SQL [ODBC]
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], embedded SQL
- SQL statements [ODBC], static SQL
- embedded SQL [ODBC]
- SQL [ODBC], static SQL
ms.assetid: 667d92ec-fed9-4028-81d4-bb9ba867356a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 19c4ec3454a5d5891a87203fe8c7aeaff21b239b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428987"
---
# <a name="static-sql"></a>SQL estático
El SQL incrustado que se muestra en el [ejemplo de SQL incrustado](../../odbc/reference/embedded-sql-example.md) se conoce como SQL estático. Se denomina SQL estático porque las instrucciones SQL del programa son estáticas; es decir, no cambian cada vez que se ejecuta el programa. Tal y como se describe en la sección anterior, estas instrucciones se compilan cuando se compila el resto del programa.  
  
 SQL estático funciona bien en muchas situaciones y se puede usar en cualquier aplicación para la que se pueda determinar el acceso a los datos en tiempo de diseño del programa. Por ejemplo, un programa de entrada de pedidos siempre usa la misma instrucción para insertar un nuevo pedido, y un sistema de reserva de una línea aérea siempre usa la misma instrucción para cambiar el estado de un puesto de disponible a reservado. Cada una de estas instrucciones se generalizará mediante el uso de variables de host; se pueden insertar valores diferentes en un pedido de ventas y se pueden reservar diferentes puestos. Dado que estas instrucciones pueden estar codificadas de forma rígida en el programa, estos programas tienen la ventaja de que las instrucciones se deben analizar, validar y optimizar solo una vez, en tiempo de compilación. Esto da como resultado un código relativamente rápido.
