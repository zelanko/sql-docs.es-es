---
description: Instrucciones generan resultados y libre de resultado
title: Instrucciones de generación de resultados y sin resultados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result-generating statements [ODBC]
- batches [ODBC], result-generating statements
- batches [ODBC], result-free statements
- SQL statements [ODBC], batches
- result-free statements [ODBC]
ms.assetid: 2f3475d1-3999-4dd8-aba2-a6e1299c95f8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 31484578a544bb6f2cf3f8e37ffbac4674a7f055
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429117"
---
# <a name="result-generating-and-result-free-statements"></a>Instrucciones generan resultados y libre de resultado
Las instrucciones SQL se pueden dividir de forma flexible en las cinco categorías siguientes:  
  
-   **Conjunto de resultados: generar instrucciones** Se trata de instrucciones SQL que generan un conjunto de resultados. Por ejemplo, una instrucción **Select** .  
  
-   **Recuento de filas-generar instrucciones** Se trata de instrucciones SQL que generan un recuento de filas afectadas. Por ejemplo, una instrucción **Update** o **Delete** .  
  
-   **Instrucciones del lenguaje de definición de datos (DDL)** Se trata de instrucciones SQL que modifican la estructura de la base de datos. Por ejemplo, **CREATE TABLE** o **Drop index**.  
  
-   **Instrucciones de cambio de contexto** Se trata de instrucciones SQL que cambian el contexto de una base de datos. Por ejemplo, las instrucciones **use** y **set** en SQL Server.  
  
-   **Instrucciones administrativas** Se trata de instrucciones SQL que se usan para fines administrativos en una base de datos. Por ejemplo, **Grant** y **REVOKE**.  
  
 Las instrucciones SQL de las dos primeras categorías se conocen colectivamente como *instrucciones de generación de resultados*. Las instrucciones SQL en las tres últimas categorías se conocen colectivamente como *instrucciones sin resultados*. ODBC define la semántica de los lotes que solo incluyen instrucciones que generan resultados. Estas semánticas varían considerablemente y, por lo tanto, son específicas del origen de datos. Por ejemplo, el controlador SQL Server no permite quitar un objeto y, a continuación, hacer referencia al mismo objeto o volver a crearlo en el mismo lote. Por lo tanto, el término *batch* tal como se usa en este manual solo se refiere a los lotes de instrucciones de generación de resultados.
