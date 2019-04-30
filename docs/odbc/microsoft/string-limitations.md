---
title: Limitaciones de cadena | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: ec1da65f-c69d-415d-bf75-8fda8aa2b39f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 003cd318d6db54c7547375219805c63cfc4ce249
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63269861"
---
# <a name="string-limitations"></a>Limitaciones de cadena
La longitud máxima de una cadena de instrucción SQL es 65 000 caracteres.  
  
 Cuando se usa el controlador de Microsoft Access, se admiten solo constantes de cadena de SQL-92 (con comillas simples, comillas dobles no).  
  
 El carácter de barra vertical (&#124;) no se puede usar en una cadena, si el carácter está entre comillas atrás o no.  
  
 Para obtener la máxima interoperatividad, las aplicaciones deben pasar cadenas de parámetros, en lugar de pasar cadenas de comillas.
