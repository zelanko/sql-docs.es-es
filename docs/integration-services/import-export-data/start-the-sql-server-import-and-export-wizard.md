---
title: "Iniciar SQL Server de importación y exportación Asistente | Documentos de Microsoft"
ms.custom: 
ms.date: 06/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Import and Export Wizard
- starting SQL Server Import and Export Wizard
- Import and Export Wizard
- starting Import and Export Wizard
ms.assetid: 5fc4f6d1-1f6f-444e-9aeb-827f85e1c405
caps.latest.revision: 130
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 0a4240a8ae3f62ac986a871b198ffb2aefe78862
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="start-the-sql-server-import-and-export-wizard"></a>Iniciar SQL Server de importación y exportación de Asistente

 > Para el contenido relacionado con las versiones anteriores de SQL Server, vea [ejecutar la importación de SQL Server y el Asistente para exportación de](https://msdn.microsoft.com/en-US/library/ms140052(SQL.120).aspx).

Iniciar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Import and Export Wizard en uno de los métodos descritos en este tema para importar datos desde y exportar datos a cualquier origen de datos admitidos.

> [!IMPORTANT]
> En este tema solo se describe cómo **iniciar** el asistente. Si está buscando algo, consulte [relacionados con tareas y contenido](#related).

Puede iniciar al asistente:
-   En el [menú Inicio](#startStart).
-   En el [símbolo del sistema](#startCmd). 
-   En [SQL Server Management Studio (SSMS)](#startSSMS).
-   En [Visual Studio con SQL Server Data Tools (SSDT)](#startVS).

## <a name="prerequisite---is-the-wizard-installed-on-your-computer"></a>¿Requisito previo: es el Asistente para instalar en el equipo?
Si desea ejecutar el asistente, pero no tiene [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalado en el equipo, puede instalar el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la instalación de SQL Server Data Tools (SSDT). Para obtener más información, vea [Descargar SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).

## <a name="startStart"></a> menú Inicio  
### <a name="start-the-sql-server-import-and-export-wizard-from-the-start-menu"></a>Iniciar la importación de SQL Server y el Asistente para exportación desde el menú Inicio
1.  En el **iniciar** menú, busque y expanda **Microsoft SQL Server 2016**.
3.  Haga clic en una de las opciones siguientes.
  
    -   **Importar y exportar datos de SQL Server 2016 (64 bits)**
          
    -   **Importar y exportar datos de SQL Server 2016 (32 bits)**  
  
    Ejecute la versión de 64 bits del asistente, a menos que sepa que el origen de datos requiere un proveedor de datos de 32 bits.
 
    ![Iniciar el asistente desde Inicio](../../integration-services/import-export-data/media/start-wizard-start.jpg)
  
## <a name="startCmd"></a> Command prompt
### <a name="start-the-sql-server-import-and-export-wizard-from-the-command-prompt"></a>Iniciar la importación de SQL Server y el Asistente para exportación desde la línea de comandos  
En una ventana del símbolo del sistema, ejecute **DTSWizard.exe** desde una de las siguientes ubicaciones.  
  
-   **C:\Archivos de programa\Microsoft SQL Server\130\DTS\Binn** para la versión de 64 bits.  
  
-   **C:\Archivos de programa (x86)\Microsoft SQL Server\130\DTS\Binn** para la versión de 32 bits.  
  
Ejecute la versión de 64 bits del asistente, a menos que sepa que el origen de datos requiere un proveedor de datos de 32 bits.

![Iniciar el asistente desde el símbolo del sistema](../../integration-services/import-export-data/media/start-wizard-cmd.jpg)  
  
## <a name="startSSMS"></a> SQL Server Management Studio (SSMS)
### <a name="start-the-sql-server-import-and-export-wizard-from-sql-server-management-studio-ssms"></a>Iniciar el Asistente de exportación y la importación de SQL Server desde SQL Server Management Studio (SSMS)    
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese a una instancia del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)].
    
2.  Expanda **Bases de datos**.
3.  Haga clic con el botón derecho en una base de datos.
4.  Seleccione **Tareas**.
5.  Haga clic en una de las opciones siguientes.
  
    -   **Importar datos**
      
    -   **Exportar datos**  

    ![Iniciar el asistente desde SSMS](../../integration-services/import-export-data/media/start-wizard-ssms.jpg) 

Si no tiene instalado SQL Server o si dispone de SQL Server pero no tiene instalado SQL Server Management Studio, consulte [Descargar SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx).
  
## <a name="startVS"></a>Visual Studio
### <a name="start-the-sql-server-import-and-export-wizard-from-visual-studio-with-sql-server-data-tools-ssdt"></a>Iniciar el Asistente de exportación y la importación de SQL Server desde Visual Studio con SQL Server Data Tools (SSDT) 
 En Visual Studio con [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], con un proyecto de Integration Services abierto, realice una de las acciones siguientes. 
  
-   En el menú **Proyecto** , haga clic en el **Asistente para importación y exportación de SSIS**. 

    ![Iniciar el asistente desde Proyecto](../../integration-services/import-export-data/media/start-wizard-project.jpg) 
    
    \- o bien
    
-   En el Explorador de soluciones, haga clic con el botón derecho en la carpeta **Paquetes SSIS** y haga clic en **Asistente para importación y exportación de SSIS**.

    ![Iniciar el asistente desde Paquetes](../../integration-services/import-export-data/media/start-wizard-packages.jpg)

Si no tiene instalado Visual Studio o si dispone de Visual Studio pero no tiene instalado SQL Server Data Tools, consulte [Descargar SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).

## <a name="get-the-wizard"></a>Obtener el Asistente
Si desea ejecutar el asistente, pero no tiene [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalado en el equipo, puede instalar el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la instalación de SQL Server Data Tools (SSDT). Para obtener más información, vea [Descargar SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).

## <a name="get-help-while-the-wizard-is-running"></a>Obtener ayuda mientras se ejecuta el Asistente
> [!TIP]
> Pulse la tecla F1 en cualquier página o cuadro de diálogo del Asistente para ver la documentación de la página actual.   

 ## <a name="whats-next"></a>¿Qué debe hacer a continuación?  
 Al iniciar el Asistente, la primera página es **Asistente para importación y exportación de SQL Server**. No hace falta que realice ninguna acción en esta página. Para obtener más información, vea [Asistente para importación y exportación de SQL Server](../../integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md).  
  
## <a name="related"></a>Contenido y las tareas relacionadas  
 A continuación, presentamos algunas otras tareas básicas.
-   **Vea un ejemplo rápido de cómo funciona el asistente.**

    -   **Si prefiere ver capturas de pantalla.** Eche un vistazo a este sencillo ejemplo de extremo a extremo en una sola página - [empezar a trabajar con este ejemplo sencillo de la importación y el Asistente para exportación de](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md).

    -   **Si prefiere ver un vídeo.** Vea este vídeo de cuatro minutos desde YouTube que muestra el asistente y se explica con claridad y simplemente cómo exportar datos a Excel - [mediante la importación de SQL Server y el Asistente para exportación para exportar a Excel](https://go.microsoft.com/fwlink/?linkid=829049).

-   **Más información sobre cómo funciona el asistente.**

    -   **Más información sobre el asistente.** Si quiere obtener información general sobre el asistente, consulte [Asistente para importación y exportación de SQL Server](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md).

    -   **Obtenga información acerca de los pasos del asistente.** Si desea obtener información acerca de los pasos del asistente, consulte [los pasos de la importación de SQL Server y el Asistente para exportación de](../../integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard.md). También hay una página independiente de la documentación de cada página del asistente.

    -   **Obtenga información acerca de cómo conectarse a orígenes de datos y destinos.** Si desea obtener información acerca de cómo conectarse a los datos, seleccione la página que desee en la lista aquí - [conectar a orígenes de datos con la importación de SQL Server y el Asistente para exportación de](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md). Hay una página independiente de la documentación de cada uno de varios orígenes de datos de uso frecuente.



