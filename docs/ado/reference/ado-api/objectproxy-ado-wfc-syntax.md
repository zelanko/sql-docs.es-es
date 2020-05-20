---
title: ObjectProxy (ADO-sintaxis WFC) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: ff9cd79b4ac787987ef44ea3f73cbd9fb102ae43
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762324"
---
# <a name="objectproxy-ado---wfc-syntax"></a>ObjectProxy (ADO - sintaxis WFC)
Un objeto **ObjectProxy** representa un servidor y lo devuelve el método **CreateObject** del objeto [DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) . La clase ObjectProxy tiene un método, **Call**, que puede invocar un método en el servidor y devolver un objeto resultante de esa invocación.  
  
 **paquete com. ms. wfc. Data**  
  
## <a name="methods"></a>Métodos  
  
### <a name="call-method-adowfc-syntax"></a>Call (método, sintaxis de ADO/WFC)  
 Invoca un método en el servidor representado por ObjectProxy. Opcionalmente, los argumentos de método se pueden pasar como una matriz de objetos.  
  
#### <a name="syntax"></a>Sintaxis  
  
```  
public Object ObjectProxy.( String method )  
public Object ObjectProxy.( String method, Object[] args)  
```  
  
#### <a name="returns"></a>Devoluciones  
 Object  
 Objeto que es el resultado de invocar el método.  
  
#### <a name="parameters"></a>Parámetros  
 *ObjectProxy*  
 Objeto **ObjectProxy** que representa el servidor.  
  
 *method*  
 Cadena que contiene el nombre del método que se va a invocar en el servidor.  
  
 *args*  
 Opcional. Matriz de objetos que son argumentos del método en el servidor. Los tipos de datos de Java se convierten automáticamente en tipos de datos adecuados para su uso en el servidor.
