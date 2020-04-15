---
title: Configuración de ExtendedAnsiSQL ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6b5c2e4ed4d8bd64d02fb6a62861db832f6b0898
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300805"
---
# <a name="setting-extendedansisql"></a>Establecer ExtendedAnsiSQL
El atributo se puede controlar en la cadena de conexión agregando el atributo ExtendedAnsiSQL:  
  
|Value|Descripción|  
|-----------|-----------------|  
|ExtendedAnsiSQL-0 (predeterminado)|Esta configuración no habilita las nuevas características.|  
|ExtendedAnsiSQL-1|Esta configuración habilita las nuevas características.|  
  
 El atributo también se puede establecer en un DSN a través del cuadro de diálogo **Opciones avanzadas** al configurar un DSN a través del Panel de control.  
  
 Establecer el atributo en 0 deshabilita las nuevas características; estableciendo en 1 habilita las nuevas características.  
  
 El atributo también se puede establecer mediante SQLSetConnectAttr(). El valor del atributo es 65501 y se establece en un valor SQLINTEGER de 1 o 0, como se documenta en la tabla anterior. Se puede llamar antes o después de la conexión, pero es mejor llamarlo después de conectarse debido al orden en que el controlador procesa los atributos de conexión almacenados en caché y las cadenas de conexión.
