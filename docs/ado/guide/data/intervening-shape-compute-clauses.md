---
title: Cláusulas COMPUTE de forma que intervengan | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- COMPUTE clause [ADO]
- data shaping [ADO], COMPUTE clause
ms.assetid: a576bf81-8f3c-4ba1-817b-87e89a8da684
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2b51bdbb489c3ddb1c00663dc70d05841dd6fb36
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63161479"
---
# <a name="intervening-shape-compute-clauses"></a>Cláusulas COMPUTE de forma que intervengan
Es válido para insertar una o más cláusulas COMPUTE entre los primarios y secundarios en un comando de forma con parámetros, como se muestra en el ejemplo siguiente:  
  
```  
SHAPE {select au_lname, state from authors} APPEND   
   ((SHAPE   
      (SHAPE   
         {select * from authors where state = ?} rs   
      COMPUTE rs, ANY(rs.state) state, ANY(rs.au_lname) au_lname   
      BY au_id) rs2   
   COMPUTE rs2, ANY(rs2.state) BY au_lname)   
RELATE state TO PARAMETER 0)  
```  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la forma de datos](../../../ado/guide/data/data-shaping-example.md)   
 [Gramática formal de forma](../../../ado/guide/data/formal-shape-grammar.md)   
 [Comandos Shape en General](../../../ado/guide/data/shape-commands-in-general.md)
