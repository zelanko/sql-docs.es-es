---
description: Optimizar la administración automatizada en una empresa
title: Optimizar la administración automatizada en una empresa
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- performance [SQL Server], automated administration
- tuning automated administration [SQL Server]
- monitoring performance [SQL Server], automated administration
ms.assetid: 671fed35-3859-4b0d-8f38-4dd07436857e
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 6fbb2e883e77ed797fb367c3624429c2b1a4d720
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/14/2020
ms.locfileid: "92038736"
---
# <a name="tune-automated-administration-across-an-enterprise"></a>Optimizar la administración automatizada en una empresa

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> En [Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance), actualmente son compatibles la mayoría de las características del Agente SQL Server. Consulte [Diferencias entre T-SQL de Azure SQL Managed Instance y SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para más información.

La administración multiservidor con el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de Microsoft aprovecha las características de optimización automática de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por tanto, en condiciones normales no es necesaria la optimización adicional de trabajos. Sin embargo, la carga de red aumenta al ejecutar trabajos, generar alertas y notificar operadores. Puede optimizar la administración automatizada en una empresa para minimizar el tráfico de red que causan estas actividades.  

## <a name="see-also"></a>Consulte también

[Supervisar el rendimiento del motor de flujo de datos](../../integration-services/performance/performance-counters.md)