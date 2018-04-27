---
title: Iniciar el Asistente para importación y exportación de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/20/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: import-export-data
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
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
manager: craigg
ms.workload: Active
ms.openlocfilehash: 6e1016714fa05b35e4a762cb162fce7ce1a34305
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="start-the-sql-server-import-and-export-wizard"></a>Iniciar el Asistente para importación y exportación de SQL Server

 > Para el contenido relacionado con las versiones anteriores de SQL Server, vea [Ejecutar el Asistente para importación y exportación de SQL Server](https://msdn.microsoft.com/library/ms140052(SQL.120).aspx).

Inicie el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] siguiendo uno de los métodos que se describen en este tema para importar datos de cualquier origen de datos admitido o exportar datos a este.

> [!IMPORTANT]
> En este tema solo se describe cómo **iniciar** el asistente. Si busca algo más, consulte [Temas y tareas relacionados](#related).

Puede iniciar el asistente de las siguientes maneras:
-   En el [menú Inicio](#startStart).
-   En el [símbolo del sistema](#startCmd). 
-   En [SQL Server Management Studio (SSMS)](#startSSMS).
-   En [Visual Studio con SQL Server Data Tools (SSDT)](#startVS).

## <a name="prerequisite---is-the-wizard-installed-on-your-computer"></a>Requisito previo: ¿Está instalado el asistente en el equipo?
Si desea ejecutar el asistente, pero no tiene [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalado en el equipo, puede instalar el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la instalación de SQL Server Data Tools (SSDT). Para obtener más información, vea [Descargar SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).

> [!NOTE]
> Para usar la versión de 64 bits del asistente para importación y exportación de SQL Server, tendrá que instalar SQL Server. SQL Server Data Tools (SSDT) y SQL Server Management Studio (SSMS) son aplicaciones de 32 bits y solo instalan archivos de 32 bits, incluida la versión de 32 bits del asistente.

## <a name="startStart"></a> menú Inicio  
### <a name="start-the-sql-server-import-and-export-wizard-from-the-start-menu"></a>Iniciar el Asistente para importación y exportación de SQL Server desde el menú Inicio
1.  En el menú **Inicio**, busque y expanda **Microsoft SQL Server 2016**.
3.  Haga clic en una de las opciones siguientes.
  
    -   **Importar y exportar datos de SQL Server 2016 (64 bits)**
          
    -   **Importar y exportar datos de SQL Server 2016 (32 bits)**  
  
    Ejecute la versión de 64 bits del asistente, a menos que sepa que el origen de datos requiere un proveedor de datos de 32 bits.
 
    ![Iniciar el asistente desde Inicio](../../integration-services/import-export-data/media/start-wizard-start.jpg)
  
## <a name="startCmd"></a> Command prompt
### <a name="start-the-sql-server-import-and-export-wizard-from-the-command-prompt"></a>Iniciar el Asistente para importación y exportación de SQL Server desde el símbolo del sistema  
En una ventana del símbolo del sistema, ejecute **DTSWizard.exe** desde una de las siguientes ubicaciones.  
  
-   **C:\Archivos de programa\Microsoft SQL Server\130\DTS\Binn** para la versión de 64 bits.  
  
-   **C:\Archivos de programa (x86)\Microsoft SQL Server\130\DTS\Binn** para la versión de 32 bits.  
  
Ejecute la versión de 64 bits del asistente, a menos que sepa que el origen de datos requiere un proveedor de datos de 32 bits.

![Iniciar el asistente desde el símbolo del sistema](../../integration-services/import-export-data/media/start-wizard-cmd.jpg)  
  
## <a name="startSSMS"></a> SQL Server Management Studio (SSMS)
### <a name="start-the-sql-server-import-and-export-wizard-from-sql-server-management-studio-ssms"></a>Iniciar el asistente para importación y exportación de SQL Server desde SQL Server Management Studio (SSMS)    
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese a una instancia del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)].
    
2.  Expanda **Bases de datos**.
3.  Haga clic con el botón derecho en una base de datos.
4.  Seleccione **Tareas**.
5.  Haga clic en una de las opciones siguientes.
  
    -   **Importar datos**
      
    -   **Exportar datos**  

    ![Iniciar el asistente desde SSMS](../../integration-services/import-export-data/media/start-wizard-ssms.jpg) 

Si no tiene instalado SQL Server o si dispone de SQL Server pero no tiene instalado SQL Server Management Studio, consulte [Descargar SQL Server Management Studio (SSMS)](../../ssms/download-sql-server-management-studio-ssms.md).
  
## <a name="startVS"></a> Visual Studio
### <a name="start-the-sql-server-import-and-export-wizard-from-visual-studio-with-sql-server-data-tools-ssdt"></a>Iniciar el Asistente para importación y exportación de SQL Server desde Visual Studio con SQL Server Data Tools (SSDT) 
 En Visual Studio con [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], con un proyecto de Integration Services abierto, realice una de las acciones siguientes. 
  
-   En el menú **Proyecto** , haga clic en el **Asistente para importación y exportación de SSIS**. 

    ![Iniciar el asistente desde Proyecto](../../integration-services/import-export-data/media/start-wizard-project.jpg) 
    
    \- o bien
    
-   En el Explorador de soluciones, haga clic con el botón derecho en la carpeta **Paquetes SSIS** y haga clic en **Asistente para importación y exportación de SSIS**.

    ![Iniciar el asistente desde Paquetes](../../integration-services/import-export-data/media/start-wizard-packages.jpg)

Si no tiene instalado Visual Studio o si dispone de Visual Studio pero no tiene instalado SQL Server Data Tools, consulte [Descargar SQL Server Data Tools (SSDT)](../../ssdt/download-sql-server-data-tools-ssdt.md).

## <a name="get-the-wizard"></a>Obtener el asistente
Si desea ejecutar el asistente, pero no tiene [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalado en el equipo, puede instalar el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la instalación de SQL Server Data Tools (SSDT). Para obtener más información, vea [Descargar SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).

## <a name="get-help-while-the-wizard-is-running"></a>Obtener ayuda mientras se ejecuta el Asistente
> [!TIP]
> Pulse la tecla F1 en cualquier página o cuadro de diálogo del Asistente para ver la documentación de la página actual.   

 ## <a name="whats-next"></a>¿Qué sigue?  
 Al iniciar el Asistente, la primera página es **Asistente para importación y exportación de SQL Server**. No es necesario que realice ninguna acción en esta página. Para obtener más información, vea [Asistente para importación y exportación de SQL Server](../../integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md).  
  
## <a name="related"></a> Temas y tareas relacionados  
 A continuación, se presentan algunas tareas básicas adicionales.
-   **Vea un ejemplo rápido de cómo funciona el asistente.**

    -   **Si prefiere ver capturas de pantalla.** Eche un vistazo a este ejemplo sencillo y completo en una sola página: [Get started with this simple example of the Import and Export Wizard (Comenzar con este sencillo ejemplo del Asistente para importación y exportación)](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md).

    -   **Si prefiere ver un vídeo.** Aquí tiene un vídeo de cuatro minutos de YouTube en el que se muestra el asistente y se explica cómo exportar datos a Excel, con instrucciones claras y sencillas: [Using the SQL Server Import and Export Wizard to Export to Excel (Usar el Asistente para importación y exportación de SQL Server para exportar a Excel)](https://go.microsoft.com/fwlink/?linkid=829049).

-   **Obtenga más información sobre cómo funciona el asistente.**

    -   **Obtenga más información sobre el asistente.** Si quiere obtener información general sobre el asistente, consulte [Asistente para importación y exportación de SQL Server](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md).

    -   **Obtenga más información sobre los pasos del asistente.** Si está buscando información sobre los pasos del asistente, consulte [Steps in the SQL Server Import and Export Wizard (Pasos del asistente para importación y exportación de SQL Server)](../../integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard.md). También hay una página independiente de documentación para cada página del asistente.

    -   **Obtenga información sobre cómo conectarse a orígenes y destinos de datos.** Si está buscando información sobre cómo conectarse a sus datos, seleccione la página que quiera de esta lista: [Connect to data sources with the SQL Server Import and Export Wizard](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md) (Conexión a orígenes de datos con el Asistente para importación y exportación de SQL Server). Hay una página independiente de documentación para cada origen de datos de uso frecuente.


