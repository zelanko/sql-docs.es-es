---
title: Habilitar nuevos tipos de datos estableciendo ExtendedAnsiSQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- extendedANSISQL [ODBC], enabling new data types
ms.assetid: f2865543-7fff-44fa-9a6a-968bec33acdc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 88f11adcab09dbe6964bfd67a944912fc185bccb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68031120"
---
# <a name="enabling-new-data-types-by-setting-extendedansisql"></a>Habilitar a nuevos tipos de datos estableciendo ExtendedAnsiSQL
Dos nuevos tipos de datos están disponibles en las bases de datos Jet 4,0 cuando la marca ExtendedAnsiSQL está activada: SQL_DECIMAL y SQL_NUMERIC. La precisión y la escala predeterminadas son 18 y 0, respectivamente. Los datos a los que se obtiene acceso a través de ODBC que se escriben como SQL_DECIMAL o SQL_NUMERIC se asignarán a Microsoft Jet decimal en lugar de a la moneda.  
  
 Cuando se desactiva la marca ExtendedAnsiSQL, no se pueden crear tablas con tipos decimales o numéricos, y estos tipos no aparecerán en SQLGetTypeInfo (). Sin embargo, si la tabla contiene los nuevos tipos de datos, se pueden usar con los tipos de datos correctos.
