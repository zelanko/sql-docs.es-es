---
title: Definición del período de retención de distribución
description: Establezca el período de retención de los datos de la base de datos de distribución en SQL Server Management Studio (SSMS).
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transaction retention periods [SQL Server replication]
- retention periods [SQL Server replication]
ms.assetid: 9a98c53a-fea5-4235-b23d-6c69587c5676
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: a5f1f925d4ab0438ab237a903b2ad80007e86e20
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479736"
---
# <a name="set-distribution-retention-period-for-transactional-publications"></a>Establecer el período de retención de distribución para las publicaciones transaccionales
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  Especifique el período de retención de distribución mínimo y máximo en el cuadro de diálogo **Propiedades de base de datos de distribución: \<DistributionDatabase>** . Está disponible en la página **General** del cuadro de diálogo **Propiedades del distribuidor: \<Distributor>** . Para más información acerca de cómo obtener acceso a este cuadro de diálogo, [Ver y modificar las propiedades del distribuidor y del publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md).  
  
### <a name="to-specify-the-distribution-retention-period"></a>Para especificar el período de retención de distribución  
  
1.  En la página **General** del cuadro de diálogo **Propiedades del distribuidor: \<Distributor>** , haga clic en el botón de propiedades ( **...** ) de la base de datos de distribución.  
  
2.  Para especificar el período mínimo de retención de distribución, escriba un valor en el cuadro **Al menos** ; para especificar el período máximo de retención de distribución, escriba un valor en el cuadro **Pero no más de** .  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="see-also"></a>Consulte también  
 [Configurar distribución](../../relational-databases/replication/configure-distribution.md)   
 [Desactivación y expiración de la suscripción](../../relational-databases/replication/subscription-expiration-and-deactivation.md)  
  
  
