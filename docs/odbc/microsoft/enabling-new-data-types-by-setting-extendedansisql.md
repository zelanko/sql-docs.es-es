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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68031120"
---
# <a name="enabling-new-data-types-by-setting-extendedansisql"></a>Habilitar a nuevos tipos de datos estableciendo ExtendedAnsiSQL
Dos nuevos tipos de datos están disponibles en las bases de datos de Jet 4.0 cuando se activa la marca ExtendedAnsiSQL: SQL_DECIMAL y SQL_NUMERIC. La precisión y escala predeterminadas son 18 y 0, respectivamente. Acceso a través de ODBC que se escribe como SQL_DECIMAL o SQL_NUMERIC de datos se asignarán a Microsoft Jet Decimal en lugar de moneda.  
  
 Cuando la marca ExtendedAnsiSQL está desactivada, no se puede crear tablas con tipos decimales o numéricos, y estos tipos no aparecerán en SQLGetTypeInfo(). Sin embargo, si la tabla contiene los nuevos tipos de datos, puede usar con los tipos de datos correcto.
