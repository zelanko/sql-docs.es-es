---
description: ObjectProxy (ADO - sintaxis WFC)
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
ms.openlocfilehash: 7809c1b9ce4d090ed63465061045ea04000f47dc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443037"
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
