---
title: Establecimiento del período de retención del historial (SSMS)
description: Aprenda a establecer el período de retención del historial de la base de datos de distribución en SQL Server Management Studio (SSMS).
ms.custom: seo-lt-2019
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
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: 5bf353b2e8fae3277a9377c2e4703a4340411a2c
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479676"
---
# <a name="set-the-history-retention-period-sql-server-management-studio"></a>Establecer el período de retención del historial (SQL Server Management Studio)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  Especifique el período de retención del historial en la página **General** del cuadro de diálogo **Propiedades de base de datos de distribución: \<DistributionDatabase>** . Este parámetro controla durante cuánto tiempo se almacena el historial del agente de replicación. Esta página está disponible en la página **General** del cuadro de diálogo **Propiedades del distribuidor: \<Distributor>** . Para más información acerca de cómo obtener acceso a este cuadro de diálogo, [Ver y modificar las propiedades del distribuidor y del publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md).  
  
### <a name="to-specify-the-history-retention-period"></a>Para especificar el período de retención del historial  
  
1.  En la página **General** del cuadro de diálogo **Propiedades del distribuidor: \<Distributor>** , haga clic en el botón de propiedades ( **…** ) de la base de datos de distribución.  
  
2.  Escriba un valor en el cuadro **Almacenar historial de rendimiento de replicación al menos** .  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte también  
 [Configurar distribución](../../relational-databases/replication/configure-distribution.md)  
  
  
