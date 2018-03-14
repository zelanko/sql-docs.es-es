---
title: "Administración de espacios de tabla de Oracle | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Oracle publishing [SQL Server replication], managing tablespaces
- tablespaces [SQL Server replication]
ms.assetid: b8ea6c3b-01d6-4efc-bbfb-03b264530bbd
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d6a685337d7aeb6dbf388faec93051ce29cc5759
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/08/2018
---
# <a name="manage-oracle-tablespaces"></a>Administrar espacios de tabla de Oracle
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Un espacio de tabla es una unidad de almacenamiento en una base de datos que equivale aproximadamente a un grupo de archivos en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Los espacios de tabla permiten el almacenamiento y la administración de objetos de base de datos en grupos individuales. Para obtener más información, vea la documentación de Oracle.  
  
 Al configurar una tabla como parte de una publicación de Oracle, puede especificar un espacio de tabla de Oracle existente, para utilizarlo al almacenar la información de registro de la replicación. Si no lo especifica, el espacio de tabla que se utilizará para los objetos de la replicación será el espacio de tabla predeterminado asociado con el esquema de usuario administrativo de la replicación configurado al configurar el publicador.  
  
 **Para especificar un espacio de tabla para una tabla de registro de artículos**:  
  
-   Especifique un espacio de tabla en el cuadro de diálogo **Propiedades del artículo** . Para obtener más información sobre el acceso a este cuadro de diálogo, vea [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
-   Use [sp_changearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md). Para utilizar **sp_changearticle**, especifique lo siguiente:  
  
    -   El nombre del publicador de Oracle para el parámetro **@publisher**.  
  
    -   El nombre de la publicación de Oracle para el parámetro **@publication**.  
  
    -   El nombre del artículo para el parámetro **@article**.  
  
    -   Un valor de espacio de tabla para el parámetro **@property**.  
  
    -   El nombre del espacio de tabla para el parámetro **@value**.  
  
## <a name="see-also"></a>Ver también  
 [Configurar un publicador de Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Objects Created on the Oracle Publisher](../../../relational-databases/replication/non-sql/objects-created-on-the-oracle-publisher.md)  
  
  
