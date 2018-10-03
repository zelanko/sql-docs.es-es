---
Title: 'Tutorial: Using templates in SQL Server Management Studio'
description: Tutorial para usar plantillas en SSMS.
keywords: SQL Server, SSMS, SQL Server Management Studio, Plantillas
author: MashaMSFT
ms.author: mathoma
ms.date: 03/13/2018
ms.topic: Tutorial
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
ms.openlocfilehash: 4d3f2de58bdbfb4f476710bb9bb629dcac3db940
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47670043"
---
# <a name="tutorial-using-templates-in-sql-server-management-studio"></a>Tutorial: uso de plantillas en SQL Server Management Studio
En este tutorial se presentan las plantillas predefinidas de Transact-SQL (T-SQL) que están disponibles en SQL Server Management Studio (SSMS). En este artículo aprenderá a:

> [!div class="checklist"]
> * Usar el explorador de plantillas para generar scripts de T-SQL
> * Editar una plantilla existente 
> * Buscar plantillas en el disco
> * Crear una plantilla
   

## <a name="prerequisites"></a>Prerequisites
Para llevar a cabo este tutorial, necesita tener SQL Server Management Studio, así como acceso a un servidor SQL Server. 

- Instale [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
- Instale [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads).

 

## <a name="use-template-browser"></a>Usar el explorador de plantillas
En esta sección aprenderá a buscar y usar el explorador de plantillas. 

1. Abra SQL Server Management Studio.
2. En el menú **Vista**, seleccione **Explorador de plantillas** (Ctrl + Alt + T): 

    ![Abrir el explorador de plantillas](media/templates-ssms/templatebrowser.png)
    
    Puede ver las plantillas que se han usado recientemente en la parte inferior del explorador de plantillas.

3. Expanda el nodo que le interesa. Haga clic con el botón derecho en la plantilla y, después, seleccione **Abrir**:

    ![Abrir una plantilla](media/templates-ssms/opentemplate.png)
    
    También puede hacer doble clic en el nombre de la plantilla para abrirla.

4. Se abrirá una nueva ventana de consulta. El script de T-SQL ya se habrá rellenado. 
5. Modifique la plantilla según sus necesidades y, después, seleccione **Ejecutar** para ejecutar la consulta:
    
    ![Crear una plantilla de base de datos](media/templates-ssms/createdbtemplate.png)


## <a name="edit-an-existing-template"></a>Editar una plantilla existente
También puede editar las plantillas existentes en el explorador de plantillas.  

1. En Explorador de plantillas, vaya a la plantilla con la que quiere trabajar.
2. Haga clic con el botón derecho en la plantilla y, después, seleccione **Editar**:

    ![Editar una plantilla](media/templates-ssms/edittemplate.png)

3. En la ventana de consulta que se abre, efectúe los cambios que quiera.
4. Para guardar la plantilla, seleccione **Archivo** > **Guardar** (Ctrl + S).
5. Cierre la ventana de consulta.
6. Vuelva a abrir la plantilla. Deberían aparecer las ediciones.
 

## <a name="locate-templates-on-disk"></a>Buscar plantillas en el disco
Si tiene una plantilla abierta, puede buscar las plantillas que están en el disco.

1. En Explorador de plantillas, seleccione una plantilla y, después, seleccione **Editar**.
2. Haga clic con el botón derecho en **Título de la consulta** y, después, seleccione **Abrir carpeta contenedora**. Se debería abrir el explorador en la ubicación en la que se almacenan en disco las plantillas: 

   ![Plantillas en el disco](media/templates-ssms/templatesondisk.png)
  

## <a name="create-a-new-template"></a>Crear una plantilla
También puede crear una plantilla en Explorador de plantillas. En los siguientes pasos se indica cómo crear una carpeta y, después, crear una plantilla dentro de esa carpeta. También puede seguir estos pasos para crear una plantilla personalizada en una carpeta existente. 

1. Abra Explorador de plantillas.
2. Haga clic con el botón derecho en **Plantillas de SQL Server** y, después, seleccione **Nuevo** > **Carpeta**.
3. Asigne a esta carpeta el nombre **Plantillas personalizadas**:

    ![Crear una carpeta de plantillas personalizadas](media/templates-ssms/creatingcustomtemplate.png)

4. Haga clic con el botón derecho en la carpeta Plantillas personalizadas que acaba de crear y, después, seleccione **Nuevo** > **Plantilla**. Escriba un nombre para la plantilla:
 
    ![Crear una plantilla personalizada](media/templates-ssms/createnewtemplate.png)
   
5. Haga clic con el botón derecho en la plantilla que ha creado y, después, seleccione **Editar**. Se abrirá la ventana Nueva consulta.
6. Escriba el texto de T-SQL que quiere guardar. 
7. En el menú **Archivo**, seleccione **Guardar**.
8. Cierre la ventana de consulta existente y abra la nueva plantilla personalizada. 

    

## <a name="next-steps"></a>Pasos siguientes
En el siguiente artículo se proporcionan recomendaciones y trucos adicionales para usar SQL Server Management Studio. 

> [!div class="nextstepaction"]
> [Otras recomendaciones y trucos al usar SSMS](ssms-tricks.md)
