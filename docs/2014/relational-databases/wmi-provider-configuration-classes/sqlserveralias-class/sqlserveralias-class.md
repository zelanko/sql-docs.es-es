---
title: Clase SqlServerAlias | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
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
ms.openlocfilehash: 0ffbf733db8cbd672f171773e7b44560686e7d1a
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53377896"
---
# <a name="sqlserveralias-class"></a>Clase SqlServerAlias
  La [clase SqlServerAlias](sqlserveralias-class.md) representa un alias de conexión del servidor.  
  
 Se requiere un alias de conexión del servidor cuando se dan las dos condiciones siguientes:  
  
-   El cliente se conecta a una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a través de un transporte de la red que no es el predeterminado.  
  
-   La instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a la que se conecta el cliente está a la escucha en una canalización con nombre alternativa.  
  
 **Nota:** El [clase SqlServerAlias](sqlserveralias-class.md) hereda el `Put` método de la clase de proveedor. Sin embargo, no devuelve ningún resultado indicado por el método `Provider::Put`. Para obtener más información, vea la documentación de WMI.  
  
## <a name="see-also"></a>Vea también  
 [Configurar protocolos de cliente](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
