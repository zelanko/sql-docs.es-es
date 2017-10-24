---
title: "Propiedades del conjunto de registros dinámicos en XML | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Recordset dynamic properties in XML [ADO]
ms.assetid: 52f8e379-812a-4db8-9210-94458926301c
caps.latest.revision: 3
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 62d9b59fc1145e09f89bbe69b8d7b6e561798e70
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="recordset-dynamic-properties-in-xml"></a>Propiedades del conjunto de registros dinámicos en XML
Actualmente, las siguientes propiedades específicas del proveedor de conjunto de registros (desde el motor de Cursor de cliente) se conservan en el formato XML:  
  
-   Resincronización de la actualización  
  
-   Tabla única  
  
-   Esquema único  
  
-   Catálogo único  
  
-   Comando Resync  
  
-   IRowsetChange  
  
-   IRowsetUpdate  
  
-   CommandTimeout  
  
-   BatchSize  
  
-   UpdateCriteria  
  
-   Cambiar la forma de nombre  
  
-   AutoRecalc  
  
 Estas propiedades se guardan en la sección de esquema como atributos de la definición de elemento para el conjunto de registros que se conserva. Estos atributos se definen en el espacio de nombres de esquema de conjunto de filas y debe tener el prefijo "rs:".  
  
## <a name="see-also"></a>Vea también  
 [Almacenar registros en formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)

