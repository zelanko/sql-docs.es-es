---
title: "Crear una categoría de trabajo | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Agent jobs, categories
- jobs [SQL Server Agent], categories
- categories [SQL Server Agent jobs]
ms.assetid: e24a6d38-d231-4f64-ab89-2d1ef6f5792c
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 960865a8bb263a2089dc51a75304e3e6e40b85bf
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="create-a-job-category"></a>Crear una categoría de trabajo
En este tema se describe cómo crear una categoría de trabajo en [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)], [!INCLUDE[tsql](../../includes/tsql_md.md)] u Objetos de administración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] .  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] El Agente proporciona categorías de trabajo integradas a las que puede asignar trabajos, o bien puede crear una categoría de trabajo y asignarle trabajos. Las categorías de trabajo le ayudan a organizar los trabajos para poder filtrarlos y agruparlos fácilmente. Por ejemplo, puede organizar todos los trabajos de copia de seguridad de las bases de datos en la categoría Mantenimiento de bases de datos. También puede crear sus propias categorías.  
  
**En este tema**  
  
-   **Antes de empezar:**  
  
    [Limitaciones y restricciones](#Restrictions)  
  
    [Seguridad](#Security)  
  
-   **Para crear una categoría de trabajo, utilizando:**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [objetos de administración de SQL Server](#SMO)  
  
## <a name="BeforeYouBegin"></a>Antes de comenzar  
  
### <a name="Restrictions"></a>Limitaciones y restricciones  
Las categorías multiservidor existen solo en los servidores maestros. Solo hay una categoría de trabajo predeterminada disponible en un servidor maestro: [**Sin categoría (Multiservidor)**]. Cuando se descarga un trabajo multiservidor, su categoría se cambia a **Trabajos del servidor principal** en el servidor de destino.  
  
### <a name="Security"></a>Seguridad  
Para obtener información detallada, vea [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMS"></a>Usar SQL Server Management Studio  
  
#### <a name="to-create-a-job-category"></a>Para crear una categoría de trabajo  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor en el que desea crear una categoría de trabajo.  
  
2.  Haga clic en el signo más para expandir **Agente SQL Server**.  
  
3.  Haga clic con el botón derecho en la carpeta **Trabajos** y seleccione **Administrar categorías de trabajos**.  
  
4.  En el cuadro de diálogo **Administrar categorías de trabajo***nombre_servidor* , haga clic en **Agregar**.  
  
5.  En el nuevo cuadro de diálogo, en el cuadro **Nombre** , especifique un nombre para la nueva categoría de trabajo.  
  
6.  Active la casilla **Mostrar todos los trabajos** . Seleccione uno o varios trabajos para la nueva categoría activando las casillas correspondientes a los trabajos.  
  
7.  Haga clic en **Aceptar**.  
  
8.  En el cuadro de diálogo **Administrar categorías de trabajo***server_name* , haga clic en **Actualizar** para asegurarse de que la nueva categoría de trabajo esté activa. Si todo se busca conforme a lo esperado, cierre este cuadro de diálogo.  
  
Para más información sobre estos cuadros de diálogo, consulte [Categorías de trabajo - Administrar categorías de trabajo](../../ssms/agent/job-categories-manage-job-categories.md) y [Propiedades de categorías de trabajo - Nueva categoría de trabajo](../../ssms/agent/job-categories-properties-new-job-category.md).  
  
## <a name="TSQL"></a>Usar Transact-SQL  
  
#### <a name="to-create-a-job-category"></a>Para crear una categoría de trabajo  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    -- creates a local job category named AdminJobs   
    USE msdb ;  
    GO  
    EXEC dbo.sp_add_category  
        @class=N'JOB',  
        @type=N'LOCAL',  
        @name=N'AdminJobs' ;  
    GO  
    ```  
  
Para más información, consulte [sp_add_category (Transact-SQL)](http://msdn.microsoft.com/en-us/6cca32cd-d941-4378-aed6-a7c90cb7520a).  
  
## <a name="SMO"></a>Usar Objetos de administración de SQL Server  
**Para crear una categoría de trabajo**  
  
Llame a la clase **JobCategory** mediante un lenguaje de programación de su elección, como Visual Basic, Visual C# o PowerShell. Para el código de ejemplo, consulte [Programar tareas administrativas automáticas en el Agente SQL Server](http://msdn.microsoft.com/en-us/900242ad-d6a2-48e9-8a1b-f0eea4413c16).  
  

