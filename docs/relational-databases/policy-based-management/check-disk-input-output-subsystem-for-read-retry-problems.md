---
title: 'Comprobación de los problemas de reintento de lectura en el subsistema de E/S de disco: administración basada en directivas'
description: Esta regla comprueba el registro de eventos en busca del mensaje de error 825 de SQL Server, que indica que SQL Server no pudo leer los datos del disco en el primer intento.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: cedf4097-5b73-4964-9935-74a101847019
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 0f894452dd056cf0e613100a5d1a7ee2d5e9ae0c
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "75558203"
---
# <a name="check-disk-input-output-subsystem-for-read-retry-problems"></a>Comprobación de la existencia de problemas de reintento de lectura en el subsistema de entrada y salida del disco
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Esta regla comprueba si existe el mensaje de error 825 de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el registro de eventos. Este mensaje indica que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no pudo leer los datos del disco al primer intento. Este mensaje indica un problema importante con el subsistema de E/S de disco. Este mensaje no indica actualmente un problema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Sin embargo, el problema de disco podría producir la pérdida de datos o daños en la base de datos si no se resuelve.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 Las siguientes acciones podrían ayudarle a detectar y resolver el problema de hardware subyacente:  
  
-   Revise el registro de errores y el texto variable de este mensaje para obtener pistas que expliquen el problema.  
  
-   Compruebe el sistema de disco. El problema podría estar relacionado con discos, controladores de discos, tarjetas de matriz o unidades de disco.  
  
-   Póngase en contacto con el fabricante del disco para obtener las utilidades más recientes a fin de comprobar el estado del sistema de disco.  
  
-   Póngase en contacto con el fabricante del disco para obtener las últimas actualizaciones del controlador.  
  
## <a name="for-more-information"></a>Para obtener más información  
 [MSSQLSERVER_825](../errors-events/mssqlserver-825-database-engine-error.md)  
  
 [Elementos fundamentales de E/S de SQL Server, capítulo 2](/previous-versions/sql/sql-server-2005/administrator/cc917726(v=technet.10))  
  
  
