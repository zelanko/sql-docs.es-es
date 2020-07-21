---
title: Implementar ensamblados | Microsoft Docs
description: Obtenga información sobre cómo trabajar con ensamblados hospedados en SQL Server, incluido cómo crear o modificar ensamblados, quitar o habilitar o deshabilitar ensamblados y administrar versiones.
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- assemblies [CLR integration], implementing
ms.assetid: c228d7bf-a906-4f37-a057-5d464d962ff8
author: rothja
ms.author: jroth
ms.openlocfilehash: 8d97ef8c7dfc617cb6cd56dbcc6d83e0540051d7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85695360"
---
# <a name="assemblies---implementing"></a>Ensamblados: implementación
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  En este tema se proporciona información acerca de las áreas siguientes para ayudarle a implementar ensamblados y trabajar con ellos en la base de datos:  
  
-   Crear ensamblados  
  
-   Modificar ensamblados  
  
-   Quitar, deshabilitar y habilitar ensamblados  
  
-   Administrar versiones de ensamblado  
  
## <a name="creating-assemblies"></a>Crear ensamblados  
 Los ensamblados se crean en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la instrucción CREATE ASSEMBLY de [!INCLUDE[tsql](../../includes/tsql-md.md)], o bien en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] mediante el editor asistido de ensamblados. Además, al implementar un proyecto de SQL Server en, [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] se registra un ensamblado en la base de datos que se especificó para el proyecto. Para más información, consulte [Deploying CLR Database Objects](../../relational-databases/clr-integration/deploying-clr-database-objects.md).  
  
 **Para crear un ensamblado mediante Transact-SQL**  
  
-   [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)  
  
 **Para crear un ensamblado mediante SQL Server Management Studio**  
  
-   [Propiedades de ensamblado &#40;página general&#41;](../../relational-databases/clr-integration/assemblies-properties.md)  
  
## <a name="modifying-assemblies"></a>Modificar ensamblados  
 Los ensamblados se modifican en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la instrucción ALTER ASSEMBLY de [!INCLUDE[tsql](../../includes/tsql-md.md)], o bien en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] mediante el editor asistido de ensamblados. Se puede modificar un ensamblado cuando se desea hacer lo siguiente:    
  
-   Cambiar la implementación del ensamblado cargando una versión más reciente de los binarios del ensamblado. Para obtener más información, vea [administrar versiones de ensamblados](#_managing) más adelante en este tema.  
  
-   Cambiar el conjunto de permisos del ensamblado. Para obtener más información, vea [Diseño de ensamblados](../../relational-databases/clr-integration/assemblies-designing.md).  
  
-   Cambiar la visibilidad del ensamblado. Los ensamblados visibles están disponibles para hacer referencia a los mismos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los invisibles no están disponibles, aunque se hayan cargado en la base de datos. De forma predeterminada, los ensamblados cargados en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] son visibles.  
  
-   Agregar o quitar un archivo de depuración o de origen asociado con el ensamblado.  
  
 **Para modificar un ensamblado mediante Transact-SQL**  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)  
  
 **Para modificar un ensamblado mediante SQL Server Management Studio**  
  
-   [Propiedades de ensamblado &#40;página general&#41;](../../relational-databases/clr-integration/assemblies-properties.md)  
  
## <a name="dropping-disabling-and-enabling-assemblies"></a>Quitar, deshabilitar y habilitar ensamblados  
 Los ensamblados se quitan mediante la instrucción DROP ASSEMBLY de [!INCLUDE[tsql](../../includes/tsql-md.md)] o mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Para quitar un ensamblado mediante Transact-SQL**  
  
-   [DROP ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)  
  
 **Para quitar un ensamblado mediante SQL Server Management Studio**  
  
-   [Eliminar objetos](../../ssms/object/delete-objects.md)  
  
 De forma predeterminada, ningún ensamblado creado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se puede ejecutar. Puede usar la opción **clr enabled** del **sp_configure** procedimiento almacenado del sistema para deshabilitar o habilitar la ejecución de todos los ensamblados que se cargan en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Al deshabilitar la ejecución de ensamblados se impide la ejecución de funciones, procedimientos almacenados, desencadenadores, agregados y tipos definidos por el usuario CLR (Common Language Runtime), y se detienen los que se están ejecutando. El hecho de deshabilitar la ejecución no deshabilita la capacidad de crear, alterar o quitar ensamblados. Para obtener más información, vea [clr enabled (opción de configuración del servidor](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)).  
  
 **Para deshabilitar y habilitar la ejecución de ensamblados**  
  
-   [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
##  <a name="managing-assembly-versions"></a><a name="_managing"></a>Administrar versiones de ensamblado  
 Cuando un ensamblado se carga en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se almacena y administra en los catálogos de sistema de la base de datos. Cualquier cambio realizado en la definición del ensamblado en el [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] debe propagarse al ensamblado que se almacena en el catálogo de la base de datos.  
  
 Si desea modificar un ensamblado, debe emitir una instrucción ALTER ASSEMBLY para actualizar el ensamblado en la base de datos. De este modo se actualizará el ensamblado a la copia más reciente de los módulos [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] que almacenan su implementación.  
  
 La cláusula WITH UNCHECKED DATA de la instrucción ALTER ASSEMBLY indica a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que actualice incluso los ensamblados de los que dependen los datos almacenados en la base de datos. En concreto, se debe especificar WITH UNCHECKED DATA si existe alguno de los elementos siguientes:    
  
-   Columnas calculadas persistentes que hacen referencia a métodos del ensamblado, ya sea directa o indirectamente, mediante funciones o métodos de [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   Columnas con el tipo CLR definido por el usuario que dependen del ensamblado, y el tipo implementa un formato de serialización **UserDefined** (distinto de **Native**).  
  
> [!CAUTION]  
>  Si no se especifica WITH UNCHECKED DATA, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intentará evitar que ALTER ASSEMBLY se ejecute si la nueva versión de ensamblado afecta a los datos existentes de tablas, índices u otros sitios permanentes. Sin embargo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no garantiza que las columnas calculadas, los índices, las vistas indizadas o las expresiones sean coherentes con rutinas y tipos subyacentes cuando el ensamblado CLR se actualice. Al ejecutar ALTER ASSEMBLY, tenga cuidado de que no se produzcan discrepancias entre el resultado de una expresión y los valores basados en esa expresión almacenada en el ensamblado.  
  
 Solo los miembros del rol fijo de base de datos **db_owner** y **DB_DDLOWNER** pueden ejecutar Alter Assembly mediante la cláusula with unchecked Data.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] expone un mensaje al registro de eventos de aplicación Windows en el que indica que se ha modificado el ensamblado con datos no comprobados en las tablas. A continuación, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] indica que las tablas que contienen datos que dependen del ensamblado tienen datos no comprobados. La **has_unchecked_assembly_data** columna de la vista de catálogo **Sys. Tables** contiene el valor 1 para las tablas que contienen datos no comprobados y 0 para las tablas sin datos no comprobados.  
  
 Para resolver la integridad de los datos no comprobados, ejecute DBCC CHECKDB con EXTENDED_LOGICAL_CHECKS en cada tabla que tenga datos no comprobados. Si se produce un error en DBCC CHECKDB con EXTENDED_LOGICAL_CHECKS, debe eliminar las filas de la tabla que no son válidas o modificar el código de ensamblado para solucionar los problemas y, a continuación, emitir instrucciones ALTER ASSEMBLy adicionales.  
  
 ALTER ASSEMBLY cambia la versión de ensamblado. La referencia cultural y el token de clave pública del ensamblado siguen siendo los mismos. SQL Server no permite registrar distintas versiones de un ensamblado con el mismo nombre, referencia cultural y clave pública.  
  
### <a name="interactions-with-computer-wide-policy-for-version-binding"></a>Interacciones con la directiva de equipos para los enlaces de versión  
 Si las referencias a ensamblados almacenados en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se redirigen a versiones determinadas mediante una directiva de edición o una directiva de administrador de equipos, debe realizar una de las acciones siguientes:    
  
-   Asegúrese de que la nueva versión a la que se redirigen las referencias se encuentra en la base de datos.  
  
-   Modifique las instrucciones de los archivos de directivas externas del equipo o la directiva de edición para asegurarse de que hacen referencia a la versión específica que se encuentra en la base de datos.  
  
 De lo contrario, los intentos de carga de una nueva versión de ensamblado en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provocarán errores.  
  
 **Para actualizar la versión de un ensamblado**  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ensamblados &#40;Motor de base de datos&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md)   
 [Obtener información acerca de los ensamblados](../../relational-databases/clr-integration/assemblies-getting-information.md)  
  
  
