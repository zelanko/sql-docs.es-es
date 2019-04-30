---
title: Mostrar un plan de ejecución real | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- displaying execution plans
- actual execution plans
- viewing execution plans
- execution plans [SQL Server], displaying
ms.assetid: 9e583a18-5f4a-4054-bfe1-4b2a76630db6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9403e6e2cf1c341780a06bbdff1c5f38685dd34a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63150970"
---
# <a name="display-an-actual-execution-plan"></a>Mostrar un plan de ejecución real
  En este tema se describe cómo generar planes de ejecución gráficos reales mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Cuando se generan planes de ejecución reales, se ejecutan los lotes o consultas [!INCLUDE[tsql](../../includes/tsql-md.md)] . El plan de ejecución que se ha generado muestra el plan de ejecución de consultas real que utiliza el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] para ejecutar las consultas.  
  
 Para utilizar esta característica, los usuarios deben tener los permisos apropiados para ejecutar las consultas [!INCLUDE[tsql](../../includes/tsql-md.md)] para las que se genera un plan de ejecución gráfico y deben tener concedido el permiso SHOWPLAN para todas las bases de datos a las que hace referencia la consulta.  
  
### <a name="to-include-an-execution-plan-for-a-query-during-execution"></a>Para incluir un plan de ejecución para una consulta durante la ejecución  
  
1.  En la barra de herramientas de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , haga clic en **Consulta de motor de base de datos**. También puede abrir una consulta existente y mostrar el plan de ejecución estimado haciendo clic en el botón **Abrir archivo** de la barra de herramientas y buscando la consulta existente.  
  
2.  Especifique la consulta para la que desee mostrar el plan de ejecución real.  
  
3.  En el menú **Consultar** , haga clic en **Incluir plan de ejecución real** o en el botón **Incluir plan de ejecución real** de la barra de herramientas.  
  
4.  Ejecute la consulta haciendo clic en el botón **Ejecutar** de la barra de herramientas. El plan utilizado por el optimizador de consultas se muestra en la pestaña **Plan de ejecución** del panel de resultados. Coloque el mouse (ratón) sobre los operadores lógicos y físicos para ver la descripción y las propiedades de los operadores en la información sobre herramientas que se muestra.  
  
     También puede ver las propiedades del operador en la ventana Propiedades. Si las propiedades no están visibles, haga clic con el botón derecho en un operador y seleccione **Propiedades**. Seleccione un operador para ver sus propiedades.  
  
5.  Para cambiar la visualización del plan de ejecución, haga clic con el botón derecho en el plan de ejecución y seleccione **Acercar**, **Alejar**, **Zoom personalizado**o **Zoom para ajustar**. **Acercar** y **Alejar** permiten acercarse o alejarse del plan de ejecución, mientras que **Zoom personalizado** permite definir su propio zoom, como por ejemplo un 80 por ciento de zoom. **Zoom para ajustar** amplía el plan de ejecución para que se ajuste al panel de resultados.  
  
  
