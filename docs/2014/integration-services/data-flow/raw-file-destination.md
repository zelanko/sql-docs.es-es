---
title: Destino de archivo sin formato | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.rawfiledest.f1
helpviewer_keywords:
- append options [Integration Services]
- destinations [Integration Services], Raw File
- raw data [Integration Services]
- writing raw data
- Raw File destination
ms.assetid: d311b458-aefc-4b4d-b1a1-4c0ebbb34214
author: janinezhang
ms.author: janinez
ms.openlocfilehash: bf4d31a05977cc34cf9aaee8fff38867aa302f37
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84914816"
---
# <a name="raw-file-destination"></a>destino de archivo sin formato
  El destino de archivo sin formato escribe datos sin procesar en un archivo. Como el formato de los datos es el nativo del destino, no es necesario traducir los datos y prácticamente no es necesario analizar el archivo. Esto significa que el destino de archivo sin formato puede escribir datos más rápidamente que otros destinos, como el destino de archivo plano o los destinos de OLE DB.  
  
 Además de escribir datos sin procesar en un archivo, puede utilizar el destino de archivo sin formato para generar un archivo sin formato vacío que contenga solo las columnas (archivo solo para metadatos), sin tener que ejecutar el paquete. El origen de archivo sin formato se usa para recuperar datos sin formato escritos previamente por el destino. Puede también designar el origen de archivo sin formato para el archivo que solo tiene metadatos.  
  
 El archivo sin formato contiene información sobre el orden. El destino de archivo sin formato guarda toda la información sobre el orden incluidas las marcas de comparación para las columnas de cadena. El origen de archivo sin formato lee y respeta la información sobre el orden. Tiene la opción de configurar el origen de archivo sin formato para omitir los marcas de orden en el archivo; para ello use el Editor avanzado. Para obtener más información acerca de las marcas de comparación, vea [Comparing String Data](comparing-string-data.md).  
  
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
|Append|Anexa datos a un archivo existente. Los metadatos de los datos anexados deben coincidir con el formato del archivo.|  
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
  
2.  Restablezca la propiedad WriteOption en **Append** y establezca la propiedad ValidateExternalMetadata en `False` .  
  
 Si usa la opción **TruncateAppend** en lugar de la opción **Append** , truncará las filas que se agregaron en toda iteración anterior y anexará filas nuevas. Con la opción **TruncateAppend** también es necesario que los datos tengan el mismo formato que el archivo.  
  
## <a name="configuration-of-the-raw-file-destination"></a>Configuración del destino de archivo sin formato  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Common Properties](../common-properties.md)  
  
-   [Propiedades personalizadas de archivo sin formato](raw-file-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obtener información sobre cómo establecer las propiedades del componente, vea [Establecer las propiedades de un componente de flujo de datos](set-the-properties-of-a-data-flow-component.md).  
  
## <a name="related-content"></a>Contenido relacionado  
 Entrada del blog, sobre los [archivos sin formato](https://www.sqlservercentral.com/blogs/31-days-of-ssis-%e2%80%93-raw-files-are-awesome-131), en sqlservercentral.com  
  
## <a name="see-also"></a>Consulte también  
 [Origen de archivo sin formato](raw-file-source.md)   
 [Flujo de datos](data-flow.md)  
  
  
