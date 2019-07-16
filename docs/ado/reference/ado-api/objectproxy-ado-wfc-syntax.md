---
title: ObjectProxy (ADO - sintaxis WFC) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ObjectProxy collection [ADO]
ms.assetid: f68f58bc-ad28-46cc-9fb3-099e1a678397
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 485d011fa6762acd04cad54ff7fffc8d8136e063
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917956"
---
# <a name="objectproxy-ado---wfc-syntax"></a>ObjectProxy (ADO - sintaxis WFC)
Un **ObjectProxy** objeto representa un servidor y es devuelto por la **createObject** método de la [DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) objeto. La clase ObjectProxy tiene un método, **llamar**, que se puede invocar un método en el servidor y devolver un objeto resultante de esa llamada.  
  
 **paquete com.ms.wfc.data**  
  
## <a name="methods"></a>Métodos  
  
### <a name="call-method-adowfc-syntax"></a>Llame al método (sintaxis de ADO/WFC)  
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
 Cadena que contiene el nombre del método que se invocará en el servidor.  
  
 *args*  
 Opcional. Una matriz de objetos que son argumentos para el método en el servidor. Tipos de datos de Java se convierten automáticamente en los tipos de datos adecuados para su uso en el servidor.
