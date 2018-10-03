---
title: Mostrar el plan de ejecución estimado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- zoom [SQL Server]
- estimated execution plan [SQL Server]
- displaying execution plans
- viewing execution plans
- execution plans [SQL Server], displaying
- customizing execution plan display [SQL Server]
- modifying execution plan display
- custom zoom [SQL Server]
ms.assetid: e94aa576-4c0c-4c54-ad05-6c3432cc615b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: bcdd937dcd0bde4359c03fa5735947668e88fceb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48136895"
---
# <a name="display-the-estimated-execution-plan"></a>Mostrar el plan de ejecución estimado
  En este tema se describe cómo generar planes de ejecución estimados gráficos utilizando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Cuando se generan planes de ejecución estimados, las consultas o lotes [!INCLUDE[tsql](../../includes/tsql-md.md)] no se ejecutan. En su lugar, el plan de ejecución que se genera muestra el plan de ejecución de la consulta que el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] utilizaría con más probabilidad si se ejecutaran realmente las consultas.  
  
 Para utilizar esta característica, los usuarios deben tener los permisos correspondientes para ejecutar la consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] para la que se va a generar un plan de ejecución gráfico, y se les debe conceder el permiso SHOWPLAN para todas las bases de datos a las que haga referencia la consulta.  
  
### <a name="to-display-the-estimated-execution-plan-for-a-query"></a>Para mostrar el plan de ejecución estimado de una consulta  
  
1.  En la barra de herramientas, haga clic en **Consulta de motor de base de datos**. También puede abrir una consulta existente y mostrar el plan de ejecución estimado haciendo clic en el botón **Abrir archivo** de la barra de herramientas y buscando la consulta existente.  
  
2.  Especifique la consulta para la que desea mostrar el plan de ejecución estimado.  
  
3.  En el menú **Consulta** , haga clic en **Mostrar plan de ejecución estimado** o haga clic en el botón **Mostrar plan de ejecución estimado** de la barra de herramientas. El plan de ejecución estimado se muestra en la pestaña **Plan de ejecución** del panel de resultados. Para ver información adicional, sitúe el cursor del mouse (ratón) sobre los iconos de operador lógico y físico, y vea la descripción y las propiedades del operador en la información sobre herramientas que se muestra. También puede ver las propiedades del operador en la ventana Propiedades. Si las propiedades no están visibles, haga clic con el botón derecho en un operador y haga clic en **Propiedades**. Seleccione un operador para ver sus propiedades.  
  
4.  Para cambiar la visualización del plan de ejecución, haga clic con el botón derecho en el plan de ejecución y seleccione **Acercar**, **Alejar**, **Zoom personalizado**o **Zoom para ajustar**. **Acercar** y **Alejar** permiten aumentar o reducir el plan de ejecución en incrementos fijos. **Zoom personalizado** le permite definir su propia ampliación de la visualización, como alejar hasta un 80 por ciento. **Zoom para ajustar** amplía el plan de ejecución para que se ajuste al panel de resultados.  
  
  
