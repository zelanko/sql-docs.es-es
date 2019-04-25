---
title: Información general sobre la forma de datos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], overview
ms.assetid: 4cb5fd29-4e56-46ac-ae48-a6771c321c0c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 64b54acb2334aa09c5d4c2fde421f1dca9f8f3c5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62472397"
---
# <a name="data-shaping-overview"></a>Información general sobre la forma de datos
*Dar forma a datos* significa la creación de relaciones jerárquicas entre dos o más entidades lógicas en una consulta. La jerarquía puede verse en las relaciones de elementos primarios y secundarios entre un registro de una [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)y uno o más registros (también conocido como un capítulo) de otro **Recordset**. En una relación de elementos primarios y secundarios, el elemento primario **Recordset** contiene el elemento secundario **Recordset**. Un ejemplo de este tipo de relación jerárquica es customers y orders. Para cada cliente en una base de datos, puede haber cero o más pedidos. La relación jerárquica puede ser recursivas, lo que significa que se pueden anidar registros secundarios en un registro secundario. En principio, se puede anidar un registro jerárquico a cualquier profundidad. En la práctica, ADO limita la recursividad hasta un máximo de 512 **Recordset**s.  
  
 En generales, columnas de una forma **Recordset** pueden contener datos de un proveedor de datos como Microsoft® SQL Server, las referencias a otro **Recordset**, los valores derivan de un cálculo en una sola fila de un  **Conjunto de registros**, o valores derivan de una operación sobre una columna de toda una **Recordset**. También puede ser una columna recién fabricadas y vacía.  
  
 Cuando se recupera el valor de una columna que contiene una referencia a otro **Recordset**, ADO devuelve automáticamente los datos reales **Recordset** representado por la referencia. La referencia a un **Recordset** es realmente una referencia a un subconjunto del elemento secundario, denominado un *capítulo*. Un elemento único primario puede hacer referencia a más de un elemento secundario **Recordset**.  
  
 Compatibilidad con ADO para dar forma a datos le permite consultar un origen de datos y devolver un **Recordset** en el que un registro (principal) representa un elemento (secundario) **Recordset**. En el escenario de pedidos de cliente, puede usar la forma de recuperar información de los clientes, así como los pedidos realizados por cada cliente en una sola consulta de datos. El resultante **Recordset** también conocido como la forma de **Recordset**.  
  
 Además, la forma en que ADO de datos permiten crear nuevos **Recordset** objetos sin un origen de datos subyacente utilizando la **NEW** palabra clave para describir los campos de los primarios y secundarios  **Conjuntos de registros**. El nuevo **Recordset** objeto puede, a continuación, se rellena con datos y almacenar de manera permanente. Los desarrolladores también pueden realizar varios cálculos o agregaciones (por ejemplo, **suma**, **AVG**, y **MAX**) en los campos secundarios. Dar forma a datos también puede crear un elemento primario **Recordset** desde un elemento secundario **Recordset** agrupando los registros en el elemento secundario y colocando una fila en el elemento primario de cada grupo en el elemento secundario.  
  
 SQL regular le permite recuperar datos mediante **UNIR** sintaxis, pero esto puede ser ineficaz y difícil de manejar porque los datos primarios redundantes se repiten en cada registro devuelto para una relación de elementos primarios y secundarios especificada. Forma de datos puede relacionar un registro primario único en el elemento primario **Recordset** con varios registros secundarios en el elemento secundario **Recordset**, evitando la redundancia de un **UNIR**. Mayoría de los usuarios encontrar los elementos primarios y secundarios varios **Recordset** modelo de programación más natural y más fácil trabajar con que el único **Recordset UNIR** modelo.
