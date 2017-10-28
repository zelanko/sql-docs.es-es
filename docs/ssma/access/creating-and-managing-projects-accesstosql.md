---
title: Crear y administrar proyectos (AccessToSQL) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
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
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: bc89d40afd125aef5c874c4578bb153cdfcf6993
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="creating-and-managing-projects-accesstosql"></a>Crear y administrar proyectos (AccessToSQL)
Para migrar bases de datos de Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure, primero debe crear un proyecto SSMA. El proyecto es un archivo que contiene metadatos sobre las bases de datos de acceso que se van a migrar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure, metadatos acerca de la instancia de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure que recibirá los datos y los objetos migrados [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] información de conexión y configuración del proyecto.  
  
## <a name="reviewing-default-project-settings"></a>Revisar la configuración predeterminada del proyecto  
SSMA contiene varias opciones de conversión y sincronizar objetos de base de datos y para convertir los datos. La configuración predeterminada para estas opciones es adecuada para muchos usuarios. Sin embargo, antes de crear un nuevo proyecto SSMA, debe revisar las opciones y, si lo desea, cambie la configuración predeterminada que se usará para todos los proyectos nuevos.  
  
**Para revisar la configuración predeterminada del proyecto**  
  
1.  En el **herramientas** menú, seleccione **configuración de proyecto predeterminada**.  
  
2.  Seleccione el tipo de proyecto en **versión de destino de migración** a los valores que se van a ver / cambiar y, a continuación, haga clic en el menú desplegable **General** ficha.  
  
3.  En el panel izquierdo, haga clic en **conversión**.  
  
4.  En el panel derecho, revise las opciones. Para obtener más información acerca de estas opciones, consulte [configuración del proyecto (conversión)](http://msdn.microsoft.com/en-us/bcebc635-c638-4ddb-924c-b9ccfef86388).  
  
5.  Cambiar las opciones según sea necesario.  
  
6.  Repita los pasos anteriores para la **migración**, **GUI**, y **Type Mapping** páginas.  
  
    -   Para obtener información acerca de las opciones de migración, consulte [configuración del proyecto (migración)](http://msdn.microsoft.com/en-us/4caebc9c-8680-4b99-a8fa-89c43161c95d).  
  
    -   Para obtener información sobre las opciones de interfaz de usuario, consulte [configuración de proyecto (GUI)](http://msdn.microsoft.com/en-us/cf06baf1-8714-48a3-95dc-781f6ca53693).  
  
    -   Para obtener más información acerca de la configuración de asignación de tipos de datos, vea [configuración del proyecto (tipo de asignación)](http://msdn.microsoft.com/en-us/b87b9683-abed-4677-8c50-18bdba704655).  
  
    -   Para obtener información acerca de la configuración de SQL Azure, consulte [configuración del proyecto (SQL Azure)](http://msdn.microsoft.com/en-us/bbb8a204-d0e4-4f0b-9709-271feb1f136e).  
  
**Tenga en cuenta** configuración de SQL Azure estará disponible solo cuando se selecciona la migración a SQL Azure al crear un proyecto.  
  
## <a name="creating-new-projects"></a>Crear nuevos proyectos  
SSMA se inicia sin cargar un proyecto predeterminado. Para migrar datos de bases de datos de Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure, debe crear un proyecto.  
  
**Para crear un nuevo proyecto**  
  
1.  En el menú **Archivo**, seleccione **Nuevo proyecto**.  
  
    Aparecerá el cuadro de diálogo **Nuevo proyecto** .  
  
2.  En el **nombre** cuadro, escriba un nombre para el proyecto.  
  
3.  En el **ubicación** cuadro, escriba o seleccione una carpeta para el proyecto  
  
4.  En la lista de migración a abajo, seleccione uno de SQL Server 2005 o SQL Server 2008 / SQL Server 2012 o SQL Server 2014 / SQL Server 2016 / Azure SQL DB y, a continuación, haga clic en **Aceptar**.  
  
SSMA crea el archivo de proyecto. Ahora puede realizar el paso siguiente de [agregar uno o más bases de datos de Access](http://msdn.microsoft.com/en-us/e944c740-4c8a-4bc1-b0ed-be57bc06dced).  
  
## <a name="customizing-project-settings"></a>Personalizar la configuración de proyecto  
Además de definir la configuración del proyecto de forma predeterminada, que se aplican a todos los nuevos proyectos SSMA, también puede personalizar la configuración para cada proyecto. Para obtener más información, consulte [conversión de configuración y opciones de migración](http://msdn.microsoft.com/en-us/0a7304df-2f35-4453-96ef-7ac83dea1167).  
  
Si desea personalizar asignaciones de tipos de datos entre las bases de datos de origen y de destino, puede definir asignaciones en el proyecto, la base de datos o el nivel de objeto. Para obtener más información sobre la asignación de tipo, consulte [tipos de datos de destino y origen de asignación](http://msdn.microsoft.com/en-us/b362a075-16e7-423f-b63f-e1e9f02844a9).  
  
## <a name="saving-projects"></a>Guardar proyectos  
Cuando se guarda un proyecto, SSMA conserva la configuración del proyecto y, opcionalmente, los metadatos de la base de datos, en el archivo de proyecto.  
  
**Para guardar un proyecto**  
  
-   En el **archivo** menú, seleccione **Guardar proyecto**.  
  
    Si las bases de datos dentro del proyecto han cambiado o que no se ha convertido, SSMA le pedirá que guarde los metadatos en el proyecto. Guardar los metadatos le permite trabajar sin conexión. También le permite enviar un archivo de proyecto completo a otras personas, incluido el personal de soporte técnico. Si le pide que guarde los metadatos, realice lo siguiente:  
  
    1.  Para cada base de datos que muestra un estado de **faltan metadatos**, active la casilla situada junto al nombre de la base de datos.  
  
        Guardar los metadatos puede tardar varios minutos. Si no desea guardar los metadatos en este momento, no seleccione las casillas de verificación.  
  
    2.  Haga clic en **Guardar**.  
  
        SSMA analizará los esquemas de acceso y guardar los metadatos en el archivo de proyecto.  
  
## <a name="opening-projects"></a>Abrir proyectos  
Cuando se abre un proyecto, se desconecta [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure. Esto le permite trabajar sin conexión. Para actualizar los objetos de base de datos de carga de metadatos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure. Para migrar datos, debe volver a conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure.  
  
**Para abrir un proyecto**  
  
1.  Realice uno de los siguientes procedimientos:  
  
    -   En el **archivo** menú, elija **proyectos recientes**y, a continuación, seleccione el proyecto que desea abrir.  
  
    -   En el **archivo** menú, seleccione **Abrir proyecto**, busque el archivo de proyecto .a2ssproj, seleccione el archivo y, a continuación, haga clic en **abiertos**.  
  
2.  Para volver a conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], en la **archivo** menú, seleccione **volver a conectar a SQL Server**.  
  
3.  Para volver a conectarse a SQL Azure, en la **archivo** menú, seleccione **volver a conectarse a SQL Azure.**  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso del proceso de migración consiste en [agregar uno o más bases de datos de Access](http://msdn.microsoft.com/en-us/e944c740-4c8a-4bc1-b0ed-be57bc06dced).  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de Access a SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
[Agregar y quitar archivos de base de datos de Access](http://msdn.microsoft.com/en-us/e944c740-4c8a-4bc1-b0ed-be57bc06dced)  
  

