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
manager: craigg
ms.openlocfilehash: 80a86ef188796883e76c6d5f6149a3e40afd341b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63128004"
---
# <a name="enabling-new-data-types-by-setting-extendedansisql"></a>Habilitar a nuevos tipos de datos estableciendo ExtendedAnsiSQL
Dos nuevos tipos de datos están disponibles en las bases de datos de Jet 4.0 cuando se activa la marca ExtendedAnsiSQL: SQL_DECIMAL y SQL_NUMERIC. La precisión y escala predeterminadas son 18 y 0, respectivamente. Acceso a través de ODBC que se escribe como SQL_DECIMAL o SQL_NUMERIC de datos se asignarán a Microsoft Jet Decimal en lugar de moneda.  
  
 Cuando la marca ExtendedAnsiSQL está desactivada, no se puede crear tablas con tipos decimales o numéricos, y estos tipos no aparecerán en SQLGetTypeInfo(). Sin embargo, si la tabla contiene los nuevos tipos de datos, puede usar con los tipos de datos correcto.
