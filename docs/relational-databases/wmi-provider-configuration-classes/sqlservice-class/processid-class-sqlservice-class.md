---
title: ProcessId (clase) (SqlService)
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ProcessId Class (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ProcessId property
ms.assetid: 99b5a2e9-b44a-48a0-993e-04bd15c7fef4
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 226530ebb5347ab2ace2804fc8e293d1c5899793
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85888389"
---
# <a name="processid-class-sqlservice-class"></a>Clase ProcessId (clase SqlService)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Obtiene el id. del proceso del sistema que identifica un servicio de forma inequívoca.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.ProcessId [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Objeto de la [clase SqlService](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) que representa el servicio.  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor **UInt32** que especifica el identificador que identifica de forma única el proceso.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="example"></a>Ejemplo  
  
```  
mysqlservice.ProcessId = 324  
```  
  
## <a name="see-also"></a>Consulte también  
 [Iniciar y detener servicios](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
