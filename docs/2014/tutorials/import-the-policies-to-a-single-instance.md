---
title: Importar las directivas a una sola instancia | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: bc5bcd87-663f-41d9-bb7b-b3e083cd63df
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 410f3a317a9d3ad2f8cab52d9f57fd4a63c1c36c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62865104"
---
# <a name="import-the-policies-to-a-single-instance"></a>Importar las directivas a una instancia única
  En esta tarea, importará las directivas de prácticas recomendadas que desea programar en la administración basada en directivas en una única instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="prerequisites"></a>Requisitos previos  
 Debe realizar este procedimiento en un servidor que ejecute [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] o una versión posterior.  
  
### <a name="import-the-best-practices-policies-for-the-database-engine"></a>Importar las directivas de prácticas recomendadas para el Motor de base de datos  
  
1.  Inicie [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]y después conéctese a [!INCLUDE[ssDE](../includes/ssde-md.md)].  
  
2.  En el Explorador de objetos, expanda **Administración**y, a continuación, expanda **Administración de directivas**.  
  
3.  Haga clic con el botón secundario en **Directivas**y, a continuación, haga clic en **Importar directiva**.  
  
4.  En el **importar** cuadro de diálogo, junto a la **archivos para importar** cuadro, haga clic en el botón de puntos suspensivos (**...** ) botón.  
  
5.  En la lista **Buscar en** , busque la carpeta siguiente, que contiene las directivas de prácticas recomendadas:  
  
     **C:\Program archivos (x86) \Microsoft SQL Server\110\Tools\Policies\DatabaseEngine\1033**  
  
    > [!NOTE]  
    >  La ruta de acceso puede variar según dónde instalara los archivos de programa de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , si ejecuta un sistema operativo de 32 bits o de 64 bits y el identificador de idioma.  
  
6.  En el cuadro de diálogo **Seleccionar directiva** , seleccione uno o más archivos de directivas.  
  
     Para seleccionar archivos no consecutivos, haga clic en uno, mantenga presionada la tecla CTRL y, a continuación, haga clic en cada archivo adicional. Para seleccionar archivos consecutivos, haga clic en el primero de la secuencia, mantenga presionada la tecla MAYÚS y, a continuación, haga clic en el último archivo.  
  
7.  Cuando termine de seleccionar los archivos, haga clic en **Abrir**.  
  
8.  En el cuadro de diálogo **Importar** , asegúrese de que la lista **Estado de directiva** está establecida en **Conservar el estado de las directivas al importar** (el valor predeterminado) y, a continuación, haga clic en **Aceptar**.  
  
     Las directivas se importan en el nodo **Directivas** en **Administración de directivas**. De forma predeterminada, las directivas importadas se establecen en el modo de evaluación "A petición".  
  
## <a name="next-steps"></a>Pasos siguientes  
 [Programar las directivas](../../2014/tutorials/schedule-the-policies.md)  
  
  
