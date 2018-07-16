---
title: Administrar servidores mediante administración basada en directivas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- facet See facets
- Declarative Management Framework See Policy-Based Management
- surface area configuration [SQL Server], Policy-Based Management
- Policy-Based Management
- facets [Policy-Based Management]
- Policy-Based Management, administering
- conditions [Policy-Based Management]
- facets [Policy-Based Management], about facets
- PolicyAdministratorRole role
ms.assetid: ef2a7b3b-614b-405d-a04a-2464a019df40
caps.latest.revision: 75
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 85dce54590cfb35286b6939ae9bffdc91f367fbe
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37264461"
---
# <a name="administer-servers-by-using-policy-based-management"></a>Administrar servidores mediante administración basada en directivas
  La administración basada en directivas es un sistema para administrar una o varias instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cuando los administradores de directivas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizan la administración basada en directivas, utilizan [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para crear directivas que permitan administrar las entidades en el servidor, como la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], las bases de datos u otros objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="benefits-of-policy-based-management"></a>Ventajas de la administración basada en directivas  
 La administración basada en directivas resulta útil para resolver los problemas que se presentan en los escenarios siguientes:  
  
-   Una directiva de la compañía prohíbe habilitar Correo electrónico de base de datos o SQL Mail. Una directiva se crea para comprobar el estado del servidor de esas dos características. Un administrador compara el estado del servidor con la directiva. Si el estado del servidor indica que es incompatible, el administrador elige el modo Configurar y la directiva pone el estado del servidor como compatible.  
  
-   La base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] tiene una convención de nomenclatura que requiere que todos los nombres de los procedimientos almacenados comiencen con las letras AW_. Se crea una directiva para aplicar esta convención. Un administrador prueba esta directiva y recibe una lista de procedimientos almacenados que no la cumplen. Si los procedimientos almacenados futuros no obedecen esta convención de nomenclatura, se produce un error en las instrucciones de creación de los procedimientos almacenados.  
  
> [!NOTE]  
>  Tenga en cuenta que las directivas pueden afectar a la forma de funcionamiento de algunas características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por ejemplo, la captura de datos modificados y la replicación transaccional usan ambas la tabla systranschemas, que carece de índice. Si habilita una directiva que indique que todas las tablas deben tener un índice, exigir el cumplimiento de la directiva hará que estas características generen un error.  
  
 Las directivas se crean y se administran por medio de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. El proceso consta de los pasos siguientes:  
  
1.  Seleccione una faceta de administración basada en directivas que contenga las propiedades que se van a configurar.  
  
2.  Defina una condición que especifique el estado de una faceta de administración.  
  
3.  Defina una directiva que contenga la condición, las condiciones adicionales que filtran los conjuntos de destinos y el modo de evaluación.  
  
4.  Compruebe si una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cumple la directiva.  
  
 En las directivas que no se cumplen, el Explorador de objetos indica una advertencia de estado crítico mediante un icono rojo junto al destino y los nodos superiores del árbol del Explorador de objetos.  
  
> [!NOTE]  
>  Cuando el sistema calcula el conjunto de objetos para una directiva, los objetos del sistema se excluyen de forma predeterminada.  Por ejemplo, si el conjunto de objetos de la directiva hace referencia a todas las tablas, la directiva no se aplicará a las tablas del sistema. Si los usuarios desean evaluar una directiva con los objetos del sistema, pueden agregar explícitamente objetos del sistema al conjunto de objetos. Sin embargo, aunque se admiten todas las directivas para el modo de evaluación **Comprobar en la programación** , por razones de rendimiento, no todas las directivas con conjuntos de objetos arbitrarios se admiten para el modo de evaluación **Comprobar en los cambios** . Para obtener más información, consulte: [http://blogs.msdn.com/b/sqlpbm/archive/2009/04/13/policy-evaluation-modes.aspx](http://blogs.msdn.com/b/sqlpbm/archive/2009/04/13/policy-evaluation-modes.aspx)  
  
## <a name="policy-based-management-concepts"></a>Conceptos de la administración basada en directivas  
 La administración basada en directivas tiene tres componentes:  
  
-   Administración de directivas  
  
     Los administradores de directivas crean las directivas.  
  
-   Administración explícita  
  
     Los administradores seleccionan uno o varios destinos administrados y comprueban explícitamente que los destinos cumplan una directiva concreta o hacen que la cumplan.  
  
-   Modos de evaluación  
  
     Hay cuatro modos de evaluación; tres de ellos se pueden automatizar:  
  
    -   **A petición**. Este modo evalúa la directiva cuando lo especifica el usuario directamente.  
  
    -   **Al cambiar: impedir**. Este modo automatizado utiliza desencadenadores DDL para evitar infracciones de las directivas.  
  
        > [!IMPORTANT]  
        >  Si la opción de configuración de servidor de desencadenadores anidados está deshabilitada, **On change: prevent** no funcionará correctamente. La administración basada en directivas se basa en los desencadenadores DDL para detectar y revertir las operaciones DDL que no obedecen a las directivas que utilizan este modo de evaluación. Al quitar los desencadenadores DDL de la administración basada en directivas o deshabilitar los desencadenadores anidados, este modo de evaluación provocará un error o se comportará de forma inesperada.  
  
    -   **Al cambiar: solo registrar**. Este modo automatizado utiliza la notificación de eventos para evaluar una directiva cuando se realiza un cambio relevante.  
  
    -   **Al programar**. Este modo automatizado utiliza un trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para evaluar una directiva periódicamente.  
  
     Cuando las directivas automatizadas no estén habilitadas, la administración basada en directivas no afectará al rendimiento del sistema.  
  
## <a name="policy-based-management-terms"></a>Términos de la administración basada en directivas  
 Destino de la administración basada en directivas  
 Entidades que se administran con la administración basada en directivas, como una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], una base de datos, una tabla o un índice. Todos los destinos de una instancia de servidor forman una jerarquía de destino. Un conjunto de destinos es el resultado de aplicar un conjunto de filtros de destino a la jerarquía de destino, por ejemplo, todas las tablas de la base de datos que es propiedad del esquema HumanResources.  
  
 Faceta de administración basada en directivas  
 Conjunto de propiedades lógicas que modelan el comportamiento o las características de ciertos tipos de destinos administrados. El número y las características de las propiedades están integrados en la faceta y solo el fabricante de la faceta las puede agregar o quitar. Un tipo de destino puede implementar una o varias facetas de administración, y uno o varios tipos de destino pueden implementar una faceta de administración. Algunas propiedades de una faceta solo se pueden aplicar a una versión concreta.  
  
 Condición de la administración basada en directivas  
 Una expresión booleana que especifica un conjunto de estados permitidos de un destino administrado mediante la administración basada en directivas con respecto a una faceta de administración. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intenta observar las intercalaciones al evaluar una condición. Cuando las intercalaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no coinciden exactamente con las intercalaciones de Windows, compruebe su condición para determinar el modo en que el algoritmo resuelve los conflictos.  
  
 Directiva de administración basada en directivas  
 Una condición de administración basada en directivas y el comportamiento esperado, por ejemplo, el modo de evaluación, los filtros de destino y la programación. Una directiva solo puede contener una condición. Las directivas pueden estar habilitadas o deshabilitadas. Las directivas se almacenan en la base de datos msdb.  
  
 Categoría de directiva de administración basada en directivas  
 Categoría definida por el usuario para ayudar a administrar las directivas. Los usuarios pueden clasificar las directivas en categorías diferentes. Una directiva pertenece a una y solo una categoría. Las categorías de directiva se aplican a las bases de datos y servidores. En el nivel de base de datos, se aplican las condiciones siguientes:  
  
-   Los propietarios de base de datos pueden suscribir una base de datos a un conjunto de categorías de directiva.  
  
-   Solo las directivas de sus categorías subscritas pueden gobernar una base de datos.  
  
-   Todas las bases de datos se suscriben implícitamente a la categoría de directiva predeterminada.  
  
 En el nivel de servidor, las categorías de directiva se pueden aplicar a todas las bases de datos.  
  
 Directiva efectiva  
 Las directivas efectivas de un destino son las que lo gobiernan. Una directiva solo es efectiva con respecto a un destino si se satisfacen todas las condiciones siguientes:  
  
-   La directiva está habilitada.  
  
-   El destino pertenece al conjunto de destinos de la directiva.  
  
-   El destino o uno de los antecesores de los destinos se suscribe al grupo de directivas que contiene esta directiva.  
  
## <a name="policy-based-management-tasks"></a>Tareas de administración basada en directivas  
 La administración basada en directivas es un sistema basado en directivas para administrar una o más instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Utilice la administración basada en directivas para crear condiciones que contengan expresiones de condición. A continuación, cree directivas que apliquen las condiciones a los objetos de destino de la base de datos.  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Describe cómo se guardan las directivas de administración basada en directivas.|Almacenamiento de la administración basada en directivas|  
|Describe cómo se configuran alertas para notificar los errores de directiva a los administradores de directivas.|[Configurar alertas para notificar los errores de directiva a los administradores de directivas](configure-alerts-to-notify-policy-administrators-of-policy-failures.md)|  
|Describe cómo se crea, consulta, modifica y elimina una condición de la administración basada en directivas.|[Crear una nueva condición de administración basada en directivas](create-a-new-policy-based-management-condition.md)<br /><br /> [Eliminar una condición de administración basada en directivas](delete-a-policy-based-management-condition.md)<br /><br /> [Ver o modificar las propiedades de una condición de administración basada en directivas](view-or-modify-the-properties-of-a-policy-based-management-condition.md)|  
|Describe cómo se crea, consulta, modifica y elimina una directiva de la administración basada en directivas.|[Crear una directiva de administración basada en directivas](create-a-policy-based-management-policy.md)<br /><br /> [Eliminar una directiva de administración basada en directivas](delete-a-policy-based-management-policy.md)<br /><br /> [Ver o modificar las propiedades de una directiva de administración basada en directivas](view-or-modify-the-properties-of-a-policy-based-management-policy.md)|  
|Describe cómo se exporta e importa una directiva de la administración basada en directivas.|[Exportar una directiva de administración basada en directivas](export-a-policy-based-management-policy.md)<br /><br /> [Importar una directiva de administración basada en directivas](import-a-policy-based-management-policy.md)|  
|Describe cómo se comprueba que una instancia de servidor, una base de datos, un objeto de servidor o un objeto de base de datos cumple la directiva.|[Evaluar una directiva de administración basada en directivas desde un objeto](evaluate-a-policy-based-management-policy-from-an-object.md)<br /><br /> [Evaluar una directiva de administración basada en directivas desde dicha directiva](evaluate-a-policy-based-management-policy-from-that-policy.md)<br /><br /> [Evaluar una directiva de administración basada en directivas según una programación](evaluate-a-policy-based-management-policy-on-a-schedule.md)|  
|Describe cómo se consulta y se copia en un archivo un estado de faceta de administración basada en directivas.|[Trabajar con facetas de administración basada en directivas](working-with-policy-based-management-facets.md)|  
|Proporciona un conjunto de archivos de directivas que puede importar como directivas de procedimientos recomendados y describe cómo se evalúan las directivas con un conjunto de destinos que incluye instancias, objetos de instancia, bases de datos u objetos de base de datos.|[Supervisar y aplicar las prácticas recomendadas usando la administración basada en directivas](monitor-and-enforce-best-practices-by-using-policy-based-management.md)|  
|Proporciona los temas de la Ayuda F1 para el nodo **Administración de directivas** del Explorador de objetos de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].|[Nodo Administración de directivas &#40;Explorador de objetos&#41;](../../ssms/object/object-explorer.md)|  
  
## <a name="see-also"></a>Vea también  
 [Vistas de administración basada en directivas &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/policy-based-management-views-transact-sql)  
  
  
