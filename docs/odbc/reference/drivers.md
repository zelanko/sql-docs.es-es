---
title: Controladores | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC architecture [ODBC], drivers
- drivers [ODBC]
- drivers [ODBC], about drivers
ms.assetid: d6795d92-877e-44e1-b7d5-2ff2fd3989bd
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 709bb1e5f7ac9aefa740897d517c48dc1525cdbb
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="drivers"></a>Controladores
*Controladores* son bibliotecas que implementan las funciones de la API de ODBC. Cada uno de ellos es específico para un DBMS determinado; Por ejemplo, un controlador para Oracle no puede acceder directamente a datos en un DBMS de Informix. Controladores de exponen las capacidades de los DBMS subyacentes; que no son necesarias para implementar funciones no admitidas por el DBMS. Por ejemplo, si el DBMS subyacente no admite combinaciones externas, a continuación, ninguna de ellas debe el controlador. La única excepción importante para esto es que controladores para DBMS que no tienen los motores de base de datos independiente, como Xbase, deben implementar un motor de base de datos que admita al menos una cantidad mínima de SQL.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Tareas de controlador](../../odbc/reference/driver-tasks.md)  
  
-   [Arquitectura de controladores](../../odbc/reference/driver-architecture.md)  
  
## <a name="see-also"></a>Vea también  
 [Controladores ODBC proporcionados por Microsoft](../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)
