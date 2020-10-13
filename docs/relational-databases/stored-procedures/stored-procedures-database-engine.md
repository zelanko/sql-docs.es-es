---
title: Procedimientos almacenados (motor de base de datos) | Microsoft Docs
description: Aquí descubrirá que un procedimiento almacenado de SQL Server es un grupo de una o varias instrucciones Transact-SQL o una referencia a un método de Common Runtime Language de .NET Framework.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- storing programs as stored procedures
- stored procedures [SQL Server], about stored procedures
ms.assetid: cc6daf62-9663-4c3e-950a-ab42e2830427
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1ea9a185b1f7a00c8e6ea7e6d848cf2b4e88319f
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/07/2020
ms.locfileid: "91809631"
---
# <a name="stored-procedures-database-engine"></a>Procedimientos almacenados (motor de base de datos)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  Un procedimiento almacenado de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es un grupo de una o más instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] o una referencia a un método de Common Runtime Language (CLR) de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Los procedimientos se asemejan a las construcciones de otros lenguajes de programación, porque pueden:  
  
-   Aceptar parámetros de entrada y devolver varios valores en forma de parámetros de salida al programa que realiza la llamada.  
  
-   Contener instrucciones de programación que realicen operaciones en la base de datos. Entre otras, pueden contener llamadas a otros procedimientos.  
  
-   Devolver un valor de estado a un programa que realiza una llamada para indicar si la operación se ha realizado correctamente o se han producido errores, y el motivo de estos.  
  
## <a name="benefits-of-using-stored-procedures"></a>Ventajas de usar procedimientos almacenados  
 En la siguiente lista se describen algunas de las ventajas que brinda el uso de procedimientos.  
  
 Tráfico de red reducido entre el cliente y el servidor  
 Los comandos de un procedimiento se ejecutan en un único lote de código. Esto puede reducir significativamente el tráfico de red entre el servidor y el cliente porque únicamente se envía a través de la red la llamada que va a ejecutar el procedimiento. Sin la encapsulación de código que proporciona un procedimiento, cada una de las líneas de código tendría que enviarse a través de la red.  
  
 Mayor seguridad  
 Varios usuarios y programas cliente pueden realizar operaciones en los objetos de base de datos subyacentes a través de un procedimiento, aunque los usuarios y los programas no tengan permisos directos sobre esos objetos subyacentes. El procedimiento controla qué procesos y actividades se llevan a cabo y protege los objetos de base de datos subyacentes. Esto elimina la necesidad de conceder permisos en cada nivel de objetos y simplifica los niveles de seguridad.  
  
 La cláusula [EXECUTE AS](../../t-sql/statements/execute-as-clause-transact-sql.md) puede especificarse en la instrucción CREATE PROCEDURE para habilitar la suplantación de otro usuario o para permitir que los usuarios o las aplicaciones puedan realizar ciertas actividades en la base de datos sin necesidad de contar con permisos directos sobre los objetos y comandos subyacentes. Por ejemplo, algunas acciones como TRUNCATE TABLE no tienen permisos que se puedan conceder. Para poder ejecutar TRUNCATE TABLE, el usuario debe tener permisos ALTER en la tabla especificada. Puede que la concesión de permisos ALTER a un usuario en una tabla no sea lo ideal, pues en realidad el usuario tendrá permisos muy superiores a la posibilidad de truncar una tabla. Si se incorpora la instrucción TRUNCATE TABLE en un módulo y se especifica la ejecución del módulo como un usuario con permisos para modificar la tabla, se pueden ampliar los permisos para truncar la tabla al usuario al que se concedan permisos EXECUTE para el módulo.  
  
 Al llamar a un procedimiento a través de la red, solo está visible la llamada que va a ejecutar el procedimiento. Por lo tanto, los usuarios malintencionados no pueden ver los nombres de los objetos de base de datos y tabla, incrustados en sus propias instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] , ni buscar datos críticos.  
  
 El uso de parámetros de procedimientos ayuda a protegerse contra ataques por inyección de código SQL. Dado que la entrada de parámetros se trata como un valor literal y no como código ejecutable, resulta más difícil para un atacante insertar un comando en la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] del procedimiento y comprometer la seguridad.  
  
 Los procedimientos pueden cifrarse, lo que ayuda a ofuscar el código fuente. Para más información, consulte [SQL Server Encryption](../../relational-databases/security/encryption/sql-server-encryption.md).  
  
 Reutilización del código  
 El código de cualquier operación de base de datos redundante resulta un candidato perfecto para la encapsulación de procedimientos. De este modo, se elimina la necesidad de escribir de nuevo el mismo código, se reducen las inconsistencias de código y se permite que cualquier usuario o aplicación que cuente con los permisos necesarios pueda acceder al código y ejecutarlo.  
  
 Mantenimiento más sencillo  
 Cuando las aplicaciones cliente llaman a procedimientos y mantienen las operaciones de base de datos en la capa de datos, solo deben actualizarse los cambios de los procesos en la base de datos subyacente. El nivel de aplicación permanece independiente y no tiene que tener conocimiento sobre los cambios realizados en los diseños, las relaciones o los procesos de la base de datos.  
  
 rendimiento mejorado.  
 De forma predeterminada, un procedimiento se compila la primera vez que se ejecuta y crea un plan de ejecución que vuelve a usarse en posteriores ejecuciones. Como el procesador de consultas no tiene que crear un nuevo plan, normalmente necesita menos tiempo para procesar el procedimiento.  
  
 Si ha habido cambios importantes en las tablas o datos a los que se hace referencia en el procedimiento, el plan precompilado podría hacer que el procedimiento se ejecutara con mayor lentitud. En este caso, volver a crear el procedimiento y forzar un nuevo plan de ejecución puede mejorar el rendimiento.  
  
## <a name="types-of-stored-procedures"></a>Tipos de procedimientos almacenados  

 **Definidos por el usuario**  
 Un procedimiento definido por el usuario se puede crear en una base de datos definida por el usuario o en todas las bases de datos del sistema excepto en la base de datos **Resource** . El procedimiento se puede desarrollar en [!INCLUDE[tsql](../../includes/tsql-md.md)] o como una referencia a un método de Common Runtime Language (CLR) de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].  
  
 **Temporales**  
 Los procedimientos temporales son una forma de procedimientos definidos por el usuario. Los procedimientos temporales son iguales que los procedimientos permanentes salvo porque se almacenan en **tempdb**. Hay dos tipos de procedimientos temporales: locales y globales. Se diferencian entre sí por los nombres, la visibilidad y la disponibilidad. Los procedimientos temporales locales tienen como primer carácter de sus nombres un solo signo de número (#); solo son visibles en la conexión actual del usuario y se eliminan cuando se cierra la conexión. Los procedimientos temporales globales presentan dos signos de número (##) antes del nombre; son visibles para cualquier usuario después de su creación y se eliminan al final de la última sesión en la que se usa el procedimiento.  
  
 **Sistema**  
 Los procedimientos del sistema se incluyen con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Están almacenados físicamente en la base de datos interna y oculta **Resource** y se muestran de forma lógica en el esquema **sys** de cada base de datos definida por el sistema y por el usuario. Además, la base de datos **msdb** también contiene procedimientos almacenados del sistema en el esquema **dbo** que se usan para programar alertas y trabajos. Dado que los procedimientos del sistema empiezan con el prefijo **sp_** , le recomendamos que no use este prefijo cuando asigne un nombre a los procedimientos definidos por el usuario. Para obtener una lista completa de los procedimientos del sistema, vea [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite los procedimientos del sistema que proporcionan una interfaz de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a los programas externos para varias actividades de mantenimiento. Estos procedimientos extendidos usan el prefijo xp_. Para obtener una lista completa de los procedimientos extendidos, vea [Procedimientos almacenados extendidos generales &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md).  
  
 **Extendidos definidos por el usuario**  
 Los procedimientos extendidos le permiten crear sus propias rutinas externas en un lenguaje de programación como puede ser C. Estos procedimientos son DLL que una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede cargar y ejecutar dinámicamente.  
  
> [!NOTE]  
>  Los procedimientos almacenados extendidos se quitarán en una versión futura de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No utilice esta característica en nuevos trabajos de desarrollo y modifique lo antes posible las aplicaciones que actualmente la utilizan. Cree en su lugar procedimientos CLR. Este método constituye una alternativa más consolidada y segura para escribir procedimientos extendidos.  
  
## <a name="related-tasks"></a>Related Tasks  
  
| Descripción de la tarea | Tema |
| ---------------- | ----- |
|Describe cómo se crea un procedimiento almacenado.|[Crear un procedimiento almacenado](../../relational-databases/stored-procedures/create-a-stored-procedure.md)|  
|Describe cómo se modifica un procedimiento almacenado.|[Modificar un procedimiento almacenado](../../relational-databases/stored-procedures/modify-a-stored-procedure.md)|  
|Describe cómo se elimina un procedimiento almacenado.|[Eliminar un procedimiento almacenado](../../relational-databases/stored-procedures/delete-a-stored-procedure.md)|  
|Describe cómo se ejecuta un procedimiento almacenado.|[Ejecutar un procedimiento almacenado](../../relational-databases/stored-procedures/execute-a-stored-procedure.md)|  
|Describe cómo se conceden permisos en un procedimiento almacenado.|[Conceder permisos para un procedimiento almacenado](../../relational-databases/stored-procedures/grant-permissions-on-a-stored-procedure.md)|  
|Describe cómo se devuelven datos de un procedimiento almacenado a una aplicación.|[Devolver datos de un procedimiento almacenado](../../relational-databases/stored-procedures/return-data-from-a-stored-procedure.md)|  
|Describe cómo se recompila un procedimiento almacenado.|[Volver a compilar un procedimiento almacenado](../../relational-databases/stored-procedures/recompile-a-stored-procedure.md)|  
|Describe cómo se cambia el nombre de un procedimiento almacenado.|[Cambiar el nombre de un procedimiento almacenado](../../relational-databases/stored-procedures/rename-a-stored-procedure.md)|  
|Describe cómo se consulta la definición de un procedimiento almacenado.|[Ver la definición de un procedimiento almacenado](../../relational-databases/stored-procedures/view-the-definition-of-a-stored-procedure.md)|  
|Describe cómo se consultan las dependencias de un procedimiento almacenado.|[Ver las dependencias de un procedimiento almacenado](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md)|  
|Describe cómo se usan los parámetros en un procedimiento almacenado.|[Parámetros](../../relational-databases/stored-procedures/parameters.md)|  
  
## <a name="related-content"></a>Contenido relacionado  
 [Procedimientos almacenados de CLR](/dotnet/framework/data/adonet/sql/clr-stored-procedures)  
 [Resolución diferida de nombres](../../t-sql/statements/create-trigger-transact-sql.md#deferred-name-resolution)
