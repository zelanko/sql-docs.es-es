---
title: Propiedades del conjunto de registros dinámicos en XML | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924445"
---
# <a name="recordset-dynamic-properties-in-xml"></a>Propiedades del conjunto de registros dinámicos en XML
Actualmente, las siguientes propiedades específicas del proveedor de conjunto de registros (desde el motor de Cursor de cliente) se conservan en el formato XML:  
  
-   Resincronización de la actualización  
  
-   Tabla única  
  
-   Esquema único  
  
-   Catálogo único  
  
-   Resincronizar comando  
  
-   IRowsetChange  
  
-   IRowsetUpdate  
  
-   CommandTimeout  
  
-   BatchSize  
  
-   UpdateCriteria  
  
-   Cambiar la forma de nombre  
  
-   AutoRecalc  
  
 Estas propiedades se guardan en la sección de esquema como atributos de la definición de elemento para el conjunto de registros que se hace persistente. Estos atributos se definen en el espacio de nombres del esquema de conjunto de filas y debe tener el prefijo "rs:".  
  
## <a name="see-also"></a>Vea también  
 [Almacenar registros en formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
