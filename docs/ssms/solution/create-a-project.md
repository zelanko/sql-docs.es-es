---
title: Crear un proyecto
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- projects [SQL Server Management Studio], creating
ms.assetid: 7897be19-365b-4b06-bcf0-8a669f67a673
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.openlocfilehash: 2ad58a10987050bcd89e17e2a3dbef4fd39586d1
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "75251932"
---
# <a name="create-a-project"></a>Crear un proyecto

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Puede crear uno o varios proyectos nuevos en una solución existente.  
  
## <a name="create-a-new-project-and-add-it-to-a-solution"></a>Crear un proyecto y agregarlo a una solución  
  
1.  En el Explorador de soluciones, seleccione la solución.  
  
2.  En el menú **Archivo** , seleccione **Agregar**y haga clic en **Nuevo proyecto**.  
  
3.  En el cuadro de diálogo  **Nuevo proyecto** , haga clic en un tipo de proyecto.  
  
    **Templates** (Plantillas [C++])  
    En el cuadro **Plantillas** , seleccione una plantilla. Aparecerá una breve descripción de la plantilla del proyecto seleccionado debajo del cuadro **Plantillas** .  
  
    **Nombre**  
    Escriba el nombre del proyecto de scripts que desea crear. También se creará una carpeta con el mismo nombre que el proyecto en la ubicación que aparece en el campo **Ubicación** . En algunos proyectos, [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] crea archivos de origen y otros archivos de compatibilidad, y los agrega a la nueva carpeta del proyecto.  
  
    > [!NOTE]  
    > En algunos tipos de proyecto, el cuadro de texto **Nombre** no está disponible porque al especificar la ubicación se establece el nombre. Por ejemplo, las aplicaciones y los servicios web se ubican en un servidor web y obtienen su nombre del directorio virtual especificado en ese servidor.  
  
    Los nombres no pueden contener los siguientes caracteres:  
  
    -   Número (#)  
  
    -   Porcentaje (%)  
  
    -   Símbolo de y comercial (&)  
  
    -   Asterisco (*)  
  
    -   Barra vertical (|)  
  
    -   Barra diagonal inversa (\\)  
  
    -   Dos puntos (:)  
  
    -   Comillas (")  
  
    -   Menor que (\<)  
  
    -   Mayor que (>)  
  
    -   Signo de interrogación (?)  
  
    -   Barra diagonal (/)  
  
    -   Espacios iniciales y finales (' ')  
  
    -   Nombres reservados para Microsoft Windows o MS-DOS, como ("nul", "aux", "con", "com1", "lpt1", etc.)  
  
    **Ubicación**  
    Escriba la ubicación donde desea crear el proyecto o elija una en la lista.  
  
    **Browse**  
    Muestra el cuadro de diálogo **Ubicación del proyecto** , que le permite navegar a un nuevo directorio en el que guardar el proyecto.  
  
    **Solución**  
    Seleccione **Crear nueva solución** para crear una solución en el Explorador de soluciones. Seleccione **Agregar a solución** para agregar el nuevo proyecto a la solución actualmente abierta en el Explorador de soluciones.  
  
    **Crear directorio para la solución**  
    Seleccione habilitar el cuadro de texto **Nombre (solución)** . Esta opción crea un nuevo directorio del nombre elegido para el proyecto y la solución.  
  
    **Nombre de solución**  
    Especifique el nombre de la nueva solución en la que desea crear el proyecto. De manera predeterminada, este campo utiliza el mismo nombre que el especificado en el campo **Nombre** .  
  
    **Nota** Para tener acceso a esta opción, deberá seleccionar **Crear nueva solución** en las casillas **Solución** y **Crear directorio para la solución** . Algunas plantillas de proyecto no admiten esta opción, como las aplicaciones web.  
  
    **Agregar al control de código fuente**  
    Cuando esta casilla está seleccionada, la aplicación de control de código fuente se abre al hacer clic en **Aceptar**. Complete la información que necesite la aplicación de control de código fuente para continuar. Para utilizar esta opción, deberá tener una aplicación cliente de control de código fuente instalada.  
  
4.  Haga clic en **OK**.  
  
Puede establecer un nombre para el proyecto de script, aunque [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] establece los nombres de las carpetas y no se pueden modificar. Puede configurar la unidad y la especificación de la ruta de acceso de los conjuntos comunes de carpetas mediante el cuadro de diálogo **Agregar nuevo proyecto** . Haga clic con el botón derecho en el icono de soluciones del **Explorador de soluciones**y, a continuación, haga clic en **Agregar**. La ubicación predeterminada de las carpetas de los proyectos de script es: C:\Documents and Settings\\*NombreDeUsuario*\Mis documentos\SQL Server Management Studio\Projects\\.  
  
## <a name="see-also"></a>Consulte también

[Explorador de soluciones](../../ssms/solution/solution-explorer.md)  
[Agregar un proyecto existente a una solución](../../ssms/solution/add-an-existing-project-to-a-solution.md)  
[Agregar nuevos elementos a un proyecto](../../ssms/solution/add-new-items-to-a-project.md)  
[Agregar elementos existentes a un proyecto](../../ssms/solution/add-existing-items-to-a-project.md)  
[Cambiar la ubicación predeterminada de los proyectos](../../ssms/solution/change-the-default-location-for-projects.md)  
[Quitar o eliminar un elemento o un proyecto](../../ssms/solution/remove-or-delete-an-item-or-project.md)  
[Eliminar una solución](../../ssms/solution/delete-a-solution.md)  