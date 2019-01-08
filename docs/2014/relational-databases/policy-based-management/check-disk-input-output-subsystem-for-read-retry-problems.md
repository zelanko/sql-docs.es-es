---
title: Compruebe el subsistema de entrada y salida de disco para problemas de reintento de lectura | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: cedf4097-5b73-4964-9935-74a101847019
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1072668681a7e989e0ebb1bbcc385cc53e5a7b2d
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53362417"
---
# <a name="check-disk-input-output-subsystem-for-read-retry-problems"></a>Comprobación de la existencia de problemas de reintento de lectura en el subsistema de entrada y salida del disco
  Esta regla comprueba si existe el mensaje de error 825 de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el registro de eventos. Este mensaje indica que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no pudo leer los datos del disco al primer intento. Este mensaje indica un problema importante con el subsistema de E/S de disco. Este mensaje no indica actualmente un problema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Sin embargo, el problema de disco podría producir la pérdida de datos o daños en la base de datos si no se resuelve.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 Las siguientes acciones podrían ayudarle a detectar y resolver el problema de hardware subyacente:  
  
-   Revise el registro de errores y el texto variable de este mensaje para obtener pistas que expliquen el problema.  
  
-   Compruebe el sistema de disco. El problema podría estar relacionado con discos, controladores de discos, tarjetas de matriz o unidades de disco.  
  
-   Póngase en contacto con el fabricante del disco para obtener las utilidades más recientes a fin de comprobar el estado del sistema de disco.  
  
-   Póngase en contacto con el fabricante del disco para obtener las últimas actualizaciones del controlador.  
  
## <a name="for-more-information"></a>Para obtener más información  
 [MSSQLSERVER_825](../errors-events/mssqlserver-825-database-engine-error.md)  
  
 [Elementos fundamentales de E/S de SQL Server, capítulo 2](https://go.microsoft.com/fwlink/?linkid=69370)  
  
  
