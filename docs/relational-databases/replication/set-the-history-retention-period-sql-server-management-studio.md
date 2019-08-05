---
title: Establecer el período de retención del historial (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- history retention periods [SQL Server replication]
- retention periods [SQL Server replication]
ms.assetid: c288daab-5181-4d4b-ba2a-8a147098e758
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 9a33317c8f430a3665c47e94441e8f78c68085c6
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768379"
---
# <a name="set-the-history-retention-period-sql-server-management-studio"></a>Establecer el período de retención del historial (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Especifique el período de retención del historial en la página **General** del cuadro de diálogo **Propiedades de base de datos de distribución: \<baseDeDatosDeDistribución>** . Este parámetro controla durante cuánto tiempo se almacena el historial del agente de replicación. Esta página está disponible en la página **General** del cuadro de diálogo **Propiedades del distribuidor - \<distribuidor>** . Para obtener más información acerca de cómo obtener acceso a este cuadro de diálogo, [Ver y modificar las propiedades del distribuidor y del publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md).  
  
### <a name="to-specify-the-history-retention-period"></a>Para especificar el período de retención del historial  
  
1.  En la página **General** del cuadro de diálogo **Propiedades del distribuidor - \<distribuidor>** , haga clic en el botón de propiedades ( **…** ) para la base de datos de distribución.  
  
2.  Escriba un valor en el cuadro **Almacenar historial de rendimiento de replicación al menos** .  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte también  
 [Configurar distribución](../../relational-databases/replication/configure-distribution.md)  
  
  
