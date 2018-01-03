---
title: Limitaciones de identificadores | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: b3466382-71cb-4f82-8318-092a8fcef3df
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6bc9deecbd06b3bcb0aec9d3e0d3b8790c7af0b6
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="identifiers-limitations"></a>Limitaciones de identificadores
Si un identificador contiene un espacio o un símbolo especial, el identificador debe incluirse entre comillas atrás. Un nombre válido es una cadena de no más de 64 caracteres, de los cuales el primer carácter no debe ser un espacio. Los nombres válidos no pueden contener caracteres de control ni los siguientes caracteres especiales: ' &#124; # * ? [ ] . ! $ .  
  
 No utilice palabras reservadas que se enumeran en la gramática SQL en el apéndice C de la *referencia del programador de ODBC* (o la forma abreviada de estas palabras reservadas) como identificadores (es decir, tabla o columna de nombres), a menos que rodean la palabra en la parte posterior comillas (').
