---
title: Limitaciones de identificadores | Documentos de Microsoft
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
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: b3466382-71cb-4f82-8318-092a8fcef3df
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 559a9208b95f4e2e24bfd21ecf83aba98efbb628
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="identifiers-limitations"></a>Limitaciones de identificadores
Si un identificador contiene un espacio o un símbolo especial, el identificador debe incluirse entre comillas atrás. Un nombre válido es una cadena de no más de 64 caracteres, de los cuales el primer carácter no debe ser un espacio. Los nombres válidos no pueden contener caracteres de control ni los siguientes caracteres especiales: ' &#124; # * ? [ ] . ! $ .  
  
 No utilice palabras reservadas que se enumeran en la gramática SQL en el apéndice C de la *referencia del programador de ODBC* (o la forma abreviada de estas palabras reservadas) como identificadores (es decir, tabla o columna de nombres), a menos que rodean la palabra en la parte posterior comillas (').
