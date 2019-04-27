---
title: Importación de SQL Server y el Asistente para exportación | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- exporting data
- mapping files [Integration Services]
- SQL Server Import and Export Wizard
- SSIS packages, creating
- packages [Integration Services], copying
- Integration Services packages, creating
- packages [Integration Services], creating
- SQL Server Integration Services packages, creating
- Import and Export Wizard
- copying data [Integration Services]
- importing data, SSIS packages
- sources [Integration Services], copying data
ms.assetid: c0e4d867-b2a9-4b2a-844b-2fe45be88f81
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2f3ce90e2670357d0842b0a6ac7838f396465bab
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62768172"
---
# <a name="sql-server-import-and-export-wizard"></a>Asistente para importación y exportación de SQL Server
  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Import and Export Wizard ofrece el método más sencillo para crear un [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] paquete que copia datos de un origen a un destino.  
  
> [!NOTE]  
>  En un equipo de 64 bits, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] instala la versión de 64 bits del Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (DTSWizard.exe). Sin embargo, algunos orígenes de datos, como Access o Excel, solo tienen un proveedor de 32 bits disponible. Para trabajar con estos orígenes de datos, podría tener que instalar y ejecutar la versión de 32 bits del asistente. Para instalar la versión de 32 bits del asistente, seleccione Herramientas cliente o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] durante la instalación.  
  
 Puede iniciar el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde el menú Inicio, desde [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], desde [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] o en el símbolo del sistema. Para obtener más información, consulte [ejecutar la importación de SQL Server y el Asistente para exportación de](start-the-sql-server-import-and-export-wizard.md).  
  
 El Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede copiar datos entre orígenes de datos para los que esté disponible un proveedor de datos de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] administrado o un proveedor OLE DB nativo. La lista de proveedores disponibles incluye los orígenes de datos siguientes:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Archivos planos  
  
-   Microsoft Office Access  
  
-   Microsoft Office Excel  
  
 Algunas características del asistente funcionan de forma diferente dependiendo del entorno en el que se inicie:  
  
-   Si inicia el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] importación y exportación en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], ejecutar el paquete inmediatamente activando la **ejecutar inmediatamente** casilla de verificación. Esta casilla está activada de forma predeterminada y el paquete se ejecuta de inmediato.  
  
     También puede decidir si desea guardar el paquete en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o en el sistema de archivos. Si selecciona guardar el paquete, también debe especificar un nivel de protección de paquetes. Para obtener más información acerca de los niveles de protección de paquetes, consulte [Control del acceso a datos confidenciales en paquetes](../security/access-control-for-sensitive-data-in-packages.md).  
  
     Una vez que el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] haya creado el paquete y copiado los datos, puede utilizar el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] para abrir y cambiar el paquete guardado agregando tareas, transformaciones y lógica controlada por eventos.  
  
    > [!NOTE]  
    >  En [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], la opción para guardar el paquete creado por el asistente no está disponible.  
  
-   Si inicia el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde un proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], el paquete no puede ejecutarse como paso para completar el asistente. En lugar de ello, el paquete se agrega al proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] desde el cual se inició el asistente. Seguidamente, puede ejecutar el paquete o ampliarlo agregando tareas, transformaciones y lógica controlada por eventos usando el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)].  
  
 Para obtener más información, consulte [ejecutar la importación de SQL Server y el Asistente para exportación de](start-the-sql-server-import-and-export-wizard.md).  
  
## <a name="permissions-required-by-the-import-and-export-wizard"></a>Permisos requeridos por el Asistente para importación y exportación  
 Para completar el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] correctamente, se debe disponer como mínimo de los siguientes permisos:  
  
-   Permisos para conectarse a las bases de datos o recursos compartidos de archivos de origen y de destino. Para ello, en [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se requieren derechos de inicio de sesión del servidor y de la base de datos.  
  
-   Permiso para leer datos de la base de datos o el archivo de origen. Para ello, en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se requieren permisos SELECT para las tablas y vistas de origen.  
  
-   Permisos para escribir datos en la base de datos o el archivo de destino. Para ello, en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se requieren permisos INSERT para las tablas de destino.  
  
-   Si se desea crear una base de datos o tabla de destino, o un archivo de destino, se requieren permisos suficientes para crear una base de datos, una tabla o un archivo. Para ello, en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se requieren permisos CREATE DATABASE o CREATE TABLE.  
  
-   Si desea guardar el paquete creado por el asistente, se requieren permisos suficientes para escribir en la base de datos msdb o en el sistema de archivos. En [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], se requieren permisos INSERT en la base de datos msdb.  
  
## <a name="mapping-data-types-in-the-import-and-export-wizard"></a>Asignar tipos de datos en el Asistente para importación y exportación  
 El Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona capacidades de transformación mínimas. Salvo para establecer el nombre, el tipo de datos y las propiedades de tipo de datos de las columnas de las tablas y archivos de destino nuevos, el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no admite ninguna transformación en el nivel de columna.  
  
 El Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza los archivos de asignación que [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] proporciona para asignar tipos de datos de una versión de base de datos o sistema a otro. Por ejemplo, puede crear una asignación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a Oracle. De forma predeterminada, los archivos de asignación en formato XML se instalan en C:\Archivos de programa\Microsoft SQL Server\100\DTS\MappingFiles. Si su empresa requiere diferentes asignaciones entre tipos de datos, puede actualizar las asignaciones para que tengan efecto en las asignaciones que realiza el asistente. Por ejemplo, si desea que el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **nchar** tipo de datos para asignar a DB2 **gráfico** tipo de datos en lugar de DB2 **VARGRAPHIC** al transferir datos de tipo de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a DB2, debe cambiar la **nchar** asignación en el archivo de asignación SqlClientToIBMDB2.xml para usar **gráfico** en lugar de **VARGRAPHIC.**  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] incluye asignaciones entre varias combinaciones de orígenes y destinos habitualmente utilizadas, y puede agregar nuevos archivos de asignaciones al directorio de archivos de asignación para admitir destinos y orígenes adicionales. Los nuevos archivos de asignaciones deben ajustarse al esquema XSD publicado y asignar entre una combinación única de origen y destino.  
  
> [!NOTE]  
>  Si modifica un archivo de asignación existente o agrega un nuevo archivo de asignación a la carpeta, debe cerrar y volver a abrir el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para que se reconozcan los archivos nuevos o modificados.  
  
## <a name="external-resources"></a>Recursos externos  
  
-   Vídeo, [exportar datos de SQL Server a Excel (vídeo de SQL Server)](https://go.microsoft.com/fwlink/?LinkID=200975), en technet.microsoft.com  
  
-   Ejemplo CodePlex, [exportar de ODBC a un archivo plano utilizando un Tutorial de asistente: Paquetes de lecciones](https://go.microsoft.com/fwlink/?LinkId=217657), en msftisprodsamples.codeplex.com  
  
  
