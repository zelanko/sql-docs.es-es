---
title: Apertura, consulta e impresión de un archivo de interbloqueo (SSMS)
ms.custom: seo-dt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- deadlocks [SQL Server], printing files
- deadlocks [SQL Server], opening files
- opening deadlock files
- printing deadlock files
ms.assetid: 5061b13f-2cb7-457a-b8d0-fbd437b510ab
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c305d9fd08ffcdd1c4b66d90d834c8f0fb6dead5
ms.sourcegitcommit: f018eb3caedabfcde553f9a5fc9c3e381c563f1a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2019
ms.locfileid: "74165759"
---
# <a name="open-view-and-print-a-deadlock-file-in-sql-server-management-studio-ssms"></a>Apertura, consulta e impresión de un archivo de interbloqueo en SQL Server Management Studio (SSMS)

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
  
## <a name="see-also"></a>Consulte también  
 [Guardar grafos de interbloqueo &#40;SQL Server Profiler&#41;](../../relational-databases/performance/save-deadlock-graphs-sql-server-profiler.md)  
  
  
