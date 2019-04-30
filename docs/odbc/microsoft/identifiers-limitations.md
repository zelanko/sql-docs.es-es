---
title: Limitaciones de identificadores | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: c781113124d456e1ba866546d6ada7a17371d71f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63208526"
---
# <a name="identifiers-limitations"></a>Limitaciones de identificadores
Si un identificador contiene un espacio o un símbolo especial, debe incluirse el identificador de espera entre las comillas. Un nombre válido es una cadena de no más de 64 caracteres, de los cuales el primer carácter no debe ser un espacio. ¿Los nombres válidos no pueden incluir caracteres de control o los caracteres especiales siguientes: ' &#124; # *? [ ] . ! $ .  
  
 No utilice palabras reservadas que se enumeran en la gramática de SQL en el apéndice C de la *referencia del programador de ODBC* (o la forma abreviada de estas palabras reservadas) como identificadores (es decir, tabla o columna de nombres), a menos que rodean la palabra de retroceso comillas (').
