---
title: Administración de espacios de tabla de Oracle | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], managing tablespaces
- tablespaces [SQL Server replication]
ms.assetid: b8ea6c3b-01d6-4efc-bbfb-03b264530bbd
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9a6bf22c7649646506b65628f556b52fead23375
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63022297"
---
# <a name="manage-oracle-tablespaces"></a>Administrar espacios de tabla de Oracle
  Un espacio de tabla es una unidad de almacenamiento de base de datos que equivale aproximadamente a un grupo de archivos de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Los espacios de tabla permiten el almacenamiento y la administración de objetos de base de datos en grupos individuales. Para obtener más información, vea la documentación de Oracle.  
  
 Al configurar una tabla como parte de una publicación de Oracle, puede especificar un espacio de tabla de Oracle existente, para utilizarlo al almacenar la información de registro de la replicación. Si no lo especifica, el espacio de tabla que se utilizará para los objetos de la replicación será el espacio de tabla predeterminado asociado con el esquema de usuario administrativo de la replicación configurado al configurar el publicador.  
  
 **Para especificar un espacio de tabla para una tabla de registro de artículos**:  
  
-   Especifique un espacio de tabla en el cuadro de diálogo **Propiedades del artículo** . Para obtener más información sobre el acceso a este cuadro de diálogo, vea [View and Modify Publication Properties](../publish/view-and-modify-publication-properties.md).  
  
-   Use [sp_changearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changearticle-transact-sql). Para utilizar **sp_changearticle**, especifique lo siguiente:  
  
    -   Nombre del publicador de Oracle para el parámetro **@publisher**.  
  
    -   El nombre de la publicación de Oracle para el **@publication**parámetro.  
  
    -   Nombre del artículo para el parámetro **@article**.  
  
    -   Un valor de ' Tablespaces ' para el parámetro **@property**.  
  
    -   Nombre del espacio de tablas para el parámetro **@value**.  
  
## <a name="see-also"></a>Consulte también  
 [Configurar un publicador de Oracle](configure-an-oracle-publisher.md)   
 [Objetos creados en el publicador de Oracle](objects-created-on-the-oracle-publisher.md)  
  
  
