---
title: Definir los datos de un origen de vista (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- names [Analysis Services], data source views
- name matching criteria [Analysis Services]
- Data Source View Wizard
- data source views [Analysis Services], creating
ms.assetid: 0bae4ee4-1742-40e9-bebe-17c788854484
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0d80a58d33cd6475940afaf08de2d251c5646bec
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66075400"
---
# <a name="defining-a-data-source-view-analysis-services"></a>Definir una vista del origen de datos (Analysis Services)
  Una vista del origen de datos contiene el modelo lógico del esquema utilizado por [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] base de datos multidimensional objetos a saber, cubos, dimensiones y estructuras de minería de datos. Una vista del origen de datos es la definición de metadatos, almacenada en formato XML, de estos elementos de esquema que utilizan el modelo UDM (Unified Dimensional Model) y las estructuras de minería de datos. Una vista del origen de datos:  
  
-   Contiene los metadatos que representan objetos seleccionados de uno o varios orígenes de datos subyacentes, o los metadatos que se usarán para generar un almacén de datos relacional subyacente si emplea el enfoque de arriba abajo para la generación de esquemas.  
  
-   Se puede generar con uno o más orígenes de datos, lo que permite definir objetos multidimiensionales y de minería de datos que integren datos de varios orígenes.  
  
-   Puede contener relaciones, claves principales, nombres de objeto, columnas calculadas y consultas que no están presentes en un origen de datos subyacente y que son independientes de los orígenes de datos subyacentes.  
  
-   No está visible ni disponible para que las aplicaciones cliente realicen consultas.  
  
 Una DSV es un componente necesario de un modelo multidimensional. La mayoría de los desarrolladores de Analysis Services crean una DSV durante las fases iniciales de diseño de los modelos, y generan al menos una DSV basada en una base de datos relacional externa que proporciona los datos subyacentes. Sin embargo, también puede crear la DSV en una fase posterior, generando las estructuras de esquema y de base de datos subyacente una vez creadas las dimensiones y los cubos. En ocasiones, este segundo método se denomina diseño de arriba abajo y se usa a menudo para crear prototipos y modelos de análisis. Cuando se emplea este método, se usa el Asistente para generar esquemas con el fin de crear la vista del origen de datos y los objetos de origen de datos subyacentes basados en los objetos OLAP definidos en un proyecto o base de datos de Analysis Services. Independientemente de cómo y cuándo se cree una DSV, cada modelo debe tener una para que se pueda procesar.  
  
 En este tema se incluyen las secciones siguientes:  
  
 [Composición de la vista del origen de datos](#bkmk_dsvdef)  
  
 [Crear una DSV mediante el Asistente para vistas del origen de datos](#bkmk_startWiz)  
  
 [Especificar criterios de coincidencia de nombres para las relaciones](#bkmk_NameMatch)  
  
 [Agregar un origen de datos secundario](#bkmk_secondaryDS)  
  
##  <a name="bkmk_dsvdef"></a> Composición de la vista del origen de datos  
 Una vista del origen de datos se compone de los siguientes elementos:  
  
-   Un nombre y una descripción.  
  
-   Una definición de cualquier subconjunto del esquema recuperado de uno o varios orígenes de datos que incluye el esquema completo, y que tiene todo lo que se indica a continuación:  
  
    -   Nombres de tabla.  
  
    -   Nombres de columna.  
  
    -   Tipos de datos.  
  
    -   Nulabilidad  
  
    -   Longitudes de columna.  
  
    -   Claves principales.  
  
    -   Relaciones entre claves principales y claves externas.  
  
-   Anotaciones en el esquema de los orígenes de datos subyacentes, que incluyen lo que se indica a continuación:  
  
    -   Nombres descriptivos de tablas, vistas y columnas.  
  
    -   Consultas con nombre que devuelven columnas de uno o varios orígenes de datos (que se muestran como tablas en el esquema).  
  
    -   Cálculos con nombre que devuelven columnas de un origen de datos (que se muestran como columnas en las tablas o vistas).  
  
    -   Claves principales lógicas (necesarias si no hay una clave principal definida en la tabla subyacente o no se incluye en la vista o consulta con nombre).  
  
    -   Relaciones entre claves principales lógicas y claves externas entre tablas, vistas y consultas con nombre.  
  
##  <a name="bkmk_startWiz"></a> Crear una DSV mediante el Asistente para vistas del origen de datos  
 Para crear una DSV, ejecute el Asistente para vistas del origen de datos desde el Explorador de soluciones en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
> [!NOTE]  
>  O bien, puede crear dimensiones y cubos en primer lugar, y generar después una DSV para el modelo utilizando el Asistente para generar esquemas. Para más información, vea [Asistente para generar esquemas &#40;Analysis Services&#41;](schema-generation-wizard-analysis-services.md).  
  
1.  En el Explorador de soluciones, haga clic con el botón derecho en la carpeta Vistas del origen de datos y, después, haga clic en **Nueva vista del origen de datos**.  
  
2.  Especifique un objeto de origen de datos nuevo o existente que proporcione información de conexión a una base de datos relacional externa (solo se puede seleccionar un origen de datos en el asistente).  
  
3.  En la misma página, haga clic en **Avanzadas** para elegir determinados esquemas, aplicar un filtro o excluir información de relaciones entre tablas.  
  
     **Elegir esquemas**  
  
     En el caso de orígenes de datos muy grandes que contienen varios esquemas, puede seleccionar qué esquemas desea utilizar en una lista delimitada por comas, sin espacios en blanco.  
  
     **Recuperar relaciones**  
  
     Puede omitir deliberadamente la información de relaciones entre tablas si desactiva la casilla **Recuperar relaciones** en el cuadro de diálogo Opciones avanzadas de la vista del origen de datos, lo que le permite crear manualmente las relaciones entre las tablas en el Diseñador de vistas del origen de datos.  
  
4.  **Filtrar objetos disponibles**  
  
     Si la lista de objetos disponibles contiene un gran número de objetos, puede reducir su tamaño aplicando un filtro sencillo que especifique una cadena como criterio de selección. Por ejemplo, si escribe **dbo** y hace clic en el botón **Filtro** , en la lista **Objetos disponibles** solo se mostrarán los elementos que empiecen por "dbo". El filtro puede ser una cadena parcial (por ejemplo, "sal" devuelve saldo y salario) pero no puede incluir varias cadenas ni operadores.  
  
5.  Para los orígenes de datos relacionales que no tienen definidas relaciones entre tablas, aparece una página **Coincidencia de nombres** para que seleccione el método de coincidencia de nombres adecuado. Para obtener más información, vea la sección [Especificar criterios de coincidencia de nombres para las relaciones](#bkmk_NameMatch) en este tema.  
  
##  <a name="bkmk_secondaryDS"></a> Agregar un origen de datos secundario  
 Al definir una vista del origen de datos con tablas, vistas o columnas de varios orígenes de datos, el primer origen de datos desde el que agrega objetos a la vista del origen de datos se designa como origen de datos principal (una vez que se ha definido, no se puede cambiar). Después de definir una vista del origen de datos basada en objetos de un solo origen de datos, puede agregar objetos de otros orígenes de datos.  
  
 Si una consulta de procesamiento OLAP o de minería de datos requiere datos de varios orígenes de datos en una sola consulta, el origen de datos principal debe admitir consultas remotas mediante `OpenRowset`. Normalmente, será un origen de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Por ejemplo, si designa una dimensión OLAP que contenga atributos enlazados a columnas de varios orígenes de datos, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] generará una consulta `OpenRowset` para llenar esta dimensión durante el procesamiento. Sin embargo, si un objeto OLAP se puede llenar o una consulta de minería de datos se puede resolver desde un solo origen de datos, no se creará una consulta `OpenRowset`. En ciertas situaciones, podría definir relaciones de atributo entre atributos para que no sea necesaria una consulta `OpenRowset`. Para más información sobre las relaciones de atributos, vea [Relaciones de atributos](../multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md), [Agregar o quitar tablas o vistas en una vista del origen de datos &#40;Analysis Services&#41;](adding-or-removing-tables-or-views-in-a-data-source-view-analysis-services.md) y [Definir relaciones de atributo](attribute-relationships-define.md).  
  
 Para agregar tablas y columnas de un segundo origen de datos, haga doble clic en la DSV en el Explorador de soluciones para abrirla en el Diseñador de vistas del origen de datos y, a continuación, use el cuadro de diálogo Agregar o quitar tablas para incluir objetos de otros orígenes de datos que estén definidos en el proyecto. Para más información, vea [Agregar o quitar tablas o vistas en una vista del origen de datos &#40;Analysis Services&#41;](adding-or-removing-tables-or-views-in-a-data-source-view-analysis-services.md).  
  
##  <a name="bkmk_NameMatch"></a> Especificar criterios de coincidencia de nombres para las relaciones  
 Cuando se crea una DSV, se crean relaciones entre las tablas basadas en las restricciones de clave externa del origen de datos. Estas relaciones son necesarias para que el motor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] genere las consultas adecuadas de minería de datos y de procesamiento OLAP. A veces, sin embargo, el origen de datos tiene varias tablas que no tienen restricciones de clave externa. Si el origen de datos no tiene restricciones de clave externa, el Asistente para vistas del origen de datos le pide que defina el modo en que desea que el asistente trate de hacer coincidir los nombres de columna de las diferentes tablas.  
  
> [!NOTE]  
>  Solo se solicitan criterios de coincidencia de nombres si no se detectan relaciones de clave externa en el origen de datos subyacente. Si se detectan relaciones de clave externa, se usan dichas relaciones y se debe definir manualmente cualquier relación adicional que se desee incluir en la DSV, incluidas las claves principales lógicas. Para más información, vea [Definir relaciones lógicas en una vista del origen de datos &#40;Analysis Services&#41;](define-logical-relationships-in-a-data-source-view-analysis-services.md) y [Definir claves principales lógicas en una vista del origen de datos &#40;Analysis Services&#41;](define-logical-primary-keys-in-a-data-source-view-analysis-services.md).  
  
 El Asistente para vistas del origen de datos usa la respuesta para hacer coincidir los nombres de columna y crear relaciones entre las diferentes tablas de la DSV. Puede especificar cualquiera de los criterios que se enumeran en la siguiente tabla.  
  
|Criterios de coincidencia de nombres|Descripción|  
|----------------------------|-----------------|  
|**Mismo nombre que el de la clave principal**|El nombre de la columna de clave externa de la tabla de origen es igual que el nombre de la columna de clave principal de la tabla de destino. Por ejemplo, la columna de clave externa `Order.CustomerID` es igual que la columna de clave principal `Customer.CustomerID`.|  
|**Mismo nombre que el nombre de tabla de destino**|El nombre de la columna de clave externa de la tabla de origen es igual que el nombre de la tabla de destino. Por ejemplo, la columna de clave externa `Order.Customer` es igual que la columna de clave principal `Customer.CustomerID`.|  
|**Nombre de la tabla de destino + nombre de la clave principal**|El nombre de la columna de clave externa en la tabla de origen es igual que el nombre de la tabla de destino concatenado con el nombre de la columna de clave principal. Se admite un espacio o un carácter de subrayado como separador. Por ejemplo, los siguientes pares de clave externa y principal coinciden:<br /><br /> `Order.CustomerID` y `Customer.ID`<br /><br /> `Order.Customer ID` y `Customer.ID`<br /><br /> `Order.Customer_ID` y `Customer.ID`|  
  
 El criterio seleccionado cambia la configuración de la propiedad **NameMatchingCriteria** de la DSV. Esta configuración determina cómo agrega el asistente las tablas relacionadas. Cuando se cambia la vista del origen de datos con el Diseñador de vistas del origen de datos, esta especificación determina el modo en que el diseñador hace coincidir las columnas para crear relaciones entre las tablas de la DSV. Puede cambiar la configuración de la propiedad **NameMatchingCriteria** en el Diseñador de vistas del origen de datos. Para más información, vea [Cambiar las propiedades de una vista del origen de datos &#40;Analysis Services&#41;](change-properties-in-a-data-source-view-analysis-services.md).  
  
> [!NOTE]  
>  Cuando complete el Asistente para vistas del origen de datos, puede agregar o quitar relaciones en el panel de esquema del Diseñador de vistas del origen de datos. Para más información, vea [Definir relaciones lógicas en una vista del origen de datos &#40;Analysis Services&#41;](define-logical-relationships-in-a-data-source-view-analysis-services.md).  
  
## <a name="see-also"></a>Vea también  
 [Agregar o quitar tablas o vistas en una vista del origen de datos &#40;Analysis Services&#41;](adding-or-removing-tables-or-views-in-a-data-source-view-analysis-services.md)   
 [Definir claves principales lógicas en una vista del origen de datos &#40;Analysis Services&#41;](define-logical-primary-keys-in-a-data-source-view-analysis-services.md)   
 [Definir cálculos con nombre en una vista del origen de datos &#40;Analysis Services&#41;](define-named-calculations-in-a-data-source-view-analysis-services.md)   
 [Definir consultas con nombre en una vista del origen de datos &#40;Analysis Services&#41;](define-named-queries-in-a-data-source-view-analysis-services.md)   
 [Reemplazar una tabla o una consulta con nombre en una vista del origen de datos &#40;Analysis Services&#41;](replace-a-table-or-a-named-query-in-a-data-source-view-analysis-services.md)   
 [Trabajar con diagramas en el Diseñador de vistas del origen de datos &#40;Analysis Services&#41;](work-with-diagrams-in-data-source-view-designer-analysis-services.md)   
 [Explorar datos en una vista del origen de datos &#40;Analysis Services&#41;](explore-data-in-a-data-source-view-analysis-services.md)   
 [Eliminar una vista del origen de datos &#40;Analysis Services&#41;](delete-a-data-source-view-analysis-services.md)   
 [Actualizar el esquema de una vista del origen de datos &#40;Analysis Services&#41;](refresh-the-schema-in-a-data-source-view-analysis-services.md)  
  
  
