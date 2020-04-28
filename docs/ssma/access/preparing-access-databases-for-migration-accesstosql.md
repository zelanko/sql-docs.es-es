---
title: Preparar las bases de datos de Access para la migración (AccessToSQL) | Microsoft Docs
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
ms.openlocfilehash: 58988d31687cacdce2954d8e4098d509a9dcbb2b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68260224"
---
# <a name="preparing-access-databases-for-migration-accesstosql"></a>Preparar las bases de datos de Access para la migración (AccessToSQL)
Antes de migrar las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Access a, debe determinar qué bases de datos se van a migrar y asegurarse de que dichas bases de datos están listas para la migración.  
  
## <a name="determining-when-to-migrate-to-sql-server"></a>Determinar cuándo migrar a SQL Server  
El motor de base de datos Jet, que se utiliza como motor de base de datos para el acceso, es una solución flexible y fácil de usar para la administración de datos. Sin embargo, a medida que las bases de datos se hacen más grandes y más críticas, muchos usuarios descubren que necesitan mayor rendimiento, seguridad o disponibilidad. En el caso de las aplicaciones que requieren una plataforma de datos más sólida, considere la posibilidad de mover las [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]bases de datos subyacentes para esas aplicaciones a. Para obtener más información acerca de cómo decidir cuándo migrar, consulte la página de información [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de [migración](https://go.microsoft.com/fwlink/?LinkId=68571) en el sitio Web.  
  
Después de migrar las bases de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]a, puede seguir usando el acceso mediante el uso de tablas vinculadas, o puede migrar manualmente las [!INCLUDE[msCoName](../../includes/msconame_md.md)] aplicaciones a código basado en .NET Framework que interactúe directamente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]con.  
  
## <a name="determining-which-databases-to-migrate"></a>Determinar las bases de datos que se van a migrar  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Migration Assistant (SSMA) para Access puede ubicar las bases de datos de Access. Después, puede exportar los metadatos de esas bases de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]datos a. Para obtener más información sobre cómo exportar y consultar metadatos, consulte [exportación de un inventario de acceso](exporting-an-access-inventory-accesstosql.md).  

   > [!NOTE]
   > No se admiten todas las características y configuraciones de acceso de, o se pueden convertir [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]fácilmente a. Antes de empezar a migrar las bases de datos, consulte [características de acceso incompatibles](incompatible-access-features-accesstosql.md).
  
## <a name="preparing-for-migration"></a>Preparación de la migración  
Utilice las instrucciones siguientes como ayuda para preparar las bases de datos de Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]la migración a.  
  
### <a name="upgrading-older-access-databases"></a>Actualización de bases de datos de Access anteriores  
SSMA para Access admite el acceso 97 y versiones posteriores. Si tiene bases de datos de versiones anteriores de Access, abra y guarde las bases de datos en Access 97 o una versión posterior.  
  
### <a name="removing-workgroup-protection"></a>Quitar la protección de grupo de trabajo  
SSMA no puede migrar las bases de datos que usan la protección de grupo de trabajo. Para quitar la protección de grupo de trabajo de una base de datos de Access, realice los pasos siguientes:  
  
1.  Copie el archivo de base de datos de Access en otra ubicación.  
  
2.  Abra la base de datos copiada.  
  
3.  En el menú **herramientas** , seleccione **seguridad**y, a continuación, seleccione **permisos de usuario y de grupo**.  
  
4.  Seleccione la opción **usuarios** , seleccione el usuario **Administrador** y asegúrese de que está seleccionado el permiso **administrar** .  
  
5.  Seleccione la opción **grupos** , seleccione el grupo **usuarios** y asegúrese de que está seleccionado el permiso **administrar** .  
  
6.  Haga clic en **Aceptar**y, a continuación, en el menú **archivo** , haga clic en **salir**.  
  
Ahora puede usar SSMA para migrar la base de datos copiada. Después de cargar el esquema en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede proteger manualmente la base de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]en.  
  
### <a name="backing-up-databases"></a>Copias de seguridad de bases de datos  
Antes de migrar las bases de datos de Access [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]a, debe realizar una copia de seguridad de las bases de datos de Access que va a migrar, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] así como de las bases de datos en las que va a migrar los datos y objetos de Access.  
  
Para realizar una copia de seguridad de una base de datos de Access, en el menú **herramientas** , seleccione **utilidades de base de datos**y, a continuación, **copia de seguridad de base de datos**.  
  
Para obtener información acerca de cómo realizar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] copias de seguridad de bases de datos, vea "realizar copias de seguridad y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]restaurar bases [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de datos en" en los libros en pantalla de.  
  
### <a name="documenting-databases"></a>Documentar bases de datos  
También es posible que desee documentar las propiedades, como las listas de objetos de base de datos, los tamaños de archivo y los permisos, de las bases de datos de Access. Para generar esta documentación en Access, en el menú **herramientas** , seleccione **analizar**y, a continuación, haga clic en **documentado**.  
  
## <a name="see-also"></a>Consulte también  
[Migrar bases de datos de Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[Vincular aplicaciones de Access a SQL Server](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)
