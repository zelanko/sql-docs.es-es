---
title: ObjectProxy (ADO - sintaxis WFC) | Documentos de Microsoft
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
- ObjectProxy collection [ADO]
ms.assetid: f68f58bc-ad28-46cc-9fb3-099e1a678397
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dd42478c8da0cc0eba4471ac46a66ec4a08d5bd5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="objectproxy-ado---wfc-syntax"></a>ObjectProxy (ADO - sintaxis WFC)
Un **ObjectProxy** objeto representa un servidor y se devuelve por la **createObject** método de la [DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) objeto. La clase ObjectProxy tiene un método, **llamar a**, que puede invocar un método en el servidor y devolver un objeto resultante de esa llamada.  
  
 **paquete com.ms.wfc.data**  
  
## <a name="methods"></a>Métodos  
  
### <a name="call-method-adowfc-syntax"></a>Llame al método (sintaxis ADO/WFC)  
 Invoca un método en el servidor representado por el objeto ObjectProxy. Si lo desea, se pueden pasar argumentos de método como una matriz de objetos.  
  
#### <a name="syntax"></a>Sintaxis  
  
```  
public Object ObjectProxy.( String method )  
public Object ObjectProxy.( String method, Object[] args)  
```  
  
#### <a name="returns"></a>Devuelve  
 Object  
 Objeto resultante de la llamada al método.  
  
#### <a name="parameters"></a>Parámetros  
 *ObjectProxy*  
 Un **ObjectProxy** objeto que representa el servidor.  
  
 *Método*  
 Cadena que contiene el nombre del método que se va a invocar en el servidor.  
  
 *args*  
 Opcional. Una matriz de objetos que son argumentos para el método en el servidor. Tipos de datos de Java se convierten automáticamente en tipos de datos adecuados para su uso en el servidor.
