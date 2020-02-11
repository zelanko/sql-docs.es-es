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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68185811"
---
# <a name="deploy-scheduled-policies-to-multiple-instances"></a>Implementar directivas programadas en varias instancias
  Mediante el uso de servidores registrados puede implementar directivas programadas en servidores administrados desde una ubicación central. Puede implementar directivas programadas desde un grupo de servidores locales o desde un Servidor de administración central.  
  
 En esta tarea realizará lo siguiente:  
  
1.  Exportar las directivas programadas en la tarea anterior a una carpeta.  
  
2.  Implementar las directivas programadas en instancias de destino administradas mediante servidores registrados.  
  
 Realizará estas tareas en el equipo en el que completó las tareas anteriores de esta lección.  
  
## <a name="prerequisites"></a>Prerequisites  
 Esta tarea consta de los requisitos previos siguientes:  
  
-   Debe haber completado las tareas anteriores de esta lección.  
  
-   Las instancias en las que desee implementar las directivas programadas deben ejecutar [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] o una versión posterior. Automation requiere que las directivas estén almacenadas localmente, lo que no se admite en versiones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)].  
  
-   Los servidores en los que desea implementar las directivas programadas deben estar registrados en servidores registrados en el nodo grupos de servidores **locales** o **servidores de administración central** . Para obtener más información, vea los temas siguientes:  
  
    -   [Crear o editar un grupo de servidores &#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-or-edit-a-server-group-sql-server-management-studio.md)  
  
    -   [Registra un servidor conectado &#40;SQL Server Management Studio&#41;](../ssms/register-servers/register-a-connected-server-sql-server-management-studio.md).  
  
    -   [Crear un servidor de administración central y un grupo de servidores &#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-a-central-management-server-and-server-group.md)  
  
### <a name="to-export-the-scheduled-policies-as-xml-files"></a>Para exportar las directivas programadas como archivos .xml  
  
1.  En el servidor donde configuró las directivas programadas en la tarea anterior, expanda **Administración**, expanda **Administración de directivas**y, a continuación, haga clic en **directivas**.  
  
2.  En el menú **Ver** , haga clic en **Detalles del Explorador de objetos**.  
  
3.  En el panel de **detalles del explorador de objetos** , seleccione todas las directivas de prácticas recomendadas programadas que desee implementar en otros servidores mediante servidores registrados.  
  
    > [!NOTE]  
    >  Puede hacer clic en el encabezado **categoría** para ordenar las directivas por categoría.  
  
4.  Haga clic con el botón secundario en la selección y luego haga clic en **exportar Directiva**.  
  
5.  Si seleccionó varias directivas para exportar, en el cuadro de diálogo **Buscar carpeta** , seleccione una carpeta de destino o cree una nueva carpeta. En esta lección, cree una nueva carpeta con la ruta de acceso **c:\ Scheduled_BP_Policies**y, a continuación, haga clic en **Aceptar**.  
  
     Si solo ha seleccionado una directiva para exportar, en el cuadro de diálogo **exportar Directiva** , cree una nueva carpeta con la ruta de acceso **c:\ Scheduled_BP_Policies**, haga clic en **abrir**y, a continuación, haga clic en **Guardar**.  
  
     Los archivos de directiva .xml se crean en la ubicación de carpeta.  
  
### <a name="to-deploy-the-scheduled-policies-to-servers-that-are-managed-through-registered-servers"></a>Para implementar las directivas programadas en servidores administrados mediante servidores registrados  
  
1.  En el menú **Ver** , haga clic en **Servidores registrados**.  
  
2.  Expanda **motor de base de datos**, expanda grupos de servidores **locales** o **servidores de administración central**, haga clic con el botón secundario en el nodo en el que desea implementar las directivas y, a continuación, haga clic en **importar directivas**.  
  
    > [!NOTE]  
    >  Si hace clic con el botón secundario en **grupos de servidores locales** o en el propio servidor de administración central, las directivas se implementarán en todos los servidores administrados. Si hace clic con el botón secundario en un grupo de servidores concreto, las directivas solo se implementarán en servidores de ese grupo. Si hace clic con el botón secundario en un servidor registrado, las directivas solo se implementarán en ese servidor.  
  
3.  Junto a **archivos para importar**, haga clic en el botón de puntos suspensivos (**...**).  
  
4.  En el cuadro de diálogo **seleccionar Directiva** , busque la ubicación de la carpeta en la que guardó las directivas programadas. En este ejemplo, vaya a la ubicación **c:\ Scheduled_BP_Policies**.  
  
5.  Seleccione las directivas que desea importar a las instancias de destino y, a continuación, haga clic en **abrir**.  
  
6.  En el cuadro de diálogo **importar** , en la lista Estado de la **Directiva** , seleccione el estado de directiva deseado. Puede elegir entre conservar el estado de directiva, habilitar, o deshabilitar las directivas al importar. Tenga en cuenta que las directivas deben estar habilitadas para ejecutarse según una programación.  
  
7.  Haga clic en **Aceptar** para importar las directivas a todas las instancias de destino.  
  
    > [!NOTE]  
    >  Si hay algún error, el cuadro de diálogo **importar** no desaparecerá. Haga clic en la página **registro** para revisar los mensajes. Haga clic en **Cancelar** para cerrar el cuadro de diálogo.  
  
8.  Para ver las directivas de una instancia de destino, conéctese a la instancia, abra Explorador de objetos, expanda **Administración**y, a continuación, expanda **directivas**. Debería ver las directivas importadas en el nodo **directivas** . Si hace doble clic en cada directiva, podrá ver el programa, o cambiar la configuración.  
  
    > [!NOTE]  
    >  Para ver los resultados de la evaluación después de la ejecución de una directiva programada, abra el registro de historial de directivas en la instancia de destino. Para abrir el registro, haga clic con el botón secundario en **Administración de directivas**y, a continuación, haga clic en **Ver historial**.  
  
## <a name="summary"></a>Resumen  
 Este tutorial le ha mostrado la forma de realizar evaluaciones tanto programadas como a petición de las directivas de prácticas recomendadas en una o varias instancias de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="next"></a>Pasos siguientes  
 Este tutorial ha finalizado. Para volver al inicio, vea [Tutorial: evaluar las prácticas recomendadas mediante la administración basada en directivas](../../2014/tutorials/tutorial-evaluating-best-practices-by-using-policy-based-management.md).  
  
 Para ver una lista de [!INCLUDE[ssDE](../includes/ssde-md.md)] los tutoriales, haga clic en [motor de base de datos tutoriales](../relational-databases/database-engine-tutorials.md).  
  
## <a name="see-also"></a>Consulte también  
 [Administrar servidores mediante administración basada en directivas](../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
