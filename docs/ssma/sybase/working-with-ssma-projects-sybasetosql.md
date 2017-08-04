---
title: Trabajar con proyectos SSMA (SybaseToSQL) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 11091d95-c488-48c3-891a-743cac94ac93
caps.latest.revision: 10
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 957f4148fc200fee98b29fed1f28a17bc8661d07
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="working-with-ssma-projects-sybasetosql"></a>Trabajar con proyectos SSMA (SybaseToSQL)
Migrar bases de datos de Sybase Adaptive Server Enterprise (ASE) a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure, primero cree un proyecto SSMA. El proyecto es un archivo que contiene metadatos sobre las bases de datos de ASE que se van a migrar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure, metadatos acerca de la instancia de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure que recibirá los datos y los objetos migrados [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o información de conexión de SQL Azure y configuración del proyecto.  
  
Cuando se abre un proyecto, se desconecta [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure. Esto le permite trabajar sin conexión. Puede volver a conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure. Para obtener más información, vea [conectarse a SQL Server &#40; SybaseToSQL &#41; ](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md)  /  [Conectarse a base de datos de SQL Azure &#40; SybaseToSQL &#41; ](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md).  
  
## <a name="reviewing-default-project-settings"></a>Revisar la configuración predeterminada del proyecto  
SSMA contiene varias opciones de conversión y cargar objetos de base de datos, migración de datos y la sincronización de SSMA con ASE y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure. La configuración predeterminada para estas opciones es adecuada para muchos usuarios. Sin embargo, antes de crear un nuevo proyecto SSMA, debe revisar las opciones y, si lo desea, cambie los valores predeterminados que se usará para todos los proyectos nuevos.  
  
**Para revisar la configuración predeterminada del proyecto**  
  
1.  En el **herramientas** menú, seleccione **configuración de proyecto predeterminada**.  
  
2.  Seleccione el tipo de proyecto en **versión de destino de migración** a los valores que se necesitan para puede ver o cambiar y, a continuación, haga clic en el menú desplegable **General** ficha.  
  
3.  En el panel izquierdo, haga clic en **conversión**.  
  
4.  En el panel derecho, revise las opciones, cambiar las opciones según sea necesario. Para obtener más información acerca de estas opciones, consulte [configuración del proyecto &#40; Conversión &#41; &#40; SybaseToSQL &#41; ](../../ssma/sybase/project-settings-conversion-sybasetosql.md).  
  
5.  Repita los pasos 1 a 3 para las páginas de migración, SQL Azure, cargar objetos, interfaz gráfica de usuario y la asignación de tipo.  
  
    -   Para obtener información acerca de las opciones de migración, consulte [configuración del proyecto &#40; Migración de &#41; &#40; SybaseToSQL &#41; ](../../ssma/sybase/project-settings-migration-sybasetosql.md).  
  
    -   Para obtener información sobre las opciones para cargar objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], consulte [configuración del proyecto &#40; Sincronización &#41; &#40; SybaseToSQL &#41; ](../../ssma/sybase/project-settings-synchronization-sybasetosql.md).  
  
    -   Para obtener más información acerca de las opciones de la interfaz gráfica de usuario, consulte [configuración del proyecto &#40; Interfaz gráfica de usuario &#41; &#40; SybaseToSQL &#41; ](../../ssma/sybase/project-settings-gui-sybasetosql.md).  
  
    -   Para obtener más información acerca de la configuración de asignación de tipos de datos, haga clic en [configuración del proyecto &#40; Asignación de tipos de &#41; &#40; SybaseToSQL &#41; ](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md).  
  
    -   Para obtener más información acerca de las opciones de SQL Azure, consulte [configuración del proyecto &#40; Base de datos de SQL Azure &#41; &#40; SybaseToSQL &#41; ](../../ssma/sybase/project-settings-azure-sql-db-sybasetosql.md).  
  
    > [!NOTE]  
    > Se mostrará la configuración de SQL Azure solo cuando se selecciona **migración a SQL Azure** al crear un proyecto.  
  
## <a name="creating-new-projects"></a>Crear nuevos proyectos  
Para migrar datos de bases de datos de ASE a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure, primero debe crear un proyecto.  
  
**Para crear un proyecto**  
  
1.  En el menú **Archivo**, seleccione **Nuevo proyecto**.  
  
    Aparecerá el cuadro de diálogo **Nuevo proyecto** .  
  
2.  En el **nombre** cuadro, escriba un nombre para el proyecto.  
  
3.  En el **ubicación** cuadro, escriba o seleccione una carpeta para el proyecto.  
  
4.  En el **migración a** de lista desplegable, seleccione la versión de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] usa para la migración. Las opciones disponibles son:  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016  
  
    -   Base de datos de SQL Azure  
  
Y, a continuación, haga clic en **Aceptar**.  
  
## <a name="customizing-project-settings"></a>Personalizar la configuración de proyecto  
Además de definir la configuración predeterminada del proyecto que se aplican a todos los nuevos proyectos SSMA, puede personalizar la configuración para cada proyecto. Para obtener más información, vea [establecer las opciones del proyecto &#40; SybaseToSQL &#41; ](../../ssma/sybase/setting-project-options-sybasetosql.md).  
  
Si desea personalizar asignaciones de tipos de datos entre las bases de datos de origen y de destino, puede definir asignaciones en el proyecto, la base de datos o el nivel de objeto. Para obtener más información sobre la asignación de tipo, consulte [asignación Sybase ASE y tipos de datos de SQL Server &#40; SybaseToSQL &#41; ](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).  
  
## <a name="saving-projects"></a>Guardar proyectos  
Cuando se guarda un proyecto, SSMA conserva la configuración del proyecto y, opcionalmente, los metadatos de la base de datos, en el archivo de proyecto.  
  
**Para guardar un proyecto**  
  
-   En el **archivo** menú, seleccione **Guardar proyecto**.  
  
    Si las bases de datos dentro del proyecto han cambiado o que no se ha convertido, SSMA le pedirá que guarde los metadatos en el proyecto. Guardar los metadatos le permitirá trabajar sin conexión y para enviar un archivo de proyecto completo a otras personas, incluido el personal de soporte técnico. Si le pide que guarde los metadatos, realice lo siguiente:  
  
    1.  Para cada base de datos que muestra un estado de **faltan metadatos**, active la casilla situada junto al nombre de la base de datos.  
  
        Guardar los metadatos puede tardar varios minutos. Si no desea guardar los metadatos en este momento, no seleccione las casillas de verificación.  
  
    2.  Haga clic en el **guardar** botón.  
  
        SSMA analizará los esquemas de Sybase ASE y guardar los metadatos en el archivo de proyecto.  
  
## <a name="opening-projects"></a>Abrir proyectos  
Cuando se abre un proyecto, se desconecta de ASE y de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure. Esto le permite trabajar sin conexión. Para actualizar los metadatos, cargar los objetos de base de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure. Para migrar datos, debe volver a conectarse a ASE y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure.  
  
**Para abrir un proyecto**  
  
1.  Realice uno de los siguientes procedimientos:  
  
    -   En el **archivo** menú, elija **proyectos recientes**y, a continuación, seleccione el proyecto que desea abrir.  
  
    -   En el **archivo** menú, seleccione **Abrir proyecto**, busque el archivo de proyecto .s2ssproj, seleccione el archivo y, a continuación, haga clic en **abiertos**.  
  
2.  Para volver a conectarse a ASE, en la **archivo** menú, seleccione **conectarse de nuevo a Sybase**.  
  
3.  Para volver a conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure, en la **archivo** menú, seleccione **volver a conectar a SQL Server** / **volver a conectar a SQL Azure**.  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso del proceso de migración consiste en [conectar para Sybase ASE](http://msdn.microsoft.com/en-us/a45a2330-9175-4c9e-af38-ef920e350614).  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de ASE de Sybase a SQL Server: base de datos de SQL Azure &#40; SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
[Conectarse a Sybase ASE &#40; SybaseToSQL &#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md)  
[Conectarse a SQL Server &#40; SybaseToSQL &#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md)  
[Conectarse a la base de datos de SQL Azure &#40; SybaseToSQL &#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)  
  

