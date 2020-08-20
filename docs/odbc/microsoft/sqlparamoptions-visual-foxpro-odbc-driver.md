---
description: SQLParamOptions (controlador ODBC de Visual FoxPro)
title: SQLParamOptions (controlador ODBC de Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLParamOptions function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 7f94a6e2-9c34-405c-b2b0-304d94269715
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e40af7f0bb03c0b5245717880e67e72b38559aed
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500198"
---
# <a name="sqlparamoptions-visual-foxpro-odbc-driver"></a>SQLParamOptions (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Compatibilidad: completa  
  
 Conformidad con la API de ODBC: nivel 1  
  
 Permite a una aplicación especificar varios valores para el conjunto de parámetros asignados por [SQLBindParameter](../../odbc/microsoft/sqlbindparameter-visual-foxpro-odbc-driver.md). La capacidad de especificar varios valores para un conjunto de parámetros resulta útil para las inserciones masivas y otros trabajos que requieren que el origen de datos procese la misma instrucción SQL varias veces con varios valores de parámetro. Por ejemplo, una aplicación puede especificar tres conjuntos de valores para el conjunto de parámetros asociados a una instrucción **Insert** y, a continuación, ejecutar la instrucción **Insert** una vez para realizar las tres operaciones de inserción.  
  
 Para obtener más información, vea [SQLParamOptions](../../odbc/reference/syntax/sqlparamoptions-function.md) en la *Referencia del programador de ODBC*.
