---
title: "Descripción de la propiedad de un diagrama de base de datos (Visual Database Tools) | Microsoft Docs"
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
- vdt.diagnostic.CannotOpenWithInvalidOwner
helpviewer_keywords:
- diagrams [SQL Server], ownership
- database diagrams [SQL Server], ownership
- owners [SQL Server], database diagrams
ms.assetid: 4a27a48e-c4ef-4017-82b8-0cac4d0bbcac
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: fd71d87c5a2967d23f72b7402c7ca95a8822b688
ms.lasthandoff: 04/11/2017

---
# <a name="understand-database-diagram-ownership-visual-database-tools"></a>Descripción de la propiedad de un diagrama de base de datos (Visual Database Tools)
Para usar el diseñador de diagramas de base de datos, debe primero configurarlo un miembro del rol db_owner (un rol de las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]) para controlar el acceso a los diagramas. Cada diagrama tiene un único propietario: el usuario que lo ha creado. Para más información sobre cómo configurar los diagramas, consulte [Configurar el Diseñador de diagramas de base de datos (Visual Database Tools)](../../ssms/visual-db-tools/set-up-database-diagram-designer-visual-database-tools.md).  
  
Conviene tener en cuenta algunos aspectos sobre la propiedad de los diagramas:  
  
-   Aunque cualquier usuario con acceso a una base de datos puede crear un diagrama, una vez que se ha creado, los únicos usuarios que pueden verlo son su creador y cualquier miembro del rol db_owner.  
  
-   La propiedad de los diagramas solo se puede transferir a los miembros del rol db_owner. Esto solo es posible si el propietario anterior del diagrama se ha eliminado de la base de datos.  
  
-   Si se ha eliminado de la base de datos el propietario de un diagrama, el diagrama permanecerá en la base de datos hasta que el miembro del rol db_owner intente abrirlo. En ese momento, el miembro de db_owner podrá decidir si asume su propiedad.  
  
## <a name="see-also"></a>Vea también  
[Trabajar con diagramas de base de datos (Visual Database Tools)](../../ssms/visual-db-tools/work-with-database-diagrams-visual-database-tools.md)  
[Configurar el Diseñador de diagramas de base de datos (Visual Database Tools)](../../ssms/visual-db-tools/set-up-database-diagram-designer-visual-database-tools.md)  
  

