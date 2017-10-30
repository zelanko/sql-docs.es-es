---
title: "Paso 4: Implementar el paquete de la lección 6 | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: b613cef7-7993-4d89-a429-a8251d74d435
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 504d9be296088cf3f455f8790ff013ab0c1df14b
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="lesson-6-4---deploying-the-lesson-6-package"></a>Lección 6-4: implementar el paquete de la lección 6
Implementar el paquete consiste en agregar el paquete al catálogo SSISDB de Integration Services en una instancia de SQL Server. En esta lección, agregará el paquete de la lección 6 en el catálogo SSISDB, establecerá el parámetro y ejecutará el paquete. Para esta lección, utilizará SQL Server Management Studio para agregar el paquete de la lección 6 al catálogo SSISDB e implementar el paquete. Después de implementar el paquete, modificará el parámetro para que señale una ubicación nueva y después ejecutará el paquete.  
  
En esta lección:  
  
-   Agregará el paquete al catálogo SSISDB del nodo SSIS de SQL Server.  
  
-   Implementará el paquete.  
  
-   Establecerá el valor del parámetro de paquete.  
  
-   Ejecutará el paquete en SSMS.  
  
### <a name="to-locate-or-add-the-the-ssisdb-catalog"></a>Para buscar o agregar el catálogo SSISDB  
  
1.  Haga clic en Inicio, señale Todos los programas, señale Microsoft SQL Server 2012 y después haga clic en SQL Management Studio.  
  
2.  En el cuadro de diálogo Conectar con el servidor, compruebe la configuración predeterminada y después haga clic en Conectar. Para conectarse, el cuadro Nombre de servidor debe contener el nombre del equipo en el que SQL Server está instalado. Si el motor de base de datos es una instancia con nombre, el cuadro Nombre del servidor también debe contener el nombre de la instancia con el formato <nombre_equipo>\\<nombre_instancia>.  
  
3.  En el Explorador de objetos, expanda catálogos de Integration Services.  
  
4.  Si no aparece ningún catálogo en catálogos de Integration Services, agregue el catálogo SSISDB.  
  
5.  Para agregar el catálogo SSISDB, haga clic con el botón derecho en catálogos de Integration Services y haga clic en Crear catálogo.  
  
6.  En el cuadro de diálogo Crear catálogo, seleccione Habilitar integración CLR  
  
7.  En el cuadro Contraseña, escriba una contraseña nueva y después escríbala de nuevo en el cuadro Vuelva a escribir la contraseña. Asegúrese de recordar la contraseña que escriba.  
  
8.  Haga clic en Aceptar para agregar el catálogo SSISDB.  
  
### <a name="to-add-the-package-to-the-ssisdb-catalog"></a>Para agregar el paquete en el catálogo SSISDB  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en SSISDB y después en Crear carpeta.  
  
2.  En el cuadro de diálogo Crear carpeta, escriba Tutorial de SSIS en el cuadro Nombre de carpeta y haga clic en Aceptar.  
  
3.  Expanda la carpeta Tutorial de SSIS, haga clic con el botón derecho en Proyectos y después en Importar paquetes.  
  
4.  En la página Introducción del Asistente para la conversión de proyectos de Integration Services, haga clic en Siguiente.  
  
5.  En la página Buscar paquetes, asegúrese de que Sistema de archivos está seleccionado en la lista de orígenes y haga clic en Examinar.  
  
6.  En el cuadro de diálogo Buscar carpeta, vaya a la carpeta que contiene el proyecto de Tutorial de SSIS y haga clic en Aceptar.  
  
7.  Haga clic en Siguiente.  
  
8.  En la página Seleccionar paquetes debería ver los seis paquetes de Tutorial de SSIS. En la lista Paquetes, seleccione Lesson 6.dtsx y haga clic en Siguiente.  
  
9. En la página Seleccionar destino, escriba Implementación del Tutorial de SSIS en el cuadro Nombre de proyecto y haga clic en Siguiente.  
  
10. Haga clic en Siguiente en todas las páginas restantes del asistente hasta llegar a la página Revisar.  
  
11. En la página Revisar, haga clic en Convertir.  
  
12. Cuando se complete la conversión, haga clic en Cerrar.  
  
Al cerrar el Asistente para la conversión de proyectos de Integration Services, SSIS muestra el Asistente para implementación de Integration Services. Ahora utilizará a este asistente para implementar el paquete de la lección 6.  
  
1.  En la página Introducción del Asistente para implementación de Integration Services, revise los pasos para implementar el proyecto y haga clic en Siguiente.  
  
2.  En la página Seleccionar destino, compruebe que el nombre de servidor es la instancia de SQL Server que contiene el catálogo SSISDB y que la ruta de acceso muestra la Implementación del Tutorial de SSIS; después, haga clic en Siguiente.  
  
3.  En la página Revisar, revise el Resumen y después haga clic en implementar.  
  
4.  Cuando se complete la implementación, haga clic en Cerrar.  
  
5.  En el Explorador de objetos, haga clic con el botón derecho en Catálogos de Integration Services y después en Actualizar.  
  
6.  Expanda los Catálogos de Integration Services y después SSISDB. Continúe expandiendo el árbol por debajo de Tutorial de SSIS hasta haber expandido el proyecto por completo. Debería ver Lesson 6.dtsx debajo del nodo Paquetes del nodo Implementación del Tutorial de SSIS.  
  
Para comprobar que el paquete está completo, haga clic en Lesson 6.dtsx y después en Configurar. En el cuadro de diálogo Configurar, seleccione Parámetros y compruebe que existe una entrada con Lesson 6.dtsx como Contenedor, VarFolderName como Nombre y la ruta de acceso a Nuevos datos de ejemplo como valor y después haga clic en Cerrar.  
  
Antes de continuar, cree una nueva carpeta de datos de ejemplo, asígnele el nombre Datos de ejemplo dos y copie cualquiera de los tres archivos de ejemplo originales en ella.  
  
### <a name="to-create-and-populate-a-new-sample-data-folder"></a>Para crear y rellenar una carpeta nueva de datos de ejemplo  
  
1.  En el Explorador de Windows, en el nivel de raíz de la unidad (por ejemplo, C:\\), cree una carpeta nueva denominada Datos de ejemplo dos.  
  
2.  Abra la carpeta c:\Archivos de programa\Microsoft SQL Server\110\Ejemplos\Servicios de integración\Tutorial\Creating a Simple ETL Package\Datos de muestra y, después, copie cualquiera de los tres archivos de ejemplo de la carpeta.  
  
3.  En la carpeta Nuevos datos de ejemplo, pegue los archivos copiados.  
  
### <a name="to-change-the-package-parameter-to-point-to-the-new-sample-data"></a>Para cambiar el parámetro de paquete para que señale a los nuevos datos de ejemplo  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en Lesson 6.dtsx y después en Configurar.  
  
2.  En el cuadro de diálogo Configurar, cambie el valor de parámetro a la ruta de acceso a Datos de ejemplo dos. Por ejemplo, C:\Datos de ejemplo dos si ha colocado la nueva carpeta en la carpeta raíz de la unidad C.  
  
3.  Haga clic en Aceptar para cerrar el cuadro de diálogo Configurar.  
  
### <a name="to-test-the-lesson-6-package-deployment"></a>Para probar la implementación del paquete de la lección 6  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en Lesson 6.dtsx y después en Ejecutar.  
  
2.  En el cuadro de diálogo Ejecutar paquete, haga clic en Aceptar.  
  
3.  En el cuadro de diálogo del mensaje, haga clic en Sí para abrir el informe de información general.  
  
Se visualiza el informe información general del paquete, que muestra el nombre del paquete y un resumen de estado. La sección Información general de ejecución muestra el resultado de cada tarea del paquete y la sección Parámetros usados muestra los nombres y valores de todos los parámetros utilizados en la ejecución del paquete, incluido VarFolderName.  
  
  
  

