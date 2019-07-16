---
title: Trabajar con proyectos de SSMA (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 11091d95-c488-48c3-891a-743cac94ac93
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: eb6f035b4d597e2b648134c195b698554dc78e12
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68072475"
---
# <a name="working-with-ssma-projects-sybasetosql"></a>Proyectos de SSMA (SybaseToSQL)
Para migrar bases de datos de Sybase Adaptive Server Enterprise (ASE) a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, primero cree un proyecto de SSMA. El proyecto es un archivo que contiene metadatos sobre las bases de datos de ASE que desea migrar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, los metadatos sobre la instancia de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure que va a recibir los datos y los objetos migrados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure información de conexión y configuración del proyecto.  
  
Al abrir un proyecto, se desconecta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. Esto le permite trabajar sin conexión. Puede volver a conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. Para obtener más información, consulte [conectarse a SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md) / [conexión a Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md).  
  
## <a name="reviewing-default-project-settings"></a>Revisar la configuración predeterminada del proyecto  
SSMA contiene varias opciones de conversión y cargar objetos de base de datos, migración de datos y sincronización SSMA con ASE y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. La configuración predeterminada para estas opciones es adecuada para muchos usuarios. Sin embargo, antes de crear un nuevo proyecto SSMA, debe revisar las opciones y, si lo desea, cambie los valores predeterminados que se usará para todos los proyectos nuevos.  
  
**Para revisar la configuración predeterminada del proyecto**  
  
1.  En el **herramientas** menú, seleccione **configuración de proyecto predeterminada**.  
  
2.  Seleccione el tipo de proyecto en **versión de destino de migración** a qué opciones de configuración son necesarios para ver o cambiar y, a continuación, haga clic en el menú desplegable **General** ficha.  
  
3.  En el panel izquierdo, haga clic en **conversión**.  
  
4.  En el panel derecho, revise las opciones, cambiar las opciones según sea necesario. Para obtener más información acerca de estas opciones, consulte [configuración del proyecto &#40;conversión&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md).  
  
5.  Repita los pasos 1 a 3 para las páginas de la migración, SQL Azure, al cargar objetos, interfaz gráfica de usuario y asignación de tipos.  
  
    -   Para obtener información acerca de las opciones de migración, consulte [configuración del proyecto &#40;migración&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-migration-sybasetosql.md).  
  
    -   Para obtener información sobre las opciones para cargar objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [configuración del proyecto &#40;sincronización&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-synchronization-sybasetosql.md).  
  
    -   Para obtener más información acerca de las opciones de la interfaz gráfica de usuario, consulte [configuración del proyecto &#40;GUI&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-gui-sybasetosql.md).  
  
    -   Para obtener más información acerca de la configuración de asignación de tipos de datos, haga clic en [configuración del proyecto &#40;asignación de tipo&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md).  
  
    -   Para obtener más información acerca de las opciones de SQL Azure, consulte [configuración del proyecto &#40;Azure SQL DB &#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-azure-sql-db-sybasetosql.md).  
  
    > [!NOTE]  
    > Se mostrará la configuración de SQL Azure solo cuando se selecciona **migración a SQL Azure** al crear un proyecto.  
  
## <a name="creating-new-projects"></a>Creación de nuevos proyectos  
Para migrar datos de las bases de datos de la instancia de ASE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, primero debe crear un proyecto.  
  
**Para crear un proyecto**  
  
1.  En el menú **Archivo**, seleccione **Nuevo proyecto**.  
  
    Aparecerá el cuadro de diálogo **Nuevo proyecto** .  
  
2.  En el **nombre** , escriba un nombre para el proyecto.  
  
3.  En el **ubicación** cuadro, escriba o seleccione una carpeta para el proyecto.  
  
4.  En el **migración a** lista desplegable, seleccione la versión de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usados para la migración. Las opciones disponibles son:  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016  
  
    -   Azure SQL DB  
  
Y, a continuación, haga clic en **Aceptar**.  
  
## <a name="customizing-project-settings"></a>Personalizar la configuración de proyecto  
Además de definir la configuración predeterminada del proyecto que se aplica a todos los nuevos proyectos SSMA, puede personalizar la configuración para cada proyecto. Para obtener más información, consulte [definir opciones de proyecto &#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md).  
  
Al personalizar las asignaciones de tipos de datos entre bases de datos de origen y destino, puede definir asignaciones en el proyecto, la base de datos o el nivel de objeto. Para obtener más información sobre la asignación de tipo, consulte [asignación Sybase ASE y tipos de datos de SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).  
  
## <a name="saving-projects"></a>Guardando proyectos  
Cuando se guarda un proyecto, SSMA conserva la configuración del proyecto y, opcionalmente, los metadatos de la base de datos, en el archivo de proyecto.  
  
**Para guardar un proyecto**  
  
-   En el **archivo** menú, seleccione **Guardar proyecto**.  
  
    Si las bases de datos dentro del proyecto han cambiado o no se han convertido, SSMA le solicitará que guarde los metadatos en el proyecto. Guardar metadatos le permitirá trabajar sin conexión y enviar un archivo de proyecto completo a otras personas, incluido el personal de soporte técnico. Si se le pedirá que guarde los metadatos, realice lo siguiente:  
  
    1.  Para cada base de datos que muestra el estado **donde faltan metadatos**, active la casilla situada junto al nombre de la base de datos.  
  
        Guardar metadatos podría tardar varios minutos. Si no desea guardar los metadatos en este momento, no seleccione las casillas de verificación.  
  
    2.  Haga clic en el botón **Guardar**.  
  
        SSMA analizará los esquemas de Sybase ASE y guardar los metadatos en el archivo de proyecto.  
  
## <a name="opening-projects"></a>Abrir proyectos  
Al abrir un proyecto, se desconecta de ASE y de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. Esto le permite trabajar sin conexión. Para actualizar los metadatos, cargar los objetos de base de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. Para migrar datos, debe volver a conectarse al ASE y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure.  
  
**Para abrir un proyecto**  
  
1.  Realice uno de los siguientes procedimientos:  
  
    -   En el **archivo** menú, elija **proyectos recientes**y, a continuación, seleccione el proyecto que desea abrir.  
  
    -   En el **archivo** menú, seleccione **Abrir proyecto**, busque el archivo de proyecto .s2ssproj, seleccione el archivo y, a continuación, haga clic en **abierto**.  
  
2.  Para volver a conectar al ASE, en el **archivo** menú, seleccione **volver a conectar a Sybase**.  
  
3.  Para volver a conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, en el **archivo** menú, seleccione **volver a conectar a SQL Server** / **volver a conectar a SQL Azure**.  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso del proceso de migración es [conectarse a Sybase ASE](connecting-to-sybase-ase-sybasetosql.md).  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de Sybase ASE a SQL Server: base de datos SQL Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
[Conexión a Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md)  
[Conectarse a SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md)  
[Conexión a Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)  
  
