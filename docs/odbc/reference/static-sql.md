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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68016743"
---
# <a name="static-sql"></a>SQL estático
El SQL incrustado se muestra en [ejemplo SQL incrustado](../../odbc/reference/embedded-sql-example.md) se conoce como SQL estático. Se denomina SQL estático porque son estáticas; las instrucciones SQL en el programa es decir, no cambie cada vez que se ejecuta el programa. Como se describe en la sección anterior, estas instrucciones se compilan cuando se compila el resto del programa.  
  
 SQL estático funciona bien en muchas situaciones y se puede usar en cualquier aplicación para el que se puede determinar el acceso a datos en tiempo de diseño del programa. Por ejemplo, un programa de entrada de pedidos siempre utiliza la misma instrucción para insertar un nuevo pedido y un sistema de reservas de líneas aéreas siempre utiliza la misma instrucción para cambiar el estado de un asiento de disponible para la reserva. Cada una de estas instrucciones se generalizarse mediante el uso de las variables del host. se pueden insertar valores diferentes en un pedido de ventas y diferentes puestos se pueden reservar. Puesto que tales instrucciones puede codificado de forma rígida en el programa, estos programas tienen la ventaja que necesitan las instrucciones que se analiza, valida y optimizado para una sola vez, en tiempo de compilación. Esto da como resultado un código relativamente rápido.
