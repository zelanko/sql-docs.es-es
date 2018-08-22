---
title: Crear y administrar proyectos (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- creating projects
- new projects
- opening projects
- projects
- projects, creating and managing
- saving metadata
- saving projects
ms.assetid: f2d1f0b0-5394-4adb-b3f3-abd71eb68ca7
caps.latest.revision: 22
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 860f8e569cd87aaf034718456c8157cf91f57941
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2018
ms.locfileid: "40393707"
---
# <a name="creating-and-managing-projects-accesstosql"></a>Crear y administrar proyectos (AccessToSQL)
Para migrar bases de datos de Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, primero debe crear un proyecto SSMA. El proyecto es un archivo que contiene metadatos sobre las bases de datos de acceso que desea migrar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, los metadatos sobre la instancia de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure que va a recibir los datos y los objetos migrados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] información de conexión y configuración del proyecto.  
  
## <a name="reviewing-default-project-settings"></a>Revisar la configuración predeterminada del proyecto  
SSMA contiene varias opciones de conversión y sincronizar objetos de base de datos y para convertir los datos. La configuración predeterminada para estas opciones es adecuada para muchos usuarios. Sin embargo, antes de crear un nuevo proyecto SSMA, debe revisar las opciones y, si lo desea, cambie la configuración predeterminada que se usará para todos los proyectos nuevos.  
  
**Para revisar la configuración predeterminada del proyecto**  
  
1.  En el **herramientas** menú, seleccione **configuración de proyecto predeterminada**.  
  
2.  Seleccione el tipo de proyecto en **versión de destino de migración** a qué opciones de configuración se pueden ver o cambiar y, a continuación, haga clic en el menú desplegable **General** ficha.  
  
3.  En el panel izquierdo, haga clic en **conversión**.  
  
4.  En el panel derecho, revise las opciones. Para obtener más información acerca de estas opciones, consulte [configuración del proyecto (conversión)](http://msdn.microsoft.com/bcebc635-c638-4ddb-924c-b9ccfef86388).  
  
5.  Cambiar las opciones según sea necesario.  
  
6.  Repita los pasos anteriores para el **migración**, **GUI**, y **Type Mapping** páginas.  
  
    -   Para obtener información acerca de las opciones de migración, consulte [configuración del proyecto (migración)](http://msdn.microsoft.com/4caebc9c-8680-4b99-a8fa-89c43161c95d).  
  
    -   Para obtener información sobre las opciones de la interfaz de usuario, consulte [configuración de proyecto (GUI)](http://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693).  
  
    -   Para obtener más información acerca de la configuración de asignación de tipos de datos, vea [configuración del proyecto (asignación de tipo)](http://msdn.microsoft.com/b87b9683-abed-4677-8c50-18bdba704655).  
  
    -   Para obtener información acerca de la configuración de SQL Azure, consulte [configuración del proyecto (SQL Azure)](http://msdn.microsoft.com/bbb8a204-d0e4-4f0b-9709-271feb1f136e).  
  
**Tenga en cuenta** configuración de SQL Azure estará disponible solo cuando se selecciona la migración a SQL Azure al crear un proyecto.  
  
## <a name="creating-new-projects"></a>Creación de nuevos proyectos  
SSMA se inicia sin tener que cargar un proyecto predeterminado. Para migrar datos desde bases de datos de Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, debe crear un proyecto.  
  
**Para crear un nuevo proyecto**  
  
1.  En el menú **Archivo**, seleccione **Nuevo proyecto**.  
  
    Aparecerá el cuadro de diálogo **Nuevo proyecto** .  
  
2.  En el **nombre** , escriba un nombre para el proyecto.  
  
3.  En el **ubicación** cuadro, escriba o seleccione una carpeta para el proyecto  
  
4.  En la lista para la migración hacia abajo, seleccione uno de SQL Server 2005 o SQL Server 2008 o SQL Server 2012 o SQL Server 2014 / SQL Server 2016 / Azure SQL DB y, a continuación, haga clic en **Aceptar**.  
  
SSMA crea el archivo de proyecto. Ahora puede realizar el paso siguiente del [agregar uno o más bases de datos de Access](adding-and-removing-access-database-files-accesstosql.md).  
  
## <a name="customizing-project-settings"></a>Personalizar la configuración de proyecto  
Además de definir la configuración predeterminada del proyecto, que se aplica a todos los nuevos proyectos SSMA, también puede personalizar la configuración para cada proyecto. Para obtener más información, consulte [conversión de configuración y opciones de migración](setting-conversion-and-migration-options-accesstosql.md).  
  
Al personalizar las asignaciones de tipos de datos entre bases de datos de origen y destino, puede definir asignaciones en el proyecto, la base de datos o el nivel de objeto. Para obtener más información sobre la asignación de tipo, consulte [tipos de datos de destino y origen de asignación](mapping-source-and-target-data-types-accesstosql.md).  
  
## <a name="saving-projects"></a>Guardando proyectos  
Cuando se guarda un proyecto, SSMA conserva la configuración del proyecto y, opcionalmente, los metadatos de la base de datos, en el archivo de proyecto.  
  
**Para guardar un proyecto**  
  
-   En el **archivo** menú, seleccione **Guardar proyecto**.  
  
    Si las bases de datos dentro del proyecto han cambiado o no se han convertido, SSMA le solicitará que guarde los metadatos en el proyecto. Guardar metadatos le permite trabajar sin conexión. También le permite enviar un archivo de proyecto completo a otras personas, incluido el personal de soporte técnico. Si se le pedirá que guarde los metadatos, realice lo siguiente:  
  
    1.  Para cada base de datos que muestra el estado **donde faltan metadatos**, active la casilla situada junto al nombre de la base de datos.  
  
        Guardar metadatos podría tardar varios minutos. Si no desea guardar los metadatos en este momento, no seleccione las casillas de verificación.  
  
    2.  Haga clic en **Guardar**.  
  
        SSMA analizará los esquemas de acceso y guardar los metadatos en el archivo de proyecto.  
  
## <a name="opening-projects"></a>Abrir proyectos  
Al abrir un proyecto, se desconecta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. Esto le permite trabajar sin conexión. Para actualizar los objetos de base de datos de carga de metadatos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. Para migrar datos, debe volver a conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure.  
  
**Para abrir un proyecto**  
  
1.  Realice uno de los siguientes procedimientos:  
  
    -   En el **archivo** menú, elija **proyectos recientes**y, a continuación, seleccione el proyecto que desea abrir.  
  
    -   En el **archivo** menú, seleccione **Abrir proyecto**, busque el archivo de proyecto .a2ssproj, seleccione el archivo y, a continuación, haga clic en **abierto**.  
  
2.  Para volver a conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], en el **archivo** menú, seleccione **volver a conectar a SQL Server**.  
  
3.  Para volver a conectarse a SQL Azure, en el **archivo** menú, seleccione **volver a conectarse a SQL Azure.**  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso del proceso de migración es [agregar uno o más bases de datos de Access](adding-and-removing-access-database-files-accesstosql.md).  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[Agregar y quitar archivos de base de datos de Access](adding-and-removing-access-database-files-accesstosql.md)  
  
