---
title: SQLTables (controlador ODBC de Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLTables function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 69e2a038-5def-423f-91aa-8756e069dd2a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e134b2870c4506e725f2900b83d1118e42b55d15
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63219120"
---
# <a name="sqltables-visual-foxpro-odbc-driver"></a>SQLTables (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte técnico: Completo  
  
 Conformidad de la API de ODBC: Nivel 1  
  
 Devuelve la lista de nombres de tabla especificado por el parámetro en el **SQLTables** instrucción. Si se especifica ningún parámetro, devuelve los nombres de tabla que se almacenan en el origen de datos actual. El controlador devuelve la información como un conjunto de resultados.  
  
 Las llamadas de tipo de enumeración no reciben una entrada de conjunto de resultados para las vistas remotas ni vistas con parámetros locales. Sin embargo, una llamada a **SQLTables** con una única tabla especificador de nombre encontrar una coincidencia para una vista de este tipo si está presente con ese nombre; Esto permite a la API que se usará para comprobar si hay conflictos de nombre antes de crear una nueva tabla.  
  
> [!NOTE]  
>  Marca la diferencia entre el controlador ODBC de Visual FoxPro [tablas de base de datos](../../odbc/microsoft/visual-foxpro-terminology.md) y [libre tablas](../../odbc/microsoft/visual-foxpro-terminology.md), incluso cuando ambos tipos de tablas se almacenan en el mismo directorio en el sistema. Si el origen de datos es un directorio de tablas libres, el controlador ODBC de Visual FoxPro no catálogo o devolver los nombres de todas las tablas que están asociados con una base de datos.  
  
 Para obtener más información, consulte [SQLTables](../../odbc/reference/syntax/sqltables-function.md) en el *referencia del programador de ODBC*.
