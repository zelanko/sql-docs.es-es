---
title: Los nombres de tabla | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5dd8de055521f4a1831d20a9a34bedb9309d1de6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67939787"
---
# <a name="table-names"></a>Nombres de tabla
Cuando dBASE, Microsoft Excel, Paradox, o texto que se usa el controlador, los nombres de tabla que se producen en la cláusula FROM de SELECT o DELETE, después de la cláusula INTO en INSERT y UPDATE, CREATE TABLE y DROP TABLE pueden contener una ruta de acceso válida, nombre principal y archivo de extensión de nombre .  
  
 Uso de un nombre de tabla en otra parte de una instrucción SQL no admite el uso de rutas de acceso o extensiones pero aceptará solo el nombre principal (por ejemplo, EMP desde C:\ABC\EMP).  
  
 Se pueden usar nombres de correlación (alias). Por ejemplo:  
  
```  
SELECT *    
FROM C:\ABC\EMP T1    
WHERE T1.COL1 = 'aaa'  
```
