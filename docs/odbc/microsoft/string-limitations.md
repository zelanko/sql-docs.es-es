---
title: Limitaciones de cadena | Documentos de Microsoft
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
ms.assetid: ec1da65f-c69d-415d-bf75-8fda8aa2b39f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dd397b02f72a9962e4fe87683141fa98f81cfbdc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="string-limitations"></a>Limitaciones de cadena
La longitud máxima de una cadena de instrucción SQL es 65.000 caracteres.  
  
 Cuando se utiliza el controlador de Microsoft Access, se admiten únicamente constantes de cadena de SQL-92 (con comillas simples, comillas dobles no).  
  
 El carácter de barra vertical (&#124;) no se puede usar en una cadena, si el carácter está entre comillas atrás o no.  
  
 Para obtener una interoperabilidad máxima, las aplicaciones deberían pasar cadenas en parámetros, en lugar de pasar entre comillas las cadenas.
