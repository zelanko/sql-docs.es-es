---
title: Propiedades de columna (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.columnprop.f1
ms.assetid: 4046c1a3-46c7-47db-b355-52e9c2f23671
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0bb076297af4e666513a0c5b86d6783b7c245c00
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48072425"
---
# <a name="column-properties-ssas-tabular"></a>Pestaña Propiedades de columna (SSAS tabular)
  En este tema se describen las propiedades de columna del modelo tabular.  
  
 Secciones de este tema:  
  
-   [Propiedades de columna](#bkmk_properties)  
  
-   [Para configurar los valores de propiedad de columna](#bkmk_config_prop)  
  
##  <a name="bkmk_properties"></a> Propiedades de columna  
 **Basic**  
  
|Property|Valor predeterminado|Descripción|  
|--------------|---------------------|-----------------|  
|**Nombre de la columna**||El nombre de la columna como se almacena en el modelo y como se muestra en una lista de campos del cliente de informes.|  
|**Formato de datos**|Se determina automáticamente durante la importación.|Especifica el formato de presentación que se debe utilizar para los datos de esta columna. Después de establecer un formato de datos, puede establecer propiedades que son específicas de cada formato. Por ejemplo, si elige el formato de **Moneda** , puede establecer el número de posiciones decimales visibles, elegir el separador de miles y seleccionar el símbolo de moneda. Esta propiedad tiene las opciones siguientes:<br /><br /> **General**<br /><br /> **Decimal Number**<br /><br /> **Whole Number**<br /><br /> **Moneda**<br /><br /> **Porcentaje**<br /><br /> **Científico**<br /><br /> Si los valores de columna contienen imágenes, vea **Imagen representativa**.|  
|**Tipo de datos**|Se determina automáticamente durante la importación.|Especifica el tipo de datos de todos los valores de la columna.|  
|**Descripción**||Una descripción de texto de la columna.<br /><br /> En determinados clientes de informes, si un usuario final coloca el cursor sobre esta columna en la lista de campos, aparece la descripción como una información sobre herramientas.|  
|**Oculto**|False|Especifica si la columna se oculta en las listas de campos del cliente de informes.<br /><br /> Establezca esta propiedad en **True** para ocultar esta columna de la presentación. Por ejemplo, las columnas que contienen identificadores o claves normalmente no son útiles para el usuario final.<br /><br /> Si oculta una columna del cliente de informes, el campo no se suprime en los datos del modelo. El campo todavía está visible si crea una consulta en el modelo. Una columna oculta todavía se puede utilizar para agrupar u ordenar.<br /><br /> La propiedad **Hidden** no proporciona ningún método de seguridad para los datos. Para proteger los datos, utilice filtros de fila en roles. Para obtener más información, vea [Roles &#40;SSAS Tabular&#41;](roles-ssas-tabular.md).|  
|**Ordenar por columna**||Especifica otra columna por la que ordenar los valores de esta columna. Debe existir una relación entre las dos columnas.<br /><br /> Este valor debe ser el nombre de una columna existente. No puede especificar ninguna fórmula o medida.|  
  
 **Propiedades de informes**  
  
 Para más información sobre cómo configurar las propiedades de comportamiento de una tabla de [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], vea [Configurar las propiedades de comportamiento de las tablas para informes de Power View &#40;SSAS tabular&#41;](power-view-configure-table-behavior-properties-for-reports.md).  
  
|Property|Valor predeterminado|Descripción|  
|--------------|---------------------|-----------------|  
|Imagen predeterminada|False|Especifica qué columna proporciona una imagen que representará los datos de fila (por ejemplo, un carnet con fotografía en un registro del empleado).|  
|Etiqueta predeterminada|False|Especifica qué columna proporciona un nombre para mostrar que representará los datos de fila (por ejemplo, el nombre de empleado en un registro del empleado).|  
|Dirección URL de imagen/Categoría de datos (SP1)|False|Especifica el valor de esta columna como un hipervínculo a una imagen de un servidor. Por ejemplo: http://localhost/images/image1.jpg.|  
|Mantener filas únicas|False|Especifica qué columnas proporcionan valores que se deben tratar como únicos aunque estén duplicados (por ejemplo, nombre y apellidos del empleado para los casos en que dos o varios empleados compartan el mismo nombre).|  
|Identificador de fila|False|Especifica una columna que contiene solo valores únicos, lo que permite usarla como clave interna de agrupación.|  
|Resumir por|Default|Especifica las herramientas de cliente de generación de informes que se aplican a la función de agregado SUM para cálculos de columnas cuando esta columna se agrega a una lista de campos. Para cambiar el cálculo predeterminado, selecciónelo en la lista desplegable. Esta propiedad solo se aplica a las columnas de tipo que se pueden agregar.|  
|Posición de detalles de la tabla|Ningún conjunto de campos predeterminado|Especifica que esta columna o medida se puede agregar a un conjunto de campos de una tabla para mejorar la experiencia de visualización de la misma en un cliente de informes.|  
  
###  <a name="bkmk_config_prop"></a> Para configurar los valores de propiedad de columna  
  
1.  En el diseñador de modelos, en una tabla, seleccione una columna.  
  
2.  En la ventana **Propiedades** , haga clic en una propiedad y, a continuación, escriba un valor o haga clic en la flecha abajo para seleccionar una opción de configuración.  
  
## <a name="see-also"></a>Vea también  
 [Power ver propiedades de informes &#40;Tabular de SSAS&#41;](properties-ssas-tabular.md)   
 [Ocultar o Inmovilizar columnas &#40;Tabular de SSAS&#41;](hide-or-freeze-columns-ssas-tabular.md)   
 [Agregar columnas a una tabla &#40;Tabular de SSAS&#41;](add-columns-to-a-table-ssas-tabular.md)  
  
  
