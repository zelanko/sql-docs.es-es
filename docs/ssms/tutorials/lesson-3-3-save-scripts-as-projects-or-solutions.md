---
title: Guardar scripts como proyectos o soluciones | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 72dfd37f-dbe7-4d1d-bda6-7eb54c7922d3
caps.latest.revision: 33
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 5db067d5a2fe5bbf9953484c9a999ed7b1fcddae
ms.openlocfilehash: 3772efa6ab55acd4087cd47f897040f782476636
ms.contentlocale: es-es
ms.lasthandoff: 07/31/2017

---
# <a name="lesson-3-3---save-scripts-as-projects-or-solutions"></a>Lección 3.3: Guardar scripts como proyectos o soluciones
Los desarrolladores que estén familiarizados con [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio acogerán con entusiasmo el Explorador de soluciones de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Los scripts empleados en su empresa pueden agruparse en proyectos de script; estos proyectos pueden administrarse conjuntamente en forma de solución. Cuando los scripts se colocan en soluciones y proyectos de script, pueden abrirse como un grupo o guardarse juntos en un producto de control de código fuente como Visual SourceSafe. Los proyectos de script incluyen información de conexión para que los scripts se ejecuten correctamente y pueden incluir archivos que no sean de script, por ejemplo, un archivo auxiliar de texto.  
  
En la práctica siguiente, se crea un script breve que hace consultas a la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] , ubicada en una solución y un proyecto de script.  
  
## <a name="using-script-projects-and-solutions"></a>Usar soluciones y proyectos de script  
  
#### <a name="to-create-a-script-project-and-solution"></a>Para crear una solución y un proyecto de script  
  
1.  Abra [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]y conéctese a un servidor mediante el Explorador de objetos.  
  
2.  En el menú **Archivo** , seleccione **Nuevo**y haga clic en **Proyecto**. Se abrirá el cuadro de diálogo **Nuevo proyecto** .  
  
3.  En el cuadro de texto **Nombre** , escriba **StatusCheck**, haga clic en **Scripts de SQL Server** en **Plantillas**y, después, haga clic en **Aceptar** para abrir una solución y un proyecto de script nuevos.  
  
4.  En el Explorador de soluciones, haga clic con el botón derecho en **Conexiones**y, después, en **Nueva conexión**. Se abre el cuadro de diálogo **Conectar al servidor** .  
  
5.  En el cuadro de lista **Nombre del servidor** , escriba el nombre del servidor.  
  
6.  Haga clic en **Opciones**y, después, en la pestaña **Propiedades de conexión** .  
  
7.  En el cuadro **Conectar con base de datos** , examine el servidor, seleccione la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] y, después, haga clic en **Conectar**. La información de conexión que incluye la base de datos se agregará al proyecto.  
  
8.  Si la ventana Propiedades no aparece, haga clic en la conexión nueva del Explorador de soluciones y, a continuación, presione F4. Las propiedades de la conexión aparecen y muestran información relativa a la conexión, incluida la **Base de datos inicial** como [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
9. En el Explorador de soluciones, haga clic con el botón derecho en la conexión y, después, haga clic en **Nueva consulta**. Se crea una consulta denominada **SQLQuery1.sql** , que está conectada a la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] del servidor y se agrega al proyecto de script.  
  
10. En el Editor de consultas, escriba la consulta siguiente para determinar cuántas órdenes de trabajo tienen una fecha de vencimiento anterior a la fecha de inicio. Puede copiar y pegar el código de la ventana del tutorial.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT COUNT(WorkOrderID)  
    FROM Production.WorkOrder  
    WHERE DueDate < StartDate;  
  
    ```  
  
    > [!NOTE]  
    > Si necesita más espacio para escribir la consulta, presione MAYÚS+ALT+ENTRAR para cambiar al modo de pantalla completa.  
  
11. En el Explorador de soluciones, haga clic con el botón derecho en **SQLQuery1**y, después, haga clic en **Cambiar nombre**. Escriba **Check Workorders****.sql** como el nombre nuevo para la consulta y pulse ENTRAR.  
  
12. Para guardar la solución y el proyecto de script, en el menú **Archivo** , haga clic en **Guardar todo**.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
[Resumen: Soluciones y proyectos de scripts](../../tools/sql-server-management-studio/lesson-3-4-summary-solutions-and-script-projects.md)  
  
  
  

