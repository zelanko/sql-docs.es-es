---
title: Instalar datos de ejemplo y proyectos | Documentos de Microsoft
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: fc475b25-cbb2-408a-901f-9299299538c5
caps.latest.revision: "16"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Active
ms.openlocfilehash: 0e675845383c3e54c8477a8e0866231ac302cd1f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="install-sample-data-and-projects"></a>Instalar datos de ejemplo y proyectos 
Use las instrucciones y los vínculos proporcionados en este tema para instalar todos los archivos de datos y de proyecto empleados en los tutoriales de Analysis Services.  
  
## <a name="step-1-install-sql-server-software"></a>Paso 1: instalar el software SQL Server  
En las lecciones de este tutorial se supone que tiene el siguiente software instalado. Todo el software siguiente se instala con los discos de instalación del SQL Server. Para mayor simplicidad de la implementación, puede instalar todas las características en un equipo único. Para instalar estas características, ejecute el programa de instalación de SQL Server y selecciónelas en la página Selección de características. Para obtener más información, consulte [Instalación de SQL Server 2016 desde el Asistente para la instalación &#40;programa de instalación&#41;](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md).  
  
-   Motor de base de datos  
  
-   Analysis Services  
  
    Analysis Services solo está disponible en estas ediciones: Evaluation, Enterprise, Business Intelligence, Standard.  
  
    Tenga en cuenta que las ediciones de SQL Server Express no incluyen Analysis Services. [Descargue la edición de evaluación](http://go.microsoft.com/fwlink/?LinkId=392824) si quiere probar el software de forma gratuita.  
  
    De forma predeterminada, Analysis Services se instala como una instancia multidimensional, lo que puede invalidar si elige el modo de servidor tabular en la página de configuración del servidor del Asistente para la instalación. Si desea ejecutar ambos modos de servidor, vuelva a ejecutar el programa de instalación de SQL Server en el mismo equipo para instalar una segunda instancia de Analysis Services en el otro modo.  
  
-   SQL Server Management Studio  
  
Opcionalmente, considere la posibilidad de instalar Excel para examinar los datos multidimensionales a medida que recorre el tutorial. Al instalar Excel, se habilita la característica **Analizar en Excel** , que inicia Excel con una lista de campos de tabla dinámica conectada al cubo que se está compilando. Se recomienda utilizar Excel para examinar los datos porque puede se puede crear rápidamente un informe dinámico que permite interactuar con los datos.  
  
O bien, puede examinar los datos usando el diseñador de consultas MDX integrado en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. El diseñador de consultas devuelve los mismos datos, excepto los presentados como un conjunto de filas plano.  
  
## <a name="step-2-download-sql-server-data-tools-for-visual-studio-2015"></a>Paso 2: Descargar SQL Server Data Tools para Visual Studio 2015  
En esta versión, SQL Server Data Tools se descarga e instala de forma independiente de otras características de SQL Server. Los diseñadores y las plantillas de proyecto que se emplean para crear modelos e informes de BI están disponibles como una descarga web gratuita.  
  
-   [Descargar SQL Server Data Tools](http://go.microsoft.com/fwlink/?LinkID=827542). El archivo se guarda en la carpeta Descargas. Ejecute el programa de instalación para instalar la herramienta.  
  
    Reinicie el equipo para completar la instalación.  
  
## <a name="step-3-install-databases"></a>Paso 3: Instalar bases de datos  
Un modelo multidimensional de Analysis Services usa datos transaccionales importados de un sistema de administración de bases de datos relacionales. Para los propósitos de este tutorial, utilizará la siguiente base de datos relacional como origen de datos.  
  
-   **AdventureWorksDW2012** : es un almacenamiento de datos relacional que se ejecuta en una instancia del motor de base de datos. Proporciona los datos originales que serán utilizados por las bases de datos de Analysis Services y los proyectos que va a compilar e implementar a lo largo del tutorial.  
  
    Puede usar esta base de datos de ejemplo con [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] y con [!INCLUDE[ssSQL11](../includes/sssql11-md.md)].  
  
Para instalar esta base de datos, haga lo siguiente:  
  
1.  Descargue la base de datos [AdventureWorksDW2012](http://go.microsoft.com/fwlink/p/?LinkID=221770) de la página de ejemplos del producto de codeplex.  
  
    El nombre del archivo de base de datos es AdventureWorksDW2012_Data.mdf. El archivo debe estar en la carpeta Descargas del equipo.  
  
2.  Copie el archivo AdventureWorksDW2012_Data.mdf en el directorio de datos de la instancia del Motor de base de datos de SQL Server local. De manera predeterminada, se encuentra en C:\Archivos de programa\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data.  
  
3.  Inicie Microsoft SQL Server Management Studio y conéctese a la instancia del Motor de base de datos.  
  
4.  Haga clic con el botón derecho en Bases de datos y haga clic en **Adjuntar**.  
  
5.  Haga clic en **Agregar**.  
  
6.  Seleccione el archivo de base de datos **AdventureWorksDW2012_Data.mdf** y haga clic en **Aceptar**. Si el archivo no aparece, compruebe la carpeta C:\Archivos de programa\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Data para asegurarse de que está allí.  
  
7.  En los detalles de la base de datos, quite la entrada del archivo de registro. El programa de instalación da por supuesto que tiene un archivo de registro, pero no hay ningún archivo de registro en el ejemplo. Se creará automáticamente un nuevo archivo de registro al adjuntar la base de datos. Seleccione el archivo de registro, haga clic en **Quitar**y, después, haga clic en **Aceptar** para adjuntar solo el archivo de base de datos principal.  
  
## <a name="step-4-grant-database-permissions"></a>Paso 4: Otorgar permisos de base de datos  
En los proyectos de ejemplo se usa la configuración de suplantación del origen de datos que especifica el contexto de seguridad bajo el que se importan o se procesan los datos. De forma predeterminada, los valores de suplantación especifican la cuenta de servicio de Analysis Services para obtener acceso a los datos. Para usar esta configuración predeterminada, debe asegurarse de que la cuenta de servicio bajo la que se ejecuta Analysis Services tiene permisos de lector de datos en la base de datos **AdventureWorksDW2012** .  
  
> [!NOTE]  
> Para los propósitos de aprendizaje, se recomienda que use la opción de suplantación de cuenta de servicio predeterminada y que otorgue permisos de lector de datos a la cuenta de servicio en SQL Server. Aunque hay otras opciones de suplantación disponibles, no todas ellas son convenientes para procesar las operaciones. Concretamente, la opción de usar las credenciales del usuario actual no se admite para el procesamiento.  
  
1.  Determine la cuenta de servicio. Puede usar el Administrador de configuración de SQL Server o la aplicación de consola Servicios para ver la información de cuentas. Si ha instalado Analysis Services como instancia predeterminada, usando la cuenta predeterminada, el servicio se está ejecutando como **NT Service\MSSQLServerOLAPService**.  
  
2.  En Management Studio, conéctese a la instancia del motor de base de datos.  
  
3.  Expanda la carpeta Seguridad, haga clic con el botón derecho en Inicios de sesión y seleccione **Nuevo inicio de sesión**.  
  
4.  En la página General, en Nombre de inicio de sesión, escriba **NT Service\MSSQLServerOLAPService** (o la cuenta como la que se ejecute el servicio).  
  
5.  Haga clic en **Asignación de usuarios**.  
  
6.  Active la casilla situada al lado de la base de datos **AdventureWorksDW2012** . La pertenencia al rol debería incluir **db_datareader** y **public**de forma automática. Haga clic en **Aceptar** para aceptar los valores predeterminados.  
  
## <a name="step-5-install-projects"></a>Paso 5: Instalar los proyectos  
El tutorial incluye proyectos de ejemplo para que pueda comparar sus resultados con un proyecto acabado, o iniciar una lección que está más adelante en la secuencia.  
  
El archivo de proyecto de la lección 4 es particularmente importante porque proporciona la base para esa lección y paro todas las lecciones siguientes. En contraste con los archivos de proyecto anteriores, donde los pasos del tutorial tenían como resultado una copia exacta de los archivos de proyecto completados, el proyecto de ejemplo de la lección 4 incluye la nueva información del modelo que no se encuentra en el modelo creado en las lecciones 1 a 3. En la lección 4 se supone que comienza con un archivo de proyecto de ejemplo que está disponible en la siguiente descarga.  
  
1.  Descargue el [Tutorial de Analysis Services SQL Server 2012](http://go.microsoft.com/fwlink/p/?LinkID=221866) de la página de ejemplos del producto en codeplex.  
  
    Los tutoriales de 2012 son válidos para la versión [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] .  
  
    El archivo “Analysis Services Tutorial SQL Server 2012.zip” se guardará en la carpeta de descarga en su equipo.  
  
2.  Mueva el archivo de .zip a una carpeta que esté debajo de la unidad raíz (por ejemplo, C:\Tutorial). Este paso mitiga el error “Ruta de acceso demasiado larga” que aparece en ocasiones si intenta descomprimir los archivos en la carpeta Descargas.  
  
3.  Descomprima los proyectos de ejemplo: haga clic con el botón derecho en el archivo y seleccione **Extraer todo**. Después de extraer los archivos, debería tener los siguientes proyectos instalados en su equipo:  
  
    -   Lección 1 completa  
  
    -   Lección 2 completa  
  
    -   Lección 3 completa  
  
    -   Lección 4 completa  
  
    -   Lección 4 inicio  
  
    -   Lección 5 completa  
  
    -   Lección 6 completa  
  
    -   Lección 7 completa  
  
    -   Lección 8 completa  
  
    -   Lección 9 completa  
  
    -   Lección 10 completa  
  
4.  Quite los permisos de solo lectura de estos archivos. Haga clic con el botón derecho en la carpeta principal, “Analysis Services Tutorial SQL Server 2012”, seleccione **Propiedades**y desactive la casilla **Solo lectura**. Haga clic en **Aceptar**. Aplique los cambios a esta carpeta, sus subcarpetas y sus archivos.  
  
5.  Inicie [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
6.  Abra el archivo de solución (.sln) que corresponde a la lección que está utilizando. Por ejemplo, en la carpeta denominada “Lesson 1 Complete”, abriría el archivo Analysis Services Tutorial.sln.  
  
7.  Implemente la solución para comprobar que los permisos de base de datos y la información de ubicación del servidor se han configurado correctamente.  
  
    Si Analysis Services y el motor de base de datos se instalan como la instancia predeterminada (MSSQLServer) y todo el software se está ejecutando en el mismo equipo, puede hacer clic en **Implementar solución** en el menú Compilar para compilar e implementar el proyecto de ejemplo en la instancia local de Analysis Services. Durante la implementación, los datos se procesarán (o importarán) de la base de datos **AdventureWorksDW2012** en la instancia del motor de base de datos local. Se creará una nueva base de datos de Analysis Services en la instancia de Analysis Services que contiene los datos recuperados del motor de base de datos.  
  
    Si encuentra los errores, revise los pasos anteriores de configuración de los permisos de base de datos. Además, puede ser necesario cambiar los nombres de servidor. El nombre de servidor predeterminado es localhost. Si los servidores están instalados en equipos remotos o como instancias con nombre, debe invalidar el valor predeterminado para usar un nombre de servidor válido para la instalación. Además, si los servidores están en equipos remotos, podría ser necesario configurar Firewall de Windows para permitir el acceso a los servidores.  
  
    El nombre de servidor para conectarse al motor de base de datos se especifica en el objeto de origen de datos de la solución multidimensional (tutorial de Adventure Works), que es visible en el Explorador de soluciones.  
  
    El nombre de servidor para conectarse a Analysis Services se especifica en la pestaña Implementación de las páginas de propiedades del proyecto, que también es visible en el Explorador de soluciones.  
  
8.  En SQL Server Management Studio, conéctese a Analysis Services. Compruebe que se está ejecutando en el servidor una base de datos denominada **Analysis Services Tutorial** .  
  
## <a name="next-step"></a>Paso siguiente  
Ahora está preparado para utilizar el tutorial. Para obtener más información sobre cómo comenzar, consulte [Creación de modelos multidimensionales &#40;tutorial de Adventure Works&#41;](../analysis-services/multidimensional-modeling-adventure-works-tutorial.md).  
  
## <a name="see-also"></a>Vea también  
[Instalación de SQL Server 2016 desde el Asistente para la instalación &#40;programa de instalación&#41;](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)  
[Configurar Firewall de Windows para permitir el acceso a Analysis Services](../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)  
[Configure the Windows Firewall to Allow SQL Server Access](../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)  
  
  
  
