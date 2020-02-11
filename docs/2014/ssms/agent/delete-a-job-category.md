---
title: Eliminar una categoría de trabajo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, categories
- deleting job category
- jobs [SQL Server Agent], categories
- categories [SQL Server Agent jobs]
- removing job category
ms.assetid: 47a7640b-20b3-4639-ab37-b6fc73575e6c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9bb392991afbb3707fafdb18a28cc3de53f97c78
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "72783198"
---
# <a name="delete-a-job-category"></a>Eliminar una categoría de trabajo
  En este tema se describe cómo eliminar [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] una categoría de trabajo [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] del agente [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]en [!INCLUDE[tsql](../../includes/tsql-md.md)] mediante o objetos de administración de SQL Server.  
  
 Las categorías de trabajo le ayudan a organizar los trabajos para poder filtrarlos y agruparlos fácilmente. Por ejemplo, puede organizar todos los trabajos de copia de seguridad de las bases de datos en la categoría Mantenimiento de bases de datos.  

##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
 Al eliminar una categoría de trabajo definida por el usuario, el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] le solicita que vuelva a asignar los trabajos asignados a ella a otra categoría de trabajo. Solo puede eliminar categorías de trabajo definidas por el usuario.  
  
###  <a name="Security"></a> Seguridad  
 Para obtener información detallada, vea [Implementar la seguridad del Agente SQL Server](implement-sql-server-agent-security.md).  

##  <a name="SSMS"></a> Uso de SQL Server Management Studio  
  
### <a name="to-delete-a-job-category"></a>Para eliminar una categoría de trabajo  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor en el que desea eliminar una categoría de trabajo.  
  
2.  Haga clic en el signo más para expandir **Agente SQL Server**.  
  
3.  Haga clic con el botón derecho en la carpeta **Trabajos** y seleccione **Administrar categorías de trabajos**.  
  
4.  En el cuadro de diálogo **administrar categorías de trabajo**_SERVER_NAME_ , seleccione la categoría de trabajo que desea eliminar.  
  
5.  Haga clic en **Eliminar**.  
  
6.  En el cuadro de diálogo **Categorías de trabajo** , haga clic en **Sí**.  
  
7.  Cierre el cuadro de diálogo **administrar categorías de trabajo**_SERVER_NAME_ .  
  
##  <a name="TSQL"></a> Usar Transact-SQL  
  
### <a name="to-delete-a-job-category"></a>Para eliminar una categoría de trabajo  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```sql
    -- deletes the job category named AdminJobs.  
    USE msdb ;  
    GO   
    EXEC dbo.sp_delete_category  
        @name = N'AdminJobs',  
        @class = N'JOB' ;  
    GO  
    ```  
  
 Para obtener más información, vea [sp_delete_category &#40;&#41;de Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-delete-category-transact-sql).  

  
##  <a name="SMO"></a>Usar Objetos de administración de SQL Server  

### <a name="to-delete-a-job-category"></a>Para eliminar una categoría de trabajo
  
 Llame a la clase `JobCategory` mediante el lenguaje de programación que desee, como Visual Basic, Visual C# o PowerShell.  
