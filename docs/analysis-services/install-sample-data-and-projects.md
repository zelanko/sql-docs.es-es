---
title: Instalar los datos de ejemplo de Analysis Services y proyectos | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: df7311aad9c356376fffafc8a4882af8e29e746b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62659244"
---
# <a name="install-sample-data-and-multidimensional-projects"></a>Instalar los datos de ejemplo y proyectos multidimensionales 
[!INCLUDE[ssas-appliesto-sqlas-all](../includes/ssas-appliesto-sqlas-all.md)]

Use las instrucciones y vínculos proporcionados en este artículo para instalar los archivos de proyecto y los datos usados en los tutoriales de Analysis Services. 
  
## <a name="step-1-install-prerequisites"></a>Paso 1: Requisitos previos de instalación 
En las lecciones de este tutorial se supone que tiene el siguiente software instalado. Puede instalar todas las características en un único equipo. Para instalar estas características, ejecute el programa de instalación de SQL Server y selecciónelas en la página Selección de características.  
  
-   Motor de base de datos de SQL Server  
  
-   SQL Server Analysis Services (SSAS) 
  
    Analysis Services está disponible en estas ediciones solo: Evaluation, Enterprise, Business Intelligence, Standard. No se admiten los modelos multidimensionales en Azure Analysis Services.
  
    De forma predeterminada, Analysis Services 2016 y versiones posteriores se instala como una instancia tabular, que puede invalidar si elige el modo servidor Multidimensional en el servidor de página de configuración del Asistente para la instalación.
  
## <a name="step-2-download-and-install-developer-and-management-tools"></a>Paso 2: Descargue e instale las herramientas de administración y desarrollo
SQL Server Data Tools (SSDT) para Visual Studio se descargan e instalado por separado de otras características de SQL Server. Los diseñadores y plantillas de proyecto que se usa para crear modelos de BI e informes están incluidas en SSDT para Visual Studio 2015 o como [paquetes de Nuget](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects) para Visual Studio 2017.  
  
[Descargar SQL Server Data Tools](http://go.microsoft.com/fwlink/?LinkID=827542).   

SQL Server Management Studio (SSMS) está descargado y se instala por separado de otras características de SQL Server.  

[Descargar SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)  

Opcionalmente, considere la posibilidad de instalar Excel para examinar los datos multidimensionales a medida que recorre el tutorial. Al instalar Excel, se habilita la característica **Analizar en Excel** , que inicia Excel con una lista de campos de tabla dinámica conectada al cubo que se está compilando. Se recomienda utilizar Excel para examinar los datos porque puede se puede crear rápidamente un informe dinámico que permite interactuar con los datos.  
  
O bien, puede examinar los datos usando el diseñador de consultas MDX integrado en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. El diseñador de consultas devuelve los mismos datos, excepto los presentados como un conjunto de filas plano.  
  
## <a name="step-3-install-databases"></a>Paso 3: Instalar bases de datos  
Un modelo multidimensional de Analysis Services usa datos transaccionales importados de un sistema de administración de bases de datos relacionales. Para los fines de este tutorial, usará la siguiente base de datos relacional como origen de datos.  
  
-   **AdventureWorksDW2012 o una versión posterior** -se trata de un almacén de datos relacional que se ejecuta en una instancia del motor de base de datos. Proporciona los datos originales usados por las bases de datos de Analysis Services y los proyectos que generará e implementará en el tutorial. El tutorial supone que está usando AdventureWorksDW2012, sin embargo, ¿funcionan las versiones posteriores.
  
    Puede usar esta base de datos de ejemplo con [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] y versiones posteriores. En general, debe usar la versión de base de datos de ejemplo que coincida con la versión del motor de base de datos.
  
Para instalar la base de datos, realice lo siguiente:  
  
1.  Descargue un [AdventureWorkDW](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) copia de seguridad de base de datos de GitHub.  
  
2.  Copie el archivo de copia de seguridad en el directorio de datos de la instancia del motor de base de datos de SQL Server local.
  
3.  Inicie Microsoft SQL Server Management Studio y conéctese a la instancia del Motor de base de datos.  
  
4.  Restaure la base de datos.  
  
## <a name="step-4-grant-database-permissions"></a>Paso 4: Conceder permisos de base de datos  
En los proyectos de ejemplo se usa la configuración de suplantación del origen de datos que especifica el contexto de seguridad bajo el que se importan o se procesan los datos. De forma predeterminada, los valores de suplantación especifican la cuenta de servicio de Analysis Services para obtener acceso a los datos. Para usar esta configuración predeterminada, debe asegurarse de que la cuenta de servicio que se ejecuta Analysis Services tiene permisos de lector de datos en el **AdventureWorksDW** base de datos.  
  
> [!NOTE]  
> Para los propósitos de aprendizaje, se recomienda que use la opción de suplantación de cuenta de servicio predeterminada y que otorgue permisos de lector de datos a la cuenta de servicio en SQL Server. Aunque hay otras opciones de suplantación disponibles, no todas ellas son convenientes para procesar las operaciones. Concretamente, la opción de usar las credenciales del usuario actual no se admite para el procesamiento.  
  
1.  Determine la cuenta de servicio. Puede usar el Administrador de configuración de SQL Server o la aplicación de consola Servicios para ver la información de cuentas. Si ha instalado Analysis Services como instancia predeterminada, usando la cuenta predeterminada, el servicio se está ejecutando como **NT Service\MSSQLServerOLAPService**.  
  
2.  En Management Studio, conéctese a la instancia del motor de base de datos.  
  
3.  Expanda la carpeta Seguridad, haga clic con el botón derecho en Inicios de sesión y seleccione **Nuevo inicio de sesión**.  
  
4.  En la página General, en Nombre de inicio de sesión, escriba **NT Service\MSSQLServerOLAPService** (o la cuenta como la que se ejecute el servicio).  
  
5.  Haga clic en **Asignación de usuarios**.  
  
6.  Active la casilla de verificación junto a la **AdventureWorksDW** base de datos. La pertenencia al rol debería incluir **db_datareader** y **public**de forma automática. Haga clic en **Aceptar** para aceptar los valores predeterminados.  
  
## <a name="step-5-install-projects"></a>Paso 5: Instalar los proyectos  

El tutorial incluye proyectos de ejemplo para que pueda comparar sus resultados con un proyecto acabado, o iniciar una lección que está más adelante en la secuencia.  
  
1.  Descargue el [adventure-works-multidimensional-tutorial-projects.zip](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks-analysis-services) en el ejemplo de Adventure Works para la página de ejemplos de Analysis Services en GitHub.  
  
    Los proyectos del tutorial funcionan para [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] y versiones posteriores.  
  
2.  Mueva el archivo de .zip a una carpeta que esté debajo de la unidad raíz (por ejemplo, C:\Tutorial). Este paso mitiga el error "Ruta de acceso demasiado larga" que a veces se produce si intenta descomprimir los archivos en la carpeta descargas.  
  
3.  Descomprima los proyectos de ejemplo: haga clic con el botón derecho en el archivo y seleccione **Extraer todo**. Después de extraer los archivos, debe tener las carpetas lección 1, 2, 3, 5, 6, 7, 8, 9, 10 completar y Lesson 4 Start. 
  
4.  Quite los permisos de solo lectura de estos archivos. Haga clic en la carpeta principal, seleccione **propiedades**y desactive la casilla de verificación **de sólo lectura**. Haga clic en **Aceptar**. Aplique los cambios a esta carpeta, sus subcarpetas y sus archivos.  

5.  Abra el archivo de solución (.sln) que corresponde a la lección en que se encuentra. Por ejemplo, en la carpeta denominada “Lesson 1 Complete”, abriría el archivo Analysis Services Tutorial.sln.  
  
6.  Implementar la solución para comprobar que los permisos de base de datos e información de ubicación de servidor estén configurados correctamente.  
  
    Si Analysis Services y el motor de base de datos se instalan como la instancia predeterminada (MSSQLServer) y todo el software se está ejecutando en el mismo equipo, puede hacer clic en **Implementar solución** en el menú Compilar para compilar e implementar el proyecto de ejemplo en la instancia local de Analysis Services. Durante la implementación, datos es procesados (o importan) desde el **AdventureWorksDW** base de datos en la instancia del motor de base de datos local. Se crea una nueva base de datos de Analysis Services en la instancia de Analysis Services que contiene los datos recuperados desde el motor de base de datos.  
  
    Si encuentra los errores, revise los pasos anteriores de configuración de los permisos de base de datos. Además, puede ser necesario cambiar los nombres de servidor. El nombre de servidor predeterminado es localhost. Si los servidores están instalados en equipos remotos o como instancias con nombre, debe invalidar el valor predeterminado para usar un nombre de servidor válido para la instalación. Además, si los servidores están en equipos remotos, podría ser necesario configurar Firewall de Windows para permitir el acceso a los servidores.  
  
    El nombre de servidor para conectarse al motor de base de datos se especifica en el objeto de origen de datos de la solución multidimensional (tutorial de Adventure Works), que es visible en el Explorador de soluciones.  
  
    El nombre de servidor para conectarse a Analysis Services se especifica en la pestaña Implementación de las páginas de propiedades del proyecto, que también es visible en el Explorador de soluciones.  
  
7.  En SQL Server Management Studio, conéctese a Analysis Services. Compruebe que se está ejecutando en el servidor una base de datos denominada **Analysis Services Tutorial** .  
  
## <a name="next-step"></a>Paso siguiente  
Ahora está preparado para utilizar el tutorial. Para obtener más información sobre cómo comenzar, consulte [Creación de modelos multidimensionales &#40;tutorial de Adventure Works&#41;](../analysis-services/multidimensional-modeling-adventure-works-tutorial.md).  
  
## <a name="see-also"></a>Vea también  
[Configurar Firewall de Windows para permitir el acceso a Analysis Services](../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)  
[Configure the Windows Firewall to Allow SQL Server Access](../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)  
  
  