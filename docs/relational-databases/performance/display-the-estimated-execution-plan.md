---
title: "Mostrar el plan de ejecución estimado | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 26
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ab88419f449c00dae258d7cf101d08df56f26d2b
ms.lasthandoff: 04/11/2017

---
# <a name="display-the-estimated-execution-plan"></a>Mostrar el plan de ejecución estimado
  En este tema se describe cómo generar planes de ejecución estimados gráficos utilizando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Cuando se generan planes de ejecución estimados, las consultas o lotes [!INCLUDE[tsql](../../includes/tsql-md.md)] no se ejecutan. En su lugar, el plan de ejecución que se genera muestra el plan de ejecución de la consulta que el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] utilizaría con más probabilidad si se ejecutaran realmente las consultas.  
  
 Para utilizar esta característica, los usuarios deben tener los permisos correspondientes para ejecutar la consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] para la que se va a generar un plan de ejecución gráfico, y se les debe conceder el permiso SHOWPLAN para todas las bases de datos a las que haga referencia la consulta.  
  
### <a name="to-display-the-estimated-execution-plan-for-a-query"></a>Para mostrar el plan de ejecución estimado de una consulta  
  
1.  En la barra de herramientas, haga clic en **Consulta de motor de base de datos**. También puede abrir una consulta existente y mostrar el plan de ejecución estimado haciendo clic en el botón **Abrir archivo** de la barra de herramientas y buscando la consulta existente.  
  
2.  Especifique la consulta para la que desea mostrar el plan de ejecución estimado.  
  
3.  En el menú **Consulta** , haga clic en **Mostrar plan de ejecución estimado** o haga clic en el botón **Mostrar plan de ejecución estimado** de la barra de herramientas. El plan de ejecución estimado se muestra en la pestaña **Plan de ejecución** del panel de resultados. Para ver información adicional, sitúe el cursor del mouse (ratón) sobre los iconos de operador lógico y físico, y vea la descripción y las propiedades del operador en la información sobre herramientas que se muestra. También puede ver las propiedades del operador en la ventana Propiedades. Si las propiedades no están visibles, haga clic con el botón derecho en un operador y haga clic en **Propiedades**. Seleccione un operador para ver sus propiedades.  
  
4.  Para cambiar la visualización del plan de ejecución, haga clic con el botón derecho en el plan de ejecución y seleccione **Acercar**, **Alejar**, **Zoom personalizado**o **Zoom para ajustar**. **Acercar** y **Alejar** permiten aumentar o reducir el plan de ejecución en incrementos fijos. **Zoom personalizado** le permite definir su propia ampliación de la visualización, como alejar hasta un 80 por ciento. **Zoom para ajustar** amplía el plan de ejecución para que se ajuste al panel de resultados.  
  
  
