---
title: Información sobre la propiedad del diagrama de base de datos
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.diagnostic.CannotOpenWithInvalidOwner
helpviewer_keywords:
- diagrams [SQL Server], ownership
- database diagrams [SQL Server], ownership
- owners [SQL Server], database diagrams
ms.assetid: 4a27a48e-c4ef-4017-82b8-0cac4d0bbcac
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: faebe8539698fbe605035dff737065864c70929b
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "75241844"
---
# <a name="understand-database-diagram-ownership-visual-database-tools"></a>Descripción de la propiedad de un diagrama de base de datos (Visual Database Tools)

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Para usar el diseñador de diagramas de base de datos, debe primero configurarlo un miembro del rol db_owner (un rol de las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ) para controlar el acceso a los diagramas. Cada diagrama tiene un único propietario: el usuario que lo ha creado. Para más información sobre cómo configurar los diagramas, consulte [Configurar el Diseñador de diagramas de base de datos (../../ssms/visual-db-tools/set-up-database-diagram-designer-visual-database-tools.md).  
  
Conviene tener en cuenta algunos aspectos sobre la propiedad de los diagramas:  
  
-   Aunque cualquier usuario con acceso a una base de datos puede crear un diagrama, una vez que se ha creado, los únicos usuarios que pueden verlo son su creador y cualquier miembro del rol db_owner.  
  
-   La propiedad de los diagramas solo se puede transferir a los miembros del rol db_owner. Esto solo es posible si el propietario anterior del diagrama se ha eliminado de la base de datos.  
  
-   Si se ha eliminado de la base de datos el propietario de un diagrama, el diagrama permanecerá en la base de datos hasta que el miembro del rol db_owner intente abrirlo. En ese momento, el miembro de db_owner podrá decidir si asume su propiedad.  
  
## <a name="see-also"></a>Consulte también

[Trabajar con diagramas de bases de datos](../../ssms/visual-db-tools/work-with-database-diagrams-visual-database-tools.md)  
[Configurar el Diseñador de diagramas de base de datos](../../ssms/visual-db-tools/set-up-database-diagram-designer-visual-database-tools.md)