---
description: Limitaciones de identificadores
title: Limitaciones de los identificadores | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: b3466382-71cb-4f82-8318-092a8fcef3df
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f5efaba8fa73f61082be8d7cd8dca78626a9f972
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500348"
---
# <a name="identifiers-limitations"></a>Limitaciones de identificadores
Si un identificador contiene un espacio o un símbolo especial, el identificador debe incluirse entre comillas. Un nombre válido es una cadena de no más de 64 caracteres, de los cuales el primer carácter no debe ser un espacio. Los nombres válidos no pueden incluir caracteres de control ni los siguientes caracteres especiales: ' &#124; # *? [ ] . ! $ .  
  
 No use las palabras reservadas que aparecen en la gramática de SQL en el Apéndice C de la *Referencia del programador de ODBC* (o la forma abreviada de estas palabras reservadas) como identificadores (es decir, nombres de tablas o columnas), a menos que rodee la palabra entre comillas (').
