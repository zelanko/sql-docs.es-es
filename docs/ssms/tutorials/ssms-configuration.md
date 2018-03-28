---
Title: 'Tutorial: SQL Server Management Studio Components and Configuration'
description: Tutorial en el que se describen los componentes y las opciones de configuración básicas para su entorno de SQL Server Management Studio.
keywords: SQL Server, SSMS, SQL Server Management Studio
author: MashaMSFT
ms.author: mathoma
ms.date: 03/16/2018
ms.topic: Tutorial
ms.suite: sql
ms.prod_service: sql-tools
ms.reviewer: sstein
manager: craigg
ms.openlocfilehash: c9ede90c1232469797f85af353c7e3fced6851b5
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/21/2018
---
# <a name="tutorial-sql-server-management-studio-components-and-configuration"></a>Tutorial: Componentes y configuración de SQL Server Management Studio
En este tutorial se describen los distintos componentes de ventana que hay en SQL Server Management Studio (SSMS), así como algunas opciones de configuración básicas para el área de trabajo. En este artículo aprenderá lo siguiente: 
- Los distintos componentes que conforman el entorno de SSMS
- Cambiar el diseño del entorno y restablecerlo al diseño predeterminado
- Maximizar el editor de consultas
- Cambiar algunas opciones básicas, como las siguientes:
    - Cambiar la fuente
    - Configurar las opciones de inicio
    - Restablecer la configuración predeterminada.

## <a name="prerequisites"></a>Prerequisites
Para llevar a cabo este tutorial necesita tener SQL Server Management Studio.  

- Instale [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms).

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
 

    

## <a name="changing-the-environmental-layout"></a>Cambiar el diseño del entorno 
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
    
## <a name="maximizing-query-editor"></a>Maximizar el Editor de consultas
El editor de consultas se puede maximizar al modo de pantalla completa.

1. Haga clic en cualquier parte de la ventana del editor de consultas.
2. Presione MAYÚS + ALT + ENTRAR para alternar entre el modo normal y el modo de pantalla completa. 

Este método abreviado de teclado funciona con cualquier ventana de documento. 



## <a name="changing-basic-settings"></a>Cambiar la configuración básica
En esta sección se describe cómo modificar algunas opciones básicas en SSMS. Estas opciones están en la opción de menú **Herramientas**:

  ![Menú Herramientas](media/ssms-configuration/tools.png)


- La barra de herramientas resaltada se puede modificar yendo al menú **Herramientas** > **Personalizar**:

    ![Personalizar la barra de herramientas](media/ssms-configuration/toolbar.png)

- La fuente se puede cambiar en el menú **Herramientas** > **Opciones** > **Fuentes y colores**:

     ![Fuentes y colores](media/ssms-configuration/fontsandcolors.png)

- Las opciones de inicio determinan el aspecto del área de trabajo la primera vez que se inicia SSMS. Se pueden configurar en el menú **Herramientas** > **Opciones** > **Inicio**:
 
    ![Opciones de inicio](media/ssms-configuration/startup.png)

- Todas estas opciones se pueden exportar e importar desde el menú **Herramientas** > **Importar y exportar opciones**. 

    ![Opciones de importación + exportación](media/ssms-configuration/settings.png)
    - Aquí también puede restablecer toda la configuración a los valores predeterminados. 



