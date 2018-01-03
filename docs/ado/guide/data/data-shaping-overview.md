---
title: "Información general sobre la forma de datos | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: data shaping [ADO], overview
ms.assetid: 4cb5fd29-4e56-46ac-ae48-a6771c321c0c
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9720e3312332fe0c4a00bac01cbaa82908125dfb
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="data-shaping-overview"></a>Información general sobre la forma de datos
*Dar forma a datos* significa crear relaciones jerárquicas entre dos o más entidades lógicas en una consulta. La jerarquía puede verse en las relaciones de elementos primarios y secundarios entre un registro de una [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)y uno o más registros (también conocido como un capítulo) de otro **conjunto de registros**. En una relación de elementos primarios y secundarios, el elemento primario **Recordset** contiene el elemento secundario **conjunto de registros**. Un ejemplo de este tipo de relación jerárquica es customers y orders. Para cada cliente en una base de datos, puede haber cero o más pedidos. La relación jerárquica puede ser recursivas, lo que significa que los registros secundarios se pueden anidar en un registro secundario. En principio, un registro jerárquico se puede anidar hasta cualquier profundidad. En la práctica, ADO limita la recursividad hasta un máximo de 512 **Recordset**s.  
  
 En generales, columnas de una forma **Recordset** puede contener datos de un proveedor de datos como Microsoft® SQL Server, referencias a otro **Recordset**, valores derivan de un cálculo en una sola fila de un  **Conjunto de registros**, o valores derivan de una operación sobre una columna de toda una **conjunto de registros**. También puede ser una columna recién fabricadas y vacía.  
  
 Cuando se recupera el valor de una columna que contiene una referencia a otro **Recordset**, ADO devuelve automáticamente los datos reales **Recordset** representado por la referencia. La referencia a un **Recordset** es realmente una referencia a un subconjunto del elemento secundario, se denomina un *capítulo*. Un elemento principal único puede hacer referencia a más de un elemento secundario **conjunto de registros**.  
  
 Compatibilidad de ADO para dar forma a datos permite consultar un origen de datos y devolver un **Recordset** en el que un registro (principal) representa un elemento (secundario) **conjunto de registros**. En el escenario de pedidos de cliente, puede usar para recuperar información de los clientes, así como los pedidos realizados por cada cliente en una única consulta de forma de datos. El resultante **Recordset** tiene la forma también se denomina **conjunto de registros**.  
  
 Además, la forma en ADO de datos permiten crear nuevos **Recordset** objetos sin un origen de datos subyacente mediante el uso de la **NEW** palabra clave para describir los campos de los elementos primarios y secundarios  **Conjuntos de registros**. El nuevo **Recordset** objeto puede, a continuación, se rellena con datos y almacenar de manera permanente. Los desarrolladores también pueden realizar diversos cálculos o agregaciones (por ejemplo, **suma**, **AVG**, y **MAX**) en los campos secundarios. Dar forma a datos también puede crear un elemento primario **Recordset** de un elemento secundario **Recordset** agrupando los registros en el objeto secundario y colocando una fila en el elemento primario de cada grupo en el elemento secundario.  
  
 Regular SQL le permite recuperar datos mediante **UNIR** sintaxis, pero esto puede ser ineficaz y difícil de manejar porque los datos primarios redundantes se repiten en cada registro devuelto para una relación determinada de elementos primarios y secundarios. Forma de datos puede relacionar un registro primario único en el elemento primario **Recordset** con varios registros secundarios en el elemento secundario **Recordset**, evitando la redundancia de un **UNIR**. La mayoría de la gente considera los elementos primarios y secundarios varios **Recordset** modelo de programación más natural y más fácil trabajar con que el único **UNIR de conjunto de registros** modelo.
