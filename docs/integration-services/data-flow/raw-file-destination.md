---
title: Destino de archivo sin formato | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.rawfiledest.f1
- sql13.dts.designer.rawfiledestinationconnectionmanager.f1
- sql13.dts.designer.rawfiledestinationcolumns.f1
helpviewer_keywords:
- append options [Integration Services]
- destinations [Integration Services], Raw File
- raw data [Integration Services]
- writing raw data
- Raw File destination
ms.assetid: d311b458-aefc-4b4d-b1a1-4c0ebbb34214
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c89496fabad28d3491d9b2f648d6355ae404685b
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/20/2019
ms.locfileid: "58282309"
---
# <a name="raw-file-destination"></a>destino de archivo sin formato
  El destino de archivo sin formato escribe datos sin procesar en un archivo. Como el formato de los datos es el nativo del destino, no es necesario traducir los datos y prácticamente no es necesario analizar el archivo. Esto significa que el destino de archivo sin formato puede escribir datos más rápidamente que otros destinos, como el destino de archivo plano o los destinos de OLE DB.  
  
 Además de escribir datos sin procesar en un archivo, puede utilizar el destino de archivo sin formato para generar un archivo sin formato vacío que contenga solo las columnas (archivo solo para metadatos), sin tener que ejecutar el paquete. El origen de archivo sin formato se usa para recuperar datos sin formato escritos previamente por el destino. Puede también designar el origen de archivo sin formato para el archivo que solo tiene metadatos.  
  
 El archivo sin formato contiene información sobre el orden. El destino de archivo sin formato guarda toda la información sobre el orden incluidas las marcas de comparación para las columnas de cadena. El origen de archivo sin formato lee y respeta la información sobre el orden. Tiene la opción de configurar el origen de archivo sin formato para omitir los marcas de orden en el archivo; para ello use el Editor avanzado. Para obtener más información acerca de las marcas de comparación, vea [Comparing String Data](../../integration-services/data-flow/comparing-string-data.md).  
  
 Puede configurar el destino de archivo sin formato de las maneras siguientes:  
  
-   Especifique un modo de acceso que sea el nombre del archivo o una variable que contenga el nombre del archivo en el que escribe el destino de archivo sin formato.  
  
-   Indique si el destino de archivo sin formato anexa datos a un archivo existente que tiene el mismo nombre o crea un nuevo archivo.  
  
 El destino de archivo sin formato con frecuencia se usa para escribir resultados intermedios de datos procesados parcialmente entre ejecuciones de paquetes. El almacenamiento de datos sin procesar significa que los datos pueden ser leídos rápidamente por un origen de archivo sin formato y luego se pueden transformar todavía más antes de que se carguen en su destino final. Por ejemplo, un paquete puede ejecutarse varias veces y cada vez puede escribir datos sin procesar en los archivos. Posteriormente, otro paquete puede usar el origen de archivo sin formato para leer de cada archivo, usar una transformación Unión de todo para combinar los datos en un solo conjunto de datos y luego aplicar transformaciones adicionales que resuman los datos antes de cargar los datos en su destino final, como una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  El destino de archivo sin formato admite datos NULL pero no admite datos de objetos binarios grandes (BLOB).  
  
> [!NOTE]  
>  El destino de archivo sin formato no usa un administrador de conexiones.  
  
 Este origen tiene una entrada normal. No admite una salida de error.  
  
## <a name="append-and-new-file-options"></a>Opciones de anexar y nuevo archivo  
 La propiedad WriteOption incluye opciones para anexar datos a un archivo existente o para crear un archivo.  
  
 En la tabla siguiente se describen las opciones disponibles para la propiedad WriteOption.  
  
|Opción|Descripción|  
|------------|-----------------|  
|Anexar|Anexa datos a un archivo existente. Los metadatos de los datos anexados deben coincidir con el formato del archivo.|  
|Crear siempre|Crea siempre un nuevo archivo.|  
|Crear una vez|Crea un nuevo archivo. Si existe el archivo, el componente genera un error.|  
|Truncar y anexar|Trunca un archivo existente y luego escribe los datos en el archivo. Los metadatos de los datos anexados deben coincidir con el formato del archivo.|  
  
 Los siguientes elementos son importantes cuando se anexan datos:  
  
-   Cuando se anexan datos a un archivo sin formato existente no se vuelven a ordenar.  
  
     Debe asegurarse de que las claves ordenadas permanecen en el orden correcto.  
  
-   Cuando se anexan datos a un archivo sin formato existente no se cambian los metadatos del archivo (información sobre el orden).  
  
 Por ejemplo, un paquete lee los datos ordenados en ProductKey (PK). El flujo de datos del paquete anexa los datos a un archivo sin formato existente. La primera vez que se ejecuta un paquete, se reciben tres filas (PK 1000, 1100, 1200). Ahora, el archivo sin formato contiene los datos siguientes.  
  
-   1000, productA  
  
-   1100, productB  
  
-   1200, productC  
  
 La segunda vez que se ejecuta el paquete, se reciben dos filas nuevas (PK 1001, 1300). Ahora, el archivo sin formato contiene los datos siguientes.  
  
-   1000, productA  
  
-   1100, productB  
  
-   1200, productC  
  
-   1001, productD  
  
-   1300, productE  
  
 Los datos nuevos se anexan al final del archivo sin formato y las claves ordenadas (PK) no se incluyen en el orden. Además, la operación de anexar no ha cambiado los metadatos del archivo (información sobre el orden). Si lee el archivo con el origen de archivo sin formato, el componente indica que el archivo todavía está ordenado según PK aunque los datos del archivo ya no estén en el orden correcto.  
  
 Para mantener las claves ordenadas en el orden correcto mientras se anexan datos, puede diseñar el flujo de datos del paquete como sigue:  
  
1.  Recupere filas nuevas mediante Origen A.  
  
2.  Recupere filas existentes desde RawFile1 con Origen B.  
  
3.  Combine las entradas Origen A y Origen B mediante la transformación Unión de todo.  
  
4.  Ordene según PK.  
  
5.  Escriba en RawFile2 mediante el destino de archivo sin formato.  
  
     RawFile1 está bloqueado porque se está leyendo en el flujo de datos.  
  
6.  Reemplace RawFile1 con RawFile2.  
  
### <a name="using-the-raw-file-destination-in-a-loop"></a>Usar el destino de archivo sin formato en un bucle  
 Si el flujo de datos que usa el destino de archivo sin formato se encuentra en un bucle, puede resultar conveniente crear el archivo una vez y, después, agregar los datos al archivo cuando se repita el bucle. Para agregar los datos al archivo, los datos agregados deben tener el mismo formato que el archivo existente.  
  
 Para crear el archivo en la primera iteración del bucle y, posteriormente, agregar filas en las iteraciones subsiguientes, debe hacer lo siguiente en tiempo de diseño:  
  
1.  Establezca la propiedad WriteOption en **CreateOnce** o **CreateAlways**y ejecute una iteración del bucle. Se crea el archivo. Así se garantiza que los metadatos de los datos agregados y del archivo sean iguales.  
  
2.  Restablezca la propiedad WriteOption a **Append** y establezca la propiedad ValidateExternalMetadata en **False**.  
  
 Si usa la opción **TruncateAppend** en lugar de la opción **Append** , truncará las filas que se agregaron en toda iteración anterior y anexará filas nuevas. Con la opción **TruncateAppend** también es necesario que los datos tengan el mismo formato que el archivo.  
  
## <a name="configuration-of-the-raw-file-destination"></a>Configuración del destino de archivo sin formato  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propiedades personalizadas de archivo sin formato](../../integration-services/data-flow/raw-file-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obtener información sobre cómo establecer las propiedades del componente, vea [Establecer las propiedades de un componente de flujo de datos](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="related-content"></a>Contenido relacionado  
 Entrada del blog, sobre los [archivos sin formato](https://www.sqlservercentral.com/blogs/stratesql/archive/2011/1/1/31-days-of-ssis-_1320_-raw-files-are-awesome-_2800_1_2F00_31_2900_.aspx), en sqlservercentral.com  
  
## <a name="raw-file-destination-editor-connection-manager-page"></a>Editor de destino de archivos sin formato (página Administrador de conexiones)
  Use el editor de destino de archivos sin formato para configurar el destino de archivo sin formato con el fin de escribir datos sin formato en un archivo.  
  
 **¿Qué desea hacer?**  
  
-   [Abra el editor de destino de archivos sin formato](#open)  
  
-   [Establecer opciones en la pestaña Administrador de conexiones](#connection)  
  
-   [Establecer las opciones de la pestaña Columnas](#mapping)  
  
###  <a name="open"></a> Abra el editor de destino de archivos sin formato  
  
1.  Agregue el destino de archivo sin formato a un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  Haga clic con el botón derecho en el componente y, después, haga clic en **Editar**.  
  
###  <a name="connection"></a> Establecer opciones en la pestaña Administrador de conexiones  
 **Modo de acceso**  
 Seleccione cómo se especifica el nombre de archivo. Seleccione **Nombre de archivo** para escribir el nombre de archivo y la ruta de acceso directamente o **Nombre de archivo de la variable** para especificar una variable que contiene el nombre de archivo.  
  
 **Nombre de archivo** o **Nombre de variable**  
 Escriba el nombre y la ruta de acceso del archivo sin formato o seleccione la variable que contiene el nombre de archivo.  
  
 **Opción de escritura**  
 Seleccione el método que va a utilizar para crear y escribir en el archivo.  
  
 **Generar un archivo sin formato inicial**  
 Haga clic en el botón para generar un archivo sin formato vacío que contenga solo las columnas (solo archivos de metadatos), sin tener que ejecutar el paquete. El archivo contiene las columnas seleccionadas en la página **Columnas:** del **Editor de destino de archivos sin formato**. Puede designar el origen de archivo sin formato para este archivo que solo tiene metadatos.  
  
 Al hacer clic en **Generar archivo sin formato inicial**, aparece un cuadro de mensaje. Haga clic en **Aceptar** para continuar con la creación del archivo. Haga clic en **Cancelar** para seleccionar otra lista de columnas en la página **Columnas:** .  
  
###  <a name="mapping"></a> Establecer las opciones de la pestaña Columnas  
 **Columnas de entrada disponibles**  
 Seleccione una o varias columnas de entrada para escribir en el archivo sin formato.  
  
 **Columna de entrada**  
 Una columna de entrada se agrega automáticamente a esta tabla cuando se selecciona en **Columnas de entrada disponibles**, o puede seleccionar la columna de entrada directamente en esta tabla.  
  
 **Alias de salida**  
 Especifique un nombre alternativo para usarlo en la columna de salida.  
  
## <a name="raw-file-destination-editor-columns-page"></a>Editor de destino de archivo sin formato (página Columnas)
  Use el editor de destino de archivos sin formato para configurar el destino de archivo sin formato con el fin de escribir datos sin formato en un archivo.  
  
 **¿Qué desea hacer?**  
  
-   [Abra el editor de destino de archivos sin formato](#open)  
  
-   [Establecer opciones en la pestaña Administrador de conexiones](#connection)  
  
-   [Establecer las opciones de la pestaña Columnas](#mapping)  
  
###  <a name="open"></a> Abra el editor de destino de archivos sin formato  
  
1.  Agregue el destino de archivo sin formato a un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  Haga clic con el botón derecho en el componente y, después, haga clic en **Editar**.  
  
###  <a name="connection"></a> Establecer opciones en la pestaña Administrador de conexiones  
 **Modo de acceso**  
 Seleccione cómo se especifica el nombre de archivo. Seleccione **Nombre de archivo** para escribir el nombre de archivo y la ruta de acceso directamente o **Nombre de archivo de la variable** para especificar una variable que contiene el nombre de archivo.  
  
 **Nombre de archivo** o **Nombre de variable**  
 Escriba el nombre y la ruta de acceso del archivo sin formato o seleccione la variable que contiene el nombre de archivo.  
  
 **Opción de escritura**  
 Seleccione el método que va a utilizar para crear y escribir en el archivo.  
  
 **Generar un archivo sin formato inicial**  
 Haga clic en el botón para generar un archivo sin formato vacío que contenga solo las columnas (solo archivos de metadatos), sin tener que ejecutar el paquete. Puede designar el origen de archivo sin formato para el archivo que solo tiene metadatos.  
  
 Al hacer clic en el botón, aparece una lista de columnas. Puede hacer clic en Cancelar y modificar las columnas, o hacer clic en Aceptar y continuar con la creación del archivo.  
  
###  <a name="mapping"></a> Establecer las opciones de la pestaña Columnas  
 **Columnas de entrada disponibles**  
 Seleccione una o varias columnas de entrada para escribir en el archivo sin formato.  
  
 **Columna de entrada**  
 Una columna de entrada se agrega automáticamente a esta tabla cuando se selecciona en **Columnas de entrada disponibles**, o puede seleccionar la columna de entrada directamente en esta tabla.  
  
 **Alias de salida**  
 Especifique un nombre alternativo para usarlo en la columna de salida.  
  
## <a name="see-also"></a>Consulte también  
 [Origen de archivo sin formato](../../integration-services/data-flow/raw-file-source.md)   
 [Flujo de datos](../../integration-services/data-flow/data-flow.md)  
  
  
