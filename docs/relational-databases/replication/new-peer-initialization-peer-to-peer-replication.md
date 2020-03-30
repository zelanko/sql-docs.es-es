---
title: Inicialización de nuevos nodos del mismo nivel (punto a punto) | Microsoft Docs
description: Describe la "inicialización de nuevos nodos del mismo nivel" que se usa para realizar la replicación punto a punto en SQL Server Management Studio (SSMS).
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.p2pwizard.init.f1
ms.assetid: 050c00e1-78bd-4d9c-affe-40e22feb4d94
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d5841e80156b177d63e5975498a667e3f95cabcd
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "75321922"
---
# <a name="new-peer-initialization-peer-to-peer-replication"></a>Inicialización de nuevos nodos del mismo nivel (replicación punto a punto)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Use la página **Inicialización de nuevos nodos del mismo nivel** para especificar cómo se han inicializado las bases de datos del mismo nivel. (Antes de completar este asistente se deben inicializar las bases de datos del mismo nivel). Las bases de datos del mismo nivel se inicializan manualmente o bien mediante la funcionalidad **initialize with backup** que proporciona la replicación transaccional. (La replicación transaccional punto a punto no permite inicializar bases de datos del mismo nivel mediante una instantánea). Si diferentes bases de datos del mismo nivel se deben inicializar con métodos diferentes, debe agregarlas por separado mediante la ejecución del asistente varias veces.  
  
## <a name="options"></a>Opciones  
 **Especificar cómo se inicializaron las nuevas bases de datos del mismo nivel.**  
 El esquema y los datos correspondientes a todos los objetos publicados deben estar presentes en cada nodo del mismo nivel. Seleccione una de las siguientes opciones:  
  
-   Seleccione la primera opción si ha creado manualmente el esquema de los objetos publicados o si ha restaurado una copia de seguridad pero no se han efectuado cambios en la primera base de datos de publicación desde la creación de la copia de seguridad. Si ha creado el esquema manualmente, debe asegurarse de que todos los datos requeridos estén presentes en cada nodo del mismo nivel. Esta opción corresponde a un valor de **replication support only** para la propiedad de suscripción **sync_type**.  
  
-   Seleccione la segunda opción si ha restaurado una copia de seguridad, y si se han efectuado cambios en la primera base de datos de publicaciones desde la obtención de la copia de seguridad. La replicación debe entregar los cambios desde la primera base de datos de publicaciones que no se incluyeron en la copia de seguridad. Esta opción corresponde a un valor de **initialize with backup** para la propiedad de suscripción **sync_type**.  
  
     Cuando se habilita una publicación para una replicación punto a punto, se establece la propiedad de publicación **ayos_initialize_from_backup** . La replicación empieza inmediatamente a realizar el seguimiento de los cambios en la primera base de datos de publicación. Por tanto, estos cambios se pueden entregar a una base de datos restaurada en uno o más pares si la opción **initialize with backup** está seleccionada. Haga clic en el botón **Examinar** para localizar la copia de seguridad utilizada; la replicación leerá el número de secuencia de registro (LSN) de la copia de seguridad. Todos los cambios efectuados en la primera base de datos de publicación que tengan un LSN más alto se entregarán a cada nodo del mismo nivel.  
  
     Es posible que esta opción no esté disponible si la creación o la agregación se realizan en una topología que incluye [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. La tabla siguiente muestra si la opción está disponible al agregar un nodo a una topología existente.  
  
    |Nuevo nodo|Primer nodo|Nodos adicionales|Opción|  
    |--------------|----------------|----------------------|------------|  
    |[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|Disabled|  
    |[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|None|Disabled|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|Disabled|  
    |[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|None|habilitado|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|None|habilitado|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|habilitado|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|None|habilitado|  
  
## <a name="see-also"></a>Consulte también  
 [Administrar una topología punto a punto &#40;programación de la replicación con Transact-SQL&#41;](../../relational-databases/replication/administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  
