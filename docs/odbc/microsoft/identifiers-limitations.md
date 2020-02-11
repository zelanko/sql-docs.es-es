---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 251ae0e4e94cec903e2c4b5cf687ed9b8b41dfc8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67952397"
---
# <a name="identifiers-limitations"></a>Limitaciones de identificadores
Si un identificador contiene un espacio o un símbolo especial, el identificador debe incluirse entre comillas. Un nombre válido es una cadena de no más de 64 caracteres, de los cuales el primer carácter no debe ser un espacio. Los nombres válidos no pueden incluir caracteres de control ni los siguientes caracteres especiales: ' &#124; # *? [ ] . ! $ .  
  
 No use las palabras reservadas que aparecen en la gramática de SQL en el Apéndice C de la *Referencia del programador de ODBC* (o la forma abreviada de estas palabras reservadas) como identificadores (es decir, nombres de tablas o columnas), a menos que rodee la palabra entre comillas (').
