---
description: Método RemoveCertificate (clase ServerSettings)
title: Método RemoveCertificate (ServerSettings)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- RemoveCertificate Method (ServerSettings Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- RemoveCertificate method
ms.assetid: 9ffdbc39-93f5-48fb-859a-86a3ad545827
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 07ff32236bfb4b8eb26a7f0e9f8b891b77222ecb
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544358"
---
# <a name="removecertificate-method-serversettings-class"></a>Método RemoveCertificate (clase ServerSettings)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Quita el certificado de seguridad actual de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.RemoveCertificate()  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Objeto de la [clase ServerSettings](../../../relational-databases/wmi-provider-configuration-classes/serversettings-class/serversettings-class.md) que representa la configuración del servidor en una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor u**Int32** que es 0 si el servicio se modificó correctamente, 1 si no se admite la solicitud y cualquier otro número para indicar un error.  
  
## <a name="remarks"></a>Observaciones  
  
## <a name="see-also"></a>Consulte también  
 [Configurar protocolos y bibliotecas de red de servidores de red](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
