---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2e6d053e4d2a5520432c4c1debbafb35fdb17bc4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68016743"
---
# <a name="static-sql"></a>SQL estático
El SQL incrustado que se muestra en el [ejemplo de SQL incrustado](../../odbc/reference/embedded-sql-example.md) se conoce como SQL estático. Se denomina SQL estático porque las instrucciones SQL del programa son estáticas; es decir, no cambian cada vez que se ejecuta el programa. Tal y como se describe en la sección anterior, estas instrucciones se compilan cuando se compila el resto del programa.  
  
 SQL estático funciona bien en muchas situaciones y se puede usar en cualquier aplicación para la que se pueda determinar el acceso a los datos en tiempo de diseño del programa. Por ejemplo, un programa de entrada de pedidos siempre usa la misma instrucción para insertar un nuevo pedido, y un sistema de reserva de una línea aérea siempre usa la misma instrucción para cambiar el estado de un puesto de disponible a reservado. Cada una de estas instrucciones se generalizará mediante el uso de variables de host; se pueden insertar valores diferentes en un pedido de ventas y se pueden reservar diferentes puestos. Dado que estas instrucciones pueden estar codificadas de forma rígida en el programa, estos programas tienen la ventaja de que las instrucciones se deben analizar, validar y optimizar solo una vez, en tiempo de compilación. Esto da como resultado un código relativamente rápido.
