---
title: Limitaciones de la instrucción ALTER TABLE | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1333cd6cd5946b7a3a70152e12f4d3decfa7fed0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138433"
---
# <a name="alter-table-statement-limitations"></a>Limitaciones de declaración de tabla ALTER
Cuando se usa el controlador dBASE o Paradox, una vez que se ha creado un índice y se ha agregado un nuevo registro, la instrucción ALTER TABLE no puede cambiar la estructura de la tabla a menos que se quite el índice y se elimine el contenido de la tabla.  
  
 No se admiten las instrucciones ALTER TABLE para los controladores de texto o de Microsoft Excel.  
  
> [!NOTE]  
>  Cuando se usa el controlador de Paradox sin implementar el Motor de base de datos de Borland, no se admiten las instrucciones ALTER TABLE. solo se permiten las instrucciones Read y Append.
