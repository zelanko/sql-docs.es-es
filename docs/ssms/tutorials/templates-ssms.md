---
Title: 'Tutorial: Using Templates in SQL Server Management Studio'
description: Tutorial para usar plantillas en SSMS. .
keywords: SQL Server, SSMS, SQL Server Management Studio, Plantillas
author: MashaMSFT
ms.author: mathoma
ms.date: 03/13/2018
ms.topic: Tutorial
ms.suite: sql
ms.prod: sql
ms.technology: ssms
ms.prod_service: sql-tools
ms.reviewer: sstein
manager: craigg
helpviewer_keywords:
- templates [SQL Server], SQL Server Management Studio
- source controls [SQL Server Management Studio], tutorials
- Help [SQL Server], SQL Server Management Studio
- tutorials [SQL Server Management Studio]
- Transact-SQL tutorials
- SQL Server Management Studio [SQL Server], tutorials
- scripts [SQL Server], SQL Server Management Studio
ms.openlocfilehash: f981d8455f82db44979a04611e861bb4d13d20d4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="tutorial-using-templates-within-sql-server-management-studio"></a>Tutorial: Usar plantillas en SQL Server Management Studio
En este tutorial se presentan las plantillas predefinidas de Transact-SQL (T-SQL) que están disponibles en SQL Server Management Studio (SSMS). En este artículo aprenderá a:

> [!div class="checklist"]
> * Usar el Explorador de plantillas para generar scripts de T-SQL
> * Editar una plantilla existente 
> * Buscar las plantillas en el disco
> * Crear una plantilla
   

## <a name="prerequisites"></a>Prerequisites
Para llevar a cabo este tutorial necesita tener SQL Server Management Studio, así como acceso a un servidor SQL Server. 

- Instale [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms).
- Instale [SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads).

 

## <a name="using-the-template-browser"></a>Usar el Explorador de plantillas
En esta sección aprenderá a buscar y usar el **Explorador de plantillas**. 

1. Inicie SQL Server Management Studio.
2. En el menú **Vista** > **Explorador de plantillas** (Ctrl + Alt + T): 

    ![Explorador de plantillas](media/templates-ssms/templatebrowser.png)
    - También puede ver las plantillas que se han usado recientemente en la parte inferior del **Explorador de plantillas**.

3. Expanda el nodo que le interese > haga clic con el botón derecho en la plantilla > Abrir:

    ![Abrir la plantilla](media/templates-ssms/opentemplate.png)
    - Si se hace doble clic en la plantilla, el efecto será el mismo.

4. Se abrirá una nueva ventana de consulta con el código T-SQL ya rellenado. 
5. Modifique la plantilla según sus necesidades y, después, seleccione **Ejecutar** para ejecutar la consulta:
    
    ![Crear una plantilla de base de datos](media/templates-ssms/createdbtemplate.png)


## <a name="edit-an-existing-template"></a>Editar una plantilla existente
También puede editar las plantillas existentes en el **Explorador de plantillas**.  

1. Busque la plantilla que quiera en el **Explorador de plantillas**.
2. Haga clic con el botón derecho en la plantilla > **Editar**:

    ![Editar plantilla](media/templates-ssms/edittemplate.png)

3. Haga los cambios que quiera en la ventana de consulta que se abre.
4. Guarde la plantilla yendo a **Archivo** > **Guardar** (Ctrl + S).
5. Cierre la ventana de consulta.
6. Vuelva a abrir la plantilla que acaba de guardar. Las ediciones deberían aparecer ahí.
 

## <a name="locate-the-templates-on-disk"></a>Búsqueda de plantillas en el disco
Cuando una plantilla esté abierta, podrá buscarla en el disco.

1. Seleccione una plantilla en el **Explorador de plantillas** > **Editar**.
2. Haga clic con el botón derecho en el **título de la consulta** > **Abrir carpeta contenedora**. Se debería abrir el explorador en la ubicación en la que se almacenan en disco las plantillas: 

    ![Plantillas en el disco](media/templates-ssms/templatesondisk.png)
  

## <a name="create-a-new-template"></a>Creación de una plantilla
En el **Explorador de plantillas** también puede crear plantillas. Estos pasos le enseñarán a crear una carpeta y, después, una plantilla dentro de esa carpeta, aunque con estos pasos también puede crear una plantilla personalizada dentro de las carpetas existentes. 

1. Abra el **Explorador de plantillas**.
2. Haga clic con el botón derecho en Plantillas de SQL Server > **Nuevo** > **Carpeta**.
3. Asigne a esta carpeta el nombre **Plantillas personalizadas**:

    ![Crear plantillas personalizadas](media/templates-ssms/creatingcustomtemplate.png)

4. Haga clic con el botón derecho en la carpeta **Plantillas personalizadas** que acaba de crear > **Nuevo** > **Plantilla** > asigne un nombre a la plantilla:
 
    ![Crear una plantilla personalizada](media/templates-ssms/createnewtemplate.png)
   
5. Haga clic con el botón derecho en la plantilla que acaba de crear > **Editar**. Se abrirá una **nueva ventana de consulta**.
6. Escriba el texto del código T-SQL que quiere guardar. 
7. Guarde el archivo yendo al menú **Archivo** > **Guardar**.
8. Cierre la **ventana de consulta** existente y abra la nueva plantilla personalizada. 

    

## <a name="next-steps"></a>Pasos siguientes
En el siguiente artículo se proporcionan algunas recomendaciones y trucos adicionales para usar SQL Server Management Studio. 

Vaya al siguiente artículo para obtener más información
> [!div class="nextstepaction"]
> [Botón de pasos siguientes](ssms-tricks.md)
