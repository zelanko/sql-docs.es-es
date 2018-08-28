---
title: Abrir, ver e imprimir un archivo de interbloqueo (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: performance
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ef0c53c294a653d433242546c5f4d4b69a2dea75
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43070597"
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
  
  
