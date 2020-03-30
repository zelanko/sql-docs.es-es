---
title: Mostrar y guardar planes de ejecución | Microsoft Docs
ms.custom: ''
ms.date: 08/21/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Showplan results
- execution plans [SQL Server]
- queries [SQL Server], tuning
- execution plans [SQL Server], how-to topics
- SQL Server Management Studio [SQL Server], execution plans
- tuning queries [SQL Server]
ms.assetid: bcd6f094-c613-4835-ae19-4caaadb4bb17
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 11c33865990bd67e62436de3106282f873e5d0fb
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "67946834"
---
# <a name="display-and-save-execution-plans"></a>Mostrar y guardar planes de ejecución
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
En esta sección se explica cómo visualizar los planes de ejecución y cómo guardarlos en un archivo de formato XML mediante Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
Los planes de ejecución muestran de forma gráfica los métodos de recuperación de datos que usa el optimizador de consultas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los planes de ejecución representan el costo de ejecución de las instrucciones y consultas específicas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando iconos en lugar de la representación tabular que crean las instrucciones [SET SHOWPLAN_ALL](../../t-sql/statements/set-showplan-all-transact-sql.md) o [SET SHOWPLAN_TEXT](../../t-sql/statements/set-showplan-text-transact-sql.md). Este enfoque gráfico resulta útil para comprender las características de rendimiento de una consulta.  

Mientras que el optimizador de consultas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genera un único plan de ejecución, existen los planes de ejecución **estimados** y **reales**.
-  Un [plan de ejecución estimado](../../relational-databases/performance/display-the-estimated-execution-plan.md) devuelve el plan de ejecución tal como lo genera el optimizador de consultas en tiempo de compilación. Al generar el plan de ejecución estimado, realmente no se ejecuta la consulta o el lote, por lo que no contiene información en tiempo de ejecución, como las métricas de uso de recursos actual o advertencias en tiempo de ejecución. 
-  Un [plan de ejecución real](../../relational-databases/performance/display-an-actual-execution-plan.md) devuelve el plan de ejecución tal como lo genera el optimizador de consultas, mientras que las consultas y los lotes terminan de ejecutarse después. Esto incluye información en tiempo de ejecución sobre las métricas de uso de recursos y las advertencias en tiempo de ejecución.  

Para obtener más información sobre los planes de ejecución de consultas, vea la [Guía de arquitectura de procesamiento de consultas](../../relational-databases/query-processing-architecture-guide.md).
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Mostrar el plan de ejecución estimado](../../relational-databases/performance/display-the-estimated-execution-plan.md)  
  
-   [Mostrar un plan de ejecución real](../../relational-databases/performance/display-an-actual-execution-plan.md)  
  
-   [Guardar un plan de ejecución en formato XML](../../relational-databases/performance/save-an-execution-plan-in-xml-format.md)  
  
  
