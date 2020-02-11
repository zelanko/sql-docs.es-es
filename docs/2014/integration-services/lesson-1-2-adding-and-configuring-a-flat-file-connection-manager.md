---
title: 'Paso 2: Agregar y configurar un administrador de conexiones de archivos planos | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 9a77dd32-d8c2-4961-ad37-2a971f9d6043
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0c6cd41be722d80baf442db907d6fdab9f334859
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62891800"
---
# <a name="step-2-adding-and-configuring-a-flat-file-connection-manager"></a>Paso 2: agregar y configurar un administrador de conexiones de archivos planos
  En esta tarea, agregará un administrador de conexiones de archivos planos al paquete que acaba de crear. Un administrador de conexiones de archivos planos permite a un paquete extraer datos de un archivo plano. Mediante el administrador de conexiones de archivos planos puede especificar el nombre y la ubicación del archivo, la configuración regional y la página de códigos, y el formato del archivo, incluyendo los delimitadores de columna, que deben aplicarse cuando el paquete extrae datos del archivo plano. Además, puede especificar de forma manual el tipo de datos para columnas individuales, o usar el cuadro de diálogo **Sugerir tipos de columna** para asignar de forma automática las columnas de datos extraídos a los tipos de datos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
 Debe crear un administrador de conexiones de archivos planos para cada formato de archivo que utilice. En este tutorial se extraen datos de varios archivos planos que tienen exactamente el mismo formato de datos, por lo que tendrá que agregar y configurar solamente un administrador de conexiones de archivos planos para el paquete.  
  
 En este tutorial, configurará las propiedades siguientes en el administrador de conexiones de archivos planos:  
  
-   **Nombres de columna:** Dado que el archivo plano no tiene nombres de columna, el administrador de conexiones de archivos planos crea nombres de columna predeterminados. Estos nombres predeterminados no son útiles para identificar qué representa cada columna. Para que estos nombres predeterminados sean más útiles, debe cambiar los nombres predeterminados por nombres que coincidan con la tabla de hechos en la que deben cargarse los datos del archivo plano.  
  
-   **Asignaciones de datos:** Todas las asignaciones de tipos de datos que especifique para el administrador de conexiones de archivos planos se utilizarán en todos los componentes de origen de datos de archivo plano que hagan referencia al administrador de conexiones. Puede asignar los tipos de datos de forma manual mediante el administrador de conexiones de archivos planos o usar el cuadro de diálogo **Sugerir tipos de columna** . En este tutorial, verá las asignaciones sugeridas en el cuadro de diálogo **Sugerir tipos de columna** y luego realizará de forma manual las asignaciones necesarias en el cuadro de diálogo **Editor del administrador de conexiones de archivos planos** .  
  
 El administrador de conexiones de archivos planos proporciona información de configuración regional acerca del archivo de datos. Si el equipo no está configurado para usar la opción regional inglés (Estados Unidos), debe establecer propiedades adicionales en el cuadro de diálogo **Editor del administrador de conexiones de archivos planos** .  
  
### <a name="to-add-a-flat-file-connection-manager-to-the-ssis-package"></a>Para agregar un administrador de conexiones de archivos planos al paquete SSIS  
  
1.  Haga clic con el botón derecho en cualquier punto del área **Administradores de conexión** y luego haga clic en **Nueva conexión de archivos planos**.  
  
2.  En el cuadro de diálogo **Editor del administrador de conexiones de archivos planos** , en **Nombre del administrador de conexiones**, escriba **Sample Flat File Source Data**.  
  
3.  Haga clic en **Examinar**.  
  
4.  En el cuadro de diálogo **Abrir** , busque el archivo SampleCurrencyData.txt en el equipo.  
  
     Los datos de ejemplo se incluyen con los paquetes de lecciones de [!INCLUDE[ssIS](../includes/ssis-md.md)] . Para descargar los datos de ejemplo y los paquetes de lecciones, haga lo siguiente.  
  
    1.  Vaya a [Integration Services ejemplos de productos](https://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  Haga clic en la pestaña **descargas** .  
  
    3.  Haga clic en el archivo SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip.  
  
5.  Borre los nombres de columna de la primera casilla de fila de datos.  
  
### <a name="to-set-locale-sensitive-properties"></a>Para establecer las propiedades dependientes de la configuración regional  
  
1.  En el cuadro de diálogo **Editor del administrador de conexiones de archivos planos** , haga clic en **General**.  
  
2.  Establezca **configuración regional** en inglés (Estados Unidos) y **Página de códigos** en 1252.  
  
### <a name="to-rename-columns-in-the-flat-file-connection-manager"></a>Para cambiar el nombre de las columnas del administrador de conexiones de archivos planos  
  
1.  En el cuadro de diálogo **Editor del administrador de conexiones de archivos planos** , haga clic en **Avanzadas**.  
  
2.  En el panel de propiedades, realice los cambios siguientes:  
  
    -   Cambie la propiedad nombre de **columna 0** a `AverageRate`.  
  
    -   Cambie la propiedad **columna 1** nombre a `CurrencyID`.  
  
    -   Cambie la propiedad **columna 2** nombre a `CurrencyDate`.  
  
    -   Cambie la propiedad **columna 3** nombre a `EndOfDayRate`.  
  
    > [!NOTE]  
    >  De forma predeterminada, las cuatro columnas están inicialmente establecidas en el tipo de datos de cadena [DT_STR] con `OutputColumnWidth` con el valor 50.  
  
### <a name="to-remap-column-data-types"></a>Para volver a asignar tipos de datos de columna  
  
1.  En el cuadro de diálogo **Editor del administrador de conexiones de archivos planos** , haga clic en **Sugerir tipos**.  
  
     
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] sugiere de forma automática los tipos de datos más adecuados en función de las 200 primeras filas de datos. También puede cambiar estas opciones de sugerencia para obtener más o menos datos de ejemplo, especificar el tipo de datos predeterminado para datos enteros o booleanos, o agregar espacios como relleno para las columnas de cadena.  
  
     De momento, no cambie las opciones del cuadro de diálogo **Sugerir tipos de columna** y haga clic en **Aceptar** para que [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] sugiera los tipos de datos para las columnas. Esto le devuelve al panel **Avanzadas** del cuadro de diálogo **Editor del administrador de conexiones de archivos planos** , donde puede ver los tipos de datos de columna sugeridos por [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. (Si hace clic en **Cancelar**, no se realizan sugerencias en los metadatos de columna y se usa el tipo de datos predeterminado de cadena [DT_STR]).  
  
     En este tutorial, [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] sugiere los tipos de datos que se muestran en la segunda columna de la siguiente tabla para los datos del archivo SampleCurrencyData.txt. No obstante, los tipos de datos que se requieren para las columnas en el destino, que se definirán en un paso posterior, se muestran en la última columna de la tabla siguiente.  
  
    |Columna de archivo plano|Tipo sugerido|Columna de destino|Tipo de destino|  
    |----------------------|--------------------|------------------------|----------------------|  
    |AverageRate|float [DT_R4]|FactCurrency.AverageRate|FLOAT|  
    |CurrencyID|string [DT_STR]|DimCurrency,CurrencyAlternateKey|nchar(3)|  
    |CurrencyDate|date [DT_DATE]|DimDate.FullDateAlternateKey|date|  
    |EndOfDayRate|float [DT_R4]|FactCurrency.EndOfDayRate|FLOAT|  
  
     El tipo de datos sugerido para `CurrencyID` la columna no es compatible con el tipo de datos del campo en la tabla de destino. Dado que el tipo de `DimCurrency.CurrencyAlternateKey` datos de es NCHAR (3 `CurrencyID` ), debe cambiarse de la cadena [DT_STR] a la cadena [DT_WSTR]. Además, el campo `DimDate.FullDateAlternateKey` se define como un tipo de datos de fecha; por lo `CurrencyDate` tanto, debe cambiarse de la fecha [DT_Date] a la fecha de la base de datos [DT_DBDATE].  
  
2.  En la lista, seleccione la columna CurrencyID y, en el panel de propiedades, cambie el tipo de `CurrencyID` datos de la columna de cadena [DT_STR] a cadena Unicode [DT_WSTR].  
  
3.  En el panel de propiedades, cambie el tipo de datos `CurrencyDate` de la columna de fecha [DT_DATE] a fecha de base de datos [DT_DBDATE].  
  
4.  Haga clic en **OK**.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Paso 3: agregar y configurar un administrador de conexiones OLE DB](lesson-1-3-adding-and-configuring-an-ole-db-connection-manager.md)  
  
## <a name="see-also"></a>Consulte también  
 [Administrador de conexiones de archivos planos](connection-manager/file-connection-manager.md)   
 [Tipos de datos de Integration Services](data-flow/integration-services-data-types.md)  
  
  
