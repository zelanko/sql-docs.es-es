---
title: Implementar ensamblados | Documentos de Microsoft
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- assemblies [CLR integration], implementing
ms.assetid: c228d7bf-a906-4f37-a057-5d464d962ff8
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3739ec98683810b683bf644912268d22efe6e261
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="assemblies---implementing"></a>Ensamblados - implementación
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
En este tema se proporciona información acerca de las áreas siguientes para ayudarle a implementar ensamblados y trabajar con ellos en la base de datos:  
  
-   Crear ensamblados  
  
-   Modificar ensamblados  
  
-   Quitar, deshabilitar y habilitar ensamblados  
  
-   Administración de versiones de ensamblado  
  
## <a name="creating-assemblies"></a>Crear ensamblados  
 Los ensamblados se crean en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la instrucción CREATE ASSEMBLY de [!INCLUDE[tsql](../../includes/tsql-md.md)], o bien en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] mediante el editor asistido de ensamblados. Además, un proyecto de SQL Server en la implementación [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] registra un ensamblado en la base de datos que se especificó para el proyecto. Para más información, consulte [Deploying CLR Database Objects](../../relational-databases/clr-integration/deploying-clr-database-objects.md).  
  
 **Para crear un ensamblado mediante Transact-SQL**  
  
-   [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)  
  
 **Para crear un ensamblado mediante SQL Server Management Studio**  
  
-   [Propiedades del ensamblado &#40; Página general &#41;](../../relational-databases/clr-integration/assemblies-properties.md)  
  
## <a name="modifying-assemblies"></a>Modificar ensamblados  
 Los ensamblados se modifican en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la instrucción ALTER ASSEMBLY de [!INCLUDE[tsql](../../includes/tsql-md.md)], o bien en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] mediante el editor asistido de ensamblados. Se puede modificar un ensamblado cuando se desea hacer lo siguiente:    
  
-   Cambiar la implementación del ensamblado cargando una versión más reciente de los binarios del ensamblado. Para obtener más información, consulte [administrar versiones de ensamblados](#_managing) más adelante en este tema.  
  
-   Cambiar el conjunto de permisos del ensamblado. Para obtener más información, consulte [diseñar ensamblados](../../relational-databases/clr-integration/assemblies-designing.md).  
  
-   Cambiar la visibilidad del ensamblado. Los ensamblados visibles están disponibles para hacer referencia a los mismos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los invisibles no están disponibles, aunque se hayan cargado en la base de datos. De forma predeterminada, los ensamblados cargados en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] son visibles.  
  
-   Agregar o quitar un archivo de depuración o de origen asociado con el ensamblado.  
  
 **Para modificar un ensamblado mediante Transact-SQL**  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)  
  
 **Para modificar un ensamblado mediante SQL Server Management Studio**  
  
-   [Propiedades del ensamblado &#40; Página general &#41;](../../relational-databases/clr-integration/assemblies-properties.md)  
  
## <a name="dropping-disabling-and-enabling-assemblies"></a>Quitar, deshabilitar y habilitar ensamblados  
 Los ensamblados se quitan mediante la instrucción DROP ASSEMBLY de [!INCLUDE[tsql](../../includes/tsql-md.md)] o mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Para quitar un ensamblado mediante Transact-SQL**  
  
-   [DROP ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)  
  
 **Para quitar un ensamblado mediante SQL Server Management Studio**  
  
-   [Eliminar objetos](http://msdn.microsoft.com/library/49541441-179c-40d3-ba0c-01bcae545984)  
  
 De forma predeterminada, ningún ensamblado creado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se puede ejecutar. Puede usar el **clr habilitado** opción de la **sp_configure** procedimiento para deshabilitar o habilitar la ejecución de todos los ensamblados que se cargan en almacenado del sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Al deshabilitar la ejecución de ensamblados se impide la ejecución de funciones, procedimientos almacenados, desencadenadores, agregados y tipos definidos por el usuario CLR (Common Language Runtime), y se detienen los que se están ejecutando. El hecho de deshabilitar la ejecución no deshabilita la capacidad de crear, alterar o quitar ensamblados. Para obtener más información, consulte [clr enabled (opción) de configuración de servidor](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md).  
  
 **Para deshabilitar y habilitar la ejecución de ensamblado**  
  
-   [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
##  <a name="_managing"></a>Administración de versiones de ensamblado  
 Cuando un ensamblado se carga en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se almacena y administra en los catálogos de sistema de la base de datos. Los cambios realizados en la definición del ensamblado en el [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] debería propagar al ensamblado que se almacena en el catálogo de base de datos.  
  
 Si desea modificar un ensamblado, debe emitir una instrucción ALTER ASSEMBLY para actualizar el ensamblado en la base de datos. De este modo se actualizará el ensamblado a la copia más reciente de los módulos [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] que almacenan su implementación.  
  
 La cláusula WITH UNCHECKED DATA de la instrucción ALTER ASSEMBLY indica a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que actualice incluso los ensamblados de los que dependen los datos almacenados en la base de datos. En concreto, se debe especificar WITH UNCHECKED DATA si existe alguno de los elementos siguientes:    
  
-   Columnas calculadas persistentes que hacen referencia a métodos del ensamblado, ya sea directa o indirectamente, mediante funciones o métodos de [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   Columnas de un tipo definido por el usuario CLR que dependan del ensamblado y el tipo implementa una **UserDefined** (no -**nativo**) formato de serialización.  
  
> [!CAUTION]  
>  Si no se especifica WITH UNCHECKED DATA, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intentará evitar que ALTER ASSEMBLY se ejecute si la nueva versión de ensamblado afecta a los datos existentes de tablas, índices u otros sitios permanentes. Sin embargo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no garantiza que las columnas calculadas, los índices, las vistas indizadas o las expresiones sean coherentes con rutinas y tipos subyacentes cuando el ensamblado CLR se actualice. Al ejecutar ALTER ASSEMBLY, tenga cuidado de que no se produzcan discrepancias entre el resultado de una expresión y los valores basados en esa expresión almacenada en el ensamblado.  
  
 Solo los miembros de la **db_owner** y **db_ddlowner** rol fijo de base de datos puede ejecutar ALTER ASSEMBLY de ejecución mediante la cláusula WITH UNCHECKED DATA.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] envía un mensaje al registro de eventos de aplicación de Windows que se ha modificado el ensamblado con datos no comprobados en las tablas. A continuación, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] indica que las tablas que contienen datos que dependen del ensamblado tienen datos no comprobados. El **has_unchecked_assembly_data** columna de la **sys.tables** vista de catálogo contiene el valor 1 para las tablas que contienen datos no comprobados y 0 para las tablas sin datos no comprobados.  
  
 Para resolver la integridad de datos no comprobados, ejecute DBCC CHECKDB WITH EXTENDED_LOGICAL_CHECKS en cada tabla que tiene datos no comprobados. Si se produce un error de DBCC CHECKDB WITH EXTENDED_LOGICAL_CHECKS, debe eliminar las filas de tabla que no son válidas o modificar el código de ensamblado para solucionar los problemas y, a continuación, emita las instrucciones ALTER ASSEMBLY adicionales.  
  
 ALTER ASSEMBLY cambia la versión de ensamblado. La referencia cultural y el token de clave pública del ensamblado siguen siendo los mismos. SQL Server no permite registrar distintas versiones de un ensamblado con el mismo nombre, referencia cultural y clave pública.  
  
### <a name="interactions-with-computer-wide-policy-for-version-binding"></a>Interacciones con la directiva de equipos para los enlaces de versión  
 Si las referencias a ensamblados almacenados en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se redirigen a versiones determinadas mediante una directiva de edición o una directiva de administrador de equipos, debe realizar una de las acciones siguientes:    
  
-   Asegúrese de que la nueva versión a la que se redirigen las referencias se encuentra en la base de datos.  
  
-   Modifique las instrucciones de los archivos de directivas externas del equipo o la directiva de edición para asegurarse de que hacen referencia a la versión específica que se encuentra en la base de datos.  
  
 De lo contrario, los intentos de carga de una nueva versión de ensamblado en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provocarán errores.  
  
 **Para actualizar la versión de un ensamblado**  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)  
  
## <a name="see-also"></a>Vea también  
 [Ensamblados &#40; motor de base de datos &#41;](../../relational-databases/clr-integration/assemblies-database-engine.md)   
 [Obtener información acerca de los ensamblados](../../relational-databases/clr-integration/assemblies-getting-information.md)  
  
  
