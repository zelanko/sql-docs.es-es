---
title: Abrir, ver e imprimir un archivo de interbloqueo (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: performance
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- deadlocks [SQL Server], printing files
- deadlocks [SQL Server], opening files
- opening deadlock files
- printing deadlock files
ms.assetid: 5061b13f-2cb7-457a-b8d0-fbd437b510ab
caps.latest.revision: 14
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 971e5ae6448c26cea0c7212fac45bad5ff26e08f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="open-view-and-print-a-deadlock-file-sql-server-management-studio"></a>Abrir, ver e imprimir un archivo de interbloqueo (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Cuando [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] genera un interbloqueo, puede capturar y guardar la información de interbloqueo en un archivo. Después de guardar el archivo de interbloqueo, puede abrirlo en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para verlo o imprimirlo.  
  
## <a name="open-and-view-a-deadlock-file"></a>Abrir y ver un archivo de interbloqueo  
  
1. En el menú **Archivo** de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], seleccione **Abrir** y, a continuación, **Archivo**.  
  
2. En el cuadro de diálogo **Abrir archivo** , en **Archivos de tipo** , seleccione el tipo de archivo .xdl. Se mostrará una lista filtrada en la que solo aparecerán archivos de interbloqueo.  
  
## <a name="print-a-deadlock-file"></a>Imprimir un archivo de interbloqueo  
  
1. En el menú **Archivo** de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], seleccione **Abrir** y, a continuación, **Archivo**.  
  
2. En el cuadro de diálogo **Abrir archivo** , en **Archivos de tipo** , seleccione el tipo de archivo .xdl. Se mostrará una lista filtrada en la que solo aparecerán archivos de interbloqueo.  
  
3. Seleccione el archivo de interbloqueo que quiera imprimir y, a continuación, **Abrir**.  
  
4. En el menú **Archivo**, seleccione **Imprimir**.  
  
## <a name="see-also"></a>Vea también  
 [Guardar grafos de interbloqueo &#40;SQL Server Profiler&#41;](../../relational-databases/performance/save-deadlock-graphs-sql-server-profiler.md)  
  
  
