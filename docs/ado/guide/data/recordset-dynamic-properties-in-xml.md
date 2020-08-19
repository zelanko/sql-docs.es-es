---
description: Propiedades del conjunto de registros dinámicos en XML
title: Propiedades dinámicas del conjunto de registros en XML | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset dynamic properties in XML [ADO]
ms.assetid: 52f8e379-812a-4db8-9210-94458926301c
author: rothja
ms.author: jroth
ms.openlocfilehash: ad241bc794a3f7e462031691baf068928fb300c5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452977"
---
# <a name="recordset-dynamic-properties-in-xml"></a>Propiedades del conjunto de registros dinámicos en XML
Las siguientes propiedades específicas del proveedor de conjuntos de registros (del motor de cursor de cliente) se guardan actualmente en el formato XML:  
  
-   Actualizar resincronización  
  
-   Tabla única  
  
-   Esquema único  
  
-   Catálogo único  
  
-   Comando Resync  
  
-   IRowsetChange  
  
-   IRowsetUpdate  
  
-   CommandTimeout  
  
-   BatchSize  
  
-   UpdateCriteria  
  
-   Nombre de la reformación  
  
-   AutoRecalc  
  
 Estas propiedades se guardan en la sección Schema como atributos de la definición de elemento para el conjunto de registros que se va a conservar. Estos atributos se definen en el espacio de nombres del esquema del conjunto de filas y deben tener el prefijo "RS:".  
  
## <a name="see-also"></a>Consulte también  
 [Almacenar registros en formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
