---
title: Clase SqlServerAlias | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
api_name:
- SqlServerAlias Class
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SqlServerAlias class
ms.assetid: 475662b9-6985-45bf-b1e9-b0f26ef50443
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: d913f28415c708ad09b419732ebef4e26b607ecb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48221415"
---
# <a name="sqlserveralias-class"></a>Clase SqlServerAlias
  La [clase SqlServerAlias](sqlserveralias-class.md) representa un alias de conexión del servidor.  
  
 Se requiere un alias de conexión del servidor cuando se dan las dos condiciones siguientes:  
  
-   El cliente se conecta a una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a través de un transporte de la red que no es el predeterminado.  
  
-   La instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a la que se conecta el cliente está a la escucha en una canalización con nombre alternativa.  
  
 **Nota:** el [clase SqlServerAlias](sqlserveralias-class.md) hereda el `Put` método de la clase de proveedor. Sin embargo, no devuelve ningún resultado indicado por el método `Provider::Put`. Para obtener más información, vea la documentación de WMI.  
  
## <a name="see-also"></a>Vea también  
 [Configurar protocolos de cliente](http://technet.microsoft.com/library/ms181035.aspx)  
  
  
