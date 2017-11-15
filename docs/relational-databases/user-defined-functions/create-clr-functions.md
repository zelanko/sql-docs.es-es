---
title: "Creación funciones CLR | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-udf
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- CLR functions [SQL Server]
- user-defined functions [SQL Server], CLR
ms.assetid: a82df075-2243-4e19-bfe1-ae6d65dabd0f
caps.latest.revision: "34"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 99f9daf70ad70f36d4e6435eaf2230c51d171850
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="create-clr-functions"></a>Crear funciones CLR
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Es posible crear un objeto de base de datos dentro de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] programada en un ensamblado creado en Common Language Runtime (CLR) de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] . Los objetos de bases de datos capaces de aprovechar el modelo enriquecido de programación suministrado por Common Language Runtime son las funciones de agregado, las funciones, los procedimientos almacenados, los desencadenadores y los tipos.  
  
 Para crear una función CLR en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se deben seguir los pasos detallados a continuación:  
  
-   Definir la función como un método estático de una clase en un lenguaje admitido por [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Para obtener más información sobre cómo programar funciones en Common Language Runtime, vea [Funciones CLR definidas por el usuario](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md). A continuación, compilar la clase para generar un ensamblado en [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] mediante el compilador del lenguaje adecuado.  
  
-   Registrar el ensamblado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la instrucción CREATE ASSEMBLY. Para obtener más información sobre ensamblados en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Ensamblados &#40;motor de base de datos&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md).  
  
-   Crear la función que hace referencia al ensamblado registrado mediante la instrucción [CREATE FUNCTION](../../t-sql/statements/create-function-transact-sql.md) .  
  
> [!NOTE]  
>  La implementación de un proyecto de SQL Server en [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] registra un ensamblado en la base de datos especificada para el proyecto. La implementación del proyecto también crea funciones CLR en la base de datos para todos los métodos anotados con el atributo **SqlFunction** . Para más información, consulte [Deploying CLR Database Objects](../../relational-databases/clr-integration/deploying-clr-database-objects.md).  
  
> [!NOTE]  
>  La capacidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para ejecutar el código CLR se encuentra desactivada de manera predeterminada. Puede crear, modificar y quitar objetos de base de datos que hacen referencia a los módulos de códigos administrados, pero estas referencias no se ejecutarán en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a menos que se haya habilitado la opción [clr enabled Option](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) por medio de [sp_configure (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
## <a name="accessing-external-resources"></a>Obtener acceso a recursos externos  
 Las funciones CLR se pueden utilizar para obtener acceso a recursos externos tales como archivos, recursos de red, servicios web y otras bases de datos (incluidas las instancias remotas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]). Para ello, es posible utilizar diversas clases en [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], como por ejemplo `System.IO`, `System.WebServices`, `System.Sql`, etc. El ensamblado que contiene estas funciones debe estar configurado por lo menos con el conjunto de permisos EXTERNAL_ACCESS que tiene este objetivo. Para más información, consulte [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md). El proveedor administrado cliente SQL se puede utilizar para obtener acceso a instancias remotas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No obstante, las conexiones vinculadas en bucles de retorno con el servidor de origen no están admitidas en las funciones CLR.  
  
 **Para crear, modificar o quitar ensamblados de SQL Server**  
  
-   [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)  
  
-   [DROP ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)  
  
 **Para crear una función CLR**  
  
-   [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)  
  
## <a name="accessing-native-code"></a>Acceso a código nativo  
 Las funciones CLR se pueden usar para tener acceso a código nativo (no administrado), como el código escrito en C o C++, a través del uso de PInvoke desde código administrado (vea [Llamar a funciones nativas desde código administrado](http://go.microsoft.com/fwlink/?LinkID=181929) para obtener detalles). Así, puede reutilizar el código heredado como las UDF de CLR, o escribir UDF esenciales para el rendimiento en código nativo. Esto requiere usar un ensamblado UNSAFE. Vea [CLR Integration Code Access Security](../../relational-databases/clr-integration/security/clr-integration-code-access-security.md) para conocer advertencias acerca del uso de ensamblados UNSAFE.  
  
## <a name="see-also"></a>Vea también  
 [Crear funciones definidas por el usuario &#40;motor de base de datos&#41;](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md)   
 [Crear funciones de agregado definidas por el usuario](../../relational-databases/user-defined-functions/create-user-defined-aggregates.md)   
 [Ejecutar funciones definidas por el usuario](../../relational-databases/user-defined-functions/execute-user-defined-functions.md)   
 [Ver funciones definidas por el usuario](../../relational-databases/user-defined-functions/view-user-defined-functions.md)   
 [Conceptos de programación en el ámbito de la integración de Common Language Runtime &#40;CLR&#41;](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
  
  
