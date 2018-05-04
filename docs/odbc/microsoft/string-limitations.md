---
title: Limitaciones de cadena | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: ec1da65f-c69d-415d-bf75-8fda8aa2b39f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 740a6688d80d104d483c67c6998d20ec204ab41f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="string-limitations"></a>Limitaciones de cadena
La longitud máxima de una cadena de instrucción SQL es 65.000 caracteres.  
  
 Cuando se utiliza el controlador de Microsoft Access, se admiten únicamente constantes de cadena de SQL-92 (con comillas simples, comillas dobles no).  
  
 El carácter de barra vertical (&#124;) no se puede usar en una cadena, si el carácter está entre comillas atrás o no.  
  
 Para obtener una interoperabilidad máxima, las aplicaciones deberían pasar cadenas en parámetros, en lugar de pasar entre comillas las cadenas.
