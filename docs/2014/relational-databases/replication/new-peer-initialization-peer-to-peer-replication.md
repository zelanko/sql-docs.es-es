---
title: Inicialización de nuevos nodos del mismo nivel (replicación punto a punto) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.p2pwizard.init.f1
ms.assetid: 050c00e1-78bd-4d9c-affe-40e22feb4d94
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 51e5ec3832d497f342c4fc3132a75261f6c3c154
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63022687"
---
# <a name="new-peer-initialization-peer-to-peer-replication"></a>Inicialización de nuevos nodos del mismo nivel (replicación punto a punto)
  Use la página **nueva inicialización del mismo nivel** para especificar cómo se inicializaron las bases de datos del mismo nivel. (Los elementos del mismo nivel se deben inicializar antes de completar este asistente). Los elementos del mismo nivel se inicializan manualmente o mediante la funcionalidad **Initialize with backup** que proporciona la replicación transaccional. (La replicación transaccional punto a punto no admite la inicialización de elementos del mismo nivel mediante una instantánea). Si se deben inicializar diferentes pares con métodos diferentes, debe agregar los elementos del mismo nivel por separado mediante la ejecución del asistente varias veces.  
  
## <a name="options"></a>Opciones  
 **Especificar cómo se inicializaron las nuevas bases de datos del mismo nivel**  
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
 [Administrar una topología punto a punto &#40;programación de la replicación con Transact-SQL&#41;](administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [Peer-to-Peer Transactional Replication](transactional/peer-to-peer-transactional-replication.md)  
  
  
