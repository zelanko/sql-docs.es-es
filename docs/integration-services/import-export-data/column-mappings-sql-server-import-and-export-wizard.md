---
title: Asignaciones de columnas (Asistente para importación y exportación de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.columnmapandtransform.f1
ms.assetid: eadc54a6-f936-4ffc-91d7-fbfd2bdcab93
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a16e270acae2a2685bcaf53045883eaa078ab03d
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "71285930"
---
# <a name="column-mappings-sql-server-import-and-export-wizard"></a>Asignaciones de columnas (Asistente para importación y exportación de SQL Server)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Después de seleccionar las tablas y vistas existentes para copiar o revisar la consulta que ha proporcionado, si hace clic en **Editar asignaciones**, el Asistente para importar y exportar de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muestra el cuadro de diálogo **Asignaciones de columnas** . En esta página puede especificar y configurar columnas de destino para recibir los datos copiados de las columnas de origen. A menudo no tiene que cambiar nada en esta página.
  
Si no quiere copiar todas las columnas de la tabla seleccionada, una de las cosas que puede hacer en esta página es excluir las columnas no deseadas. Seleccione **omitir** en la columna **Destino** de la lista **Asignaciones** para aquellas columnas que no quiera copiar.
 
## <a name="screen-shot-of-the-column-mappings-page"></a>Captura de pantalla de la página Asignaciones de columnas 
 En la siguiente captura de pantalla se muestra el cuadro de diálogo **Asignaciones de columnas** del asistente. 
 
 En este ejemplo, puede ver que el asistente va a crear una nueva tabla de destino, porque la opción **Crear tabla de destino** está seleccionada. De manera predeterminada, el asistente asigna a cada columna de la nueva tabla de destino el mismo nombre, el mismo tipo de datos y las mismas propiedades que la columna de origen correspondiente. 
  
 ![Página de asignaciones de columnas del Asistente para importar y exportar](../../integration-services/import-export-data/media/column-mappings.png "Página de asignaciones de columnas del Asistente para importar y exportar")  
  
## <a name="review-the-source-and-destination"></a>Revisar el origen y el destino 
![Página Asignaciones de columnas, sección de origen y destino](../../integration-services/import-export-data/media/column-mappings-page-source-and-destination-section.png)

 **Origen**  
 Tabla de origen, vista o consulta seleccionada.  
  
 **Destino**  
 Tabla de destino o vista seleccionada.  

## <a name="optionally-create-a-new-destination-table"></a>De manera opcional, cree una nueva tabla de destino.
![Página Asignaciones de columnas, sección de nueva tabla](../../integration-services/import-export-data/media/column-mappings-page-new-table-section.png)

 **Crear tabla o archivo de destino**  
 Cree la tabla de destino si aún no existe.    
  
 **Editar SQL**  
Haga clic en **Editar SQL** para abrir el cuadro de diálogo **Instrucción Create Table de SQL** . Use la instrucción CREATE TABLE generada automáticamente o modifíquela según sus necesidades. Si cambia esta instrucción de manera manual, tiene que asegurarse de que la lista de asignaciones de columnas reconozca los cambios. Para más información, vea [Instrucción Create Table de SQL](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md).  

### <a name="sometimes-these-options-are-disabled"></a>A veces, estas opciones están deshabilitadas
La opción **Create destination table/file** (Crear tabla o archivo de destino) y el botón **Editar SQL** se habilita o deshabilita automáticamente.

-   **Habilitado.** Si ha especificado una tabla de destino **nueva** en la página **Seleccionar tablas y vistas de origen**, la opción **Crear tabla de destino** se selecciona automáticamente y el botón **Editar SQL** se habilita.

-   **Deshabilitado.** Si ha seleccionado una tabla de destino **existente** en la página **Seleccionar tablas y vistas de origen**, la opción **Crear tabla de destino** y el botón **Editar SQL** se deshabilitan. Si quiere crear una tabla de destino nueva, vuelva a la página **Seleccionar tablas y vistas de origen** y especifique el nombre de una tabla **nueva** en la columna **Destino**.  

## <a name="what-about-existing-data-in-the-destination"></a>¿Qué sucede con los datos existentes en el destino?
![Página Asignaciones de columnas, sección de opciones](../../integration-services/import-export-data/media/column-mappings-page-options-section.png)

 **Eliminar filas en la tabla o archivo de destino**  
 Especifique si deben eliminarse datos de una tabla existente antes de cargar los datos nuevos.  
  
 **Anexar filas a la tabla o archivo de destino**  
 Especifique si deben anexarse datos nuevos a los datos que contiene una tabla existente.  
  
 **Quitar y volver a crear la tabla de destino**  
 Elija esta opción para sobrescribir la tabla de destino. Esta opción solo está disponible si se usa el asistente para crear la tabla de destino. La tabla de destino se quita y se vuelve a crear solo si guarda el paquete que el asistente crea y después vuelve a ejecutar el paquete. Esta es una opción adecuada si quiere probar la configuración varias veces.
  
 **Habilitar la inserción de identidad**  
 Elija esta opción para poder insertar los valores de identidad existentes del origen de datos en una columna de identidad de la tabla de destino. De manera predeterminada, la columna de identidad de destino normalmente no lo permite.  
  
> [!TIP]
> Si las claves principales existentes están en una columna de identidad, una columna autonumérica o su equivalente, normalmente es necesario seleccionar esta opción para mantener los valores de clave principales existentes.  De lo contrario, la columna de identidad de destino normalmente asigna nuevos valores.  

## <a name="keep-your-autonumber-or-identity-values"></a>Mantener los valores de autonumeración o identidad
Si exporta datos que tienen una columna de autonumeración o una columna de identidad (por ejemplo, si realiza la exportación desde Microsoft Access), asegúrese de seleccionar **Habilitar la inserción de identidad** de acuerdo con la descripción inmediatamente anterior.

## <a name="review-column-mappings"></a>Revisar las asignaciones de columnas
![Página Asignaciones de columnas, sección de asignaciones](../../integration-services/import-export-data/media/column-mappings-page-mappings-section.png)

 **Asignaciones**  
 Muestra el modo en que cada columna del origen de datos se asigna a una columna en el destino.
 
La lista **Asignaciones** tiene las columnas siguientes:  
  
-    **Origen**  
     Vea cada una de las columnas de origen.  
  
-   **Destino**  
    Vea la columna de destino asignada o seleccione una columna diferente.
    
    No tiene que copiar todas las columnas de la tabla de origen. Seleccione **Omitir** en esta columna para las columnas que quiera omitir. Antes de asignar columnas, debe omitir todas las columnas que no se asignarán.  
  
-   **Tipo**  
    Vea el tipo de datos de la columna de destino o seleccione un tipo de datos diferente.
  
-   **Admisión de valores NULL**  
    Especifique si la columna de destino permite un valor NULL.  
  
-   **Tamaño**  
    Especifique el número de caracteres de la columna de destino, si corresponde.  
  
-    **Precisión**  
    Especifique la precisión de los datos numéricos en la columna de destino, que hace referencia al número de dígitos, si corresponde.  
  
 -   **Escala**  
    Especifique la escala de datos numéricos en la columna de destino, que hace referencia al número de posiciones decimales, si corresponde.  
  
## <a name="whats-next"></a>¿Qué sigue?  
 Después de revisar y configurar las columnas de destino para recibir los datos copiados de las columnas de origen y hacer clic en **Aceptar**, el cuadro de diálogo **Asignaciones de columnas** le devolverá a la página **Seleccionar tablas y vistas de origen** o a la página **Configurar el destino del archivo plano**. Para más información, vea [Seleccionar tablas y vistas de origen](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md) o [Configurar el destino del archivo plano](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md).  
  
 Si especifica una asignación que puede que no se realice correctamente en la lista **Asignaciones** , el cuadro de diálogo **Asignaciones de columnas** le lleva a la página **Revisar asignación de tipos de datos** . En esta página, revise las advertencias, especifique las opciones de conversión y también especifique cómo controlar los errores. Para más información, vea [Revisar asignación de tipos de datos](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md).  
 
 ## <a name="see-also"></a>Consulte también
[Asignación de tipos de datos en el Asistente para importación y exportación de SQL Server](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)  
[Comenzar con este sencillo ejemplo del Asistente para importar y exportar](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)

