---
title: Controladores | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC architecture [ODBC], drivers
- drivers [ODBC]
- drivers [ODBC], about drivers
ms.assetid: d6795d92-877e-44e1-b7d5-2ff2fd3989bd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6460410488186c94713d859bf2912f2844ca2736
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67915430"
---
# <a name="drivers"></a>Controladores
Los *Controladores* son bibliotecas que implementan las funciones de la API de ODBC. Cada es específico de un DBMS determinado; por ejemplo, un controlador para Oracle no puede acceder directamente a los datos de un DBMS de Informix. Los controladores exponen las capacidades de los DBMS subyacentes. no son necesarios para implementar funciones no admitidas por el DBMS. Por ejemplo, si el DBMS subyacente no admite combinaciones externas, ninguno debe ser el controlador. La única excepción principal es que los controladores para DBMS que no tienen motores de base de datos independientes, como xBase, deben implementar un motor de base de datos que admita al menos una cantidad mínima de SQL.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Tareas de controlador](../../odbc/reference/driver-tasks.md)  
  
-   [Arquitectura de controladores](../../odbc/reference/driver-architecture.md)  
  
## <a name="see-also"></a>Consulte también  
 [Controladores ODBC proporcionados por Microsoft](../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)
