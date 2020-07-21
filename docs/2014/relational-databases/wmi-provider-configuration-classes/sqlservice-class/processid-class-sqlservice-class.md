---
title: Clase ProcessId (clase SqlService) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f64a81709e63510af507996cc2d2968a765e0fad
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85002128"
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
  
## <a name="remarks"></a>Comentarios  
  
## <a name="example"></a>Ejemplo  
  
```  
mysqlservice.ProcessId = 324  
```  
  
## <a name="see-also"></a>Consulte también  
 [Iniciar y detener servicios](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
