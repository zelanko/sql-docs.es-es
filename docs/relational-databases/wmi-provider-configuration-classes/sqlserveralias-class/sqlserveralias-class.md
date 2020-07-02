---
title: Clase SqlServerAlias
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
apiname:
- SqlServerAlias Class
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SqlServerAlias class
ms.assetid: 475662b9-6985-45bf-b1e9-b0f26ef50443
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 18d6cfd0b2d0184e5bf667fc12f57a6c0dcf5025
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85753727"
---
# <a name="sqlserveralias-class"></a>Clase SqlServerAlias
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/applies-to-version/sqlserver.md)]
  La [clase SqlServerAlias](../../../relational-databases/wmi-provider-configuration-classes/sqlserveralias-class/sqlserveralias-class.md) representa un alias de conexión del servidor.  
  
 Se requiere un alias de conexión del servidor cuando se dan las dos condiciones siguientes:  
  
-   El cliente se está conectando a una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a través de un transporte de red que no es el transporte de red predeterminado.  
  
-   La instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a la que se conecta el cliente está a la escucha en una canalización con nombre alternativa.  
  
 **Nota** : La [clase SqlServerAlias](../../../relational-databases/wmi-provider-configuration-classes/sqlserveralias-class/sqlserveralias-class.md) hereda el método **Put** de la clase Provider. Sin embargo, no devuelve ningún resultado indicado por el método **Provider::Put** . Para obtener más información, vea la documentación de WMI.  
  
## <a name="see-also"></a>Consulte también  
 [configurar protocolos de cliente](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
