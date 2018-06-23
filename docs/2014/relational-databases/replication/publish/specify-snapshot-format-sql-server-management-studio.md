---
title: Especificar el formato de instantánea (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- snapshots [SQL Server replication], formats
- snapshot replication [SQL Server], formats
ms.assetid: 7c95f545-731a-4743-9acb-0b325ef9b98b
caps.latest.revision: 36
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 0f3d7042d4359b31764fdeefbe4f42a281ed1849
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107161"
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
  
  