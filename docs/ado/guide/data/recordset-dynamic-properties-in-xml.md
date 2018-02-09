---
title: "Propiedades del conjunto de registros dinámicos en XML | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Recordset dynamic properties in XML [ADO]
ms.assetid: 52f8e379-812a-4db8-9210-94458926301c
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 221ecdff804539bf8ff80335c71f762cbe7b28de
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="recordset-dynamic-properties-in-xml"></a>Propiedades del conjunto de registros dinámicos en XML
Actualmente, las siguientes propiedades específicas del proveedor de conjunto de registros (desde el motor de Cursor de cliente) se conservan en el formato XML:  
  
-   Resincronización de la actualización  
  
-   Tabla única  
  
-   Unique Schema  
  
-   Catálogo único  
  
-   Comando Resync  
  
-   IRowsetChange  
  
-   IRowsetUpdate  
  
-   CommandTimeOut  
  
-   BatchSize  
  
-   UpdateCriteria  
  
-   Cambiar la forma de nombre  
  
-   AutoRecalc  
  
 Estas propiedades se guardan en la sección de esquema como atributos de la definición de elemento para el conjunto de registros que se conserva. Estos atributos se definen en el espacio de nombres de esquema de conjunto de filas y debe tener el prefijo "rs:".  
  
## <a name="see-also"></a>Vea también  
 [Almacenar registros en formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
