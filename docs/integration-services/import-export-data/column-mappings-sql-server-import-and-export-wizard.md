---
title: "Asignaciones de columnas (Asistente para importaci&#243;n y exportaci&#243;n de SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.impexpwizard.columnmapandtransform.f1"
ms.assetid: eadc54a6-f936-4ffc-91d7-fbfd2bdcab93
caps.latest.revision: 69
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 58
---
# Asignaciones de columnas (Asistente para importaci&#243;n y exportaci&#243;n de SQL Server)
  Después de seleccionar las tablas y vistas existentes para copiar o revisar la consulta que ha proporcionado, si hace clic en **Editar asignaciones**, el Asistente para importar y exportar de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muestra el cuadro de diálogo **Asignaciones de columnas**. En esta página puede especificar y configurar columnas de destino para recibir los datos copiados.  
 
## <a name="screen-shot-of-the-column-mappings-page"></a>Captura de pantalla de la página Asignaciones de columnas 
 En la siguiente captura de pantalla se muestra el cuadro de diálogo **Asignaciones de columnas** del asistente. 
 
 En este ejemplo, puede ver que el asistente va a crear una nueva tabla de destino, porque la opción **Crear tabla de destino** está seleccionada. De manera predeterminada, cada columna de la nueva tabla de destino tiene el mismo nombre, tipo de datos y propiedades que la columna de origen correspondiente. 
  
 ![Column mappings page of the Import and Export Wizard](../../integration-services/import-export-data/media/column-mappings.png "Column mappings page of the Import and Export Wizard")  
  
## <a name="confirm-the-source-and-destination"></a>Confirmar el origen y destino  
 **Origen**  
 Identifica la tabla, vista o consulta de origen seleccionada.  
  
 **Destino**  
 Identifica la tabla o vista de destino seleccionada.  

## <a name="create-a-new-destination-table"></a>Crear una tabla de destino
 **Crear tabla o archivo de destino**  
 Cree la tabla de destino si aún no existe.    
  
 **Editar SQL**  
Haga clic en **Editar SQL** para abrir el cuadro de diálogo **Instrucción Create Table de SQL**. Use la instrucción CREATE TABLE predeterminada o modifíquela según sus necesidades. Si cambia esta instrucción de manera manual, tiene que asegurarse de que la lista de asignaciones de columnas reconozca los cambios. Para más información, vea [Instrucción Create Table de SQL](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md).  
  
 > [!TIP] Si ha especificado una nueva tabla de destino en la página **Seleccionar tablas y vistas de origen**, la opción **Crear tabla de destino** se selecciona automáticamente y el botón **Editar SQL** se habilita. De otro modo, si quiere crear la tabla de destino, tiene que volver a la página **Seleccionar tablas y vistas de origen** y especificar el nombre de una tabla **nueva** en la columna **Destino**.
>
> Si la opción **Crear tabla de destino** y el botón **Editar SQL** están deshabilitados en la página **Asignaciones de columnas**, vuelva a la página **Seleccionar tablas y vistas de origen** y escriba el nombre de una tabla **nueva** en la columna **Destino**. Si ha especificado una nueva tabla o tablas de destino en la página y ha hecho clic en **Siguiente**, la opción **Crear tabla de destino** se selecciona automáticamente y el botón **Editar SQL** se habilita en la página **Asignaciones de columnas**. Seleccione **Editar SQL** para mostrar el cuadro de diálogo **Instrucción Create Table de SQL**.  

## <a name="specify-options-for-existing-data-in-the-destination"></a>Especificar opciones para los datos existentes en el destino
 **Eliminar filas en la tabla o archivo de destino**  
 Especifique si deben eliminarse datos de una tabla existente antes de cargar los datos nuevos.  
  
 **Anexar filas a la tabla o archivo de destino**  
 Especifique si deben anexarse datos nuevos a los datos que contiene una tabla existente.  
  
 **Quitar y volver a crear la tabla de destino**  
 Elija esta opción para sobrescribir la tabla de destino. Esta opción solo está disponible si se usa el asistente para crear la tabla de destino. La tabla de destino se quita y se vuelve a crear solo si guarda el paquete que el asistente crea y después vuelve a ejecutar el paquete. Esta es una opción adecuada si quiere probar la configuración varias veces.
  
 **Habilitar la inserción de identidad**  
 Elija esta opción para poder insertar los valores de identidad existentes del origen de datos en una columna de identidad de la tabla de destino. De manera predeterminada, la columna de identidad de destino normalmente no lo permite.  
  
> [!TIP] Si las claves principales existentes están en una columna de identidad, una columna autonumérica o su equivalente, normalmente es necesario seleccionar esta opción para mantener los valores de clave principales existentes.  De lo contrario, la columna de identidad de destino normalmente asigna nuevos valores.  

## <a name="review-column-mappings-and-destination-data-types"></a>Revisar la asignación de columnas y los tipos de datos de destino 
 **Asignaciones**  
 Muestra el modo en que cada columna del origen de datos se asigna a una columna en el destino.
 
 Seleccione **Omitir** en la columna de **destino** para las columnas que no quiere copiar. No tiene que copiar todas las columnas en una tabla.  
 
 ![Asignaciones de columnas: asignaciones](../../integration-services/import-export-data/media/column-mappings-mappings.png)
  
 La lista **Asignaciones** tiene las columnas siguientes:  
  
-    **Origen**  
     Vea cada columna de origen para la que puede especificar la configuración de conversión si es necesario.  
  
-   **Destino**  
    Vea la columna de destino asignada o seleccione una columna diferente.
    
    Especifique si desea omitir una columna durante la operación de copia. Puede copiar solo un subconjunto de columnas si selecciona **Omitir** en esta columna para las columnas que quiera omitir. Antes de asignar columnas, debe omitir todas las columnas que no se asignarán.  
  
-   **Tipo**  
    Vea el tipo de datos de la columna de destino o seleccione un tipo de datos diferente.
  
-   **Admisión de valores NULL**  
    Especifique si la columna de destino permite un valor NULL.  
  
-   **Tamaño**  
    Especifique el número de caracteres de la columna de destino, si corresponde.  
  
-    **Precisión**  
    Especifique la precisión de datos numéricos en la columna de destino, que hace referencia al número de dígitos, si corresponde.  
  
 -   **Escala**  
    Especifique la escala de datos numéricos en la columna de destino, que hace referencia al número de posiciones decimales, si corresponde.  
  
## <a name="whats-next"></a>¿Qué debe hacer a continuación?  
 Después de especificar y configurar las columnas de destino para recibir los datos copiados y hacer clic en **Aceptar**, el cuadro de diálogo **Asignaciones de columnas** le devolverá a la página **Seleccionar tablas y vistas de origen** o a la página **Configurar el destino del archivo plano**. Para más información, vea [Seleccionar tablas y vistas de origen](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md) o [Configurar el destino del archivo plano](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md).  
  
 Si especifica una asignación que puede que no se realice correctamente en la lista **Asignaciones**, el cuadro de diálogo **Asignaciones de columnas** le lleva a la página **Revisar asignación de tipos de datos**. En esta página, revise las advertencias, especifique las opciones de conversión y también especifique cómo controlar los errores. Para más información, vea [Revisar asignación de tipos de datos](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md).  
 
 ## <a name="see-also"></a>Vea también
[Asignación de tipos de datos en el Asistente para importación y exportación de SQL Server](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)
