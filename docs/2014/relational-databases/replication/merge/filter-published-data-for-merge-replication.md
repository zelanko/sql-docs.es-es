---
title: Filtrar datos publicados para la replicación de mezcla | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication [SQL Server replication], filtering published data
- replication [SQL Server], filtering published data
ms.assetid: 46c5023d-7a3b-4455-becc-e159fcb5d6c4
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ad9ad45a64f57a6bef8255373180ea943af9893f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85049369"
---
# <a name="filter-published-data-for-merge-replication"></a>Filtrar datos publicados para la replicación de mezcla
  Además de los filtros de fila estáticos y los filtros de columna que se pueden definir en otros tipos de replicación, la replicación de mezcla ofrece filtros de fila con parámetros y filtros de combinación. Para más información sobre los filtros de fila estáticos y los filtros de columna, vea [Filtrar datos publicados](../publish/filter-published-data.md).  
  
 La replicación de mezcla se utiliza en muchas aplicaciones que admiten usuarios móviles; estas aplicaciones normalmente tienen muchas suscripciones, cada una de las cuales recibe un conjunto de datos único. Los filtros con parámetros combinados con los filtros de combinación permiten a un administrador configurar una publicación (o, como máximo, un pequeño número de publicaciones) y proporcionar diferentes conjuntos de datos a los usuarios, lo que reduce la sobrecarga de administración que supone la creación de varias publicaciones.  
  
-   Los filtros con parámetros permiten enviar diferentes particiones de datos a suscriptores distintos sin la necesidad de crear varias publicaciones. Por ejemplo, se puede filtrar una tabla para que la replicación de los datos de un determinado vendedor se envíe solamente a ese vendedor. Los filtros con parámetros tienen diversas opciones que permiten adaptar el filtro para optimizar el rendimiento y ajustarse perfectamente a los requisitos de los datos y aplicaciones. Para obtener más información, consulte [Filtros de fila con parámetros](parameterized-filters-parameterized-row-filters.md).  
  
-   Los filtros de combinación se utilizan normalmente junto con filtros con parámetros para ampliar el filtro a tablas relacionadas (también se pueden utilizar junto con filtros estáticos). Por ejemplo, el vendedor normalmente tiene datos en otras tablas, como las de clientes y pedidos. Estos datos se pueden filtrar para que los vendedores solo reciban los datos de los pedidos de sus clientes. Para obtener más información, consulte [Join Filters](join-filters.md).  
  
 Un filtro no debe incluir la columna `rowguidcol` que usa la replicación para identificar filas. De forma predeterminada, es la columna agregada al configurar la replicación de mezcla y se denomina **rowguid**.  
  
## <a name="see-also"></a>Consulte también  
 [Publicar datos y objetos de base de datos](../publish/publish-data-and-database-objects.md)  
  
  
