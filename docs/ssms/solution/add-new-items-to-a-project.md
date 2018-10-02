---
title: Agregar nuevos elementos a un proyecto | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- projects [SQL Server Management Studio], item additions
- adding project items
ms.assetid: 76af8692-324f-4f5e-b1a0-d72ca8a107e3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 369e132b176237a7c1318d101026ccf2663505dc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47804173"
---
# <a name="add-new-items-to-a-project"></a>Agregar nuevos elementos a un proyecto
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Agregue elementos nuevos a un proyecto para ampliar la funcionalidad de la aplicación. Un elemento nuevo puede ser una consulta o una conexión. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] tiene dos tipos de proyectos: proyecto de script de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y proyecto de script de Analysis Services. El tipo de proyecto determina los elementos que se pueden agregar al proyecto. Por ejemplo, se puede agregar una consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] (un archivo con una extensión .sql) a un proyecto de script de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , pero no a un proyecto de script de Analysis Services.  
  
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] no permite crear carpetas dentro de los proyectos. Para organizar el trabajo, cree varios proyectos dentro de la solución.  
  
### <a name="to-add-a-new-query-to-an-existing-project"></a>Para agregar una consulta nueva a un proyecto existente  
  
1.  En el Explorador de soluciones, seleccione el proyecto de destino.  
  
2.  En el menú **Proyecto** , haga clic en **Agregar nuevo elemento**.  
  
3.  En el cuadro de diálogo **Agregar nuevo elemento** , seleccione una categoría en el panel de la izquierda.  
  
4.  Seleccione una plantilla de consulta en el panel de la derecha y haga clic en **Agregar**. La consulta nueva se agrega a la carpeta **Consultas** del proyecto.  
  
5.  En el cuadro de diálogo **Conectar al motor de base de datos** , especifique una conexión para la consulta nueva y haga clic en **Conectar**. Si no desea asociar una conexión a la consulta nueva, puede hacer clic en **Cancelar** en el cuadro de diálogo de conexión.  
  
6.  Si lo desea, cambie el nombre de la consulta en el Explorador de soluciones.  
  
### <a name="to-add-a-new-connection-to-an-existing-project"></a>Para agregar una conexión nueva a un proyecto existente  
  
1.  En el Explorador de soluciones, seleccione el proyecto de destino.  
  
2.  En el menú **Proyecto** , haga clic en **Agregar nuevo elemento**.  
  
3.  Seleccione **Conexión** en el panel de la izquierda.  
  
4.  Seleccione **Nueva conexión** en el panel de la derecha y haga clic en **Agregar**.  
  
5.  En el cuadro de diálogo **Conectar al motor de base de datos** , especifique una conexión para la consulta nueva y haga clic en **Conectar**. La conexión nueva se agrega a la carpeta **Conexiones** del proyecto.  
  
## <a name="see-also"></a>Ver también  
[Explorador de soluciones](../../ssms/solution/solution-explorer.md)  
[Asociación de extensiones de archivo a un editor de código](../../relational-databases/scripting/associate-file-extensions-to-a-code-editor.md)  
[Agregar elementos existentes a un proyecto](../../ssms/solution/add-existing-items-to-a-project.md)  
[Quitar o eliminar un elemento o un proyecto](../../ssms/solution/remove-or-delete-an-item-or-project.md)  
  
