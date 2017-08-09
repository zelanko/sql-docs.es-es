---
title: "Solucionar problemas de recuperación de datos de informes de Reporting Services | Documentos de Microsoft"
ms.custom: 
ms.date: 02/27/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7680946a-1660-4b59-a03a-c4d474cd8ed3
caps.latest.revision: 4
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 3f801ab4a8033d7f457aad0483ead5cb080fd8ed
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="troubleshoot-data-retrieval-issues-with-reporting-services-reports"></a>Solución de problemas de recuperación de datos de informes de Reporting Services
El primer paso durante el procesamiento de informes es recuperar los datos del informe para cada conjunto de datos ejecutando la consulta del conjunto de datos. Al obtener una vista previa de un informe localmente, las conexiones a un origen de datos y las credenciales deben utilizar los permisos suficientes para recuperar los datos en el equipo. Al ejecutar un informe en el servidor de informes, las conexiones a un origen de datos y las credenciales deben utilizar los permisos suficientes para recuperar los datos en el servidor de informes. Utilice este tema como ayuda para solucionar los problemas de la recuperación de datos del informe.   
  
## <a name="i-cannot-create-a-connection-to-a-data-source"></a>No puedo crear una conexión a un origen de datos.  
Al crear un origen de datos, ejecutar una consulta del conjunto de datos u ofrecer una vista previa de un informe, podría obtener el mensaje siguiente: No se puede crear una conexión al origen de datos `<data source name>`.   
    
### <a name="data-source-is-not-available"></a>El origen de datos no está disponible.  
El origen de datos está sin conexión o no está disponible por alguna otra razón.   
  
Compruebe que tiene acceso al origen de datos y que está disponible. Por ejemplo, utilice SQL Server Management Studio para conectarse al origen de datos. En las bases de datos relacionales y la base de datos multidimensional, utilice el botón **Probar** en el cuadro de diálogo **Propiedades de conexión** con el fin de comprobar la conexión y los permisos para el origen de datos.   
  
### <a name="data-source-credentials-are-not-valid"></a>Las credenciales del origen de datos no son válidas.  
Las credenciales que usa para conectarse al origen de datos no tienen permisos suficientes para recuperar los datos especificados en la consulta.  
  
Compruebe que las credenciales que está utilizando sean las correctas. Por ejemplo, puede tener permiso para recuperar los datos de una tabla o vista, pero no para una columna concreta; o podría no disponer de los permisos necesarios para ejecutar un procedimiento almacenado que rellena una vista.   
  
> [!NOTE]  
> Los permisos que utiliza para recuperar los datos de una vista previa de un informe pueden ser diferentes de los que se necesitan para recuperar los datos una vez publicado un informe en un servidor de informes.   
  
### <a name="not-a-valid-password"></a>La contraseña no es válida.  
Para los orígenes de datos con credenciales pedidas o credenciales especificados en la cadena de conexión, los caracteres de la contraseña se pasan a los controladores del origen de datos subyacente. Si la contraseña o la cadena contienen caracteres especiales como signos de puntuación, algunos controladores del origen de datos no pueden validar los caracteres especiales.   
  
Compruebe que la contraseña no incluya caracteres especiales. Si cambiar la contraseña resulta poco práctico, hable con el administrador de la base de datos para almacenar las credenciales adecuadas de forma local en el servidor como parte de un nombre del origen de datos OBDC (DSN) del sistema. Para más información, consulte "OdbcConnection.ConnectionString" en la documentación del SDK de .NET Framework en MSDN.   
  
> [!NOTE]  
>Se recomienda no agregar información de inicio de sesión, como contraseñas, a la cadena de conexión. El Diseñador de informes proporciona una página **Credenciales** en los cuadros de diálogo [Propiedades del origen de datos](~/reporting-services/report-data/enter-data-source-credentials-dialog-box-report-builder.md) o [Propiedades del origen de datos compartidos](~/reporting-services/report-data/enter-data-source-credentials-dialog-box-report-builder.md) que puede utilizar para escribir las credenciales. Estas credenciales se almacenan de forma segura en el equipo en el que se crea el informe.  
  
## <a name="why-do-i-see-no-data-when-i-run-my-query-in-the-query-designer"></a>¿Por qué no veo ningún dato cuando ejecuto una consulta en el diseñador de consultas?  
Cuando haya creado el conjunto de datos, la colección de campos de conjunto de datos aparecerá en el panel Datos de informe. A veces, la colección de campos del conjunto de datos no se muestra como se esperaba.   
  
### <a name="import-query-does-not-import-calculated-fields"></a>La consulta de importación no importa los campos calculados  
  
Aunque los campos calculados se guarden en una definición de informe, no se incluyen al importar una consulta del conjunto de datos desde otro informe. Solo los campos especificados por la consulta del conjunto de datos aparecen en el panel Datos de informe después de crear un conjunto de datos importando una consulta desde otro informe.   
  
Para ver los campos calculados en el panel Datos de informe, debe definirlos para cada informe en el que se utilizan.   
  
### <a name="some-data-providers-do-not-support-automatic-population-of-the-dataset-field-collection"></a>Algunos proveedores de datos no admiten el rellenado automático de la colección de campos de conjunto de datos  
Al definir una consulta en el cuadro de diálogo Propiedades del conjunto de datos y, a continuación, cerrar el cuadro de diálogo, la colección de campos de conjunto de datos normalmente aparece en el panel Datos de informe. Con algunos orígenes de datos, la colección de campos de conjunto de datos no se rellena de forma automática.   
  
Para rellenar la colección de campos de conjunto de datos, haga lo siguiente:  
* Asegúrese de que dispone de permisos para recuperar la información de los campos de la base de datos. En algunos orígenes de datos, puede que tenga permiso para obtener acceso al origen de datos pero no a la tabla o a la columna. Puede que disponga del permiso para tener acceso a una vista pero no de los permisos para ejecutar los procedimientos almacenados que crean la vista. Para validar su acceso a tablas o columnas concretas en una base de datos, compruebe los resultados de la consulta en una aplicación independiente como SQL Server Management Studio utilizando los mismos permisos que para el informe. Si no puede ver los resultados que desea para la consulta, trabaje con el administrador del sistema para ajustar sus permisos a los datos.   
* Ejecute la consulta en el panel de consulta del cuadro de diálogo **Propiedades del conjunto de datos** . Para más información, consulte [Conjuntos de datos de informe (Generador de informes 3.0 y SSRS)](../../reporting-services/report-data/report-datasets-ssrs.md).  
* Agregue campos manualmente. Para más información, consulte [Agregar, editar y actualizar campos en el panel Datos de informe (Generador de informes 3.0 y SSRS)](../../reporting-services/report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md).   
  
## <a name="see-also"></a>Vea también  
[Errores y eventos (Reporting Services)](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect.md)]




