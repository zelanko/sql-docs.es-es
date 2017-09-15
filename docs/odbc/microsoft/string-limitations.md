---
title: Limitaciones de cadena | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: ec1da65f-c69d-415d-bf75-8fda8aa2b39f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e6f9d8add08f80b59adaa42f02bc1da006356081
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="string-limitations"></a>Limitaciones de cadena
La longitud máxima de una cadena de instrucción SQL es 65.000 caracteres.  
  
 Cuando se utiliza el controlador de Microsoft Access, se admiten únicamente constantes de cadena de SQL-92 (con comillas simples, comillas dobles no).  
  
 El carácter de canalización (&#124;) no se puede usar en una cadena, si el carácter está entre comillas atrás o no.  
  
 Para obtener una interoperabilidad máxima, las aplicaciones deberían pasar cadenas en parámetros, en lugar de pasar entre comillas las cadenas.
