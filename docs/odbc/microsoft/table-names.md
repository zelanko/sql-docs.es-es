---
title: Nombres de tabla | Documentos de Microsoft
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
- SQL grammar [ODBC], table names
- table names [ODBC]
ms.assetid: f7a5cb0a-3be7-4f46-82f9-64ffdbceaa9b
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f1b1032ccda48d5a645e9992e2c501c851f51b7e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
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
