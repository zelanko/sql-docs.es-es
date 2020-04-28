---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a058a2d0c5a808f29807744c6ba01f658bebc120
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67924445"
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
