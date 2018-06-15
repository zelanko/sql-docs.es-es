---
title: Limitaciones de identificadores | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: b3466382-71cb-4f82-8318-092a8fcef3df
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 087d7ba056a5da10ae8d191592f06c312583b62b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32900270"
---
# <a name="identifiers-limitations"></a>Limitaciones de identificadores
Si un identificador contiene un espacio o un símbolo especial, el identificador debe incluirse entre comillas atrás. Un nombre válido es una cadena de no más de 64 caracteres, de los cuales el primer carácter no debe ser un espacio. ¿Los nombres válidos no pueden contener caracteres de control ni los siguientes caracteres especiales: ' &#124; # *? [ ] . ! $ .  
  
 No utilice palabras reservadas que se enumeran en la gramática SQL en el apéndice C de la *referencia del programador de ODBC* (o la forma abreviada de estas palabras reservadas) como identificadores (es decir, tabla o columna de nombres), a menos que rodean la palabra en la parte posterior comillas (').
