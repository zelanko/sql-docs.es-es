---
title: Nombres de la tabla ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL grammar [ODBC], table names
- table names [ODBC]
ms.assetid: f7a5cb0a-3be7-4f46-82f9-64ffdbceaa9b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 91a415cd456186f18ef358b9d504145f78152774
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303126"
---
# <a name="table-names"></a>Nombres de tabla
Cuando se utiliza el controlador dBASE, Microsoft Excel, Paradox o Text, los nombres de tabla que se producen en la cláusula FROM de SELECT o DELETE, después de la cláusula INTO en INSERT y después de UPDATE, CREATE TABLE y DROP TABLE pueden contener una ruta de acceso válida, un nombre principal y una extensión de nombre de archivo.  
  
 El uso de un nombre de tabla en otra parte de una instrucción SQL no admite el uso de rutas de acceso o extensiones, pero solo aceptará el nombre principal (por ejemplo, EMP FROM C:-ABC-EMP).  
  
 Se pueden utilizar nombres de correlación (alias). Por ejemplo:  
  
```  
SELECT *    
FROM C:\ABC\EMP T1    
WHERE T1.COL1 = 'aaa'  
```
