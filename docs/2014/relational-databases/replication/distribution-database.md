---
title: Base de datos de distribución | Microsoft Docs
ms.custom: ''
ms.date: 06/30/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.rep.configuredistributionwizard.distributiondatabase.f1
ms.assetid: 5b42a083-7a11-41d8-9e3f-320c7c907237
caps.latest.revision: 25
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 6114aa6d8a1f283eb1ffaf8969b5026dafdffc40
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106731"
---
# <a name="distribution-database"></a>Base de datos de distribución
  En la base de datos de distribución se almacenan metadatos y datos del historial de todos los tipos de replicación y transacciones de replicación transaccional.  
  
 En muchas ocasiones, una sola base de datos de distribución resulta suficiente. No obstante, si varios publicadores utilizan un único distribuidor, considere la posibilidad de crear una base de datos de distribución para cada publicador. De esta forma, se garantiza que los datos que pasan por cada base de datos de distribución son distintos. Para especificar una base de datos de distribución para el distribuidor, puede utilizar el Asistente para configurar la distribución. Si es necesario, especifique bases de datos de distribución adicionales en el cuadro de diálogo **Propiedades del distribuidor** .  
  
## <a name="options"></a>Opciones  
 **Nombre de base de datos de distribución**  
 Escriba el nombre de la base de datos de distribución. El nombre predeterminado de la base de datos de distribución es "distribution". Si especifica un nombre, éste puede tener como máximo 128 caracteres, debe ser único dentro de una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]y debe respetar las reglas para los identificadores. Para obtener más información, vea [Database Identifiers](../databases/database-identifiers.md).  
  
 **Carpeta para el archivo de la base de datos de distribución** y **Carpeta para el archivo de registro de la base de datos de distribución**  
 Escriba la ruta de acceso de la base de datos de distribución y los archivos de registro. Las rutas de acceso deben hacer referencia a discos locales del distribuidor y empezar con una letra de unidad y dos puntos (por ejemplo, C:). No puede utilizar rutas de acceso de redes ni letras de unidades asignadas.  
  
> [!NOTE]  
>  Puede reducir el tiempo que se tarda en escribir las transacciones y mejorar el rendimiento de la replicación si coloca el registro de la base de datos de distribución en una unidad de disco separada de la base de datos de distribución.  
  
## <a name="see-also"></a>Vea también  
 [Configurar distribución](configure-distribution.md)   
 [Configurar la publicación y la distribución](configure-publishing-and-distribution.md)   
 [Ver y modificar las propiedades del distribuidor y del publicador](view-and-modify-distributor-and-publisher-properties.md)  
  
  