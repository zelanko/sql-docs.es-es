---
title: DataSpace (ADO - sintaxis WFC) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- DataSpace collection [ADO], ADO/WFC syntax
ms.assetid: 950d45d8-07de-467b-b255-f9a7b997204c
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0344190472a9548880e828786bd252bdb17de29b
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="dataspace-ado---wfc-syntax"></a>DataSpace (ADO - sintaxis WFC)
El **createObject** método de la **DataSpace** clase especifica un objeto de negocio para procesar solicitudes de aplicación de cliente (*progid*) y el protocolo de comunicaciones y el servidor (*conexión*). **createObject** devuelve un [ObjectProxy](../../../ado/reference/ado-api/objectproxy-ado-wfc-syntax.md) objeto que representa el servidor.  
  
## <a name="package-commswfcdata"></a>paquete com.ms.wfc.data  
  
### <a name="constructor"></a>Constructor  
  
```  
public DataSpace()  
```  
  
### <a name="methods"></a>Métodos  
  
```  
public static ObjectProxy DataSpace.createObject(String  
    progid, String connection)  
```  
  
### <a name="properties"></a>Propiedades  
  
```  
public static int getInternetTimeout()  
public static void setInternetTimeout(int plInetTimeout)  
```  
  
## <a name="see-also"></a>Vea también  
 [Objeto DataSpace (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)

