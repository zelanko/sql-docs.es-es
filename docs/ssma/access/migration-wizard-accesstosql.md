---
title: Asistente para la migración (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Migration Wizard dialog box
- Migration Wizard, adding Access databases
- Migration Wizard, Connect to SQL Azure
- Migration Wizard, Connect to SQL Server
- Migration Wizard, Link Tables
- Migration Wizard, Migration status
- Migration Wizard, New Project
- Migration Wizard, Selecting objects to migrate
ms.assetid: 5bab5914-b2ae-4795-8cf5-83e42d64bef2
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 0c77ff9dae7d6d700289cdff4daff56ba4457651
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47636203"
---
# <a name="migration-wizard-accesstosql"></a>Asistente para la migración (AccessToSQL)
El Asistente para migración le guía a través de la migración de una o varias bases de datos de Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. Mediante el Asistente para crear un proyecto, agregará las bases de datos al proyecto, seleccionar objetos para migrar y conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. También se convertir, cargar y migrar datos y esquemas de acceso. Si lo desea, puede vincular las tablas de Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tablas o SQL Azure.  
  
La mayoría de las páginas del Asistente de migración contienen las mismas opciones que los cuadros de diálogo SSMA existentes. Por lo tanto, aquí se describen las páginas del asistente y, a continuación, se proporcionan vínculos para que puede obtener más información acerca de las opciones individuales. Si una página contiene opciones únicas, se documentan aquí.  
  
## <a name="starting-the-migration-wizard"></a>Iniciar al Asistente para migración  
De forma predeterminada, el Asistente para migración aparece al iniciar SSMA. También puede iniciar el Asistente en el **archivo** menú seleccionando **Asistente para migración**.  
  
## <a name="welcome-page"></a>Página Asistente  
La página de bienvenida presenta al Asistente para migración y ofrece la opción siguiente para iniciar al asistente.  
  
**Iniciar a este asistente en el inicio.**  
De forma predeterminada, SSMA iniciará al Asistente para migración cuando inicie SSMA. Para evitar que el inicio automático del asistente, desactive esta casilla de verificación.  
  
## <a name="create-new-project-page"></a>Crear nueva página de proyecto  
La página Crear nuevo proyecto es donde especificar el proyecto archivo migración, la ubicación y el nombre de tipo de proyecto (la versión de SQL Server utilizado para la migración de destino). Para obtener más información, consulte [nuevo proyecto (SSMA)](http://msdn.microsoft.com/ca294f6d-eeb5-42ca-9306-156281a3f0f3)  
  
## <a name="add-access-databases-page"></a>Agregar página de acceso a las bases de datos  
La página Agregar bases de datos de Access es donde agregar uno o más bases de datos de Access al proyecto. Puede agregar bases de datos individuales haciendo **agregar bases de datos**y, a continuación, seleccione las bases de datos desde el **abierto** ventana. O bien, puede encontrar las bases de datos mediante el **buscar bases de datos** botón. Para obtener más información, consulte los temas siguientes:  
  
-   [Agregar y quitar archivos de base de datos de Access](adding-and-removing-access-database-files-accesstosql.md)  
  
-   [Asistente de las bases de datos (Seleccionar ubicaciones) Buscar](http://msdn.microsoft.com/00b2d32a-998b-47a7-b25c-589b5bd6777a)  
  
-   [Encontrar al Asistente de las bases de datos (seleccionar archivos)](http://msdn.microsoft.com/2f574a34-4bab-40a4-89a8-ad4907ffc3fd)  
  
-   [Asistente Buscar bases de datos (Comprobar selección)](http://msdn.microsoft.com/62e20e03-50cc-4ac8-8072-524d194d2ec3)  
  
## <a name="select-objects-to-migrate-page"></a>Seleccionar objetos para migrar de página  
En los objetos Seleccione página de migración, seleccione objetos que se va a convertir. Puede seleccionar todos los objetos, grupos de objetos o los objetos individuales.  
  
**Para seleccionar objetos**  
  
1.  Expanda **acceso de metabase**y, a continuación, expanda **bases de datos**.  
  
2.  Realice uno o varios de los procedimientos siguientes:  
  
    -   Para convertir todas las bases de datos, seleccione la casilla de verificación junto a **bases de datos**.  
  
    -   Para convertir u omitir las bases de datos individuales, active o desactive la casilla de verificación situada junto al nombre de la base de datos.  
  
    -   Para convertir u omitir las consultas, expanda la base de datos y, a continuación, active o desactive el **consultas** casilla de verificación.  
  
    -   Para convertir u omitir las tablas individuales, expanda la base de datos, **tablas**y, a continuación, active o desactive la casilla de verificación junto a la tabla.  
  
Si tiene muchos objetos, desea utilizar el **selección avanzada de objeto** opciones en el panel derecho para filtrar el acceso a objetos de base de datos. Por ejemplo, si selecciona **tablas** en el panel izquierdo, a continuación, puede filtrar la lista de tablas mediante la especificación de cadenas en el **filtro** cuadro. A continuación, puede seleccionar o borrar las tablas filtradas para la migración mediante los botones en la parte superior del panel.  
  
Para obtener más información sobre el filtrado, consulte la sección de opciones de [selección avanzada de objeto (SSMA comunes)](http://msdn.microsoft.com/f53b0c79-5473-410a-a0dc-d8f544f7a63c).  
  
## <a name="connect-to-sql-server-page"></a>Conectarse a la página SQL Server  
En la conexión a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] página, especifique las propiedades de conexión y, a continuación, conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, consulte [conectar con SQL Server](http://msdn.microsoft.com/00e0432e-ec26-4ab4-af64-c9ca760e3541)  
  
> [!IMPORTANT]  
> Tan pronto como la conexión se realiza correctamente, se encontrará con **vincular tablas** donde tendrá la opción de vincular las tablas de página. Haga clic en **siguiente** y comienza la migración.  
  
## <a name="connect-to-sql-azure-page"></a>Conectarse a SQL Azure página  
En la página Conectar a SQL Azure, especifique las propiedades de conexión y, a continuación, conectarse a SQL Azure. Para crear una nueva base de datos de azure, puede hacerlo mediante el uso de **crear base de datos de Azure** opciones que aparece al hacer clic en **examinar** botón. Para obtener más información, consulte [conectarse a SQL Azure](connect-to-azure-sql-db-accesstosql.md)  
  
> [!IMPORTANT]  
> Tan pronto como la conexión se realiza correctamente, se encontrará con **vincular tablas** donde tendrá la opción de vincular las tablas de página. Haga clic en **siguiente** botón en la página de vínculos para iniciar la migración.  
  
## <a name="link-tables-page"></a>Página de las tablas de vínculo  
La página de vincular tablas le permite vincular las tablas de acceso originales a la que se migrado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o tablas de SQL Azure. Vincular tablas modifica la base de datos de acceso para que las páginas de acceso a las consultas, formularios, informes y datos usan los datos en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o base de datos de SQL Azure en lugar de los datos de la base de datos de Access.  
  
**Vincular tablas**  
Seleccione el **vincular tablas** casilla de verificación para vincular las tablas de acceso a los datos migrados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o tablas de SQL Azure. Para iniciar la migración, debe hacer clic en **siguiente** botón.  
  
## <a name="migration-status-page"></a>Página de migración de estado  
La página de estado de la migración muestra el progreso de la conversión de los esquemas de acceso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o esquemas de SQL Azure, cargando los esquemas convertidos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, y la migración de datos.  
  
Para obtener más información acerca de esta página, vea [convertir, cargar y migrar](http://msdn.microsoft.com/4ec83e96-88a5-4b7b-8d5a-f3429d9a936b)  
  
## <a name="see-also"></a>Vea también  
[Introducción a SQL Server Migration Assistant para Access &#40;AccessToSQL&#41;](../../ssma/access/getting-started-with-sql-server-migration-assistant-for-access-accesstosql.md)  
[Migrar bases de datos de Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[Reference(Access) de interfaz de usuario](http://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
