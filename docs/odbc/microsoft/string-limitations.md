---
title: Limitaciones de la cadena ( String Limitations) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 61f81ff3da882095a0a6c41bb5061addd497a5d2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306066"
---
# <a name="string-limitations"></a>Limitaciones de cadena
La longitud máxima de una cadena de instrucción SQL es de 65.000 caracteres.  
  
 Cuando se utiliza el controlador de Microsoft Access, solo se admiten las constantes de cadena SQL-92 (entre comillas simples, no comillas dobles).  
  
 El carácter de tubería (&#124;) no se puede utilizar en una cadena, independientemente de si el carácter está entre comillas o no.  
  
 Para una interoperabilidad máxima, las aplicaciones deben pasar cadenas en parámetros, en lugar de pasar cadenas entrecomilladas.
