---
title: Limitaciones de identificadores ? Microsoft Docs
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
ms.openlocfilehash: 7154f2db09b69e6376b1fe3af1de3f2c646ee94e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286255"
---
# <a name="identifiers-limitations"></a>Limitaciones de identificadores
Si un identificador contiene un espacio o un símbolo especial, el identificador debe incluirse entre comillas inversas. Un nombre válido es una cadena de no más de 64 caracteres, de los cuales el primer carácter no debe ser un espacio. Los nombres válidos no pueden incluir caracteres de control o los siguientes caracteres especiales: ' &#124; ? [ ] . ! $ .  
  
 No utilice las palabras reservadas enumeradas en la gramática SQL en el Apéndice C de la *Referencia del Programador ODBC* (o la forma abreviada de estas palabras reservadas) como identificadores (es decir, nombres de tabla o columna), a menos que rodee la palabra entre comillas posteriores (').
