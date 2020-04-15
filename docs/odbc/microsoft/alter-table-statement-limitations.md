---
title: Limitaciones de la Declaración ALTER TABLE ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, ALTER TABLE statement limitations
- ALTER TABLE statement limitations [ODBC]
ms.assetid: f3e88f85-edf4-47cd-a822-292b106ddb34
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 19afa8b07b0051de9ce45ec652ea337c0f689f52
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304704"
---
# <a name="alter-table-statement-limitations"></a>Limitaciones de declaración de tabla ALTER
Cuando se utiliza el controlador dBASE o Paradox, una vez que se ha creado un índice y se ha agregado un nuevo registro, la instrucción ALTER TABLE no puede cambiar la estructura de la tabla a menos que se descarta el índice y se elimine el contenido de la tabla.  
  
 Las instrucciones ALTER TABLE no se admiten para los controladores de Microsoft Excel o Text.  
  
> [!NOTE]  
>  Cuando se utiliza el controlador Paradox sin implementar El motor de base de datos de Borland, no se admiten instrucciones ALTER TABLE; solo se permiten instrucciones de lectura y anexión.
