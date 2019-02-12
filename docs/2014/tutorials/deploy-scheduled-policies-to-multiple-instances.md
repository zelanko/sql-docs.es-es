---
title: Implementar directivas programadas en varias instancias | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: f551b8e8-3668-4ed4-852f-bae826254f4f
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 8d37dafd5501a289e45a119323eed61242707184
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56016726"
---
# <a name="deploy-scheduled-policies-to-multiple-instances"></a>Implementar directivas programadas en varias instancias
  Mediante el uso de servidores registrados puede implementar directivas programadas en servidores administrados desde una ubicación central. Puede implementar directivas programadas desde un grupo de servidores locales o desde un Servidor de administración central.  
  
 En esta tarea realizará lo siguiente:  
  
1.  Exportar las directivas programadas en la tarea anterior a una carpeta.  
  
2.  Implementar las directivas programadas en instancias de destino administradas mediante servidores registrados.  
  
 Realizará estas tareas en el equipo en el que completó las tareas anteriores de esta lección.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Esta tarea consta de los requisitos previos siguientes:  
  
-   Debe haber completado las tareas anteriores de esta lección.  
  
-   Las instancias en las que desee implementar las directivas programadas deben ejecutar [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] o una versión posterior. Automation requiere que las directivas estén almacenadas localmente, lo que no se admite en versiones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)].  
  
-   Los servidores donde desea implementar las directivas programadas deben estar registrados en servidores registrados en el el **grupos de servidores locales** o **servidores de Administración Central** nodo. Para obtener más información, vea los temas siguientes:  
  
    -   [Crear o editar un grupo de servidores &#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-or-edit-a-server-group-sql-server-management-studio.md)  
  
    -   [Registrar un servidor conectado &#40;SQL Server Management Studio&#41;](../ssms/register-servers/register-a-connected-server-sql-server-management-studio.md).  
  
    -   [Crear un servidor de administración central y un grupo de servidores &#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-a-central-management-server-and-server-group.md)  
  
### <a name="to-export-the-scheduled-policies-as-xml-files"></a>Para exportar las directivas programadas como archivos .xml  
  
1.  En el servidor donde configuró las directivas programadas en la tarea anterior, expanda **administración**, expanda **administración de directivas**y, a continuación, haga clic en **directivas**.  
  
2.  En el menú **Ver** , haga clic en **Detalles del Explorador de objetos**.  
  
3.  En el **detalles del explorador de objetos** panel, seleccione todas las prácticas recomendadas programadas las directivas que desea implementar en otros servidores mediante servidores registrados.  
  
    > [!NOTE]  
    >  Puede hacer clic en el **categoría** encabezado para ordenar las directivas por categoría.  
  
4.  Haga clic en la selección y, a continuación, haga clic en **Exportar directiva**.  
  
5.  Si ha seleccionado varias directivas para exportar, en el **Buscar carpeta** cuadro de diálogo, seleccione una carpeta de destino o cree una nueva carpeta. En esta lección, cree una nueva carpeta con la ruta de acceso **C:\Scheduled_BP_Policies**y, a continuación, haga clic en **Aceptar**.  
  
     Si ha seleccionado solamente una directiva para exportar, en el **Exportar directiva** diálogo cuadro, cree una nueva carpeta con la ruta de acceso **C:\Scheduled_BP_Policies**, haga clic en **abierto**y, a continuación, haga clic en **Guardar**.  
  
     Los archivos de directiva .xml se crean en la ubicación de carpeta.  
  
### <a name="to-deploy-the-scheduled-policies-to-servers-that-are-managed-through-registered-servers"></a>Para implementar las directivas programadas en servidores administrados mediante servidores registrados  
  
1.  En el menú **Ver** , haga clic en **Servidores registrados**.  
  
2.  Expanda **motor de base de datos**, expanda el **grupos de servidores locales** o **servidores de Administración Central**, haga clic en el nodo que desea implementar las directivas y, a continuación, Haga clic en **importar directivas**.  
  
    > [!NOTE]  
    >  Si hace doble clic en **grupos de servidores locales** o el servidor de Administración Central, las directivas se implementarán en todos los servidores administrados. Si hace clic con el botón secundario en un grupo de servidores concreto, las directivas solo se implementarán en servidores de ese grupo. Si hace clic con el botón secundario en un servidor registrado, las directivas solo se implementarán en ese servidor.  
  
3.  Junto a **archivos para importar**, haga clic en el botón de puntos suspensivos (**...** ).  
  
4.  En el **Seleccionar directiva** cuadro de diálogo, vaya a la ubicación de la carpeta donde guardó las directivas programadas. En este ejemplo, vaya a la ubicación **C:\Scheduled_BP_Policies**.  
  
5.  Seleccione las directivas que desea importar en las instancias de destino y, a continuación, haga clic en **abierto**.  
  
6.  En el **importación** cuadro de diálogo el **estado de la directiva** lista, seleccione el estado de directiva que desee. Puede elegir entre conservar el estado de directiva, habilitar, o deshabilitar las directivas al importar. Tenga en cuenta que las directivas deben estar habilitadas para ejecutarse según una programación.  
  
7.  Haga clic en **Aceptar** para importar las directivas a todas las instancias de destino.  
  
    > [!NOTE]  
    >  Si hay algún error, el **importación** cuadro de diálogo desaparece. Haga clic en el **registro** página para revisar los mensajes. Haga clic en **cancelar** para cerrar el cuadro de diálogo.  
  
8.  Para ver las directivas de una instancia de destino, conéctese a la instancia, abra el Explorador de objetos, expanda **administración**y, a continuación, expanda **directivas**. Debería ver las directivas importadas en el **directivas** nodo. Si hace doble clic en cada directiva, podrá ver el programa, o cambiar la configuración.  
  
    > [!NOTE]  
    >  Para ver los resultados de la evaluación después de la ejecución de una directiva programada, abra el registro de historial de directivas en la instancia de destino. Para abrir el registro, haga clic en **administración de directivas**y, a continuación, haga clic en **Ver historial**.  
  
## <a name="summary"></a>Resumen  
 Este tutorial le ha mostrado la forma de realizar evaluaciones tanto programadas como a petición de las directivas de prácticas recomendadas en una o varias instancias de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="next"></a>Siguiente  
 Este tutorial ha finalizado. Para volver al principio, vea [Tutorial: Evaluar las prácticas recomendadas usando administración basada en directivas](../../2014/tutorials/tutorial-evaluating-best-practices-by-using-policy-based-management.md).  
  
 Para ver una lista de [!INCLUDE[ssDE](../includes/ssde-md.md)] tutoriales, haga clic en [tutoriales del motor de base de datos](../relational-databases/database-engine-tutorials.md).  
  
## <a name="see-also"></a>Vea también  
 [Administrar servidores mediante administración basada en directivas](../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
