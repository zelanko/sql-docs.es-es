---
title: Guardar scripts como proyectos o soluciones | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 72dfd37f-dbe7-4d1d-bda6-7eb54c7922d3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6d17dd44f597d7b3ddfce574670e9e6bfd55f908
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62753051"
---
# <a name="save-scripts-as-projects-or-solutions"></a>Guardar scripts como proyectos o soluciones
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
    >  Si necesita más espacio para escribir la consulta, presione MAYÚS+ALT+ENTRAR para cambiar al modo de pantalla completa.  
  
11. En el Explorador de soluciones, haga clic con el botón derecho en **SQLQuery1**y, después, haga clic en **Cambiar nombre**. Escriba **checkss. SQL** como el nuevo nombre de la consulta y presione Entrar.  
  
12. Para guardar la solución y el proyecto de script, en el menú **Archivo** , haga clic en **Guardar todo**.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Resumen: Soluciones y proyectos de scripts](lesson-3-4-summary-solutions-and-script-projects.md)  
  
  
