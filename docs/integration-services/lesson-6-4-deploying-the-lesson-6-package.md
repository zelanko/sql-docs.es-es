---
title: 'Paso 4: Implementar el paquete de la lección 6 | Microsoft Docs'
ms.custom: ''
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: b613cef7-7993-4d89-a429-a8251d74d435
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 501161af0ea953b528bca174ba0c910b1bb3bd09
ms.sourcegitcommit: 5ca813d045e339ef9bebe0991164a5d39c8c742b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/24/2019
ms.locfileid: "54880498"
---
# <a name="lesson-6-4-deploy-the-lesson-6-package"></a>Lección 6-4: Implementar el paquete de la lección 6

La implementación del paquete conlleva agregar el paquete al catálogo SSISDB de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en una instancia de SQL Server. En esta lección se agrega el paquete de la lección 6 al catálogo SSISDB, se establece el nuevo parámetro y se ejecuta el paquete. En esta lección se usa SQL Server Management Studio para agregar el paquete de la lección 6 al catálogo SSISDB e implementar el paquete. Después de implementar el paquete, se modifica el parámetro para que apunte a una ubicación nueva y luego se ejecuta el paquete.   
En esta tarea se:  

1. Agregará el paquete al catálogo SSISDB del nodo SSIS de SQL Server.  
  
2. Implementará el paquete.  
  
3. Establecerá el valor del parámetro de paquete.  

4. Ejecutará el paquete en SSMS.  
  
## <a name="locate-or-add-the-ssisdb-catalog"></a>Buscar o agregar el catálogo SSISDB  
  
1.  Seleccione **Iniciar** > **Todos los programas** > **Microsoft SQL Server 2017** y luego **SQL Management Studio**.  
  
2.  En el cuadro de diálogo **Conectar con el servidor**, compruebe la configuración predeterminada y seleccione **Conectar**. Para conectarse, el nombre del **Servidor** debe ser el nombre del equipo en el que está instalado SQL Server. Si el **Motor de base de datos** es una instancia con nombre, el nombre del **Servidor** debe ser el nombre de la instancia con el formato *\<nombre_equipo>\\\<nombre_instancia>*. 
  
3.  En el **Explorador de objetos**, expanda **Catálogos de Integration Services**.  
  
4.  Si no aparece ningún catálogo en **Catálogos de Integration Services**, agregue el catálogo SSISDB.  
  
5.  Para agregar el catálogo SSISDB, haga clic con el botón derecho en **Catálogos de Integration Services** y seleccione **Crear catálogo**.  
  
6.  En el cuadro de diálogo **Crear catálogo**, seleccione **Habilitar integración CLR**.  
  
7.  En el cuadro **Contraseña**, escriba una contraseña y después escríbala de nuevo en el cuadro **Vuelva a escribir la contraseña**. 
  
8.  Seleccione **Aceptar** para agregar el catálogo SSISDB.  
  
## <a name="add-the-package-to-the-ssisdb-catalog"></a>Agregar el paquete al catálogo SSISDB  
  
1.  En el **Explorador de objetos**, haga clic con el botón derecho en **SSISDB** y seleccione **Crear carpeta**.  
  
2.  En el cuadro de diálogo **Crear carpeta**, escriba Tutorial de SSIS en el cuadro Nombre de carpeta y seleccione **Aceptar**.  
  
3.  Expanda la carpeta **Tutorial de SSIS**, haga clic con el botón derecho en **Proyectos** y seleccione **Importar paquetes**.  
  
4.  En la página **Introducción** del **Asistente para la conversión de proyectos de Integration Services**, seleccione **Siguiente**.  
  
5.  En la página **Buscar paquetes**, asegúrese de que **Sistema de archivos** está seleccionado en la lista **Origen** y seleccione **Examinar**.  
  
6.  En el cuadro de diálogo **Buscar carpeta**, vaya a la carpeta que contiene este proyecto Tutorial de SSIS y seleccione **Aceptar**.  
  
7.  Seleccione **Siguiente**.  
  
8.  En la página Seleccionar paquetes debería ver los seis paquetes de Tutorial de SSIS. En la lista **Paquetes**, seleccione **Lesson 6.dtsx** y luego **Siguiente**.  
  
9. En la página **Seleccionar destino**, escriba **Implementación de Tutorial de SSIS** en el cuadro **Nombre de proyecto** y seleccione **Siguiente**.

10. Seleccione **Siguiente** en todas las páginas restantes del asistente hasta llegar a la página **Revisar**.  
  
11. En la página **Revisar**, seleccione **Convertir**.  
  
12. Cuando finalice la conversión, seleccione **Cerrar**.  
  
Al cerrar el Asistente para la conversión de proyectos de Integration Services, SSIS muestra el Asistente para implementación de Integration Services. Este asistente ahora se usa para implementar el paquete de la lección 6.  
  
1.  En la página **Introducción** del **Asistente para implementación de Integration Services**, revise los pasos para implementar el proyecto y seleccione **Siguiente**.  
  
2.  En la página **Seleccionar destino**, compruebe que el nombre de servidor es la instancia de SQL Server que contiene el catálogo SSISDB y que la ruta de acceso muestra **Implementación de Tutorial de SSIS** y después seleccione **Siguiente**.  
  
3.  En la página **Revisar**, revise el **Resumen** y seleccione **Implementar**.  
  
4.  Cuando finalice la implementación, seleccione **Cerrar**.  
  
5.  En el **Explorador de objetos**, haga clic con el botón derecho en **Catálogos de Integration Services** y seleccione **Actualizar**.  
  
6.  Expanda **Catálogos de Integration Services** y luego **SSISDB**. Continúe expandiendo el árbol por debajo de **Tutorial de SSIS** hasta haber expandido el proyecto por completo. Debería ver **Lesson 6.dtsx** en el nodo **Paquetes** del nodo **Implementación de Tutorial de SSIS**.  
  
7.  Para comprobar que el paquete está completo, haga clic con el botón derecho en **Lesson 6.dtsx** y seleccione **Configurar**. En el cuadro de diálogo **Configurar**, seleccione **Parámetros** y compruebe que existe una entrada con **Lesson 6.dtsx** como **Contenedor**, **VarFolderName** como **Nombre** y la ruta de acceso a **Nuevos datos de ejemplo** como valor y luego seleccione **Cerrar**.  
  
## <a name="create-and-populate-a-new-sample-data-folder"></a>Crear y rellenar una carpeta de nuevos datos de ejemplo  
  
1.  En el **Explorador de Windows**, en el nivel raíz de la unidad (por ejemplo, **C:\\**), cree una carpeta denominada **Datos de ejemplo dos**.  
  
2.  Abra la carpeta **Datos de ejemplo** desde los [requisitos previos de la lección 1](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites) y copie cualquiera de los tres archivos de ejemplo.  
  
3.  Vaya a la carpeta **Datos de ejemplo dos** y pegue los archivos copiados.  
  
## <a name="change-the-package-parameter-to-point-to-the-new-sample-data"></a>Cambiar el parámetro de paquete para que apunte a los nuevos datos de ejemplo  
  
1.  En el **Explorador de objetos**, haga clic con el botón derecho en **Lesson 6.dtsx** y seleccione **Configurar**.  
  
2.  En el cuadro de diálogo **Configurar**, cambie el valor de parámetro a la ruta de acceso a **Datos de ejemplo dos**, por ejemplo, **C:\\Datos de ejemplo dos**.  
  
3.  Seleccione **Aceptar** para cerrar el cuadro de diálogo **Configurar**.  
  
## <a name="test-the-lesson-6-package-deployment"></a>Probar la implementación del paquete de la lección 6  
  
1.  En el **Explorador de objetos**, haga clic con el botón derecho en **Lesson 6.dtsx** y seleccione **Ejecutar**.  
  
2.  En el cuadro de diálogo **Ejecutar paquete**, seleccione **Aceptar**.  
  
3.  En el cuadro de diálogo del mensaje, seleccione **Sí** para abrir el **Informe general**.  
  
El **Informe general** del paquete muestra el nombre del paquete y un resumen de estado. La sección **Información general de ejecución** muestra el resultado de cada tarea del paquete. La sección **Parámetros usados** muestra los nombres y valores de todos los parámetros empleados en la ejecución del paquete, incluido **VarFolderName**.  
  
