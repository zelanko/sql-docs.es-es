---
title: "Configurar el Diseñador de diagramas de base de datos (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vdt.diagnostic.InstallSqlDiagramSupport
helpviewer_keywords:
- Database Diagram Designer
- database diagrams [SQL Server], Database Diagram Designer
- diagrams [SQL Server], Database Diagram Designer
ms.assetid: 927321ee-b459-4f5b-9719-4a7a95639143
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9afcf20de2220aee5d9be2763a0b274ec738e48c
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="set-up-database-diagram-designer-visual-database-tools"></a>Configurar el Diseñador de diagramas de base de datos (Visual Database Tools)
Para usar el diseñador de diagramas de base de datos, un miembro del rol **db_owner** debe configurarlo primero para controlar el acceso a los diagramas.  
  
### <a name="to-set-up-database-diagramming"></a>Para configurar diagramas de base de datos  
  
1.  En el Explorador de objetos, expanda un nodo de base de datos.  
  
2.  Expanda el nodo de Diagramas de base de datos bajo la conexión de bases de datos.  
  
3.  Seleccione **Sí** cuando se le pregunte si desea configurar la creación de diagramas de base de datos.  
  
    > [!NOTE]  
    > De esta forma creará la tabla de diagrama de base de datos, los procedimientos almacenados del sistema y una función del sistema en la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] .  
  
4.  Visual Studio creará los siguientes objetos en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]:  
  
    1.  sysdiagrams - Tabla  
  
    2.  sp_alterdiagam - Procedimiento almacenado  
  
    3.  sp_creatediagram - Procedimiento almacenado  
  
    4.  sp_dropdiagram - Procedimiento almacenado  
  
    5.  sp_renamediagram - Procedimiento almacenado  
  
    6.  fn_diagramobjects - Función  
  
    7.  sp_helpdiagrams - Procedimiento almacenado  
  
    8.  sp_helpdiagramsdefinition - Procedimiento almacenado  
  
    9. sp_upgraddiagrams - Procedimiento almacenado  
  
## <a name="see-also"></a>Vea también  
[Descripción de la propiedad de un diagrama de base de datos &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/understand-database-diagram-ownership-visual-database-tools.md)  
[Actualizar diagramas de base de datos de ediciones anteriores &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/upgrade-database-diagrams-from-previous-editions-visual-database-tools.md)  
[ALTER AUTHORIZATION (Transact-SQL)](http://msdn.microsoft.com/en-us/8c805ae2-91ed-4133-96f6-9835c908f373)  
  

