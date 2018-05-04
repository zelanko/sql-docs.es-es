---
title: Propiedades de columna | Documentos de Microsoft
ms.custom: ''
ms.date: 02/21/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.asvs.bidtoolset.columnprop.f1
ms.assetid: 4046c1a3-46c7-47db-b355-52e9c2f23671
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 78fc7f81e8d4f6bfae572c0f7ff12b2e17d90e05
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="column-properties"></a>Propiedades de columna 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Este artículo describen las propiedades de columna de modelo tabular.  
  
>  [!NOTE]  
>  Algunas propiedades no se admiten en todos los niveles de compatibilidad.    
  
##  <a name="bkmk_properties"></a> Propiedades de columna  
**Avanzadas**  
  
|Propiedad|Valor predeterminado|Description|  
|--------------|---------------------|-----------------|  
|**Carpeta para mostrar**||Una carpeta única o anidada para organizar las columnas en una lista de campos de la aplicación de cliente.|  

**Básico**  
  
|Propiedad|Valor predeterminado|Description|  
|--------------|---------------------|-----------------|  
|**Nombre de la columna**||El nombre de la columna como se almacena en el modelo y como se muestra en una lista de campos del cliente de informes.|  
|**Formato de datos**|Se determina automáticamente durante la importación.|Especifica el formato de presentación que se debe utilizar para los datos de esta columna. Esta propiedad tiene las opciones siguientes:<br /><br /> **General**<br /><br /> **Decimal Number**<br /><br /> **Whole Number**<br /><br /> **Moneda**<br /><br /> **Porcentaje**<br /><br /> **Científico**<br /><br /> Después de establecer un formato de datos, puede establecer propiedades que son específicas de cada formato. Por ejemplo, si elige el formato de **Moneda** , puede establecer el número de posiciones decimales visibles, elegir el separador de miles y seleccionar el símbolo de moneda.<br /><br /> <br /><br /> Si los valores de columna contienen imágenes, vea **Imagen representativa**.|  
|**Tipo de datos**|Se determina automáticamente durante la importación.|Especifica el tipo de datos de todos los valores de la columna.|  
|**Description**||Una descripción de texto de la columna.<br /><br /> En determinados clientes de informes, si un usuario final coloca el cursor sobre esta columna en la lista de campos, aparece la descripción como una información sobre herramientas.|  
|**Oculto**|False|Especifica si la columna se oculta en las listas de campos del cliente de informes.<br /><br /> Establezca esta propiedad en **True** para ocultar esta columna de la presentación. Por ejemplo, las columnas que contienen identificadores o claves normalmente no son útiles para el usuario final.<br /><br /> Si oculta una columna del cliente de informes, el campo no se suprime en los datos del modelo. El campo todavía está visible si crea una consulta en el modelo. Una columna oculta todavía se puede utilizar para agrupar u ordenar.<br /><br /> La propiedad **Hidden** no proporciona ningún método de seguridad para los datos. Para proteger los datos, utilice filtros de fila en roles. Para obtener más información, consulte [Roles](../../analysis-services/tabular-models/roles-ssas-tabular.md).|  
|**Ordenar por columna**||Especifica otra columna por la que ordenar los valores de esta columna. Debe existir una relación entre las dos columnas.<br /><br /> Este valor debe ser el nombre de una columna existente. No puede especificar ninguna fórmula o medida.|  

 **Varios**  
  
|Propiedad|Valor predeterminado|Description|  
|--------------|---------------------|-----------------|  
|**Sugerencias de codificación**|Predeterminado|Especifica la codificación para optimizar el procesamiento. Valor codificación puede mejorar el rendimiento de las consultas para las columnas numéricas que se suelen usar en agregaciones. La codificación hash es columnas group by (a menudo valores de tabla de dimensiones) y claves externas. Las columnas de cadena siempre son hash codificado.|  

 **Propiedades de informes**  
  
|Propiedad|Valor predeterminado|Description|  
|--------------|---------------------|-----------------|  
|Imagen predeterminada|False|Especifica qué columna proporciona una imagen que representará los datos de fila (por ejemplo, un carnet con fotografía en un registro del empleado).|  
|Etiqueta predeterminada|False|Especifica qué columna proporciona un nombre para mostrar que representará los datos de fila (por ejemplo, el nombre de empleado en un registro del empleado).|  
|Dirección URL de imagen/Categoría de datos (SP1)|False|Especifica el valor de esta columna como un hipervínculo a una imagen de un servidor. Por ejemplo: `http://localhost/images/image1.jpg`.|  
|Mantener filas únicas|False|Especifica qué columnas proporcionan valores que se deben tratar como únicos aunque estén duplicados (por ejemplo, nombre y apellidos del empleado para los casos en que dos o varios empleados compartan el mismo nombre).|  
|Identificador de fila|False|Especifica una columna que contiene solo valores únicos, lo que permite usarla como clave interna de agrupación.|  
|Resumir por|Predeterminado|Especifica las herramientas de cliente de generación de informes que se aplican a la función de agregado SUM para cálculos de columnas cuando esta columna se agrega a una lista de campos. Para cambiar el cálculo predeterminado, selecciónelo en la lista desplegable. Esta propiedad solo se aplica a las columnas de tipo que se pueden agregar.|  
|Posición de detalles de la tabla|Ningún conjunto de campos predeterminado|Especifica que esta columna o medida se puede agregar a un conjunto de campos de una tabla para mejorar la experiencia de visualización de la misma en un cliente de informes.|  
  
##  <a name="bkmk_config_prop"></a> Configurar los valores de las propiedades de columna  
  
1.  En el diseñador de modelos, en una tabla, seleccione una columna.  
  
2.  En la ventana **Propiedades** , haga clic en una propiedad y, a continuación, escriba un valor o haga clic en la flecha abajo para seleccionar una opción de configuración.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades informes de Power View](../../analysis-services/tabular-models/power-view-reporting-properties-ssas-tabular.md)   
 [Ocultar o Inmovilizar columnas](../../analysis-services/tabular-models/hide-or-freeze-columns-ssas-tabular.md)   
 [Agregar columnas a una tabla](../../analysis-services/tabular-models/add-columns-to-a-table-ssas-tabular.md)  
  
  
