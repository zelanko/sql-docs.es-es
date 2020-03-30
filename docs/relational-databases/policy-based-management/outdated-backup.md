---
title: Copia de seguridad no actualizada | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 307a4ad0-675a-4f97-9a3c-cedd61bdfae5
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 929262bc559730b99407415a9b907091a479289f
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "68087032"
---
# <a name="outdated-backup"></a>Copia de seguridad no actualizada
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Esta regla comprueba que una base de datos tiene copias de seguridad recientes. Programar copias de seguridad regulares es importante para proteger las bases de datos contra la pérdida de datos que provocan numerosos errores diferentes. La frecuencia adecuada para la copia de seguridad de los datos depende del modelo de recuperación de la base de datos, de los requisitos comerciales sobre la pérdida de datos potencial y de la frecuencia con que se actualiza la base de datos. En una base de datos actualizada frecuentemente, el riesgo de perder parte del trabajo aumenta con bastante rapidez entre las copias de seguridad.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 Recomendamos que realice frecuentemente suficientes copias de seguridad para proteger las bases de datos contra la pérdida de datos.  
  
 El modelo de recuperación simple y el modelo de recuperación completa requieren ambos copias de seguridad de los datos. En cualquier modelo de recuperación puede complementar las copias de seguridad completas con copias de seguridad diferenciales para reducir eficazmente el riesgo de pérdida de datos.  
  
 En una base de datos que use el modelo de recuperación completa, recomendamos que realice copias de seguridad del registro con frecuencia. En una base de datos de producción que contiene datos muy importantes, las copias de seguridad del registro normalmente se realizarían en intervalos de entre uno y quince minutos.  
  
> [!NOTE]  
>  El método recomendado para programar las copias de seguridad es un plan de mantenimiento de bases de datos.  
  
## <a name="for-more-information"></a>Para obtener más información  
 [Realizar copias de seguridad y restaurar bases de datos del sistema &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)  
  
 [Modelos de recuperación &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)  
  
 [Crear una copia de seguridad diferencial de una base de datos &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
 [Crear una copia de seguridad completa de base de datos &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
 [Planes de mantenimiento](../../relational-databases/maintenance-plans/maintenance-plans.md)  
  
 [Copias de seguridad de registros de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)  
  
## <a name="see-also"></a>Consulte también  
 [Supervisar y aplicar las prácticas recomendadas usando la administración basada en directivas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
