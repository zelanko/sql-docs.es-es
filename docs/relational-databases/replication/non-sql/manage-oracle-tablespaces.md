---
title: Administración de espacios de tabla de Oracle | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], managing tablespaces
- tablespaces [SQL Server replication]
ms.assetid: b8ea6c3b-01d6-4efc-bbfb-03b264530bbd
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6320d7192d2493486779a1b6ac433f78a45114ca
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "70276539"
---
# <a name="manage-oracle-tablespaces"></a>Administrar espacios de tabla de Oracle
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Un espacio de tabla es una unidad de almacenamiento de base de datos que equivale aproximadamente a un grupo de archivos de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Los espacios de tabla permiten el almacenamiento y la administración de objetos de base de datos en grupos individuales. Para obtener más información, vea la documentación de Oracle.  
  
 Al configurar una tabla como parte de una publicación de Oracle, puede especificar un espacio de tabla de Oracle existente, para utilizarlo al almacenar la información de registro de la replicación. Si no lo especifica, el espacio de tabla que se utilizará para los objetos de la replicación será el espacio de tabla predeterminado asociado con el esquema de usuario administrativo de la replicación configurado al configurar el publicador.  
  
 **Para especificar un espacio de tabla para una tabla de registro de artículos**:  
  
-   Especifique un espacio de tabla en el cuadro de diálogo **Propiedades del artículo** . Para obtener más información sobre el acceso a este cuadro de diálogo, vea [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
-   Use [sp_changearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md). Para utilizar **sp_changearticle**, especifique lo siguiente:  
  
    -   El nombre del publicador de Oracle para el parámetro **\@publisher**.  
  
    -   El nombre de la publicación de Oracle para el parámetro **\@publication**.  
  
    -   El nombre del artículo para el parámetro **\@article**.  
  
    -   Un valor de "espacio de tabla" para el parámetro **\@property**.  
  
    -   El nombre del espacio de tabla para el parámetro **\@value**.  
  
## <a name="see-also"></a>Consulte también  
 [Configurar un publicador de Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Objetos creados en el publicador de Oracle](../../../relational-databases/replication/non-sql/objects-created-on-the-oracle-publisher.md)  
  
  
