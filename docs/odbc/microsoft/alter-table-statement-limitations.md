---
title: "Limitaciones de declaración de tabla ALTER | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC SQL grammar, ALTER TABLE statement limitations
- ALTER TABLE statement limitations [ODBC]
ms.assetid: f3e88f85-edf4-47cd-a822-292b106ddb34
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: acdeccfa07141c267a77a927217ad2ec610034c7
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="alter-table-statement-limitations"></a>Limitaciones de declaración de tabla ALTER
Cuando el controlador de Paradox o dBASE se usa, una vez que se ha creado un índice y agrega un nuevo registro, la estructura de la tabla no se puede cambiar mediante la instrucción ALTER TABLE, a menos que se quite el índice y se elimina el contenido de la tabla.  
  
 Las instrucciones ALTER TABLE no se admiten para los controladores de Microsoft Excel o texto.  
  
> [!NOTE]  
>  Cuando se usa el controlador de Paradox sin necesidad de implementar el motor de base de datos de Borland, no se admiten las instrucciones ALTER TABLE; solo lectura y anexar se permiten las instrucciones.
