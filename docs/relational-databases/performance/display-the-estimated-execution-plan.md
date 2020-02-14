---
title: Mostrar el plan de ejecución estimado | Microsoft Docs
ms.custom: ''
ms.date: 11/21/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
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
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4d0d5930734bb48c0914300a735f81e3ca2ced38
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "67946867"
---
# <a name="display-the-estimated-execution-plan"></a>Mostrar el plan de ejecución estimado
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  En este tema se describe cómo generar planes de ejecución estimados gráficos utilizando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Cuando se generan planes de ejecución estimados, las consultas o lotes [!INCLUDE[tsql](../../includes/tsql-md.md)] no se ejecutan. Por este motivo, un plan de ejecución estimado no contiene ninguna información en tiempo de ejecución, como métricas de uso real de recursos o advertencias en tiempo de ejecución. En su lugar, el plan de ejecución que se genera muestra el plan de ejecución de la consulta que [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] usaría con más probabilidad si se ejecutaran realmente las consultas, así como las filas estimadas de los operadores del plan.  
  
 Para utilizar esta característica, los usuarios deben tener los permisos correspondientes para ejecutar la consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] para la que se va a generar un plan de ejecución gráfico, y se les debe conceder el permiso SHOWPLAN para todas las bases de datos a las que haga referencia la consulta.  
  
## <a name="to-display-the-estimated-execution-plan-for-a-query"></a>Para mostrar el plan de ejecución estimado de una consulta  
  
1.  En la barra de herramientas, haga clic en **Consulta de motor de base de datos**. También puede abrir una consulta existente y mostrar el plan de ejecución estimado haciendo clic en el botón **Abrir archivo** de la barra de herramientas y buscando la consulta existente.  
  
2.  Especifique la consulta para la que desea mostrar el plan de ejecución estimado.  
  
3.  En el menú **Consulta** , haga clic en **Mostrar plan de ejecución estimado** o haga clic en el botón **Mostrar plan de ejecución estimado** de la barra de herramientas. El plan de ejecución estimado se muestra en la pestaña **Plan de ejecución** del panel de resultados. 

    ![Botón Plan de ejecución estimado de la barra de herramientas](../../relational-databases/performance/media/estimatedexecplantoolbar.png "Botón Plan de ejecución estimado de la barra de herramientas")    

    Para ver información adicional, sitúe el cursor del mouse (ratón) sobre los iconos de operador lógico y físico, y vea la descripción y las propiedades del operador en la información sobre herramientas que se muestra. También puede ver las propiedades del operador en la ventana Propiedades. Si las propiedades no están visibles, haga clic con el botón derecho en un operador y haga clic en **Propiedades**. Seleccione un operador para ver sus propiedades.  

    ![Clic con el botón derecho en Propiedades en el operador del plan](../../relational-databases/performance/media/planproperties.png "Clic con el botón derecho en Propiedades en el operador del plan")    
  
4.  Para cambiar la visualización del plan de ejecución, haga clic con el botón derecho en el plan de ejecución y seleccione **Acercar**, **Alejar**, **Zoom personalizado**o **Zoom para ajustar**. **Acercar** y **Alejar** permiten aumentar o reducir el plan de ejecución en incrementos fijos. **Zoom personalizado** le permite definir su propia ampliación de la visualización, como alejar hasta un 80 por ciento. **Zoom para ajustar** amplía el plan de ejecución para que se ajuste al panel de resultados. Como alternativa, use una combinación de la tecla CTRL y la rueda del mouse para activar el **zoom dinámico**.  

5.  Para navegar por la presentación del plan de ejecución, use las barras de desplazamiento horizontal y vertical, o bien **haga clic y mantenga presionado el ratón en cualquier área en blanco** del plan de ejecución, y **arrástrelo**. Otra opción es hacer clic y mantener presionado el signo más (+) de la esquina inferior derecha de la ventana del plan de ejecución para mostrar un mapa en miniatura del plan de ejecución completo.
 
> [!NOTE] 
> También puede usar [SET SHOWPLAN_XML](../../t-sql/statements/set-showplan-xml-transact-sql.md) para devolver la información del plan de ejecución de cada instrucción sin tener que ejecutarla. Si se usa en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], la pestaña *Resultados* tendrá un vínculo para abrir el plan de ejecución en un formato gráfico.   
