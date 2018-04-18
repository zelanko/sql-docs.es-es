---
title: Limitaciones de declaración de tabla ALTER | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ODBC SQL grammar, ALTER TABLE statement limitations
- ALTER TABLE statement limitations [ODBC]
ms.assetid: f3e88f85-edf4-47cd-a822-292b106ddb34
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 06af545611da90d51ad0fc82136a4cb1ecc3984c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="alter-table-statement-limitations"></a>Limitaciones de declaración de tabla ALTER
Cuando el controlador de Paradox o dBASE se usa, una vez que se ha creado un índice y agrega un nuevo registro, la estructura de la tabla no se puede cambiar mediante la instrucción ALTER TABLE, a menos que se quite el índice y se elimina el contenido de la tabla.  
  
 Las instrucciones ALTER TABLE no se admiten para los controladores de Microsoft Excel o texto.  
  
> [!NOTE]  
>  Cuando se usa el controlador de Paradox sin necesidad de implementar el motor de base de datos de Borland, no se admiten las instrucciones ALTER TABLE; solo lectura y anexar se permiten las instrucciones.
