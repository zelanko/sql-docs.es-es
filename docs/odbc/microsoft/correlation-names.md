---
title: Nombres de correlación | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- correlation names [ODBC]
- SQL grammar [ODBC], correlation names
ms.assetid: 76c36c6f-f8e1-4ece-a77b-611dde3bdd8a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0b8a253f9d252beb42080d2085adb962206ebd94
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47792763"
---
# <a name="correlation-names"></a>Nombres de correlación
Nombres de correlación son totalmente compatibles, incluidos dentro de la lista de tabla. Por ejemplo, en la siguiente cadena, E1 es el nombre de correlación para la tabla denominada Emp:  
  
```  
SELECT * FROM Emp E1   
WHERE E1.LastName = 'Smith'  
```
