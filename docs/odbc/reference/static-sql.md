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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 55710d8ea734cba86ae5e4daa725f75e94e65a64
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81279907"
---
# <a name="static-sql"></a>SQL estático
El SQL incrustado que se muestra en el [ejemplo de SQL incrustado](../../odbc/reference/embedded-sql-example.md) se conoce como SQL estático. Se denomina SQL estático porque las instrucciones SQL del programa son estáticas; es decir, no cambian cada vez que se ejecuta el programa. Tal y como se describe en la sección anterior, estas instrucciones se compilan cuando se compila el resto del programa.  
  
 SQL estático funciona bien en muchas situaciones y se puede usar en cualquier aplicación para la que se pueda determinar el acceso a los datos en tiempo de diseño del programa. Por ejemplo, un programa de entrada de pedidos siempre usa la misma instrucción para insertar un nuevo pedido, y un sistema de reserva de una línea aérea siempre usa la misma instrucción para cambiar el estado de un puesto de disponible a reservado. Cada una de estas instrucciones se generalizará mediante el uso de variables de host; se pueden insertar valores diferentes en un pedido de ventas y se pueden reservar diferentes puestos. Dado que estas instrucciones pueden estar codificadas de forma rígida en el programa, estos programas tienen la ventaja de que las instrucciones se deben analizar, validar y optimizar solo una vez, en tiempo de compilación. Esto da como resultado un código relativamente rápido.
