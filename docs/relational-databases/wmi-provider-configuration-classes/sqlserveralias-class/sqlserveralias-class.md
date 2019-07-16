---
title: Clase SqlServerAlias | Microsoft Docs
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
ms.openlocfilehash: cdcbd34978738d64d52b3c70a280507b6cb0c391
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68052370"
---
# <a name="sqlserveralias-class"></a>Clase SqlServerAlias
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  La [clase SqlServerAlias](../../../relational-databases/wmi-provider-configuration-classes/sqlserveralias-class/sqlserveralias-class.md) representa un alias de conexión del servidor.  
  
 Se requiere un alias de conexión del servidor cuando se dan las dos condiciones siguientes:  
  
-   El cliente se conecta a una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a través de un transporte de la red que no es el predeterminado.  
  
-   La instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a la que se conecta el cliente está a la escucha en una canalización con nombre alternativa.  
  
 **Nota:** El [clase SqlServerAlias](../../../relational-databases/wmi-provider-configuration-classes/sqlserveralias-class/sqlserveralias-class.md) hereda el **colocar** método de la clase de proveedor. Sin embargo, no devuelve ningún resultado indicado por el método **Provider::Put** . Para obtener más información, vea la documentación de WMI.  
  
## <a name="see-also"></a>Vea también  
 [Configurar protocolos de cliente](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
