---
Title: 'Tutorial: SQL Server Management Studio Components and Configuration'
description: Tutorial en el que se describen los componentes y las opciones de configuración básicas para su entorno de SQL Server Management Studio.
keywords: SQL Server, SSMS, SQL Server Management Studio
author: MashaMSFT
ms.author: mathoma
ms.date: 03/16/2018
ms.topic: Tutorial
ms.suite: sql
ms.prod: sql
ms.technology: ssms
ms.prod_service: sql-tools
ms.reviewer: sstein
manager: craigg
ms.openlocfilehash: 51fb197c3b5177c699134a48fc4888cd134e1711
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="tutorial-sql-server-management-studio-components-and-configuration"></a>Tutorial: Componentes y configuración de SQL Server Management Studio
En este tutorial se describen los distintos componentes de ventana que hay en SQL Server Management Studio (SSMS), así como algunas opciones de configuración básicas para el área de trabajo. En este artículo aprenderá lo siguiente: 

> [!div class="checklist"]
> * Los distintos componentes que conforman el entorno de SSMS
> * Cambiar el diseño del entorno y restablecerlo al diseño predeterminado
> * Maximizar el editor de consultas
> * Cambiar la fuente 
> * Configurar las opciones de inicio 
> * Restablecer la configuración predeterminada. 

## <a name="prerequisites"></a>Prerequisites
Para llevar a cabo este tutorial necesita tener SQL Server Management Studio.  

- Instale [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

## <a name="sql-server-management-studio-components"></a>Componentes de SQL Server Management Studio
En esta sección se describen los distintos componentes de ventana disponibles en el área de trabajo y su finalidad. 

- Los componentes de ventana se pueden cerrar pulsando la X situada en la esquina de la barra de título y se pueden volver a abrir desde el menú desplegable **Vista** del menú principal. 

    ![Menú Ver](media/ssms-configuration/viewmenu.png)

- **Explorador de objetos** (F8): el Explorador de objetos es una vista de árbol de todos los objetos de base de datos que contiene un servidor. Puede contener las bases de datos del Motor de base de datos de SQL Server, Analysis Services, Reporting Services e Integration Services. El Explorador de objetos incluye información de todos los servidores a los que está conectado. 
    
    ![Explorador de objetos](media/ssms-configuration/objectexplorer.png)
- **Ventana Consulta** (Ctrl + N): una vez que haya hecho clic en **Nueva consulta**, esta es la ventana en la que escribirá las consultas de Transact-SQL (T-SQL). Los resultados de las consultas también se pueden ver aquí.
    
    ![Ventana Nueva consulta](media/ssms-configuration/newquery.png)

- **Propiedades** (F4): se pueden ver al abrir la **ventana Consulta**. Se muestran las propiedades básicas de la consulta. Por ejemplo, se mostrará la hora de inicio de una consulta, el número de filas devueltas o los detalles de conexión.  

    ![Propiedades](media/ssms-configuration/properties.png)

- **Explorador de plantillas** (Ctrl + Alt + T): hay una serie de plantillas predefinidas de T-SQL que encontrará en el Explorador de plantillas. Estas plantillas le permiten llevar a cabo distintas funciones, como crear una base de datos o hacer una copia de seguridad de la base de datos. 

    ![Explorador de plantillas](media/ssms-configuration/templates.png)

- **Detalles del Explorador de objetos** (F7): se trata de una vista más detallada de lo que se puede ver en el Explorador de objetos. Le permite manipular varios objetos a la vez. Por ejemplo, en la ventana Detalles del Explorador de objetos puede seleccionar varias bases de datos al mismo tiempo y eliminarlas o generar un script para ellas. 

    ![Detalles del Explorador de objetos](media/ssms-configuration/objectexplorerdetails.PNG) 
 

    

## <a name="change-the-environmental-layout"></a>Cambio del diseño del entorno 
En esta sección se describe la manipulación del diseño del entorno (por ejemplo, mover las distintas ventanas). 

-  Todos los componentes de ventana se pueden mover manteniendo presionado el título y arrastrando la ventana. 
- Todos los componentes de ventana se pueden anclar y desanclar seleccionando el icono de la chincheta de la barra de título:
    
    ![Anclar objetos](media/ssms-configuration/pushpin.png)

- Todos los componentes de ventana tienen una flecha desplegable que permite manipular la ventana de distintas maneras: 

    ![Ventana Opciones](media/ssms-configuration/windowoptions.png)

- Una vez que tenga dos o más ventanas de consulta abiertas, puede desplazarse por ellas mediante la tabulación de forma vertical u horizontal de modo que las dos ventanas estén siempre visibles. Para ello, haga clic con el botón derecho en el título de la consulta y seleccione la opción de tabulación que quiera. 
 
    ![Opciones de tabulación de consultas](media/ssms-configuration/querytabbedoptions.png)

    - Este es el **grupo de pestañas horizontal**: ![Grupo de pestañas horizontal](media/ssms-configuration/horizontaltab.png)     
    
    - Este es el **grupo de pestañas vertical**:  
        ![Grupo de pestañas vertical](media/ssms-configuration/verticaltabgroup.png)
        

    - Para volver a combinar las pestañas, vuelva a hacer clic con el botón derecho en el título de la consulta y seleccione **Move to Next Tab Group** (Ir al siguiente grupo de pestañas) o **Move to Previous Tab Group** (Ir al grupo de pestañas anterior):
    
        ![Combinar pestañas de consulta](media/ssms-configuration/mergetabgroups.png)

- Para restaurar el diseño de entorno predeterminado, haga clic en el **menú Ventana** > **Restablecer diseño de la ventana**:
 
    ![Restablecer diseño de la ventana](media/ssms-configuration/resetwindowlayout.png)
    
## <a name="maximize-query-editor"></a>Maximizar el editor de consultas
El editor de consultas se puede maximizar al modo de pantalla completa.

1. Haga clic en cualquier parte de la ventana del editor de consultas.
2. Presione MAYÚS + ALT + ENTRAR para alternar entre el modo normal y el modo de pantalla completa. 

Este método abreviado de teclado funciona con cualquier ventana de documento. 



## <a name="change-basic-settings"></a>Cambio de la configuración básica
En esta sección se describe cómo modificar algunas opciones básicas en SSMS. Estas opciones están en la opción de menú **Herramientas**:

  ![Menú Herramientas](media/ssms-configuration/tools.png)


- La barra de herramientas resaltada se puede modificar yendo al menú **Herramientas** > **Personalizar**:

    ![Personalizar la barra de herramientas](media/ssms-configuration/toolbar.png)

### <a name="change-the-font"></a>Cambio del tamaño de fuente
- La fuente se puede cambiar en el menú **Herramientas** > **Opciones** > **Fuentes y colores**:

     ![Fuentes y colores](media/ssms-configuration/fontsandcolors.png)

### <a name="change-the-startup-options"></a>Cambio de las opciones de inicio
- Las opciones de inicio determinan el aspecto del área de trabajo la primera vez que se inicia SSMS. Se pueden configurar en el menú **Herramientas** > **Opciones** > **Inicio**:
 
    ![Opciones de inicio](media/ssms-configuration/startup.png)

### <a name="reset-settings-to-default"></a>Restablecimiento de la configuración predeterminada
- Todas estas opciones se pueden exportar e importar desde el menú **Herramientas** > **Importar y exportar opciones**. 

    ![Opciones de importación + exportación](media/ssms-configuration/settings.png)
    - Aquí también puede restablecer toda la configuración a los valores predeterminados. 


## <a name="next-steps"></a>Pasos siguientes
En el artículo siguiente se le enseñarán algunos trucos y consejos adicionales para usar SSMS, como dónde encontrar el registro de errores de SQL Server o el nombre de instancia de SQL. 

Vaya al siguiente artículo para obtener más información
> [!div class="nextstepaction"]
> [Botón de pasos siguientes](ssms-tricks.md)
 
 




