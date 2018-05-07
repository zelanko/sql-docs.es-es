---
title: Preparar las bases de datos de acceso para la migración (AccessToSQL) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-access
ms.custom: ''
ms.date: 08/15/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
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
caps.latest.revision: 20
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: 1862e57551ccbc4a41c14c58b1fb0f9de43998d9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="preparing-access-databases-for-migration-accesstosql"></a>Preparar las bases de datos de acceso para la migración (AccessToSQL)
Antes de migrar bases de datos de Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], debe determinar qué bases de datos para migrar y asegúrese de que las bases de datos están listos para la migración.  
  
## <a name="determining-when-to-migrate-to-sql-server"></a>Determinar cuándo se debe migrar a SQL Server  
El motor de base de datos Jet, que se usa como el motor de base de datos para el acceso, es una solución flexible y fácil de usar para la administración de datos. Sin embargo, como las bases de datos mayor y más aplicaciones de misión crítica, muchos usuarios opinan que requieren un mayor rendimiento, la seguridad o la disponibilidad. Para aplicaciones que requieren una plataforma de datos más sólida, considere la posibilidad de mover las bases de datos subyacentes para dichas aplicaciones puedan [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Para obtener más información acerca de cómo decidir cuándo realizar la migración, consulte el [página de información de migración](http://go.microsoft.com/fwlink/?LinkId=68571) en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] sitio Web.  
  
Después de migrar las bases de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], aún puede usar el acceso mediante el uso de tablas vinculadas o puede migrar manualmente sus aplicaciones para [!INCLUDE[msCoName](../../includes/msconame_md.md)] código basado en .NET Framework que interactúa directamente con [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
## <a name="determining-which-databases-to-migrate"></a>Determinar qué bases de datos para migrar  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant (SSMA) para acceso puede localizar las bases de datos de Access para usted. A continuación, puede exportar los metadatos acerca de las bases de datos para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Para obtener más información sobre cómo exportar y consultar los metadatos, vea [exportar un inventario de acceso](http://msdn.microsoft.com/7e1941fb-3d14-4265-aff6-c77a4026d0ed).  

   > [!NOTE]
   > No todas las características de acceso y la configuración son compatibles con, o se puede convertir fácilmente, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Antes de iniciar la migración de bases de datos, consulte [características incompatibles de acceso](http://msdn.microsoft.com/99d45b9c-e3b9-4d56-8c25-b594b887ace1).
  
## <a name="preparing-for-migration"></a>Preparación para la migración  
Utilice las instrucciones siguientes para ayudar a preparar las bases de datos de acceso para la migración a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
### <a name="upgrading-older-access-databases"></a>Actualizar bases de datos de acceso anteriores  
SSMA para Access admite Access 97 y versiones posteriores. Si tiene bases de datos de versiones anteriores de Access, abra y guarde las bases de datos en Access 97 o una versión posterior.  
  
### <a name="removing-workgroup-protection"></a>Quitar la protección del grupo de trabajo  
SSMA no puede migrar las bases de datos que usan la protección del grupo de trabajo. Para quitar la protección de grupo de trabajo de una base de datos de Access, siga los pasos siguientes:  
  
1.  Copie el archivo de base de datos de Access a otra ubicación.  
  
2.  Abra la base de datos copiada.  
  
3.  En el **herramientas** menú, elija **seguridad**y, a continuación, seleccione **permisos de usuario y grupo**.  
  
4.  Seleccione el **usuarios** opción, seleccione la **administración** usuario y, a continuación, asegúrese de que el **administrar** permiso está seleccionado.  
  
5.  Seleccione el **grupos** opción, seleccione el **usuarios** y, a continuación, asegúrese de que el **administrar** permiso está seleccionado.  
  
6.  Haga clic en **Aceptar**y, a continuación, en la **archivo** menú, haga clic en **Exit**.  
  
Ahora puede usar SSMA para migrar la base de datos copiada. Después de cargar el esquema en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], puede proteger manualmente la base de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
### <a name="backing-up-databases"></a>Copia de seguridad de bases de datos  
Antes de migrar las bases de datos de Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], debe realizar copia de seguridad tanto el acceso a bases de datos que va a migrar, así como la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] acceso a las bases de datos en la que va a migrar objetos y datos.  
  
Para realizar la copia de seguridad de una base de datos de Access, en la **herramientas** menú, elija **utilidades de base de datos**y, a continuación, seleccione **copia de seguridad de la base de datos**.  
  
Para obtener información acerca de cómo realizar una copia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] bases de datos, consulte "Backing Up and Restoring Databases en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]" en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] libros en pantalla.  
  
### <a name="documenting-databases"></a>Documentar bases de datos  
También puede documentar las propiedades, como las listas de objetos de base de datos, los tamaños de archivo y los permisos, de las bases de datos de Access. Para generar esta documentación en Access, en la **herramientas** menú, elija **analizar**y, a continuación, haga clic en **documentadas**.  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de Access a SQL Server](http://msdn.microsoft.com/76a3abcf-2998-4712-9490-fe8d872c89ca)  
[Vincular las aplicaciones de Access a SQL Server](http://msdn.microsoft.com/82374ad2-7737-4164-a489-13261ba393d4)
