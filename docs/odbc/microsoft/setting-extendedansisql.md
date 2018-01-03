---
title: Establecer ExtendedAnsiSQL | Documentos de Microsoft
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
helpviewer_keywords: extendedANSISQL [ODBC], setting
ms.assetid: 37b775d1-65ac-45ac-8572-454bc4e3c1a2
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d263d57d9fecbcb03f737dc73472452367900a47
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="setting-extendedansisql"></a>Establecer ExtendedAnsiSQL
El atributo puede controlarse en la cadena de conexión agregando el atributo ExtendedAnsiSQL:  
  
|Valor|Description|  
|-----------|-----------------|  
|ExtendedAnsiSQL = 0 (valor predeterminado)|Esta configuración no habilita las características nuevas.|  
|ExtendedAnsiSQL = 1|Esta opción habilita las características nuevas.|  
  
 El atributo también puede establecerse en un DSN a través de la **opciones avanzadas** cuadro de diálogo al configurar un DSN a través del Panel de Control.  
  
 Establecer el atributo como 0, se deshabilita las nuevas características; Si se establece en 1, habilita las características nuevas.  
  
 El atributo también puede establecerse utilizando SQLSetConnectAttr(). El valor del atributo es 65501 y se establece en un valor SQLINTEGER de 1 ó 0, tal como se describe en la tabla anterior. Se puede llamar antes o después de conectarse, pero resulta más conveniente llamar después de conectarse debido al orden en el que los procesos de controlador en caché atributos de conexión y las cadenas de conexión.
