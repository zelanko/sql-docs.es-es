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
ms.openlocfilehash: 330b55ef2d4fee090c453990d3fe75e6e2dacb6f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68063597"
---
# <a name="setting-extendedansisql"></a>Establecer ExtendedAnsiSQL
El atributo se puede controlar en la cadena de conexión agregando el atributo ExtendedAnsiSQL:  
  
|Value|Descripción|  
|-----------|-----------------|  
|ExtendedAnsiSQL = 0 (valor predeterminado)|Esta configuración no habilita las nuevas características.|  
|ExtendedAnsiSQL = 1|Esta configuración habilita las nuevas características.|  
  
 El atributo también se puede establecer en un DSN mediante el cuadro de diálogo **Opciones avanzadas** al configurar un DSN a través del panel de control.  
  
 Al establecer el atributo en 0, se deshabilitan las nuevas características; Si se establece en 1, se habilitan las nuevas características.  
  
 El atributo también se puede establecer mediante SQLSetConnectAttr (). El valor del atributo es 65501 y se establece en un valor SQLINTEGER donde de 1 o 0, como se documenta en la tabla anterior. Se puede llamar antes o después de la conexión, pero es mejor llamarlo después de la conexión debido al orden en el que el controlador procesa los atributos de conexión y las cadenas de conexión almacenados en caché.
