---
title: Importación de SQL Server y el Asistente para exportación | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 87
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 3e320ff0fdb834ca242739a76fb9e0b1242e3579
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36200171"
---
# <a name="sql-server-import-and-export-wizard"></a>Asistente para importación y exportación de SQL Server
  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Import and Export Wizard ofrece el método más sencillo para crear un [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] paquete que copia datos de un origen a un destino.  
  
> [!NOTE]  
>  En un equipo de 64 bits, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] instala la versión de 64 bits del Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (DTSWizard.exe). Sin embargo, algunos orígenes de datos, como Access o Excel, solo tienen un proveedor de 32 bits disponible. Para trabajar con estos orígenes de datos, podría tener que instalar y ejecutar la versión de 32 bits del asistente. Para instalar la versión de 32 bits del asistente, seleccione Herramientas cliente o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] durante la instalación.  
  
 Puede iniciar el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde el menú Inicio, desde [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], desde [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] o en el símbolo del sistema. Para obtener más información, consulte [ejecutar la importación de SQL Server y el Asistente para exportación de](start-the-sql-server-import-and-export-wizard.md).  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Import and Export Wizard pueden copiar datos a y desde cualquier origen de datos para los que un administrado [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] proveedor de datos o un proveedor OLE DB nativo está disponible. La lista de proveedores disponibles incluye los orígenes de datos siguientes:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Archivos planos  
  
-   Microsoft Office Access  
  
-   Microsoft Office Excel  
  
 Algunas características del asistente funcionan de forma diferente dependiendo del entorno en el que se inicie:  
  
-   Si inicia la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Import and Export Wizard en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], ejecutar inmediatamente el paquete seleccionando la **ejecutar inmediatamente** casilla de verificación. Esta casilla está activada de forma predeterminada y el paquete se ejecuta de inmediato.  
  
     También puede decidir si desea guardar el paquete en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o en el sistema de archivos. Si selecciona guardar el paquete, también debe especificar un nivel de protección de paquetes. Para obtener más información acerca de los niveles de protección del paquete, consulte [Control de acceso para los datos confidenciales en paquetes](../security/access-control-for-sensitive-data-in-packages.md).  
  
     Después de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Import and Export Wizard ha creado el paquete y copiado los datos, puede usar el [!INCLUDE[ssIS](../../includes/ssis-md.md)] diseñador para abrir y cambiar el paquete guardado agregando tareas, transformaciones y lógica controlada por eventos.  
  
    > [!NOTE]  
    >  En [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], la opción para guardar el paquete creado por el asistente no está disponible.  
  
-   Si inicia la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Import and Export Wizard desde una [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] proyecto en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], no se puede ejecutar el paquete como un paso para completar el asistente. En lugar de ello, el paquete se agrega al proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] desde el cual se inició el asistente. Seguidamente, puede ejecutar el paquete o ampliarlo agregando tareas, transformaciones y lógica controlada por eventos usando el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)].  
  
 Para obtener más información, consulte [ejecutar la importación de SQL Server y el Asistente para exportación de](start-the-sql-server-import-and-export-wizard.md).  
  
## <a name="permissions-required-by-the-import-and-export-wizard"></a>Permisos requeridos por el Asistente para importación y exportación  
 Para completar la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Import and Export Wizard correctamente, debe tener al menos los permisos siguientes:  
  
-   Permisos para conectarse a las bases de datos o recursos compartidos de archivos de origen y de destino. En [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], esto requiere derechos de inicio de sesión de servidor y base de datos.  
  
-   Permiso para leer datos de la base de datos o el archivo de origen. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se requieren permisos SELECT en las tablas de origen y vistas.  
  
-   Permisos para escribir datos en la base de datos o el archivo de destino. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se requieren permisos INSERT en las tablas de destino.  
  
-   Si se desea crear una base de datos o tabla de destino, o un archivo de destino, se requieren permisos suficientes para crear una base de datos, una tabla o un archivo. Para ello, en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se requieren permisos CREATE DATABASE o CREATE TABLE.  
  
-   Si desea guardar el paquete creado por el asistente, se requieren permisos suficientes para escribir en la base de datos msdb o en el sistema de archivos. En [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], se requieren permisos INSERT en la base de datos msdb.  
  
## <a name="mapping-data-types-in-the-import-and-export-wizard"></a>Asignar tipos de datos en el Asistente para importación y exportación  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Import and Export Wizard proporciona capacidades de transformación mínimas. Salvo para establecer el nombre, el tipo de datos y las propiedades de tipo de datos de las columnas de las tablas y archivos de destino nuevos, el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no admite ninguna transformación en el nivel de columna.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Import and Export Wizard utiliza la asignación de archivos que [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] proporciona para asignar tipos de datos de versión de una base de datos o sistema a otra. Por ejemplo, puede crear una asignación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a Oracle. De forma predeterminada, los archivos de asignación en formato XML se instalan en C:\Archivos de programa\Microsoft SQL Server\100\DTS\MappingFiles. Si su empresa requiere diferentes asignaciones entre tipos de datos, puede actualizar las asignaciones para que tengan efecto en las asignaciones que realiza el asistente. Por ejemplo, si desea que la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **nchar** tipo de datos para asignar a DB2 **gráficos** tipo de datos en lugar de DB2 **VARGRAPHIC** al transferir datos de tipo de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a DB2, debe cambiar la **nchar** asignación en el archivo de asignación SqlClientToIBMDB2.xml para usar **gráficos** en lugar de **VARGRAPHIC.**  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] incluye asignaciones entre varias combinaciones de orígenes y destinos habitualmente utilizadas, y puede agregar nuevos archivos de asignaciones al directorio de archivos de asignación para admitir destinos y orígenes adicionales. Los nuevos archivos de asignaciones deben ajustarse al esquema XSD publicado y asignar entre una combinación única de origen y destino.  
  
> [!NOTE]  
>  Si edita un archivo de asignación existente o agregar un nuevo archivo de asignación a la carpeta, debe cerrar y volver a abrir la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Import and Export Wizard o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para que se reconozcan los archivos nuevos o modificados.  
  
## <a name="external-resources"></a>Recursos externos  
  
-   Vídeo, [exportar datos de SQL Server a Excel (vídeo de SQL Server)](http://go.microsoft.com/fwlink/?LinkID=200975), en technet.microsoft.com  
  
-   Ejemplo de CodePlex, [exportar de ODBC a un archivo plano usando un Tutorial de asistente: paquetes de lecciones](http://go.microsoft.com/fwlink/?LinkId=217657), en msftisprodsamples.codeplex.com  
  
  