---
title: Nombres de tabla | Documentos de Microsoft
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
- SQL grammar [ODBC], table names
- table names [ODBC]
ms.assetid: f7a5cb0a-3be7-4f46-82f9-64ffdbceaa9b
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 480ca31108b608139b5563f0c18d1fa020e76f75
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="table-names"></a>Nombres de tabla
Cuando el dBASE, Microsoft Excel, Paradox, o se utiliza el controlador de texto, nombres de tabla que se producen en la cláusula FROM de SELECT o DELETE, después de la cláusula INTO de INSERCIÓN y después de la actualización, CREATE TABLE y DROP TABLE pueden contener una ruta de acceso válida, nombre del servidor principal y nombre de archivo extensión .  
  
 Uso de un nombre de tabla en otra parte de una instrucción SQL no admite el uso de las rutas de acceso o extensiones pero aceptará solo el nombre principal (por ejemplo, EMP desde C:\ABC\EMP).  
  
 Nombres de correlación (alias) se pueden usar. Por ejemplo:  
  
```  
SELECT *    
FROM C:\ABC\EMP T1    
WHERE T1.COL1 = 'aaa'  
```
