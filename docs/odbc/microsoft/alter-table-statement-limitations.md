---
description: Limitaciones de declaración de tabla ALTER
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 53f86e8d2c21fb6ea2d016610848773564d4a384
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449597"
---
# <a name="alter-table-statement-limitations"></a>Limitaciones de declaración de tabla ALTER
Cuando se usa el controlador dBASE o Paradox, una vez que se ha creado un índice y se ha agregado un nuevo registro, la instrucción ALTER TABLE no puede cambiar la estructura de la tabla a menos que se quite el índice y se elimine el contenido de la tabla.  
  
 No se admiten las instrucciones ALTER TABLE para los controladores de texto o de Microsoft Excel.  
  
> [!NOTE]  
>  Cuando se usa el controlador de Paradox sin implementar el Motor de base de datos de Borland, no se admiten las instrucciones ALTER TABLE. solo se permiten las instrucciones Read y Append.
