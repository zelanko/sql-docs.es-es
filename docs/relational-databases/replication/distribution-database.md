---
title: Base de datos de distribución | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.configuredistributionwizard.distributiondatabase.f1
ms.assetid: 5b42a083-7a11-41d8-9e3f-320c7c907237
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 9f86ef648812c553a2445afac6a50f03824e8e72
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "76284560"
---
# <a name="distribution-database"></a>Base de datos de distribución
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  En la base de datos de distribución se almacenan metadatos y datos del historial de todos los tipos de replicación y transacciones de replicación transaccional.  
  
 En muchas ocasiones, una sola base de datos de distribución resulta suficiente. No obstante, si varios publicadores utilizan un único distribuidor, considere la posibilidad de crear una base de datos de distribución para cada publicador. De esta forma, se garantiza que los datos que pasan por cada base de datos de distribución son distintos. Para especificar una base de datos de distribución para el distribuidor, puede utilizar el Asistente para configurar la distribución. Si es necesario, especifique bases de datos de distribución adicionales en el cuadro de diálogo **Propiedades del distribuidor** .  
  
## <a name="options"></a>Opciones  
 **Nombre de base de datos de distribución**  
 Escriba el nombre de la base de datos de distribución. El nombre predeterminado de la base de datos de distribución es "distribution". Si especifica un nombre, este puede tener como máximo 128 caracteres, debe ser único dentro de una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y debe respetar las reglas de los identificadores. Para obtener más información, vea [Database Identifiers](../../relational-databases/databases/database-identifiers.md).  
  
 **Carpeta para el archivo de la base de datos de distribución** y **Carpeta para el archivo de registro de la base de datos de distribución**  
 Escriba la ruta de acceso de la base de datos de distribución y los archivos de registro. Las rutas de acceso deben hacer referencia a discos locales del distribuidor y empezar con una letra de unidad y dos puntos (por ejemplo, C:). No puede utilizar rutas de acceso de redes ni letras de unidades asignadas.  
  
> [!NOTE]  
>  Puede reducir el tiempo que se tarda en escribir las transacciones y mejorar el rendimiento de la replicación si coloca el registro de la base de datos de distribución en una unidad de disco separada de la base de datos de distribución.  
  
## <a name="see-also"></a>Consulte también  
 [Configurar distribución](../../relational-databases/replication/configure-distribution.md)   
 [Configurar la publicación y la distribución](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Ver y modificar las propiedades del distribuidor y del publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)  
  
  
