---
title: Preparar las bases de datos de acceso para la migración (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/15/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases, versions
- Access databases, when to migrate
- Access databases, workgroup security
- backing up databases
- documenting databases
- files, preparing
- migrating databases, versions
- migrating databases, when to migrate
- versions of Access
- workgroup security
ms.assetid: 9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: 9495ff7a58da124255cc6bf5674d92ebeef4c2b0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63299479"
---
# <a name="preparing-access-databases-for-migration-accesstosql"></a>Preparar las bases de datos de acceso para la migración (AccessToSQL)
Antes de migrar bases de datos de Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], debe determinar qué bases de datos para migrar y asegúrese de que esas bases de datos están preparados para la migración.  
  
## <a name="determining-when-to-migrate-to-sql-server"></a>Determinar cuándo realizar la migración a SQL Server  
El motor de base de datos Jet, que se utiliza como el motor de base de datos para el acceso, es una solución flexible y fácil de usar para la administración de datos. Sin embargo, como las bases de datos aumentan de tamaño y más críticas, muchos usuarios encontrar que requieren un mayor rendimiento, seguridad o la disponibilidad. Para las aplicaciones que requieren una plataforma de datos más sólida, considere la posibilidad de mover las bases de datos subyacentes para esas aplicaciones a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información acerca de cómo decidir cuándo realizar la migración, consulte el [página de información de migración](https://go.microsoft.com/fwlink/?LinkId=68571) en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sitio Web.  
  
Después de migrar las bases de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], aún puede usar el acceso mediante el uso de las tablas vinculadas o manualmente puede migrar sus aplicaciones a [!INCLUDE[msCoName](../../includes/msconame_md.md)] código basado en .NET Framework que interactúa directamente con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="determining-which-databases-to-migrate"></a>Determinar qué bases de datos para migrar  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) para el acceso puede localizar las bases de datos de Access para usted. A continuación, puede exportar los metadatos sobre esas bases de datos para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información sobre cómo exportar y consultar los metadatos, vea [exportar un inventario de Access](exporting-an-access-inventory-accesstosql.md).  

   > [!NOTE]
   > No todas las características de acceso y la configuración son compatibles con, o se pueden convertir fácilmente, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Antes de iniciar la migración de bases de datos, vea [características de Access incompatibles](incompatible-access-features-accesstosql.md).
  
## <a name="preparing-for-migration"></a>Preparación para la migración  
Use las directrices siguientes para ayudar a preparar las bases de datos de acceso para la migración a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="upgrading-older-access-databases"></a>Actualizar bases de datos de acceso anterior  
SSMA para Access es compatible con Access 97 y versiones posteriores. Si tiene bases de datos de versiones anteriores de Access, abra y guarde las bases de datos en Access 97 o una versión posterior.  
  
### <a name="removing-workgroup-protection"></a>Quitar la protección del grupo de trabajo  
SSMA no puede migrar las bases de datos que usan la protección del grupo de trabajo. Para quitar la protección de grupo de trabajo de una base de datos de Access, realice los pasos siguientes:  
  
1.  Copie el archivo de base de datos de Access a otra ubicación.  
  
2.  Abra la base de datos copiada.  
  
3.  En el **herramientas** menú, elija **seguridad**y, a continuación, seleccione **permisos de usuario y grupo**.  
  
4.  Seleccione el **usuarios** opción, seleccione el **Admin** usuario y, a continuación, asegúrese de que el **administrar** permiso está seleccionado.  
  
5.  Seleccione el **grupos** opción, seleccione el **usuarios** de grupo y, a continuación, asegúrese de que el **administrar** permiso está seleccionado.  
  
6.  Haga clic en **Aceptar**y, a continuación, en el **archivo** menú, haga clic en **Exit**.  
  
Ahora puede usar SSMA para migrar la base de datos copiada. Después de cargar el esquema en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], para proteger manualmente la base de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="backing-up-databases"></a>La copia de seguridad de bases de datos  
Antes de migrar las bases de datos de Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], debe realizar copias de seguridad tanto el acceso a bases de datos que va a migrar, así como la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] acceso a las bases de datos en la que va a migrar objetos y datos.  
  
Para realizar copias de seguridad de una base de datos de Access, el **herramientas** menú, elija **utilidades de base de datos**y, a continuación, seleccione **copia de seguridad de la base de datos**.  
  
Para obtener información acerca de cómo realizar copias de seguridad [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bases de datos, vea "copia de seguridad y restaurar bases de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]" en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] libros en pantalla.  
  
### <a name="documenting-databases"></a>Documentar bases de datos  
También puede documentar las propiedades, como las listas de objetos de base de datos, los tamaños de archivo y permisos de las bases de datos de Access. Para generar esta documentación en Access, en el **herramientas** menú, elija **analizar**y, a continuación, haga clic en **documentado**.  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[Vinculación de aplicaciones de acceso a SQL Server](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)
