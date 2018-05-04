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
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, ALTER TABLE statement limitations
- ALTER TABLE statement limitations [ODBC]
ms.assetid: f3e88f85-edf4-47cd-a822-292b106ddb34
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9ccff64afd3a4df26b813bb30a84322d50519bd2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="alter-table-statement-limitations"></a>Limitaciones de declaración de tabla ALTER
Cuando el controlador de Paradox o dBASE se usa, una vez que se ha creado un índice y agrega un nuevo registro, la estructura de la tabla no se puede cambiar mediante la instrucción ALTER TABLE, a menos que se quite el índice y se elimina el contenido de la tabla.  
  
 Las instrucciones ALTER TABLE no se admiten para los controladores de Microsoft Excel o texto.  
  
> [!NOTE]  
>  Cuando se usa el controlador de Paradox sin necesidad de implementar el motor de base de datos de Borland, no se admiten las instrucciones ALTER TABLE; solo lectura y anexar se permiten las instrucciones.
