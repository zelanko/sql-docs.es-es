---
title: SQL estático ? Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81279907"
---
# <a name="static-sql"></a>SQL estático
El SQL incrustado que se muestra en Ejemplo de [SQL incrustado](../../odbc/reference/embedded-sql-example.md) se conoce como SQL estático. Se denomina SQL estático porque las instrucciones SQL del programa son estáticas; es decir, no cambian cada vez que se ejecuta el programa. Como se describe en la sección anterior, estas instrucciones se compilan cuando se compila el resto del programa.  
  
 SQL estático funciona bien en muchas situaciones y se puede utilizar en cualquier aplicación para la que el acceso a datos se puede determinar en el momento del diseño del programa. Por ejemplo, un programa de entrada de pedidos siempre utiliza la misma instrucción para insertar un nuevo pedido y un sistema de reserva de aerolínea siempre utiliza la misma instrucción para cambiar el estado de un asiento de disponible a reservado. Cada una de estas instrucciones se generalizaría mediante el uso de variables de host; se pueden insertar valores diferentes en un pedido de cliente y se pueden reservar diferentes asientos. Dado que estas instrucciones se pueden codificar de forma rígida en el programa, estos programas tienen la ventaja de que las instrucciones deben analizarse, validarse y optimizarse solo una vez, en tiempo de compilación. Esto da como resultado un código relativamente rápido.
