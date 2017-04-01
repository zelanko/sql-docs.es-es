---
title: "Start the SQL Server Import and Export Wizard | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Asistente para importación y exportación de SQL Server"
  - "iniciar el Asistente para importación y exportación de SQL Server"
  - "Asistente para importación y exportación"
  - "Asistente para importación y exportación, iniciar"
ms.assetid: 5fc4f6d1-1f6f-444e-9aeb-827f85e1c405
caps.latest.revision: 130
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 112
---
# Start the SQL Server Import and Export Wizard
Puede iniciar el Asistente para importar y exportar de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] siguiendo los métodos siguientes.
-   En el [menú Inicio](#startStart) o el [símbolo del sistema](#startCmd) para tareas de importación o exportación usando cualquier origen de datos compatible.
-   En [SQL Server Management Studio (SSMS)](#startSSMS) para tareas de importación o exportación usando SQL Server.
-   En [Visual Studio con SQL Server Data Tools (SSDT)](#startVS) si tiene un proyecto de SQL Server Integration Services abierto.

En este tema solo se describe cómo **iniciar** el asistente.
-   Si quiere obtener información general sobre el asistente, consulte [Asistente para importación y exportación de SQL Server](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md).
-   Si quiere obtener información acerca de los pasos del asistente, seleccione la página correspondiente en el menú de navegación de contenido. Hay una página independiente de documentación para cada página del asistente. O pulse la tecla F1 en cualquier página o cuadro de diálogo del asistente para ver la documentación de la página actual.

**Obtenga el asistente**. Si desea ejecutar el asistente, pero no tiene [!INCLUDE[msCoName] (../Token/msCoName_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalado en el equipo, puede instalar el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la instalación de SQL Server Data Tools (SSDT). Para obtener más información, vea [Descargar SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).  

## <a name="a-namestartstarta-start-the-wizard-from-the-start-menu"></a><a name="startStart"></a> Iniciar el asistente desde el menú Inicio  
1.  En el menú **Inicio** , haga clic en **Todas las aplicaciones**.
2.  Busque y expanda **Microsoft SQL Server 2016**.
3.  Haga clic en una de las opciones siguientes.
  
    -   **Importar y exportar datos de SQL Server 2016 (64 bits)**
          
    -   **Importar y exportar datos de SQL Server 2016 (32 bits)**  
  
Ejecute la versión de 64 bits del asistente, a menos que sepa que el origen de datos requiere un proveedor de datos de 32 bits.
 
![Iniciar el asistente desde Inicio](../../integration-services/import-export-data/media/start-wizard-start.jpg)
  
## <a name="a-namestartcmda-start-the-wizard-from-the-command-prompt"></a><a name="startCmd"></a> Iniciar el asistente desde el símbolo del sistema  
En una ventana del símbolo del sistema, ejecute **DTSWizard.exe** desde una de las siguientes ubicaciones.  
  
-   **C:\Archivos de programa\Microsoft SQL Server\130\DTS\Binn** para la versión de 64 bits.  
  
-   **C:\Archivos de programa (x86)\Microsoft SQL Server\130\DTS\Binn** para la versión de 32 bits.  
  
Ejecute la versión de 64 bits del asistente, a menos que sepa que el origen de datos requiere un proveedor de datos de 32 bits.

![Iniciar el asistente desde el símbolo del sistema](../../integration-services/import-export-data/media/start-wizard-cmd.jpg)  
  
## <a name="a-namestartssmsa-start-the-wizard-from-sql-server-management-studio-ssms"></a><a name="startSSMS"></a> Iniciar el asistente desde SQL Server Management Studio (SSMS)  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
2.  Expanda **Bases de datos**.
3.  Haga clic con el botón derecho en una base de datos.
4.  Seleccione **Tareas**.
5.  Haga clic en una de las opciones siguientes.
  
    -   **Importar datos**
      
    -   **Exportar datos**  

![Iniciar el asistente desde SSMS](../../integration-services/import-export-data/media/start-wizard-ssms.jpg) 

Si no tiene instalado SQL Server o si dispone de SQL Server pero no tiene instalado SQL Server Management Studio, consulte [Descargar SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx).
    
## <a name="a-namestartvsa-start-the-wizard-from-visual-studio-with-sql-server-data-tools-ssdt"></a><a name="startVS"></a> Iniciar al asistente desde Visual Studio con SQL Server Data Tools (SSDT)  
 En Visual Studio con [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], con un proyecto de Integration Services abierto, realice una de las acciones siguientes.  
  
-   En el menú **Proyecto**, haga clic en el **Asistente para importación y exportación de SSIS**. 

    ![Iniciar el asistente desde Proyecto](../../integration-services/import-export-data/media/start-wizard-project.jpg) 
    
    \- o bien
    
-   En el Explorador de soluciones, haga clic con el botón derecho en la carpeta **Paquetes SSIS** y haga clic en **Asistente para importación y exportación de SSIS**.

    ![Iniciar el asistente desde Paquetes](../../integration-services/import-export-data/media/start-wizard-packages.jpg)

Si no tiene instalado Visual Studio o si dispone de Visual Studio pero no tiene instalado SQL Server Data Tools, consulte [Descargar SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx). 

## <a name="get-help-while-the-wizard-is-running"></a>Obtener ayuda mientras se ejecuta el Asistente
> [!TIP] Pulse la tecla F1 en cualquier página o cuadro de diálogo del Asistente para ver la documentación de la página actual.   

 ## <a name="whats-next"></a>¿Qué debe hacer a continuación?  
 Al iniciar el Asistente, la primera página es **Asistente para importación y exportación de SQL Server**. No hace falta que realice ninguna acción en esta página. Para obtener más información, vea [Asistente para importación y exportación de SQL Server](../../integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md).  
  
  