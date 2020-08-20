---
description: Limitaciones de la instrucción de actualización
title: Limitaciones de la instrucción UPDATE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- UPDATE statement limitations [ODBC]
- ODBC SQL grammar, UPDATE statement limitations
ms.assetid: 14700aac-e135-4dc0-9138-4b01224461d5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b7c1ea2e5e9d887005084cdb5454dcf9b5e8fa24
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471404"
---
# <a name="update-statement-limitations"></a>Limitaciones de la instrucción de actualización
Para que el controlador de Paradox actualice una tabla, la tabla debe tener un índice único (clave principal de Paradox). Cuando se usa el controlador de Paradox sin implementar el Motor de base de datos de Borland, no es posible actualizar una tabla de Paradox.  
  
 No es compatible con el controlador de texto.  
  
 Cuando se utiliza el controlador de Microsoft Excel, es posible actualizar los valores, pero no se puede eliminar una fila de una tabla basada en una hoja de cálculo de Microsoft Excel. Como resultado, la instrucción UPDATE no se considera oficialmente compatible con el controlador de Microsoft Excel. Solo se considera compatible la instrucción INSERT.
