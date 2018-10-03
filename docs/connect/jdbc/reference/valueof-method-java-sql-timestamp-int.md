---
title: Método valueOf (java.sql.Timestamp, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 114f55af-62ab-4c60-8724-0affbbbbbcdc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4ced75c886fcc0bf58d1671e50a213d5a6003a97
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47704110"
---
# <a name="valueof-method-javasqltimestamp-int"></a>Método valueOf (java.sql.Timestamp, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Crea un objeto **DateTimeOffset** que representa un punto en el tiempo en un desfase concreto de GMT según un valor java.sql.Timestamp y un valor que indica el desfase en minutos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public static DateTimeOffset valueOf(java.sql.Timestamp timestamp, int minutesOffset)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *timestamp*  
  
 Un valor java.sql.Timestamp.  
  
 *minutesOffset*  
  
 El desplazamiento en minutos.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un objeto DateTimeOffset que representa el punto cronológico determinado por el objeto java.sql.Timestamp en el desplazamiento dado, minutos, de GMT.  
  
## <a name="see-also"></a>Ver también  
 [Clase DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [Miembros DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
