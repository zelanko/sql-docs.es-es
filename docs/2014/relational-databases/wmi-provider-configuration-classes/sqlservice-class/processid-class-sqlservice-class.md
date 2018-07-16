---
title: Clase ProcessId (clase SqlService) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ProcessId Class (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- ProcessId property
ms.assetid: 99b5a2e9-b44a-48a0-993e-04bd15c7fef4
caps.latest.revision: 35
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 0885ca6300d50b1d9f9aacd81ae4382985f650d8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37251537"
---
# <a name="processid-class-sqlservice-class"></a>Clase ProcessId (clase SqlService)
  Obtiene el id. del proceso del sistema que identifica un servicio de forma inequívoca.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object  
.ProcessId [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Objeto de la [clase SqlService](sqlservice-class.md) que representa el servicio.  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor `uint32` que especifica el id. que identifica el proceso de forma inequívoca.  
  
## <a name="remarks"></a>Notas  
  
## <a name="example"></a>Ejemplo  
  
```  
mysqlservice.ProcessId = 324  
```  
  
## <a name="see-also"></a>Vea también  
 [Iniciar y detener servicios](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
