---
title: DataSpace (ADO - sintaxis WFC) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- DataSpace collection [ADO], ADO/WFC syntax
ms.assetid: 950d45d8-07de-467b-b255-f9a7b997204c
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 160fe6068b86edc5d10f277dbd298954dc37838f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
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
