---
title: "Asistente para la migración (AccessToSQL) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-access
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
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
caps.latest.revision: "22"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7b8e039ef80efd41fabbaeeddbb9e3e1e9acc2ea
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="migration-wizard-accesstosql"></a>Asistente para la migración (AccessToSQL)
El Asistente para migración le guía a través de la migración de una o varias bases de datos de acceso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure. Mediante el Asistente para crear un proyecto, agregará las bases de datos al proyecto, seleccionar objetos para migrar y conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure. También se convertir, cargar y migrar datos y esquemas de acceso. Si lo desea, puede vincular las tablas de Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tablas o SQL Azure.  
  
La mayoría de las páginas del Asistente de migración contienen las mismas opciones que los cuadros de diálogo SSMA existentes. Por lo tanto, a continuación se describen las páginas del asistente y, a continuación, se proporcionan vínculos para que puede obtener más información acerca de las opciones individuales. Si una página contiene opciones únicas, se documentan aquí.  
  
## <a name="starting-the-migration-wizard"></a>Iniciar al Asistente para migración  
De forma predeterminada, el Asistente para migración aparece cuando se inicia SSMA. También puede iniciar el Asistente en el **archivo** menú seleccionando **Asistente para migración de**.  
  
## <a name="welcome-page"></a>Página Asistente  
La página de bienvenida presenta al Asistente para migración y proporciona la siguiente opción para iniciar al asistente.  
  
**Iniciar a este asistente en el inicio.**  
De forma predeterminada, SSMA iniciará al Asistente para migración cuando inicie SSMA. Para evitar el inicio automático del asistente, desactive esta casilla de verificación.  
  
## <a name="create-new-project-page"></a>Crear nueva página de proyecto  
La página Crear nuevo proyecto es donde debe especificar el proyecto archivo migración, la ubicación y el nombre del tipo de proyecto (la versión de SQL Server utilizada para la migración de destino). Para obtener más información, vea [nuevo proyecto (SSMA)](http://msdn.microsoft.com/en-us/ca294f6d-eeb5-42ca-9306-156281a3f0f3)  
  
## <a name="add-access-databases-page"></a>Agregar página de acceso a las bases de datos  
La página Agregar bases de datos de Access es donde agregar uno o más bases de datos de Access al proyecto. Puede agregar bases de datos individuales haciendo clic en **agregar bases de datos**y, a continuación, seleccione las bases de datos de la **abiertos** ventana. O bien, puede encontrar las bases de datos mediante el uso de la **buscar bases de datos** botón. Para obtener más información, consulte los temas siguientes:  
  
-   [Agregar y quitar archivos de base de datos de Access](http://msdn.microsoft.com/en-us/e944c740-4c8a-4bc1-b0ed-be57bc06dced)  
  
-   [Buscar al Asistente de bases de datos (seleccionados ubicaciones)](http://msdn.microsoft.com/en-us/00b2d32a-998b-47a7-b25c-589b5bd6777a)  
  
-   [Buscar al Asistente de bases de datos (seleccionados archivos)](http://msdn.microsoft.com/en-us/2f574a34-4bab-40a4-89a8-ad4907ffc3fd)  
  
-   [Asistente Buscar bases de datos (Comprobar selección)](http://msdn.microsoft.com/en-us/62e20e03-50cc-4ac8-8072-524d194d2ec3)  
  
## <a name="select-objects-to-migrate-page"></a>Seleccione los objetos que migre la página  
En los objetos Seleccione página de migración, seleccione objetos que se va a convertir. Puede seleccionar todos los objetos, grupos de objetos o los objetos individuales.  
  
**Seleccione los objetos**  
  
1.  Expanda **acceso metabase**y, a continuación, expanda **bases de datos**.  
  
2.  Realice uno o varios de los procedimientos siguientes:  
  
    -   Para convertir todas las bases de datos, active la casilla situada junto a **bases de datos**.  
  
    -   Para convertir u omitir las bases de datos individuales, active o desactive la casilla de verificación situada junto al nombre de la base de datos.  
  
    -   Para convertir u omitir las consultas, expanda la base de datos y, a continuación, active o desactive el **consultas** casilla de verificación.  
  
    -   Para convertir u omitir las tablas individuales, expanda la base de datos, **tablas**y, a continuación, active o desactive la casilla situada junto a la tabla.  
  
Si tiene muchos objetos, puede usar el **selección avanzada de objeto** opciones en el panel derecho para filtrar el acceso a objetos de base de datos. Por ejemplo, si selecciona **tablas** en el panel izquierdo, a continuación, puede filtrar la lista de tablas mediante la especificación de cadenas en la **filtro** cuadro. A continuación, puede Active o desactive las tablas filtradas para la migración mediante los botones en la parte superior del panel.  
  
Para obtener más información acerca del filtrado, vea la sección de opciones de [selección avanzada de objeto (SSMA común)](http://msdn.microsoft.com/en-us/f53b0c79-5473-410a-a0dc-d8f544f7a63c).  
  
## <a name="connect-to-sql-server-page"></a>Conectarse a la página SQL Server  
En la conexión a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] página, especifique propiedades de conexión y, a continuación, conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Para obtener más información, vea [conectar con SQL Server](http://msdn.microsoft.com/en-us/00e0432e-ec26-4ab4-af64-c9ca760e3541)  
  
> [!IMPORTANT]  
> Tan pronto como la conexión se realiza correctamente, se producirán **vincular tablas** donde tiene la opción de vincular las tablas de página. Haga clic en **siguiente** y comienza la migración.  
  
## <a name="connect-to-sql-azure-page"></a>Conectarse a SQL Azure página  
En la página conectarse a SQL Azure, especifique propiedades de conexión y, a continuación, conéctese a SQL Azure. Para crear una nueva base de datos de azure, puede hacerlo mediante el uso de **crear base de datos de Azure** opciones que aparece al hacer clic en **examinar** botón. Para obtener más información, vea [conectarse a SQL Azure](http://msdn.microsoft.com/en-us/bf44b236-d9be-41ae-a5fd-bd73038e505f)  
  
> [!IMPORTANT]  
> Tan pronto como la conexión se realiza correctamente, se producirán **vincular tablas** donde tiene la opción de vincular las tablas de página. Haga clic en **siguiente** botón en la página de vínculos para iniciar la migración.  
  
## <a name="link-tables-page"></a>Página de las tablas de vínculo  
La página de vincular tablas le permite vincular las tablas de acceso originales a la migrados [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o tablas de SQL Azure. Vincular tablas modifica la base de datos de Access para que las páginas de acceso a las consultas, formularios, informes y datos usan los datos de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure en lugar de los datos de la base de datos de Access.  
  
**Vincular tablas**  
Seleccione el **vincular tablas** casilla de verificación para vincular tablas de Access a la migrados [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o tablas de SQL Azure. Para iniciar la migración, debe hacer clic en **siguiente** botón.  
  
## <a name="migration-status-page"></a>Página de estado de migración  
La página de estado de la migración muestra el progreso de la conversión de los esquemas de acceso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o esquemas de SQL Azure, cargando los esquemas convertidos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure, y, a continuación, migrar datos.  
  
Para obtener más información acerca de esta página, vea [convertir, cargar y migrar](http://msdn.microsoft.com/en-us/4ec83e96-88a5-4b7b-8d5a-f3429d9a936b)  
  
## <a name="see-also"></a>Vea también  
[Introducción a SQL Server Migration Assistant para acceder al &#40; AccessToSQL &#41;](../../ssma/access/getting-started-with-sql-server-migration-assistant-for-access-accesstosql.md)  
[Migrar bases de datos de Access a SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
[Reference(Access) de interfaz de usuario](http://msdn.microsoft.com/en-us/af24c303-4a41-449b-9c86-d6558a97e839)  
  
