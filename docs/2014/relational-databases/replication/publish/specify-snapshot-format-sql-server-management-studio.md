---
title: Especificar el formato de instantánea (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], formats
- snapshot replication [SQL Server], formats
ms.assetid: 7c95f545-731a-4743-9acb-0b325ef9b98b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8e13b0635e750f8b6e59420fd25fe81af74eb7a0
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52811047"
---
# <a name="specify-snapshot-format-sql-server-management-studio"></a>Especificar el formato de instantánea (SQL Server Management Studio)
  Especifique el formato de instantánea en la página **Instantánea** del cuadro de diálogo **Propiedades de la publicación: \<publicación>**. Para obtener más información sobre el acceso a este cuadro de diálogo, vea [View and Modify Publication Properties](view-and-modify-publication-properties.md).  
  
### <a name="to-specify-snapshot-format"></a>Para especificar el formato de instantánea  
  
1.  En la página **Instantánea**, del cuadro de diálogo **Propiedades de la publicación: \<publicación>**, seleccione **SQL Server nativo: todos los suscriptores deben ser servidores que ejecuten SQL Server** o **Carácter: es necesario si un publicador o suscriptor no ejecuta SQL Server**.  
  
    > [!NOTE]  
    >  Se recomienda seleccionar el formato nativo, a menos que esta publicación deba ser compatible con suscripciones a una base de datos de [!INCLUDE[ssEW](../../../includes/ssew-md.md)] o una base de datos que no sea de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Configurar propiedades de instantáneas &#40;programación de la replicación con Transact-SQL&#41;](configure-snapshot-properties-replication-transact-sql-programming.md)   
 [Cambiar las propiedades de la publicación y de los artículos](change-publication-and-article-properties.md)   
 [Inicializar una suscripción con una instantánea](../initialize-a-subscription-with-a-snapshot.md)  
  
  
