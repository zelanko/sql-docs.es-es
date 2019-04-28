---
title: Las instrucciones generan resultados y libre de resultado | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f357576e9e7510ae581b41a50976a34981f35109
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62861525"
---
# <a name="result-generating-and-result-free-statements"></a>Instrucciones generan resultados y libre de resultado
Las instrucciones SQL pueden dividirse flexible en las cinco categorías siguientes:  
  
-   **Como resultado la generación de conjunto de instrucciones** estas son las instrucciones SQL que generan un conjunto de resultados. Por ejemplo, un **seleccione** instrucción.  
  
-   **Instrucciones de generación de recuento de filas** estas son las instrucciones SQL que generan un recuento de filas afectadas. Por ejemplo, un **actualización** o **eliminar** instrucción.  
  
-   **Data Definition Language (DDL) instrucciones** estas son las instrucciones SQL que modifican la estructura de la base de datos. Por ejemplo, **CREATE TABLE** o **DROP INDEX**.  
  
-   **Instrucciones de cambio de contexto** estas son las instrucciones SQL que cambian el contexto de una base de datos. Por ejemplo, el **USE** y **establecer** instrucciones en SQL Server.  
  
-   **Instrucciones administrativas** son instrucciones SQL usadas para fines administrativos en una base de datos. Por ejemplo, **GRANT** y **REVOCAR**.  
  
 Las instrucciones SQL en las dos primeras categorías se conocen colectivamente como *generan instrucciones*. Instrucciones SQL en las tres categorías este últimas se conocen colectivamente como *libre de resultado instrucciones*. ODBC define la semántica de los lotes que incluyen solo generan instrucciones. Estas semánticas varían ampliamente y, por tanto, son específicas del origen de datos. Por ejemplo, el controlador de SQL Server no admite la eliminación de un objeto y, a continuación, que hace referencia a o volver a crear el mismo objeto en el mismo lote. Por lo tanto, el término *batch* que se usa en este manual se refiere solo a los lotes de generan instrucciones.
