---
title: Procesar inserciones, actualizaciones y eliminaciones | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- incremental load [Integration Services],processing data
ms.assetid: 13a84d21-2623-4efe-b442-4125a7a2d690
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 20a8e6b8a2850d135c10ebf487c8f8e37114dc12
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/12/2018
ms.locfileid: "35400477"
---
# <a name="process-inserts-updates-and-deletes"></a>Procesar inserciones, actualizaciones y eliminaciones
  En el flujo de datos de un paquete de Integration Services que realiza una carga incremental de datos modificados, la segunda tarea consiste en separar las inserciones, las actualizaciones y las eliminaciones. A continuación, puede utilizar los comandos adecuados para aplicarlos en el destino.  
  
> [!NOTE]  
>  La primera tarea para diseñar el flujo de datos de un paquete que realiza una carga incremental de datos modificados consiste en configurar el componente de origen que ejecuta la consulta que recupera dichos datos. Para obtener más información sobre este componente, vea [Recuperar y describir datos modificados](../../integration-services/change-data-capture/retrieve-and-understand-the-change-data.md). Para obtener una descripción del proceso general de creación de un paquete que realiza una carga incremental de los datos modificados, vea [Captura de datos modificados &#40;SSIS&#41;](../../integration-services/change-data-capture/change-data-capture-ssis.md).  
  
## <a name="associating-friendly-values-to-separate-inserts-updates-and-deletes"></a>Asociar valores descriptivos para separar las inserciones, las actualizaciones y las eliminaciones  
 En la consulta de ejemplo que recupera los datos modificados, la función **cdc.fn_cdc_get_net_changes__<capture_instance>** solo devuelve la columna de metadatos denominada **__$operation**. Esta columna de metadatos contiene un valor ordinal que indica la operación que ha causado el cambio.  
  
> [!NOTE]  
>  Para obtener más información sobre la consulta que usa llamadas a la función **cdc.fn_cdc_get_net_changes_ <capture_instance>**, vea [Crear la función para recuperar los datos modificados](../../integration-services/change-data-capture/create-the-function-to-retrieve-the-change-data.md).  
  
 Hacer coincidir un valor ordinal con su operación correspondiente no es tan fácil como utilizar una tecla de acceso para la operación. Por ejemplo, 'D' puede representar fácilmente una operación de eliminación e 'I' una operación de inserción. La consulta de ejemplo que se creó en el tema, [Crear la función para recuperar los datos modificados](../../integration-services/change-data-capture/create-the-function-to-retrieve-the-change-data.md)realiza esta conversión de un valor ordinal a un valor de cadena descriptivo que se devuelve en una nueva columna. El segmento de código siguiente muestra esta conversión:  
  
```sql
select   
    ...  
    case __$operation  
        when 1 then 'D'  
        when 2 then 'I'  
        when 4 then 'U'  
        else null  
     end as CDC_OPERATION  
```  
  
## <a name="configuring-a-conditional-split-transformation-to-direct-inserts-updates-and-deletes"></a>Configurar una transformación División condicional para dirigir las inserciones, las actualizaciones y las eliminaciones  
 La transformación División condicional es idónea para dirigir filas de datos modificados a una de las tres salidas. La transformación comprueba el valor de la columna **CDC_OPERATION** en cada fila y determina si el cambio fue una inserción, una actualización o una eliminación.  
  
> [!NOTE]  
>  La columna CDC_OPERATION contiene un valor de cadena descriptivo derivado del valor numérico de la columna **__$operation** .  
  
#### <a name="to-split-inserts-updates-and-deletes-for-processing-by-using-a-conditional-split-transformation"></a>Para dividir las inserciones, las actualizaciones y las eliminaciones para su procesamiento mediante una transformación División condicional  
  
1.  En la pestaña **Flujo de datos** , agregue una transformación División condicional.  
  
2.  Conecte la salida del origen de OLE DB a la transformación División condicional.  
  
3.  En el **Editor de transformación División condicional**, en el panel inferior del editor, escriba las tres líneas siguientes para designar las tres salidas.  
  
    1.  Para las inserciones, escriba una línea con la condición `CDC_OPERATION == "I"` que dirija las filas insertadas a la salida.  
  
    2.  Para las actualizaciones, escriba una línea con la condición `CDC_OPERATION == "U"` que dirija las filas actualizadas a la salida.  
  
    3.  Para las eliminaciones, escriba una línea con la condición `CDC_OPERATION == "D"` que dirija las filas eliminadas a la salida.  
  
## <a name="next-step"></a>Paso siguiente  
 Una vez divididas las filas para su procesamiento, el paso siguiente consiste en aplicar los cambios en el destino.  
  
 **Tema siguiente:** [Aplicar los cambios al destino](../../integration-services/change-data-capture/apply-the-changes-to-the-destination.md)  
  
## <a name="see-also"></a>Ver también  
 [Transformación División condicional](../../integration-services/data-flow/transformations/conditional-split-transformation.md)   
 [División de un conjunto de datos con la transformación División condicional](../../integration-services/data-flow/transformations/split-a-dataset-by-using-the-conditional-split-transformation.md)  
  
  
