---
title: Limitaciones de cadena | Documentos de Microsoft
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
ms.assetid: ec1da65f-c69d-415d-bf75-8fda8aa2b39f
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2a805c4a0f98b394929f5b5a7b21613eac728533
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="string-limitations"></a>Limitaciones de cadena
La longitud máxima de una cadena de instrucción SQL es 65.000 caracteres.  
  
 Cuando se utiliza el controlador de Microsoft Access, se admiten únicamente constantes de cadena de SQL-92 (con comillas simples, comillas dobles no).  
  
 El carácter de canalización (&#124;) no se puede usar en una cadena, si el carácter está entre comillas atrás o no.  
  
 Para obtener una interoperabilidad máxima, las aplicaciones deberían pasar cadenas en parámetros, en lugar de pasar entre comillas las cadenas.
