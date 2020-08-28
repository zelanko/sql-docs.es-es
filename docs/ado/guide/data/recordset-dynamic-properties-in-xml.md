---
description: Propiedades del conjunto de registros dinámicos en XML
title: Propiedades dinámicas del conjunto de registros en XML | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset dynamic properties in XML [ADO]
ms.assetid: 52f8e379-812a-4db8-9210-94458926301c
author: rothja
ms.author: jroth
ms.openlocfilehash: 395a81108e3ceaed99ad8ccf1fbab29831dd116d
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979896"
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
