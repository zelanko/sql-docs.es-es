---
title: Descripción de la propiedad de un diagrama de base de datos (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vdt.diagnostic.CannotOpenWithInvalidOwner
helpviewer_keywords:
- diagrams [SQL Server], ownership
- database diagrams [SQL Server], ownership
- owners [SQL Server], database diagrams
ms.assetid: 4a27a48e-c4ef-4017-82b8-0cac4d0bbcac
caps.latest.revision: 19
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 6a05d1be7a194bd3ed47aed4936cdc51d479e81f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36203555"
---
# <a name="understand-database-diagram-ownership-visual-database-tools"></a>Descripción de la propiedad de un diagrama de base de datos (Visual Database Tools)
  Para usar el diseñador de diagramas de base de datos, debe primero configurarlo un miembro del rol db_owner (un rol de las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) para controlar el acceso a los diagramas. Cada diagrama tiene un único propietario: el usuario que lo ha creado. Para obtener más información acerca de la configuración de diagramas, vea [establecer seguridad del Diseñador de diagramas de base de datos &#40;Visual Database Tools&#41;](visual-database-tools.md).  
  
 Conviene tener en cuenta algunos aspectos sobre la propiedad de los diagramas:  
  
-   Aunque cualquier usuario con acceso a una base de datos puede crear un diagrama, una vez que se ha creado, los únicos usuarios que pueden verlo son su creador y cualquier miembro del rol db_owner.  
  
-   La propiedad de los diagramas solo se puede transferir a los miembros del rol db_owner. Esto solo es posible si el propietario anterior del diagrama se ha eliminado de la base de datos.  
  
-   Si se ha eliminado de la base de datos el propietario de un diagrama, el diagrama permanecerá en la base de datos hasta que el miembro del rol db_owner intente abrirlo. En ese momento, el miembro de db_owner podrá decidir si asume su propiedad.  
  
## <a name="see-also"></a>Vea también  
 [Trabajar con diagramas de base de datos &#40;Visual Database Tools&#41;](work-with-database-diagrams-visual-database-tools.md)   
 [Configurar el Diseñador de diagramas de base de datos &#40;Visual Database Tools&#41;](visual-database-tools.md)  
  
  