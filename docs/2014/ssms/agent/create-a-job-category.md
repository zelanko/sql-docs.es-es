---
title: Crear una categoría de trabajo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, categories
- jobs [SQL Server Agent], categories
- categories [SQL Server Agent jobs]
ms.assetid: e24a6d38-d231-4f64-ab89-2d1ef6f5792c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d904f82c793acf6135f600e1ed5392bda96e1bb8
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2019
ms.locfileid: "54130855"
---
# <a name="create-a-job-category"></a>Crear una categoría de trabajo
  En este tema se describe cómo crear una categoría de trabajo en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] u Objetos de administración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] El Agente proporciona categorías de trabajo integradas a las que puede asignar trabajos, o bien puede crear una categoría de trabajo y asignarle trabajos. Las categorías de trabajo le ayudan a organizar los trabajos para poder filtrarlos y agruparlos fácilmente. Por ejemplo, puede organizar todos los trabajos de copia de seguridad de las bases de datos en la categoría Mantenimiento de bases de datos. También puede crear sus propias categorías.  
  
 
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
 Las categorías multiservidor existen solo en los servidores maestros. Solo hay una categoría de trabajo predeterminada disponible en un servidor maestro: [**Sin categoría (Multiservidor)**]. Cuando se descarga un trabajo multiservidor, su categoría se cambia a **Trabajos del servidor principal** en el servidor de destino.  
  
###  <a name="Security"></a> Seguridad  
 Para obtener información detallada, vea [Implementar la seguridad del Agente SQL Server](implement-sql-server-agent-security.md).  
  

  
##  <a name="SSMS"></a> Usar SQL Server Management Studio  
  
#### <a name="to-create-a-job-category"></a>Para crear una categoría de trabajo  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor en el que desea crear una categoría de trabajo.  
  
2.  Haga clic en el signo más para expandir **Agente SQL Server**.  
  
3.  Haga clic con el botón derecho en la carpeta **Trabajos** y seleccione **Administrar categorías de trabajos**.  
  
4.  En el cuadro de diálogo **Administrar categorías de trabajo**_nombre_servidor_ , haga clic en **Agregar**.  
  
5.  En el nuevo cuadro de diálogo, en el cuadro **Nombre** , especifique un nombre para la nueva categoría de trabajo.  
  
6.  Active la casilla **Mostrar todos los trabajos** . Seleccione uno o varios trabajos para la nueva categoría activando las casillas correspondientes a los trabajos.  
  
7.  Haga clic en **Aceptar**.  
  
8.  En el cuadro de diálogo **Administrar categorías de trabajo**_server_name_ , haga clic en **Actualizar** para asegurarse de que la nueva categoría de trabajo esté activa. Si todo se busca conforme a lo esperado, cierre este cuadro de diálogo.  
  
 Para obtener más información sobre estos cuadros de diálogo, vea [categorías de trabajo: Administrar categorías de trabajo](job-categories-manage-job-categories.md) y [propiedades de las categorías y la nueva categoría de trabajo del trabajo](job-categories-properties-new-job-category.md).  
  
 
  
##  <a name="TSQL"></a> Usar Transact-SQL  
  
#### <a name="to-create-a-job-category"></a>Para crear una categoría de trabajo  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
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
  
 Para obtener más información, consulte [sp_add_category &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-category-transact-sql).  
  

  
##  <a name="SMO"></a> Usar objetos de administración de SQL Server  
 **Para crear una categoría de trabajo**  
  
 Llame a la clase `JobCategory` mediante el lenguaje de programación que desee, como Visual Basic, Visual C# o PowerShell. Para el código de ejemplo, consulte [Programar tareas administrativas automáticas en el Agente SQL Server](sql-server-agent.md).  
  
 
  
  
