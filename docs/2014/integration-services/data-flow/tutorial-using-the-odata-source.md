---
title: 'Tutorial: Usar el origen OData [SSIS] | Documentos de Microsoft'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2c64cf8b-5edb-48df-8ffe-697096258f71
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: a9a680d00867de1a82a1ead0837961ce0492e466
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36109008"
---
# <a name="tutorial-using-the-odata-source-ssis"></a>Tutorial: Usar el origen OData [SSIS]
  En este tutorial se describe el proceso para extraer la colección **Employees** del servicio OData del ejemplo **Northwind** (http://services.odata.org/V3/Northwind/Northwind.svc/)) y, después, cargarlo en un archivo plano.  
  
## <a name="1-create-an-integration-services-project"></a>1. Crear un proyecto de Integration Services  
  
1.  Inicie **SQL Server Data Tools** o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
2.  Haga clic en **Archivo**, seleccione **Nuevo**y haga clic en **Proyecto**.  
  
3.  En el cuadro de diálogo **Nuevo proyecto** , expanda **Instalado**, expanda **Plantillas**, expanda **Business Intelligence**y haga clic en **Integration Services**.  
  
4.  Seleccione **Proyecto de Integration Services** como tipo de proyecto.  
  
5.  Escriba un **nombre** y seleccione una **ubicación** para el proyecto; a continuación, haga clic en **Aceptar**.  
  
## <a name="2-add-and-configure-odata-source-to-the-ssis-package"></a>2. Agregar y configurar el origen OData al paquete SSIS  
  
1.  Arrastre y coloque una **Tarea Flujo de datos** desde el **Cuadro de herramientas de SSIS** hasta la superficie de diseño del flujo de control del paquete SSIS.  
  
2.  Haga clic en la pestaña **Flujo de datos** o haga doble clic en la **Tarea Flujo de datos** recién agregada para iniciar la **superficie de diseño Flujo de datos**.  
  
3.  Arrastre y coloque **Origen OData** desde el grupo **Común** del **Cuadro de herramientas de SSIS**. La primera vez que se instala el **Origen OData** , aparecerá en el grupo **Común** del **Cuadro de herramientas de SSIS**.  
  
4.  Haga doble clic en el componente **Origen OData** para iniciar el cuadro de diálogo **Editor de origen OData** .  
  
5.  Haga clic en **Nuevo...** para agregar un nuevo Administrador de conexiones OData.  
  
6.  Escriba la dirección URL del servicio OData en **Ubicación de documento de servicio**. Puede ser la dirección URL del documento de servicio, o de una fuente o una entidad específica. Para este tutorial, escriba [ http://services.odata.org/V3/Northwind/Northwind.svc/ ](http://services.odata.org/V3/Northwind/Northwind.svc/).  
  
7.  Confirme que se ha seleccionado **Autenticación de Windows** como la **autenticación** que se usará para tener acceso al servicio OData. **Autenticación de Windows** está seleccionada de forma predeterminada. Para usar la autenticación básica, seleccione **Usar este nombre de usuario y esta contraseña**.  
  
8.  Haga clic en **Probar conexión** y, a continuación, haga clic en **Aceptar** para crear una instancia del Administrador de conexiones OData.  
  
9. En el cuadro de diálogo **Editor de origen OData** , confirme que se ha seleccionado **Colección** para la opción **Usar colección en la ruta de acceso a recursos** .  
  
10. En la lista desplegable **Colección** , seleccione **Employees**.  
  
11. Especifique cualquier otra opción o filtro de consulta adicional de OData en **Opciones de consulta**. Por ejemplo, $orderby=CompanyName&$top=100. Para este tutorial, escriba **$top=5**.  
  
12. Haga clic en **Vista previa** para obtener una vista previa de los datos.  
  
13. Haga clic en **Columnas** en el panel de navegación de la izquierda para cambiar a la página **Columnas** .  
  
14. Seleccione **EmployeeID**, **FirstName**y **LastName** en **Columnas externas disponibles** activando las casillas correspondientes.  
  
15. Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Editor de origen OData** .  
  
## <a name="3-add-flat-file-destination-and-test-the-solution"></a>3. Agregar el destino del archivo plano y probar la solución  
  
1.  Después, arrastre y coloque un **Destino de archivo plano** desde el **Cuadro de herramientas de SSIS** hasta la superficie de diseño Flujo de datos, debajo el componente **Origen OData**.  
  
2.  Conecte el componente **Origen OData** con el componente **Destino de archivo plano** usando la flecha azul.  
  
3.  Haga doble clic en **Destino de archivo plano**. Debe ver el cuadro de diálogo **Editor de destino de archivos planos** .  
  
4.  En el cuadro de diálogo **Editor de destino de archivos planos** , haga clic en **Nuevo** para crear un nuevo administrador de conexiones de archivos planos.  
  
5.  En el cuadro de diálogo **Formato del archivo plano** , seleccione **Delimitado**. Debe ver el cuadro de diálogo **Editor del administrador de conexiones de archivos planos** .  
  
6.  En el cuadro de diálogo **Editor del administrador de conexiones de archivos planos** , en **Nombre de archivo**, escriba **c:\Employees.txt**.  
  
7.  En el panel de navegación de la izquierda, haga clic en **Columnas**. Puede obtener una vista previa de los datos de esta página.  
  
8.  Haga clic en Aceptar para cerrar el cuadro de diálogo **Editor del administrador de conexiones de archivos planos** .  
  
9. En el cuadro de diálogo **Editor de destino de archivos planos** , haga clic en **Asignaciones** en el panel de navegación de la izquierda. Revise las asignaciones.  
  
10. Haga clic en Aceptar para cerrar el cuadro de diálogo **Editor de destino de archivos planos** .  
  
11. Genere y ejecute el paquete SSIS. Compruebe que el archivo de salida creado contiene el ID, First Name y Last Name de 5 empleados de la fuente OData.  
  
  