---
title: Establecer ExtendedAnsiSQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- extendedANSISQL [ODBC], setting
ms.assetid: 37b775d1-65ac-45ac-8572-454bc4e3c1a2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c9b8999e229e8a6ed4804b2f06a4072d139ae93a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63159364"
---
# <a name="setting-extendedansisql"></a>Establecer ExtendedAnsiSQL
El atributo se puede controlar en la cadena de conexión, agregando el atributo ExtendedAnsiSQL:  
  
|Valor|Descripción|  
|-----------|-----------------|  
|ExtendedAnsiSQL = 0 (valor predeterminado)|Esta configuración no habilita las nuevas características.|  
|ExtendedAnsiSQL = 1|Esta configuración habilita las características nuevas.|  
  
 El atributo también se puede establecer en un DSN mediante el **opciones avanzadas** cuadro de diálogo al configurar un DSN mediante el Panel de Control.  
  
 Establecer el atributo en 0 deshabilita las características nuevas; Si se establece en 1, habilita las características nuevas.  
  
 El atributo también puede establecerse utilizando SQLSetConnectAttr(). El valor del atributo es 65501 y se establece en un valor SQLINTEGER 1 ó 0, tal como se describe en la tabla anterior. Se puede llamar antes o después de conectarse, pero es mejor que lo llame después de conectarse debido al orden en el que los procesos de controlador en caché los atributos de conexión y las cadenas de conexión.
