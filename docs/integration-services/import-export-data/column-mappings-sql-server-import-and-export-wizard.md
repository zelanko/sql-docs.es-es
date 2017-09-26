---
title: Asignaciones de columnas (SQL Server importar y exportar) | Documentos de Microsoft
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.columnmapandtransform.f1
ms.assetid: eadc54a6-f936-4ffc-91d7-fbfd2bdcab93
caps.latest.revision: 69
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b1ed879f21396c3c8d588307eaf087daea8c44c3
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="column-mappings-sql-server-import-and-export-wizard"></a>Asignaciones de columnas (Asistente para importación y exportación de SQL Server)
  Después de seleccionar las tablas y vistas existentes para copiar o revisar la consulta que ha proporcionado, si hace clic en **Editar asignaciones**, el Asistente para importar y exportar de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muestra el cuadro de diálogo **Asignaciones de columnas** . En esta página especificar y configurar columnas de destino para recibir los datos copiados desde las columnas de origen. A menudo no tiene que cambiar nada en esta página.
  
Si no desea copiar todas las columnas en la tabla seleccionada, único lo que puede hacer en esta página es excluir las columnas que no desea. Seleccione **omitir** en el **destino** columna de la **asignaciones** lista para las columnas que no desea copiar.
 
## <a name="screen-shot-of-the-column-mappings-page"></a>Captura de pantalla de la página Asignaciones de columnas 
 La captura de pantalla siguiente muestra un ejemplo de la **asignaciones de columnas** cuadro de diálogo del asistente. 
 
 En este ejemplo, puede ver que el asistente va a crear una nueva tabla de destino, porque la opción **Crear tabla de destino** está seleccionada. De forma predeterminada, el asistente asigna cada columna en la nueva tabla de destino el mismo nombre, tipo de datos y propiedades como la columna de origen correspondiente. 
  
 ![Página de asignaciones de columna de la importación y el Asistente para exportación de](../../integration-services/import-export-data/media/column-mappings.png "página de asignaciones de columna de la importación y el Asistente para exportación")  
  
## <a name="review-the-source-and-destination"></a>Revise el origen y destino 
![Sección de página, origen y destino de asignaciones de columna](../../integration-services/import-export-data/media/column-mappings-page-source-and-destination-section.png)

 **Source**  
 La tabla de origen seleccionada, vista o consulta.  
  
 **Destino**  
 La tabla de destino seleccionada o la vista.  

## <a name="optionally-create-a-new-destination-table"></a>Si lo desea, cree una nueva tabla de destino
![Página de asignaciones de columna, nueva sección de tabla](../../integration-services/import-export-data/media/column-mappings-page-new-table-section.png)

 **Crear tabla o archivo de destino**  
 Crear la tabla de destino si aún no existe.    
  
 **Editar SQL**  
Haga clic en **Editar SQL** para abrir el cuadro de diálogo **Instrucción Create Table de SQL** . Utilice la instrucción CREATE TABLE de generadas automáticamente o modificarlo para sus fines. Si cambia esta instrucción de manera manual, tiene que asegurarse de que la lista de asignaciones de columnas reconozca los cambios. Para más información, vea [Instrucción Create Table de SQL](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md).  

### <a name="sometimes-these-options-are-disabled"></a>A veces, estas opciones están deshabilitadas
El **crear tabla de destino** opción y la **Editar SQL** botón se habilita automáticamente o deshabilita automáticamente.

-   **Habilitado.** Si ha especificado un **nueva** tabla de destino en la **seleccionar tablas de origen y vistas** página, el **crear tabla de destino** opción se selecciona automáticamente y la ** Editar SQL** botón está habilitado.

-   **Deshabilitado.** Si ha seleccionado un **existente** tabla de destino en la **seleccionar tablas de origen y vistas** página, el **crear tabla de destino** opción y la **Editar SQL ** botón se deshabilita. Si desea crear una nueva tabla de destino, vuelva a la **seleccionar tablas de origen y vistas** página y escriba el nombre de un **nueva** tabla el **destino** columna.  

## <a name="what-about-existing-data-in-the-destination"></a>¿Qué ocurre con los datos existentes en el destino?
![Página de asignaciones de columna, sección de opciones](../../integration-services/import-export-data/media/column-mappings-page-options-section.png)

 **Eliminar filas en la tabla o archivo de destino**  
 Especifique si deben eliminarse datos de una tabla existente antes de cargar los datos nuevos.  
  
 **Anexar filas a la tabla o archivo de destino**  
 Especifique si deben anexarse datos nuevos a los datos que contiene una tabla existente.  
  
 **Quitar y volver a crear la tabla de destino**  
 Elija esta opción para sobrescribir la tabla de destino. Esta opción solo está disponible cuando se utiliza el Asistente para crear la tabla de destino. La tabla de destino se quita y se vuelve a crear solo si guarda el paquete que el asistente crea y después vuelve a ejecutar el paquete. Esta es una opción adecuada si quiere probar la configuración varias veces.
  
 **Habilitar la inserción de identidad**  
 Elija esta opción para poder insertar los valores de identidad existentes del origen de datos en una columna de identidad de la tabla de destino. De manera predeterminada, la columna de identidad de destino normalmente no lo permite.  
  
> [!TIP]
> Si las claves principales existentes están en una columna de identidad, una columna autonumérica o su equivalente, normalmente es necesario seleccionar esta opción para mantener los valores de clave principales existentes.  De lo contrario, la columna de identidad de destino normalmente asigna nuevos valores.  

## <a name="keep-your-autonumber-or-identity-values"></a>Mantener los valores de autonumeración o la identidad
Si va a exportar los datos que tienen una columna Autonumérica o una columna de identidad: por ejemplo, si va a exportar desde Microsoft Access - Asegúrese de que selecciona **Habilitar inserción de identidad** tal como se describió inmediatamente.

## <a name="review-column-mappings"></a>Revise las asignaciones de columna
![Página de asignaciones de columna, sección asignaciones](../../integration-services/import-export-data/media/column-mappings-page-mappings-section.png)

 **Asignaciones**  
 Muestra el modo en que cada columna del origen de datos se asigna a una columna en el destino.
 
La lista **Asignaciones** tiene las columnas siguientes:  
  
-    **Source**  
     Muestre cada columna de origen.  
  
-   **Destino**  
    Vea la columna de destino asignada o seleccione una columna diferente.
    
    No tienes que copiar todas las columnas de la tabla de origen. Seleccione **Omitir** en esta columna para las columnas que quiera omitir. Antes de asignar columnas, debe omitir todas las columnas que no se asignarán.  
  
-   **Tipo**  
    Vea el tipo de datos de la columna de destino o seleccione un tipo de datos diferente.
  
-   **Admisión de valores NULL**  
    Especifique si la columna de destino permite un valor NULL.  
  
-   **Tamaño**  
    Especifique el número de caracteres de la columna de destino, si corresponde.  
  
-    **Precisión**  
    Especifique la precisión de datos numéricos en la columna de destino: es decir, el número de dígitos: si es aplicable.  
  
 -   **Escala**  
    Especifique la escala de los datos numéricos en la columna de destino: es decir, el número de posiciones decimales - si es aplicable.  
  
## <a name="whats-next"></a>¿Qué debe hacer a continuación?  
 Después de revisar y configurar columnas de destino para recibir los datos copiados desde las columnas de origen y haga clic en **Aceptar**, **asignaciones de columnas** cuadro de diálogo vuelve a la **seleccionar archivos de origen Tablas y vistas** página o a la **configurar destino de archivo plano** página. Para más información, vea [Seleccionar tablas y vistas de origen](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md) o [Configurar el destino del archivo plano](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md).  
  
 Si especifica una asignación que puede que no se realice correctamente en la lista **Asignaciones** , el cuadro de diálogo **Asignaciones de columnas** le lleva a la página **Revisar asignación de tipos de datos** . En esta página, revise las advertencias, especifique las opciones de conversión y también especifique cómo controlar los errores. Para más información, vea [Revisar asignación de tipos de datos](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md).  
 
 ## <a name="see-also"></a>Vea también
[Asignación de tipos de datos en el Asistente para importación y exportación de SQL Server](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)  
[Comenzar con este sencillo ejemplo del Asistente para importar y exportar](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)


