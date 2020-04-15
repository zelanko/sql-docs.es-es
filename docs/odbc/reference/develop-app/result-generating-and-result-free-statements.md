---
title: Declaraciones de generación de resultados y sin resultados Microsoft Docs
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
ms.openlocfilehash: fc94aabd7982fba5879519573980db03b1857ef6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300095"
---
# <a name="result-generating-and-result-free-statements"></a>Instrucciones generan resultados y libre de resultado
Las instrucciones SQL se pueden dividir libremente en las siguientes cinco categorías:  
  
-   **Declaraciones de generación de conjuntos de resultados** Se trata de instrucciones SQL que generan un conjunto de resultados. Por ejemplo, una instrucción **SELECT.**  
  
-   **Declaraciones de generación de recuento de filas** Se trata de instrucciones SQL que generan un recuento de filas afectadas. Por ejemplo, una instrucción **UPDATE** o **DELETE.**  
  
-   Declaraciones de lenguaje de definición de **datos (DDL)** Se trata de instrucciones SQL que modifican la estructura de la base de datos. Por ejemplo, **CREATE TABLE** o **DROP INDEX**.  
  
-   **Declaraciones de cambio de contexto** Se trata de instrucciones SQL que cambian el contexto de una base de datos. Por ejemplo, las instrucciones **USE** y **SET** en SQL Server.  
  
-   **Declaraciones Administrativas** Se trata de instrucciones SQL que se usan con fines administrativos en una base de datos. Por ejemplo, **GRANT** y **REVOKE**.  
  
 Las instrucciones SQL de las dos primeras categorías se conocen colectivamente como *instrucciones generadoras de resultados.* Las instrucciones SQL de las tres últimas categorías se conocen colectivamente como *instrucciones sin resultados.* ODBC define la semántica de lotes que incluyen solo instrucciones de generación de resultados. Estas semánticas varían ampliamente y, por lo tanto, son específicas del origen de datos. Por ejemplo, el controlador de SQL ServerSQL Server no admite quitar un objeto y, a continuación, hacer referencia o volver a crear el mismo objeto en el mismo lote. Por lo tanto, el término *lote* tal como se usa en este manual se refiere únicamente a lotes de instrucciones generadoras de resultados.
